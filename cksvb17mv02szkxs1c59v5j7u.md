---
title: "Secure Your Next.js Application in 5 minutes !!"
datePublished: Sat Aug 28 2021 04:49:30 GMT+0000 (Coordinated Universal Time)
cuid: cksvb17mv02szkxs1c59v5j7u
slug: secure-your-nextjs-application-in-5-minutes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1630056233711/cfZQ_vvsS.png
tags: programming-blogs, javascript, reactjs, auth, nextjs

---

## Table of Contents
- **Intro to Next.js authentication**
- **About NextAuth package**
- **Setting up NextAuth**
- **Authentication with different providers (ex: Google, Github, Facebook, LinkedIn etc)**
- **Handling SignIn, SignOut functionalities**
- **Securing Pages**

----

## Intro to Next.js authentication
- The internet is a magical place where you can connect to people from any part of the world, but it is also a place where criminals lurk and try to steal your identity, your money, and your data. 
- One of the biggest problems with the internet is identity theft but it can be prevented with authentication.
- Compare to **React.js** where we only have to deal with **Client-Side authentication**, In **Next.js** we have to authenticate not only **Client-side** but also **Server-Side** and **API routes**.
- In this blog, I'm going to implement authentication with the help of the **Next-auth **package in **Next.js**.
- 
![CatDayLetItBeginGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629987856394/q5XBXLLdN.gif)

-----

## About NextAuth package
- **NextAuth ** in my opinion is the best way to handle authentication in **Next.js** till now.
- It's because **NextAuth** provides built-in support for **Google, Facebook, Auth0, Apple**, and many more.
- If you don't want to authenticate your users with these providers, **NextAuth** provides **Built-in email / passwordless / magic link** authentication too.
- Also If you want to **persist the user** then also you can do it by bringing your own Databases like **MySQL, Postgres, MSSQL, MongoDB**, etc.
- It also provides CSRF Token validation **JWT **with **JWS / JWE / JWK / JWK**, **Tab syncing**, **auto-revalidation** etc.
- 
![MathematologistSpongebobGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1630053969756/9szxTmfDk.gif)

------

