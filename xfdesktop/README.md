# xfdesktop

## Available patches

* [Right-click command](#right-click-command)

## Building and running

Get the xfdesktop's source code and checkout a tag related to a supported version:
```
git clone https://github.com/xfce-mirror/xfdesktop.git && cd xfdesktop
git checkout xfdesktop-4.14.1
```

Determine the system library path (do it on your own) and set a variable. For a Ubuntu-based distro it'll be:
```
LIBDIRPATH=/usr/lib/x86_64-linux-gnu
```

Configure the build environment (install required dependencies on your own) and compile the source code:
```
./autogen.sh --prefix=/usr --libdir=$LIBDIRPATH --libexecdir=$LIBDIRPATH && make
```

_Note:_ Make sure to install `libgarcon` development package, as it's marked as optional, but it's important.

Check if the compiled version is working correctly:
```
killall xfdesktop; ./src/xfdesktop & disown
```

If everything's fine, you can replace your currently installed version:
```
sudo make install
```

If you want to restore the original version (example for Ubuntu):
```
sudo make uninstall
sudo apt install --reinstall xfdesktop4
```

## Right-click command

This is a patch that allows running a command on desktop right-click, instead of the applications menu.

To use the patch, drop its file into the source code directory, apply it and rebuild the modified version:
```
git apply xfdesktop-4.14.1-right-click-command.patch && make
```

By default, the command is empty and everything works as usual. Once the command is specified and not empty, it'll be executed every time after right-clicking on a desktop area, and the applications menu will be no longer displayed.

To specify the command, use following query:

```
xfconf-query -c xfce4-desktop -p /general/right-click-command -s "xfce4-terminal"
```
