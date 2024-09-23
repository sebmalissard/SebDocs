# Linux File Permissions

Sources :  
[https://wiki.archlinux.org/index.php/File_permissions_and_attributes](https://wiki.archlinux.org/index.php/File_permissions_and_attributes)
[https://www.mkssoftware.com/docs/man1/ls.1.asp](https://www.mkssoftware.com/docs/man1/ls.1.asp)

## Viewing standard permissions

Use the ```ls -l``` command to view the permissions set for the contents of a directory.

```sh
$ ls -l /home/$USER
total 32
drwxr-xr-x 2 seb seb 4096 déc.   7 20:05 Desktop
drwxr-xr-x 2 seb seb 4096 déc.   7 20:05 Documents
drwxr-xr-x 2 seb seb 4096 déc.   7 20:05 Downloads
drwxr-xr-x 2 seb seb 4096 déc.   7 20:05 Music
drwxr-xr-x 2 seb seb 4096 déc.   7 20:05 Pictures
drwxr-xr-x 2 seb seb 4096 déc.   7 20:05 Public
drwxr-xr-x 2 seb seb 4096 déc.   7 20:05 Templates
drwxr-xr-x 2 seb seb 4096 déc.   7 20:05 Videos
```

You can view permissions along a path with ```namei -l``` command.

```sh
$ namei -l /home/seb/Documents/document.txt 
f: /home/seb/Documents/document.txt
drwxr-xr-x root root /
drwxr-xr-x root root home
drwxr-xr-x seb  seb  seb
drwxr-xr-x seb  seb  Documents
-rw-r--r-- seb  seb  document.txt
```

The first character is the file type, the next characters are three permission (owner, group and other) triads (read, write and execute) and the optional final character indicated an extended permission.

### File type

| Character | Description           |
|-----------|-----------------------|
| -         | Regular file          |
| b         | Block device file     |
| c         | Character device file |
| d         | Directory             |
| l         | Symbolic link         |
| n         | Network file          |
| p         | Named pipe            |
| s         | Local socket file     |

[https://linuxconfig.org/identifying-file-types-in-linux](https://linuxconfig.org/identifying-file-types-in-linux)

### Read permission

| Character | Description                                                         |
|-----------|---------------------------------------------------------------------|
| -         | The file cannot be read or the directory's content cannot be shown. |
| r         | The file can be read or the directory's content can be shown.       |

### Write permission

| Character | Description                                                                                                                                |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------|
| -         | The file cannot be modified or the directory's content cannot be modified.                                                                 |
| w         | The file can be modified or the directory's content be modified (requires the execute permission otherwise this permission has no effect). |

### Execute permission

| Character | Description                                                                                                       |
|-----------|-------------------------------------------------------------------------------------------------------------------|
| -         | The file cannot be executed or the directory cannot be accessed with cd.                                          |
| x         | The file can be executed or the directory can be accessed with cd.                                                |
| s         | Set the x permission and add the setuid bit when found in user triad or the setgid when found in the group triad. |
| S         | Add the setuid bit when found in user triad or the setgid when found in the group triad.                          |
| t         | Set the x permission and add the stickly bit when found in the others triad.                                      |
| T         | Add the stickly bit when found in the others triad.                                                               |

### Extended permission

| Character | Description             |
|-----------|-------------------------|
|           | No extended permission. |
| +         | ACL.                    |
| .         | SEpolicy.               |

## Modify standard permission

### chmod

The setuid can be enable with the following command:
```
chmod 4755 file
chmod u+s file
```

setuid=4, setgid=2 and sticky=1

### chown

TODO

## Access Control List (ACL)

[https://linuxconfig.org/how-to-manage-acls-on-linux](https://linuxconfig.org/how-to-manage-acls-on-linux)

ACLs are a second level of discretionary permissions, that may override the standard permissions.

### Mount filesystem with ACL

To verify that the filesystem was mounted with the acl option the ```tune2fs -l``` can be used:

```
# tune2fs -l /dev/sda5 | grep "Default mount options"
Default mount options:    user_xattr acl
```

If your filesystem has not been mounted with the ‘acl’ option, you can re-mount it giving the needed option:

```
# mount -o remount -o acl /dev/sda1
```

However, notice that the mount options set this way, will not be persistent, and will not survive a reboot. If you want to obtain persistence, you have to modify the filesystem mount options in /etc/fstab, assigning the ‘acl’ option statically.


## Get ACL

The command to get acl information is getfacl.

```
$ ls -al document.txt 
-rw-rw-r--+ 1 seb seb 9 mars  13 20:41 document.txt
$ getfacl document.txt 
# file: document.txt
# owner: seb
# group: seb
user::rw-
user:toto:rw-
group::r--
mask::rw-
other::r--
```

With ACL, the group triad is replace by the ACL mask.

Note: If the file had not acl, the standard permission are display.

```
$ ls -l file.txt 
-rw-r--r-- 1 seb seb 0 mars  13 21:48 file.txt
$ getfacl file.txt 
# file: file.txt
# owner: seb
# group: seb
user::rw-
group::r--
other::r--
```

## Set ACL

The command to set acl information is setfacl.

```
$ setfacl -m u:toto:rw document.txt
```

With acl a mask is applied to the other ACL permission (except for owner permission). Example:
```
$ setfacl -m g::rw document.txt
$ setfacl -m mask:r document.txt
$ getfacl document.txt 
# file: document.txt
# owner: seb
# group: seb
user::rw-
user:toto:rw-  #effective:r--
group::rw-  #effective:r--
mask::r--
other::r--
$ ls -l document.txt 
-rw-r--r--+ 1 seb seb 9 mars  13 20:41 document.txt
```

Example to set several permission in the same command with setfacl -m:
```
$ setfacl -m user::rx,other::rwx document.txt
$ getfacl document.txt 
# file: document.txt
# owner: seb
# group: seb
user::r-x
user:toto
group::rw-
mask::rw-
other::rwx
```
