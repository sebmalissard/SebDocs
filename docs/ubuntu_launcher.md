# Ubuntu Launcher

## Creating launcher .desktop

```
cd /usr/share/applications/
cd ~/.local/share/applications/
```
```
touch <progrm>.desktop
```

Example:
```
[Desktop Entry]
Version=x.y
Name=Program Name
Comment=Program description
Exec=/opt/<application>/program
Icon=/opt/<application>/icon.png
Terminal=false
Type=Application
Categories=Utility;Application;
```

Check:
```
desktop-file-validate <progrm>.desktop
```

Install:
```
xdg-desktop-menu install <progrm>.desktop
```

## Usual path

Icon:
```
/usr/share/icons/
~/.local/share/icons
```

## Install

Install desktop file:
```
xdg-desktop-menu install <progrm>.desktop
```

Install icon:
```
xdg-icon-resource install --size <icon_size> <icon>.png
```
