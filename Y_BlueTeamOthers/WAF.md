*Web Application Firewall*

## Characteristic

1. Language: Often JSON format logs
2. Logs: time/severity of event, URL parameters, HTTP method
3. Layer: Application Layer (HTTP/HTTPS)
4. Deployment: As Reverse Proxy in front of Web Server
5. Protection against injections / malicious API requests (OWASP Top10)

## Stateless WAF
- Based on static signatures
- Exp: Block %27 (') within a URL request

## Stateful WAF
- Based on signature, patterns and heuristic data
- Exp: Block Hex obfuscation (737472696E67) in conjunction with IP reputation
   - IP Reputation: DB of known IP addresses used in the past
