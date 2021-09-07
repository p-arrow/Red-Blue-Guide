*VLAN (802.1q / Layer 2)*

## Features 
- Separated logical networks on same physical hardware
- Increased security and efficiency
- VLAN Tunnel Endpoints (VTEP) exist on each end of line
- Microsegmentation at application layer (i/o L2/L3) possible

## VLAN Trunking
- Multiple VLANs transmitted over same physical cable

## VXLAN (Virtual Extensible LAN)
- Tunneling solution allow Layer2 segments to span Layer3 (IP) networks

## Tag Format (4 Bytes)
- Tag Protocol Identifier (TPID)
- Tag Control Identifier (TCI)
- non-tagged VLAN = Native VLAN

![grafik](https://user-images.githubusercontent.com/84674087/132401550-4c3ee79c-10ae-4d10-a5f1-7f0c750099a7.png)


## VLAN Attacks
1. **Switch Spoofing**
   - Attacker pretends to be a switch
   - Attacker negotiates trunk link to break out of VLAN
     - Disable "Dynamic Trunk Protocol" at VLAN port
2. **Double Tagging** (CVE-2005-4440)
   - Attacker (VLAN1) adds an additional "VLAN2" tag
   - At forwarding switch the native VLAN1 tag is removed 
   - Next Switch only reads "VLAN2" and sends the malicious packet to VLAN2 NW
     - prevent this by moving all ports out of default/native VLAN group
     - change native VLAN to unused ID (e.g. VLAN 999)

## VLAN Best Practice
1. VLAN-Management should be separated from all others
2. Watch for Promiscious Ports and unused interfaces
3. Be selective on what VLANs are allowed on the trunk
