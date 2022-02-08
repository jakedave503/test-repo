### Caching and Security

Many hosting providers will offer to cache your content at the edge in order to serve data to your users as fast as possible. For example Vercel will [cache your content on the Vercel Edge Network](https://vercel.com/docs/concepts/edge-network/caching) for all static content and Serverless Functions if you provide the necessary caching headers on your response.

It's generally a bad idea to cache any response that requires authentication, even if the response's content appears safe to cache there may be other data in the response that isn't.

This SDK offers a rolling session by default, which means that any response that reads the session will have a `Set-Cookie` header to update the cookie's expiry. Vercel and potentially other hosting providers include the `Set-Cookie` header in the cached response, so even if you think the response's content can be cached publicly, the responses `Set-Cookie` header cannot.

Check your hosting provider's caching rules, but in general you should **never** cache responses that either require authentication or even touch the session to check authentication (eg when using `withApiAuthRequired`, `withPageAuthRequired` or even just `getSession` or `getAccessToken`).

### Error Handling and Security

The default server side error handler for the `/api/auth/*` routes prints the error message to screen, eg

```js
try {
  await handler(req, res);
} catch (error) {
  res.status(error.status || 400).end(error.message);
}
```

Because the error can come from the OpenID Connect `error` query parameter we do some [basic escaping](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html#rule-1-html-encode-before-inserting-untrusted-data-into-html-element-content) which makes sure the default error handler is safe from XSS.

If you write your own error handler, you should **not** render the error message without using a templating engine that will properly escape it for other HTML contexts first.

### Base Path and Internationalized Routing

With Next.js you can deploy a Next.js application under a sub-path of a domain using [Base Path](https://nextjs.org/docs/api-reference/next.config.js/basepath) and serve internationalized (i18n) routes using [Internationalized Routing](https://nextjs.org/docs/advanced-features/i18n-routing).

If you use these features the urls of your application will change and so the urls to the nextjs-auth0 routes will change. To accommodate this there are various places in the SDK that you can customise the url.

For example if `basePath: '/foo'` you should prepend this to the `loginUrl` and `profileUrl` specified in your `Auth0Provider`

```jsx
// _app.jsx
function App({ Component, pageProps }) {
  return (
    <UserProvider loginUrl="/foo/api/auth/login" profileUrl="/foo/api/auth/me">
      <Component {...pageProps} />
    </UserProvider>
  );
}
```

Also, any links to login or logout should include the `basePath`:

```html
<a href="/foo/api/auth/login">Login</a><br />
<a href="/foo/api/auth/logout">Logout</a>
```

You should configure [baseUrl](https://auth0.github.io/nextjs-auth0/interfaces/config.baseconfig.html#baseurl) (or the `AUTH0_BASE_URL` environment variable) eg

```shell
# .env.local
AUTH0_BASE_URL=http://localhost:3000/foo
```

For any pages that are protected with the Server Side [withPageAuthRequired](https://auth0.github.io/nextjs-auth0/modules/helpers_with_page_auth_required.html#withpageauthrequired) you should update the `returnTo` parameter depending on the `basePath` and `locale` if necessary.

```js
// ./pages/my-ssr-page.jsx
export default MySsrPage = () => <></>;

const getFullReturnTo = (ctx) => {
  // TODO: implement getFullReturnTo based on the ctx.resolvedUrl, ctx.locale
  // and your next.config.js's basePath and i18n settings.
  return '/foo/en-US/my-ssr-page';
};

export const getServerSideProps = (ctx) => {
  const returnTo = getFullReturnTo(ctx.req);
  return withPageAuthRequired({ returnTo })(ctx);
};
```

### Comparison with the Auth0 React SDK

We also provide an Auth0 React SDK, [auth0-react](https://github.com/auth0/auth0-react), which may be suitable for your Next.js application.

The SPA security model used by `auth0-react` is different from the Web Application security model used by this SDK. In short, this SDK protects pages and API routes with a cookie session (see ["Cookies and Security"](#cookies-and-security)). A SPA library like `auth0-react` will store the user's ID Token and Access Token directly in the browser and use them to access external APIs directly.

You should be aware of the security implications of both models. However, [auth0-react](https://github.com/auth0/auth0-react) may be more suitable for your needs if you meet any of the following scenarios:

- You are using [Static HTML Export](https://nextjs.org/docs/advanced-features/static-html-export) with Next.js.
- You do not need to access user data during server-side rendering.
- You want to get the access token and call external API's directly from the frontend layer rather than using Next.js API Routes as a proxy to call external APIs

### Testing

By default, the SDK creates and manages a singleton instance to run for the lifetime of the application. When testing your application, you may need to reset this instance, so its state does not leak between tests.

If you're using Jest, we recommend using `jest.resetModules()` after each test. Alternatively, you can look at [creating your own instance of the SDK](./EXAMPLES.md#create-your-own-instance-of-the-sdk), so it can be recreated between tests.

For end to end tests, have a look at how we use a [mock OIDC Provider](./scripts/oidc-provider.js).

# Deploying

For deploying, have a look at [how we deploy our example app to Vercel](./examples/README.md).
