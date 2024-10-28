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

Now let's make sure that you can ssh in as that user. First let's switch to the `tim` user if we haven't already:

```
su - tim
```

Create the `.ssh` directory** (if it doesn’t already exist) and set the appropriate permissions:

```
mkdir -p ~/.ssh
chmod 700 ~/.ssh

```

Add your `ssh` key which is found in `~/.ssh/id_rsa.pub`:

```
echo "your-public-ssh-key" >> ~/.ssh/authorized_keys
```

Then set the appropriate permissions:

```
chmod 600 ~/.ssh/authorized_keys
```

and you can exit and then try to `ssh` in as `tim`. 