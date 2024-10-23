---
title: Editing A Static Site With Obsidian
aliases:
  - docs/editing-a-static-site-with-obsidian
---
# Editing A Static Site With Obsidian

Let me tell you about how this site works because I love it. 

My setup has two components:

1. A [hugo site](https://gohugo.io) that lives at `~/repos/wiki`
	- This particular [hugo theme](https://themes.gohugo.io/themes/hugo-book/) expects content to be in `wiki/content` and `wiki/content/docs` if it is to be shown in the sidebar 
2. An Obsidian Vault that lives at `~/repos/vault`

**Now for the magic:** 

We do a symlink from `wiki/content` *into* `~/repos/vault` which means that I can use Obsidian's super fast file traversal to edit my personal notes as well as the wiki and most importantly feed my vim addiction!

![image](/obsidian-editing.png)

*How cool is that!*

**How about testing and publishing?**

I've also udpated my `.zshrc` to have two nifty commands: `$ wiki-serve` to test the site and `$ wiki-push` to build and push to Github. Currently I use vercel to deploy from Github. 

My `.zshrc` looks like this:

```
# the brackets means that a subshell is created to cd into the directory
alias wiki-serve='(cd ~/repos/wiki && hugo server)'
alias wiki-push='~/repos/configs/hugo-build-and-push.sh ~/repos/wiki'
```

and the `hugo-build-and-push.sh` script looks like this:

```
#!/bin/bash

# Check if the script is being sourced
(return 0 2>/dev/null) && sourced=1 || sourced=0

# If the script is sourced, don't execute the main functionality
if [ $sourced -eq 1 ]; then
    echo "Script is being sourced. Skipping execution."
    return 0
fi

# Check if a directory is passed as an argument
if [ -z "$1" ]; then
    echo "No directory provided. Usage: ./script.sh <directory>"
    exit 1
fi

# Navigate to the specified directory
DIRECTORY="$1"

if [ ! -d "$DIRECTORY" ]; then
    echo "The specified directory does not exist: $DIRECTORY"
    exit 1
fi

cd "$DIRECTORY" || { echo "Failed to navigate to directory: $DIRECTORY"; exit 1; }

echo "Building Hugo site in $DIRECTORY..."
hugo

echo "Checking for changes..."
if git status --porcelain | grep -q .; then
    echo "Changes detected. Adding files..."
    git add . > /dev/null 2>&1
    
    echo "Committing changes..."
    git commit -m "update content" > /dev/null 2>&1
    
    echo "Pushing changes to remote repository..."
    if git push > /dev/null 2>&1; then
        echo "Changes pushed successfully."
    else
        echo "Failed to push changes. Please check your network connection and remote repository settings."
    fi
else
    echo "No changes detected after Hugo build."
fi

echo "Script completed."

```

**Notes:**

I'm still figuring out how to make images work. If you know please ping me at [@wayfaring_tim](https:/x.com/wayfaring_tim)!