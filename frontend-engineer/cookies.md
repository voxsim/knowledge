# Cookies

Cookies are mainly used for these three purposes:
- Session management (user logins, shopping carts)
- Personalization (user preferences)
- Tracking (analyzing user behavior)

Cookies have also been used for general client-side storage. While this use could have been considered legitimate at a time when there was no other way to store data on the client side, it is no longer the case nowadays where web browsers are capable of using various storage APIs. Since cookies are sent along with every request, it can be an additional performance burden (especially for mobile web).

## Creating cookies
When receiving an HTTP request, a server can send a Set-Cookie header with the response. The cookie is usually stored by the browser and, afterwards, the cookie value is sent along with every request made to the same server as the content of a Cookie HTTP header. Additionally, an expiration delay can be specified as well as restrictions to a specific domain and path, limiting how long and to which site the cookie is sent to.
