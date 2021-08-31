## Readme

A framework that performs automatic reconnaissance for you!

**How To** (Example cisco.com)
- workspaces create cisco.com 
- marketplace info [module] / marketplace install [module]
- modules load [module]: info / options set [Name]
- db insert domains cisco.com

**Example Modules**
1. run google_site_web
    - show hosts
2. run recon/hosts-hosts/resolve (resolve IPv4 hosts)
3. keys add ipinfodb <API key> ; modules load recon/hosts-hosts/ipinfodb
    - check IP location of target
    - register yourself to receive API keys
4. Module pocs: investigate Email addresses
5. Module reporting/html: create report
