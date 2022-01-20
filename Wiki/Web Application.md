1. [BASICS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Networks/Web%20Application.md#basics)
2. [WEB TECHNOLOGIES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Networks/Web%20Application.md#web-technologies)

## BASICS
### URL Encoding
- Encodes 8bit characters that have specific meaning for URLs
- URL contains **reserved characters** `: / ? # @ % $ & ! ' ( ) , ; =`
- URL contains **unreserved characters** `a-z, A-Z, 0-9`
- URL cannot contain **unsafe characters**: `\ < > { } space`
- Can be misused to obfuscate the nature of URL (malicious script !)

![image](https://user-images.githubusercontent.com/84674087/150371312-03b97345-484c-4caf-b09d-faef2f3fc53b.png)

### Chunk Encoding
- The server can send content without waiting for the full response to be ready
- The server sends the size of a chunk (in hexadecimal) followed by the chunk
- Therefore no Content-Length header in HTTP traffic

### URI (Uniform Ressource Identifier)
1. **URL is like URI, but for resources on the web**
2. URI scheme: http, https, file, mailto, data ...
3. Hostname: en.wikipedia.org
4. Path: /wiki/Fish
- `:` --> goes always after URI scheme
- `//` --> goes always before hostname
- `#` --> Fragment (all text with prepended # is NOT sent to servers. Often used for DOM XSS Attacks !)
- Same Origin: If scheme, hostname and port are identical
- **Examples**
   - mailto:spam@example.net
   - https://www.google.com
   - https://en.wikipedia.org/wiki/Oxygen#Discovery

### HTTP
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
- HTTP Status Codes:
   - Status Code 200 OK
   - Status Code 201 Created
   - Status Code 202 Accepted
   - Status Code 301 Moved Permanently
   - Status Code 302 Not Found (Moved Temporarily)
   - Status Code 304 Not Modified
- **Client Status Codes**
   - Status Code 400 Bad Request
   - Status Code 401 Unauthorized 
   - Status Code 403 Forbidden
   - Status Code 404 Not Found
   - Status Code 410 Gone
   - Status Code 415 Unsupported Media Type
- **Server Status Codes**
   - Status Code 500 Internal Server Error
   - Status Code 501 Not Implemented
   - Status Code 502 Bad Gateway
   - Status Code 503 Service Unavailable

#### HTTP Methods
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

<br />

## WEB TECHNOLOGIES
### Cookie Flags
- **Security Attribute**
   - If Activated: User agent includes Cookie only via HTTPS (Forcing WebAppOverTSL does not automatically include Cookie)
- **Max Age**
   - If Activated: Deletion of Cookie after specified life time
- **HttpOnly Attribute**
   - If Activated: Cookie is inaccessible to JS Document.cookie API
   - Mitigates XSS Attackes
- **Domain Attribute**
   - If Activated: Specifies which hosts are allowed to receive the cookie
- **Path Attribute**
   - If Activated: Specifies URL Path that must exist in the requested URL in order to send Cookie

### Same Site
- Same Origin != Same Site
- SameOriginPolicy (SOP) prevents Third Party from reading
- SOP does NOT prevent writing/sending of Cookies by Third Parties 
- Effective TopLevelDomains+1 (eTLD+1) accounts as Same Site
- Domain Attribute and Same Site Attribute define security level
   - **strict**: Cookies are sent to Same Site only
   - **lax**: Cross Site is partly allowed
   - **none**: Both Same Site and Cross Site are possible
- If Domain Attribute is empty: Host Only Cookie is set automatically

### Postback
- Document Initiator type
- WebApp reloads whole page 
- NW traffic monitoring can be lost if you don't enable persistent logs

### AJAX (Asynchronous JavaScript and XML)
- XHR Initiator type
- Decouples data interchange layer from the presentation layer
- Changes content dynamically without reload entire page
- Commonly utilized with JSON (i/o XML)

### XHR (XMLHttpRequests)
- API in form of an object
- Requires JS enabled in web browser
- Can be used with other protocols than HTTP/XML (e.g. JSON, HTML, Plain Text)

### OAuth V2
- Often used together with OpenID
- Delegated authorization framework for RESTful APIs-
- Enables Apps to obtain access w/o giving away user's password
- Four Parties Involed
   - Clients: Apps that User wants to use
   - Resource owners: End User
   - Resource servers: Provided by service that User wants to use
   - Auth servers: Servers owned by ID provider

### JWT (JSON Web Tokens)
- Token contains header / payload / signature (JSON object)
- Normally transmitted via URL and Base64 encoded
- Created by Server during Authen
- Handed over to Client (w/o saving @Server)
- Server maintains Integrity of JWT through digital signature

### SOAP (Simple Object Access Protocol)

*XML-based web service protocol*

- Used for:
    - Exchange asynchronous messages
    - Authentication
    - Transport security
    - Built-in error handling
    - Often used with SAML for ID management

- Existing Vulns of SOAP:
    - Probing: Enumeration against the web service
    - Coercive Parsing: modifies SOAP requests -> malicious XML parsing
    - External References
    - Malware: Consider input validation!
    - SQL Injection: Avoid transmitting SQL statements over SOAP

### REST (Representational State Transfer)
1. Stateless Protocol
2. Simple alternative to SOAP (because less restrictive)
3. Five principles (i/o defined implementation)
   - Client-Server-Architecture
   - Stateless (enhances scalability)
   - (HTTP) Caching
   - Multilayer system (1x client interface sufficient)
   - Uniform interface 
      - Ressource access via URI
      - Representation of ressource change (HTML, JSON, XML)
      - self-writing messages (via standard methods)
      - "Hypermedia as the Engine of Application State" (HATEOAS)
4. REST-conformity often matched along with WWW (XML, HTTP, CSV, JSON)
5. Does not provide encryption. HTTPS recommended (!)
6. Versioning via DNS / URL / HTTP-Header (mostly URL)
   - http://foo.com/api/v2.0/customer/1234
   - http://foo.com/api/v2.2/customer/1234

### Same Origin Policy (SOP)
> Imagine that you open Website A and Website B in your browser. SOP prevents Website A from reading content of Website B and vice versa.

- SOP is enforced by your browser, and influenced by server
    - If you use an API which is accessed directly (w/o browser) you need other defense layers: Authentication, Rate-limiting, Captchas etc. 
- Open any website (e.g. websitea.com), open WebDev Tool, go to Console and enter:
    - `var fee = window.open('https://www.websitea.com', 'right')`
    - This opens websitea.com in another tab 
    - Then enter on current website A: `fee.document.body.innerHTML='hello'`
    - This code works only when website A has same origin as website A (which is obviously the case) 
    - If not, SOP prevents execution
    - The second tab with websitea.com has a reference to your current webiste A, so called "window opener"
    - You cannot change the content of website A, but the location: `window.opener.location='www.google.de'`
- **Local Storage** is accessible from sites with same origin, e.g. open website A in several tabs and they all have access to the same local storage
- Contrary to SOP, **Cookies** are identified by name / domain / path
    - name = value; domain = example.com; path = /  
    - This means cookies don't compare URI scheme or port (!)
    - Cookies can be shared among subdomains
- **Frames** can only access content of frames with same origin  +navigate other frames
    - Parent frame: `window.frames[0].location` 
    - Child frame: `window.parent`, `window.top`
    - Windows: `window.opener`, `var x = window.open(...)`
- **XHR**: One can send requests to other sites (from website A) but SOP prevents to see the response (from website B)
    - `var xhr = new XMLHttpRequest()`
    - `xhr.open("GET", "https://www.websitea", "false")` 
    - `xhr.send()` --> this works 
    - `xhr.open("GET", "https://www.websiteb", "false")` 
    - `xhr.send()` --> this don't work thus you don't have access to the response
- **CORS** (Cross-Origin Resource Sharing) allows a site to "opt-in" to weakening SOP and allow other sites to read data
    - If website A requests data from website B, then website B must enforce an exception
    - Sender: uses XHR
    - Receiver: uses CORS --> Access-Control-Allow-Origin: http://websitea.com

![grafik](https://user-images.githubusercontent.com/84674087/137503278-1decbb67-ae8f-4c75-8e22-bff3f978aa22.png)

