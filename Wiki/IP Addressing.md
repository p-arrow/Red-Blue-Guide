## Basics
- IPv4 Address: 32bit
- IPv6 Address: 128bit
- MAC Adresse: 48bit (Media Access Control)
- Private IP Address: for free
- Public IP Address: charged by ISP (Internet Service Provider)
- 127.0.0.1 (IPv4 loopback address)
- ::1  (IPv6 loopback address)
- 0.0.0.0 (Variable for all IPv4 addresses on host)

## Network Classes
Address Class | Value in First Octet | Classful Mask | Classful Mask | Private Scope
------------- | -------------------- | ------------- | ------------- | -------------
Class A | 1-126  | 255.0.0.0  | /8 | 10.0.0.0 - 10.255.255.255
Class B | 128-191 | 255.255.0.0 | /16 | 172.16.0.0 - 172.31.255.255
Class C | 192-223 | 255.255.255.0 | /24 | 192.168.0.0 - 192.168.255.255
Class D | 224-239 | n/a | n/a | Multicast Purpose

## CIDR (Classless Interdomain Routing)
- Used to summarize contiguous networks (e.g. /26)

## VLSM (Variable-Length Subnet Masking)
- Allows subnets of various sizes
- Requires suitable routing protocol (RIPv2, OSPF etc.)
