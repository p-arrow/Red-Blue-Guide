# RedTeam

... 

<br />

# BlueTeam

## Disable/Enable Autorun (Group Policy)

1. Open gpedit.msc 
2. `Computer Configuration\Administrative Templates\Windows Components\Autoplay Policies`
3. In the Details pane, double-click Turn off Autoplay
4. Click Enabled, and then select All drives in the Turn off Autoplay box to disable Autorun on all drives
5. gpupdate.msc

## Disable/Enable Autorun (Registry)

*Windows 7, Windows Server 2008, Windows Vista, Windows Server 2003, or Windows XP*

1. Open regedit
2. Locate following entry in the registry: `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\Explorer\NoDriveTypeAutorun`
3. Right-click NoDriveTypeAutoRun, and then click Modify (Alternatively, Create a new dword 32 bit value "NoDriveTypeAutoRun")
4. In the Value data box, type `0xFF` to disable all types of drives
5. Restart explorer.exe

## Change USB Permission

1. Open Explorer, choose your flash drive and right click on it, choose properties from there
2. Under Format tab, choose NTFS
4. After successful formatting, choose again properties
5. Under security tab, choose Everyone from group or user names
6. Click on the Edit button to change permissions of the flash drive to **read only** rights
