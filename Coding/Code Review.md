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
- Improper usage of malicious code identified?
- Code relying on user-controlled data?
- Control over arguments?
- What if code is executed from two different users at exact same time (w/o logging)?
- Filtering in place?
- Sufficient filtering in place?
- Functions flags corretly set? (look at DOCs to study available flags)
- Implementation of Cryptography Libs acc. to best practices or developer-custom-solution?
- Selection and implementation of hash functions correct?

## Node.js/Javascript
- `routes/index.js`: Learn the structure of the code
- `package.json`: Get an overview about used packages
  - `npm audit`: run this command in VS Code Terminal to get an overview about vulnerabilities
  - Check manually to recognize false positives 
- Important Keywords:
  - `open` 
  - `req.body`
  - `innerhHTML`
