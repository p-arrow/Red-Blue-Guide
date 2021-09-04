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

**SOAP (Simple Object Access Protocol)**

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
