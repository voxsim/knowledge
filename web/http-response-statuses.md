## 1×× Informational
- 100 Continue
  This interim response indicates that everything so far is OK and that the client should continue with the request or ignore it if it is already finished.

## 2×× Success
- 200 OK
  The request has succeeded. The meaning of a success varies depending on the HTTP method:
  GET: The resource has been fetched and is transmitted in the message body.
  HEAD: The entity headers are in the message body.
  POST: The resource describing the result of the action is transmitted in the message body.
  TRACE: The message body contains the request message as received by the server
- 201 Created
  The request has succeeded and a new resource has been created as a result of it. This is typically the response sent after a PUT request.
- 202 Accepted
  The request has been received but not yet acted upon. It is non-committal, meaning that there is no way in HTTP to later send an asynchronous response indicating the outcome of processing the request. It is intended for cases where another process or server handles the request, or for batch processing.
- 204 No content
  There is no response body. We can use when we have PUT, DELETE.
- 207 Multi-Status
  The response body contains multiple status informations for different parts of a batch/bulk request
  
## 3×× Redirection
- 300 Multiple Choices
  The request has more than one possible responses. User-agent or user should choose one of them. There is no standardized way to choose one of the responses.
- 301 Moved Permanently
  This response code means that URI of requested resource has been changed. Probably, new URI would be given in the response.
- 302 Found
  This response code means that URI of requested resource has been changed temporarily. New changes in the URI might be made in the future. Therefore, this same URI should be used by the client in future requests.
- 303 See Other
  Server sent this response to directing client to get requested resource to another URI with an GET request.
- 304 Not Modified
  This is used for caching purposes. It is telling to client that response has not been modified. So, client can continue to use same cached version of response.

## 4×× Client Error
- 400 Bad Request
  This response means that server could not understand the request due to invalid syntax.
- 401 Unauthorized
  Authentication is needed to get requested response. This is similar to 403, but in this case, authentication is possible.
- 403 Forbidden
  Client does not have access rights to the content so server is rejecting to give proper response.
- 404 Not Found
  Server can not find requested resource. This response code probably is most famous one due to its frequency to occur in web.
- 405 Method Not Allowed
  The request method is known by the server but has been disabled and cannot be used. The two mandatory methods, GET and HEAD, must never be disabled and should not return this error code.
- 429 Too many requests
  The client does not consider rate limiting and sent too many requests.

## 5×× Server Error
- 500 Internal Server Error
  The server has encountered a situation it doesn't know how to handle.
- 501 Not Implemented
  The request method is not supported by the server and cannot be handled. The only methods that servers are required to support (and therefore that must not return this code) are GET and HEAD.
- 502 Bad Gateway
  This error response means that the server, while working as a gateway to get a response needed to handle the request, got an invalid response.
- 503 Service Unavailable
  The server is not ready to handle the request. Common causes are a server that is down for maintenance or that is overloaded. Note that together with this response, a user-friendly page explaining the problem should be sent. This responses should be used for temporary conditions and the Retry-After: HTTP header should, if possible, contain the estimated time before the recovery of the service. The webmaster must also take care about the caching-related headers that are sent along with this response, as these temporary condition responses should usually not be cached.

For more info: https://httpstatuses.com/
