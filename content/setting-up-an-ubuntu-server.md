---
title: Setting Up An Ubuntu Server
tags:
  - snippets
date: 2024-10-27
---
# Setting Up An Ubuntu Server

## Provision The First User 

It's not a good idea to use `root` so let's set up the main user.

Create the user:

```bash
$ sudo adduser tim
```

Add the user to the `sudo` group:

```bash
$ sudo usermod -aG sudo tim
```

Verify sudo access by switching to the `tim` user:

```
$ su - tim
```

Then, check if sudo access works by running a sudo command, like listing the root directory:

```
$ sudo ls /root
```

