# Mount

## Bind mount

The bind option allows to mount in a other location a part of the file system. By default, mount expected a device block, so the bind (or derivate) option is mandatory to mount a part of the filesystem in another location. For example with a simple situation with 3 directories a,b and c:

```
├── a
│   └── b
├── b
│   └── file
└── c
    └── a
```
Mount bind b in the a directory:
```
mount --bind b a/b
```
```
├── a
│   └── b
│       └── file
├── b
│   └── file
└── c
    └── a
```

If you add files or directories in /b, there are automatically add in /a/b and inversely. Now, if you mount bind a in c/a:
```
mount --bind a c/a
```
```
├── a
│   └── b
│       └── file
├── b
│   └── file
└── c
    └── a
        └── b
```

This time, datas of b directory are not add in c/a/b because the bind is not recursive, to do this you need to use the rbind option:

```
mount --rbind a c/a
```
```
├── a
│   └── b
│       └── file
├── b
│   └── file
└── c
    └── a
        └── b
            └── file
```

In this case, all modification in /b, /a/b and /c/a/b are synchronized.

## tmpfs

```
mount -t tmpfs -o size=512M tmpfs opt/a
```
