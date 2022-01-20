*IOC = Indicator of Compromise*

## Types
### 1) Traffic Spikes
- High number of TIME_WAIT connections in load balancer
- High number of HTTP 503 Service Unavailable logs
- Unexpected high outbound traffic could indicate victimized hosts in NW

### 2) DDoS

**> [3_Exploitation/Denial of Service(DoS)](https://github.com/p-arrow/Red-Blue-Guide/blob/main/3_Exploitation/Denial%20of%20Service%20(DoS).md)**

### 3) Irregular P2P Communication
1. Normally between Client/Server
2. Direct Client2Client (via SMB) is suspicious
   - Investigate with Network Sniffer
3. Layer2 ARP Poisoning generates more traffic than usual
   - Compare potential victim's ARP cache/Trusted Server ARP Cache 

### 4) Rogue Device

*Unauthorized device (WAP, DHCP, DNS) allows unauthorized individuals access to NW*

**Best Practice**
- Visual Inspection of ports and switches
- Network Mapping and Host Discovery
- Packet Sniffing (of unauthorized protocols/communication)
- NAC and Intrusion Detection
- MAC Address reporting from Routers/Switches

### 5) Nonstandard Port Usage
- If dynamic port appears constantly open, it maight be IOC
- Non-standard traffic over well-known/registered ports

**Best Practice**
- Configure firewall for whitelisting ports
- Config Doc should show which ports on any given host are allowed
