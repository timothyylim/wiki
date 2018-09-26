---
title: Publishing a Hexo Site to gh-pages 
---

This shows you how to publish a Hexo site to a project page in Github. This assumes that you already have a repository set up.


## Update your Hexo configuration

Set your public directory to 'docs' in _config.yml:

```
public_dir: docs
```

Set the url and root appropriately:

```
url: https://timothyylim.github.io/wiki
root: /wiki/
```

Generate the site:

```
$ hexo g
```

Push to your repo and set the github pages to point to /docs.
