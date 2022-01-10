## tcpdump
Argument | Meaning
-------- | -------
-w test.pcap | write .pcap
-r test.pcap | read .pcap
-D | show all interfaces
-A | print each packet in ASCII; good for capturing web pages
-i eth0 -vv | select specific interface eth0
-n | numeric
-s0 | snaplen to default = 262144 bytes = data from each packet
host | indicate host

## tshark (Wireshark CLI Tool)
Argument | Meaning
-------- | -------
- -i | interface]
- -f | packet filter
- -D | print interfaces
- -L | print link layer types
- -O [protocol] | only show specific packets of this protocol
- -F | output file type
- -c [packet count] | stop after n packets
- -n | disable name resolution
- -d [layer type]==[selector] | -d tcp.port==21,ftp
- -r [file] | read from file.pcap
- -w [file] | write result to file

## Examples
- `tshark.exe -d tcp.port==21,ftp -w ftp.pcap`
- `sudo tcpdump -ni eth0 -s0 -A icmp`
- `sudo tcpdump -i enp0s3 port telnet -w telnetloginattempts.pcap`
- `sudo tcpdump host [IPv4] -s0 -A` (listen to raw packets on IPv4)
