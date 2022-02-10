The Auth0 Next.js SDK is a library for implementing user authentication in Next.js applications.

## Installation

Using [npm](https://npmjs.org):

```sh
npm install @auth0/nextjs-auth0
```

This library supports the following tooling versions:

- Node.js: `^10.13.0 || >=12.0.0`

- Next.js: `>=10`

## Getting Started

### Auth0 Configuration

Create a **Regular Web Application** in the [Auth0 Dashboard](https://manage.auth0.com/#/applications).

> **If you're using an existing application**, verify that you have configured the following settings in your Regular Web Application:
>
> - Click on the "Settings" tab of your application's page.
> - Scroll down and click on the "Show Advanced Settings" link.
> - Under "Advanced Settings", click on the "OAuth" tab.
> - Ensure that "JsonWebToken Signature Algorithm" is set to `RS256` and that "OIDC Conformant" is enabled.

Next, configure the following URLs for your application under the "Application URIs" section of the "Settings" page:

- **Allowed Callback URLs**: `http://localhost:3000/api/auth/callback`
- **Allowed Logout URLs**: `http://localhost:3000/`

Take note of the **Client ID**, **Client Secret**, and **Domain** values under the "Basic Information" section. You'll need these values in the next step.

### Basic Setup

You need to allow your Next.js application to communicate properly with Auth0. You can do so by creating a `.env.local` file under your root project directory that defines the necessary Auth0 configuration values as follows:

```bash
# A long, secret value used to encrypt the session cookie
AUTH0_SECRET='LONG_RANDOM_VALUE'
# The base url of your application
AUTH0_BASE_URL='http://localhost:3000'
# The url of your Auth0 tenant domain
AUTH0_ISSUER_BASE_URL='https://YOUR_AUTH0_DOMAIN.auth0.com'
# Your Auth0 application's Client ID
AUTH0_CLIENT_ID='YOUR_AUTH0_CLIENT_ID'
# Your Auth0 application's Client Secret
AUTH0_CLIENT_SECRET='YOUR_AUTH0_CLIENT_SECRET'
```

You can execute the following command to generate a suitable string for the `AUTH0_SECRET` value:

```bash
node -e "console.log(crypto.randomBytes(32).toString('hex'))"
```

You can see a full list of Auth0 configuration options in the ["Configuration properties"](https://auth0.github.io/nextjs-auth0/modules/config.html#configuration-properties) section of the "Module config" document.

> For more details about loading environmental variables in Next.js, visit the ["Environment Variables"](https://nextjs.org/docs/basic-features/environment-variables) document.

Go to your Next.js application and create a [catch-all, dynamic API route handler](https://nextjs.org/docs/api-routes/dynamic-api-routes#optional-catch-all-api-routes) under the `/pages/api` directory:

- Create an `auth` directory under the `/pages/api/` directory.

- Create a `[...auth0].js` file under the newly created `auth` directory.

The path to your dynamic API route file would be `/pages/api/auth/[...auth0].js`. Populate that file as follows:

```js
import { handleAuth } from '@auth0/nextjs-auth0';

export default handleAuth();
```

Executing `handleAuth()` creates the following route handlers under the hood that perform different parts of the authentication flow:

- `/api/auth/login`: Your Next.js application redirects users to your Identity Provider for them to log in (you can optionally pass a `returnTo` parameter to return to a custom relative URL after login, eg `/api/auth/login?returnTo=/profile`).

- `/api/auth/callback`: Your Identity Provider redirects users to this route after they successfully log in.

- `/api/auth/logout`: Your Next.js application logs out the user.

- `/api/auth/me`: You can fetch user profile information in JSON format.

Wrap your `pages/_app.js` component with the `UserProvider` component:

```jsx
// pages/_app.js
import React from 'react';
import { UserProvider } from '@auth0/nextjs-auth0';

export default function App({ Component, pageProps }) {
  return (
    <UserProvider>
      <Component {...pageProps} />
    </UserProvider>
  );
}
```

You can now determine if a user is authenticated by checking that the `user` object returned by the `useUser()` hook is defined. You can also log in or log out your users from the frontend layer of your Next.js application by redirecting them to the appropriate automatically-generated route:

```jsx
// pages/index.js
import { useUser } from '@auth0/nextjs-auth0';

export default function Index() {
  const { user, error, isLoading } = useUser();

  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>{error.message}</div>;

  if (user) {
    return (
      <div>
        Welcome {user.name}! <a href="/api/auth/logout">Logout</a>
      </div>
    );
  }

  return <a href="/api/auth/login">Login</a>;
}
```

> Next linting rules might suggest using the `Link` component instead of an anchor tag. The `Link` component is meant to perform [client-side transitions between pages](https://nextjs.org/docs/api-reference/next/link). As the links point to an API route and not to a page, you should keep them as anchor tags.

There are two additional ways to check for an authenticated user; one for Next.js pages using [withPageAuthRequired](https://auth0.github.io/nextjs-auth0/modules/helpers_with_page_auth_required.html#withpageauthrequired) and one for Next.js API routes using [withAPIAuthRequired](https://auth0.github.io/nextjs-auth0/modules/helpers_with_page_auth_required.html#withpageauthrequired).

For other comprehensive examples, see the [EXAMPLES.md](./EXAMPLES.md) document.

## Documentation
