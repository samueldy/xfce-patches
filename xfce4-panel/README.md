# xfce4-panel

## Available patches

* [Tasklist: centered labels](#tasklist-centered-labels)
* [Tasklist: faded long labels](#tasklist-faded-long-labels)

## Building and running

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

## Tasklist: centered labels

This is a patch for the tasklist plugin that centers the window button labels.

It looks good if you want to hide application icons, as spacing between labels is more jarring that way.

To use the patch, drop its file into the source code directory, apply it and rebuild the modified version:
```
git apply xfce4-panel-4.14.1-tasklist-centered-labels.patch && make
```

## Tasklist: faded long labels

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
