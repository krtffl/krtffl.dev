+++
title = "the meta post"
date = 2024-09-13
draft = false
description = "the post about the blog"
tags = [
    "meta", 
    "blog",
]
categories = [
    "meta",
    "blog",
]
+++

this is probably the post that makes the least sense of all but i still need to get some practice before i get into business and dive deep into the technicalities so here it is 

<!--more-->

after i decided to start up with this gathering of bullshit-fun-technical-wannabe garbage the first big decision was presented: how the fuck do i get a blog going? of course, as an engineer - yep, i'm going to call myself an engineer because it sounds great - you always want to do everything yourself from scratch. 

i guess i always got the DRY the wrong way - **DO, REPEAT YOURSELF**

from scratch it is then!

- maybe use it to learn a new language?
- just copy some repo out there that looks nice?
- there is probably tons of nice templates that i can use, no?

### first try: learn django

ai ai ai ai ai ai ai ai ai ai 
ai
ai ai ai
ai (no idea how this is gonna print out, i am obviously not using any kind of live previewer and the most markdown i've written is for the changelogs of my projects...  so we will see!) is everywhere. eveything. articial inteligence. which is of course not intelligent as we (i) are, but i still had to look up whether intelligence had one or two l. turns out it had 2. so a big L for me :) 

so, artifical intelligence, you need to know python. you *better* know python if you wanna keep some chances at keeping your job. go build your boring blog in python.

what about django? it sounds cool. i really liked the movie and of course i judge a book by its cover, and a film by its name, so let's go with it. i started following a couple of articles that i found informative enough

- [build a blog from scratch, jasmine finer, real python](https://realpython.com/build-a-blog-from-scratch-django/)
- [build a blog application, django central](https://djangocentral.com/building-a-blog-application-with-django/)

there was more than enough out there to build a fully functioning blog website or application or web application or whatever you want to call it. of course some prior python knowledge is welcome, otherwise there is some stuff you won't get, or at i least i didn't.

by the way, it turns out django is quite nice, it has some built-in administration features that i found reeeeeally nice. i had no idea. if you need to build some API and then an admin panel to manage the different data structures, it just out of the box done. nice.

however it looked U G L Y as F U C K. and that is actually my problem with everything. it is not the funcionality (sometimes) or getting it running (often) but the looks of it (always). 

put in the trash then.  

(yes i considered adding some tailwind maybe, play with the css and the classes, but that it's just so much time and i knew i woulnd't even get it pretty anyway)

### second try: copy a repo

for this there is again a bunch of options however i really (sadly) know that i need to step up - actually, start - my react game. everything is react when it comes the visually appealing applications and i need to get into that cult before it is too late. it is too late already but, you know, even more too late.

from scracth it was not an option. no no no no no. not for this. maybe for some other application i will need to do it, but not for the blog please. i cannot spend 3 weeks starting and discarding projects until i finally get the blog running.

so i came across the [tailwind nextjs starter blog](https://github.com/timlrx/tailwind-nextjs-starter-blog). it doesn't look as pretty as i would like but it is react. it is next even. and has tailwind. it is not bad, and they have a list of examples build with the starter that look quite good.

so i clone the repo, play with it, edit some information. but no.

it is huge. there is a hundreds (maybe not but sounds better than tens) of files in there, and i don't wanna overcomplicate it. who the hell is gonna wanna subscribe to my newsletter? i don't even want to write a newsletter! 

honestly i don't even remember anymore if the newsletter option comes out of the box, but you get it. when you have a big nextjs blog with all that javascript running there, it is asking for the newsletter. and the comment sections and all that stuff than involves user participation and i don't like people. plus it looks really sad when there are not comments, or no users that want to get your newsletter. 

screw it then.

### third try: templates?

after discarding the nextjs starter, i went back to the repo and read its description once again

> perfect as a replacement to existing Jekyll and Hugo individual blogs
>> replacement to existing Jekyll and Hugo individual blogs
>>> Hugo 

yep. i will walk this way in reverse. i knew about [hugo](https://gohugo.io/), the static site generator which is actually written in go. i didn't know about jekyll so i checked that out too. 

then of course i asked reddit which one was better and people where saying all kinds of stuff. so hey, let's see the templates they have because i want to do as little as possible when it comes to stylizing it. and rapidly i decided for hugo because they have a [gallery of themes for you to choose](https://themes.gohugo.io/).

i found a couple that i liked but eventually as one can infer by simply reading this bunch of crap i went with risotto because who doesn't love some risotto. i love rice. i love it. and it looked quite good. similar to what i had visualized when i thought of a blog of mine - thanks [joe roe!](https://github.com/joeroe).

i had never used hugo before but i figured it would be quite easy and it was. great documentation, great configuration options, so i just started a new project, set the theme, and configured it based on the risotto especifications and that is about it.

i could get into the commands that i used and everything but honestly it is perfectly clear and well written on their pages.

then i checked what was the easiest way to deploy a hugo generated static site and of course cloudflare - who doesn't like cloudflare? they are like, the best - makes the life easy for you with [basically two-click automatic deployment](https://developers.cloudflare.com/pages/framework-guides/deploy-a-hugo-site/).

and that is about it

### fourth try: conclusion?

a bunch of text needs to end in a conclusion!!! what did we get out of this? 

- for starters that the D in DRY is actually a **DO NOT** and until you realize it you mostly waste time and time.
- that styling, designing and all that bunch of stuff is a career per se. it is hard. so avoid it as much as possible.
- simpler is better. just find the most simple solution and it is probably good enough.
