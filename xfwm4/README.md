# xfwm4

## Building and running

Get the xfwm4's source code and checkout a tag related to a supported version:
```
git clone https://github.com/xfce-mirror/xfwm4.git && cd xfwm4
git checkout xfwm4-4.14.0
```

Determine the system library path (do it on your own) and set a variable. For a Ubuntu-based distro it'll be:
```
LIBDIRPATH=/usr/lib/x86_64-linux-gnu
```

Configure the build environment (install required dependencies on your own) and compile the source code:
```
./autogen.sh --prefix=/usr --libdir=$LIBDIRPATH --libexecdir=$LIBDIRPATH && make
```

Check if the compiled version is working correctly:
```
./src/xfwm4 --replace & disown
```

If everything's fine, you can replace your currently installed version:
```
sudo make install
```

If you want to restore the original version (example for Ubuntu):
```
sudo make uninstall
sudo apt install --reinstall xfwm4
```

## Rounded corners

This is a patch that allows drawing windows with rounded corners and, optionally, no decorations.

It is based on [an Openbox patch](https://github.com/dylanaraps/openbox-patched) and thus there is no antialiasing, despite xfwm's compositing capabilities.

To use the patch, drop its file into the source code directory, apply it and rebuild the modified version:
```
git apply xfwm4-4.14.0-rounded-corners.patch && make
```

By default, rounded corners have a radius of 8 px and are disabled for maximized windows. Also, window decorations are visible by default, but mind that most xfwm themes won't look good with rounded corners because they provide side and bottom borders. Themes with no borders, but only with titlebar, should look fine though.

To configure mentioned options, use following commands:

```
xfconf-query -c xfwm4 -p /general/rounded_corners_radius -s 12
xfconf-query -c xfwm4 -p /general/rounded_corners_maximized -s true
xfconf-query -c xfwm4 -p /general/rounded_corners_keep_decorations -s false
```

Setting the radius value to 0 disables the effect and restores original window shapes.

## Center window (part 1)

This is the first part of a patch that enables binding a keyboard shortcut to center the focused window.

To use the patch, drop its file into the source code directory, apply it and rebuild the modified version:
```
git apply xfwm4-4.14.0-center-window.patch && make
```

To get the keyboard shortcut working, you must also apply the second part of the patch to libxfce4ui.
