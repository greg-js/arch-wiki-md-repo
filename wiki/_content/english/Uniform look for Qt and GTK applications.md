[Qt](/index.php/Qt "Qt") and [GTK+](/index.php/GTK%2B "GTK+") based programs both use a different widget toolkit to render the graphical user interface. Each come with different themes, styles and icon sets by default, among other things, so the "look and feel" differ significantly. This article will help you make your Qt and GTK+ applications look similar for a more streamlined and integrated desktop experience.

## Contents

*   [1 Overview](#Overview)
*   [2 Styles for both Qt and GTK+](#Styles_for_both_Qt_and_GTK.2B)
    *   [2.1 Breeze](#Breeze)
    *   [2.2 Adwaita](#Adwaita)
*   [3 Theme engines](#Theme_engines)
    *   [3.1 QGtkStyle](#QGtkStyle)
    *   [3.2 QGnomePlatform](#QGnomePlatform)
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

*   Modify [GTK+ and Qt styles](#Styles_for_both_Qt_and_GTK.2B) separately with the tools listed below for each toolkit and aim for choosing similarly looking themes (style, colors, icons, cursors, fonts).
*   Use a special [theme engine](#Theme_engines), which intermediates the modification of the other graphical toolkit to match your main toolkit.

## Styles for both Qt and GTK+

There are widget style sets available for the purpose of integration, where builds are written and provided for both Qt and GTK+, all major versions included. With these, you can have one look for all applications regardless of the toolkit they had been written with.

**Tip:** You may want to apply user defined styles to root applications, see [GTK#Theme not applied to root applications](/index.php/GTK#Theme_not_applied_to_root_applications "GTK") and [Qt#Theme not applied to root applications](/index.php/Qt#Theme_not_applied_to_root_applications "Qt").

**Note:** Since version 3.16, GTK+ 3 [does not support](https://bbs.archlinux.org/viewtopic.php?pid=1518404#p1518404) non-CSS themes, hence previous solutions such as Oxygen-Gtk are [no longer viable](https://bugs.kde.org/show_bug.cgi?id=340288) options.

### Breeze

Breeze is the default Qt style of KDE Plasma. It can be installed with the [breeze](https://www.archlinux.org/packages/?name=breeze) package for Qt5, the [breeze-kde4](https://www.archlinux.org/packages/?name=breeze-kde4) package for Qt4, and the [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) package for GTK+ 2 and GTK+ 3.

Once installed, you can use one of the many [GTK+ configuration tools](/index.php/GTK%2B#Configuration_tools "GTK+") to change the GTK+ theme.

### Adwaita

Adwaita is the default GNOME theme. The GTK+ 3 version is included in the [gtk3](https://www.archlinux.org/packages/?name=gtk3) package, while the GTK+ 2 version is in [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard). [adwaita-qt](https://github.com/MartinBriza/adwaita-qt) is a Qt port of the Adwaita theme. Unlike [#QGtkStyle](#QGtkStyle), which mimics the GTK+ 2 theme, it provides a native Qt style made to look like the GTK+ 3 Adwaita. It can be [installed](/index.php/Install "Install") with the [adwaita-qt4](https://aur.archlinux.org/packages/adwaita-qt4/) and [adwaita-qt5](https://aur.archlinux.org/packages/adwaita-qt5/) packages for the Qt 4 and 5 versions, respectively.

To set the Qt style as default:

*   For Qt4, it can be enabled with *Qt Configuration* (`qtconfig-qt4`), choose *adwaita* under *Appearance > GUI Style*. Alternatively, edit the `/etc/xdg/Trolltech.conf` (system-wide) or `~/.config/Trolltech.conf` (user-specific) file:

 `~/.config/Trolltech.conf` 
```
...
[Qt]
style=adwaita
...
```

*   For Qt 5, it can be enabled by setting the following [environment variable](/index.php/Environment_variables#Graphical_applications "Environment variables"): `QT_STYLE_OVERRIDE=adwaita`.

## Theme engines

A *theme engine* can be thought of as a thin layer API which translates themes (excluding icons) between one or more toolkits. These engines add some extra code in the process and it is arguable that this kind of a solution is not as elegant and optimal as using native styles.

### QGtkStyle

**Note:** QGtkStyle has been removed from [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) 5.7.0 [[1]](https://github.com/qtproject/qtbase/commit/899a815414e95da8d9429a4a4f4d7094e49cfc55) and added to [qt5-styleplugins](https://aur.archlinux.org/packages/qt5-styleplugins/) [[2]](https://github.com/qtproject/qtstyleplugins/commit/102da7d50231fc5723dba6e72340bef3d29471aa)

**Warning:** Depending on GTK+ 2 theme, this style may cause rendering issues such as transparent fonts or inconsistent widgets.

This Qt style uses GTK+ 2 to render all components to blend in with [GNOME](/index.php/GNOME "GNOME") and similar GTK+ based environments. Beginning with Qt 4.5, this style is included in Qt. It requires [gtk2](https://www.archlinux.org/packages/?name=gtk2) to be installed and configured.

This is the default Qt4 style in Cinnamon, GNOME and Xfce, and the default Qt5 style in Cinnamon, GNOME, MATE, LXDE and Xfce. In other environments:

*   For Qt4, it can be enabled with *Qt Configuration* (`qtconfig-qt4`), choose *GTK+* under *Appearance > GUI Style*. Alternatively, edit the `/etc/xdg/Trolltech.conf` (system-wide) or `~/.config/Trolltech.conf` (user-specific) file:

 `~/.config/Trolltech.conf` 
```
...
[Qt]
style=GTK+
...
```

*   For Qt 5, it can be enabled by installing [qt5-styleplugins](https://aur.archlinux.org/packages/qt5-styleplugins/) and setting the following [environment variable](/index.php/Environment_variables#Graphical_applications "Environment variables"): `QT_QPA_PLATFORMTHEME='gtk2'`

For full uniformity, make sure that the configured [GTK+ theme](/index.php/GTK%2B#Themes "GTK+") supports both GTK+ 2 and GTK+ 3.

### QGnomePlatform

This Qt 5 platform theme applies the appearance settings of GNOME for Qt applications. It can be installed with the [qgnomeplatform-git](https://aur.archlinux.org/packages/qgnomeplatform-git/) package. It does not provide a Qt style itself, instead it requires a [style that support both Qt and GTK+](#Styles_for_both_Qt_and_GTK.2B).

This platform theme is enabled automatically in GNOME since version 3.20\. For other systems, it can be enabled by setting the following [environment variable](/index.php/Environment_variables#Graphical_applications "Environment variables"): `QT_QPA_PLATFORMTHEME=qgnomeplatform`.

## Tips and tricks

### KDE file dialogs for GTK+ applications

**Warning:** Some GTK+ applications may not be compatible with KGtk-wrapper (e.g. [Chromium](/index.php/Chromium "Chromium")), sometimes the wrapper makes the application crash (e.g. [Firefox](/index.php/Firefox "Firefox")) and even other applications like [KDM](/index.php/KDM "KDM") (when used with e.g. [Thunderbird](/index.php/Thunderbird "Thunderbird")).

[kgtk](https://aur.archlinux.org/packages/kgtk/) from the [AUR](/index.php/AUR "AUR") is a wrapper script which uses `LD_PRELOAD` to force KDE file dialogs in GTK+ 2.x apps. Once installed you can run GTK+ 2.x applications with `kgtk-wrapper` in two ways (using [GIMP](/index.php/GIMP "GIMP") in the examples):

*   Calling `kgtk-wrapper` directly and using the GTK+ 2.x binary as an argument:

	 `$ /usr/bin/kgtk-wrapper gimp` 

*   Modifying the KDE .desktop shortcuts files you can find at `/usr/share/applications/` to prefix the `Exec` statement with kgtk-wrapper.

	e.g. with [GIMP](/index.php/GIMP "GIMP"), edit the `/usr/share/applications/gimp.desktop` shortcut file and replace `Exec=gimp-2.8 %U` by `Exec=kgtk-wrapper gimp-2.8 %U`.

### Using a GTK+ icon theme in Qt apps

If you are running Plasma, install [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config) and select the icon-theme under *System Settings > Application Style > GTK*.

If you are using [GNOME](/index.php/GNOME "GNOME"), first check if [dconf-editor](https://www.archlinux.org/packages/?name=dconf-editor) is installed.

Then, run `dconf-editor` and look under *org > gnome > desktop > interface* for `icon-theme` key and change it to your preferred icon theme.

If you are not using [GNOME](/index.php/GNOME "GNOME"), for example if you are running a minimal system with [i3-wm](https://www.archlinux.org/packages/?name=i3-wm), first install [dconf-editor](https://www.archlinux.org/packages/?name=dconf-editor).

Then, run `dconf-editor` and look under *org > gnome > desktop > interface* for `icon-theme` key and change it to your preferred icon theme.

Since, you are not using [GNOME](/index.php/GNOME "GNOME"), you might have to set the value of `DESKTOP_SESSION` in your profile. To do that execute the below code in a terminal and restart your system.

```
$ echo 'export DESKTOP_SESSION=gnome' >> /etc/profile

```

**OR**

Set `export DESKTOP_SESSION=gnome` somewhere in your `~/.xinitrc` or, if you are using a [Display manager](/index.php/Display_manager "Display manager") in [Xprofile](/index.php/Xprofile "Xprofile").

**Note:** If the icon theme was not applied, you might want to check if the name that you entered of your preferred theme, was in the correct format. For example, if you want to apply the currently active icon theme to your QT applications, you can find the correct format of it's name with the command:- `cat /home/$USER/.gtkrc-2.0 ` 

### Improve subpixel rendering of GTK apps under KDE Plasma

See [Font configuration#LCD filter](/index.php/Font_configuration#LCD_filter "Font configuration").

## Troubleshooting

### Qt applications do not use QGtkStyle

Qt will not apply QGtkStyle correctly if GTK+ is using the [GTK+-Qt Engine](#GTK.2B-Qt_Engine). Qt determines whether the GTK+-Qt Engine is in use by reading the GTK+ configuration files listed in the environmental variable `GTK2_RC_FILES`. If the environmental variable is not set properly, Qt assumes you are using the engine, sets QGtkStyle to use the style GTK+ style *Clearlooks*, and outputs an error message:

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

Newer versions of [gtk-qt-engine](https://aur.archlinux.org/packages/gtk-qt-engine/) use `~/.gtkrc2.0-kde` and set the export variable in `~/.kde/env/gtk-qt-engine.rc.sh`. If you recently removed **gtk-qt-engine** and are trying to set a GTK+ theme then you must also remove `~/.kde/env/gtk-qt-engine.rc.sh` and reboot. Doing this will ensure that GTK+ looks for its settings in the standard `~/.gtkrc2.0` instead of the `~/.gtkrc2.0-kde` file.