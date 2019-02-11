The display server is accompanied by a *cursor theme* that helps various aspects of GUI navigation and manipulation. The display server includes a cursor theme, however, other cursor themes can be installed and selected.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Packages](#Packages)
    *   [1.2 Manually](#Manually)
*   [2 Configuration](#Configuration)
    *   [2.1 XDG specification](#XDG_specification)
    *   [2.2 LXAppearance](#LXAppearance)
    *   [2.3 Desktop environments](#Desktop_environments)
        *   [2.3.1 GNOME](#GNOME)
        *   [2.3.2 MATE](#MATE)
        *   [2.3.3 XFCE](#XFCE)
    *   [2.4 X resources](#X_resources)
    *   [2.5 Environment variable](#Environment_variable)
    *   [2.6 Display managers](#Display_managers)
        *   [2.6.1 GDM](#GDM)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Create links to missing cursors](#Create_links_to_missing_cursors)
    *   [3.2 Supplying missing cursors](#Supplying_missing_cursors)
        *   [3.2.1 rdesktop](#rdesktop)
    *   [3.3 Change X shaped default cursor](#Change_X_shaped_default_cursor)
    *   [3.4 .Xdefaults](#.Xdefaults)
*   [4 See also](#See_also)

## Installation

Installation can be done with a package, or downloaded and extracted to an appropriate directory.

### Packages

Cursors themes are available in the:

*   [Official repositories](/index.php/Official_repositories "Official repositories") — ["xcursor-" search](https://www.archlinux.org/packages/?sort=&q=xcursor-&maintainer=&last_update=&flagged=&limit=50).
*   [AUR](/index.php/AUR "AUR") — ["cursor" search](https://aur.archlinux.org/packages.php?O=0&L=0&C=17&K=cursor&SeB=nd&SB=n&SO=a&PP=50&do_Search=Go).

### Manually

If a cursor theme is not available in the official repositories or the AUR, it can be added manually. A number of websites exist where cursor themes can be downloaded. Once downloaded, they need to be put in the *icons* directory (as cursors have the ability to be bundled with icon themes).

Some websites that have cursor themes:

*   [GNOME Look](https://www.gnome-look.org/browse/cat/107/ord/latest/)
*   [Customize.org](http://www.customize.org/list/xcursors)
*   [Deviant Art](https://www.deviantart.com/browse/all/customization/skins/linuxutil/x11cursors/)
*   [Open Desktop](https://www.opendesktop.org/browse/cat/107/)

For *user-specific* installation, use the `~/.icons/` directory. Extract them with this command that will work for most archives:

```
$ tar xvf foobar-cursor-theme.tar.gz -C ~/.icons

```

The cursor theme directory structure is `theme-name/cursors`, for example: `~/.icons/*theme*/cursors/`; make sure the extracted files follow this structure.

**Note:** For *system-wide* installation the `/usr/share/icons` directory is used. Direct extraction to this directory is usually discouraged as files here are not tracked by [pacman](/index.php/Pacman "Pacman"); it is recommended to create a [package](/index.php/PKGBUILD "PKGBUILD") for the cursor theme instead.

Already installed cursor themes can be viewed with the command:

```
find /usr/share/icons ~/.icons -type d -name "cursors"

```

If the package includes an `index.theme` file, check if there is an "Inherits" line inside. If yes, check whether the inherited theme also exists on the system (rename if needed).

## Configuration

There are various ways to set the cursor theme.

### XDG specification

This method applies to both [X11](/index.php/X11 "X11") and [Wayland](/index.php/Wayland "Wayland") cursor themes.

For *user-specific* configuration, create or edit `~/.icons/default/index.theme`; for *system-wide* configuration, one can edit `/usr/share/icons/default/index.theme`.

The `Inherits` option in the `[icon theme]` section must be set to the xcursor theme directory name `*cursor_theme_name*`, for example `xcursor-breeze-snow`:

 `~/.icons/default/index.theme` 
```
[icon theme] 
Inherits=*cursor_theme_name*
```

You should then edit `~/.config/gtk-3.0/settings.ini`, replacing the `*cursor_theme_name*` with the chosen one:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-cursor-theme-name=*cursor_theme_name*
```

Re-login for the changes to take effect.

### LXAppearance

[LXAppearance](/index.php/LXDE#Cursors "LXDE") sets the default cursor by creating an `~/.icons/default/index.theme` file: if you edited that file manually, LXAppearance will overwrite it. Remember to also edit `~/.config/gtk-3.0/settings.ini` manually as specified in [#XDG specification](#XDG_specification), because applications like Firefox use this setting instead.

### Desktop environments

[Desktop environments](/index.php/Desktop_environments "Desktop environments") use the [XSETTINGS protocol](http://standards.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html), typically implemented through a settings daemon. While this allows to change the cursor on-the-fly, the applied theme may be inconsistent across applications. See [#XDG specification](#XDG_specification) to change the cursor theme manually.

#### GNOME

To change the theme in [GNOME](/index.php/GNOME "GNOME"), use [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks) or set the configuration directly with:

```
gsettings set org.gnome.desktop.interface cursor-theme *cursor_theme_name*

```

Change the cursor size with (depending on the theme, sizes are 24, 32, 48, 64):

```
gsettings set org.gnome.desktop.interface cursor-size *cursor_theme_size*

```

#### MATE

In MATE one can use mate-control-center or gsettings. To change the theme:

```
gsettings set org.mate.peripherals-mouse cursor-theme *cursor_theme_name*

```

To change the size:

```
gsettings set org.mate.peripherals-mouse *theme-size*

```

#### XFCE

To change the xcursor theme, use:

```
xfconf-query --channel xsettings --property /Gtk/CursorThemeName --set *cursor_theme_name*

```

To change the size:

```
xfconf-query --channel xsettings --property /Gtk/CursorThemeSize --set *cursor_theme_size*

```

### X resources

To locally name a cursor theme, add to the `~/.Xresources` file:

```
Xcursor.theme: cursor-theme

```

To have the cursor theme properly loaded it will need to be done so by the window manager; if it does not, it can be forced to load prior the window manager by putting the following command in `~/.xinitrc` or [.xprofile](/index.php/.xprofile ".xprofile") (depending on ones personal setup):

```
$ xrdb ~/.Xresources

```

Optionally, add this line to `~/.Xresources` if your cursor theme supports multiple sizes:

```
Xcursor.size: 16

```

**Tip:** 32, 48 or 64 may also be good size.

If in doubt over supported cursor sizes, start X without this setting and let it choose the cursor size automatically. (Refer to your window manager documentation for details.)

### Environment variable

You can use an [environment variable](/index.php/Environment_variable "Environment variable") to set a theme for a single application to try it out temporarily, for example:

```
$ XCURSOR_THEME=SomeThemeName xclock

```

XCURSOR_SIZE is optional if your cursor theme supports multiple sizes.

### Display managers

Cursor theme can usually be set within a display manager, but keep in mind the cursor theme may not carry over to the user session.

#### GDM

See [GDM#Changing the cursor theme](/index.php/GDM#Changing_the_cursor_theme "GDM").

## Troubleshooting

### Create links to missing cursors

Applications may keep using the default cursors when a theme lacks some cursors. This can be corrected by adding links to the missing cursors. For example:

```
$ cd ~/.icons/*theme*/cursors/
$ ln -s right_ptr arrow
$ ln -s cross crosshair
$ ln -s right_ptr draft_large
$ ln -s right_ptr draft_small
$ ln -s cross plus
$ ln -s left_ptr top_left_arrow
$ ln -s cross tcross
$ ln -s hand hand1
$ ln -s hand hand2
$ ln -s left_side left_tee
$ ln -s left_ptr ul_angle
$ ln -s left_ptr ur_angle
$ ln -s left_ptr_watch 08e8e1c95fe2fc01f976f1e063a24ccd

```

If the above does not solve the problem, look in `/usr/share/icons/whiteglass/cursors` for additional cursors your theme may be missing, and create links for these as well.

**Tip:** You can also remove unwanted cursors. To for example remove the "watch" cursor:
```
$ cd ~/.icons/*theme*/cursors/
$ rm watch left_ptr_watch
$ ln -s left_ptr watch
$ ln -s left_ptr left_ptr_watch

```

### Supplying missing cursors

Some programs set their own custom cursors which you may want to override. A common example of this is rdesktop, which connects to a Microsoft Windows computer and uses the cursors obtained from the remote machine, which can often be difficult to see due to protocol limitations yielding poor conversion quality.

This can be resolved by replacing these cursors with ones from the same (or another) cursor theme. In order to do this, the **hash** of the image must be obtained. This is done by setting the `XCURSOR_DISCOVER` environment variable prior to launching the application that sets these cursors:

```
$ XCURSOR_DISCOVER=1 rdesktop ...

```

The first time (and only the first time) the cursor is set, some details will be displayed, like this:

```
Cursor image name: 24020000002800000528000084810000
...
Cursor image name: 7bf1cc07d310bf080118007e08fc30ff
...
Cursor hash 24020000002800000528000084810000 returns 0x0

```

When Xcursor looks for missing cursors, the search path includes `~/.icons/default/cursors` so this is where an image can be placed for Xcursor to find. First, create this directory if it does not already exist:

```
$ mkdir -p ~/.icons/default/cursors

```

Then link the hash to the target image. Here we are using the `left_ptr` image from the `Vanilla-DMZ` cursor theme:

```
$ ln -s /usr/share/icons/Vanilla-DMZ/cursors/left_ptr ~/.icons/default/cursors/24020000002800000528000084810000

```

The change will be visible as soon as the application is restarted. No special method of launching the application is required.

#### rdesktop

Here are some common Microsoft Windows cursors that rdesktop uses when connecting to a remote machine running Windows 7\. Unfortunately animated cursors are difficult to override as they are sent frame-by-frame, so one mapping will be needed for every frame!

```
$ ln -s /usr/share/icons/$THEME/cursors/xterm          ~/.icons/default/cursors/00000000017e000002fc000000000000
$ ln -s /usr/share/icons/$THEME/cursors/right_ptr      ~/.icons/default/cursors/00000093000010860000631100006609
$ ln -s /usr/share/icons/$THEME/cursors/plus           ~/.icons/default/cursors/01e00000201c00004038000080300000
$ ln -s /usr/share/icons/$THEME/cursors/left_ptr       ~/.icons/default/cursors/24020000002800000528000084810000
$ ln -s /usr/share/icons/$THEME/cursors/left_ptr_watch ~/.icons/default/cursors/6ce0180090108e0005814700a0021400
$ ln -s /usr/share/icons/$THEME/cursors/hand           ~/.icons/default/cursors/d2201000a2c622004385440041308800
$ ln -s /usr/share/icons/$THEME/cursors/watch          ~/.icons/default/cursors/fc618c00da110f0034fd0e004e082400

```

### Change X shaped default cursor

The default X shaped Xcursor appears in window managers that do not set the default cursor to left_ptr or in window managers using XCB (like [awesome](/index.php/Awesome "Awesome")) instead of Xlib.

To fix this simply add the following to your `~/.xinitrc` , xsession or window managers startup configuration if possible (for example bspwm's bspwmrc).

```
$ xsetroot -cursor_name left_ptr

```

The list of cursor styles is in [appendix B](https://tronche.com/gui/x/xlib/appendix/b/) of the X protocol.

### .Xdefaults

If you have conflicting cursors then it might be because a different cursor has been set in the `~/.Xdefaults` file.

## See also

*   [Xcursor(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xcursor.3) — For more information about cursors in X (supported directories, formats, compatibility, etc.).