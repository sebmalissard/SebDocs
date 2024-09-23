# Wifi

## Scan wifi

```
sudo iwlist wlan0 scan
sudo iwlist wlan0 scan | grep Freebox-476BED
```

## Configure Wifi

### Raspbian

```
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```
```
network={
    ssid="Freebox-476BED"
    psk="xxxxxxxxxxxxxxxxxxxxx"
}
```
```
sudo reboot
```

Start manually:
```
wpa_supplicant -B -c/etc/wpa_supplicant/wpa_supplicant.conf -iwlan0 -Dnl80211,wext
wpa_supplicant -B -c/etc/wpa_supplicant.conf -iwlan0 -Dnl80211,wext
```
