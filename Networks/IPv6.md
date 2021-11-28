## Advantages
1) Much larger address space
2) No broadcasts (more efficient)
3) Instead using Anycast: Let one host initiate efficient updating of router tables for a group of hosts
4) No fragmentation (no MTU, more efficient)
5) Can coexist with IPv4 (Dual Stack Tunnel)
6) Simplified header (only 5 i/o 12 fields)
7) Groups of 0's can be summarized as `::` (Exp: 2018::4815:54ae)
8) Ability to auto configurate its own IP address (DHCP not necessary)

## Disadvantages
1) Spoofing is possible 
2) Subnet reconnaissance is possible
3) Integrated IPSec does not solve everything (not by default activated)
4) SecConfig for IPv4 and IPv6 has to be done separately

## NDP (Neighbor Discovery Protocol i/o ARP)
- To learn Layer 2 addresses on the network
- Successor: Secure Neighbour Discovery (SEND)
- Features:
   - Router Solicitation / Advertisment
   - Neighbor Solicitation / Advertisment
   - Redirect (to get better first-hop)
- Show neighbors: `netsh interface ipv6 show neighbors`

## IPv6 Address Types
- 2000 to 3999 = Globally routable unicast
- FE80 ... = Link-Local (not globally routable)
- FF ... = Multicast

## Disable IPv6 on Linux
1. Verify if IPv6 is enabled:
   - `lsmod | grep ipv6`
   - `cat /proc/net/if_inet6`
   - `sysctl -a 2>/dev/null | grep disable_ipv6`
2. In `/etc/default/grub` append `GRUB_CMDLINE_LINUX=”ipv6.disable=1”`
3. Update grub


## Security Best Practice
- Enable authen for routing protocols
- Activate Bogon Filters
- Use Host based FWs
- Use non-predictable address space in Subnet
- Avoid (dynamic) Tunnels: This can decrease visibility for FWs
- Check IPv6 Attack Surface (scan6) due to IPv6 Autoconfig
