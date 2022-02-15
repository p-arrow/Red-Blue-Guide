## General
### What to look at (except code itself)?
- Framework Docs
- Respective code security best practices
- Malicious keywords known in respective code base

### How to progress?
1. Look at all classes/functions (**Best coverage but time consuming!**)
2. Top Down: Look at functions with user input and follow the embedded function/method calls to the bottom
3. Bottom Up: Look at functions without other function calls and got to top
4. Look for specific function(e.g. Create User Account): Look at how it is implement connected with other functions (**Recommended**)

### What to ask yourself?
- Where are Input/Output boundaries within the code? 
  - data feeds
  - files
  - events
  - data responses from other systems
  - cookies
  - environment variables
- How are authentication controls implemented?
  - 2MFA?
  - OAuth?
  - JWT? 
- How are authorization controls implemented?
- How is sensitive data encrypted?
- How are encryption keys handled?
- How do error messages display sensitive information to the user?
- What protections are implemented against SQL Injection?
- What protections are implemented against XXS?
- What if code is executed from two different users at exact same time (w/o logging)?
- What kind of filtering is in place? Is it sufficient?
- Are function flags corretly set? (look at framework/code DOCs to study available flags)
- Are Cryptography Libraries implemented acc. to best practices or developer-custom-solution?
- What type of hash functions are used and how are they implemented?

## Node.js/Javascript
- `/routes/index.js`: Learn the structure of the code
- `/package.json`: Get an overview about used packages
- `npm audit --no-color > audit.txt`: get an overview about vulnerabilities, but check manually for false positives 
- Important Keywords:
  - `open` 
  - `req.body`
  - `innerhHTML`
