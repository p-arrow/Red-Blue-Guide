
## URL Encoding

- Encodes 8bit characters that have specific meaning for URLs
- URL contains **reserved characters** `: / ? # @ % $ & ! ' ( ) , ; =`
- URL contains **unreserved characters** `a-z, A-Z, 0-9`
- URL cannot contain **unsafe characters**: `\ < > { } space`

- Allows to submit safe or unsafe character to server
- Can be misused to obfuscate the nature of URL (malicious script)
- Tricky attackers may apply double encoding to "%" too

**Encoding Codes**

Character | URL Encoding
--------- | ------------
null | %00
space | %20
\+ | %2B
% | %25
/ | %2F
\ | %5C
. | %2E
? | %3F
" | %22
' | %27
< | %3C
\> | %3E
: | %3A
@ | %40
; | %3B
= | %3D

<br />

## URI (Uniform Ressource Identifier)

*URL is like URI, but for resources on the web*

#### Syntax
1. URI scheme: http, https, file, mailto, data ...
2. Hostname: en.wikipedia.org
3. Path: /wiki/Fish
- `:` --> goes always after URI scheme
- `//` --> goes always before hostname
- `#` --> Fragment
- Same Origin: If scheme, hostname and port are identical

#### Examples
- mailto:spam@example.net
- https://www.google.com
- https://en.wikipedia.org/wiki/Oxygen#Discovery

<br />

## Cookie Flags

#### Security Attribute
- If Activated: User agent includes Cookie only via HTTPS (Forcing WebAppOverTSL does not automatically include Cookie)

#### Max Age
- If Activated: Deletion of Cookie after specified life time

#### HttpOnly Attribute
- If Activated: Cookie is inaccessible to JS Document.cookie API
- Mitigates XSS Attackes

#### Domain Attribute
- If Activated: Specifies which hosts are allowed to receive the cookie

#### Path Attribute
- If Activated: Specifies URL Path that must exist in the requested URL in order to send Cookie

#### Same Site
- Same Origin != Same Site
- SameOriginPolicy (SOP) prevents Third Party from reading
- SOP does NOT prevent writing/sending of Cookies by Third Parties 
- Effective TopLevelDomains+1 (eTLD+1) accounts as Same Site
- Domain Attribute and Same Site Attribute define security level
   - **strict**: Cookies are sent to Same Site only
   - **lax**: Cross Site is partly allowed
   - **none**: Both Same Site and Cross Site are possible
- If Domain Attribute is empty: Host Only Cookie is set automatically


## Web Technologies

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


