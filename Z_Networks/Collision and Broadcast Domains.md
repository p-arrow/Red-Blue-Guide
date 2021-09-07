*Red: Collision Domain*

*Violett: Broadcast Domain*

## HUB (Layer 1)
- Passive (w/o amplification)
- Active (with amplification)
- Smart (Active hub with enhanced features)

![grafik](https://user-images.githubusercontent.com/84674087/132392173-c09b522d-edc8-4c28-90c6-1f2e63cc5c50.png)

## Bridge (Layer 2)
- Used within one network
- 1x input port/1x output port
- Analyze source MAC
- Populate internal MAC table
- Intelligent forwarding based on destination MAC
- Breaks Collision Domains (better security+efficiency)
- 
![grafik](https://user-images.githubusercontent.com/84674087/132392208-47532cf9-e065-4abf-8486-bb1d2e5269f8.png)

## Switch (Layer 2)
- Used within one network
- Multiport Bridge
- Full Duplex
- 1x Broadcast Domain per switch
- MAC Flooding: Switch can fail-open and act like a hub (!)
- MAC Spoofing: Pretend to be another MAC (!)
- Physical tampering: The switch should be physically locked and stored (!)

![grafik](https://user-images.githubusercontent.com/84674087/132392261-37cceca1-dc79-4cec-b466-3f368fc6734f.png)

## Router (Layer 3)
- Routes traffic between different subnets or networks
- 1x Collision Domain per port
- 1x Broadcast Domain per port
- IP Spoofing: Used to trick a router's ACL (Access Control List) (!)

![grafik](https://user-images.githubusercontent.com/84674087/132392281-431178e0-9fc4-41a3-a35e-3eb8fba95db2.png)

## Multilayer Switch (Layer 3)
- 1x Collision Domain per port
- 1x Broadcast Domain per port
- Effective for small networks, but normally dedicated router preferred
