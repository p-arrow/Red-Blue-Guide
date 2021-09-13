## Abbreviations

- ACPI (Advanced Configuration and Power Interface)
- LVM (Logical Volume Manager): Manage storage in server environments 
- PPA (Personal Package Archive): Selected beta releases of official main repositories
- PAM (Pluggable Authentication Modules)
- TTY (teletypewriter): Terminal ; Press Ctrl+Alt+F1-6 if GUI is freezed
- APT (Advanced Package Tool)
- CGI (Common Gateway Interface): 
   - Data exchange between webserver and Third Party SW
   - Used for first dynamic web site development back in old days
   - Forwarding of web requests to web server shell (ShellShock!)
- YUM (Yellowdog Updater Modifier): Like apt, but on RPM based Linux (Fedore, CentOS)
- RPM (Red Hat Package Management): Standardized Installation App
- PCRE (Perl Compatible Regular Expression)
- RUID (Real User ID): Describes user who created the process
- EUID (Effective User ID): Describes user whose file access permissions are used by the process
- Ubuntu ESM (Extended Security Maintenance): Ongoing patches after end of life of standard security patches

## Directories

**System**
- /usr/share/man/man1: manuals
- /etc/apt/sources.list: Packet sources 
- etc/shells: valid login shells
- /usr/share/doc/paketname/copyright: Licences for each packet installed on machine 
- /etc/sudoers: sudo user policy
- /etc/pam.d/common-password (check enabled PW hash algorithm)
- grep -r -i [exploit_name] /usr/share/exploitdb/exploits/ (check available exploits on Kali)

**Network**
- /etc/network/interfaces: Config of eth0, eth1 etc.
- /var/www/html/: Web server path (index.html etc.)
- /etc/apache2/mods-available: Modules for Apache Server
- /etc/ssh/sshd_config 
