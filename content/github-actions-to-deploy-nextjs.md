---
title: github actions to deploy a nextjs site with shadcn
date: 2024-10-29
tags:
  - snippets
---
# github actions to deploy a nextjs site with shadcn

This took some blood and tears so I'm just saving it here for now:

```yaml
name: Node.js CI

on:
  push:
    branches: [ "main" ]

jobs:
  build:

    runs-on: self-hosted

    strategy:
      matrix:
        node-version: [20]

    steps:
    - name: Check out code
      uses: actions/checkout@v4

    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v4
      with:
        node-version: ${{ matrix.node-version }}
        cache: 'npm'

    - name: Install dependencies
      run: npm ci --legacy-peer-deps

    - name: Build the application
      run: npm run build --if-present

    - name: Replace /home/dev/birdseye directory with built files
      run: |
        rm -rf /home/dev/birdseye
        mkdir -p /home/dev/birdseye
        # Copy only necessary files and the build output
        cp -R ${{ github.workspace }}/.next /home/dev/birdseye/.next
        cp ${{ github.workspace }}/package.json /home/dev/birdseye/
        cp ${{ github.workspace }}/package-lock.json /home/dev/birdseye/

    - name: Install production dependencies on server
      run: |
        cd /home/dev/birdseye
        npm ci --only=production --legacy-peer-deps

    - name: Start or Restart PM2
      run: |
        # Check if birdseye-app already exists
        if pm2 describe birdseye-app > /dev/null; then
          pm2 restart birdseye-app
        else
          pm2 start npm --name "birdseye-app" -- start --prefix /home/dev/birdseye
        fi
        pm2 save

```