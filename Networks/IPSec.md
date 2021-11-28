## Characteristics
- **Authentication Header** (AH): Integrity / Authentication
- **Encapsulation Security Payload** (ESP): packet encap.+encryp.
- AH and ESP are used alternatively (seldom together)
- **Security Association** (SA): provides Certificates/Cryptokeys

## IPSec Process Flow
1. host1 sends traffic to host2 (certificate/PSK)
2. Router inits IPSec tunnel
3. Routers from host 1 and 2 negotiate SA to form IKE Phase 1 tunnel
4. IKE Phase 2 tunnel (IPSec tunnel) is set up via Shared Secret (DH)
5. Tunnel is established and information is securely sent
6. Choose Mode:
   - Main (3 separate exchanges)
   - Aggressive (3 packets)
   - Quick (negotiate parameters)
7. If IPSec tunnel is torn down: IPSec deletes SA

## Security
- IKE used for parameter exchange (PreSharedKey, PKE and Forward Key Exchange)
- IKE runs over 500/udp or 4500/udp 
- Client and server have to belong to same DH Group (Diffie Hellman)
   - DH Group 1 (768 Bit) - 5 (1536 Bit) is deprecated (!)
   - Recommended is DH Group 14 (2048 Bit), DH Group 20 (256 Bit elliptic) or even higher

## Transport Mode
- Payload = encrypted
- Header = unencrypted (!)
- Provides original IP header
- Used for client2site VPN

## Tunnel Mode
- Payload = encrypted
- Header = encrypted 
- Provides new IP header
- Used for site2site VPN
