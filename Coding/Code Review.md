## DIFFERENT APPROACHES
1. Look at all classes/functions (**Best coverage but time consuming!**)
2. Top Down: Look at functions with user input and follow the embedded function/method calls to the bottom
3. Bottom Up: Look at functions without other function calls and got to top
4. Look for specific function(e.g. Create User Account): Look at how it is implement connected with other functions (**Recommended**)

<br />

## WHAT TO ASK YOURSELF #1 (grepping for vulnerabilities)
- Are there hardcoded credentials? 
  - Open your favorite code editor and hit the search functionality
  - `password` | `secret` | `credentials` | `token` | `hash`  
- Are dangerous functions used?
  - The keywords depend on the underlying codebase
  - Check out the respective framework docs
  - Check out the respective known security best practices, if any ([Example Angular](https://angular.io/guide/security))
  - After gathering malicious keywords start grepping them from the source code
  - `exec()` | `system()` | `open()` | `eval()` | `<script src` | `bypassSecurity` | `trust` | `safe` ...
- Is the application subject to outdated dependencies (direct / transitive)? 
  - **Node.js**
    - `/routes/index.js`: Learn the structure of the code
    - `/package.json` / `/package-lock.json`: Get an overview about required packages
    - `npm audit --no-color > audit.txt`: get an overview about vulnerabilities, but check manually for false positives  
- Where are input streams (sources)? 
  - Follow the data flow from your findings mentioned above
  - `data feeds` | `files` | `events` | `data responses from other systems` | `cookies` | `environment variables`
  - **Node.js/JS/HTML**
    - `req.body` | `innerhHTML`
- Where are output streams (sinks)? 
  - Follow the data flow from your findings mentioned above
  - **PHP**
    - `exec()` | `system()`
  - **Ruby**
    - `open()`

<br />

## WHAT TO ASK YOURSELF #2 (comprehensive review of high-risk components)
- How are authentication controls implemented?
  - 2MFA | OAuth | JWT
- How are authorization controls implemented?
- How is sensitive data encrypted?
- How are encryption keys handled?
- Do error messages display sensitive information to the user?
- What protection is implemented against SQL Injection?
- What protection is implemented against XXS?
- What if code is executed from two different users at exact same time (w/o logging)?
- What kind of filtering is in place? Is it sufficient?
- Are function flags corretly set? (look at framework/code DOCs to study available flags)
- Are cryptography libraries implemented acc. to best practices or developer-custom-solution?
- What type of hash functions are used and how are they implemented?

