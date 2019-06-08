Title: First Post / How to Setup Pelican + GitHub Pages
Date: 2019-06-08 15:04
Tags: pelican, github
Slug: pelican-plus-ghpages-ftw
Authors: Mike Yu
Category: Python
Summary: First blog post

This is a meta-blog post about setting up this blog.

Requirements:

* Using Pelican because I like using Python
* Using GitHub pages because it's free hosting
* Look nice-ish / minimalist -- hopefully accomplishable with a premade Pelican theme
* Markdown content
* Eventual jupyter notebook integration -- Can be done with [pelican-ipynb](https://github.com/danielfrg/pelican-ipynb)
* Simple publishing workflow
* Doable in a few hours

## Workflow

I'm hoping this is the eventual workflow:

* Start writing, maybe using a blank template so I'm consistent with post metadata (author, date, tags, etc.)
* Run command to build html pages from source
* Run command to push to the GitHub

Essentially a two-click build process.

## Setup

So far I've read online that you can create two repositories to get it working:

* `<username>.github.io` - where the built content lives that will be published
* `<username>.github.io-src` - raw source files

This workflow makes sense to me so I'll try to do it. The part that doesn't make sense is git submodules. Idk what those are.

Luckily when I Googled "github pages submodules pelican" I came across [GitHub Pages with Pelican](https://fedoramagazine.org/make-github-pages-blog-with-pelican/) by Fedora Magazine which basically lays out everything needed to get started.

The only changes I made were how I named the folder on my local computer (blog instead of ghpages):

```sh
$ git clone git@github.com:joeeoj/joeeoj.github.io-src blog
```

Since I access work repos on this laptop I had to set the git config locally after I download the repo by:

```sh
$ cd blog
$ git config user.name "Mike Yu"
$ git config user.email <firstinitial+last@probablygmail.com>
```

Otherwise it would've tried to use my work email when pushing and pulling.

## Quick start

Per the above website I went through `pelican-quickstart` and also followed their instructions. It was easy.

## Theme

I also wanted to change the default theme which is documented on the [pelican-themes](https://github.com/getpelican/pelican-themes#using-themes) GitHub page. Basically you:

* Clone the repo recursively to your computer
* Then add the full path of the subfolder of the theme you want to your pelicanconf.py and set it equal to variable named `THEME`

## Content

I wrote up this post and saved in the content folder as a Markdown (.md) file. Then ran this to view a local preview (before pushing to GitHub).

```sh
$ make html && make serve
```

## Publishing

Slightly modified from the website above:

```sh
$ cd output # this is the submodule
$ git add .
$ git commit -m "First post"
$ git push -u origin master
$ cd .. # go back up to src file
$ touch .gitignore # I added *.pyc and .DS_Store
$ git add .
$ git commit -m "Add gitignore"
$ git push -u origin master
```

## Finished

That's it. Took about 1.5 hours including writing this post.
