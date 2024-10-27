---
title: Tweeting From The Terminal
tags:
  - snippets
date: 2024-10-26
---
# Tweeting From The Terminal

I'm still working on open sourcing the code but it works something like this:
1. Set up an app at developer.twitter.com
2. Use those credentials to do local authentication 
3. I use nodejs to run an express server so auth can happen in a browser 
4. Get the tokena and save it locally, it's long lived so it can just be reused until revoked by the user 
5. Post using token 


