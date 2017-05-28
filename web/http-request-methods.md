HTTP defines a set of request methods to indicate the desired action to be performed for a given resource. Although they can also be nouns, these request methods are sometimes referred to as HTTP verbs. Each of them implements a different semantic, but some common features are shared by a group of them: e.g. a request method can be safe, idempotent, or cacheable.

## Safe Methods

Request methods are considered "safe" if their defined semantics are essentially read-only; i.e., the client does not request, and does not expect, any state change on the origin server as a result of applying a safe method to a target resource.  Likewise, reasonable use of a safe method is not expected to cause any harm, loss of property, or unusual burden on the origin server.

## Idempotent Methods
 A request method is considered "idempotent" if the intended effect on the server of multiple identical requests with that method is the same as the effect for a single such request.  Of the request methods defined by this specification, PUT, DELETE, and safe request methods are idempotent.
 
## Cachable Methods
Request methods can be defined as "cacheable" to indicate that responses to them are allowed to be stored for future reuse

## GET
The GET method requests a representation of the specified resource. Requests using GET should only retrieve data.
- Request has body	No
- Successful response has body	Yes
- Safe	Yes
- Idempotent	Yes
- Cacheable	Yes
- Allowed in HTML forms	Yes 

## HEAD
The HEAD method asks for a response identical to that of a GET request, but without the response body.
The HTTP HEAD method requests the headers that are returned if the specified resource would be requested with an HTTP GET method.
Such a request can be done before deciding to download a large resource to save bandwidth, for example.

A response to a HEAD method should not have a body. If so, it must be ignored. Even so, entity headers describing the content of the body, like Content-Length may be included in the response. They don't relate to the body of the HEAD response, which should be empty, but to the body of similar request using the GET method would have returned as a response.

If the result of a HEAD request shows that a cached resource after a GET request is now outdated, the cache is invalidated, even if no GET request has been made.

Request has body	No
Successful response has body	No
Safe	Yes
Idempotent	Yes
Cacheable	Yes
Allowed in HTML forms	No

## POST
The POST method is used to submit an entity to the specified resource, often causing a change in state or side effects on the server
The HTTP POST method sends data to the server. The type of the body of the request is indicated by the Content-Type header.

The difference between PUT and POST is that PUT is idempotent: calling it once or several times successively has the same effect (that is no side effect), where successive identical POST may have additional effects, like passing an order several times.

A POST request is typically sent via an HTML form and results in a change on the server. In this case, the content type is selected by putting the adequate string in the enctype attribute of the <form> element or the formenctype attribute of the <input> or <button> elements:
- application/x-www-form-urlencoded: the values are encoded in key-value tuples separated by '&', with a '=' between the key and the value. Non-alphanumeric characters are percent encoded: this is the reason why this type is not suitable to use with binary data (use application/form-data instead)
- application/form-data
- text/plain
When the POST request is sent via another method that an HTML form, like via an XMLHttpRequest, the body can take any type. 
As described in the HTTP 1.1 specification, POST is designed to allow a uniform method to cover the following functions:
- Annotation of existing resources
- Posting a message to a bulletin board, newsgroup, mailing list, or similar group of articles;
- Providing a block of data, such as the result of submitting a form, to a data-handling process;
- Extending a database through an append operation.

Request has body	Yes
Successful response has body	Yes
Safe	No
Idempotent	No
Cacheable	Only if freshness information is included
Allowed in HTML forms	Yes

## PUT
The PUT method replaces all current representations of the target resource with the request payload.
The HTTP PUT request method creates a new resource or replaces a representation of the target resource with the request payload.

The difference between PUT and POST is that PUT is idempotent: calling it once or several times successively has the same effect
(that is no side effect), where successive identical POST may have additional effects, like passing an order several times.

Request has body	Yes
Successful response has body	No
Safe	No
Idempotent	Yes
Cacheable	No
Allowed in HTML forms	No

## DELETE
The DELETE method deletes the specified resource.

Request has body	No
Successful response has body	No
Safe	No
Idempotent	Yes
Cacheable	No
Allowed in HTML forms	No

##CONNECT
The CONNECT method establishes a tunnel to the server identified by the target resource. It can be used to open a tunnel.

For example, the CONNECT method can be used to access websites that use SSL (HTTPS). The client asks an HTTP Proxy server to tunnel the TCP connection to the desired destination. The server then proceeds to make the connection on behalf of the client. Once the connection has been established by the server, the Proxy server continues to proxy the TCP stream to and from the client.

CONNECT is a hop-by-hop method.

Request has body	Yes
Successful response has body	Yes
Safe	No
Idempotent	No
Cacheable	No
Allowed in HTML forms	No

## OPTIONS
The OPTIONS method is used to describe the communication options for the target resource.
The HTTP OPTIONS method is used to describe the communication options for the target resource. The client can specify a specific URL for the OPTIONS method, or an asterisk (*) to refer to the entire server.

Request has body	No
Successful response has body	No
Safe	Yes
Idempotent	Yes
Cacheable	No
Allowed in HTML forms	No

## TRACE
The TRACE method performs a message loop-back test along the path to the target resource.

## PATCH
The PATCH method is used to apply partial modifications to a resource.
The HTTP PATCH request method applies partial modifications to a resource.

The HTTP PUT method is already defined to overwrite a resource with a complete new body, and for the POST method there is no standard way to discover patch format support. Unlike PUT, but like POST, PATCH is not idempotent, meaning successive identical patch requests will have different effects.

To find out whether a server supports PATCH, a server can advertise its support by adding it to the list in the Allow or Access-Control-Allow-Methods (for CORS) response headers.

Another (implicit) indication that PATCH is allowed, is the presence of the Accept-Patch header, which specifies the patch document formats accepted by the server.

Request has body	Yes
Successful response has body	No
Safe	No
Idempotent	No
Cacheable	No
Allowed in HTML forms	No
