The **Tile-windows** application is a tool which allows for the tiling of windows within non-tiling window manager. It is similar to the [PyTyle](https://code.google.com/archive/p/pytyle/) window manager. As an alternative one can use a native tiling window manager, as explained in the article [Window manager#Tiling window managers](/index.php/Window_manager#Tiling_window_managers "Window manager").

## Installation

[tile-windows](https://aur.archlinux.org/packages/tile-windows/) can be installed from from the [AUR](/index.php/AUR "AUR").

## Configuration

For [fluxbox](/index.php/Fluxbox "Fluxbox") and [openbox](/index.php/Openbox "Openbox") etc, you need to use:

```
$ tile -m

```

This will follow fluxbox rules to choose only some of the windows to tile, not all of them.

For [GNOME](/index.php/GNOME "GNOME") and net-wm etc. you should use:

```
$ tile -w

```

A config file exists in the `/etc/tile/rc` directory. You may want to make a copy to your home folder like: `/home/yourname/.tile/rc` Do **NOT** change `/etc/tile/rc` , because it will not work until you copy it to your .tile folder.

Then make some changes like change multi-desktop from off to workspace if you are using fluxbox:

```
# Multiple Desktop support.. netwm (GNOME/etc), workspace (*Box/Oroborus/etc), off. Default: off
# multi-desktop netwm|workspace|off
multi-desktop workspace

```

Also you can ignore some of the windows by:

```
# X11 Atom / String Value pairs to ignore for calculations and re-placement. No Defaults
# Syntax: avoid Atom(STRING) value
avoid WM_NAME Bottom Panel
avoid WM_NAME Desktop
avoid WM_CLASS FrontPanel

```

To find out the application you want to ignore in tiling, run this command in your terminal:

```
$> xprop WM_CLASS

```

When you mouse become a cross, click on the application window, then xprop will give you the WM_NAME and WM_CLASS. I add one line like this for tilda, my pop up command tool:

```
avoid WM_CLASS Tilda

```