# TABLE OF CONTENTS
1) [WINDOWS CMD](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Windows.md#windows-cmd)
2) [WINDOWS POWERSHELL](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Windows.md#windows-powershell)
3) [LEGITIMATE PROCESSES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Windows.md#legitimate-processes)
4) [MASTER FILE TABLE](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Windows.md#windows-master-file-table)
5) [WINDOWS SHORTCUTS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Windows.md#windows-shortcuts)

<br />

# WINDOWS CMD
## TABLE OF CONTENTS
1. [BASICS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Windows.md#basics)
2. [DISPLAY](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Windows.md#display)
3. [NETWORK](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Windows.md#network)
4. [DATA / FILE](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Windows.md#data--file)
5. [SYSTEM](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Windows.md#system)

<br />

## BASICS
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

<br />

## DISPLAY
- **color**:
   - `color xy`: x = background color, y = foreground color
- **mode con**: change console window size
   - `mode con: cols=18 lines=1`: con = console, cols = columns
- **title**: change title of CMD-Window

<br />

## NETWORK
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

<br />

## DATA / FILE
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
   - Details: [Win Docs](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/icacls)
   - F - Full access
   - M - Modify access
   - RX - Read and execute access
   - R - Read-only access
   - W - Write-only access
   - Examples:
      - `icacls [file] /grant User1:(D,WDAC)`: Grant the User1 Delete and Write DAC permissions to [file]
      - `icacls [file] /grant *S-1-1-0:(D,WDAC)`: Grant the User defined by SID S-1-1-0 Delete and Write DAC permissions to [file]

<br />

## SYSTEM
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
- **bcdedit**: configure the boot behavior
   - `bcdedit /default {40e2e288-0252-11eb-81b7-4ce173422c3c}`: select default booting disk by UUID
   - `bcdedit /set {bootmgr} path \EFI\Microsoft\Boot\bootmgfw.efi`: Make windows default boot partition
   - `bcdedit /set {bootmgr} path \EFI\debian\grubx64.efi`: Make Linux default boot partition
   - `bcdedit /deletevalue {bootmgr} path \EFI\debian\grubx64.efi`: Delecte boot value

<br />

# WINDOWS POWERSHELL
## TABLE OF CONTENTS
1. [PS BASICS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Windows.md#ps-basics)
2. [PS NETWORK](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Windows.md#ps-network)
3. [USEFUL COMMANDS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Windows.md#useful-commands)

<br />

**Powershell = PS**

<br />

## PS BASICS
- **get-help**
   - `get-help [command] OPTION`
     - OPTION = `-examples` / `-detailed` / `-full` etc.
   - `help [command]`
- **manage-bde**
   - `manage-bde /?`: open BitLocker menu
- **get-command**
   - Exp: `get-command -module [module name]`: 
     - module names = netsecurity, defender etc. 
- **stop-service**
   - Exp: `stop service -Name [Spooler] -Force`
- **set-service**
   - Exp: `set-service -Name [Spooler] -StartupType Disabled`
- **get-content**: Get content of item 
   - `get-content` or `gc`
- **get-itemproperty**
   - Exp: `Get-ItemProperty HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\* | Where-Object {($_.DisplayName -eq "name")}`
- **PS Command History**:
   - `C:\Users\%USER%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine`

<br />

## PS NETWORK
- `Get-NetIPAddress | Format-Table`
- `Get-NetAdapter`
- `Get-NetIPConfiguration -All`
- `Test-NetConnection [DST IPv4]`
- `Test-NetConnection www.example.com -InformationLevel Detailed`
- `Test-NetConnection www.example.com -Traceroute`
- `Get-NetRoute | Format-List -Property *`: Routing Table
- `Get-NetTCPConnection`
- `Set-NetFirewallProfile -Profile OPTION -Enabled False/True`
   - OPTION = `Domain` / `Public` / `Private`

<br />

## USEFUL COMMANDS
#### Update Package (Exp: Powershellget)
1. `Install-PackageProvider -Name NuGet -Force`
2. `Install-Module -Name PowerShellGet -Force`
3. `Update-Module -Name PowerShellGet`
4. Verify: `Get-Module -ListAvailable (PowerShellGet)`

#### Disable/Remove Features 
- `Disable-WindowsOptionalFeature -FeatureName "feature" -Online -NoRestart`
   - `-Online` = the currently running Windows

#### Execution Policy
- `Get-ExecutionPolicy -List | Format-Table -AutoSize`: List execution policy
- `Set-ExecutionPolicy -ExecutionPolicy Restricted/RemoteSigned/Undefined/AllSigned`: Set execution policy   
- **Evade PowerShell Execution Policy (3 Options)**
   1. `Get-Content runme.ps1 | Invoke-Expression` (Alternative: `GC runme.ps1 | iex`)
   2. `PowerShell.exe -ExecutionPolicy Bypass -File .runme.ps1`
   3. `PowerShell.exe -ExecutionPolicy Unrestricted -File .runme.ps1`

#### Users/Groups
- `Search-ADAccount –AccountInactive –UsersOnly`: Find unused accounts in Active Directory

#### System
- `wsl --help`: Windows Subsystem for Linux
   - command overview: [https://aka.ms/wslstore](https://aka.ms/wslstore)

#### Execute File in PowerShell
- [Details: social.technet.microsoft.com](https://social.technet.microsoft.com/wiki/contents/articles/7703.powershell-running-executables.aspx)
- Direct: `.\testapp.exe`

#### Remove User Jumplists 
- **gci** (get-ChildItem): show files in one or more specified locations
```
$profiles = gci \\server\share
foreach ($profile in $profiles)
{
gci ($profile.fullname + '\UPM_Profile\AppData\Roaming\Microsoft\Windows\Recent\') | Where-Object LastWriteTime -lt (get-date).AddDays(-7) | remove-item -Force -Recurse
}
```

#### Search for Sensitive Data 
- `Get-ChildItem -Path "c:\users\" -Recurse -Force -Include *.doc, *.docx, *.xls, *.xlsx, *.txt, *.pdf, *.ppt, *.pptx | Select-String "[P|p]assword" | Select-Object Path, Line, LineNumber | Export-Csv "c:\Users\%USER%\Desktop\passwordPII.csv"`

<br />

# LEGITIMATE PROCESSES
**See here:** [3_Exploitation/Processes](https://github.com/p-arrow/Red-Blue-Guide/blob/main/3_Exploitation/Windows%20Legitimate%20Processes.md)

<br />

# WINDOWS MASTER FILE TABLE
## Characteristic
- Each file on NTFS has record in master file table
- NTFS reserves first 16 records of the table for special information
- First record describes MFT itself, followed by MFT mirror record
- If first MFT record is corrupted, MFT mirror can be used
- Small Files/Directories: <512 Bytes
- Small Records can entirely be contained in MFT

#### NTFS performs faster Data Access compared to FAT (File Allocation Table), because ...
- FAT first reads the file allocation table and assures that it exists
- FAT retrieves the file by searching the chain of allocation units assigned to the file
- With NTFS, as soon as you look up file, it's there to use

<br />

![grafik](https://user-images.githubusercontent.com/84674087/140794801-936f790a-ad9e-4706-9299-e372dd7c8c70.png)

<br />

# WINDOWS SHORTCUTS
## SHORTCUTS
- Windows-key + r: open run dialog box
- Windows-key + r & `cmd + Ctrl+Shift+Enter`: Open CMD as admin
- Windows-key + r & `runas /user:administrator cmd`: Open CMD as admin
- Windows-key + r & `winver`: Windows VVersion Information

## WHEN RUN DIALOG BOX IS OPEN 
Command | Explanation
------- | -----------
control | System Control
diskmgmt.msc | Disk Management
msconfig | System Configuration (Autostart etc.)
sysdm.cpl | System Control Panel Applet
firewall.cpl | Firewall
regedit | Windows Registry
services.msc | Services
msinfo32.exe | System info
MMC | Microsoft Management Console
lusrmgr.msc | Local User and Groups
eventvwr.exe | Event Viewer
optionalfeatures | Windows Features
ncpa.cpl | NW Control Panel
perfmon | Performance Monitor (Baseline etc.)
compmgmt.msc | Computer Management
gpedit.msc | Group Policies
gpupdate | Update Group Policies after modification
appwiz.cpl | Programm overview 
devmgmt.msc | Device Manager
tpm.msc | TPM Management Console

## IMPORTANT DIRECTORIES
- `Windows/System32/drivers/etc`: host file
- `Windows/System32/config/SAM`: user credentials (SAM = Security Account Manager)
- `Windows/System32/winevt/Logs`: event protocol
   - Check out here too: [WinEventLogs](https://github.com/p-arrow/Red-Blue-Guide/blob/main/3_Exploitation/Windows%20Event%20Logs.md) 

## GOD MODE
- Create new file on Desktop: `file_name.{ED7BA470-8E54-465E-825C-99712043E01C}`