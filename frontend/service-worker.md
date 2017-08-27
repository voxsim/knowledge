## What it is this?
A service worker is a background worker that acts as a programmable proxy, allowing us to control what happens on a request-by-request basis. We can use it to make (parts of, or even entire) web apps work offline. It works only with HTTPS.

Service workers depend on two APIs to work effectively: Fetch (a standard way to retrieve content from the network) and Cache (content storage for application data. This cache is independent from the browser cache or network status).

## A base for advanced features
Service workers are also designed to work as a bedrock API for unlocking features that enable web apps to work more like native apps. This includes:
* Push API — An API enabling push services to send push messages to a webapp. Servers can send messages at any time, even when the webapp or browser are not running.
* Background Sync — for deferring actions until the user has stable connectivity. This is handy for making use whatever the user wants to send is actually sent. This enables pushing periodic updates when the app is next online.

## Service Worker Lifecycle
Each service worker goes through three steps in its lifecycle: registration, installation and activation.

### Registration
To install a service worker, you need to register it in script. Registration informs the browser where your service worker is located and lets it know it can start installing in the background. Basic registration in your index.html could look like this:

```javascript
// Check for browser support of service worker
if ('serviceWorker' in navigator) {

 navigator.serviceWorker.register('service-worker.js')
 .then(function(registration) {
   // Successful registration
   console.log('Hooray. Registration successful, scope is:', registration.scope);
 }).catch(function(err) {
   // Failed registration, service worker won’t be installed
   console.log('Whoops. Service worker registration failed, error:', error);
 });
}
```
The service worker is registered with navigator.serviceWorker.register which returns a Promise that resolves when the SW has been successfully registered. The scope of the service worker is logged with registration.scope.

## Scope
The scope of the service worker determines from which path it will intercept requests. The default scope is the path to the service worker file. If service-worker.js is located in the root directory, the service worker will control requests from all files at the domain. You can set an arbitrary scope by passing an extra parameter while registering:

```javascript
navigator.serviceWorker.register('service-worker.js', {
 scope: '/app/'
});
```

## Installation and activation
Service workers are event driven. The installation and activation processes fire off corresponding install and activate events to which the service workers can respond.

With the service worker registered, the first time a user hits your PWA, the install event will be triggered and this is where you’ll want to cache the static assets for the page. This happens if the service worker is considered new, either because this is the first service worker encountered for the page or there’s a byte-difference between the current service worker and the previously installed one. install is the point when you can cache anything before getting a chance to control clients.

We could add very basic caching to a static app using the following code:

```javascript
var CACHE_NAME = 'my-pwa-cache-v1';
var urlsToCache = [
  '/',
  '/styles/styles.css',
  '/script/webpack-bundle.js'
];

self.addEventListener('install', function(event) {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(function(cache) {
        // Open a cache and cache our files
        return cache.addAll(urlsToCache);
      })
  );
});
```

addAll() takes an array of URLs, requests, fetches them and adds them to the cache. If any fetch/write fails, the op fails and the cache gets returned to its last state.

## Intercepting and caching requests

When a service worker controls a page, it can intercept each request being made by the page and decide what to do with it. This makes it a lot like a background proxy. We can use this to intercept requests to our urlsToCache and return the locally cached versions of assets instead of having to go back to the network. We can do this by attaching a handler to the fetch event:

```javascript
self.addEventListener('fetch', function(event) {
    console.log(event.request.url);
    event.respondWith(
        caches.match(event.request).then(function(response) {
            return response || fetch(event.request);
        })
    );
});
```

## Other stuff
* [Push](http://w3c.github.io/push-api/)
* [Background sync](https://github.com/slightlyoff/BackgroundSync)
* [Geofencing](https://github.com/slightlyoff/Geofencing)
* https://jakearchibald.com/2014/offline-cookbook/
* https://michalzalecki.com/progressive-web-apps-with-webpack/
* https://developers.google.com/web/fundamentals/instant-and-offline/service-worker/lifecycle
* https://developers.google.com/web/updates/2015/12/background-sync?hl=en
* https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API
* https://developer.mozilla.org/en-US/docs/Web/API/Cache
* https://serviceworke.rs/
