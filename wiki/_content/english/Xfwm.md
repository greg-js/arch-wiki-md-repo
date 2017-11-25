Related articles

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Xfce](/index.php/Xfce "Xfce")
*   [Xorg](/index.php/Xorg "Xorg")

**xfwm** is the window manager for the [Xfce](/index.php/Xfce "Xfce") environment.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Starting Xfwm](#Starting_Xfwm)
*   [2 Configuration](#Configuration)
    *   [2.1 Composite manager](#Composite_manager)
    *   [2.2 Window roll-up](#Window_roll-up)
    *   [2.3 Window tiling](#Window_tiling)
    *   [2.4 Extra settings provided by the xfce settings manager](#Extra_settings_provided_by_the_xfce_settings_manager)
    *   [2.5 Additional Themes](#Additional_Themes)
*   [3 Tips & Tricks](#Tips_.26_Tricks)
    *   [3.1 Hide the titlebar when window is maximized](#Hide_the_titlebar_when_window_is_maximized)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 No icons shown in browser for downloaded items](#No_icons_shown_in_browser_for_downloaded_items)
    *   [4.2 Number of workspaces changes unexpectedly](#Number_of_workspaces_changes_unexpectedly)
    *   [4.3 Video tearing](#Video_tearing)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [xfwm4](https://www.archlinux.org/packages/?name=xfwm4) package.

### Starting Xfwm

To run xfwm as stand-alone, edit [Xinitrc](/index.php/Xinitrc "Xinitrc") and add the following line:

```
exec xfwm4

```

## Configuration

Most xfwm settings can be accessed through `xfwm4-settings`, for window behavior and shortcuts, `xfwm4-tweaks-settings`, for advanced settings and compositing, and `xfwm4-workspace-settings`, for the number of workspaces and their names.

### Composite manager

**Note:**

*   This compositor may cause video tearing in applications, see [#Video tearing](#Video_tearing).
*   From Xfwm 4.12 onward, the compositor is enabled by default.

To enable or disable the Xfwm compositor and adjust its settings, go to *Window Manager Tweaks*:

```
$ xfwm4-tweaks-settings

```

Alternatively, it can be enabled with `--compositor` or using *xfconf*. For example:

 `~/.xinitrc`  `exec xfwm4 --compositor=on` 
```
$ xfconf-query -c xfwm4 -p /general/use_compositing -s *true*

```

### Window roll-up

Double clicking the titlebar, or clicking *roll window up* in the window menu, causes the window contents to disappear leaving only the titlebar. To disable this functionality with `xfconf`, run:

```
$ xfconf-query -c xfwm4 -p /general/mousewheel_rollup -s false

```

### Window tiling

Xfwm can "tile" a window automatically when it is moved to an edge of the screen. It does so by resizing it to fit the top half of the screen. To enable or disable this behaviour with `xfconf`, run:

```
$ xfconf-query -c xfwm4 -p /general/tile_on_move -s false
$ xfconf-query -c xfwm4 -p /general/tile_on_move -s true

```

Alternatively, (un)check *Window Manager Tweaks* > *Accessibility* > *Automatically tile windows when moving toward the screen edge*.

### Extra settings provided by the xfce settings manager

[Install](/index.php/Install "Install") [xfce4-settings](https://www.archlinux.org/packages/?name=xfce4-settings) from the [official repositories](/index.php/Official_repositories "Official repositories")

**Note:** Installing [xfce4-settings](https://www.archlinux.org/packages/?name=xfce4-settings) may change the default applications for certain tasks. See [xdg-open](/index.php/Xdg-open "Xdg-open") to set the default applications to your liking.

### Additional Themes

[Install](/index.php/Install "Install") [xfwm4-themes](https://www.archlinux.org/packages/?name=xfwm4-themes) from the [official repositories](/index.php/Official_repositories "Official repositories")

The themes installed will be shown in the `xfwm4-settings` window.

## Tips & Tricks

### Hide the titlebar when window is maximized

Go to `Accessibility` and check `Hide title of windows when maximized`.

**Note:** It is recommend to install [xfce4-windowck-plugin](https://aur.archlinux.org/packages/xfce4-windowck-plugin/) if you want to put the titlebar of current maximized window on you panel.

## Troubleshooting

### No icons shown in browser for downloaded items

This is fixed by [installing](/index.php/Installing "Installing") [xfce4-settings](https://www.archlinux.org/packages/?name=xfce4-settings) from the [official repositories](/index.php/Official_repositories "Official repositories").

### Number of workspaces changes unexpectedly

Keep in mind *Xfwm* assigns shortcuts to adding and removing workspaces. By default these are `Alt+Delete` and `Alt+Insert`, respectively.

If the number of workspaces resets at login, change the amount **after** Xfwm is started. This is ensured by the `sleep` command. [[1]](https://bugs.launchpad.net/ubuntu/+source/xfwm4/+bug/787934)

 `~/.xinitrc` 
```
(sleep 3 && xfconf-query -v -c xfwm4 -p /general/workspace_count -s *number*) &
exec xfwm4

```

or, from [xfce4-session](https://www.archlinux.org/packages/?name=xfce4-session):

 `~/.config/autostart/workspace.desktop` 
```
[Desktop Entry]
Exec=sh -c "sleep 3 && xfconf-query -v -c xfwm4 -p /general/workspace_count -s *number*"
```

See also: [Logout alters workspaces](http://forum.xfce.org/viewtopic.php?id=6056)

### Video tearing

If you experience video tearing whilst using Xfwm, open *xfwm4-tweaks-settings*, navigate to the compositor tab and tick the *Synchronize drawing to the vertical blank* option. If you use Intel graphics and you have already enabled "TearFree" option in Xorg config as described in [Intel graphics#Tear-free video](/index.php/Intel_graphics#Tear-free_video "Intel graphics"), then disable *Synchronize drawing to the vertical blank* option.

If this does not fix the tearing, consider disabling Xfwm's compositor and using an alternative [composite manager](/index.php/Composite_manager "Composite manager").

## See also

*   [Xfwm - Introduction](http://docs.xfce.org/xfce/xfwm4/introduction)