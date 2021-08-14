### Successful responses
#### 200 OK
The request has succeeded. The meaning of the success depends on the HTTP method:
 * GET: The resource has been fetched and is transmitted in the message body.
 * HEAD: The representation headers are included in the response without any message body.
* PUT or POST: The resource describing the result of the action is transmitted in the message body.
* TRACE: The message body contains the request message as received by the server.
#### 201 Created
The request has succeeded and a new resource has been created as a result. This is typically the response sent after POST requests, or some PUT requests.
#### 202 Accepted
The request has been received but not yet acted upon. It is noncommittal, since there is no way in HTTP to later send an asynchronous response indicating the outcome of the request. It is intended for cases where another process or server handles the request, or for batch processing.
#### 203 Non-Authoritative Information
This response code means the returned meta-information is not exactly the same as is available from the origin server, but is collected from a local or a third-party copy. This is mostly used for mirrors or backups of another resource. Except for that specific case, the "200 OK" response is preferred to this status.
#### 204 No Content
There is no content to send for this request, but the headers may be useful. The user-agent may update its cached headers for this resource with the new ones.
#### 205 Reset Content
Tells the user-agent to reset the document which sent this request.
<hr/>

### Client error responses
#### 400 Bad Request
The server could not understand the request due to invalid syntax.
#### 401 Unauthorized
Although the HTTP standard specifies "unauthorized", semantically this response means "unauthenticated". That is, the client must authenticate itself to get the requested response.
#### 402 Payment Required 
This response code is reserved for future use. The initial aim for creating this code was using it for digital payment systems, however this status code is used very rarely and no standard convention exists.
#### 403 Forbidden
The client does not have access rights to the content; that is, it is unauthorized, so the server #### is refusing to give the requested resource. Unlike 401, the client's identity is known to the server.
#### 404 Not Found
The server can not find the requested resource. In the browser, this means the URL is not recognized. In an API, this can also mean that the endpoint is valid but the resource itself does #### not exist. Servers may also send this response instead of 403 to hide the existence of a resource from an unauthorized client. This response code is probably the most famous one due to its frequent occurrence on the web.
#### 405 Method Not Allowed
The request method is known by the server but has been disabled and cannot be used. For example, an API may forbid DELETE-ing a resource. The two mandatory methods, GET and HEAD, must never be disabled and should not return this error code.

#### 408 Request Timeout
This response is sent on an idle connection by some servers, even without any previous request by the client. It means that the server would like to shut down this unused connection. This response is used much more since some browsers, like Chrome, Firefox 27+, or IE9, use HTTP pre-connection mechanisms to speed up surfing. Also note that some servers merely shut down the connection without sending this message.

## References
1. https://developer.mozilla.org/en-US/docs/Web/HTTP/Status
2. 