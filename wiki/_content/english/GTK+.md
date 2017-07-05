From the [GTK+ website](http://www.gtk.org):

	GTK+, or the GIMP Toolkit, is a multi-platform toolkit for creating graphical user interfaces. Offering a complete set of widgets, GTK+ is suitable for projects ranging from small one-off tools to complete application suites.

GTK+, The GIMP Toolkit, was initially made by the [GNU Project](/index.php/GNU_Project "GNU Project") for the [GIMP](/index.php/GIMP "GIMP") but is now a very popular toolkit with bindings for many languages. This article will explore the tools used to configure the GTK+ theme, style, icon, font and font size, and also detail manual configuration.

## Contents

*   [1 Installation](#Installation)
*   [2 Themes](#Themes)
    *   [2.1 GTK+ and Qt](#GTK.2B_and_Qt)
*   [3 Configuration tools](#Configuration_tools)
*   [4 Configuration](#Configuration)
    *   [4.1 Basic theme configuration](#Basic_theme_configuration)
    *   [4.2 Dark theme variant](#Dark_theme_variant)
    *   [4.3 Keyboard shortcuts](#Keyboard_shortcuts)
        *   [4.3.1 Emacs keybindings](#Emacs_keybindings)
    *   [4.4 GNOME menu delay](#GNOME_menu_delay)
    *   [4.5 Reduce widget sizes](#Reduce_widget_sizes)
    *   [4.6 File-Chooser Startup-Location](#File-Chooser_Startup-Location)
    *   [4.7 Legacy scrolling behavior](#Legacy_scrolling_behavior)
    *   [4.8 Disable overlay scrollbars](#Disable_overlay_scrollbars)
        *   [4.8.1 Remove overlay scroll indicators](#Remove_overlay_scroll_indicators)
*   [5 GDK backends](#GDK_backends)
    *   [5.1 Broadway backend](#Broadway_backend)
    *   [5.2 Wayland backend](#Wayland_backend)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Different themes between GTK+ 2 and GTK+ 3 applications](#Different_themes_between_GTK.2B_2_and_GTK.2B_3_applications)
    *   [6.2 Theme not applied to root applications](#Theme_not_applied_to_root_applications)
    *   [6.3 Client-side decorations](#Client-side_decorations)
    *   [6.4 cedilla ç/Ç instead of ć/Ć](#cedilla_.C3.A7.2F.C3.87_instead_of_.C4.87.2F.C4.86)
    *   [6.5 Suppress warning about accessibility bus](#Suppress_warning_about_accessibility_bus)
    *   [6.6 Titlebar background color mismatch](#Titlebar_background_color_mismatch)
    *   [6.7 Wrong focus events with tiling window managers](#Wrong_focus_events_with_tiling_window_managers)
    *   [6.8 Thumbnail support for GTK+ 2 file dialog](#Thumbnail_support_for_GTK.2B_2_file_dialog)
    *   [6.9 Button/menu icons in some apps in GNOME Wayland session](#Button.2Fmenu_icons_in_some_apps_in_GNOME_Wayland_session)
    *   [6.10 Printers not shown in the GTK print dialog](#Printers_not_shown_in_the_GTK_print_dialog)
    *   [6.11 Some GTK+ 2 themes only change the UI color palette](#Some_GTK.2B_2_themes_only_change_the_UI_color_palette)
*   [7 Examples](#Examples)
*   [8 See also](#See_also)

## Installation

Two versions of GTK+ are currently available in the [official repositories](/index.php/Official_repositories "Official repositories"). They can be [installed](/index.php/Install "Install") with the following packages:

*   **GTK+ 3.x** is available with the [gtk3](https://www.archlinux.org/packages/?name=gtk3) package.
*   **GTK+ 2.x** is available with the [gtk2](https://www.archlinux.org/packages/?name=gtk2) package.
*   **GTK+ 1.x** is available with the [gtk](https://aur.archlinux.org/packages/gtk/) package.

## Themes

In GTK+ 2, the default theme is *Raleigh*, but Arch Linux has a custom configuration file at `/usr/share/gtk-2.0/gtkrc`, which sets the default theme to *Adwaita*. In GTK+ 3, the default theme is *Adwaita*, but *HighContrast*, *HighContrastInverse* and *Raleigh* themes are also included.

To force a specific theme, you can set environment variables.

*   For GTK+ 2, use the `GTK2_RC_FILES` environment variable, for example:

```
$ GTK2_RC_FILES=/usr/share/themes/Industrial/gtk-2.0/gtkrc gimp

```

	will launch GIMP with the Industrial theme.

*   For GTK+ 3, use the `GTK_THEME` environment variable, for example:

```
$ GTK_THEME=Adwaita:dark gnome-calculator

```

	will launch GNOME Calculator with the dark variant of Adwaita theme.

More themes can be installed from the official repositories or the [AUR](/index.php/AUR "AUR").

**GTK+ 2 and GTK+ 3.20 or newer are supported:**

*   **Adapta** — An adaptive Gtk+ theme based on Material Design Guidelines. Includes: *Adapta*, *Adapta-Eta*, *Adapta-Nokto*, *Adapta-Nokto-Eta*

	[https://github.com/tista500/Adapta](https://github.com/tista500/Adapta) || [adapta-gtk-theme](https://www.archlinux.org/packages/?name=adapta-gtk-theme)

*   **Arc** — A flat theme with a modern look and transparent elements. Includes: *Arc*, *Arc-Dark*, *Arc-Darker*

	[https://github.com/horst3180/arc-theme](https://github.com/horst3180/arc-theme) || with transparency: [arc-gtk-theme](https://www.archlinux.org/packages/?name=arc-gtk-theme), without transparency: [arc-solid-gtk-theme](https://www.archlinux.org/packages/?name=arc-solid-gtk-theme)

*   **Breeze** — GTK+ version of KDE's default widget theme. Includes: *Breeze*, *Breeze-Dark*

	[https://cgit.kde.org/breeze-gtk.git](https://cgit.kde.org/breeze-gtk.git) || [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk)

*   **Deepin** — Default theme for the Deepin desktop. Includes: *deepin*, *deepin-dark*

	[https://github.com/linuxdeepin/deepin-gtk-theme](https://github.com/linuxdeepin/deepin-gtk-theme) || [deepin-gtk-theme](https://www.archlinux.org/packages/?name=deepin-gtk-theme)

*   **GNOME Standard Themes** — Default themes for the GNOME desktop. Includes: *Adwaita*, *Adwaita-dark*, *HighContrast*

	[https://github.com/GNOME/gnome-themes-standard](https://github.com/GNOME/gnome-themes-standard) || [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard)

*   **MATE Themes** — Default themes for the MATE desktop. Includes: *BlackMATE*, *Blue-Submarine*, *BlueMenta*, *ContrastHighInverse*, *Green-Submarine*, *GreenLaguna*, *Menta*, *TraditionalGreen*, *TraditionalOk*

	[https://github.com/mate-desktop/mate-themes](https://github.com/mate-desktop/mate-themes) || [mate-themes](https://www.archlinux.org/packages/?name=mate-themes)

*   **Numix** — A flat and light theme with a modern look (GNOME, Openbox, Unity, Xfce). Includes: *Numix*

	[https://github.com/shimmerproject/Numix](https://github.com/shimmerproject/Numix) || [numix-gtk-theme](https://www.archlinux.org/packages/?name=numix-gtk-theme)

*   **Blackbird** — Dark Desktop Suite for Xfce.

	[https://github.com/shimmerproject/Blackbird](https://github.com/shimmerproject/Blackbird) || [xfce-theme-blackbird](https://aur.archlinux.org/packages/xfce-theme-blackbird/)

*   **Flat-Plat** — A Material Design-like flat theme for GTK3, GTK2, and GNOME-Shell.

	[https://github.com/nana-4/Flat-Plat](https://github.com/nana-4/Flat-Plat) || [flatplat-theme-git](https://aur.archlinux.org/packages/flatplat-theme-git/)

*   **Gnome-breeze** — A GTK theme created to match with the new Plasma 5 Breeze.

	[https://github.com/dirruk1/gnome-breeze](https://github.com/dirruk1/gnome-breeze) || [gnome-breeze-git](https://aur.archlinux.org/packages/gnome-breeze-git/)

*   **Greybird** — A grey and blue Xfce theme, used by default in Xubuntu 12.04.

	[https://github.com/shimmerproject/Greybird](https://github.com/shimmerproject/Greybird) || [xfce-theme-greybird](https://aur.archlinux.org/packages/xfce-theme-greybird/)

*   **Vertex** — Theme for GTK 3, GTK 2, Gnome-Shell and Cinnamon.

	[https://github.com/horst3180/vertex-theme](https://github.com/horst3180/vertex-theme) || [vertex-themes](https://aur.archlinux.org/packages/vertex-themes/)

*   **Zuki** — Themes for GTK, gnome-shell and more.

	[https://github.com/lassekongo83/zuki-themes](https://github.com/lassekongo83/zuki-themes) || [zuki-themes-git](https://aur.archlinux.org/packages/zuki-themes-git/)

**Only GTK+ 2 is supported:**

*   **GTK+ Engines** — Theme engines for GTK+ 2\. Includes: *Clearlooks*, *Crux*, *Industrial*, *Mist*, *Redmond*, *ThinIce*

	[https://github.com/GNOME/gtk-engines](https://github.com/GNOME/gtk-engines) || [gtk-engines](https://www.archlinux.org/packages/?name=gtk-engines)

*   **Xfce Gtk+ Engine** — Xfce Gtk+-2.0 engine and themes

	[http://git.xfce.org/xfce/gtk-xfce-engine/](http://git.xfce.org/xfce/gtk-xfce-engine/) || [gtk-xfce-engine](https://www.archlinux.org/packages/?name=gtk-xfce-engine)

*   **Oxygen-Gtk** — Port of the default KDE widget theme (Oxygen) to GTK2

	[https://cgit.kde.org/oxygen-gtk.git](https://cgit.kde.org/oxygen-gtk.git) || [oxygen-gtk2](https://www.archlinux.org/packages/?name=oxygen-gtk2)

*   **Aurora Gtk Engine** — Latest member of the Clearlooks family.

	[http://gnome-look.org/content/show.php/Aurora+Gtk+Engine?content=56438](http://gnome-look.org/content/show.php/Aurora+Gtk+Engine?content=56438) || [gtk-engine-aurora](https://www.archlinux.org/packages/?name=gtk-engine-aurora)

*   **QtCurve** — A configurable set of widget styles for KDE and Gtk.

	[https://cgit.kde.org/qtcurve.git](https://cgit.kde.org/qtcurve.git) || [qtcurve-gtk2](https://www.archlinux.org/packages/?name=qtcurve-gtk2)

There are a number of additional GTK+ themes in the [AUR](/index.php/AUR "AUR"): [search for gtk-theme](https://aur.archlinux.org/packages.php?K=gtk-theme), [search for gtk2-theme](https://aur.archlinux.org/packages.php?K=gtk2-theme).

**Note:** Because GTK+ 3 changes rapidly, GTK+ 3 themes often require re-working after a GTK+ 3 release. For this reason, not all GTK+ 3 themes may look as intended when used with the latest GTK+ 3 version.

### GTK+ and Qt

If you have GTK+ and Qt (KDE) applications on your desktop then you know that their looks do not blend well. If you wish to make your GTK+ styles match your Qt styles please read [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

## Configuration tools

Most major [desktop environments](/index.php/Desktop_environments "Desktop environments") provide tools to configure the GTK+ theme, icons, font and font size, and manage these settings via [XSettings](http://standards.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html):

*   If you use [Cinnamon](/index.php/Cinnamon "Cinnamon"), use Themes tool (*cinnamon-settings themes*): go to *System Settings > Themes*.
*   If you use [Enlightenment](/index.php/Enlightenment "Enlightenment"): go to *Settings > All > Look > Application Theme*.
*   If you use [GNOME](/index.php/GNOME "GNOME"), use GNOME Tweak Tool (*gnome-tweak-tool*): install [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool).
*   If you use [MATE](/index.php/MATE "MATE"), use the Appearance Preferences tool (*mate-appearance-properties*): go to *System > Settings > Appearance*.
*   If you use [Xfce](/index.php/Xfce "Xfce"), use the Appearance tool: go to *Settings > Appearance*.

Other GUI tools generally overwrite the [configuration files](#Configuration).

**Both GTK+ 2 and GTK+ 3 are supported:**

*   **KDE GTK Configurator** — Application that allows you to change style and font of GTK+ 2 and Gtk+ 3 applications.

	[https://cgit.kde.org/kde-gtk-config.git](https://cgit.kde.org/kde-gtk-config.git) || [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)

	After installation, `kde-gtk-config` can also be found in *System Settings > Application Style > GTK*.

*   **LXAppearance** — Desktop independent GTK+ 2 and GTK+ 3 style configuration tool from the LXDE project (it does not require other parts of the LXDE desktop).

	[http://wiki.lxde.org/en/LXAppearance](http://wiki.lxde.org/en/LXAppearance) || [lxappearance](https://www.archlinux.org/packages/?name=lxappearance)

*   **Oo-mox** — Graphical application for generating different color variations of Numix theme (GTK2, GTK3) and gnome-colors icon theme.

	[https://github.com/actionless/oomox](https://github.com/actionless/oomox) || [oomox](https://aur.archlinux.org/packages/oomox/)

**Only GTK+ 2 is supported:**

*   **GTK+ Change Theme** — Little program that lets you change your GTK+ 2.0 theme (considered a better alternative to *switch2*).

	[http://plasmasturm.org/code/gtk-chtheme/](http://plasmasturm.org/code/gtk-chtheme/) || [gtk-chtheme](https://www.archlinux.org/packages/?name=gtk-chtheme)

*   **GTK+ Preference Tool** — GTK+ theme selector and font switcher.

	[http://gtk-win.sourceforge.net/home/index.php/Main/GTKPreferenceTool](http://gtk-win.sourceforge.net/home/index.php/Main/GTKPreferenceTool) || [gtk2_prefs](https://www.archlinux.org/packages/?name=gtk2_prefs)

*   **GTK+ Theme Switch** — Simple GTK+ theme switcher.

	[http://muhri.net/nav.php3?node=gts](http://muhri.net/nav.php3?node=gts) || [gtk-theme-switch2](https://www.archlinux.org/packages/?name=gtk-theme-switch2)

## Configuration

GTK+ settings can be specified manually in configuration files, but desktop environments and applications can override these settings. Depending on GTK+ version, these files are located at:

*   GTK+ 2 user specific: `~/.gtkrc-2.0`
*   GTK+ 2 system wide: `/etc/gtk-2.0/gtkrc`
*   GTK+ 3 user specific: `$XDG_CONFIG_HOME/gtk-3.0/settings.ini`, or `$HOME/.config/gtk-3.0/settings.ini` if `$XDG_CONFIG_HOME` is not set
*   GTK+ 3 system wide: `/etc/gtk-3.0/settings.ini`

**Note:**

*   See the [GTK+ 3 *GtkSettings* properties](http://library.gnome.org/devel/gtk3/stable/GtkSettings.html#GtkSettings.properties) (and [GTK+ 2 properties](http://library.gnome.org/devel/gtk2/stable/GtkSettings.html#GtkSettings.properties)) in the GTK+ programming reference manual for the full list of currently supported GTK+ configuration options.
*   Some of the settings described below (such as `gtk-icon-sizes`) are deprecated and ignored since GTK+ 3.10.
*   If you edit your GTK+ configuration files, only newly started applications will display the changes.

### Basic theme configuration

To manually change the GTK+ theme, icons, font and font size, add the following to the configuration files, for example:

**GTK+ 2:**

 `~/.gtkrc-2.0` 
```
gtk-icon-theme-name = "Adwaita"
gtk-theme-name = "Adwaita"
gtk-font-name = "DejaVu Sans 11"
```

**GTK+ 3:**

 `$XDG_CONFIG_HOME/gtk-3.0/settings.ini` 
```
[Settings]
gtk-icon-theme-name = Adwaita
gtk-theme-name = Adwaita
gtk-font-name = DejaVu Sans 11
```

**Note:** The icon theme name is the name defined in the theme's index file, *not* the name of its directory.

### Dark theme variant

Some GTK+ 3 themes contain a dark theme variant, but it's only used by default when the application requests it explicitly. To use dark theme variant with all GTK+ 3 applications, set:

```
gtk-application-prefer-dark-theme = true

```

### Keyboard shortcuts

Keyboard shortcuts (otherwise known as *accelerators* in GTK+) may be changed by hovering the mouse over the respective menu item, and pressing the desired key combination. To enable this feature, set:

```
gtk-can-change-accels = 1

```

#### Emacs keybindings

To get Emacs-like keybindings in gtk apps:

For GTK2, add `gtk-key-theme-name = "Emacs"` to `~/.gtkrc-2.0`.

For GTK3 add the following to the noted file:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-key-theme-name = Emacs
```

Then run:

```
$ gsettings set org.gnome.desktop.interface gtk-key-theme "Emacs"

```

XFCE has a similar setting:

```
$ xfconf-query -c xsettings -p /Gtk/KeyThemeName -s Emacs

```

The config files in `/usr/share/themes/Emacs/` determine what the Emacs bindings are, and can be changed. Copying sections to the users `~/.gtkrc-2.0` file allows for changes on a per user basis.

### GNOME menu delay

This setting controls the delay between pointing the mouse at a menu and that menu opening. This delay is measured in milliseconds.

```
gtk-menu-popup-delay = 0

```

### Reduce widget sizes

If you have a small screen or you just do not like big icons and widgets, you can resize things easily.

To have icons without text in toolbars ([valid values](https://developer.gnome.org/gtk3/stable/gtk3-Standard-Enumerations.html#GtkToolbarStyle)), use

```
gtk-toolbar-style = GTK_TOOLBAR_ICONS

```

To use smaller icons, use a line like this:

```
gtk-icon-sizes = "panel-menu=16,16:panel=16,16:gtk-menu=16,16:gtk-large-toolbar=16,16\
:gtk-small-toolbar=16,16:gtk-button=16,16"

```

Or to remove icons from buttons completely:

```
gtk-button-images = 0

```

You can also remove icons from menus:

```
gtk-menu-images = 0

```

See also [[1]](http://martin.ankerl.com/2008/10/10/how-to-make-a-compact-gnome-theme/) and [[2]](http://gnome-look.org/content/show.php/Simple+eGTK?content=119812).

### File-Chooser Startup-Location

Open the file-chooser within the **current-working-directory** and not the **recent** location. Normally the **current-working-directory** is **home-directory**.

**GTK+ 3**

Modify DConf with *gsettings*, as the database file ($XDG_CONFIG_HOME/dconf/users) is binary:

```
$ gsettings set org.gtk.Settings.FileChooser startup-mode cwd

```

**GTK+ 2**

Modify `~/.config/gtk-2.0/gtkfilechooser.ini` configuration file:

 `~/.config/gtk-2.0/gtkfilechooser.ini`  `StartupMode=cwd` 

### Legacy scrolling behavior

**Note:** This setting is not obeyed by all GTK+ applications.

**Tip:** Legacy scrolling behaviour can be achieved reliably simply by using right click instead of left click.

Prior to GTK+ 3.6, clicking on either side of the slider in the scrollbar would move the scrollbar in the direction of the click by approximately one page. Since GTK+ 3.6, the slider will move directly to the position of the click. This behaviour can be reverted in some applications by creating the file with the content below:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-primary-button-warps-slider = false

```

### Disable overlay scrollbars

Since GTK+ 3.15, overlay scrollbars are enabled by default, meaning that scrollbars will be shown only on mouseover in GTK+ 3 applications. This behavior can be reverted by setting the following environment variable: `GTK_OVERLAY_SCROLLING=0`.

See [Environment variables#Graphical applications](/index.php/Environment_variables#Graphical_applications "Environment variables").

#### Remove overlay scroll indicators

The positions of the overlay scrollbars are indicated by thin dashed lines in the application window. These dashed lines will be present even when overlay scrolling is disabled using the environment variable discussed in the section above. To remove the indicator lines, create the following file:

 `~/.config/gtk-3.0/gtk.css` 
```
/* Remove dotted lines from GTK+ 3 applications */
undershoot.top, undershoot.right, undershoot.bottom, undershoot.left { background-image: none; }

```

## GDK backends

GDK (the underlying abstraction layer of GTK+) supports multiple backends to display GTK+ applications. The default backend is *x11*.

### Broadway backend

The GDK Broadway backend provides support for displaying GTK+ applications in a web browser, using HTML5 and web sockets. [[3]](https://developer.gnome.org/gtk3/3.8/gtk-broadway.html)

When using broadwayd, specify the display number to use, prefixed with a colon, similar to X. The default display number is 1.

```
$ display_number=:5

```

Start it.

```
$ broadwayd $display_number 

```

Port Used on default

```
port = 8080 + $display_number

```

Point your browser to [http://127.0.0.1:port](http://127.0.0.1:port)

To Start apps

```
$ GDK_BACKEND=broadway BROADWAY_DISPLAY=$display_number *<<app>>*

```

Alternatively can set address and port

```
$ broadwayd --port $port_number --address $address $display_number

```

### Wayland backend

The GDK [Wayland](/index.php/Wayland "Wayland") backend can be enabled by setting the `GDK_BACKEND=wayland` environment variable.

**Tip:** To disable GTK window decorations in Wayland, [install](/index.php/Install "Install") the [gtk3-optional-csd](https://aur.archlinux.org/packages/gtk3-optional-csd/) package and set the environment variable `GTK_CSD=0`.

## Troubleshooting

### Different themes between GTK+ 2 and GTK+ 3 applications

In general, if a selected theme has support for both GTK+ 2 and GTK+ 3, the theme will be applied to all GTK+ 2 and GTK+ 3 applications. If a selected theme has support for only GTK+ 2, it will be used for GTK+ 2 applications and the default GTK+ theme will be used for GTK+ 3 applications. If the selected theme has support for only GTK+ 3, it will be used for GTK+ 3 applications and the default GTK+ theme will be used for GTK+ 2 applications. Thus for application theme consistency, it is best to use a theme which has support for both GTK+ 2 and GTK+ 3.

You could find what themes installed on your system have both an GTK+ 2 and GTK+ 3 version by using this command (does not work with names containing spaces):

```
find $(find ~/.themes /usr/share/themes/ -wholename "*/gtk-3.0" | sed -e "s/^\(.*\)\/gtk-3.0$/\1/") -wholename "*/gtk-2.0" | sed -e "s/.*\/\(.*\)\/gtk-2.0/\1"/

```

### Theme not applied to root applications

As user theme files (`$XDG_CONFIG_HOME/gtk-3.0/settings.ini`, `~/.gtkrc-2.0`) are not read by other accounts, the selected theme will not apply to [X applications run as root](/index.php/Running_X_apps_as_root "Running X apps as root"). Possible solutions include:

*   Create symlinks, e.g

```
# ln -s /home/[username]/.gtkrc-2.0 /etc/gtk-2.0/gtkrc
# ln -s /home/[username]/.config/gtk-3.0/settings.ini /etc/gtk-3.0/settings.ini

```

*   Configure system-wide theme files: `/etc/gtk-3.0/settings.ini` (GTK+ 3) or `/etc/gtk-2.0/gtkrc` (GTK+ 2)
*   Adjust the theme as root

```
# gksu lxappearance

```

*   Use a settings daemon (this is what most desktop environments do). A desktop-agnostic variant using [XSettings](http://standards.freedesktop.org/xsettings-spec/xsettings-spec-0.5.html) is available in the [AUR](/index.php/AUR "AUR") under [xsettingsd-git](https://aur.archlinux.org/packages/xsettingsd-git/).

### Client-side decorations

GTK 3.12 introduced [client-side decorations](http://blogs.gnome.org/mclasen/2013/12/05/client-side-decorations-in-themes/), which move the title-bar away from the window manager. This may present issues such as [double title-bars](http://redmine.audacious-media-player.org/boards/1/topics/1135), no title-bar at all or [double shadows](https://github.com/chjj/compton/issues/189) with compositing enabled.

To remove the shadow and gap around windows (for example in combination with a tiling window manager), create the following file:

 `~/.config/gtk-3.0/gtk.css` 
```
.window-frame, .window-frame:backdrop {
 box-shadow: 0 0 0 black;
 border-style: none;
 margin: 0;
 border-radius: 0;
}

.titlebar {
 border-radius: 0;
}

.window-frame.csd.popup {
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.2), 0 0 0 1px rgba(0, 0, 0, 0.13);
}

.header-bar {
  background-image: none;
  background-color: #ededed;
  box-shadow: none;
}
/* You may want to use this if you don't like the double title.
GtkLabel.title {
    opacity: 0;
}*/

```

To adjust the buttons in the header bar, use the `gtk-decoration-layout` setting. [[4]](https://developer.gnome.org/gtk3/stable/GtkSettings.html#GtkSettings--gtk-decoration-layout) The below examples removes all buttons:

 `~/.config/gtk-3.0/settings.ini`  `gtk-decoration-layout=menu:` 

### cedilla ç/Ç instead of ć/Ć

See [[5]](https://bugs.launchpad.net/ubuntu/+source/gtk+2.0/+bug/518056), and [[6]](https://bugs.launchpad.net/ubuntu/+source/gtk+2.0/+bug/518056/comments/37) for a workaround using Xcompose (US international layout).

### Suppress warning about accessibility bus

If you do not use any [Gnome Accessibility](https://wiki.gnome.org/Accessibility) features, you may receive warnings like:

```
WARNING **: Couldn't connect to accessibility bus:

```

To suppress these warnings, execute programs with `NO_AT_BRIDGE=1` or set that as a global [environment variable](/index.php/Environment_variable "Environment variable").

### Titlebar background color mismatch

If you are using a [window manager](/index.php/Window_manager "Window manager") which uses a window decoration theme that mimics the GTK+ theme background color, you may find that the titlebar color no longer completely matches the application color in some GTK+ 3 applications. As a workaround, create the following file:

 `~/.config/gtk-3.0/gtk.css` 
```
/* Always use background color */
GtkWindow {
    background-color: @theme_bg_color;
}

/* Fix tooltip background override */
.tooltip {
    background-color: rgba(0, 0, 0, 0.8);
}

.tooltip * {
    background-color: transparent;
}

/* Fix Nautilus desktop window background override */
NautilusWindow {
     background-color: transparent; 
}

```

### Wrong focus events with tiling window managers

**Note:** This disables touchscreen support for GTK3 applications. [[7]](https://bugzilla.gnome.org/show_bug.cgi?id=677329#c14)

[Define](/index.php/Define "Define") `GDK_CORE_DEVICE_EVENTS=1` to use GTK2 style input, instead of xinput2\. [[8]](https://bugzilla.gnome.org/show_bug.cgi?id=677329#c10)

### Thumbnail support for GTK+ 2 file dialog

Install [gtk2-patched-filechooser-icon-view](https://aur.archlinux.org/packages/gtk2-patched-filechooser-icon-view/) to have the option to view files as thumbnails instead of list in the GTK+ file chooser.

### Button/menu icons in some apps in GNOME Wayland session

Your `~/.config/gtk-3.0/settings.ini` file is misconfigured. This can happend if you try other GTK+ based desktop environments. These are the offending values:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-button-images=1
gtk-menu-images=1
```

Simply set them to 0 or remove the whole file to use GNOME defaults.

### Printers not shown in the GTK print dialog

From GTK 3.22 onwards, one needs to additionally install [gtk3-print-backends](https://www.archlinux.org/packages/?name=gtk3-print-backends) to get the list of printers in the GTK print dialog.

### Some GTK+ 2 themes only change the UI color palette

Depending on the theme of choice's support for GTK+ 2, UI controls may still have the default Raleigh appearance, possibly with a different color palette. This is due to these themes requiring the GTK+ 2 Murrine engine, which is missing (GTK+ 2 programs should complain about it on their standard error output). Install the [gtk-engine-murrine](https://www.archlinux.org/packages/?name=gtk-engine-murrine) package.

## Examples

GTK+ 2 configuration example:

 `~/.gtkrc-2.0` 
```
# GTK theme
include "/usr/share/themes/Clearlooks/gtk-2.0/gtkrc"

# Font
style "myfont" {
    font_name = "DejaVu Sans 8"
}
widget_class "*" style "myfont"
gtk-font-name = "DejaVu Sans 8"

# Icon theme
gtk-icon-theme-name = "Tango"

# Toolbar style
gtk-toolbar-style = GTK_TOOLBAR_ICONS
```

GTK+ 3 example of a configuration as converted from GTK+ 2.x to GTK+ 3.x by [lxappearance](https://www.archlinux.org/packages/?name=lxappearance):

 `$XDG_CONFIG_HOME/gtk-3.0/settings.ini` 
```
[Settings] 
gtk-theme-name=TraditionalOk
gtk-icon-theme-name=Fog
gtk-font-name=Luxi Sans 12
gtk-cursor-theme-name=mate
gtk-cursor-theme-size=24
gtk-toolbar-style=GTK_TOOLBAR_BOTH_HORIZ
gtk-toolbar-icon-size=GTK_ICON_SIZE_LARGE_TOOLBAR
gtk-button-images=1
gtk-menu-images=1
gtk-enable-event-sounds=0
gtk-enable-input-feedback-sounds=0
gtk-xft-antialias=1
gtk-xft-hinting=1
gtk-xft-hintstyle=hintslight
gtk-xft-rgba=rgb
```

## See also

*   [The official GTK+ website](http://www.gtk.org/)
*   [Wikipedia article about GTK+](https://en.wikipedia.org/wiki/GTK%2B "wikipedia:GTK+")
*   [GTK+ 2.0 Tutorial](http://developer.gnome.org/gtk-tutorial/stable/)
*   [GTK+ 3 Reference Manual](http://developer.gnome.org/gtk3/stable/)
*   [gtkmm Tutorial](http://developer.gnome.org/gtkmm-tutorial/stable/)
*   [gtkmm Reference Manual](http://developer.gnome.org/gtkmm/stable/)