# Blue Team

<br />

## Table Types

**1. Filter Table (most common)**: Filtering inbound/outbound traffic

**2. NAT Table**: Defining NAT in the network

**3. Mangle Table**: For specialized packet alteration (QoS Bits in TCP Header)

**4. Raw Table**: Modify packets before Kernel starts tracking its state (?)

**5. Security Table**: Used for Mandatory (MAC) networking rules and called after Filter Table

## Chains
- INPUT
- OUTPUT
- FORWARDING
- etc.

## Components of iptables

![grafik](https://user-images.githubusercontent.com/84674087/132100832-0639895d-de51-40ea-b331-cd402d30bafa.png)

## How To

Option | Explanation
------ | -----------
iptables -L -v -n | list rules verbose numerical
iptables -S | show rules
iptables -X | deletes empty/unused chain (iptables -X ddos-attack)
iptables -A | adds a rule (at the end)
iptables -I | Insert a rule (at the top)
iptables -F | delete all rules (F=flush)
iptables -D | delete one or more rules
iptables -L --line-numbers | list with line numbers
iptables -P | set policy
-i | interface inbound
-o | interface outbound
-j | action_options
-p | protocol (tcp/udp/icmp)
-s | source (address)
-d | destination (address)
-m | match
--dport | destination port
--state | NEW
--state | ESTABLISHED
--state | RELATED (packets init new connection related to existing one)
Export Rules | sudo iptables-save > ~/iptables.txt
Import Rules | sudo iptables-restore < ~/iptables.txt

## Best Practice LAN

- `iptables -P INPUT DROP`: policy change
- `iptables -A INPUT -i lo -j ACCEPT`: Inbound to Host allowed
- `iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT`: Ingress packets of existing network connection (e.g. HTTPS) allowed
- `iptables -A OUTPUT -o lo -j ACCEPT`: Exgress host-packets allowed
- `iptables -A INPUT -s 192.168.1.10 -p tcp --dport ssh -j REJECT`

## Best Practice INTERNET
- `iptables -A OUTPUT -m state --state RELATED,ESTABLISHED -j ACCEPT`
- `iptables -A OUTPUT -o eth0 -p udp -m udp --dport 53 -j ACCEPT`
- `iptables -A OUTPUT -o eth0 -p tcp -m tcp --dport 80 -m state --state NEW -j ACCEPT`
- `iptables -A OUTPUT -o eth0 -p tcp -m tcp --dport 443 -m state --state NEW -j ACCEPT`

## Recommended Firewall Logs

1. Permitted/Denied/Failed connections
2. Ports and protocols in use
3. Bandwidth utilization
4. NAT/PAT log

## Others

**Abbreviations**
- SPT = Source Port
- DPT = Destination Port
- TTL = Time to Live
- TOS = Type of Service

**Drop vs Reject**
- Drop: sending ICMP unreachable
- Reject: sending TCP RST

