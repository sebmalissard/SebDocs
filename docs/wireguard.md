# Wireguard

## Install client

Generate new peer config see: my-toolkit/vpn/wg_gen_config.sh

### Debian

```
sudo apt install wireguard openresolv
```

Copy the config on the client:
```
sudo cp peerX.confg /etc/wireguard/wg0.conf
```

Start the VPN:
```
sudo wg-quick up wg0
```

Check the status:
```
sudo wg show
```
