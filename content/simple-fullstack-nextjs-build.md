---
title: Simple Fullstack NextJS build
date: 2024-10-26
tags:
  - snippets
---
# Simple Fullstack NextJS build

This is what I usually use as a baseline for my projects:

- NextJS (with the app router)
	- Served via vercel
- Postgres 
	- Served via neondb 
- Prisma ORM 
- NextAuth, I usually use the twitter login 
- [shadcn](https://ui.shadcn.com) , plain tailwind or MUI for a front end framework 

Might be helpful to read [how to start a nextjs project](/starting-a-nextjs-project) as well.

A simple exercise to get to basic fluency in NextJS could be to create an application with these components. If a user can log in and create something (even if it's just posting some text) it will give you an idea of how a simple fullstack application works.