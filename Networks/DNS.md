*Domain Name Server*

## Resource Records

Record | Explanation
------ |------------
A | IPv4
AAAA | IPv6
MX | Mail Server
NS | Name Server
PTR | Pointer
SOA | Start of Authority (RNAME = DNS admin mail)
CNAME | Canonical Name (Alias or Redirection)
TXT | Text (als Informationsquelle)
SRV | weitere Services
TTL | Time to Live (cache period in seconds)

## Full Qualified Domain Name (FQDN)
Record | Explanation
------ | ----------
www | hostname
google | domain
.com | TLD (Top Level Domain)
. | separator from root 

## AXFR (Asynchronous Xfer Range)
- Zone transfer between primary and secondary DNS server 
- Secondary server receives read only copy 

## DNS Flow
1) Device asks Resolver
2) Resolver, if no cache available, asks Root Server
3) Root Server, if no cache available, asks TLD Server
4) TLD Server, if no cache available, asks Authoritative Server
5) Resolver will cache the answer and revert the answer back to Device

![grafik](https://user-images.githubusercontent.com/84674087/132402603-19309f7e-654f-4f85-8ca9-4147b1a043c7.png)
