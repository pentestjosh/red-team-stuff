## NMAP Cheat Sheet
Handy nmap commands used along the way

# Firewalls IDS Evasion and Spoofing
```
-f; --mtu VALUE - Fragment packets (optionally w/given MTU)

-D decoy1,decoy2,ME - Cloak a scan with decoys

-S IP-ADDRESS - Spoof source address

-e IFACE - Use specified interface

-g PORTNUM - --source-port PORTNUM Use given port number

--proxies url1,[url2],... - Relay connections through HTTP / SOCKS4 proxies

--data-length NUM - Append random data to sent packets

--ip-options OPTIONS - Send packets with specified ip options

--ttl VALUE - Set IP time to live field

--spoof-mac ADDR/PREFIX/VENDOR - Spoof NMAP MAC address

--badsum - Send packets with a bogus TCP/UDP/SCTP checksum
```
# Timing and Performance (Important to avoid detection)
```
-T 0-5 - Set timing template - higher is faster (less accurate)

--min-hostgroup SIZE
--max-hostgroup SIZE - Parallel host scan group sizes

--min-parallelism NUMPROBES
--max-parallelism NUMPROBES - Probe parallelization

--min-rtt-timeout TIME
--max-rtt-timeout TIME
--initial-rtt-timeout TIME - Specifies probe round trip time

--max-retries TRIES - Caps number of port scan probe retransmissions

--host-timeout TIME - Give up on target after this long

--scan-delay TIME
--max-scan-delay TIME - Adjust delay between probes

--min-rate NUMBER - Send packets no slower than NUMBER per second

--max-rate NUMBER - Send packets no faster than NUMBER per second
```

# Port scanning

Quick Scan
```
nmap -Pn [ipaddress]
```
Full TCP port scan using with service version detection
```
nmap -p 1-65535 -Pn -sV -sS -T4 [ipaddress]
```
Scan particular ports
```
nmap -Pn -p 22,80,443 [ipaddress]
```
Find linux devices in local network
```
nmap -p 22 --open -sV 192.168.10.0/24
```

# Trace traffic

Trace Traffic
```
nmap --traceroute -p 80 [ipaddress]
```
Trace traffic with Geo resolving
```
nmap --traceroute --script traceroute-geolocation.nse -p 80 [ipaddress]
```

# Get Ip Info

ISP, Country, Company
```
nmap --script=asn-query [ipaddress]
```

# Test SSL
Get SSL Certificate
```
nmap --script ssl-cert -p 443 -Pn [ipaddress]
```
Test SSL Ciphers
```
nmap --script ssl-enum-ciphers -p 443 [ipaddress]
```

# Brute Force
Ftp Brute force
```
nmap --script ftp-brute --script-args userdb=users.txt,passdb=passwords.txt -p 21 -Pn [ipaddress]
```
HTTP Basic Authentication Brute force
```
nmap --script http-brute -script-args http-brute.path=/evifile-bb-demo,userdb=users.txt,passdb=passwords.txt -p 80 -Pn [ipaddress]
```
Wordpress Bruteforce
```
nmap -sV --script http-wordpress-brute --script-args userdb=users.txt,passdb=passwords.txt,http-wordpress-brute.hostname=dhound.io,http-wordpress-brute.threads=10 -p 80 [ipaddress]
```
SSH Brute Force
```
use ncrack etc
```

# Attacks
Find vulnerabilities in safe mode
```
nmap --script default,safe -Pn [ipaddress]
```
Find vulnerabilities in unsafe mode
```
nmap --script vuln -Pn [ipaddress]
```
Run DDos attack
```
nmap --script dos -Pn [ipaddress]
```
Exploit detected vulnerabilities
```
nmap --script exploit -Pn [ipaddress]
```

# Enumeration Examples
Enumerating Netbios Detect all exposed Netbios servers on the subnet.
```
nmap -sV -v -p 139,445 10.0.1.0/24
```
Nmap find Netbios name
```
nmap -sU --script nbstat.nse -p 137 10.0.1.12
```
Check if Netbios servers are vulnerable to MS08-067
```
nmap --script-args=unsafe=1 --script smb-check-vulns.nse -p 445 10.0.0.1
```
