**>> General Information: [Z_Networks/Web Application](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Z_Networks/Web%20Application.md)**

**>> Check out: [3_Exploitation/Web Application](https://github.com/p-arrow/Red-Blue-Guide/blob/main/3_Exploitation/Web%20Application.md)**

## Methodology 

> Below guide is inpired by [Carlospolop](https://github.com/carlospolop/hacktricks/tree/master/pentesting)

> Aim to apply this methodology to each discovered domain, subdomain or IP with undetermined web server inside the scope

<br />

- Start by preparing a "notebook" to keep track of all your findings (to not forget any findings and keeping an overview!)
   - [Cherrytree](https://github.com/giuspen/cherrytree)
   - [Mind Map](https://www.xmind.net/)
   - [Maltego](https://www.maltego.com/)
   - Simple Notepad
   - Excel
   - etc. 
- Identifying the **technologies** used by the web server
   - Check out main page with different extensions: home.html / home.asp / home.aspx / home.php
- Any **known vulnerability** of the version of the technology?
- Any **well known tech**?
- Any **useful trick** to extract more information?
   - Check out metadata of pictures with exiftool
- Any **specialized scanner** to run like wpscan?
- Any **general purpose scanner** to run? 
- Initial checks:
   - robots (www.example.com/robots.txt): allow/disallow search of web crawlers
   - sitemap
   - 404 error
   - SSL/TLS scan (if HTTPS)
- **Spider the web page** in order to find all possible files, folders and parameters being used
   - Anytime a new directory is discovered, it should be spidered
- **Directory Brute-Forcing**: Try to brute force all the discovered folders searching for new file and directories 
   - Anytime a new directory is discovered, it should be brute forced
- **Parameter Brute-Forcing**: Try to find hidden parameters
- Look out for backups of discovered files appending common backup extensions

**>> Once you have identified all the possible endpoints accepting user input, check for all kind of vulnerabilities related to it!**

<br />

## Tools

#### curl
```
curl example.com
curl --head example.com
curl -X GET example.com 
curl -X DELETE example.com/include/config.db
curl -X OPTIONS example.com --head (show available HTTP Methods)
curl -T file example.com 
curl -O example.com/file 
curl -u username:password http://
```
- `-X` = --request
- `-T` = upload file
- `-O` = write output to file named like remote file
- `-u` = --user

#### dirb: Web Content Scanner
- old and slow!
- `dirb http://example.com/`

#### dirbuster
- ...

#### dig
```
dig @server example.com [DNS record type]
dig example.com mx
dig axfr @NS example.com (Exp: @NS = @ns1112.ui-dns.org)
dig axfr @nsztm1.digi.ninja zonetransfer.me (for educational purpose)
```

*Checkout: [Z_Networks/DNS](https://github.com/p-arrow/Red-Blue-Guide/blob/main/Z_Networks/DNS.md)*

#### ffuf
- fast fuzzing U fool
- `ffuf -c -w /usr/share/wordlists/dirb/big.txt -u http://10.10.10.10/FUZZ`

#### gobuster
```
- gobuster dir -u http://192.168.0.155/ -w /usr/share/wordlists/dirb/common.txt
- gobuster -m dns -t 100 -u google.com -w /usr/share/wordlists/metasploit/namelist.txt
```
- t = number of concurrent threads
- m = method
- q = quit
- o = output


#### nikto
- `nikto -host example.com`

#### whatweb
- ...

#### wpscan
```
wpscan –url http://example.com –enumerate u (users)
wpscan --usernames 'wpusers' --passwords 'pass' --url http://sbva.local/blog/
```

#### red_hawk
- All in one web scan tool
- `git clone https://github.com/Tuhinshubhra/RED_HAWK.git`

<br />

## WebApplication Features

### 1) Cache-Control
- **no-cache**:
   - It does not prevent data being cached locally
   - Forces validation of the cached content
   - Browser must check for new versions when the page is requested again
- **private**:
   - private does not prevent any caching by web browsers
- **no-store**
   - strongest and preferred directive for secure applications
   - no-store instructs browsers not to store the content locally
- **Pragma**: Serves for backwards compatibility with the HTTP/1.0 caches that do not have a Cache-Control HTTP/1.1 header [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Pragma)
- View cache on Firefox: `about:cache`
