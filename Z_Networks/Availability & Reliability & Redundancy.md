## Availability

*Concerned with being up and operational (measured in uptime)*

## Reliability

*Concerned with not dropping packets*

- **MTTR** (Mean Time to Repair): Average time to repair NW device
- **MTBF** (Mean Time between Failures)
- **HSRP** (Hot Standby Router Protocol): Cisco Proprietary
- **CARP** (Common Address Redundancy Protocol): Open Std. HSRP
- **VRRP** (VirtualRouterRedundancyProtocol): IETF Open Std. HSRP
- **GLBP** (Gateway Load Balancing Protocol): Cisco proprietary

#### Performance
- LACP (Link Aggregation Control Protocol)
- Content/Caching Engine: More efficient than Proxy
- Content Switch: Switch distributes traffic to server farm (Lo.Bal.)
- Server with several NW cards (NICs)

#### Link Efficiency
- Compression: Allows buffer to delay traffic from exceeding configured rate
- LFI (Link Fragmentation & Interleaving): Fragments large data and interleaves small data 

## Redundancy

#### Questions to ask
- What is main function of network? (case by case decision)
- Identify the available budget!
- Define how to measure/manage high-availability (metrics help)
- Where redundancy? (dual power supply vs dual switch?)
- What software redundancy features are appropriate?
- What protocol characteristics affect design? (TCP/UDP)
- How to maintain environmental conditions?


#### Site Redundancy
1. **Cold Site**: Building available, Hardware&Software not
2. **Warm Site**: Building and Hardware available, Software not
3. **Hot Site**: Building, Hardware and Software available
