# TABLE OF CONTENTS
1) [APT PACKAGE TOOL](https://github.com/p-arrow/Red-Blue-Guide/tree/main/OperatingSystem/Linux.md#apt-package-tool)


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
dpkg --listfiles package (or -L)
dpkg --search file (or -S)
dpkg --list (or -l)
dpkg --contents file.deb (or -c)
dpkg --info file.deb (or -I)
dpkg --verify (display modified system files)
```
