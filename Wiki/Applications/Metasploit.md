## How To (Kali)

**Starting Point**
1. `systemctl start postgresql`
2. `systemctl enable postgresql`
3. `msfdb init`
    - Create SQL-DB in order to work with different Workspaces
    - Store scan results cumulative (better overview) 

**Msfconsole (Basic Commands)**
- `db_status`: check database
- `help`: command overview
- `workspace -a Lab`: add new workspace called "Lab"
- `workspace Lab`: Switch to workspace Lab
- `search type:scanner/exploit/auxiliary "keyword"`: search for "keyword" inside category auxiliary
- `search type:exploit platform:windows target:2008 smb`
- `info [module name]`
- `use [module loadpath]`
- `set [option] [option value]`
- `check`: to check exploitability before exploit execution)
- `exploit/run`: activate exploit

## Exploit Types

**Reliability Ranks In Metasploit For Exploit Search**
- Manual (worst)
- Low
- Average
- Normal
- Good
- Great
- Excellent (best)

**Add New Exploits/Modules**
1. Download from internet
2. move it to /usr/share/metasploit-framework/modules

**Exploit Troubleshooting**
- Run it a few more times (sometimes this works!)
- Change LPORT/RPORT
- Change payload
