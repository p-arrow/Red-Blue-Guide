## DIFFERENT APPROACHES
1. Look at all classes/functions (**Best coverage but time consuming!**)
2. Top Down: Look at functions with user input and follow the embedded function/method calls to the bottom
3. Bottom Up: Look at functions without other function calls and got to top
4. Look for specific function(e.g. Create User Account): Look at how it is implement connected with other functions (**Recommended**)

<br />

## CHECKLIST (grepping for vulnerabilities)
- Are there **hardcoded credentials**? 
  - Open your favorite code editor and hit the search functionality
  - `password` | `secret` | `credentials` | `token` | `hash`  
- Are **dangerous functions** used?
  - The keywords depend on the underlying codebase
  - Check out the respective framework docs
  - Check out the respective known security best practices, if any ([Example Angular](https://angular.io/guide/security))
  - After gathering malicious keywords start grepping them from the source code
  - `exec()` | `system()` | `open()` | `eval()` | `<script src` | `bypassSecurity` | `trust` | `safe` | `unsafe` ...
- Is the application subject to **outdated dependencies** (direct / transitive)? 
  - **Node.js**
    - `/routes/index.js`: Learn the structure of the code
    - `/package.json` / `/package-lock.json`: Get an overview about required packages
    - `npm audit --no-color > audit.txt`: get an overview about vulnerabilities, but check manually for false positives  
- Where are **input streams** (sources)? 
  - Follow the data flow from your findings mentioned above
  - `data feeds` | `files` | `events` | `data responses from other systems` | `cookies` | `environment variables`
  - **Node.js/JS/HTML**
    - `req.body.` | `innerHTML`
- Where are **output streams** (sinks)? 
  - Follow the data flow from your findings mentioned above
  - **PHP**
    - `exec()` | `system()`
  - **Ruby**
    - `open()`
- What kind of **encryption** is used?
  - `MD4` | `MD5` | `RC4` | `RC2` | `DES` | `Blowfish` | `SHA-1` | `ECB`
  - Where and how are encryption keys stored/handled?
- What kind of **authentication controls** are implemented?
  - `2MFA` | `OAuth` | `JWT`
- What kind of **authorization controls** are implemented?
- Do **error messages** display sensitive information to the user?
- What kind of **input validation/filtering** (against SQLi, XSS etc.) is implemented? 
- What kind of **logging** is implemented?
  - Are replay attacks possible?
  - What if code is executed from two different users at exact same time?
- Are **function flags** corretly set?
  - Look at framework/code DOCs to study available flags

