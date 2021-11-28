*Open Systems Intersection Model*

## OSI Layers

#### OSI Layer 1 (Physical Layer)
- Network Topolgy
- Cables (copper, fiber optic)
- Ethernet IEEE 802.3
- Wireless IEEE 802.11
- Bluetooth IEEE 802.15.1
- Devices (Hubs, WAP, Media converter)
- Synchronization:
   - **Synchronous**: Coordinate TX of sender/receiver in parallel (ref. clock)
     - Telephone (baseband)
     - Time-Divison Multiplexing (TDM)(baseband)
     - Statistical TDM (StatTDM) (more efficient version of TDM)
     - Frequency Division Multiplexing (FDM)(similar to Broadband)
   - **Asynchronous**: Start/stop bits to indicate the bit transmission

#### OSI Layer 2 (Data Link)
- MAC (Media Access Control)
- DOCSIS (Data over cable service interface specification)
- LLI (Logical Link Control): Allows ACK after receipt of messages
- LLDP (Link Layer Discovery Protocol): NW devices advertise ID/capability/neighbors
- **Devices**: Switches / Bridges / NIC (Network Interface Card)
- Synchronization:
   - **isochronous** (ref. clock source, less overhead than syn. and asyn.)
   - **synchronous** (reference clock source, beginning and end frames)
   - **asynchronous** (own internal clock, start/stop bits)

#### OSI Layer 3 (Network)
- Logical Addressing (IPv4, IPv6, AppleTalk, IPX)
- Routing
   - Packet switching: any route is fine (most common!)
   - Circuit switching: Dedicated route established (Telephone)
   - Message switching: packet switch + storing/forwarding function
- Route Discovery and Selection 
- Flow control (ICMP)
- **Devices**: Router, Multilayer Switch
- Bandwith usage
- Multiplexing strategy

#### OSI Layer 4 (Transport)
- **TCP (Transmission Control Protocol)**:
   - Reliable
   - Sequencing
   - Retransmission and flow control
   - ACK segments
- **UDP (User Datagram Protocol)**
   - Unreliable
   - No sequencing
   - No retransmission
   - No ACK
   - Exp: Audio/Video Streaming
- **Functions**:
   - Windowing
      - Adjust the segment flow, subject to retransmission rate
      - Low retransmission rate --> higher segment flow (speed optimization)
   - Buffering
      - Allocate memory to store segments before forwarding them
- Devices: WAN accelerator / Load balancer / Firewall

#### OSI Layer 5 (Session Layer)
- Building Session: Check Credentials/Assign numbers to session
- Maintaining Session
- Tearing Down a Session
- **Protocols**: H.323/H.264 (Real-time Transport Protocol/RTP) / NetBIOS


#### OSI Layer 6 (Presentation)
- Features:
   - Formatting data
   - Securing data (encryption)
   - TSL/SSL
- **Protocols**: HTML / PHP / Perl / XML / JavaScript / ASCII / UNICODE / GIF / JPEG / MP4

#### OSI Layer 7 (Application)
- Service Advertisment: Applications send announcements to state the service they offer
- Application Services: Unite communicating components between network applications
- **Protocols**: SMTP/IMAP / HTTPS / DNS / FTP / SSH/TELNET / SNMP


## Data Types of each Layer

![grafik](https://user-images.githubusercontent.com/84674087/132395011-d92c7523-7e19-44ec-908a-eb3dd87a3fd3.png)
