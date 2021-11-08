*Windows CMD*

## Basics

- **d:** : change to volume D
- **cd**: change directory
   - `cd %userprofile%`
   - `cd %APPDATA%`
- **help**:
   - `[command] help/` 
   - `[command] /?`
- **cls**: clear
- **dir**: show directory
   - `/Q` Permissions
   - `/R` ADS ([see here](https://github.com/p-arrow/Red-Blue-Guide/blob/main/X_RedTeamOthers/Alternate%20Data%20Stream%20(ADS).md))
   - `/S` SubDirectory
   - `/AH` hidden files
   - `/AS` system files
- **whoami**: 
- **shutdown**:
   - `shutdown /s /t 30`: shutdown in 30s
- **start**: start new window/program 
- **pause**: wait until arbitrary key is pressed 
- `timeout [s]`: window is closed after [s] seconds 
- `set PATH=C:\path\to\app\directory;%PATH%`: add app to system path 

## Display
- **color**:
   - `color xy`: x = background color, y = foreground color
- **mode con**: change console window size
   - `mode con: cols=18 lines=1`: con = console, cols = columns
- **title**: change title of CMD-Window

## Network

- **ipconfig**
- **netstat**: check network connections 
   - `netstat -nabp tcp`
   - `netstat -tunlp`
- **netsh**: 
   - `netsh interface ipv6 show neighbors`
   - `netsh advfirewall set allprofiles state off`
- **arp**: request ARP-Cache
   - `arp -a`
- **tracert/pathping**: 
- **route**: Modify NW routing table
   - `route print`
- **getmac**: 
   - `getmac /V`
- **nbtstat**: 
- **nslookup**: DNS recon
   - "Non autoried answer" = queried DNS is no authoritative DNS of example.com
   - `server 8.8.8.8`
   - `set all` (show options)
   - `set type=a` ; example.com
   - `set query=all` ; example.com
- **show Domain Name**:
   - `echo %LogOnServer%`
   - `wmic computersystem get domain`
   - `systeminfo | findstr /I Domain`

## Data/File

- **echo**: print function
   - `echo [...] > xyz.txt`
   - `echo [...] >> xyz.txt`
   - line break: 
     - 1) `echo Hello ^`
     - 2) More?
     - 3) `Welt`
     - 4) Result: `Hello Welt`
- **find**: for basic strings, like "grep" in Linux 
   - `dir | findstr /i /m "system"`
- **findstr**: regex searching, like "grep" in Linux
   - `dir | findstr /i /m "system"`
- **more**: show page-wise 
   - `findstr xx | more`
- **move** x y: 
- **copy** x y: 
- **del**: delete 
- **ren**: rename
- **rd**: delete directory 
- **type**: show file content
   - `type example.txt`
- **scp**: file transfer
- **start ms-windows-store**:  open WinStore from CLI
- **icacls** [file/dir]: display access rights 
   - `icaclcs testfile.txt /remove student`
   - `icacls testfile.txt /grant student:R`: R = read permission
- **attrib**: show and modify file attributes
- **fc**: file compare
- **icacls**: Displays or modifies discretionary access control lists
   - Details: (Win Docs)[https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/icacls]
   - F - Full access
   - M - Modify access
   - RX - Read and execute access
   - R - Read-only access
   - W - Write-only access
   - Examples:
      - `icacls [file] /grant User1:(D,WDAC)`: Grant the User1 Delete and Write DAC permissions to [file]
      - `icacls [file] /grant *S-1-1-0:(D,WDAC)`: Grant the User defined by SID S-1-1-0 Delete and Write DAC permissions to [file]


## System


- **diskpart**: disk management
- **chkdsk**: check disk and show status report 
- **ver**: show Windows Version
- **powercfg**: config energy management
- **powercfg.cpl**: open energy option (GUI)
- **sigverif**: verify program signature
- **tasklist**: show all processes
- **taskkill**: terminate process 
   - `taskkill /IM spotify.exe` 
- **sc** (service control): start/stop Windows Services
   - `sc stop [service name]`
- **openfiles**: show all running processes 
- **sfc**: System File Checker
- **bcdedit**: Windows-Start-Manager (activate/deactivate DEP -> /set nx alwayson)
- **fsutil usn**: Manage Change-Journal of USN
- **certutil**: certification utility
- **systeminfo**: show system information
- **net**: Diverse Netzwerk Services/Dienste managen
   - `net user`: show users 
   - `net user [username] *`: change ser password 
- **dism**: Tool for Image management
   - `dism /online /get-packages`: check installed KBs
- **setx**: create/edit environment variables in user or system context 
   - Syntax: `setx [/S System [/U [Domäne\]Benutzer [/P [Kennwort]]]] var Wert [/M]`
   - /M =  Variable is set in system-wide environment (HKEY_LOCAL_MACHINE)
   - Standard value is set in HKEY_CURRENT_USER
- **certmgr**: certificate tool
- **reg save**: save Registry Hives
   - `REG SAVE HKLM\Software\MyCo\MyApp AppBkUp.hiv`: save MyApp as AppBkUp.hiv
   - `reg save HKLM\SAM SAM`
   - Kali: `impacket-secretsdump LOCAL -sam SAM`
- **bootsect**: repair master boot record
   - `bootsect /nt60 c: /mbr`
