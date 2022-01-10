*Check out: [https://github.com/ossec/ossec-hids](https://github.com/ossec/ossec-hids)*

## How To
1. `cd /tmp`
2. `wget https://github.com/ossec/ossec-hids/archive/3.6.0.tar.gz`
3. `tar -xzf 3.6.0.tar.gz`
4. `cd ossec-hids`
5. `./install.sh` (followed by install wizard)
6. `git clone https://github.com/ossec/ossec-wui.git`
7. `mv ossec-wui* /var/www/html/ossec-wui`
8. `cd /var/www/html/ossec-wui`
9. `./setup.sh` (enter user and pw by your choice)
10. `service apache2 restart`
- Use `/var/ossec/bin/ossec-control start/stop` to start or stop the service
- Open your browser and enter `localhost/ossec`
