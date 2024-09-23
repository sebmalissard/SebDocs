# LXC

## LXD

### Installation

[Ubuntu tutorial-setting-up-lxd](https://ubuntu.com/tutorials/tutorial-setting-up-lxd-1604-fr)

By adding the non-root Unix user account to the lxd group, you are able to run any lxc commands without prepending sudo. Without this addition, you would have needed to prepend sudo to each lxc command.

```
sudo usermod -a -G lxd <user>
```

### Commands

#### List containers

```
lxc list
```

#### List container available

```
lxc remote list
```
```
lxc image list images:
lxc image list ubuntu:
```

Local:
```
lxc image list
```

#### Create and start containers from images

```
lxc launch ubuntu:18.04 mycontainer
```

Login on container Ubuntu:
```
lxc exec <container> -- sudo --user ubuntu --login
```

Alpine:
```
lxc exec <container> sh
lxc exec <container> login <user>
```

#### Proxy devices

```
lxc config device add <container> myport80 proxy listen=tcp:0.0.0.0:80 connect=tcp:127.0.0.1:80
```
```
lxc config device show <container>
```

#### Shared folder

```
lxc config device add <container> raid disk source=/media/raid/ path=/raid/
```

Verify that directory has been mounted onto <container> by running (don't work with Alpine):
```
lxc exec <container> -- "ls /media/raid/"
```

[how-to-add-or-mount-directory-in-lxd-linux-containe](https://www.cyberciti.biz/faq/how-to-add-or-mount-directory-in-lxd-linux-container/)

#### Export a container as image

```
lxc publish <container> --alias <alias-image>
```
```
lxc image export <image> <directory>
```

#### Storage

```
lxc storage list
lxc storage show default
```

Create new storage pool:
```
lxc storage create <disk_name> zfs
lxc storage create <disk_name> zfs size=10GB
```

list:
```
sudo ls -alh  /var/snap/lxd/common/lxd/disks
```

[https://lxd.readthedocs.io/en/latest/storage](https://lxd.readthedocs.io/en/latest/storage/)  
[https://discuss.linuxcontainers.org/t/change-storage-size-and-driver/6097](https://discuss.linuxcontainers.org/t/change-storage-size-and-driver/6097)

## LXC

### Commands

Always run the followings commands in root.

#### lxc-start

```
lxc-start -n <container-name>
```

#### lxc-ls

```
lxc-ls --fancy
```

#### lxc-attach

To attach container to the current console
```
lxc-attach -n <container-name>
```

#### lxc-stop

```
lxc-stop -n <container-name>
```

### Usefull path

```
/usr/share/lxc/templates
/var/lib/lxc
```
