# RedTeam

## Common Commands
- nmap -sn / -sP  (only Host Discovery)
- nmap -Pn (no Host Discovery, only port scan)
- nmap -p21,23,80 (explicit port selection)
- nmap -p- (all 65k ports)
- nmap -v (verbose)
- nmap -6 (IPv6)
- nmap -reason (short explanation of host answer)
- nmap -sI (TCP-IDLE Scan via Zombie Host) --> investigate via IP-ID if port is open/closed
- nmap -Pn -p- -sI [IPv4 Zombie] [IPv4 dest.]
- nmap -PU80,443 (UDP-Scan + explicit port selection)
- nmap -PE (ICMP type 8 = echo request)
- nmap -PP (ICMP type 14 = timestamp 
- nmap -PM (ICMP type 18 = address mask)
- nmap -sA  (ACK Paket (FW Walking possible!))
- nmap -sV  (Version identification)
- nmap -sS (SYN scan)
- nmap -sU (UDP scan)
- nmap -sT  (TCP scan) --> when -sS no option due to missing raw socket access
- nmap -O: OS identification 
- nmap -oX (Output .xml; add "--webxml" as stylesheet reference)
- nmap -T (Scan time T0 [paranoid] - T5[insane])
    - **> Fast Speed can cause fragile devices to reboot/print random data (!)**


## NSE (Nmap Script Engine)
- Written in LUA script language
- Extended analysis of target system 
- Testing for vulns of certain exploits 
- NSE-Scripts verify host & service before execution (efficient) --> only suitable scripts are executed
- Scripts are stored here: `/usr/share/nmap/scripts`

**NSE Examples:**
```
- nmap -sC [IPv4] (-sC = --script=default)
- nmap --script [script1],[script2],... [IPv4] (explicit script selection)
- nmap --script http-waf-detect [IPv4]
- nmap --script HTTP-google-malware [IPv4] (query if IP is in Google DB)
- nmap localhost -p 31000-32000 -sV
- nmap -sV --script=vuln [IPv4]
- nmap -sV -p 22 --script ssh2-enum-algos [IPv4]
- nmap --script-help "*ms* and *sql*"
```

## Quick Scans
1. `nmap -F`: 100 Ports
2. `nmap --top-ports 10`: 10 top Ports scannen
3. `nmap --exclude-ports [Portnr, Portnr, ...]`
4. `nmap -sS -sU -p T:22,25,80,U:53,161 [IPv4]`

## Scanflags
- `nmap --scanflags [your own flag]`: 
    - sN: TCP Null (no flag)
    - sF: FIN
    - sX: Xmas (FIN, PSH, URG)

## Important Directories
- `/usr/share/nmap/nmap_payloads`: Which packets are sent during scan 
- `/usr/share/nmap/nmap_services`: port list with indicated chance of being "open" 
- `/usr/share/nmap/scripts`: Script list

## Firewall Evasion (If nmap is blocked)

1. ICMP Echo Request (Typ 8): `nmap -PE`
2. ICMP Timestamp Request (Typ 13): `nmap -PP`
3. TCP SYN Port 443:`nmap -PS443`
4. TCP ACK Port 80: `nmap -PA80`

## Firewall Avoidance
1. Fragmentation of sent packets: `nmap -f [IPv4] --top-ports 10`
2. Decoy Scan: `nmap -D [fakeIPv4],...,...,ownIP] [target IPv4]`
   - Place your own IP at sixth place
   - Some IDS don't show IPv4 anymore after several recognized port scans 
3. Usage of alternative sender address: `nmap -S [fakeIPv4]`
   - Only deception (at the expense of missing scan results)
4. SYN-Stealth-Scanning: Not stealthy anymore (!)


## TTL Reply
The output of an successful ping contains information of TTL (Time to Live)
- TTL 128: Normally Windows machine
- TTL 64: Normally Linux machine

<br />

# BlueTeam

...
