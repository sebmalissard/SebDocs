# RSA

[https://medium.com/@bn121rajesh/rsa-sign-and-verify-using-openssl-behind-the-scene-bf3cac0aade2](https://medium.com/@bn121rajesh/rsa-sign-and-verify-using-openssl-behind-the-scene-bf3cac0aade2)

```
$ echo $(($(sha256sum file | awk '{printf $1}' | wc -m)*4))
256
$ echo $(($(sha1sum file | awk '{printf $1}' | wc -m)*4))
160
$ echo $(($(md5sum file | awk '{printf $1}' | wc -m)*4))
128
$ echo $(($(sha512sum file | awk '{printf $1}' | wc -m)*4))
512
```
