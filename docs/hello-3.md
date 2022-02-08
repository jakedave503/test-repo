### API Reference

- [Configuration Options](https://auth0.github.io/nextjs-auth0/modules/config.html)

**Server-side methods**:

- [handleAuth](https://auth0.github.io/nextjs-auth0/modules/handlers_auth.html)
- [handleLogin](https://auth0.github.io/nextjs-auth0/modules/handlers_login.html#handlelogin)
- [handleCallback](https://auth0.github.io/nextjs-auth0/modules/handlers_callback.html)
- [handleLogout](https://auth0.github.io/nextjs-auth0/modules/handlers_logout.html)
- [handleProfile](https://auth0.github.io/nextjs-auth0/modules/handlers_profile.html)
- [withApiAuthRequired](https://auth0.github.io/nextjs-auth0/modules/helpers_with_api_auth_required.html)
- [withPageAuthRequired](https://auth0.github.io/nextjs-auth0/modules/helpers_with_page_auth_required.html#withpageauthrequired)
- [getSession](https://auth0.github.io/nextjs-auth0/modules/session_get_session.html)
- [getAccessToken](https://auth0.github.io/nextjs-auth0/modules/session_get_access_token.html)
- [initAuth0](https://auth0.github.io/nextjs-auth0/modules/instance.html)

**Client-side methods/components**:

- [UserProvider](https://auth0.github.io/nextjs-auth0/modules/frontend_use_user.html#userprovider)
- [useUser](https://auth0.github.io/nextjs-auth0/modules/frontend_use_user.html)
- [withPageAuthRequired](https://auth0.github.io/nextjs-auth0/modules/frontend_with_page_auth_required.html)

Visit the auto-generated [API Docs](https://auth0.github.io/nextjs-auth0/) for more details.

### Cookies and Security

All cookies will be set to `HttpOnly, SameSite=Lax` and will be set to `Secure` if the application's `AUTH0_BASE_URL` is `https`.

The `HttpOnly` setting will make sure that client-side JavaScript is unable to access the cookie to reduce the attack surface of [XSS attacks](https://auth0.com/blog/developers-guide-to-common-vulnerabilities-and-how-to-prevent-them/#Cross-Site-Scripting--XSS-).

The `SameSite=Lax` setting will help mitigate CSRF attacks. Learn more about SameSite by reading the ["Upcoming Browser Behavior Changes: What Developers Need to Know"](https://auth0.com/blog/browser-behavior-changes-what-developers-need-to-know/) blog post.
