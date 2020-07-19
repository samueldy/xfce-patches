# Xfce patches

This is a repository with patches for some Xfce's components.

Don't expect any polished features. It's all just meant to be for personal use.

## About versions

Because Xfce is a modular desktop environment and its components may interact between themselves, the safest way is to keep them at the same versions as they're intended to be shipped with together. If you want to selectively upgrade (or downgrade) components, keep in mind that you might encounter some major or minor issues.

You can always check the version of any Xfce's component by using the `--version` option while executing its binary in the terminal. The component's version targeted by a patch is indicated in the file name of the given patch.

## Available patches

* [xfwm4](xfwm4)
  * [Rounded corners](xfwm4#rounded-corners)
  * [Center window (part 1)](xfwm4#center-window-part-1)
* [libxfce4ui](libxfce4ui)
  * [Center window (part 2)](libxfce4ui#center-window-part-2)
* [xfdesktop](xfdesktop)
  * [Right-click command](xfdesktop#right-click-command)
* [xfce4-panel](xfce4-panel)
  * [Tasklist: centered labels](xfce4-panel#tasklist-centered-labels)
  * [Tasklist: faded long labels](xfce4-panel#tasklist-faded-long-labels)
