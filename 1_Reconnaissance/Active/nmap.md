## Readme

### If nmap is blocked by Firewall
1. ICMP Echo Request (Typ 8) --> nmap -PE

2. ICMP Timestamp Request (Typ 13)--> nmap -PP

3. TCP SYN Port 443 --> nmap -PS443

4. TCP ACK Port 80 --> nmap -PA80
