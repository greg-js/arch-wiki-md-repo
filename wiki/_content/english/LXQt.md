In early 2013, Hong Jen Yee "PCMan" started porting [LXDE](/index.php/LXDE "LXDE") components to [Qt](/index.php/Qt "Qt"). The first [preview of LXDE-Qt](http://blog.lxde.org/?p=1013) was released on July 3rd, 2013\. On July 21st, it was announced that Razor-qt (a desktop similar in design to LXDE) and LXDE were merging.

The result is [LXQt](http://lxqt.org), a desktop built on Qt which partly uses Razor-qt and LXDE components. While development is mainly focused on LXQt, the GTK+ 2 version of LXDE will see continued development.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting the desktop](#Starting_the_desktop)
    *   [2.1 Using xinit](#Using_xinit)
    *   [2.2 Graphical login](#Graphical_login)
*   [3 Configuration](#Configuration)
    *   [3.1 Replace Openbox](#Replace_Openbox)
    *   [3.2 Autostarting applications](#Autostarting_applications)
    *   [3.3 Set-up environment variables](#Set-up_environment_variables)
    *   [3.4 Editing the Application Menu](#Editing_the_Application_Menu)
    *   [3.5 Compton](#Compton)
*   [4 Suggested applications](#Suggested_applications)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Desktop icons are grouped together](#Desktop_icons_are_grouped_together)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [lxqt](https://www.archlinux.org/groups/x86_64/lxqt/) group.

An icon theme is also needed. The default one is *Oxygen*, which can be installed with the [oxygen-icons](https://www.archlinux.org/packages/?name=oxygen-icons) package.

For additional functionality, you may wish to install the following:

*   **[Connman](/index.php/Connman "Connman")** — Network manager like [NetworkManager](/index.php/NetworkManager "NetworkManager").

	[http://git.kernel.org/cgit/network/connman](http://git.kernel.org/cgit/network/connman) || [connman](https://www.archlinux.org/packages/?name=connman)

*   **LXQt Connman applet** — LXQt system-tray applet for [Connman](/index.php/Connman "Connman").

	[https://github.com/surlykke/lxqt-connman-applet](https://github.com/surlykke/lxqt-connman-applet) || [lxqt-connman-applet-git](https://aur.archlinux.org/packages/lxqt-connman-applet-git/)

*   **LXImage-Qt** — Image viewer and screenshot tool for LXQt.

	[https://github.com/lxde/lximage-qt](https://github.com/lxde/lximage-qt) || [lximage-qt](https://aur.archlinux.org/packages/lximage-qt/)

*   **ObConf-Qt** — The Qt port of ObConf, the [Openbox](/index.php/Openbox "Openbox") configuration tool.

	[https://github.com/lxde/obconf-qt](https://github.com/lxde/obconf-qt) || [obconf-qt](https://aur.archlinux.org/packages/obconf-qt/)

*   **LXAppearance** — Easy to use GTK+ configuration tool. Part of LXDE.

	[https://sourceforge.net/projects/lxde/files/LXAppearance/](https://sourceforge.net/projects/lxde/files/LXAppearance/) || [lxappearance](https://www.archlinux.org/packages/?name=lxappearance)

*   **[SDDM](/index.php/SDDM "SDDM")** — The recommended display manager for LXQt.

	[https://github.com/sddm/sddm](https://github.com/sddm/sddm) || [sddm](https://www.archlinux.org/packages/?name=sddm)

*   A screen locker, if needed. For example, [slock](https://www.archlinux.org/packages/?name=slock) or [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver). Both are confirmed to integrate with LXQt, others may too.

Some LXQt panel plugins require extra packages to function, check the [optional dependencies](/index.php/PKGBUILD#optdepends "PKGBUILD") for [lxqt-panel](https://www.archlinux.org/packages/?name=lxqt-panel).

## Starting the desktop

### Using xinit

Append the following line to [Xinitrc](/index.php/Xinitrc "Xinitrc"):

```
exec startlxqt

```

### Graphical login

Choose *LXQt Desktop* from the menu in a [display manager](/index.php/Display_manager "Display manager") of choice.

## Configuration

LXQt in general tries to provide GUI applications to change its settings. Configuration files are in `~/.config/lxqt`. This directory is initialized automatically. The default configuration for new users is found in `/etc/xdg/lxqt`.

### Replace Openbox

While [Openbox](/index.php/Openbox "Openbox") is the default [window manager](/index.php/Window_manager "Window manager") for LXQt, you can specify a different window manager to use with LXQt via *Session Settings*, `lxqt-config-session`; or by editing `~/.config/lxqt/session.conf`. Change the following line:

```
window_manager=openbox

```

to a [window manager](/index.php/Window_manager "Window manager") of choice:

```
window_manager=*your_window_manager*

```

### Autostarting applications

To have X applications start on login, click the main menu from the LXQt -> Preferences -> LXQt Settings -> Session Settings. Alternatively, this can be launched with:

```
lxqt-config-session

```

From this window, click on "AutoStart" on the left side. Here you can add a new application to either the global autostart (launched in all sessions implementing the said specification) or your local autostart (labled LXQt Autostart) (See [issue 746](https://github.com/lxde/lxqt/issues/746) for a bug related to this option).

For each item you add, `lxqt-config-session` will create a .desktop-file at `~/.config/autostart`. Preinstalled applications that will be automatically started at login can be found at `/etc/xdg/autostart`. So you can also change your autostart preferences by editing the files in these directories. Besides, the distinction between "Global Autostart" and "LXQt Autostart" does not depend on the directory in which the corresponding .desktop-file is located, but rather on the `OnlyShowIn`-setting. If it is `OnlyShowIn=true`, it is considered an "LXQt Autostart". Furthermore, if `X-LXQt-Module=true`, the item is not shown in `lxqt-config-session`.

### Set-up environment variables

Environment variables for LXQt session can be defined in Session Settings.

For example use `SAL_USE_VCLPLUGIN=gtk` to force starting libreoffice with gtk2 UI.

### Editing the Application Menu

It is possible to edit menu entries by editing their .desktop files stored in `/usr/share/applications/lxqt-*.desktop` files. See [Desktop entries](/index.php/Desktop_entries "Desktop entries").

### Compton

If present [Compton](/index.php/Compton "Compton") should auto start with the initial default session.

## Suggested applications

As LXQt is a lightweight desktop, a plain install will not provide many desktop applications. It is left to the user to choose what applications they wish to install. The [Razor-qt wiki](https://github.com/Razor-qt/razor-qt/wiki/3rd-party-applications) has a page which lists of number of useful Qt applications that you may wish to install. Also see the [List of applications](/index.php/List_of_applications "List of applications") page for a comprehensive list of applications available in Arch.

## Troubleshooting

### Desktop icons are grouped together

When moving icons on the desktop it is possible to place them a bit too close to each other making them connected. If unable to separate them Stop Desktop from Session Settings, remove `.config/pcmanfm-qt/lxqt/desktop-items-0.conf` and Start Desktop again.

## See also

*   [LXQt homepage](http://lxqt.org)
*   [LXQt development](https://github.com/lxde/lxqt)
*   [LXQt on deviantART](http://lxqt-de.deviantart.com/)
*   [LXQt wiki on GitHUb](https://github.com/lxde/lxqt/wiki)