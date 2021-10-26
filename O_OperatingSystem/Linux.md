## Abbreviations

- **ACPI** (Advanced Configuration and Power Interface)
- **LVM** (Logical Volume Manager): Manage storage in server environments 
- **PPA** (Personal Package Archive): Selected beta releases of official main repositories
- **PAM** (Pluggable Authentication Modules)
- **TTY** (teletypewriter): Terminal ; Press Ctrl+Alt+F1-6 if GUI is freezed
- **APT** (Advanced Package Tool)
- **CGI** (Common Gateway Interface): 
   - Data exchange between webserver and Third Party SW
   - Used for first dynamic web site development back in old days
   - Forwarding of web requests to web server shell (ShellShock!)
- **YUM** (Yellowdog Updater Modifier): Like apt, but on RPM based Linux (Fedore, CentOS)
- **RPM** (Red Hat Package Management): Standardized Installation App
- **PCRE** (Perl Compatible Regular Expression)
- **RUID** (Real User ID): Describes user who created the process
- **EUID** (Effective User ID): Describes user whose file access permissions are used by the process
- **Ubuntu ESM** (Extended Security Maintenance): Ongoing patches after end of life of standard security patches

## Directories

#### Overview
- **bin/sbin** (binary/system binary): Programs
- **cdrom**: to mount CDs/DVDs
- **etc**: Configuration
- **media** (mount by OS): floppy disk, USB, ext. hard drive etc.
- **mnt** (mount manually)
- **opt** (optional): Data from vendors, self created stuff
- **proc** (process): Sudo proc files + kernel export data to user space
- **run**: For temporary data run in RAM
- **srv** (service): Data storage when OS is used as server
- **tmp** (temporary): Running applications store data here 
- **usr** (unix system resource): Non essential user data
- **var** (variable): for growing data (log files, crash reports)

**System Paths**
- `/usr/share/man/man1`: manuals
- `/etc/apt/sources.list`: Packet sources 
- `etc/shells`: valid login shells
- `/usr/share/doc/paketname/copyright`: Licences for each packet installed on machine 
- `/etc/sudoers`: sudo user policy
- `/etc/pam.d/common-password`: check enabled PW hash algorithm
- `grep -r -i [exploit_name] /usr/share/exploitdb/exploits/`: check available exploits on Kali

**Network Paths**
- `/etc/network/interfaces`: Config of eth0, eth1 etc.
- `/var/www/html/`: Web server path (index.html etc.)
- `/etc/apache2/mods-available`: Modules for Apache Server
- `/etc/ssh/sshd_config` 

## APT Package Tool

```
apt update
apt upgrade
apt full-upgrade --> upgrade + rm obsolete packages + install new dependencies
apt remove
apt purge --> remove package, config, user data
apt cache search [packet] --> check if packet is available
apt cache showpkg [packet] --> show packet information
apt cache -v --> show apt version
apt cache stats --> show statistics
apt cache unmet --> show unmet dependencies
apt cache depends [packet] --> show dependencies
apt cache policy --> show installed repository files
apt reinstall
apt clean --> empties directory /var/cache/apt/archives/
apt autoclean --> only removes packages that can no longer be downloaded, i.e. disappeared from mirror
apt list --upgradable
apt list --installed --> show all installed packages
apt policy --> show installed version
apt-file search [package] --> APT package searching utility
```

## dpkg (Debian Package) vs APT (Advanced Package Tool)

#### dpkg Features
- dpkg do installation/analysis of .deb packages and their contents
- dpkg will fail if a dependency is not met (APT fix this limitation)
- dpkg installs a package located on your local system
- dpkg does not automatically resolve dependencies

#### APT Features
- APT relies on dpkg but differs from it
- APT installs package from online source
- APT works to resolve dependencies
- APT was developed later to overcome design flaws of apt-get
- APT can be used as GUI via aptitude / synaptic

#### dpkg CMD
```
dpkg --listfiles package (or -L)
dpkg --search file (or -S)
dpkg --list (or -l)
dpkg --contents file.deb (or -c)
dpkg --info file.deb (or -I)
dpkg --verify (display modified system files)
```

## etc/shadow

*/etc/passwd --> 644 / rw-r--r--*

*/etc/shadow --> 640 / rw-r-----*

#### Format /etc/shadow
1. User
2. PW-Hash
   -  Hash Algorithm
   -  Salt (in between two $ signs)
   -  PW + Salt Hash
3. last change
4. Min.Days between PW change
5. PW validity
6. Warning threshold
7. Account inactive (days)
8. Time since account is disabled

![grafik](https://user-images.githubusercontent.com/84674087/133145945-6f2abac5-ac9d-41b4-b5a0-a53b14ee0aac.png)

#### Format /etc/passwd

![grafik](https://user-images.githubusercontent.com/84674087/133145975-8aea2c1e-ff8c-4db9-8373-c67905fdbda0.png)

#### Hash-Code /etc/shadow
- $1: MD5
- $2a: Blowfish
- $2y: eksBlowfish
- $5: SHA256
- $6: SHA512 
