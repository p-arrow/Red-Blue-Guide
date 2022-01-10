*Tool for Linux Auditing System: https://www.man7.org/linux/man-pages/man7/audit.rules.7.html*

# RedTeam

...

# BlueTeam


## Features 
- ausearch / aureport: Viewing logs
- auditctl: Configuring audit system / loading rules
   - Results: `/var/log/audit/audit.log`
   - Check Rules: `sudo auditctl -l`
   - Report Status: `sudo auditctl -s`
- During Startup: `/etc/audit/audit.rules` is read by auditctl and loaded into kernel at startup

## Installation
```
sudo apt install auditd
sudo service auditd start
sudo service auditd status
systemctl is-enabled auditd
```


## Audit.rules (control, file, syscall)
1. Control: These rules are at top of rules file for config purpose
2. File: To audit files
   - w: path-to-file
   - k: keyname
   - p: permissions
      - r: read file
      - w: write file
      - x: execute file
      - a: change in file's attribute 
3. Syscall: The more rules, the bigger the performance drop (!)
   - Matching Filter Lists: task, exit user, exclude
   - `-a` = action,list (valid actions: always/never)
   - `-S` = syscall
   - `-F` = field (=value)
   - `-k` = keyname

## Example: audit.rules
```
auditctl -w /etc/sudoers -p wa -k change_in_sudoers
auditctl -w /etc/shadow -p wa -k change_in_shadow
```

## Example: ausearch
```
ausearch --start this-week -k access --raw | aureport --file --summary
ausearch --start this-week -k access --raw | aureport --user --summary
```
