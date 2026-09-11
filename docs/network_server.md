# Network server

## Remote scan server port

tcp scan:
```
nmap -p 0-65535 -v <ip_server/url>
```
udp scan:
```
sudo nmap -p 0-65535 -v <ip_server/url> -sU
```
tcp scan + service identification:
```
nmap -sV -sC -p- <ip_server/url>
```

## Get listen port

```
netstat -lnp
```
