---
title: Editing H5P docs
tags:
  - draft
---
# Editing this page

## Hugo setup

Let's get it running locally first: 

```
$ brew install hugo
$ git clone https://github.com/timothyylim/h5p-site
$ cd h5p-site
$ hugo serve
```

Navigate to `http://localhost:1313/` to see that it works. 

## Editing the site

You can open the repo in any text editor you wish, the posts will go under `/content`. Note that images will go in `/content` too until I find a better place to put them. 

All the posts are markdown but note that articles will need to have properties defined at the top like so:

```
---
date: 2024-10-24
title: What Is H5P?
---

# What is H5P?
```

## Pushing your changes

You need to build the site before updating `git`: 

```
$ hugo build
$ git add .
$ git commit -m 'update site'
$ git push
```

You can then check `h5p.timothylim.is` for changes. 






