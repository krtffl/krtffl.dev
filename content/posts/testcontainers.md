+++
title = "testcontainers"
date = 2024-09-14
draft = true
description = "testing: the real deal"
tags = [
    "go",
    "testing",
]
categories = [
    "go",
    "testing",
    "testcontainers",
]
toc = true
+++

it was about time to start seeing some code in this (supposedly) blog that shows how i become a 10x engineer. one might start to think the fastest approach to 10x your skills is to stop writing code, but i assure you that is not the case. 

<!--more-->

the happy path for me to start showing some code is then to talk about the latest stuff i have been playing with, which turns to be **[testcontainers](https://testcontainers.com/)**. that is actually quite nice because testcontainers are the real deal. awesome. i used to hate writing integration test. now i still hate it but i am found of testcontainers. i have said it too much in this sentence no? testcontainers. testcontainers. 

i feel like andy the first time he got its buzz lightyear - now it would be awesome to add a picture to illustrate the phrase, that is something people like when reading stuff right? sadly i don't think i can stick up a frame of a pixar movie in here. you'll have to imagine it. i mean, everyone has seen toy story multiple times so it won't be hard. 

well, actually let me draw it for you because i need that you reeeally picture it and understand how cool testcontainers are. ok i swear i won't use the word anymore.

 {{< figure src="/images/andy_happy.jpg" title="andy super happy because he got buzz" width="350">}} 

i am really sorry but i needed to do that. alright, now, to have some consistency let me see how i structured the previous post... ok got it.

- what are tests?
- do we even need to test?
- why are ~~testc-~~ they cool?

### tests???

you now what tests are. the pyramid. tests are very useful, very helpful, blah, blah, blah.

### i don't want to test!!

do tests. even if you have qa. _do not ever trust a qa._ trust your code to test your code, not a person. not people. and please, not the end user.

i just want to say something brief here and is more as a reminder to me than anything else. tests really help you out and sometimes - sometimes - you won't break your prod environment thanks to a test, but they are no saving net unless you write good tests. even though.

> go ahead and write shit code, but at least do good tests. 

i can recall about 4 or 5 times where i deployed a bug into a production enviroment when i was working at adidas. we had about 75% coverage throughout the entire codebase. 

about 2 of them where breaking some functionality in our application. huge impact

- allowed users to make returns/exchanges after the exchange period
- broke the entire exchange use case 

this was worldwide. to all adidas customers. 

and as always, the fix were a couple of lines of code. it is very easy to overlook stuff.

with well-thought tests than actually tested functionality, we would have noticed it. 

### wasn't this about testcontainers?

ok so testcontainers are really cool because you can just write integration tests soooo easily. 

integration tests are the ones that save you from a call at 3AM from your boss, but so often are such a pain in the ass to write. you need the database, or a database, and to set it up... and how the hell do i do that?

> testcontainers

bascially they are gonna spin up docker containers for your dependencies so that you can run yours tests agains them, and in the end it will be like nothing happened. so, no mocks. no sqlite to test my database connections. real containers with the same images that you are running.


 {{< figure src="/images/testcontainers_flow.png" title="testcontainers workflow" width="700">}} 

and they support just a bunch of languages by the way. and also have ready to go containers for a bunch of the most common dependencies so you can just plug and play: cassandra, postgresql, kafka, minio, redis...

### testcontainers in action

i simply have a postgresql for now and i will test my repository layer for one of my entities. if you want to test a more complex setup, there is a nice post here ([integration testing using testcontainers, shaibu shaibu](https://volomn.com/blog/integration-testing-in-go-using-testcontainers)) with both a postgresql and a redis. the idea is the same. 

#### domain entities

i define my entities in my domain layer

> `internal/domain/dojo.go`

```go
type Dojo struct {
	ID          string    `json:"id"`
	Name        string    `json:"name"`
	Address     string    `json:"address,omitempty"`     // optional
	Phone       string    `json:"phone,omitempty"`       // optional
	Email       string    `json:"email,omitempty"`       // optional
	FoundedDate time.Time `json:"foundedDate,omitempty"` // optional
}

```

i like to differentiate between my domain entities and my database models, but for this simple example i will use the entity directly.

#### define interface 
```go
var (
	ErrCreateDojo = errors.New("coulnd't create dojo")
	ErrUpdateDojo = errors.New("coulnd't update dojo")
	ErrDeleteDojo = errors.New("coulnd't delete dojo")
	ErrGetDojo    = errors.New("coulnd't find dojo")
	ErrListDojos  = errors.New("coulnd't list dojos")
)

type DojoRepository interface {
	Create(entity *Dojo) (*Dojo, error)
	Update(ID string, entity *Dojo) (*Dojo, error)
	Delete(ID string) error
	Get(ID string) (*Dojo, error)
	List(filter *DojoFilter) ([]*Dojo, error)
}
```

and i define the interface that we will need to satisfy in our repositories. as i said in this case i will use a postgresql so 

#### implement repository

> `internal/infra/postgresql/dojo.go`

and as you will be familiar

```go
type DojoRepository struct {
	db *gorm.DB
}

func NewDojoRepository(
	db *gorm.DB,
) domain.DojoRepository {
	return &DojoRepository{
		db: db,
	}
}
```

and we define the methods as described in the interface. case you are wondering why am i using [gorm](https://gorm.io/), often it gives me headaches but for simple querying it is indeed really helpful.

```go
func (instance *DojoRepository) Get(entityID string) (*domain.Dojo, error) {
	var model *domain.Dojo
	if err := instance.db.
		Where("id = ?", entityID).
		First(&model).
		Error; err != nil {
		e := fmt.Errorf("%v: %v", domain.ErrGetDojo, err)
		logger.Error(e.Error())
		return nil, e
	}

	logger.Debug(
		"Fetched dojo: %+v", model)

	return model, nil
}
```

also slightly off topic but i want my repository layer to already return a mapped error, with the error identified defined in the domain as well. sometimes i just log the err details here, and return the domain error instead, but i find context is missing when the error is eventually returned to the user.

```go
func (repo *DojoRepository) List(
	filter *domain.DojoFilter,
) ([]*domain.Dojo, error) {
	var models []*domain.Dojo
	if err := manageDojoFilters(repo.db, filter).
		Order("Name").
		Find(&models).
		Error; err != nil {
		e := fmt.Errorf("%v: %v", domain.ErrListDojos, err)
		logger.Error(e.Error())
		return nil, e
	}

	logger.Debug("Fetched %d dojos with %+v", len(models), filter)
	return models, nil
}
```

the order could be handled differently but who cares. and in case you want to see the function that manages the filters, it is pretty straightforward

```go
func manageDojoFilters(query *gorm.DB, filter *domain.DojoFilter) *gorm.DB {
	if strings.TrimSpace(filter.Name) != "" {
		query = query.Where("dojos.name = ?", filter.Name)
	}

	return query
}
```

for this scenario it doesn't really matter but lately i've been following this approach where i define a struct with the fields which can be filtered, and then apply them programmatically when their values are not null. 

```go
func (repo *DojoRepository) Create(entity *domain.Dojo) (
    *domain.Dojo, error) {
	if err := repo.db.Create(&entity).Error; err != nil {
		e := fmt.Errorf("%v: %v", domain.ErrCreateDojo, err)
		logger.Error(e.Error())
		return nil, e
	}

	logger.Debug(
		"Dojo created: %+v", entity)

	return entity, nil
}
```
```go
func (repo *DojoRepository) Update(
	entityID string,
	entity *domain.Dojo,
) (*domain.Dojo, error) {
	var model *domain.Dojo
	if err := repo.db.
		Model(&model).
		Where("id = ?", entityID).
		Updates(entity).
		Error; err != nil {
		e := fmt.Errorf("%v: %v", domain.ErrUpdateDojo, err)
		logger.Error(e.Error())
		return nil, e
	}

	logger.Debug(
		"Dojo updated: %+v", entity)

	if err := repo.db.
		Where("id = ?", entityID).
		First(&model).
		Error; err != nil {
		e := fmt.Errorf("%v: %v", domain.ErrUpdateDojo, err)
		logger.Error(e.Error())
		return nil, e
	}

	logger.Debug("[DojoRepository] - [UpdateDojo] "+
		"Fetched updated dojo: %+v", model)

	return model, nil
}
```
```go
func (repo *DojoRepository) Delete(entityID string) error {
	var model *domain.Dojo
	if err := repo.db.
		Where("id = ?", entityID).
		Delete(&model).
		Error; err != nil {
		e := fmt.Errorf("%v: %v", domain.ErrDeleteDojo, err)
		logger.Error(e.Error())
		return e
	}

	logger.Debug("[DojoRepository] - [DeleteDojo] "+
		"Dojo deleted: %+v", model)

	return nil
}
```

#### testcontainers in action (now for real)

