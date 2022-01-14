# TABLE OF CONTENTS
1) [APT PACKAGE TOOL](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#apt-package-tool)
2) [BASH PROFILES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#bash-profiles)
3) [CLI](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#linux-cli)
4) [ETC/SHADOW](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#etcshadow)
5) [SSH](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#ssh)
6) [TERMINOLOGY](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#terminology)

<br />

# APT PACKAGE TOOL
## Common Commands
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

#### dpkg CLI
```
dpkg --listfiles [package] (or -L)
dpkg --search [file] (or -S)
dpkg --list (or -l)
dpkg --contents [file.deb] (or -c)
dpkg --info [file.deb] (or -I)
dpkg --verify (display modified system files)
dpkg-query -f'${binary:package}\n' -W > applist  #create list of installed apps and save in "applist"
```

<br />

# BASH PROFILES
**Credits to:** [Ivan](https://ivanitlearning.wordpress.com/2021/10/22/bash-configuration-files/)

- **/etc/profile**: This is a system-wide initialisation file that is executed during login. This file provides initial environment variables and initial “PATH” locations.
- **/etc/bashrc**: This again is a system-wide initialisation file. This file is executed each time a Bash shell is opened by a user. Here you can define your default prompt and add alias information. Values in this file can be overridden by their local ~/.bashrc entry
- **~/.bash_profile**: If this file exists, it is executed automatically after /etc/profile during the login process. This file can be used by each user to add individual entries. The file however is only executed once at login and normally then runs the users .bashrc file.
- **~/.bash_login**: If the .bash_profile does not exist, then this file will be executed automatically at login.
- **~/.profile**: If the .bash_profile or .bash_login do not exist, then this file is executed automatically at login.
- **~/.bashrc**: This file contains individual specific configurations. This file is read at login and also each time a new Bash shell is started. Ideally, this is where you should place any aliases.
- **~/.bash_logout**: This file is executed automatically during logout.
- **~/.inputrc**: This file is used to customize key bindings/key strokes.

<br />

To note: `/etc/profile` is executed for **interactive shells** while `/etc/bashrc` is loaded for both **interactive and non-interactive shells**

<br />

# LINUX CLI
## Table of Contents
1. [Basics](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#basics)
2. [Configuration](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#configuration)
3. [Network](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#network)
4. [Data / File](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#data--file)
5. [Security / Encryption](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#security--encryption)
6. [User / Groups](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#user--groups)
7. [System](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#system)
8. [Applications](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#applications)

<br />

## Basics
- `[command1] && [command2]`: command2 gets executed when command1 finished successfully 
- `Alt + print-key`: Screenshot
- `Alt + "+"`: zoom in 
- **pwd**: print working directory
   - `pwdx [pid]`: print workig directory of process pid  
- **echo**: print function
- **xargs**: build and execute command lines from standard input
   - `find | xargs 2>/dev/null | base64 -d | strings -n 8`
   - `ls | while read line; do xargs $line; done`
- **man**: show manual   
   - `man [command]`
   - `/` = search within manual
   - jump through search result: `N` (forward)/`Shift+N` (backward)
- **ls**: show content of directory 
    - `ls -a` ("all")
    - `ls -l` ("long", more detailed)
- **cd**: change directory
    - `cd ..` (parent directory)
    - `cd ~` (Home directory)
    - `cd /` (root directory)
- `Strg + C`: abort process
- **exit**: finish terminal
- `mkfifo [Option] [Name]`: create named pipe (e.g. from terminal1 to terminal2)
- **date**: show date and time 
   - datum = $(date +%d.%m.%Y)
   - touch $(date +`hostname`-%d-%m-%y-%H%M.log)
- **cal**: calendar
- **background**
   - `[command] &`: perform [command] in background 

<br />

## Configuration

- **bashrc** (bash resource): script file that’s executed when a user logs in
   - `nano ~/.bashrc`: configure bashrc
- **$PS1**: (Primary) Prompt Shell Variable
   - Example: PS1="[\u@\h \w]$" --> [user@host working directory]$
- **$RANDOM**: Generates random integer between 0 and 32,767 each time it is referenced
   - `echo $(($RANDOM % 100))`: random number between 0 and 99
- **$PATH**: Indicates the search path for commands
- **$LANG**: Display Language
- **chsh**: change shell
   - (1) `cat /etc/shells` (check existing shells) 2) `chsh -s $(which zsh)` (switch shell)
   - `chsh -s /bin/rbash [username]` (apply restricted shell to user)
- **timedatectl**: show time settings 
   - `timedatectl list-timezones`
   - `timedatectl set-timezone`
   - `timedatectl set-local-RTC 0`
- **DEBIAN_FRONTEND**: environment variable for adjusting debconf (Debian package configuration system)
   - `DEBIAN_FRONTEND=noninteractive apt-get -y update`
   - `DEBIAN_FRONTEND=noninteractive apt-get -y upgrade`
   - `DEBIAN_FRONTEND=dialog` (default frontend for apt/apt-get )
   - `DEBIAN_FRONTEND=readline` (most traditional; for slow remote connections; entirely CLI)
- **tasksel**: a user interface for installing tasks
- **update-alternatives**: creates, removes, maintains and displays information about the symbolic links comprising the Debian alternatives system
   - `update-alternatives --query editor` to check the installed editors on the system
   - `update-alternatives --config x-session-manager` to choose a particular implementation of x-session-manager (e.g. GNOME, XFCE, Cinnamon etc.)

<br />

## Network
- **ifconfig**: show interface details
- **ip**:
   - `ip addr show`
   - `ip addr sh eth0`
   - `ip -br link show` (br=brief)
- **netstat**: print network connections
   - `netstat -tulpn`
- `ping [IPv4]`
- **host**: Identify host
   - `host [IPv4]`   
- **openssl**:
   - `openssl [command] -help`
   - `openssl s_client -connect host:port`
   - `openssl enc -aes256 -k secret101 -in /tmp/backup.tgz  -out /tmp/backup.tgz.enc`: create encrypted backup archive non-interactive with -key "secret101"
   - `openssl enc -aes256 -k secret101 -d -in file.txt.enc -out file.txt`: decrypt file non-interactive with supplied key "secret101"
- **scp** (OpenSSH secure file copy):
   - `scp option source user@host:/tmp`
- **fuser**: find out process that opened specific port
   - `fuser 22/tcp`: SSH pid will be shown
- **ufw** (uncomplicated FW): managing netfilter FW
   - `ufw status`: show FW status
- **ipv6toolkit**:
   - `sudo scan6 -i [interface] -L -P local --print-unique -e`: get IPv6 + MAC
- **traceroute**: UDP probe by default (often ignored by FW though)
   - `traceroute -I example.com` (-I = send ICMP probe)
   - `traceroute -w 10 example.com` (-w = wait for response in seconds)
- **iperf**: check bandwidth between two \*nix machines
- **ssh**
   - `ssh username@host -p port`
   - `ssh username@host -i privateKey`
   - `ssh username@host 'bash --noprofile / --norc'`: start ssh session with clean profile
   - `ssh username@host /bin/bash << command1 ; command2; EOF`
   - `ssh username@host 'bash -s' < script`
   - `ssh -t user@host 'bash -l'`: -t = interactive tty ; -l = login shell
   - `ssh -f -N -L [localPort]:[remoteHost:port] user@remoteHost`: LocalPortForwarding
   - `ssh -f -N -R [remotePort]:[localHost:port] user@remoteHost`: ReversePortForwarding
   - `ssh -f -N -D [localPort] user@remoteHost`: DynamicPortForwarding to evade FW for instance
   - `ssh -Q cipher`: check available ciphers of ssh client
   - `nmap -p22 -n -sV --script ssh2-enum-algos [IPv4]`: check ciphers of SSH server
   - `ssh -o KexAlgorithms=diffie-hellman-group1-sha1 user@host`: set specific algorithm option
- **iptables**
   - See here:[Wiki/iptables](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Wiki/Applications/Iptables.md) 

<br />

## Data / File
- `./[binary or script]`: execute binary/script
- **STDIN: 0 / STDOUT: 1 / STDERR: 2**
    - `2>&1`: redirect STDERR to STDOUT (">&" means "redirect file descriptor")
    - `&>/dev/null`: redirects all output to /dev/null
- **cp**: copy from to
    - `cp example.txt /var/www/html/`
- **less**: display data page by page
    - `q`: quit
- **head**: show first lines of file
- **tail**: show last lines of file
- **mv**: 1) Rename file 2) move file from to
    - `mv example1 example2`
    - `mv example1 /tmp`
- **rm**: remove file 
    - `rm *`: remove all data 
    - `rm -rf`: remove non-empty directory (-r=recursively, -f=no prompt)
- **mkdir**: create directory 
    - `mkdir -p lib/x86_64_so`: create directory including parent directory
    - `mkdir /home/newuser/{downloads,uploads}`: create several files at once
- **mktemp**: create file/directory with random name
    - `mktemp -d dir.XXXX` (-d = directory)
- **rmdir**: remove directory 
- **unlink**: to remove the specified file
    - `unlink [file]`
- **wc**: word count (lines / words / bytes / filename)
- **grep**: search for text file 
    - `-i`: ignore uppercase/lowercase 
    - `-v`: invers 
    - `-w`: treat serach term as word 
    - `-c`: return count of matching strings
    - `-l`: return name of files with matching lines
    - `-o`: print only matched parts (-o "s" ; -o "Word")
    - `-A NUM`: print NUM lines of trailing context after matching lines (`grep -A 3 passwd /home/.bash_history`)
    - `-B NUM`: print NUM lines of leading context before matching lines
    - `ls | grep .pdf`
    - `grep 'word1\|word2'`: search two terms 
    - `grep "10\.1\.0\.10\," firewall.log | grep "23$"`
    - `grep -r -i "voldemort" /tmp/*.sh`
- **cat**: concatenate/read the file and output content
    - `cat -b dictionary.txt`
- **which** [data]: Returns path of linux file if existing in PATH
- **locate** [string]: Returns all paths that contain [string]
- **whereis** [data]: Returns all paths
- **find**:
    - `find ./dir1/dir2 -name example.txt`: look for example.txt in dir2
    - `find . -readable -and -size 1033c`: look for readable file with 1033 bytes
    - `find ./dir -perm 664`: look for file in /dir with permission 664
    - `find /usr/bin/ -perm 4000` Find files with suid functionality
    - `find . -empty`: find empty files in current dir
    - `find -name '*.php' -mtime -1 -ls`: find .php with modification time 
    - `find $HOME -mtime 0`: find all file in home directory with modification within last 24 hours 
    - `find /home -name .bashrc -exec grep "secret" {} \;`: find all .bashrc files in /home and apply grep with pattern "secret" upon
- **file**: display data-type info
- **zip/unzip**: for packages
- **tar**: Archive program for files and directories 
     - `tar -xvf [file]`: extract file verbosly
     - `tar -cvf [file] /etc`: create file verbosly 
     - `tar -cf archiv.tar test.txt test2.txt`: create archiv with files "test" and "test2"
     - `tar -xzvf archiv.tar.gz`: extract zipped file verbosly
- **bzip2**:
     - `bzip2 -d file.bz2`: decompress bz2 file 
- **cpio** (copy in and out)
     - `cpio -t < backup.cpio`: list the files insde the archive with extraction
     - `cpio -iv < backup.cpio`: extract backup.cpio verbosely in current directory 
     - `cpio -ocv0  > /tmp/archive.cpio`: create cpio archive verbosely, wherein files are delimited by null character
- **sleep**: invoke delay (indicate in seconds)
- **wget**: non-interactive download of files from the Web
- **dd**: convert and copy a file (dd if=file_in of=file_out bs=1 skip=40)
- **pr** (print): Does formatting of files on the terminal screen or for a printer
- **touch**: 
    - `touch -a [filename]`: change access timestamp of file (-a access/-m modification time)
    - `touch -m [filename]`: change modification timestamp
    - `touch [filename1] -r [filename2]`: apply timestamp from f1 upon f2
    - `touch -h [filename]`: change timestamp of symbolic link (i/o original file)
    - `touch [filename]`: create file 
    - `touch -c [filename]`: do not create file if file does not exist yet (but only change timestamp)
    - `touch /tmp/'dir;bash -p'`: create file/dir + start bash 
- **ln**: create soft links
    - `ln -s [file] [name]`: soft link with self-created name
      - `-s` = soft link
      - hard links by default
- **sort**: Returns sorted text file 
    - `-r` = sorted reverse
    - `-n` = sorted in numerical order
    - `-k 2` = sorted acc. to second column
    - `-t ","` = delimited by ","
    - `sort -t "," -k 2 syslog.txt`
- **uniq**: retrieve unique elements from file
    - `uniq -u [word]`: -u = unique 
- **tr**: translate/squeeze/delete characters from stdin
    - `cat linux.txt | tr [a-z] [A-Z]`: Change text from lowercase to uppercase
    - `echo "TEXT" | tr a-zA-Z n-za-mN-ZA-M` (ROT13/Cäsar-Encryption)
    - `tr -s ' ' '\n'`: replace space with newline
- **nano**:
    - `Ctrl+Shift+6`: Mark block, then move cursor, then Strg+K to delete
    - `nano -l [file]`: show line number
- **vi/vim**:
    - `i`: start insert Mode
    - `ESC`: exit insert Mode
    - In Normal mode: `y/y^/y$` (copy), `d/d$` (delete), `p` (paste)
    - `:wq` (write and quit)
    - `:wq!` (write, quit and override)
    - [Spawn shell inside vim](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Wiki/Restricted%20Shell%20Escape.md)
- **tee**: read from standard input and write to standard output and files
- **sed**: Stream Editor, useful with regex
    - `cat [file] | sed /regex-pattern/action`
    - action: d(elete), s(ubstitute), -n p(rint)
    - `cat /etc/passwd | sed '1,5s/sh/quiet/g'`
    - `cat /etc/passwd | sed -n '1,3p'`
    - `cat testing | sed '/^daemon/d'`
    - [Tutorialspoint](https://www.tutorialspoint.com/unix/unix-regular-expressions.htm)
- **cut**: Remove specific part of results
    - `cut -c5-5 syslog.txt`: returns 5th - 10th char. in each line
    - `cut -d " " -f1-4 syslog.txt`: returns first four entries of each line, delimited by " "
- **unshadow**:
    1. `sudo unshadow /etc/passwd /etc/shadow > password.txt`
    2. `john password.txt`
- **eog**: GNOME image viewer
    - `eog *` show all photos 
- **awk/gawk**:
    -  Predefined variables
       - `RS`: record separator. Normally one line of the input file
       - `NR`: Current input record number. Normally current input line nmumber
       - `NF`: Number of fields in current record. Normally fields separated by FS/OFS (white space) and thus: field = word
       - `FS/OFS`: Input and Output Field Separator. Default is "white space"   
    - *awk pattern { action }*: if pattern is evaluated true, action is executed
    - `awk '1 { print }' file` or `awk 1 file`:  print each line of file
    - `awk 'NR>1' file`: print all lines except first
    - `awk 'NF' file`: print all lines with at least one non-whitespace (NF=0 -> line has only white space)

<br />

## Security / Encryption
- **md5sum**
   - `echo -n admin | md5sum`: create md5 hash of "admin" (Don't forget `-n` o skip newline)
- **sha256sum**
- **sha384sum**
- **sha512sum**
- **gpg**: built-in encryption/decryption tool (e.g. password vault, signature)
   - `gpg --full-gen-key`: generate keys + user ID
   - `gpg -c file`: encrypt with password (based on AES128 algorithm)
   - `gpg --encrypt file`: encrypt file with generated key + user ID
   - `gpg --decrypt file`: alternatively: gpg file.gpg
   - `gpg --keyserver pgp.mit.edu --search-keys example@email.com`: Search for public key online
   - `gpg --keyserver pgp.mit.edu --receive-keys 48BF6357AB80EB5E`: Get public key via key ID
   - `gpg --recipient example@email.net --armor --encrypt plain.txt`
      - `--armor` = for base64 encoded output
      - `--recipient` = to specify the public key
   - `gpg --keyserver pgp.mit.edu --send-keys [your fingerprint]`: Push your public key to keyserver 
   - `gpg --keyserver pgp.mit.edu --refresh-keys`: To check if your key has been successfully sent
- **cryptsetup**
   - `cryptsetup luksDump /dev/sba1`: LUKS header information
   - `sudo cryptsetup luksFormat -c aes-xts-plain64 -s 512 -h sha512 -y /dev/sba`: create encrypted partition. You will be asked for a password
   - `cryptsetup luksAddKey --key-slot=2 /dev/sba2`: A single encrypted partition can have eight different keys. This command adds one key on slot 2
- **lvm**
   - `lvm vgdisplay`: show volume group info 
   - `lvm vgs`: show info of volume groups
   - `lvm lvs`: Report information about Logical Volumes
- **fail2ban**
   - rate limiting to mitigate brute force attacks
   - `git clone https://github.com/fail2ban/fail2ban.git`
   - `cd fail2ban`
   - `sudo python setup.py install`
   - Details: [https://kalilinuxtutorials.com/fail2ban/](https://kalilinuxtutorials.com/fail2ban/)
 

<br />

## User / Groups
- **id**: show ID of user
    - `id [user]`
- **passwd**: Create new password for current user
- **smbpasswd**: Create new Samba password for current user
    - `smbpasswd -a [user]` (-a = add)
    - Ensure synchronization of Samba DB: smb.conf --> global setting --> `unix password sync` 
- **whoami**: Current User
- **users/who/w/finger**: Show Logged-In Users
- **su**: switch user account
    - `su [username]` 
- **chown**: change owner
    - `chown alice:alice document.docx`: user and group is "alice"
- **chgrp**: change group
- **chmod**: user (u), group (g) and others (o)
    - `chmod u=rw,g=rw,o=r [file name]`
    - `chmod o+w [file name]`
    - `chmod g-w [file name]`
    - `chmod 750 [file name]` (-rwx r-x ---)
    - `chmod 777 .` 
    - `chmod a=r [file name]`: set read-permission for "all"
    - `chmod 4755 file`: set setuid
    - `chmod +xs file`: set setuid
    - `chmod 2755/g+s file`: set setguid
    -  r/w/x | binary | octal
       ----- | ------ | -----
        ---  |  000   |   0
        --x  |  001   |   1
        -w-  |  010   |   2
        -wx  |  011   |   3
        r--  |  100   |   4
        r-x  |  101   |   5
        rw-  |  110   |   6
        rwx  |  111   |   7
- **useradd**: Adds accounts to the system
    - `useradd -d homedir -g groupname -m -s shell -u userid accountname`
    - `-m` = Creates the home directory if it doesn't exist
    - `-s /bin/false` = the new user would not be able to login via SSH
    - `useradd -d /home/mcmohd -g developers -s /bin/ksh mcmohd`
    -  The useradd command modifies /etc/passwd, /etc/shadow, and /etc/group (!)
- **usermod**: Modifies account attributes
    - `usermod -a -G sudo user` (appends user to group sudo)
- **userdel**: Deletes accounts from the system
    - `deluser user group` (deletes user from group)
- **groups**: list all groups of current user
- **groupadd**: Adds groups to the system
    - `groupadd [-g gid [-o]] [-r] [-f] groupname`
    - `-o` = with non-unique GID
    - `-r` =  add a system account
    - `-f` = exit if group already exists
- **groupmod**: Modifies group attributes
- **groupdel**: Removes groups from the system
- **chfn**: change user information
    - `chfn [user]`
    - `finger [user]`: Einträge von chfn anzeigen
- **history**: show command history of user
- **getent**: get entries from Name Service Libs
    - `getent group sudo`
- **sudo**:
    - `sudo -l`: list allowed commands
    - `sudo -u victim /bin/bash`: if allowed you can run commands on behalf of other user e.g. victim

## System
- **apt**
    - `apt update`
    - `apt upgrade`
    - More details: [BlueTeamOthers/Linux](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Y_BlueTeamOthers/Linux.md#apt-package-tool) 
- **shutdown**
    - `shutdown -h now`: Instant shutdown
    - `shutdown -r now`: reboot
- **reboot**
- **Read-in CD**
    - `apt-cdrom add /media/cdrom`
- **service**:
    - `service [program] restart`: restart service (after config change)
    - `service [program] status`: show status 
    - `systemctl status [program]` 
- **nohup** (no hangup): continue command even user logs out or exit shell
- **journalctl**: query the systemd journal
    - `journalctl -xe`
- **lsusb**: display usb devices
- **lsmod**: display modules in the linux kernel
- **udevadm**: u(ser)dev(ice)adm(inistration) tool
    - `udevadm info -a -p /sys/bus/usb/devices/1-1`: -p = path, 1-1 = bus1 & port1
- **uname**: print system information (kernel etc.)
    - `uname -r`: show distribution version
    - `uname -a`: show all
- **uptime**: show uptime
- **lsb_release**: print distribution specific information (lsb=Linux Standard Base)
    - `lsb_release -a`: show all
    - `lsb_release -c`: show codename of distribution
    - `lsb_release -s`: show information without header
- **df**: show disk space of complete file system
    - `df -ah`
- **du**: show disk usage of files in a directory
    - `du -ah /etc`
- **ps**: display information of active processes
    - VSZ (Virtual MemSize) / RSS (Physical MemSize) / TTY (?=none) / STAT (S=sleeping,R=running)
    - `ps -fp [pid]`: show corresponding CLI command 
    - `ps axu | grep [pid/program]`
    - `ps aux --sort=-%mem | less`
- **dmidecode**: displays the S(ystem)M(anagement)BIOS/DMI in a human-readable way
- **export**: show environment variables 
    - `export PS1='$ '` set PS1 to '$ '
- **modprobe**: remove/add modules
- **dmesg**: show Kernel-Ringpuffer
    - `dmesg -H` 
- **lspci**: Show PCI Devices
     - `lspci -vnn | grep [x]`: -vnn = verbose + PCI Vendor name & numbers
- **lsof**: Anzeige von belegten Ressourcen
    - `lsof -i :22` (SSH-Ressourcen)
    - `lsof -p [pid]`
    - `lsof -u [uid]`
    - `lsof -R [pid]` (show PPID)
- **free**: Memory Consumption
- **top**: Memory Consumption
- **kill**: send signal to process
    - `kill -l`: show all available signals
    - `kill -9 [PID]`
    - `sudo killall sshd`: kick out unauthorized user
- **htop**: GUI top
- **systemd**
- **pstree**: Show parent/child relation of processes
- **fsck**: file system check
- **cron**:
    - `* * * * * /usr/bin/echo.sh >> /dev/pts/0`: redirect output from echo.sh
    - `*/2 * * * * command`: execute command every two minutes
- **crontab**: 
    - `crontab -l`: display cron jobs
    - `crontab -u root -l`: user specific)
    - `grep -r [cronjob] /etc/cron.* /etc/crontab`
- **write**: send a message to another user on the host
- **mesg**: display (or do not display) messages from other users
- **jobs**: 	Lists all jobs
    - `bg %n`: 	Places job in background, where n is the job ID
    - `fg %n`: 	Brings job into foreground, where n is the job ID
    - `Control-Z`: Stops foreground job, places it in the background as stopped job
    - `[command] &`: "&" puts job in background
- **screen**: terminal multiplexer
    - `screen -S [name]`: start screen session with specified name
    - start task in window 0
    - `Ctrl+A, c`: create new window 1 (create another task)
    - `Ctrl+A, 0 or 1`: switch windows
    - `Ctrl+A,Shift+S`: split window horizontally
    - `Ctrl+A, Tab`: switch between split windows
    - `Ctrl+A, (|)`: split vertically
    - `Ctrl+A, Q`: Close all regions except the current one.
    - `Ctrl+A, X`: Close the current region
- **tmux**: Terminal Multiplexer
    -  Change default prefix key (from C-b to Alt-q):
       - `set-option -g prefix M-q`
       - `unbind-key C-b`
       - `bind-key M-q send-prefix`
    - Common commands:
       - `tmux set-option -g status-style bg=blue`: change background color of status bar
       - `prefix key + "`: split into top and bottom
       - `prefix key + %`: split into left and right
       - `prefix key + $`: rename current session
       - `prefix key + ,`: rename current window
       - `prefix key + n`: switch to next window
       - `prefix key + up/down/left/right`: switch to next pane
       - `prefix key + c`: create new window
       - `prefix key + x`: kill current pane
       - `prefix key + w`: choose current window interactively
       - `prefix key + 0 to 9`: select windows 0 to 9
- **grub**: boot loader
    - `grub-mkpasswd-pbkdf2`: protect GRUB from anyone who boots your computer
    - `cat /var/log/boot.log`: review boot log
    - `nano /etc/default/grub`: change grub settings (timeout etc.)
- **lsblk**
    - `lsblk -o PATH, UUID`: show dev path and UUID  

## Applications
- **mysql**
    - `mysql -u root`: get access as root user without password
    - `mysql -u root -p`: you get prompted to enter a password
    - `show databases;`
    - `use [DATABASE];`
    - `show tables;`
    - `select * from [TABLE];`
    - `select load_file('/full/path/to/file.txt');`: Display content of specified file
- **postgres**
    - `psql`: start local postgreSQL DB (you need to be postgres-user on your machine)
    - `\list`: to list the databases
    - `\c [DATABASE]`: to connect to database
    - `\d`: to list the tables
    - `\d+`: to list the tables in detail
    - `SELECT * FROM [TABLE];`: select desired information
    -  Once you gain access, you can read files from file system:
       - `CREATE TABLE demo(t text);`
       - `COPY demo from '[FILENAME]';`
       - `SELECT * FROM demo;`
       - `DROP TABLE demo;`
    - `\q`: exit postgres
- **swlite3**:
    - `sqlite3 [file]`: connect to databse [file]
    - `.tables`: get a list of tables
    - `SELECT * FROM [table]`: extract the content of a table using SQL

<br />

# ETC/SHADOW
- **/etc/passwd --> 644 / rw-r--r--**
- **/etc/shadow --> 640 / rw-r-----**

## Format /etc/shadow
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

## Format /etc/passwd

![grafik](https://user-images.githubusercontent.com/84674087/133145975-8aea2c1e-ff8c-4db9-8373-c67905fdbda0.png)

## Hash-Code /etc/shadow
- $1: MD5
- $2a: Blowfish
- $2y: eksBlowfish
- $5: SHA256
- $6: SHA512 

<br />

# SSH
*nano /etc/ssh/sshd_config*

## Best Practice (Blue Team)
1. Change to uncommon SSH Port: 22 --> 2323
2. Add new line for max. Logon Attempts: "MaxAuthTries 3"
3. PermitRootLogin: No
4. Disable password-based access (instead key based, openssl)
5. Whitelist Users
   - Add new line in sshd_config:
     - AllowUsers user1 user2
     - AllowGroups group1 group2
     - DenyUsers user1 user2
     - DenyGroups group1 group2
6. Whitelist IP Addresses***
   - Add new line in /etc/hosts.allow:
     - sshd: 10.83.33.77/32
   - Add new line in /etc/hosts.deny:
     - sshd: ALL (all denied except whitelisted IP Addresses)
7. Conditional Login****
   - Add new line in sshd_config:
   - Match [User/Group/Host/Address]
      - Condition 1
      - Condition 2
   - Example:
      - Match Address 192.168.178.0/24
      - PermitRootLogin yes
8. MultiFactorAuthen via additional tools / libraries

<br />

# TERMINOLOGY
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

## System Paths
- `/usr/share/man/man1`: manuals
- `/etc/apt/sources.list`: Packet sources 
- `etc/shells`: valid login shells
- `/usr/share/doc/paketname/copyright`: Licences for each packet installed on machine 
- `/etc/sudoers`: sudo user policy
- `/etc/pam.d/common-password`: check enabled PW hash algorithm
- `grep -r -i [exploit_name] /usr/share/exploitdb/exploits/`: check available exploits on Kali

## Network Paths
- `/etc/network/interfaces`: Config of eth0, eth1 etc.
- `/var/www/html/`: Web server path (index.html etc.)
- `/etc/apache2/mods-available`: Modules for Apache Server
- `/etc/ssh/sshd_config` 

<br />
