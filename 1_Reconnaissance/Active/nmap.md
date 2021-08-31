
**If nmap is blocked by Firewall**
1. ICMP Echo Request (Typ 8): `nmap -PE`
2. ICMP Timestamp Request (Typ 13): `nmap -PP`
3. TCP SYN Port 443:`nmap -PS443`
4. TCP ACK Port 80: `nmap -PA80`

**How to avoid Firewall alert**
1. -f: Fragmentation of sent packets 
   - `nmap -f [IPv4] --top-ports 10`
2. -D: Decoy Scan
   - `nmap -D [fakeIPv4],...,...,ownIP] [target IPv4]`
   - Place your own IP at sixth place
   - Some IDS don't show IPv4 anymore after several recognized port scans 

3. -S: Usage of alternative sender address
   - `nmap -S [fakeIPv4]`
   - Only deception (at the expense of missing scan results)

4. SYN-Stealth-Scanning: Not stealthy anymore!
