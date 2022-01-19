## Features
- More efficient use of IP addresses
- Enables separation of NW for security
- Enables bandwidth control
- Reduced collisions
- classful subnet: 192.168.1.0/**24**
- classless subnet: 192.168.1.64/**26**

#### Number of created Subnets
2^s ("s" is the number of borrowed bits)

#### Number of assignable IP Addresses
2^h - 2 ("h" is the number of hosts)

#### Example
- 10.0.1.128/25
- 2^s = 2^1 = 2 subnets
- 2^h - 2 = 2^7 - 2 = 126 hosts (each subnet)
- Hint: 8 - s = h

## VLSM (Variable Length of Subnet Mask)
- Allows even more efficient usage of subnets (less waste of IP address resources)
- Multi-nested subnets possible 
- Example:
   - Main NW: 10.1.0.0/16
   - Subnet #1: 10.1.1.0/24
   - Subnets #2 & #3: 10.1.1.0/30 & 10.1.1.4/30
