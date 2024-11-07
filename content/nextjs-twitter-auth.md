---
title: NextJS Authentication With Twitter
date: 2024-11-07
tags:
  - snippets
---
# NextJS Authentication With Twitter

## Step 1. Install NextJS

Install NextJS

```
npx create-next-app@latest
```

## Step 2. Set up a twitter developer account 

Go here: https://developer.x.com/en

Make a project then an app

Read this if you get stuck: https://spacejelly.dev/posts/how-to-authenticate-next-js-apps-with-twitter-nextauth-js

Copy and save all the credentials

## Step 3. Set up your `.env` file

```
TWITTER_CLIENT_ID="<your code>"
TWITTER_CLIENT_SECRET="<your code>"
NEXTAUTH_SECRET="supersecretkey123"
NEXTAUTH_URL=http://localhost:3000
```

Make sure to update the app settings. Follow this guide (I can't be bothered to do all the screenshots right now): 

https://spacejelly.dev/posts/how-to-authenticate-next-js-apps-with-twitter-nextauth-js
## Step 2. Install and setup next-auth

```
npm install next-auth
```

Create this file in `/src/app/api/auth/[...nextauth]/route.ts`

```javascript
import NextAuth, { type NextAuthOptions } from "next-auth";
import TwitterProvider from "next-auth/providers/twitter";
import { NextResponse } from "next/server";

// Debug logs for environment variables
console.log('TWITTER_CLIENT_ID:', process.env.TWITTER_CLIENT_ID?.slice(0, 5) + '...');
console.log('TWITTER_CLIENT_SECRET:', process.env.TWITTER_CLIENT_SECRET?.slice(0, 5) + '...');

const authOptions: NextAuthOptions = {
    providers: [
        TwitterProvider({
            clientId: process.env.TWITTER_CLIENT_ID as string,
            clientSecret: process.env.TWITTER_CLIENT_SECRET as string,
            version: "2.0"
        }),
    ],
    callbacks: {
        async signIn({ user, account, profile }) {
            try {
                if (!account?.providerAccountId || !user.name) {
                    console.error('Missing required user information');
                    return false;
                }

                const username = (profile as any).data.username;
                console.log('User signed in:', { name: user.name, username, providerAccountId: account.providerAccountId });
                return true;
            } catch (error) {
                console.error('Error in signIn callback:', error);
                return false;
            }
        },
        async session({ session, token }) {
            try {
                console.log('Session created:', { session, token });
                return session;
            } catch (error) {
                console.error('Error in session callback:', error);
                return session;
            }
        },
        async jwt({ token, account }) {
            if (account) {
                token.sub = account.providerAccountId;
            }
            console.log('JWT token created:', token);
            return token;
        },
    },
    debug: true,
};

// Wrap the NextAuth handler for the App Router
const handler = NextAuth(authOptions);

export { handler as GET, handler as POST };
```

## Step 3. Test the auth

Get chatgpt to make a button to test the login, it should look something like this at your homepage `src/app/page.tsx:

```javascript
'use client';
import { signIn, signOut, useSession } from 'next-auth/react';

export default function Home() {
  const { data: session, status } = useSession();

  if (status === 'loading') {
    return <div>Loading...</div>;
  }

  if (session) {
    return (
      <div className="p-8">
        <h1 className="text-2xl font-bold mb-4">
          Welcome, {session.user.name}! 👋
        </h1>
        <p className="mb-4">
          Your Twitter username is: @{session.user.username}
        </p>
        <button
          onClick={() => signOut()}
          className="bg-red-500 hover:bg-red-600 text-white font-bold py-2 px-4 rounded"
        >
          Sign out
        </button>
      </div>
    );
  }

  return (
    <div className="p-8">
      <h1 className="text-2xl font-bold mb-4">
        Welcome to the App! 🚀
      </h1>
      <button
        onClick={() => signIn('twitter')}
        className="bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded"
      >
        Sign in with Twitter
      </button>
    </div>
  );
}

```



---

Notes, don't read:

Drizzle is an ORM (Object Relational Mapping) which means that you don't have to write raw SQL to interact with your database.

You can follow this guide:
- next-auth 
- drizzle 

- twitter dev account 
- db 

https://orm.drizzle.team/docs/get-started/vercel-new

```
npm i drizzle-orm @vercel/postgres dotenv
npm i -D drizzle-kit tsx
```


https://developer.x.com/en

https://next-auth.js.org/getting-started/example

https://next-auth.js.org/configuration/initialization#route-handlers-app


```
# nb: http not https
http://localhost:3000/api/auth/callback/twitter
```

