# TABLE OF CONTENTS
1) [APT PACKAGE TOOL](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#apt-package-tool)
2) [BASH PROFILES](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#bash-profiles)
3) [COMMAND LINE INTERFACE (CLI)](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#linux-cli)
4) [ETC/SHADOW](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#etcshadow)
5) [TROUBLESHOOTING](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#troubleshooting)

<br />

# APT PACKAGE TOOL
## Common Commands
```
apt update
apt upgrade
apt full-upgrade --> upgrade + rm obsolete packages + install new dependencies
apt remove
apt purge --> remove package, config, user data
apt-cache search [packet] --> check if packet is available
apt-cache showpkg [packet] --> show packet information
apt-cache -v --> show apt version
apt-cache stats --> show statistics
apt-cache unmet --> show unmet dependencies
apt-cache depends [packet] --> show dependencies
apt-cache policy --> show installed repository files
apt-reinstall
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
grep "installed" /var/log/dpkg.log               #get list of recently installed apps
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
   - `man 7 man`: open man(7)
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
- **kali-undercover**: 
   - `kali-undercover`: Kali undercover mode to pretend Windows OS

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
- **tasksel**:
   - a user interface for installing tasks
   - or installing desktop environments, fonts etc.
- **update-alternatives**: 
   - creates, removes, maintains and displays information about the symbolic links comprising the Debian alternatives system
   - `update-alternatives --query editor`: to check the installed editors on the system
   - `update-alternatives --config x-session-manager`: to choose a particular implementation of x-session-manager (e.g. GNOME, XFCE, Cinnamon etc.)
   - `update-alternatives --config java`: config default java version

<br />

## Network
- `/etc/network/interfaces`: Config of eth0, eth1 etc.
- `/etc/apache2/mods-available`: Modules for Apache Server
- **ifconfig**: show interface details
- **ip**:
   - `ip addr show`
   - `ip route show`
   - `ip addr sh eth0`
   - `ip -br link show` (br=brief)
- **netstat**: print network connections
   - `netstat -tulpn`
- **ss**: another socket utility 
   - `sudo ss -tulpn` 
- **ping**:
   - `ping [IPv4]`
   - `ping -c [Number] [IPv4]`: specify the amount of package with [Number]
- **host**: Identify host
   - `host [IPv4]`   
- **openssl**:
   - `openssl [command] -help`
   - `openssl list -help`
   - `openssl s_client -connect host:port`
   - `openssl enc -aes256 -k secret101 -in /tmp/backup.tgz  -out /tmp/backup.tgz.enc`: create encrypted backup non-interactively with -key "secret101"
   - `openssl enc -aes256 -k secret101 -d -in file.txt.enc -out file.txt`: decrypt non-interactively with supplied key "secret101"
   - **Generate Fingeprint from x509.pem**:
   - `openssl x509 -in x509.pem -noout -fingerprint`: Result may look like `SHA1 Fingerprint=9E:65:2E:03:...:97:0A:4D:F4:4D`
   - **Generate Private Key & Certificate (Short)**:
   - `openssl req -newkey rsa:2048 -nodes -keyout priv.pem -x509 -days 365 -out ./myCert.crt -subj "/CN=myName"`: Create cert and private key
   - **Generate Private Key & Certificate (Long)**:
   - `openssl genrsa -out private.key 1024`: Generate private key
   - `openssl req -new -x509 -key private.key -out publickey.cer -days 365`: Generate certificate 
   - `openssl pkcs12 -export -out public_privatekey.pfx -inkey private.key -in publickey.cer`: Export your x509 certificate and private key to pfx file
- **scp** (OpenSSH secure file copy):
   - Syntax: `scp option source destination`
   - `scp -v -P 2222 admin@192.168.0.23:/storage/Download/file.pdf /tmp`: copy from remote server to /tmp verbose, port 2222
   - `scp -v -P 234 /home/Download/text.txt server@192.168.0.20:/home/Documents/`: copy from own machine to remote server
- **fuser**: find out process that opened specific port
   - `fuser 22/tcp`: SSH pid will be shown
- **ufw** (uncomplicated FW): managing netfilter FW
   - `sudo ufw status verbosely`: show FW status
   - `sudo ufw enable/disable/reload`
   - `sudo ufw deny 53`
   - `sudo ufw allow 80/tcp`
   - `sudo ufw allow proto udp from 1.2.3.5 port 5469 to 1.2.3.4 port 5469`
   - `sudo nano /etc/ufw/before.rules` -> `-A ufw-before-forward -p icmp --icmp-type echo-request -j DROP`: drop pings from other hosts
- **ipv6toolkit**:
   - `sudo scan6 -i [interface] -L -P local --print-unique -e`: get IPv6 + MAC
- **traceroute**: UDP probe by default (often ignored by FW though)
   - `traceroute -I example.com` (-I = send ICMP probe)
   - `traceroute -w 10 example.com` (-w = wait for response in seconds)
- **iperf**: check bandwidth between two \*nix machines
- **iptables**
   - See here:[Wiki/iptables](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Wiki/Applications/Iptables.md) 
- **ssh**
   - **Create SSH Key Pair**
   - `ssh-keygen`: Enter directory to store the keys and passphrase
   - Put your generted public key on the remote server into the file `~/.ssh/authorized_keys`
   - **Establish SSH Connection**
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
   - **Install SSH Service on Linux Server**
   - `sudo apt install openssh-server
   - `service ssh start`
   - `service --status-all`: for verification
   -  **Best Practice (Blue Team)**
      -  All changes to be made here: **/etc/ssh/sshd_config**
      1. Change to uncommon SSH Port: 22 --> 2323
      2. Add new line for max. Logon Attempts: `MaxAuthTries 3`
      3. PermitRootLogin: `No`
      4. Disable password-based access (instead key based, openssl)
      5. Whitelist Users
         - Add new line in sshd_config:
         - `AllowUsers user1 user2`
         - `AllowGroups group1 group2`
         - `DenyUsers user1 user2`
         - `DenyGroups group1 group2`
      6. Whitelist IP Addresses:
         - Add new line in /etc/hosts.allow: `sshd: 10.83.33.77/32`
         - Add new line in /etc/hosts.deny: `sshd: ALL` (all denied except whitelisted IP Addresses)
      7. Conditional Login:
         - Add new line in sshd_config:
         - `Match [User/Group/Host/Address]`
            - `Condition 1`
            - `Condition 2`
         - Example:
            - `Match Address 192.168.178.0/24`
            - `PermitRootLogin yes`
      8. MultiFactorAuthen via additional tools / libraries
 - **curl**:
   - `curl example.com`
   - `curl --head example.com`: Fetch headers only
   - `curl example.com --dump-header -`: dump header
   - `curl --header "Content-Type: text/xml" example.com`: Fetch target with specified Header field
   - `curl -X GET example.com`: Specify HTTP MEthod as GET
   - `curl -X DELETE example.com/include/config.db`: delete data
   - `curl -X OPTIONS example.com --head`: show available HTTP Methods
   - `curl -T file example.com`: upload file to target
   - `curl -O example.com/file`: write output to file named like remote file
   - `curl -u username:password http://example.com`
   - `curl -X POST -H "Content-Type: application/json" -d '{"username":"joe","password":"5"}' http://[...]/register`: register yourself
   - `curl -X POST -H "Content-Type: application/json" -d '{ "token": "9..2", "filename": "t.txt", "content": "DATA"}' http://[..]/upload`: Upload file
   - `curl -X POST -H "Content-Type: application/xml" --data @payload.xml http://example.com/foo`: Send payload via POST
   - `curl -X HEAD 'example.com' -F "file=@webshell.jsp" -vv`: upload file
   - `curl -X GET https://example.com/extras/ --cookie "PHPSESSID=ovv...ekc3"`: send Cookie
   - **Write interactive script**:
     - `nano detect.sh`: create script
     - `curl --header [your payload] $1`: predefine the payload an add $1 at the end to execute the first argument given to the script
     - `./detect.sh [URL]`: start the script and enter your desired URL
   - **Use curl for OpenSourceVulnerability DB (OSV)**:
   - `curl -X POST -d '{"version": "2.4.1", "package": {"name": "jinja2", "ecosystem": "PyPI"}}' "https://api.osv.dev/v1/query"`: Linux
   - `curl -X POST -d "{\"package\": {\"name\": \"mruby\"}, \"version\": \"2.1.2rc\"}" "https://api.osv.dev/v1/query"`: Windows (avoid single quotes)
- **netcat/nc**
   - Syntax: `nc host port`
   - `echo -ne "HEAD / HTTP/1.1\r\nHost: 192.168.0.10\r\nConnection: close\r\n\r\n" | netcat 192.168.0.10 80`: send HTTP Head request via netcat
- **wkhtmltopdf**
   - [https://wkhtmltopdf.org/](https://wkhtmltopdf.org/)
   - `sudo apt install wkhtmltopdf`
   - `wkhtmltopdf http://google.com google.pdf`: create pdf of google website 
- **ifdown**: bring a network interface down
   - `sudo ifdown -a`: bring down interfaces according to `/etc/network/interfaces`
- **ifup**: bring a network interface up
   - `sudo ifdown -a`: bring up interfaces according to `/etc/network/interfaces`
- **tcpdump**
   - `sudo tcpdump -ni eth0 -s0 -A icmp`
   - `sudo tcpdump -i enp0s3 port telnet -w telnetloginattempts.pcap`
   - `sudo tcpdump host [IPv4] -s0 -A` (listen to raw packets on IPv4)
   - **Options**
     - `-w test.pcap`: write .pcap
     - `-r test.pcap | read .pcap
     - `-D`: show all interfaces
     - `-A`: print each packet in ASCII; good for capturing web pages
     - `-i eth0 -vv`: select specific interface eth0 verbosely
     - `-n`: numeric, don't resolve names
     - `-s0`: snaplen to default = 262144 bytes = data from each packet
     - `host`: indicate host
- **tshark** (Wireshark CLI Tool)
   - `tshark.exe -d tcp.port==21,ftp -w ftp.pcap`
   - **Options**
     - `-i`: interface
     - `-f`: acket filter
     - `-D`: pint interfaces
     - `-L`: pint link layer types
     - `-O [protocol]`: only show specific packets of this protocol
     - `-F`: output file type
     - `-c [packet count]`: stop after n packets
     - `-n`: disable name resolution
     - `-d [layer type]==[selector]`
     - `-r [file]`: read from file.pcap
     - `-w [file]`: write result to file
- **ncat/nc**
   - [https://nmap.org/ncat/guide/index.html](https://nmap.org/ncat/guide/index.html)
   - `nc [options] [host] [port]`: Execute a port scan
   - `nc -l [host] [port]`: Initiate a listener on the given port
   - `nc -4`:  Use IPv4 only
   - `nc -6`: Use IPv6
   - `nc -u`: Use UDP instead of TCP
   - `nc -k -l`: Continue listening after disconnection
   - `nc -n`: Skip DNS lookups / numerical
   - `nc -v`: verbose output 
   - **Create Channel**
     - Kali: `nc -lvnp [Port]` (Check your listening status in another terminal by using command `netstat`)
     - Windows: `nc [IPv4] [Port]` ; `get`
   - **Transfer text** (*while connection is already established*)
     - Windows: `nc -lvnp [port] > example.txt`
     - Kali: enter your text
   - **Transfer files** (*while connection is already established*)
     - Windows: `nc -lnvp [port] > wget.exe`
     - Kali: `nc [IPv4] [port] < /usr/share/windows-binaries/wget.exe`
   - **Portscan**
     - `nc -v -w 2 -z [IPv4] [port range]`
     - Exp: `nc -v -w 2 -z 3.45.21.19 10-1000`
     - w = set timeout in [s]
     - z = no transmission, only check listening services 
   - **Communicate with Web Server**
     - `nc [host] [port]`
     - `GET / HTTP/1.0`
     - Press 2x Enter
- **dnsmasq**
   - **Setup MITM DNS Service** 
   - `nano dnsmasq.conf` -> add `addn-hosts=dnsmasq.hosts`: create configuration file
   - `nano dnsmasq.hosts` -> add `IPv4  mitm.example.com`: add (malicious) hosts
   - `sudo dnsmasq -C dnsmasq.conf --no-daemon`: start dnsmasq in foreground with specified configuration
     - You may face probelms if systemd-resolve occupies port 53 --> [Look here](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#systemd-resolved-vs-dnsmasq)
   - `dig mitm.example.com` and `dig @localhost mitm.example.com`: Verify if dnsmasq works as expected
   - Get your victim to send its DNS query to your server, where dnsmasq is running
   - **Setup MITM TCP Server**
   - `sudo nc -lvnp 80`

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
    - `grep -r -i [exploit_name] /usr/share/exploitdb/exploits/`: check available exploits on Kali
    - `cat rockyou.txt | grep -x '.\{8,96\}'`: only show passwords from rockyou.txt between 8 and 96 chars long
- **cat**: concatenate/read the file and output content
    - `cat -b dictionary.txt`
    - `cat > file.txt << EOF`: enter content of `file` dynamically. To finish your input enter `EOF`
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
- **zip/unzip**:
    - `zip [file]`
    - `unzip [file]`
    - `zip -r foo.zip foo`: zip recursively with output file named foo.zip
    - **Malicious Zip Symlink**
    - `ln -s /etc/passwd symlink.jpg`: create soft link that points to `/etc/passwd`
    - `zip --symlinks pictures.zip symlink.jpg`: create zip file that contains malicious symlink
- **gzip/gunzip/zlib** (GNU zip format)
    - `gzip [file]`
    - `gunzip [file.gz]`
    - `printf "\x1f\x8b\x08\x00\x00\x00\x00\x00"  | cat - [file_with_gzipdata] | gunzip`: If gzip data is deflated (HTTP compression), you need to add Magic Bytes
         - If you capture deflated data via Wireshark: 
         - 1) Follow TCP Stream
         - 2) Save date in RAW format
    - `printf "\x1f\x8b\x08\x00\x00\x00\x00\x00" | cat - [zlib_compressed_data] | gunzip`
    - **Error**: zlib.error: Error -3 while decompressing data: incorrect header check
    - **Solution**: `result = zlib.decompress(base64.b64decode(unquote(DATA).encode()), -zlib.MAX_WBITS)`
    - **Details**: [https://newbedev.com/zlib-error](https://newbedev.com/zlib-error-error-3-while-decompressing-incorrect-header-check)
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
    - `ESC`: exit insert Mode and return to normal mode
    - `y/y^/y$`: copy
    - `d/d$/D`: delete
    - `p`: paste
    - `:q!`: quit without saving
    - `:wq`: write and quit
    - `:wq!`: write, quit and override
    - `:%s /\\n/\r/g`: search `\n` and replace with newline globally
    - `:%s /.\{64}/&\r/g`: replace globally each 64th char with `\r` (carriage return), e.g. to get correct PEM format
    - [Spawn shell inside vim](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Wiki/Restricted%20Shell%20Escape.md)
    - 
- **tee**: read from standard input and write to standard output and files
- **sed**: Stream Editor, useful with regex
    - `cat [file] | sed /regex-pattern/action`
    - action: d(elete), s(ubstitute), -n p(rint)
    - `cat /etc/passwd | sed '1,5s/sh/quiet/g'`
    - `cat /etc/passwd | sed -n '1,3p'`: print line 1 to 3
    - `cat testing | sed '/^daemon/d'`: matches all the lines starting with daemon and then deletes them 
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
- **seq**
    - `seq 0 10`: output decimal from 0 to 10
    - `for i in 'seq 0 100'; do printf "%02x\n" $i; done`: output numbers in hex-format (01 02...0c 0d...4a 4b...) 
    -  `for i in 'seq 0 100'; do printf "0x%02x.a.example.com\n" $i; done`:
- **deboprhan**: find unused packages
    - `deborphan -zP`: show unused packages with -z=size and -P=priority
    - `sudo orphaner`: remove the unused packages
- **fdisk**:
   - `sudo fdisk -l`: list all devices
   - `mkfs.fat /dev/sdb1`: format sdb1 (e.g. USB stick)
- **javac**
   - `javac myClass.java`: compile Java file; output is `myClass.class`
   - `java myClass.class`: run the Java bytecode
- **jar**:
   - `jar --create --file classes.jar Foo.class Bar.class`
   - `jar --create --file my.jar @classes.list` 
- **gcc**: GNU Compiler Collection
   - example.c --> program code in C
   - example.s --> interim data with assembler code
   - example.o --> object File
   - example --> compiled binary
   - Options (extract):
      - `-Wall` = Warning all (Syntax/Logikfehler)
      - `-o` = output
      - `-g` = generate debug info
      - `-g0` = no debug info
      - `-g1` = minimal debug info
      - `-g` = default debug info
      - `-g3` = maximal debug info
      - `-01` to `-03` = Code optimization (the more, the more compact)
      - `-save-temps` = no deletion of temporary data while compilation
      - `-m32` = compile 32bit binary on 64bit machine
   - `gcc -Wall example.c -o example`
   - `gcc -shared -o attack.so -fPIC attack.c`:
      - create **shared object / .so** file
      - For predictable results, you must also specify `-fPIC` when you specify this linker option

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
   - **Verify PGP signature of downloaded .apk**:
   - `keytool -printcert -jarfile file.apk`: Reveal some information about the certificate
   - `gpg --keyserver pgp.mit.edu --receive-keys [fingerprint or key ID]`: Use previously retrieved fingerprint/keyID
   - `gpg --verify file.apk.asc`: while being in the same directory where the file.apk resides
   - **Verify PGP signature of downloaded .asc** (example veracrypt):
   - `wget https://www.idrix.fr/VeraCrypt/VeraCrypt_PGP_public_key.asc`
   - `gpg --show-keys VeraCrypt_PGP_public_key.asc`: compare retrieved fingerprint with the public one from download page
   - `gpg --import VeraCrypt_PGP_public_key.asc`: If erverything seems OK, import the public key
   - `gpg --verify xxx.deb.sig xxx.deb`: check the signature
- **cryptsetup**
   - `sudo cryptsetup luksFormat -c aes-xts-plain64 -s 512 -h sha512 -y /dev/sba`: create encrypted partition. You will be asked for a password
   - `cryptsetup luksAddKey --key-slot=2 /dev/sdb1`: A single encrypted partition can have eight different keys. This command adds one key on slot 2
   - `cryptsetup luksChangeKey /dev/sdb1`: change passphrase
   - `cryptsetup luksDump /dev/sba1`: LUKS header information
   - `sudo cryptsetup-reencrypt --decrypt /dev/sdb1`
- **lvm**
   - `sudo vgdisplay`: show volume group info 
   - `sudo pvs`: show info of physical volumes
   - `sudo vgs`: show info of volume groups
   - `sudo lvs`: show info of logical volumes
   - How to shrink size of encrypted root partition:
      - Backup your data for safety sake
      - Boot from Live CD / Live USB
      - `sudo vgs` or `sudo vgdisplay` or `sudo vgscan`: To identify the existing volume group with /root inside
      - If your VG is encrypted you need to decrypt it first via GUI (open file system)
      - /root must be **unmounted** before resizing !
      - `sudo e2fsck -f /dev/mapper/yourVG/yourLV`: Make sure no errors are reported during file system check
      - `sudo resize2fs -p /dev/mapper/yourVG/yourLV 100G`: Resize the file system to 100G. Replace 100G with your desired size for /root
      - `sudo lvreduce -L 100G /dev/mapper/yourVG/yourLV`: Resize the logical volume to same size as file system !
      - `reboot`: To make your change effective
      - If you want to allocate the new free space to another (new) logical volume (e.g. home, tmp, var....) then proceed as below
      - `sudo lvcreate -L SIZE -n yourNewLV yourVG`: create new logical volume with size SIZE
      - `sudo mkfs.ext4 /dev/mapper/yourVF/yourLV`: format the file system on your new logical volume e.g. to ext4
      - `sudo mount /dev/mapper/yourVG/yourNewLV /mnt`: this is temporarily 
      -  Next steps are shown with `/home`
      - `sudo cp -rp /home/* /mnt`: copy everything from `/home` -recursively and -preserve (ownerships/timestamps) to new LV on `/mnt`
      - `sudo mv /home /home.orig`: make a backup for safety sake
      - `sudo mkdir /home`: create new empty `/home`
      - `sudo umount /mnt`
      - `sudo mount /dev/mapper/yourVG/yourNewLV /home`
      - `echo '/dev/mapper/yourVG/yourNewLV /home ext4 defaults 0 0' | sudo tee -a /etc/fstab`: make it permanent
      - `sudo update-grub`
   - `sudo lvextend -L 4G /dev/mapper/yourVG/yourLV`: extend your LV to new size 4Gb 
   - `sudo lvrename VG oldLVName newLVName`: change LV name. Please mind to update `/etc/fstab` and `sudo update-grub` afterwards
- **fail2ban**:
   - rate limiting to mitigate brute force attacks
   - `git clone https://github.com/fail2ban/fail2ban.git`
   - `cd fail2ban`
   - `sudo python setup.py install`
   - Details: [https://kalilinuxtutorials.com/fail2ban/](https://kalilinuxtutorials.com/fail2ban/)
 - **uudecode**:
   - `uudecode [uudecoded_file]`
- **base64**:
   - `base64 -d`: decode base64
   - `base64 -w 0`: avoid newlines while doing encoding 

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
    - `chmod o+w [file name]`: allow others to write
    - `chmod g-w [file name]`: disallow group to write
    - `chmod 750 [file name]`: -rwx r-x ---
    - `chmod 777 .`: allow all to everyone in current directory
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
    - **Restrict [command] for any non-root Linux user**:
    - `which [command]`: verify the command path, e.g. /bin/su
    - `sudo chmod o-x [command]`: disallow execution for others
    - Alternatively: `rbash`
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
    - [See here](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#apt-package-tool) 
- **shutdown**
    - `shutdown -h now`: Instant shutdown
    - `shutdown -r now`: reboot
- **reboot**
- **Read-in CD**
    - `apt-cdrom add /media/cdrom`
- **service**: runs  a System V init script located in /etc/init.d/SCRIPT, or the name of a systemd unit
    - `service [program] restart`: restart service (after config change)
    - `service [program] status`: show status 
    - `service --status-all`: query the status of all services
- **systemctl**:
    - `systemctl status [program]` 
    - `systemctl start [program]` 
    - `systemctl stop [program]` 
    - `systemctl restart [program]` 
    - `systemctl --type service`: show all services
    - `systemctl --version`  
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
- **dd** (disk duplicate):
    - `sudo dd bs=4M if=/Downloads/file.iso of=/dev/sdb1 status=progress && sync`: make ISO on sdb1 (e.g. USB stick)
- **ps**: display information of active processes
    - VSZ (Virtual MemSize) / RSS (Physical MemSize) / TTY (?=none) / STAT (S=sleeping,R=running)
    - `ps -fp [pid]`: show corresponding CLI command 
    - `ps axu | grep [pid/program]`
    - `ps aux --sort=-%mem | less`
- **dmidecode**: displays the S(ystem)M(anagement)BIOS/DMI in a human-readable way
- **export**: show environment variables 
    - `export PS1='$ '` set PS1 to '$ '
    - **Add file remporarily to PATH**:
    - `export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64`
    - `echo $JAVA_HOME`: verify
    - `export PATH=$PATH:$JAVA_HOME/bin`
    - `echo $PATH`: verify
    - **Add file permanently**:
    - `nano ~/.profile` or `nano ~/.bashrc`
    - `export PATH="$PATH:/snap/bin"`: add this line at the end of bashrc (replace /snap/bin with your app)
    - `source ~/.profile` or `source ~/.bashrc`: activate the change for current shell
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
    - Syntax:
      - Minute (0-59)
      - Hours (0-23)
      - Days (1-31)
      - Months (1-12)
      - Weekdays (1-7) 
    - `* * * * * /usr/bin/echo.sh >> /dev/pts/0`: redirect output from echo.sh
    - `*/2 * * * * command`: execute command every two minutes
    - `0 10 * * * command`: execute command every day 10 AM
    - `cron -L [NUMBER]`: Specify loglevel by [NUMBER]; e.g. 1 will log the start of all cron jobs; 2 will log the end of all cron jobs
- **crontab**: 
    - `crontab -l`: display cron jobs
    - `crontab -u root -l`: open crontap as root
    - `grep -r [cronjob] /etc/cron.* /etc/crontab`
    - Add cron job:
      -  `sudo nano /etc/crontab`
      -  Add your command: `* * * * * [USER] [COMMAND]`
      -  Example: `0 10 * * * user ~/dir/script.sh` --> Everyday at 10AM perform script.sh with user privilege
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
    - Setup your config file:
       - `nano ~/.tmux.conf`
       - `set-option -g status-style bg=blue`
       - `set-option -g base-index 1`: Set the base index for windows to 1 instead of 0
       - `set-option -g mouse on`: activate mouse scrolling (attention: mark/copy text with `Shift+Click`)
       - `bind r source-file ~/.tmux.conf \; display "Reloaded!"`: Set bind key to reload configuration file
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
    - `sudo update-grub`: same as `grub-mkconfig -o /boot/grub/grub.cfg`
- **lsblk**
    - `lsblk -o PATH, UUID`: show dev path and UUID  
- **last**
    - `last -x reboot`: show last reboots
    - `last -x shutdown`: show last shutdowns 
-**parted**:
    - `sudo parted -l` or `sudo parted /dev/sdb`
    - `(parted) mklabel [partition_table_type]`: make partition table (choose between aix, amiga, bsd, dvh, **gpt**, mac, **ms-dos**, pc98, sun, and loop)
    - `(parted) print`: show info within parted prompt
    - `mkpart primary ext4 1MB 1000GB`: create new partition with ext4 filesystem and 1000GB size
    - `(parted) quit`: quit and save
- **kvm**: Linux-based systems support VM acceleration through the KVM software package
   - `sudo apt install cpu-checker`: has to be installed firstly
   - `kvm-ok`: Expected output: INFO: /dev/kvm exists; KVM acceleration can be used
   - `sudo apt-get install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils`: install KVM on Linux
- **unattended-upgrades**
   - automatic installation of security (and other) upgrades
   - `dpkg-reconfigure --priority=low unattended-upgrades`: reconfigure "unattended-upgrades" to run not only for security but also stable updates
- **umask**
   - Set default permission for files/directories at creation time
   - `(full permissions for directory) – (umask value) = permission`: This means `umask 0543` results in -> 777 – 543 = 234 = `-w- r-x r--`
   - `(full permissions for file) – (umask value) = permission`: This means `umask 0027` results in -> 666 – 027 = 630 =  `rw- r-- ---`
   - Default: `umask 0002`
   - Hardening: `umask 0027`

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
- **sqlite3**:
    - `sqlite3 [file]`: connect to databse [file]
    - `.tables`: get a list of tables
    - `SELECT * FROM [table];`: extract the content of a table using SQL
    - `.exit`: exit 
- **docker**:
    - `docker run -d -p 80:80 docker/getting-started`: 
      - `-d` = detached
      - `-p 80:80` = map host port to container port
    - `docker run -it ubuntu bash`: start ubuntu
      -  `-it` = interactive pseudo-TTY with colored output`
    - `docker run -it -v $(pwd):/app ruby /bin/bash` 
    - `docker container ls`: list containers (running instance of an image)
    - `docker images`: show images
    - `docker stats`: show stats
    - `docker rm containerID`
    - `docker rmi imageID`
    - `docker build -t mycontainer:tag .`: Build **Dockerfile** which is located at `.`
    - `docker inspect [networkName]`: show IP address network details of container's network
    - `docker network prune`: remove existing container network
      - `-t`= provide name:tag to your container
    - `docker-compose build`: build multi-container app while being inside the repo
    - `docker-compose up -d`: start all containers in background
    - `docker-compose up`: After every change of **docker-compose.yml**
    - `docker-compose ps`: show running process
    - `docker-compose run [servicename] env`: show environment variables of service
    - `docker-compose start/stop`: start/stop container
    - **Troubleshooting**
    - `docker build ERROR: unable to select packages:   python (no such package)`
      - Open dockerfile and change from `python` to `python3` or `python3-dev`
      - If any other packages is causing errors, then look at alpine's package index yourself
      - [https://pkgs.alpinelinux.org/packages](https://pkgs.alpinelinux.org/packages)
      - [https://dl-cdn.alpinelinux.org/alpine/](https://dl-cdn.alpinelinux.org/alpine/)
    - `docker-compose build ERROR: Named volume is used in service but no declaration was found in the volumes section`
      - In docker-compose.yml look at `Services:` and `Volumes:`
      - The listed values have to match
      - If you are mapping then consider the right syntax with `./` in the beginning: `"./server:/home/node/app/server"`
- **aws**:
    - `aws configure`: setup your aws cli (enter keyID and secret key); data will be stored in `~/.aws`
    - `aws s3 ls s3://assets.example.com`: show data in s3 bucket of given website 
    - `aws s3 cp s3://assets.example.com/key.txt key.txt`: cp data from s3 bucket of given website
- **bandit**:
    - `virtualenv venv`, then `python3 -m venv venv`
    - `source venv/bin/activate`
    - `pip install wheel; pip install bandit`
    - `bandit PATH-TO-FILE -o RESULT-FILE-NAME.txt -f file`: usage pattern
 

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

# TROUBLESHOOTING
1. [FROZEN XFCE4 WINDOW MANAGER](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#frozen-xfce4-window-manager)
2. [DESKTOP ICONS DISAPPEARED (KALI)](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#frozen-xfce4-window-manager)
3. [DEBIAN VIRTUALBOX DRIVER](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#debian-virtualbox-driver)
4. [HOW TO ENABLE AltGr (KALI](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#frozen-xfce4-window-manager)
5. [BUNDLER ERROR)](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#bundler-error)
6. [SERVICE org.freedesktop.PolicyKit1 TIMED OUT](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#service-org.freedesktop.PolicyKit1-timed-out)
7. [WI-FI HARDWARE SWITCH](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#wi-fi-hardware-switch)
8. [SYSTEMD-RESOLVED VS DNSMASQ](https://github.com/p-arrow/Red-Blue-Guide/blob/main/OperatingSystem/Linux.md#systemd-resolved-vs-dnsmasq)


### FROZEN XFCE4 WINDOW MANAGER
- Open Terminal `Ctrl+Alt+T`
- `pidof xfce4-panel`
- `kill [pid]` or `killall xfce4-panel`
- `xfce4-panel &`
- `disown`: move xfce4 process out of terminal

### DESKTOP ICONS DISAPPEARED (KALI)
- Open Terminal `Crtl+Shift+T` and enter `xfwm4`: it restarts your window manager
- `xfsettingsd --replace`: make it persistent by replacing the xfce4 deamon

### DEBIAN VIRTUALBOX DRIVERS
- [https://wiki.debian.org/SecureBoot#MOK_-_Machine_Owner_Key](https://wiki.debian.org/SecureBoot#MOK_-_Machine_Owner_Key)
- `sudo mokutil --sb-state`: check SecureBoot enabled
- `ls /var/lib/shim-signed/mok/`: check if key exists
- `sudo mkdir -p /var/lib/shim-signed/mok/`
- `cd /var/lib/shim-signed/mok/`
- `sudo openssl req -new -x509 -newkey rsa:2048 -keyout MOK.priv -outform DER -out MOK.der -days 36500 -subj "/CN=YOURNAME/" -nodes`
- `sudo openssl x509 -inform der -in MOK.der -out MOK.pem`
- `sudo mokutil --import MOK.der`: prompts for one-time password
- `sudo mokutil --list-new`: recheck your key will be prompted on next boot
- reboot your machine
- Enter MOK manager: enroll MOK, continue, confirm, enter password, reboot
- `sudo dmesg | grep cert` verify your key is loaded
- `MODULE_DIR=/lib/modules/$(uname -r)/misc`: location of Oracle's module packages
- `cd $MODULE_DIR`
- `for i in *.ko ; do /usr/lib/linux-kbuild-5.10/scripts/sign-file sha256 /var/lib/shim-signed/mok/MOK.priv /var/lib/shim-signed/mok/MOK.der "$i" ; done`
- `modinfo vboxdrv`
- reboot

### HOW TO ENABLE AltGr (KALI)
- `cd ~` 
- `xev`: Then press `AltGr` and check the output (keycode + designation)
   - Example: `keycode 113 + Alt_R` (correct should be "Mode_switch")
- `nano .Xmodmap`
- Enter `"keycode 113 = Mode_switch"` and save
- `xmodmap ~/.Xmodmap`: Gnome will update the environment automatically

### BUNDLER ERROR
- **METASPLOITFRAMEWORK/MSF**
- Error Message: `cannot load such file -- bundler/setup`
- `cd /usr/share/metasploit-framework`
- Check current versions
   - `ruby -v`
   - `bundler -v`
   - `gem list bundler`
   - `cat /usr/share/metasploit-framework/gemfile.lock`: Look at line with "BUNDLED WITH" mentioned
- Remove non-matching bundler and install matching bundler
   - `gem install bundler -v [...]`
   - `bundle install`
   - `gem update --system`: cross check with `gem environment`

### SERVICE ‘org.freedesktop.PolicyKit1’ TIMED OUT 
- Check existency of polkitd user:
   - `getent passwd polkitd`
   - `getent group polkitd`
- If not available:
   - `groupadd -r polkitd`: -r = system account
   - `useradd -r -g polkitd -d / -s /sbin/nologin -c "User for polkitd" polkitd`
- Reset permissions and user/group ownership for all files provided by polkit and polkit-pkla-compat
   - `rpm -Va polkit\*`: -Va = verify all
   - `rpm --setugids polkit polkit-pkla-compat; rpm --setperms polkit polkit-pkla-compat`
- Reboot: `shutdown -h now`

### WI-FI HARDWARE SWITCH
- **Wifi is disabled by hardware switch**
- `rfkill list`: check which interfaces are blocked
- example:
```
0: tpacpi_bluetooth_sw: Bluetooth
	Soft blocked: no
	Hard blocked: no
2: phy0: Wireless LAN
	Soft blocked: yes
	Hard blocked: yes
3: hci0: Bluetooth
	Soft blocked: no
	Hard blocked: no
```
- `sudo rfkill unblock INTERFACE` or `sudo rfkill unblock all`: soft-unblock your device
- `sudo /etc/init.d/networking restart`
- **Solution**: Unplug the LAN cable, if any

### SYSTEMD-RESOLVED VS DNSMASQ
- **dnsmasq: failed to create listening socket for port 53: Address already in use**
- `systemd-resolve --status`: check the current DNS Server and Link
- ![image](https://user-images.githubusercontent.com/84674087/159803127-d0a1205f-65e5-4e7e-9ad1-5ecbb260d957.png)
- `nano /etc/dnsmasq.conf`: 
   - Add the line `server=DNS SERVER`, whereby DNS SERVER is the one indicated from `systemd-resolve --status`
   - Add the line `bind-interfaces`
- `sudo systemd-resolve --set-dns=127.0.0.1 --interface=eth0`: Add dnsmasq as DNS Server to systemd-resolve
- `sudo systemctl restart systemd-resolved`
- `sudo dnsmasq -C dnsmasq.conf --no-daemon`: start dnsmasq in foreground (`--no-daemon`)
- Verify: `dig google.com` (systemd-resolver) and `dig @localhost google.com` (dnsmasq) should yield the same result
- Credits: [Here](https://blog.down-time.io/linux/2020/02/06/systemd-resolve-dnsmasq) and [Here](https://unix.stackexchange.com/questions/304050/how-to-avoid-conflicts-between-dnsmasq-and-systemd-resolved)