## Setting up NextAuth
- Before moving ahead fork the below repository for getting the starter project.
- %[https://github.com/red-star25/next-auth-blog].
- After forking run this project, you'll see something like this -
- 
![starter.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1629999523078/Vl1sD75lD.gif)
- Okay, so now that we've done all the setup let's install **NextAuth** package.
- ## Installing NextAuth
```
npm i next-auth
```
- ## Configuring Different Providers
- To implement different auth providers we have to first create a file inside `api/auth` called `[...nextauth].js`
- 
![nextauthjs.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1629999977355/EYA065Op9.png)
- Now **Import NextAuth** and **Providers**
- 
```
import NextAuth from "next-auth" 
import Providers from "next-auth/providers"    // contains all the provider 
```
- Now export default **NextAuth**
```
import NextAuth from "next-auth" 
import Providers from "next-auth/providers"
export default NextAuth ({
   // ...
})
```
- This **NextAuth** has one property called **providers** in which we can define all the list of providers that we want to use.
- Let's add **Github** provider
- 
```
export default NextAuth({
  providers: [
    Providers.GitHub({
      clientId: process.env.GITHUB_CLIENT_ID,
      clientSecret: process.env.GITHUB_CLIENT_SECRET,
    }),
    // You can add here multiple provider as per your requirement
  ],
});
```
- To get the **CLIENT_ID** and **CLIENT_SECRET**, go to [Profile Settings](https://github.com/settings/profile).
- Click on the **Developer settings**
- 
- ![dev setting.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630044340587/fP7-yz9d6.png)
- Click on the **OAuth Apps** tab and create a **New OAuth App**
- 
- ![new oauth app.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630044237558/X-snEKO7W.png)
- Now fill the application details and **Register application**.
- ![fill application details.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630044308774/4gx_kEOdu.png)
- Now **copy** your **CLIENT_ID** and **CLIENT_SECRET** and paste it inside the `.env.local` file
- 
![idsecret.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630044550790/lTXbn_D3k.png)
- 
```
//.env.local
GITHUB_CLIENT_ID=2ff72fc2ae451c063edc
GITHUB_CLIENT_SECRET=60e9dc019d9d172b10662a66350cbfb16ff0d189 
```
- Now if you run the application and type `http://localhost:3000/api/auth/signin` in the browser, you'll see one button named **Sign in with Github**
- 
![signinbutton.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630044739265/SOmtGuZwG.png)
- And if you click on this button, you will be redirected to GitHub authorization page.
- After authorizing, you will be then redirected to the **HomePage**.
- If you want to verify whether you are signed in or not, open **Developer tool** in chrome and go to  **Cookies** under **Application** tab.
- If you see below to cookies then it means you've successfully signed in.
![authsession.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630045001846/xwmg6ANur.png)
- Now if you want to **signOut** then simply put `http://localhost:3000/api/auth/signout` in the browser URL and you will see - 
- 
![signout.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630045216654/GBt7BvEvd.png)
- If you click on this button you will be redirected to **HomePage** and your **Next-session** cookie will be deleted automatically.
- 
![signoutcokkie.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1630045312173/VV2oHhbFl.png)
- Now we will not tell user to type this `/api/auth/signin` or `/api/auth/signout` URL manually ,**right**?
- We want to handle this authentication process on some kind of button click.
- So let's see how we can do **signIn** and **signOut** on button click.

------

## Handling SignIn, SignOut on Button Click
- It's very simple, Import `signIn` and `signOut` from `next-auth/client` package
- 
```
import {signIn, signOut} from "next-auth/client"
```
- Now simply call these two functions on `onClick`. And also don't forget to pass `href`.
- 
```
function Navbar() {
    const handleSignIn = (e) => {
      e.preventDefault();
      signIn();
    };

    const handleSignOut = (e) => {
      e.preventDefault();
      signOut();
    };

  return (
    <nav>
      <Link href="/">
        <button>Home</button>
      </Link>
      <Link href="/dashboard">
        <button>Dashboard</button>
      </Link>
      <Link href="/blog">
        <button>Blog</button>
      </Link>
      <Link href="/api/auth/signin">
        <button onClick={handleSignIn}>SignIn</button>
      </Link>
      <Link href="/api/auth/signout">
        <button onClick={handleSignOut}>SignOut</button>
      </Link>
    </nav>
  );
}
export default Navbar;
```
- And **BOOM !!**.
- 
![buttonclick.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1630046392455/vAt71BHcW.gif)

- But if you see in the navbar, The **SignIn** button is still visible even if the user has signed in. And also the **SignOut** button is visible even if the user has not signed in.
- To solve this issue, we have to check if the user has signed in or not, and according to that information, we can conditionally hide or show these buttons.
- To check whether the user has signed in or not, **NextAuth** provides a hook called `useSession`.
- This hooks returns two values -
- 1. **session** object and 
- 2. **loading** flag
- If **session** is `null` that means the user has not signed in and we can show **signIn** button and hide **signOut** button and vice-versa.
- First import `useSession` hook
```
import { signIn, signOut, useSession } from "next-auth/client";
```
- And now conditionally render buttons
```
function Navbar() {
  const [session, loading] = useSession();

  return (
    <nav>
      <Link href="/">
        <button>Home</button>
      </Link>
      <Link href="/dashboard">
        <button>Dashboard</button>
      </Link>
      <Link href="/blog">
        <button>Blog</button>
      </Link>
      {!loading && !session && (
        <Link href="/api/auth/signin">
          <button onClick={handleSignIn}>SignIn</button>
        </Link>
      )}
      {session && (
        <Link href="/api/auth/signout">
          <button onClick={handleSignOut}>SignOut</button>
        </Link>
      )}
    </nav>
  );
}
export default Navbar;
```
- 
![conditionalrendering.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1630047503795/6_bEKK83t.gif)

-----

## Securing Pages
- Sometimes we want users to be authenticated to be able to access a particular page.
- To do that **NextAuth** provides a very handy hook called `getSession`.
- This will return `null` if the user has not signed in, otherwise, return an object.
- Let's secure our **Dashboard** page. We want our users to access the dashboard page if they are signed in, otherwise will be redirected to **signIn** page.
- Import packages
- 
```
import { getSession, signIn } from "next-auth/client";
import { useEffect, useState } from "react";
```
- 
```
function Dashboard() {
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const checkIsSignedIn = async () => {
      await getSession().then((session) => {
        if (!session) {
          // Not Signed In
          signIn();
        } else {
          // Signed In
          setLoading(false);
        }
      });
    };
    checkIsSignedIn();
  }, []);

  if (loading) {
    return (
      <div className={styles.dashboard}>
        <h2>Loading</h2>
      </div>
    );
  }

  return (
    <div className={styles.dashboard}>
      <h1>Dashboard page</h1>
    </div>
  );
}
export default Dashboard;
```
- Now if you click on the dashboard, you will be redirected to **signIn** page if you are not signed in otherwise to **Dashboard** page if signed in.
- 
![securingpage.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1630048578881/DRAKdEqSY.gif)

----
- Above we're securing our pages on the Client-Side. Now, what if we want to **Secure pages on the Server-Side**.
- We can use `getSession` hook to do this - 
- 
```
import { getSession } from "next-auth/client";
import styles from "../styles/Blog.module.css";
```
```
function Blog({ data }) {
  return (
    <div className={styles.blog}>
      <h1>{data}</h1>
    </div>
  );
}
export default Blog;
```
```
export async function getServerSideProps(context) {
  const session = await getSession(context);  // pass the context
  if (!session) {
     // redirecting to signIn page if not signed In
    return {
      redirect: {
        destination: "/api/auth/signin?callbackUrl=http://localhost:3000/blog",
        permanent: false,
      },
    };
  }
  return {
    props: {
      data: "Welcome to Blog page",
    },
  };
}
```
- 
![secureserverside.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1630053316889/JvJvS1zTL.gif)
---- 
- We are also dealing with **APIs** in Next.js.
- We can also **secure our API routes** using `getSession()` hook.
- Goto your API route page, and import `getSession()` hook.
- And paste the below code inside - 
- 
```
import { getSession } from "next-auth/client";
```
```
const userInfo = async (req, res) => {
  const session = await getSession({ req });
  if (!session) {
    res.status(401).json({ error: "User not authenticated" });
  } else {
    res.status(200).json({ user: session.user });
  }
};
export default userInfo;
```
- 
![secureapi.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1630053216908/hyIJn6JYV.gif)
- Now if you try to access `/api/userInfo` without **signIn** then you'll get a message - **User not authenticated**, otherwise a **user data** if signed in
- **That's it!!** We've implemented authentication and also secured the pages and API routes in Next.js.
- 
![MinionsYayGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1630126047476/CZSQVBSXU7.gif)
- You can go further and do many things with **NextAuth** as it provides so many features.
- %[https://next-auth.js.org/]
-------

## Wrapping up
- Finished Authentication :
- %[https://github.com/red-star25/next-auth-blog/tree/final]
- **Thank you for reading**. **Hope you liked it.**
- **Comments and Feedbacks are welcomed** ✍️
- 
![PeaceOutImOutGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1630056665839/kD5ix5p4b.gif)
