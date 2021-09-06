# RedTeam

...

# BlueTeam

## Get Started
- `sudo apt install apparmor-utils`: Create and manage aa-profiles
- `sudo aa-autodep [program]`: Create standard profile for [program]
- `sudo aa-complain [program]`: Enable Complain Mode
- `sudo aa-logprof [program]`: Check logs after several normal interaction with the app

**> /etc/apparmor.d: location of aa-profiles**

## Preparation
- `sudo apt install apparmor-profiles`: Install pre-loaded aa-profiles
- `sudo apparmor_status`: status check of profiles
- `sudo /etc/init.d/apparmor stop`: Clear AA profile cache (debugging purpose)
- `sudo /etc/init.d/apparmor teardown`: Unload AA profiles (debugging purpose)


## Modify the profile
- read (r) / write (w) / execute (x) / lock (k)
- path entries: determine access/deny
- capability entries: determine privilege
- network entries: determine connection type

## Best Practice
1. Create a new blank profile for the app
2. Put it into complain mode
3. Take normal actions with app; entries get added to logs
4. Run AppArmor utility to go through the logs
5. Approve or disapprove various application actions
6. Switch from complain to enforce mode 

## Troubleshooting
- If enforce mode causes errors, then check:
   - The error text
   - var/log/syslog
   - /var/log/nginx/error.log
