#### Echo/9
- Vulnerable to DDoS

#### Daytime/13
- Vulnerable to DDoS

#### Quote of the Day (QOTD)/19
- Vulnerable to DDoS
- Exp: telnet [IPv4] 17 --> returns quote
- Amplification factor: 140
- Disable/Enable: /etc/inetd.conf

#### Chargen/17 (TCP/UDP)
- Character Generator Protocol
- Vulnerable to DDoS
- Example: telnet IPv4 chargen
- Not enabled by default
- Enabling under /etc/inetd.conf
- UDP request urge random UDP reply between 0 and 512 bytes (!)

#### FTP/20,21,989/990 (TCP)
- FTPS (TSL for Encryption)
- Port 20: Communication
- Port 21: File Transfer

#### SSH/22 (TCP)
- SFTP(FTP over SSH)

#### Telnet/23 (TCP/UDP)

#### SMTP/25,465,587 (TCP)
- ESMTP (Extended SMTP): Authentifizierung + Zustellung an mehrere Empfänger

#### TACACS+/49 (TCP)
- Cisco's version of RADIUS
- Bit slower than RADIUS due to TCP
- Works for Windows, Linux and OSX
- The only protocol (besides RADIUS, LDAP, AD) that allows separate functions for Authen/Authorization

#### DNS/53 (TCP/UDP)

#### DHCPS/67 (UDP)

#### TFTP/69 (UDP)
- Trivial File Transfer Protocol
- Booting OS from LAN file server
- Client/Server application
- Sacrifies reliability for efficiency (UDP)

#### Kerberos/88 (TCP/UDP)

#### POP3/110,995 (TCP)
- Post Office Protocol

#### RPCBIND/111
- Maps RPC services to port numbers in UNIX-like environment

#### NNTP/119 (TCP)
- Network News Transfer Protocol
- Used to transport Usenet articles

#### NTP/123 (UDP)
- Network Time Protocol

#### RPC/135 (TCP/UDP)
- Remote Procedure Call
- Used to locate DCOM ports to request service from a program on another PC on the network

#### NetBIOS/137-139 (TCP/UDP)
- NetBIOS over TCP/IP (NBT)
- NetBIOS Name Service 137/udp
- NetBIOS Datagram Service 138/udp
- NetBIOS Session Service 139/tcp (Host2Host Verbindung, SMB)
- NetBIOS-Namen:
   - Always 16 chars long
   - 16th char is suffix for service 

#### IMAP/143,993 (TCP)
- Internet Mail Application Protocol

#### SNMP/161+SNMPTRAP/162 (typically UDP/also TCP)

#### SMB/CIFS/445 (TCP)
- Like Samba for Linux
- File Sharing Service 
- UNC-Pfad (Uniform Name Convention): \\Server address\Ressource
- Common Internet File System (CIFS) is evolution of SMB
   - New Feature: Remote Procedure Call (RPC) over 135/udp+tcp
   - CIFS communicates over own port 445/tcp (i/o NBT)
- SMB 1.0 is one of the biggest Vulnerability (~30 years old) and deactivated by default (!)

#### LDAP/389,636 (TCP/UDP)
- Vendor-Neutral Standard
- For accessing/manipulating distributed directory
- Based on Client-Server-Modell
- Distinguished Name (DN) = eindeutiges Objekt in LDAP
- Common Name (CN)
- Domain Component (DC)
- knowledge about User (without root) is enough to gather information 

#### ISAKMP/500 (UDP)
- Internet Security Association and Key Management
- Used to set up IPsec tunnels

#### Rlogin/513 (TCP)
- Remote Login Service

#### Syslog/514 (UDP) / 6514 (TCP/TLS)
- To conduct computer message logging
- Especially concerning routers and firewalls

#### RIP/520 (UDP)
- Routing Information Protocol

#### IPP/631 (UDP)
- Internet Printing Protocol

#### iSCSI/860 (TCP)
- Linking data storage facilities over IP (SAN)

#### MS-SQL Server/1433 (TCP)
- Receive SQL DB queries from clients

#### RADIUS/1645,1646 (proprietary) or 1812,1813 (standard)(UDP)
- Remote Authen. Dial-In User Service
- Centralized Administration of dial-up/VPN/Wireless Authen (802.1x/EAP)
- Configured at Layer 7
- Authentication 1645
- Accounting 1646

#### L2TP/1701 (UDP)
- Layer2 Tunnel Protocol

#### PPTP/1723 (TCP/UDP)

#### UPNP/1900 (UDP)
- Universal Plug and Play
- Autoconfiguration of port forwarding by games consoles/smart appliances

#### iSCSI Target/3260 (TCP)
- Listening port for iSCSI targeted device

#### FCIP/3225 (TCP/UDP)
- Fibre Channel IP
- Encapsulate Fibre Channel frames within TCP/IP packets
- Usually used for SANs

#### MySQL/3306 (TCP)

#### RDP/3389 (TCP/UDP)
- Remote Desktop Protocol
- Remote connection via GUI (MS Proprietary)

#### DIAMETER/3868 (TCP)
- More advanced AAA protocol Replacement of RADIUS

#### NAT-T-IKE/4500 (UDP)
- Set up IPsec traversal through NAT gateway

#### SIP/5060,5061 (Session Initiation Protocol)
- Signaling/controlling multimedia comm. like VoIP, Skype

#### PostgreSQL/5432 (TCP)

#### VNC/5900 (TCP)
- Virtual Network Computing
- Cross-platform version of RDP
- Requires client/server/protocol to be configured
- Should only be used for internal network (!) --> for external NWs VPN is preferred

#### WinRM/5985(HTTP) /5986(HTTPS)
- Windows Remote Management
- In Windows integrated remote management protocol 
- Uses SOAP (Simple Object Access Protokoll) for connection setup 

#### HTTP-Proxy/8080 (TCP)
- Squid Proxy: 3128
