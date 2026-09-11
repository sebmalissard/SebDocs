# Samba

[https://wiki.alpinelinux.org/wiki/Setting_up_a_samba-server](https://wiki.alpinelinux.org/wiki/Setting_up_a_samba-server)

## Installation for Alpine:

```
apk add samba
```

Modify config file:
```
vi /etc/samba/smb.conf
```
```
[global]
   workgroup = WORKGROUP
   force user = nobody
   force group = nobody
   guest account = nobody 

[nas]
   browseable = yes
   writeable = yes   
   path = /raid
   guest ok = yes
   force user = nobody
   force group = nobody
```

## Create user

Samba user need to be create and exist on the OS.

Create OS user:
```
sudo useradd -M -s /usr/sbin/nologin <user>
```

Create Samba user:
```
sudo smbpasswd -a <user>
```
Edit `/etc/samba/smb.conf` if needed and check the config with `testparm`

Restart smb server:
```
sudo service smbd force-reload
```