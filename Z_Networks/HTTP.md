## Basics
- HTTP/0.9 1991: GET is only method, all is written in HTML
- HTTP/1.0 1996: GET, POST, Headers, Status Codes
- HTTP/1.1 1999-2007: Cache Control, Compression, Host Header (multiple sites per IP)
- HTTP/2.0 2012: 
   - Multiplexing
     - HTTP/1.1
        - Can handle 1 request per connection
        - Safari, Chrome, Firefox open 6 connections to same server
        - Only 6 requests in flight at the same time possible
     - HTTP/2
        - Can handle several requests all at once over 1 connection 
   - Better Compression
   - Server Push
     -  Browser fetches HTML firstly
     -  Subsequently other resources (css, images etc.)
     -  Server Push: All resources are sent at once

## Methods

Method | Explanation
------ | -----------
GET | following a link
POST | Submit data
PUT | Creating new resources / Storing file on disk & adding records to database / GET requests will yield "201 Created" / requires authenticated user
DELETE | Counterpart of PUT / GET requests will yield "404 Not Found" / requires authenticated user
PATCH | Relatively new addition to HTTP / patching resource in some well-defined way
HEAD | Works like GET, except the server doesn't return any content — just headers
OPTIONS | Can be used to find out what features the server supports
TRACE | Echoes back what the server received from the client / is often disabled for security reasons

## Status Codes
- Status Code 200 OK
- Status Code 201 Created
- Status Code 202 Accepted
- Status Code 301 Moved Permanently
- Status Code 302 Not Found (Moved Temporarily)
- Status Code 304 Not Modified

#### Client
- Status Code 400 Bad Request
- Status Code 401 Unauthorized 
- Status Code 403 Forbidden
- Status Code 404 Not Found
- Status Code 410 Gone
- Status Code 415 Unsupported Media Type

#### Server
- Status Code 500 Internal Server Error
- Status Code 501 Not Implemented
- Status Code 502 Bad Gateway
- Status Code 503 Service Unavailable
