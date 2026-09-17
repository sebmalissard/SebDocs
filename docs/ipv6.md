# IPV6

## Structure of global unicast address

The IPv6 address size is 128bits (IPv4 size is 32bits), separate in 2 parts:

- Network identifier (64 bits)
- Interface identifier (64 bits)

### Interface identifier from MAC (SLAAC)

The ipv6 is generally derivate from the MAC address with the following steps:

MAC example: 01:02:03:04:05:06

- Add "ff:fe" in the middle of the MAC: 0102:ff:fee04:0506
- Invert the U/L bit (the second LSB bit of the first byte): 0302:ff:fee04:0506
- To finish add interface preffix (example with local): fe80::0302:ff:fee04:0506
