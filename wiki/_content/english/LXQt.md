Related articles

*   [LXDE](/index.php/LXDE "LXDE")
*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Window manager](/index.php/Window_manager "Window manager")

In early 2013, Hong Jen Yee "PCMan" started porting [LXDE](/index.php/LXDE "LXDE") components to [Qt](/index.php/Qt "Qt"). The first [preview of LXDE-Qt](http://blog.lxde.org/?p=1013) was released on July 3rd, 2013\. On July 21st, it was announced that Razor-qt (a desktop similar in design to LXDE) and LXDE were merging.

The result is [LXQt](http://lxqt.org), a desktop built on Qt which partly uses Razor-qt and LXDE components. While development is mainly focused on LXQt, the GTK+ 2 version of LXDE will see continued development.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Starting the desktop](#Starting_the_desktop)
    *   [2.1 Using xinit](#Using_xinit)
    *   [2.2 Graphical login](#Graphical_login)
*   [3 Configuration](#Configuration)
    *   [3.1 Use a different window manager](#Use_a_different_window_manager)
    *   [3.2 Autostart](#Autostart)
    *   [3.3 Set-up environment variables](#Set-up_environment_variables)
    *   [3.4 Editing the Application Menu](#Editing_the_Application_Menu)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Desktop icons are grouped together](#Desktop_icons_are_grouped_together)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Customizing Leave](#Customizing_Leave)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [lxqt](https://www.archlinux.org/groups/x86_64/lxqt/) group and an icon theme (e.g. [breeze-icons](https://www.archlinux.org/packages/?name=breeze-icons) or [oxygen-icons](https://www.archlinux.org/packages/?name=oxygen-icons)).

For additional functionality, you may wish to install the following:

*   **LXQt Connman applet** — LXQt system-tray applet for [ConnMan](/index.php/ConnMan "ConnMan").

	[https://github.com/lxqt/lxqt-connman-applet](https://github.com/lxqt/lxqt-connman-applet) || [lxqt-connman-applet](https://aur.archlinux.org/packages/lxqt-connman-applet/)

*   **[SDDM](/index.php/SDDM "SDDM")** — The recommended display manager for LXQt.

	[https://github.com/sddm/sddm](https://github.com/sddm/sddm) || [sddm](https://www.archlinux.org/packages/?name=sddm)

*   A screen locker, if needed. For example, [slock](/index.php/Slock "Slock") or [XScreenSaver](/index.php/XScreenSaver "XScreenSaver"). Both are confirmed to integrate with LXQt, others may too. If you want to disable screen locking upon suspend/sleep it is under *LXQt > Preferences > LXQt Settings > Session Settings > Lock screen before suspending/hibernating* checkbox.
*   If you haven't yet, install xorg.

**Tip:** LXQt uses *xdg-screensaver* from [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) for screen locking which only works with XScreenSaver and [xautolock](https://www.archlinux.org/packages/?name=xautolock) in LXQt session. You can use it or another screen locker by itself. For example, with *slock* you can follow [Slock#Lock on suspend](/index.php/Slock#Lock_on_suspend "Slock") as well as install patched [xdg-utils-slock](https://aur.archlinux.org/packages/xdg-utils-slock/) to obtain feelings expected by LXQt

*   Some LXQt panel plugins require extra packages to function, check the [optional dependencies](/index.php/PKGBUILD#optdepends "PKGBUILD") for [lxqt-panel](https://www.archlinux.org/packages/?name=lxqt-panel).

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

### Use a different window manager

While [Openbox](/index.php/Openbox "Openbox") is the default [window manager](/index.php/Window_manager "Window manager") for LXQt, you can specify a different window manager to use with LXQt via *Session Settings*, `lxqt-config-session`; or by editing `~/.config/lxqt/session.conf`. Change the following line:

```
window_manager=openbox

```

to a [window manager](/index.php/Window_manager "Window manager") of choice:

```
window_manager=*your_window_manager*

```

### Autostart

To have X applications start on login, click the main menu from the *LXQt > Preferences > LXQt Settings > Session Settings*. Alternatively, this can be launched with:

```
lxqt-config-session

```

From this window, click on *AutoStart* on the left side. Here you can add a new application to either the global autostart (launched in all sessions implementing the [XDG Autostart](/index.php/XDG_Autostart "XDG Autostart") specification) or your local autostart (labelled LXQt Autostart) (See [issue 746](https://github.com/lxde/lxqt/issues/746) for a bug related to this option). For each item you add, `lxqt-config-session` will create a Desktop entry (*.desktop* file) in the appropriate [XDG Autostart](/index.php/XDG_Autostart "XDG Autostart") directory.

The distinction between "Global Autostart" and "LXQt Autostart" does not depend on the directory in which the corresponding *.desktop* file is located, but rather on the `OnlyShowIn` setting. If it is `OnlyShowIn=true`, it is considered an "LXQt Autostart". Furthermore, if `X-LXQt-Module=true`, the item is not shown in `lxqt-config-session`.

### Set-up environment variables

[Environment variables](/index.php/Environment_variables "Environment variables") for LXQt session can be defined in Session Settings.

### Editing the Application Menu

It is possible to edit menu entries by editing their *.desktop* files stored in `/usr/share/applications/lxqt-*.desktop` files. See [Desktop entries](/index.php/Desktop_entries "Desktop entries").

## Troubleshooting

### Desktop icons are grouped together

When moving icons on the desktop it is possible to place them a bit too close to each other making them connected. If unable to separate them Stop Desktop from Session Settings, remove `~/.config/pcmanfm-qt/lxqt/desktop-items-0.conf` and Start Desktop again.

## Tips and tricks

### Customizing Leave

One can customize the options available under *Leave* simply by copying the respective package provide `.desktop` file to `~/.local/share/applications` and modifying it to contain the `NoDisplay=true` directive. Reference: [#876](https://github.com/lxde/lxqt/issues/876).

Complete list of files to consider masking include:

```
lxqt-hibernate.desktop
lxqt-leave.desktop
lxqt-lockscreen.desktop
lxqt-logout.desktop
lxqt-reboot.desktop
lxqt-shutdown.desktop
lxqt-suspend.desktop

```

Example: remove hibernate option.

```
$ mkdir -p ~/.local/share/applications
$ sed '/OnlyShowIn/aNoDisplay=true' </usr/share/applications/lxqt-hibernate.desktop >~/.local/share/applications/lxqt-hibernate.desktop

```

## See also

*   [LXQt homepage](http://lxqt.org)
*   [LXQt development](https://github.com/lxde/lxqt)
*   [LXQt on deviantART](http://lxqt-de.deviantart.com/)
*   [LXQt wiki on GitHub](https://github.com/lxde/lxqt/wiki)