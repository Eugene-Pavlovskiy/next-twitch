This is a [Next.js](https://nextjs.org/) project bootstrapped with
[`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js
  features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out
[the Next.js GitHub repository](https://github.com/vercel/next.js/) - your
feedback and contributions are welcome!

## Create App from Bash

```bash
cd next-twitch

npx create-next-app .

code .
```

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the
result.

You can start editing the page by modifying `pages/index.js`. The page
auto-updates as you edit the file.

[API routes](https://nextjs.org/docs/api-routes/introduction) can be accessed on
[http://localhost:3000/api/hello](http://localhost:3000/api/hello). This
endpoint can be edited in `pages/api/hello.js`.

The `pages/api` directory is mapped to `/api/*`. Files in this directory are
treated as [API routes](https://nextjs.org/docs/api-routes/introduction) instead
of React pages.

This project uses
[`next/font`](https://nextjs.org/docs/basic-features/font-optimization) to
automatically optimize and load Inter, a custom Google Font.

## Install Tailwind CSS with Next.js

`https://tailwindcss.com/docs/guides/nextjs`

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

### Configure your template paths

Add the paths to all of your template files in your `tailwind.config.js` file.

```bash
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./app/**/*.{js,ts,jsx,tsx}",
    "./pages/**/*.{js,ts,jsx,tsx}",
    "./components/**/*.{js,ts,jsx,tsx}",

    // Or if using `src` directory:
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

### Add the Tailwind directives to your CSS

Add the `@tailwind` directives for each Tailwind’s layers to your globals.css
file.

```bash
@tailwind base;
@tailwind components;
@tailwind utilities;

html {
    @apply bg-black text-white scroll-smooth
}
```

## Add to files `_app.js`

```bash
import Navbar from '@/components/Navbar'
import '@/styles/globals.css'

export default function App({ Component, pageProps }) {
  return (
    <>
      <Navbar />
      <Component {...pageProps} />
    </>
  )
}

```

## Create directory `components` and inside file `Navbar.jsx`

```bash
rafce

import React from 'react'

const Navbar = () => {
  return (
    <div>Navbar</div>
  )
}

export default Navbar
```

## Mobile Menu close on click `onClick={() => setNav(false)}`

```bash
<ul className="text-center">
          <li onClick={() => setNav(false)} className="p-4 text-3xl font-bold">
            <Link href="/">Home</Link>
          </li>
          <li onClick={() => setNav(false)} className="p-4 text-3xl font-bold">
            <Link href="/">Live Channels</Link>
          </li>
          <li onClick={() => setNav(false)} className="p-4 text-3xl font-bold">
            <Link href="/">Top Categories</Link>
          </li>
          <li onClick={() => setNav(false)} className="p-4 text-3xl font-bold">
            <Link href="/account">Account</Link>
          </li>
</ul>
```

## Install HeadlessUI for menu

`https://headlessui.com/react/menu`

```bash
npm install @headlessui/react
or
npm add @headlessui/react
```

## Install React icons

```bash
npm add react-icons
```

## Install Next Auth

```bash
npm add next-auth
or
npm install next-auth
```

## Add API route

To add NextAuth.js to a project create a file called `[...nextauth].js` in
`pages/api/auth`

```bash
import NextAuth from "next-auth"
import GithubProvider from "next-auth/providers/github"

export const authOptions = {
  // Configure one or more authentication providers
  providers: [
    GithubProvider({
      clientId: process.env.GITHUB_ID,
      clientSecret: process.env.GITHUB_SECRET,
    }),
    // ...add more providers here
  ],
}

export default NextAuth(authOptions)
```

## Change file `[...nextauth].js`

```bash
import NextAuth from 'next-auth';
import GithubProvider from 'next-auth/providers/github';
import GoogleProvider from 'next-auth/providers/google';

export default NextAuth({
  // Configure one or more authentication providers
  providers: [
    GithubProvider({
      clientId: process.env.GITHUB_ID,
      clientSecret: process.env.GITHUB_SECRET,
    }),
    GoogleProvider({
      clientId: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    }),
    // ...add more providers here
  ],
  secret: process.env.JWT_SECRET,
});
```

## Configure Shared session state `pages/_app.jsx`

To be able to use useSession first you'll need to expose the session context,
<SessionProvider />, at the top level of your application:

```bash
import { SessionProvider } from "next-auth/react"
export default function App({
  Component,
  pageProps: { session, ...pageProps },
}) {
  return (
    <SessionProvider session={session}>
      <Component {...pageProps} />
    </SessionProvider>
  )
}
```

## Create in file `.env`

`https://github.com/settings/applications`

```bash
GITHUB_ID=YOUR_SECRET_ID
GITHUB_SECRET=YOUR_SECRET_ID

GOOGLE_CLIENT_ID=YOUR_SECRET_ID
GOOGLE_CLIENT_SECRET=YOUR_SECRET_ID

NEXTAUTH_URL=http://localhost:3000/

JWT_SECRET=YOUR_SECRET_ID
```

## You can quickly create a good value on the command line via this openssl command in Bash-Terminal:

`https://next-auth.js.org/configuration/options#secret`

```bash
$ openssl rand -base64 32
```

## Create file at folder `pages/account.jsx`

## Frontend - Add React Hook `components/account.jsx`

The useSession() React Hook in the NextAuth.js client is the easiest way to
check if someone is signed in. You can use the useSession hook from anywhere in
your application (e.g. in a header component).
`https://next-auth.js.org/getting-started/example#frontend---add-react-hook`,
`https://next-auth.js.org/getting-started/client`

```bash
import { useSession, signIn, signOut } from "next-auth/react"

export default function Component() {
  const { data: session } = useSession()
  if (session) {
    return (
      <>
        Signed in as {session.user.email} <br />
        <button onClick={() => signOut()}>Sign out</button>
      </>
    )
  }
  return (
    <>
      Not signed in <br />
      <button onClick={() => signIn()}>Sign in</button>
    </>
  )
}
```

## Create GOOGLE_CLIENT_ID and GOOGLE_CLIENT_SECRET

`https://console.cloud.google.com/apis/credentials`

```bash
GOOGLE_CLIENT_ID=YOUR_SECRET_ID
GOOGLE_CLIENT_SECRET=YOUR_SECRET_ID
```

## Create new file in `components/SideMenu.jsx`

```bash
rafce
```

## Create Data from `https://www.mockaroo.com/` and create file in new folder `data/mock-data.js`

## Create files in folder `components/Layout.jsx` and `components/Main.jsx`

## File `Layout.jsx`

```bash
import React from 'react'
import Main from './Main'
import SideMenu from './SideMenu'

const Layout = () => {
  return (
    <div className='pt-[60px] flex w-full'>
        <SideMenu />
        <Main />
    </div>
  )
}

export default Layout
```
## Create files in folder `components/Hero.jsx`, `components/LiveChannels.jsx`, `components/IconBar.jsx`, `components/Categories.jsx`, `components/CategoriesItem.jsx`, `components/LiveChannelItem.jsx`

## File `Main.jsx`
```bash
import React from 'react'
import Categories from './Categories'
import Hero from './Hero'
import IconBar from './IconBar'
import LiveChannels from './LiveChannels'

const Main = () => {
  return (
    <div className='absolute left-[64px] xl:left-[220px]'>
        <Hero />
        <LiveChannels />
        <IconBar />
        <Categories />
    </div>
  )
}

export default Main
```
# Deploy app to Github Pages with CICD
```bash
git init
git add .
git commit -m "FirstDeploy"
git branch -M main
git push -u origin main
```

## Make Pages on Github
In Pages/Build and deployment/Source choose GitHub Actions. Go to nextjs and commit

## Deploy on Vercel
The easiest way to deploy your Next.js app is to use the
[Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme)
from the creators of Next.js.

Check out our
[Next.js deployment documentation](https://nextjs.org/docs/deployment) for more
details.
