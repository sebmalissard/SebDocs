# Raspberry Pi DNS

## Image

Install Raspberry Pi OS 64bit lite

```
sudo apt update
sudo apt full-upgrade
```

## Unbound

```
sudo apt install unbound dnsutils
```
Check "System clock synchronized"::
```
timedatectl
```
Create config file:
```
sudo vim /etc/unbound/unbound.conf.d/local-recursif.conf
```
```
server:
    verbosity: 0
    interface: 127.0.0.1
    port: 5335
    do-ip4: yes
    do-udp: yes
    do-tcp: yes
    do-ip6: no
    harden-glue: yes
    harden-dnssec-stripped: yes
    use-caps-for-id: no
    edns-buffer-size: 1232
    prefetch: yes
    num-threads: 2
    hide-identity: yes
    hide-version: yes
    msg-cache-size: 50m
    rrset-cache-size: 100m
    cache-min-ttl: 300
    serve-expired: yes
    private-address: 192.168.0.0/16
    private-address: 172.16.0.0/12
    private-address: 10.0.0.0/8
```
Check config syntax:
```
sudo unbound-checkconf
```
Restart:
```
sudo systemctl restart unbound
sudo systemctl status unbound
```

## Adguard

Install:
```
curl -s -S -L https://raw.githubusercontent.com/AdguardTeam/AdGuardHome/master/scripts/install.sh | sh -s -- -v
```
Check port 3000 (assistant) is opened:
```
sudo systemctl status AdGuardHome
sudo ss -tulpn | grep -E ':53 |:3000'
```
Configure:
```
http://<IP>:3000
```
Follow instructions and then go to "Paramètres" > "Paramètres DNS".

Set "Servers DNS upstream":
```
127.0.0.1:5335
```
Clear "Serveurs DNS d’amorçage"

Check port 53 is opened:
```
sudo ss -tulpn | grep ':53 '
```
Test from another PC:
```
nslookup fr.wikipedia.org <IP>
```

## ACME / Let's Encrypt

Root without history:
```
sudo -i
unset HISTFILE
```
Install ACME:
```
curl https://get.acme.sh | sh -s email=votre@email.fr
source ~/.bashrc
```
Check:
```
acme.sh --version
acme.sh --set-default-ca --server letsencrypt
dig acme-v02.api.letsencrypt.org +short
```
Generate certificat:
```
export OVH_END_POINT=ovh-eu
export OVH_AK='<application_key>'
export OVH_AS='<application_secret>'
export OVH_CK='<consumer_key>'
acme.sh --issue --dns dns_ovh -d dns.sebmd.fr --dnssleep 120
```
Install certificate for adguard:
```
mkdir -p /opt/AdGuardHome/certs
acme.sh --install-cert -d dns.sebmd.fr --ecc \
  --fullchain-file /opt/AdGuardHome/certs/fullchain.pem \
  --key-file /opt/AdGuardHome/certs/privkey.pem \
  --reloadcmd "systemctl restart AdGuardHome"
chmod 600 /opt/AdGuardHome/certs/privkey.pem
chmod 600 /root/.acme.sh/account.conf
ls -l /opt/AdGuardHome/certs/
```

## Adguard HTTPS

Go to "Paramètre" > "Paramètres de chiffrement":
 - Enable "Activer le chiffrement"
 - Nom du server : dns.sebmd.fr
 - Certificats: /opt/AdGuardHome/certs/fullchain.pem
 - Clé privée: /opt/AdGuardHome/certs/privkey.pem
