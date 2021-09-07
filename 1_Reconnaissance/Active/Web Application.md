*--> [Z_Networks/Web Application.md](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Z_Networks/Web%20Application.md)*

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
