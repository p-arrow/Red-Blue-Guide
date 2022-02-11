## General
### What to look at besides the Code?
- Framework Docs !
- Respective code security best practices
- Respective (malicious) keywords known in code

### How to progress?
1. Look at all classes/functions (**Best coverage but time consuming!**)
2. Top Down: Look at functions with user input and follow the embedded function/method calls to the bottom
3. Bottom Up: Look at functions without other function calls and got to top
4. Look for specific function(e.g. Create User Account): Look at how it is implement connected with other functions (**Recommended**)

### What to ask yourself?
1. Dangerous Code identified?
2. Control over arguments?
3. Filtering in place?
4. Sufficient filtering in place?
5. Code is reachable?

## Node.js/Javascript
- `routes/index.js`: Learn the structure of the code
- `package.json`: Get an overview about used packages
  - `npm audit`: run this command in VS Code Terminal to get an overview about vulnerabilities
  - Check manually to recognize false positives 
- Important Keywords:
  - `open` 
  - `req.body`
  - `innerhHTML`
