---
title: Translating In Your Terminal
---
# Translating In Your Terminal 

As a way to learn German, I write all my todos in German. It feels fitting, for some reason. 

I don't enjoy opening up google translate so I found [translate-shell](https://github.com/soimort/translate-shell). 

I added this to my `~/.zshrc` file: 

```
alias t='trans en:de'
```

which means I can just do this in my terminal:

```
$ t 'hello world'

hello world

Hallo Welt

Translations of hello world
[ English -> Deutsch ]

hello world
    , hallo welt
```

