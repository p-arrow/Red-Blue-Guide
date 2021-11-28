#### System Idle (PID0) / System (PID4)
- Kernel-level binary
- Parent of first user-mode process
(Session Manager/SubSystem/smss)

#### Client Server Runtime SubSystem (csrss.exe)
- Manages low-level functions
- Several normally running from %SystemRoot%\System32

#### WININIT(wininit.exe)
- Manages drivers/services
- Has only one instance as a process
- **Services.exe**
   - Hosts non-boot drivers/background services
   - Only one instance running as child of wininit.exe
   - With other services running as child of services.exe or svchost.exe
   - Services will be started by SYSTEM, LOCAL SERVICE or NETWORK SERVICE accounts
- **Local Security Authority SubSystem (lsass.exe)**
   - Handles authentication/authorization for the system
   - Single instance as child of wininit.exe

#### WINLOGON (winlogon.exe)
- Manages access to User Desktop
- Only one instance per User
- Child: Desktop Window Manager (dwm.exe) in modern Windows
- **USERINIT (userinit.exe)**
   - Sets up shell and then quits
   - Only visible briefly after log-on
- **Explorer (explorer.exe)**
   - Typical user shell launched with user's privileges (i/o SYSTEM's)
   - Likely parent for all processes started by logged-on user


## Windows Process Genealogy

![grafik](https://user-images.githubusercontent.com/84674087/133154388-3f4eb7b1-64d6-4db4-b070-0a4a1b56bde0.png)
