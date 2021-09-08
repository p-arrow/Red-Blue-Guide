## Example: Search filters
- country:DE
- city:stuttgart
- hostname:siemens
- net:88.287.456.34
- net:88.287.456.0/24
- netgear port:23
- os:windows
- title: wireless

## Example: CLI Commands
```
shodan myip
shodan host [IPv4]
shodan count microsoft iis 6.0
shodan download new-microsoft-data microsoft iis 6.0
shodan search --limit 10 --fields ip_str,port,org,hostnames microsoft iis 6.0
shodan parse --fields ip_str,port,org --separator , microsoft-data.json.gz
shodan stats telnet
shodan stats --facets ssl.cert.fingerprint has_ssl:true
shodan stats --facets isp net:0/0 (Alt: isp country:DE)
shodan stats --facets vuln.verified country:DE
```
