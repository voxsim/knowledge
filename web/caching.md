## Cache-Control

Cache-Control defines how, and for how long the individual response can be cached by the browser and other intermediate caches.
When your browser requests resources from a server the first time, it stores the returning resources in its cache according to
this header.
These resources can be of any file type, but are usually HTML, stylesheets, scripts, or images. Then, when your 
browser needs to request that resource again, it will check its cache to see if the resource is there and that it still fits 
the Cache-Control specs; if it does, then your browser will just load that resource from cache and completely avoid having to 
make a request to the server. Ultimately, this ends up saving you many requests that would likely have been made to servers 
halfway around the world.

The Cache-Control header has a couple different parameters that can be set from the server:

* “no-cache” or “no-store”: no-cache means that regardless of the Cache-Control header, this resource should always be requested from the server instead of automatically loaded from cache. However, the protocol about ETags still applies (more on that below), and if the ETags for the client version and the server version match up (thus indicating no change), then the server will instruct the client to use its cached version. Often times you use this setting for HTML files, since you always want these to be up-to-date because they link to other resources. no-store is simpler in that it tells the browser to always request the resource from the server without checking ETags, thus always forcing a full-length download from the server.
* “public” or “private”: public means that a resource can be cached by anyone – but this usually isn’t necessary as by default, defining the max-age part of the header will also set it as public (unless private is explicitly stated). private means that only the user’s browser can cache the resource, and not any intermediaries such as a CDN. This is especially important when dealing with resources with personal information, such as when you log into your bank’s website.
* “max-age”: Finally, max-age determines the length of time in seconds that this resource should be cached. max-age=120 means that this resource can be cached and reused for 2 minutes.

## Etag
The ETag header (short for entity-tag) provides a revalidation token that is automatically sent by the browser to check if 
the resource has changed since the last time it was requested.
Your browser completely ignores the ETag header until it needs to access a resource that falls outside the cache bounds set
in the Cache-Control header. Normally, if we fall inside the Cache-Control bounds, then the server is never requested for
this resource – it’s all loaded from cache internally in the browser. With ETags, we do have to make a request to the server,
but instead of re-downloading the entire resource, our goal is to check with the server to see if there’s been any
modifications to it. If there haven’t been, then the server responds back with a 304 response code – meaning “Not-Modified” –
and then the browser loads the file from its own cache instead. While using ETags does involve a request to the server,
if it works as intended, then we don’t have to needlessly download the same resource again, and the response is handled much
quicker.

An ETag is basically a random string that a server assigns to a resource, and reassigns it whenever that resource changes.

## Proper cache-policy
- Reusable Response?
  - No -> no-store
  - Yes
    - Revalidate each time? Yes -> no-cache
    - Cachable by intermediate? Yes/no -> public/private
    - maximum cache lifetime? max_age and add etag

# Pre-HTTP 1.1 headers (died)
- Expires
- Last-Modified
