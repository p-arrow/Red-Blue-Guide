## Technologies

**Postback**
- Document Initiator type
- WebApp reloads whole page 
- NW traffic monitoring can be lost if you don't enable persistent logs

**AJAX (Asynchronous JavaScript and XML)**
- XHR Initiator type
- Decouples data interchange layer from the presentation layer
- Changes content dynamically without reload entire page
- Commonly utilized with JSON (i/o XML)

**XHR (XMLHttpRequests)**
- API in form of an object
- Requires JS enabled in web browser
- Can be used with other protocols than HTTP/XML (e.g. JSON, HTML, Plain Text)

**OAuth V2**
- Often used together with OpenID
- Delegated authorization framework for RESTful APIs-
- Enables Apps to obtain access w/o giving away user's password
- Four Parties Involed
   - Clients: Apps that User wants to use
   - Resource owners: End User
   - Resource servers: Provided by service that User wants to use
   - Auth servers: Servers owned by ID provider

**JWT (JSON Web Tokens)**
- Token contains header / payload / signature (JSON object)
- Normally transmitted via URL and Base64 encoded
- Created by Server during Authen
- Handed over to Client (w/o saving @Server)
- Server maintains Integrity of JWT through digital signature
