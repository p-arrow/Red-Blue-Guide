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
