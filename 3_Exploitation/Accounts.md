# RedTeam

... 

# BlueTeam

## Hardening Guest Accounts (Linux)

- CLI: `sudo /usr/lib/lightdm/lightdm-set-defaults -l false`
- Modify Config
   - `nano /etc/lightdm/lightdm.conf`
   - `add "allow-guest=false"`
- Check inactive Users: `grep -E ^[^:]+:[^\!*] /etc/shadow | cut -d: -f1,7`

## Hardening /etc/sudoers

#### Relevant Lines in /etc/sudoers
```
User: root ALL=(ALL:ALL) ALL
Group: %admin ALL=(ALL) ALL
Group: %sudo ALL=(ALL:ALL) ALL
```

**Meaning**: all hosts involved = (all users: all group members) all commands allowed

#### Example: Restriction Control

- `%admin ALL=(ALL) ALL; !/sbin/reboot`
   - allows admin user all except reboot operation 

#### Best Practice
1. Regularly Monitoring for User Accounts and Access Levels
2. Eliminating Shared Account Usage
3. Manage and Record Privileged Activity
