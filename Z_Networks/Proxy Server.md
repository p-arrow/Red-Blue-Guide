## Functions

1. IP Proxy (hiding original IP)
2. Caching Proxy
3. Content filter
4. Web Security Gateway (DLP, IDS, AV etc)

## Types

### Nontransparent

- Redirects requests/responses for clients 

### Transparent

- Redirects requests/responses w/o client being explicitely configured to use it
- ISPs can use transparent proxies to log user data (!)

### Forward Proxy
- Mediates traffic from client to server
- Can filter, modify and caching
- Logs HTTP requests/content

### Reverse proxy
- Protects servers from direct contact with client requests
- Logs can be analyzed as IoC (malicious HTTP requests/URLs)

### SSL Proxy
- Guaranteed encryption only between Proxy and destination

### CGI proxy = Web Proxy
- Like a website where you enter the destination address
- You will enter the destination anonymously, but likely with ads
- When clicking on destination's links the traffic will go through the proxy
- Destinations might not work properly when entering through proxy (JavaScript etc) (!)
- Destinations can try to kick out the proxy connection (IP leak!)
