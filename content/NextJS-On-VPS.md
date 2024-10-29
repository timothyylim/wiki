---
title: NextJS on VPS
date: 2024-10-28
tags:
  - snippets
---
# NextJS on VPS 

Notes from [this video](https://www.youtube.com/watch?v=vj34hX8jWM0).

Assuming that you've already set up your [server](/setting-up-an-ubuntu-server), we can go ahead and get started.

## Install `nvm`

Install [nvm](https://github.com/nvm-sh/nvm) for managing node versions:

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

then 

```
source ~/.bashrc
nvm
```

and it should work.

Install the latest version of node:

```
nvm install --lts
```

## Install and configure `nginx`

Install `nginx` like so:

```
sudo apt-get install nginx
```

We need to configure `nginx` to route traffic to our app:

```
cd /etc/nginx/sites-available 
```

```
sudo vim things
```


```
server {
  listen 80;
  server_name YOUR_IP_ADDRESS;
  location / {
    proxy_pass http://localhost:3000;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
  }
}
```

```
sudo ln -s /etc/nginx/sites-available/things /etc/nginx/sites-enabled/things
```

```
sudo nginx -t
```

```
sudo service nginx restart
```

## Get the code on the server

Repo → Settings → Deploy Keys

Make an ssh key for the server:

```
ssh-keygen 
```

```
cd /home/tim
cat ~/.ssh/id_ed25519.pub
```

Paste the key into Github but do not allow write access, the server should not be able to write to the repo.

```
git clone https://github.com/timothyylim/birdseye
```

```
cd birdseye
npm run build
```

## Let's test it 

```
npm run dev
```

and visit your domain or IP. It should work


## Letting the app live

```
npm i -g pm2 
pm2 start npm --name "birdseye" -- run dev
```


---

Other resources:
- https://richardkovacs.dev/blog/bring-your-own-nextjs
- https://mohamedyamani.com/blog/how-to-deploy-nextjs-application-to-vps-using-nginx-and-pm2/