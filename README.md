# Xfce patches

This is a repository with patches for some Xfce's components.

Because Xfce is a modular desktop environment and its components may interact between themselves, the safest way is to keep them at the same versions as they're intended to be shipped with together. If you want to upgrade components to versions different than your currently installed, keep in mind that you might encounter some major or minor issues.

You can always check the version of any Xfce's component by using the `--version` option while executing its binary in the terminal. The component's version targeted by a patch is indicated in the file name of the given patch.

Don't expect any polished features. It's all just meant to be for personal use.

## Available patches

* [xfwm4](#xfwm4)
  * [Rounded corners](#rounded-corners)
  * [Center window 1/2](#center-window-12)
* [libxfce4ui](#libxfce4ui)
  * [Center window 2/2](#center-window-22)
* [xfdesktop](#xfdesktop)
  * [Right-click command](#right-click-command)
* [xfce4-panel](#xfce4-panel)
  * [Tasklist: centered labels](#tasklist-centered-labels)
  * [Tasklist: faded long labels](#tasklist-faded-long-labels)

## xfwm4

### Building and running

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

### Rounded corners

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

### Center window 1/2

This is the first part of a patch that enables binding a keyboard shortcut to center the focused window.

To use the patch, drop its file into the source code directory, apply it and rebuild the modified version:
```
git apply xfwm4-4.14.0-center-window.patch && make
```

To get the keyboard shortcut working, you must also apply the second part of the patch to libxfce4ui.

## libxfce4ui

### Building and running

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

### Center window 2/2

This is the second part of the patch that enables binding a keyboard shortcut to center the focused window.

To use the patch, drop its file into the source code directory, apply it and rebuild the modified version:
```
git apply libxfce4ui-4.14.1-center-window.patch && make
```

After this patch, you should finally be able to bind a keyboard shortcut to the "Center window" action.

## xfdesktop

### Building and running

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

### Right-click command

This is a patch that allows running a command on desktop right-click, instead of the applications menu.

To use the patch, drop its file into the source code directory, apply it and rebuild the modified version:
```
git apply xfdesktop-4.14.1-right-click-command.patch && make
```

By default, the command is empty and everything works as usual. Once the command is specified and not empty, it'll be executed every time after right-clicking on a desktop area, and the applications menu will be no longer displayed. 

To specify the command, use following <strike>comm</strike> query:

```
xfconf-query -c xfce4-desktop -p /general/right-click-command -s "jgmenu_run"
```

As a side note, `jgmenu_run` refers to the [jgmenu](https://github.com/johanmalm/jgmenu) application, that is a nice replacement for the built-in menu.

## xfce4-panel

### Building and running

Get the xfce4-panel's source code and checkout a tag related to a supported version:
```
git clone https://github.com/xfce-mirror/xfce4-panel.git && cd xfce4-panel
git checkout xfce4-panel-4.14.1
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
killall xfce4-panel; ./panel/xfce4-panel & disown
```

However, you won't see any changes made to plugins, as they are still loaded from the installed version.

If everything's fine regarding the panel itself, you can replace your currently installed version (including plugins):
```
sudo make install
```

Restart the panel to reload plugins:
```
xfce4-panel --restart
```

If you want to restore the original version (example for Ubuntu):
```
sudo make uninstall
sudo apt install --reinstall xfce4-panel
```

### Tasklist: centered labels

This is a patch for the tasklist plugin that centers the window button labels.

It looks good if you want to hide application icons, as spacing between labels is more jarring that way.

To use the patch, drop its file into the source code directory, apply it and rebuild the modified version:
```
git apply xfce4-panel-4.14.1-tasklist-centered-labels.patch && make
```

### Tasklist: faded long labels

This is a patch for the tasklist plugin that fades too long window button labels, instead of ellipsizing them.

The effect is quite similar to what you can see in Firefox, where last few letters of a long tab title are covered with a gradient. However, it looks fine only with a solid panel color, simply because it's just a colored overlay placed on top of the label.

To use the patch, drop its file into the source code directory, apply it and rebuild the modified version:
```
git apply xfce4-panel-4.14.1-tasklist-faded-long-labels.patch && make
```

By default, the overlay has the same color for normal, hovered and active window button's state, and it's picked from the panel background color. Because that might look weird with most themes, you can adjust the overlay colors for these states, by adding following lines to the `~/.config/gtk-3.0/gtk.css` file:
```
@define-color tasklist_faded_long_labels_color #ff0000;
@define-color tasklist_faded_long_labels_color_hover #00ff00;
@define-color tasklist_faded_long_labels_color_active #0000ff;
```

To see updated colors, you need to restart the panel:
```
xfce4-panel --restart
```
