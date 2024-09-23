# Network server

## Remote scan server port

tcp:
```
nmap -p 0-65535 -v <ip_server/url>
```
udp:
```
sudo nmap -p 0-65535 -v <ip_server/url> -sU
```

## Get listen port

```
netstat -lnp
```
