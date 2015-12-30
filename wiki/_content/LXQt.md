# LXQt

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [LXDE](/index.php/LXDE "LXDE")
*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Window manager](/index.php/Window_manager "Window manager")

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
    *   [3.3 Editing the Application Menu](#Editing_the_Application_Menu)
*   [4 Suggested applications](#Suggested_applications)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [lxqt](https://www.archlinux.org/groups/x86_64/lxqt/) group.

You also need an icon theme to be installed. The default one is _Oxygen_, which can be installed with the [oxygen-icons](https://www.archlinux.org/packages/?name=oxygen-icons) package.

For additional functionality, you may wish to install the following:

*   **Connman** — Network manager like [NetworkManager](/index.php/NetworkManager "NetworkManager").

[http://git.kernel.org/cgit/network/connman](http://git.kernel.org/cgit/network/connman) || [connman](https://www.archlinux.org/packages/?name=connman)

*   **LXQt Connman applet** — LXQt system-tray applet for [Connman](/index.php/Connman "Connman").

[https://github.com/surlykke/lxqt-connman-applet](https://github.com/surlykke/lxqt-connman-applet) || [lxqt-connman-applet-git](https://aur.archlinux.org/packages/lxqt-connman-applet-git/)<sup><small>AUR</small></sup>

*   **LXImage-Qt** — Image viewer and screenshot tool for LXQt.

[https://github.com/lxde/lximage-qt](https://github.com/lxde/lximage-qt) || [lximage-qt](https://aur.archlinux.org/packages/lximage-qt/)<sup><small>AUR</small></sup>

*   **ObConf-Qt** — The Qt port of ObConf, the [Openbox](/index.php/Openbox "Openbox") configuration tool.

[https://github.com/lxde/obconf-qt](https://github.com/lxde/obconf-qt) || [obconf-qt](https://aur.archlinux.org/packages/obconf-qt/)<sup><small>AUR</small></sup>

*   **QTerminal** — Lightweight Qt-based terminal emulator.

[https://github.com/qterminal/qterminal](https://github.com/qterminal/qterminal) || [qterminal](https://aur.archlinux.org/packages/qterminal/)<sup><small>AUR</small></sup>

*   **[SDDM](/index.php/SDDM "SDDM")** — The recommended display manager for LXQt.

[https://github.com/sddm/sddm](https://github.com/sddm/sddm) || [sddm](https://www.archlinux.org/packages/?name=sddm)

*   **[XScreenSaver](/index.php/XScreenSaver "XScreenSaver")** — A screen saver required for screen locking in LXQt.

[https://www.jwz.org/xscreensaver/](https://www.jwz.org/xscreensaver/) || [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver)

Some LXQt panel plugins require extra packages to function, check the [optional dependencies](/index.php/PKGBUILD#optdepends "PKGBUILD") for [lxqt-panel](https://www.archlinux.org/packages/?name=lxqt-panel).

## Starting the desktop

### Using xinit

Append the following line to [Xinitrc](/index.php/Xinitrc "Xinitrc"):

```
exec startlxqt

```

### Graphical login

Choose _LXQt Desktop_ from the menu in a [display manager](/index.php/Display_manager "Display manager") of choice.

## Configuration

LXQt in general tries to provide GUI applications to change its settings. Configuration files are in `~/.config/lxqt`. This directory is initialized automatically. The default configuration for new users is found in `/etc/xdg/lxqt`.

### Replace Openbox

While [Openbox](/index.php/Openbox "Openbox") is the default [window manager](/index.php/Window_manager "Window manager") for LXQt, you can specify a different window manager to use with LXQt via _Session Settings_, `lxqt-config-session`; or by editing `~/.config/lxqt/session.conf`. Change the following line:

```
window_manager=openbox

```

to a [window manager](/index.php/Window_manager "Window manager") of choice:

```
window_manager=_your_window_manager_

```

### Autostarting applications

To have X applications start on login, click the main menu from the LXQt -> Preferences -> LXQt Settings -> Session Settings. Alternatively, this can be launched with:

```
lxqt-config-session

```

From this window, click on "AutoStart" on the left side. Here you can add a new application to either the global autostart (launched in all sessions implementing the said specification) or your local autostart (labled LXQt Autostart) (See [issue 746](https://github.com/lxde/lxqt/issues/746) for a bug related to this option).

### Editing the Application Menu

It is possible to edit menu entries by editing their .desktop files stored in `/usr/share/applications/lxqt-*.desktop` files. See [Desktop entries](/index.php/Desktop_entries "Desktop entries").

## Suggested applications

As LXQt is a lightweight desktop, a plain install will not provide many desktop applications. It is left to the user to choose what applications they wish to install. The [Razor-qt wiki](https://github.com/Razor-qt/razor-qt/wiki/3rd-party-applications) has a page which lists of number of useful Qt applications that you may wish to install. Also see the [List of applications](/index.php/List_of_applications "List of applications") page for a comprehensive list of applications available in Arch.

## See also

*   [LXQt homepage](http://lxqt.org)
*   [LXQt development](https://github.com/lxde/lxqt)
*   [LXQt on deviantART](http://lxqt-de.deviantart.com/)
*   [LXQt wiki on GitHUb](https://github.com/lxde/lxqt/wiki)

Retrieved from "[https://wiki.archlinux.org/index.php?title=LXQt&oldid=413859](https://wiki.archlinux.org/index.php?title=LXQt&oldid=413859)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments")