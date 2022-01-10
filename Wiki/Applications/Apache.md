# RedTeam

empty

# BlueTeam

## General Step

1. Step: nano etc/apache2/apache.conf (Debian/Ubuntu)
2. Step: sudo service apache2 restart

## 1) Server Signature Minimization

- ServerTokens Prod = only display the web server type
- ServerSignature Off = remove the version information

**Create own Server Signature**
- sudo apt install libapache2-mod-security2
- sudo service apache2 restart
- ServerTokens Full
- SecServerSignature "Bare Metal" 

## 2) Directory Listing Deactivation

```
< Directory /var/www/html >
Options -Indexes
Order allow, deny
Allow from all
< /Directory >
```

## 3) Limited User Account for Webserver

```
sudo groupadd apache-group
sudo useradd -d /var/www/html -g apache-group -s /bin/nologin apache-user 
sudo chown -R apache-user /var/www/html/*
sudo chgrp -R apache-group /var/www/html/*
sudo chown -R apache-user /var/lock/apache2
sudo chgrp -R apache-group /var/lock/apache2
sudo chown -R apache-user /var/log/apache2
sudo chgrp -R apache-group /var/log/apache2
sudo chown -R kali:kali /var/www/html
sudo chown -R kali:kali /var/www/html/ossec
```

- `nano /etc/apache2/envvars`

```
export APACHE_RUN_USER=apache-user
export APACHE_RUN_GROUP=apache-group
```

- Now you can monitor logon activities


## 4) Chroot

- Allows restricted directoy access (only /var/www/html)
- This leads to sandbox behavior and complicates lateral movement

## 5) Deactive unnecessary modules

- Verify exiting modules:
   - `apachectl -M`
   - `httpd -l`

## 6) Restrict HTTP Methods

```
< LimitExcept GET POST HEAD >
deny from all
< / LimitExcept >
```

## 7) Restrict Implementation of external content

```
# Datei php.ini
allow_url_fopen Off
allow_url_include Off
```

## 8) Set Cookies
- HttpOnly Attribute
- Secure Attribute

## 9) Server Timeout

- Slow Loris Attacke: 
   - Causes several pending HTTP Requests upon web server
   - This blocks threads for other meaningful processes 
```
#Datei httpd.conf
Timeout 30 (i/o Standard 300)
```
