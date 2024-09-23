# Raspberry Pi

# Install

Download image: https://www.raspberrypi.com/software/operating-systems/

Then flash it: ```dd``` or https://etcher.balena.io/

# Setup

https://www.raspberrypi.com/documentation/computers/configuration.html#setting-up-a-headless-raspberry-pi

## Enable ssh

Create ```ssh``` empty file in the ```boot``` partition.

## Create user

New file ```userconf.txt```:
```
user:encrypted_password

```
Generate encrypted password:
```
openssl passwd -6
```