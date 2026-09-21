# Cryptomator

## WSL

To access a Cryptomator vault from WSL, set the mount type to **WinFsp (Local Drive)** in the vault options, then unlock the vault. In WSL, mount the drive manually:

```bash
sudo mkdir -p /mnt/f
sudo mount -t drvfs F: /mnt/f
```
