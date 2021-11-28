# Blue Team

<br />

## Common Jail
1. Define the Environment
```
mkdir /home/jailrestricted
cd /home/jailrestricted
mkdir -p bin lib64/x86_64-linux-gnu lib/x86_64-linux-gnu
```
2. Configure the Jail Options
```
cp $(which ls) ./bin/
cp $(which bash) ./bin/
ldd $(which bash)
cp /lib/x86_64-linux-gnu/libtinfo.so.5 lib/x86_64-linux-gnu/
cp /lib/x86_64-linux-gnu/libdl.so.2 lib/x86_64-linux-gnu/
cp /lib/x86_64-linux-gnu/libc.so.6 lib/x86_64-linux-gnu/
cp /lib64/ld-linux-x86-64.so.2 lib64/

# double check with "tree" command
```

3. Initialize the Service
- `sudo chroot jailrestricted/ bin/bash`

<br />

## SFTP Chroot Jail
1. Create specific User/Group for SFTP Usage
```
useradd -s /bin/false -g sftpgroup -m -d /home/sftpuser sftpuser
```

2. Home Directory of user to be owned by root 755
```
chown root:root /home/sftpuser
```

3. Create directories inside user home directory
```
mkdir /home/sftpuser/{download,upload} 
chown sftpuser:sftpgroup /home/sftpuser/{download,upload} 
chmod 755 /home/sftpuser/{download,upload}
```

4. Change the /etc/ssh/sshd_config file
```
Subsystem sftp internal-sftp
Match Group sftpgroup
ChrootDirectory %h (%h = home directory)
ForceCommand internal-sftp
AllowTcpForwarding no
X11Forwarding no
```

5. Restart SSH
```
service ssh restart
```

6. Verify the setting
```
sftp sftpuser@localhost
```
