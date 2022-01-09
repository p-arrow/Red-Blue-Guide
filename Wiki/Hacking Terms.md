**Daisy Chaining**
- Use compromised system for pivoting to other targets

**Doxing**
- Disclose personal data in public (Data Exposure)

**Side Channel Attack**
- Exploit physical characteristics of target system 
- Examples: memory access time, heat development, electro magnetic radiation etc.

**Evil Maid Attack**
- Unauthenticated physical access to target system (exp: in hotel room)

**Data Diddling**
- Falsify data before it is stored

**IOA**: Indicator of Attack ('in progress')

**IOC**: Indicator of Compromise

**PUP**: Potentially Unwanted Program

**PUA**: Potentially Unwanted Application

**Web Types**
1. Surface Web (indiziert)
2. Deep Web (nicht indiziert, nicht via DNS auflösbar)
3. Darknet (P2P, geschlossene Gesellschaft)

**Hacking Phases**
1. Footprinting
2. Scanning
3. Enumeration
4. Exploit/Gaining Access (Password Hacking, Social Engineering)
5. Maintaining Access (Backdoors, Trojaner, Keylogger, Rootkits, Steganographie
6. Clearing Tracks (Logfiles löschen oder manipulieren)

**Footprinting**
- Map out layout of target network (IP range, routing topology, DNS namespace)

**Fingerprinting**
- Perform single host detection to map out ports, OS, running services, metadata

**Enumeration**
- Systematische Suche nach Dienste-Daten (bspw. DNS, NetBios, SNMP)

**Slashdot Effect**
- Small websites become popular quickly due to social sites (Slashdot)

**Sweep**
- Scan directed at multiple IP addresses to discover responses of particular ports

**Shadow IT**
- Form of unintentional insider threat

**Commodity Malware**
- Widely available for sale

**Custom Malware**
- Developed and with target in mind
- Higher severity than commodity malware (!)

**Reputational Threat Research**
- Blacklist of known threat sources (IPs, DNS, signatures)

**Behavioral Threat Research**
- Refers to correlation bw. IOCs and Attack Patterns

**TTP (Tactics, Techniques and Procedures)**
- Behavioral pattern that was used in historic cyber attacks

**Port Hopping**
- APT's C2 application jumps between different ports

**Fast Flux DNS**
- Rapidly change the IP of a domain to prevent blacklisting

**Evasion**
- Technique used in order to escape detection during Pentest (Obfuscation, Encoding etc.)

**Data Execution Prevention (DEP)**
- Defensive measure to prevent attackes rewriting memory and executing code.

**SEH Overwrite**
- Attacker manipulates Structured Exception Handler and gain control of execution flow. Often combined with Buffer Overflow.

**Return Oriented Programming (ROP)**
- Attacker has control of execution flow but DEP is enabled. Then ROP gadget (Windows API Call, WriteProcessMemory Call) has to be prepared to circumvent DEP.

**Pillaging**
- Obtaining files (which contain personal information) from targeted hosts (e.g. during Pentest)

**Spoofing**
- Imitiate another person/computer/service (MAC, IP etc.)
- Prevention via Authentication

**Hijacking**
- Exploitation of computer session to gain unauthorized access
   - Session theft
   - TCP/IP hijacking: authen only during 3-way handshake
   - Blind hijacking: Randomly send packets into two machines communication
   - Clickjacking: trick a user to click on a link/button
   - MITM
   - MITB
   - Watering Hole
   - XSS

**Replay Attack**
- Valid data transmission is maliciously rebroadcast/repeated/delayed
- Prevention via Session Token / MFA

**SSL Attack**
- Heartbleed (Heap dump)

**TSL Attack** 
- Poodle (MITM via JavaScript and Downgrade to SSL)
- Block Cipher (AES) uses Cipher Block Chaining (CBC) which uses Padding (= fill up blocks)
- Then Poodle can decrypt HTTPS-Session-Cookies

**Domainsquatting**
- Reservation of similar domain names (compared to target victim domain) at low cost
- The actual rights holder (victim) gets extorted to buy the "similar domain names" at high cost

**CIA Triad**
- Confidentiality
- Integrity
- Availability
- optional: Authenticity / non repudiation /Accountability

**AAA**
- Authentication: process of verifying the ID of a person/device
- Authorisation: function of specifiying access rights to resources
- Accountability: function of assigning responsibility

**Types of Hackers**
- White: hired/contracted directly by company
- Black
- Grey
- Blue: BugBounty, Pentesters
- Elite: Zeroday Exploit developer etc
- Script Kiddies

**Threat Types**
- Script Kiddies (low level)
- Hacktivists
- Organized Crime
- Advanced Persistent Threats (High level)
