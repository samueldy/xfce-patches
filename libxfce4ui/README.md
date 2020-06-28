# libxfce4ui

## Building and running

Get the libxfce4ui's source code and checkout a tag related to a supported version:
```
git clone https://github.com/xfce-mirror/libxfce4ui.git && cd libxfce4ui
git checkout libxfce4ui-4.14.1
```

Determine the system library path (do it on your own) and set a variable. For a Ubuntu-based distro it'll be:
```
LIBDIRPATH=/usr/lib/x86_64-linux-gnu
```

Configure the build environment (install required dependencies on your own) and compile the source code:
```
./autogen.sh --prefix=/usr --libdir=$LIBDIRPATH --libexecdir=$LIBDIRPATH && make
```

Replace your currently installed version:
```
sudo make install
```

If you want to restore the original version (example for Ubuntu):
```
sudo make uninstall
sudo apt install --reinstall libxfce4ui-1-0
sudo apt install --reinstall libxfce4ui-2-0
```

## Center window (part 2)

This is the second part of the patch that enables binding a keyboard shortcut to center the focused window.

To use the patch, drop its file into the source code directory, apply it and rebuild the modified version:
```
git apply libxfce4ui-4.14.1-center-window.patch && make
```

After this patch, you should finally be able to bind a keyboard shortcut to the "Center window" action.
