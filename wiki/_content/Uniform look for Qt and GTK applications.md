# Uniform look for Qt and GTK applications

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [GTK+](/index.php/GTK%2B "GTK+")
*   [Qt](/index.php/Qt "Qt")

[Qt](/index.php/Qt "Qt") and [GTK+](/index.php/GTK%2B "GTK+") based programs both use a different widget toolkit to render the graphical user interface. Each come with different themes, styles and icon sets by default, among other things, so the "look and feel" differ significantly. This article will help you make your Qt and GTK+ applications look similar for a more streamlined and integrated desktop experience.

## Contents

*   [1 Overview](#Overview)
*   [2 Theme engines](#Theme_engines)
    *   [2.1 QGtkStyle](#QGtkStyle)
*   [3 Styles for both Qt and GTK+](#Styles_for_both_Qt_and_GTK.2B)
    *   [3.1 Breeze](#Breeze)
    *   [3.2 Adwaita](#Adwaita)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 KDE file dialogs for GTK+ applications](#KDE_file_dialogs_for_GTK.2B_applications)
    *   [4.2 Using a GTK+ icon theme in Qt apps](#Using_a_GTK.2B_icon_theme_in_Qt_apps)
    *   [4.3 Improve subpixel rendering of GTK apps under KDE Plasma](#Improve_subpixel_rendering_of_GTK_apps_under_KDE_Plasma)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Qt applications do not use QGtkStyle](#Qt_applications_do_not_use_QGtkStyle)
    *   [5.2 Themes not working in GTK+ apps](#Themes_not_working_in_GTK.2B_apps)

## Overview

To get a similar look between the toolkits, you will most likely have to modify the following:

*   **Theme**: The custom appearance of an application, widget set, etc. It usually consists of a style, an icon theme and a color theme.
*   **Style**: The graphical layout and look of the widget set.
*   **Icon Theme**: A set of global icons.
*   **Color Theme**: A set of global colors that are used in conjunction with the style.

You can choose various approaches:

*   Use a special [theme engine](#Theme_engines), which intermediates the modification of the other graphical toolkit to match your main toolkit.
*   Modify [GTK+ and Qt styles](#Styles_for_both_Qt_and_GTK.2B) separately with the tools listed below for each toolkit and aim for choosing similarly looking themes (style, colors, icons, cursors, fonts).

## Theme engines

A _theme engine_ can be thought of as a thin layer API which translates themes (excluding icons) between one or more toolkits. These engines add some extra code in the process and it is arguable that this kind of a solution is not as elegant and optimal as using native styles.

### QGtkStyle

**Warning:** Depending on GTK+ 2 theme, this style may cause rendering issues such as transparent fonts or inconsistent widgets.

This Qt style uses GTK+ 2 to render all components to blend in with [GNOME](/index.php/GNOME "GNOME") and similar GTK+ based environments. Beginning with Qt 4.5, this style is included in Qt. It requires [gtk2](https://www.archlinux.org/packages/?name=gtk2) to be installed and configured.

This is the default Qt4 style in Cinnamon, GNOME and Xfce, and the default Qt5 style in Cinnamon, GNOME, MATE, LXDE and Xfce. In other environments:

*   For Qt4, it can be enabled with _Qt Configuration_ (`qtconfig-qt4`), choose _GTK+_ under _Appearance > GUI Style_. Alternatively, edit the `/etc/xdg/Trolltech.conf` (system-wide) or `~/.config/Trolltech.conf` (user-specific) file:

 `~/.config/Trolltech.conf` 

```
...
[Qt]
style=GTK+
...
```

*   For Qt 5, it can be enabled by setting the following [environment variable](/index.php/Environment_variables#Graphical_applications "Environment variables"): `QT_STYLE_OVERRIDE=GTK+`.

For full uniformity, make sure that the configured [GTK+ theme](/index.php/GTK%2B#Themes "GTK+") supports both GTK+ 2 and GTK+ 3.

## Styles for both Qt and GTK+

There are widget style sets available for the purpose of integration, where builds are written and provided for both Qt and GTK+, all major versions included. With these, you can have one look for all applications regardless of the toolkit they had been written with.

**Note:** Since version 3.16, GTK+ 3 [does not support](https://bbs.archlinux.org/viewtopic.php?pid=1518404#p1518404) non-CSS themes, hence previous solutions such as Oxygen-Gtk are [no longer viable](https://bugs.kde.org/show_bug.cgi?id=340288) options.

### Breeze

Breeze is the default Qt style of KDE Plasma. It can be installed with the [breeze](https://www.archlinux.org/packages/?name=breeze) package for Qt5, the [breeze-kde4](https://www.archlinux.org/packages/?name=breeze-kde4) package for Qt4, and the [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) package for GTK+ 2 and GTK+ 3.

Once installed, you can use one of the many [GTK+ configuration tools](/index.php/GTK%2B#Configuration_tools "GTK+") to change the GTK+ theme.

### Adwaita

Adwaita is the default GNOME theme. It can be installed with the [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard) package, which contains the GTK+ 2 and 3 themes. [adwaita-qt](https://github.com/MartinBriza/adwaita-qt) is an unofficial Qt port of the Adwaita theme. Unlike [#QGtkStyle](#QGtkStyle), which mimic the GTK+ 2 theme, it provides a native Qt style made to look like the GTK+ 3 Adwaita. It can be [installed](/index.php/Install "Install") with the [adwaita-qt5](https://aur.archlinux.org/packages/adwaita-qt5/)<sup><small>AUR</small></sup> package for the Qt5 version, and [adwaita-qt4](https://aur.archlinux.org/packages/adwaita-qt4/)<sup><small>AUR</small></sup> for the Qt 4 version.

To set it as default, you can use [qt5ct](https://www.archlinux.org/packages/?name=qt5ct) for Qt 5, or `qtconfig-qt4` (part of the [qt4](https://www.archlinux.org/packages/?name=qt4) package) for Qt 4.

## Tips and tricks

### KDE file dialogs for GTK+ applications

**Warning:** Some GTK+ applications may not be compatible with KGtk-wrapper (e.g. [Chromium](/index.php/Chromium "Chromium")), sometimes the wrapper makes the application crash (e.g. [Firefox](/index.php/Firefox "Firefox")) and even other applications like [KDM](/index.php/KDM "KDM") (when used with e.g. [Thunderbird](/index.php/Thunderbird "Thunderbird")).

[kgtk](https://aur.archlinux.org/packages/kgtk/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR") is a wrapper script which uses `LD_PRELOAD` to force KDE file dialogs in GTK+ 2.x apps. Once installed you can run GTK+ 2.x applications with `kgtk-wrapper` in two ways (using [Gimp](/index.php/Gimp "Gimp") in the examples):

*   Calling `kgtk-wrapper` directly and using the GTK+ 2.x binary as an argument:

 `$ /usr/bin/kgtk-wrapper gimp` 

*   Modifying the KDE .desktop shortcuts files you can find at `/usr/share/applications/` to prefix the `Exec` statement with kgtk-wrapper.

e.g. with [GIMP](/index.php/GIMP "GIMP"), edit the `/usr/share/applications/gimp.desktop` shortcut file and replace `Exec=gimp-2.8 %U` by `Exec=kgtk-wrapper gimp-2.8 %U`.

### Using a GTK+ icon theme in Qt apps

If you are not using GNOME, run `gconf-editor`, look under _desktop > gnome > interface_ for the `icon_theme` key and change it to your preference. As you are not using GNOME, it is possible that you will have to set `export DESKTOP_SESSION=gnome` somewhere in your `~/.xinitrc` or, if you are using [LightDM](/index.php/LightDM "LightDM"), in `/etc/environment`.

### Improve subpixel rendering of GTK apps under KDE Plasma

See [Font configuration#LCD filter](/index.php/Font_configuration#LCD_filter "Font configuration").

## Troubleshooting

### Qt applications do not use QGtkStyle

Qt will not apply QGtkStyle correctly if GTK+ is using the [GTK+-Qt Engine](#GTK.2B-Qt_Engine). Qt determines whether the GTK+-Qt Engine is in use by reading the GTK+ configuration files listed in the environmental variable `GTK2_RC_FILES`. If the environmental variable is not set properly, Qt assumes you are using the engine, sets QGtkStyle to use the style GTK+ style _Clearlooks_, and outputs an error message:

```
QGtkStyle cannot be used together with the GTK_Qt engine.

```

Another error you may get after launching `qtconfig-qt4` from a shell and selecting the GTK+ style is:

```
QGtkStyle was unable to detect the current GTK+ theme.

```

According to [this thread](https://bbs.archlinux.org/viewtopic.php?id=99175&p=1), you may simply have to install [libgnomeui](https://www.archlinux.org/packages/?name=libgnomeui) to solve this issue. This has the added benefit that you do not need to edit a file every time you change your theme via a graphical tool, like the one provided by xfce.

Users of [Openbox](/index.php/Openbox "Openbox") and other non-GNOME environments may encounter this problem. To solve this, first add the following to your `.xinitrc` file:

 `.xinitrc` 

```
...
export GTK2_RC_FILES="$HOME/.gtkrc-2.0"
...

```

**Note:**

*   Make sure to add this line before invoking the window manager.
*   You can add multiple paths by separating them with colons.
*   Make sure to use `$HOME` instead of `~` as it will not properly expand to the user's home directory.

Then specify the theme you want in the `~/.gtkrc-2.0` file using a [dedicated application](#GTK2_styles) or manually, by adding:

 `.gtkrc-2.0` 

```
...
gtk-theme-name="[name of theme]"
...

```

Some tools only insert the following include directive in `~/.gtkrc-2.0`:

 `.gtkrc-2.0` 

```
...
include "/usr/share/themes/SomeTheme/gtk-2.0/gtkrc"
...

```

which apparently is not recognized by all versions of QGtkStyle. You can hotfix this problem by inserting the `gtk-theme-name` manually in your `~/.gtkrc-2.0` file like above.

**Note:** Style-changing applications will most probably rewrite the `~/.gtkrc-2.0` file the next time you change themes.

If these steps do not work, install [gconf](https://www.archlinux.org/packages/?name=gconf) and run this command:

```
gconftool-2 --set --type string /desktop/gnome/interface/gtk_theme [name of theme]

```

If you further want to set the same icon and cursor theme, then you have to specify them, too.

```
gconftool-2 --set --type string /desktop/gnome/interface/icon_theme Faenza-Dark

```

This sets the icon theme to Faenza-Dark located in `/usr/share/icons/Faenza-Dark`. For the cursor theme you first have to set the gconf value.

```
gconftool-2 --set --type string /desktop/gnome/peripherals/mouse/cursor_theme Adwaita

```

Then you will have to create the file `/usr/share/icons/default/index.theme` with the following lines:

```
[Icon Theme]
Inherits=Adwaita

```

### Themes not working in GTK+ apps

If the style or theme engine you set up is not showing in your GTK applications then it is likely your GTK+ settings files are not being loaded for some reason. You can check where your system expects to find these files by doing the following..

```
$ export | grep gtk

```

Usually the expected files should be `~/.gtkrc` for GTK1 and `~/.gtkrc2.0` or `~/.gtkrc2.0-kde` for GTK+ 2.x.

Newer versions of [gtk-qt-engine](https://aur.archlinux.org/packages/gtk-qt-engine/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gtk-qt-engine)]</sup> use `~/.gtkrc2.0-kde` and set the export variable in `~/.kde/env/gtk-qt-engine.rc.sh`. If you recently removed **gtk-qt-engine** and are trying to set a GTK+ theme then you must also remove `~/.kde/env/gtk-qt-engine.rc.sh` and reboot. Doing this will ensure that GTK+ looks for its settings in the standard `~/.gtkrc2.0` instead of the `~/.gtkrc2.0-kde` file.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Uniform_look_for_Qt_and_GTK_applications&oldid=411917](https://wiki.archlinux.org/index.php?title=Uniform_look_for_Qt_and_GTK_applications&oldid=411917)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Widget toolkits](/index.php/Category:Widget_toolkits "Category:Widget toolkits")
*   [Eye candy](/index.php/Category:Eye_candy "Category:Eye candy")