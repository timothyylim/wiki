---
title: Translating In Your Terminal
date: 2024-10-24
---
# Translating In Your Terminal 

As a way to learn German, I write all my todos in German. It feels fitting, for some reason. 

I don't enjoy opening up google translate so I found [translate-shell](https://github.com/soimort/translate-shell). 

For mac users:

```
$ brew install translate-shell
```

I added this to my `~/.zshrc` file: 

```
alias t='trans en:de'
```

which means I can just do this in my terminal:

```
$ t 'book flight tickets'

Flugtickets buchen

Translations of book flight tickets
[ English -> Deutsch ]

book flight tickets
    Flugtickets buchen
```