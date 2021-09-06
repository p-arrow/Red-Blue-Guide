*Distributed Denial of Service (DDoS)*

# RedTeam

## DoS Types
1) Network Layer (TCP/UDP)
2) Application Layer (HTTP/DNS etc.)

## Attack Types
1) Too many packets
2) Oversized Packets
3) Misconfigured Packets
4) Several Restarts of Server 
5) Exhaustion of Processing Power

## Vulnerable DoS Protocols
- Echo: port 9
- Daytime: port 13
- Quote of the Day: port 19
- Chargen: port 17
- SNMP: port 169
- DNS: port 53

## Examples

#### 1) Flood Attack 
a) Ping flood/ICMP echo request
b) SYN flood: Initiate multiple TCP session (w/o 3way Handshake)
c) Smurf Attack: Pings to subnet, replies to spoofed IP (server)
d) XMAS Attack: Scan with FIN/PSH/URG flags (crash of server)

#### 2) Ping of Death
Send oversized (>64kb) and malformed packet
Pretty old attack
Most systems are resistant nowadays

#### 3) Teardrop Attack
Breaks apart packets into IP fragments
Modifies them with overlapping/oversized payload

#### 4) Permanent DoS
Exploits security flaw permanently
This breaks NW device by reflashing its firmware

#### 5) Fork Bomb
Creates large number of processes
Uses up available processing power of server

#### 6) DNS Amplification
Relies on large amount of DNS information that is sent
In response to spoofed query on behalf of victim server
--> DNS Reflective Attack

# BlueTeam

## How to measure DoS?
- bps/bits per second
- Link utilization
- Baseline: Nominal bandwidth 1Gbps, actual throughput 800Mbps

## How to mitigate DoS?
1. Real-time log analysis; Identify pattern; Redirect to black/sinkhole
2. Use geolocation and IP reputation data to ignore suspicious traffic
3. Close slower connect. by reducing timeouts on affected Servers
4. Use Caching/Backend Infrastrutcure (CDN, Proxy)
5. Use Enterprise DDoS protection (Cloudflare, Akamai)
6. Disable Internet exposed services

## DRDoS (Distributed Reflection DoS)

*DDoS + implementing an amplification factor*

**Examples**
1. Spoofed ping request (ICMP)
2. Bogus DNS query (small request, big reply)
3. NTP (small request, but big reply of last 600 pcs the server contacted)
