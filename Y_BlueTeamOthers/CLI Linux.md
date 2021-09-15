## Basics

- `[command1] && [command2]`: command2 gets executed when command1 finished successfully 
- `Alt + print-key`: Screenshot
- `Alt + "+"`: zoom in 
- `pwd`: print working directory
- `pwdx [pid]`: print workig directory of process pid  
- `echo`: print function
- `man [command]`: show manual
   - `/` = search within manual
   - jump through search result: `N` (forward)/`Shift+N` (backward)
- `ls`: show content of directory 
    - `ls -a` ("all")
    - `ls -l` ("long", more detailed)
- `cd`: change directory
    - `cd ..` (parent directory)
    - `cd ~` (Home directory)
    - `cd /` (root directory)
- `Strg + C`: abort process
- `exit`: finish terminal
- `mkfifo [Option] [Name]`: create named pipe (e.g. from terminal1 to terminal2)
- `date`: show date and time 
   - datum = $(date +%d.%m.%Y)
   - touch $(date +`hostname`-%d-%m-%y-%H%M.log)
- `cal`: calendar
- `java -version`: check openJDK version
- `python --version`: check python version
- `[command] &`: perform [command] in background 

## Configuration

- `nano ~/.bashrc`: configure bash profile
- `$PS1`: (Primary) Prompt Shell Variable
   - Exp: PS1="[\u@\h \w]$"
- `$RANDOM`: Generates random integer between 0 and 32,767 each time it is referenced
   - `echo $(($RANDOM % 100))`: random number between 0 and 99
- `$PATH`: Indicates the search path for commands
- `$LANG`: Display Language
- `chsh`: change shell
   - (1) `cat /etc/shells` (check existing shells) 2) `chsh -s $(which zsh)` (switch shell)
   - `chsh -s /bin/rbash [username]` (apply restricted shell to user)
- `timedatectl`: show time settings 
   - `timedatectl list-timezones`
   - `timedatectl set-timezone`
   - `timedatectl set-local-RTC 0`
- `DEBIAN_FRONTEND`: environment variable for adjusting debconf (Debian package configuration system)
   - `DEBIAN_FRONTEND=noninteractive apt-get -y update`
   - `DEBIAN_FRONTEND=noninteractive apt-get -y upgrade`
   - `DEBIAN_FRONTEND=dialog` (default frontend for apt/apt-get )
   - `DEBIAN_FRONTEND=readline` (most traditional; for slow remote connections; entirely CLI)

## Network

- `ifconfig`: show interface details
- `ip`:
   - `ip addr show`
   - `ip addr sh eth0`
   - `ip -br link show` (br=brief)
- `netstat`: print network connections
   - `netstat -tulpn`
- `ping [IPv4]`
- `host [IPv4]`: Identify host
- openssl:
   - `openssl [command] -help`
   - `openssl s_client -connect host:port`
- scp (OpenSSH secure file copy):
   - `scp option source user@host:/tmp`
- fuser: find out process that opened specific port
   - `fuser 22/tcp`: SSH pid will be shown
- ufw (uncomplicated FW): managing netfilter FW
   - `ufw status`: show FW status
- ipv6toolkit:
   - `sudo scan6 -i [interface] -L -P local --print-unique -e`: get IPv6 + MAC
- traceroute: UDP probe by default (often ignored by FW though)
   - `traceroute -I example.com` (-I = send ICMP probe)
   - `traceroute -w 10 example.com` (-w = wait for response in seconds)
- iperf: check bandwidth between two \*nix machines
- nmblookup: netBIOS enumeration
   - `nmblookup -A [IPv4]`
