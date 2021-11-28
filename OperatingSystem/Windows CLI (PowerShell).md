*Powershell = PS*

## TABLE OF CONTENTS
1. [BASICS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Windows%20CLI%20(PowerShell).md#basics)
2. [NETWORK](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Windows%20CLI%20(PowerShell).md#network)
3. [USEFUL COMMANDS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Windows%20CLI%20(PowerShell).md#useful-commands)


<br />

## BASICS
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
   - `C:\Users\Unforgivable\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine`

<br />

## NETWORK
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


