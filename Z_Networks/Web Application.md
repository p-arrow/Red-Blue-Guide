## Technologies

#### Postback
- Document Initiator type
- WebApp reloads whole page 
- NW traffic monitoring can be lost if you don't enable persistent logs

#### AJAX (Asynchronous JavaScript and XML)
- XHR Initiator type
- Decouples data interchange layer from the presentation layer
- Changes content dynamically without reload entire page
- Commonly utilized with JSON (i/o XML)

#### XHR (XMLHttpRequests)
- API in form of an object
- Requires JS enabled in web browser
- Can be used with other protocols than HTTP/XML (e.g. JSON, HTML, Plain Text)

#### OAuth V2
- Often used together with OpenID
- Delegated authorization framework for RESTful APIs-
- Enables Apps to obtain access w/o giving away user's password
- Four Parties Involed
   - Clients: Apps that User wants to use
   - Resource owners: End User
   - Resource servers: Provided by service that User wants to use
   - Auth servers: Servers owned by ID provider

#### JWT (JSON Web Tokens)
- Token contains header / payload / signature (JSON object)
- Normally transmitted via URL and Base64 encoded
- Created by Server during Authen
- Handed over to Client (w/o saving @Server)
- Server maintains Integrity of JWT through digital signature

#### SOAP (Simple Object Access Protocol)

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

#### REST (Representational State Transfer)

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


