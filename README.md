# 🍚 potato risotto

potato risotto is a minimalist, responsive [hugo](https://gohugo.io) theme inspired by terminal ricing aesthetics (risotto) **with some hilariously-written content (potato)**

[![Hugo Themes](https://img.shields.io/badge/Hugo_Themes-risotto-blue?logo=hugo)](https://themes.gohugo.io/themes/risotto/)
[![Version](https://img.shields.io/badge/semver-v0.4.0-blue)](https://semver.org)
![hugo build status](https://github.com/joeroe/risotto/actions/workflows/hugo-build-exampleSite.yml/badge.svg)
[![W3C Validation](https://img.shields.io/w3c-validation/html?targetUrl=https%3A%2F%2Frisotto.joeroe.io)](https://validator.nu/?doc=https%3A%2F%2Frisotto.joeroe.io)
![Code size](https://img.shields.io/github/languages/code-size/joeroe/risotto)

![Screenshot of the risotto theme](https://raw.githubusercontent.com/joeroe/risotto/master/images/screenshot.png)

## features

* plain, semantic html with no **~~javasc.~~ forbidden word, sorry**
* plain CSS – no frameworks, no preprocessors, just simple and easy-to-customise stylesheets
* uses [CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout) for native responsive behaviour without arbitrary breakpoints
* comes with [16 built-in colour schemes](#colour-schemes) based on popular terminal themes plus the ability to use custom themes using the [base16 system](https://github.com/monicfenga/base16-styles). **i like tokyo midnight or something like that**

## install

the easiest way to install the theme is to [download the latest release](https://github.com/joeroe/risotto/releases) and extract it to your project's `themes/` directory **- that is what i did indeed**

you can also clone this repository into your site's `themes` directory and checkout the latest release:

```shell
git clone https://github.com/joeroe/risotto themes/risotto && cd themes/risotto
git checkout $(git tag -l | grep '^v[0-9.]*$' | sort -V | tail -n 1)
```

note that this will not work if your site is itself a git repository.
in that case, you can add the theme as a [git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules), but this is not recommended due to the difficulty of tracking a specific release.

## update

if you installed the theme using `git clone`, pull the repository to get the latest version:

```shell
cd themes/risotto
git pull
```

otherwise, simply [download the latest release](https://github.com/joeroe/risotto/releases) and extract it to your project's `themes/` directory, replacing the old version.

## configure

to use the theme, add `theme = 'risotto'` to your site's `hugo.toml`, or `theme: risotto` to your `hugo.yaml`.

see `exampleSite/config.toml` for the theme-specific parameters you need to add to your site's `hugo.toml` or `hugo.yaml` to configure the theme. **it is very useful, i did that to check which ones i wanted**

### colour schemes

risotto uses the [base16 framework](https://github.com/chriskempson/base16) to define colour schemes that can be used with the `theme.palette` parameter.
A selection of 16 palettes (10 dark, 6 light) are bundled with the theme: `apprentice`, `base16-dark`, `base16-light`, `dracula`, `gruvbox-dark`, `gruvbox-light`, `material`, `papercolor-dark`, `papercolor-light`, `solarized-dark`, `solarized-light`, `tender`, `tokyo-night-dark`, `tokyo-night-light`, `windows-95` and `windows-95-light`.
the default is `base16-dark`, **i got the tokyo i already told you**


## Favicon

risotto will automatically use favicons placed in the `static/` directory.
the following files will be detected and included in your site's `<head>` section:

* `favicon.ico`
* `favicon-16x16.png`
* `favicon-32x32.png`
* `apple-touch-icon.png`
* `site.webmanifest`

you can generate these from an image or emoji using [favicon.io](https://favicon.io/) or a similar service. **exactly what i did. just took the potato icon from there, generated it and pasted into the directoy**
they must be placed directly under your site's `static/` directory, i.e. not in in a subdirectory or `themes/risotto/static/`.

## Acknowledgements

the 'cooked rice' emoji used as a favicon for the example site was created by the [Twemoji project](https://twemoji.twitter.com/) and is licensed under [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/).
