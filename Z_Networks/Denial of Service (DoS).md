*Distributed Denial of Service (DDoS)*

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


## DRDoS (Distributed Reflection DoS)

*DDoS + implementing an amplification factor*

**Examples**
1. Spoofed ping request (ICMP)
2. Bogus DNS query (small request, big reply)
3. NTP (small request, big reply of last 600 pcs the server contacted)
