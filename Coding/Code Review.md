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
  - Check out the respective **Framework Docs**
  - Check out the respective known **Security Best Practices**
    - [https://angular.io/guide/security](https://angular.io/guide/security)
    - [https://guides.rubyonrails.org/security.html](https://guides.rubyonrails.org/security.html)
  - Source Code Signatures: [https://github.com/wireghoul/graudit/tree/master/signatures](https://github.com/wireghoul/graudit/tree/master/signatures)
  - RegEx Pattern Search: [https://semgrep.dev/r](https://semgrep.dev/r)
    - Install CLI locally: `python3 -m pip install semgrep`
    - Pick one specific rule: Search for code language (`php`) or keyword (`exec`)
    - Pick a comprehensive rule-set
    - Copy the semgrep command , for instance: `semgrep --config "p/jwt"`
    - Terminal: `semgrep --config "p/jwt" path/to/src`
    - Basic Explanation also here: [https://semgrep.dev/docs/running-rules/](https://semgrep.dev/docs/running-rules/)
  - After gathering malicious keywords start grepping them from the source code
  - `exec()` | `system()` | `open()` | `eval()` | `<script src` | `bypassSecurity` | `trust` | `safe` | `unsafe` ...
- Is the application subject to **outdated dependencies** (direct / transitive)? 
  - **Node.js**
    - `/routes/index.js`: Learn the structure of the code
    - `/package.json` / `/package-lock.json`: Get an overview about required packages
    - `npm audit --no-color > audit.txt`: get an overview about vulnerabilities, but check manually for false positives  
- Let's take a shortcut with **Static Code Analyzers**
    - **JAVA** --> **FindBugs**
      - [http://findbugs.sourceforge.net/index.html](http://findbugs.sourceforge.net/index.html)
      - Download: [http://prdownloads.sourceforge.net/findbugs/findbugs-3.0.1.tar.gz?download](http://prdownloads.sourceforge.net/findbugs/findbugs-3.0.1.tar.gz?download)
      - `gunzip -c findbugs-3.0.1.tar.gz | tar xvf -`
      - `java [JVM arguments] -jar $FINDBUGS_HOME/lib/findbugs.jar options FILE.jar`
      - Details about Options: [http://findbugs.sourceforge.net/manual/running.html](http://findbugs.sourceforge.net/manual/running.html)
      - Additional Security Plugin: [https://find-sec-bugs.github.io/](https://find-sec-bugs.github.io/)
    - **PYTHON** --> **Bandit**
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
- Are **user interactions uniquely linked** to that user?
  - User may have an ambiguous name, email oder other parameter that can lead to vague DB lookups etc. 
