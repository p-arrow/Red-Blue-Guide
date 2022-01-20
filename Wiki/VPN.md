## Pro
1. No SSL stripping (because SSL is not visible under VPN tunnel)
2. Geographical restriction bypass
3. Certain degree of annonymity because VPN's IPv4 is used
4. Get certificates from the VPN provider directly
   - VPN client only works with correct public key from VPNserver

## Con
1. Lower speed (but faster than Tor)
2. Just a piece of hidding your identity
3. It's obivous to an observer
4. Not free to use (money traceback possible!)
5. End2End correlation possible (client/destination packet analysis)
6. Higher latency
7. No protection against social engineering, fingerprinting, TCP timestamp attacks
8. VPN can be blocked at destination (Netflix etc.)
9. Encryption only from VPN client to VPN Server; not to final dest (!)
10. VPN Leaks reveal your identity: DNS (Win10) / IPv6
11. Dropped VPN (but NW connection still remains)
    - Set up proper configuration
    - Disable all non VPN traffic via FireWall

## Pay attention to 
1. Warrant Canary
   - Confirmation of VPN Providers that no secret data queries from third parties exist
2. Data Retention Law
   - How long VPN Providers keep user data stored 

## Protocols

#### 1) PPTP/1723
- Point-to-Point Tunneling Protocol
- Developed by Microsoft, proprietary
- Uses CHAP-authentication, which makes it vulnerable
- Uses GRE to encapsulate PPP packets 

#### 2) L2TP/1701
- No encryption
- Uses fixed ports. Easy to block by NAT Firewall
- Easy to setup
- Usually paired with IPSec for security reasons

#### 3) SSTP (Secure Socket Tunneling Protocol)
- Developed by Microsoft, proprietary
- Not recommended, bad security

#### 4) IKEv2 (Internet Key Exchange)
- Developed by Microsoft and Cisco
- Good for mobile platforms
- Secure and fast

#### 5) IPSec

#### 6) OpenVPN
- User friendly
- TCP/UDP based
- Not natively supported, 3rd party sofware necessary
- Maybe not easy to configure for non-technical people
- Best Practice:
    - 2048 bit or 4096 bit RSA certificates
    - DHE-RSA-AES256-SHA for exchange of OpenVPN key
    - AES-256-CBC-SHA for data
