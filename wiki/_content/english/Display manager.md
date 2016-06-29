A [display manager](https://en.wikipedia.org/wiki/X_display_manager_(program_type) "wikipedia:X display manager (program type)"), or login manager, is typically a graphical user interface that is displayed at the end of the boot process in place of the default shell. There are various implementations of display managers, just as there are various types of [window managers](/index.php/Window_managers "Window managers") and [desktop environments](/index.php/Desktop_environments "Desktop environments"). There is usually a certain amount of customization and themeability available with each one.

## Contents

*   [1 List of display managers](#List_of_display_managers)
    *   [1.1 Console](#Console)
    *   [1.2 Graphical](#Graphical)
*   [2 Loading the display manager](#Loading_the_display_manager)
    *   [2.1 Using systemd-logind](#Using_systemd-logind)
*   [3 Session configuration](#Session_configuration)
    *   [3.1 Run ~/.xinitrc as a session](#Run_.7E.2F.xinitrc_as_a_session)
    *   [3.2 Starting applications without a window manager](#Starting_applications_without_a_window_manager)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Autostarting](#Autostarting)
    *   [4.2 Set the language](#Set_the_language)
*   [5 Known issues](#Known_issues)
    *   [5.1 Incompatibility with systemd](#Incompatibility_with_systemd)

## List of display managers

### Console

*   **[CDM](/index.php/CDM "CDM")** — Ultra-minimalistic, yet full-featured login manager written in Bash.

	[https://github.com/ghost1227/cdm](https://github.com/ghost1227/cdm) || [cdm-git](https://aur.archlinux.org/packages/cdm-git/)

*   **[Console TDM](/index.php/Console_TDM "Console TDM")** — Extension for *xinit* written in pure Bash.

	[https://github.com/dopsi/console-tdm](https://github.com/dopsi/console-tdm) || [console-tdm](https://aur.archlinux.org/packages/console-tdm/)

*   **[nodm](/index.php/Nodm "Nodm")** — Minimalistic display manager for automatic logins.

	[https://github.com/spanezz/nodm](https://github.com/spanezz/nodm) || [nodm](https://www.archlinux.org/packages/?name=nodm)

### Graphical

*   **[Entrance](/index.php/Enlightenment "Enlightenment")** — An EFL based display manager, highly experimental.

	[http://enlightenment.org/](http://enlightenment.org/) || [entrance-git](https://aur.archlinux.org/packages/entrance-git/)

*   **[GDM](/index.php/GDM "GDM")** — [GNOME](/index.php/GNOME "GNOME") display manager.

	[https://wiki.gnome.org/Projects/GDM](https://wiki.gnome.org/Projects/GDM) || [gdm](https://www.archlinux.org/packages/?name=gdm)

*   **[KDM](/index.php/KDM "KDM")** — [KDE](/index.php/KDE "KDE")4 display manager (discontinued).

	[http://www.kde.org/](http://www.kde.org/) || [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)

*   **[LightDM](/index.php/LightDM "LightDM")** — Cross-desktop display manager, can use various front-ends written in any toolkit.

	[http://www.freedesktop.org/wiki/Software/LightDM](http://www.freedesktop.org/wiki/Software/LightDM) || [lightdm](https://www.archlinux.org/packages/?name=lightdm)

*   **[LXDM](/index.php/LXDM "LXDM")** — [LXDE](/index.php/LXDE "LXDE") display manager. Can be used independent of the LXDE desktop environment.

	[http://sourceforge.net/projects/lxdm/](http://sourceforge.net/projects/lxdm/) || [lxdm](https://www.archlinux.org/packages/?name=lxdm)

*   **MDM** — MDM display manager, used in Linux Mint, a fork of GDM 2.

	[https://github.com/linuxmint/mdm](https://github.com/linuxmint/mdm) || [mdm-display-manager](https://aur.archlinux.org/packages/mdm-display-manager/)

*   **[SDDM](/index.php/SDDM "SDDM")** — QML-based display manager and successor to KDE4's kdm; recommended for Plasma 5 and LXQt.

	[https://github.com/sddm/sddm](https://github.com/sddm/sddm) || [sddm](https://www.archlinux.org/packages/?name=sddm)

*   **[SLiM](/index.php/SLiM "SLiM")** — Lightweight and elegant graphical login solution. (discontinued)

	[http://sourceforge.net/projects/slim.berlios/](http://sourceforge.net/projects/slim.berlios/) || [slim](https://www.archlinux.org/packages/?name=slim)

*   **[XDM](/index.php/XDM "XDM")** — X display manager with support for XDMCP, host chooser.

	[http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html](http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html) || [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)

## Loading the display manager

To enable graphical login, [enable](/index.php/Enable "Enable") the appropriate systemd service. For example, for [SDDM](/index.php/SDDM "SDDM"), enable `sddm.service`.

This should work out of the box. If not, you might have to reset a custom `default.target` symlink to point to the default `graphical.target`.

After enabling [SDDM](/index.php/SDDM "SDDM") a symlink `display-manager.service` should be set in `/etc/systemd/system/`. You may need to use `--force` to override old symlinks.

 `$ ls -l /etc/systemd/system/display-manager.service`  `[...] /etc/systemd/system/display-manager.service -> /usr/lib/systemd/system/sddm.service` 

### Using systemd-logind

In order to check the status of your user session, you can use *loginctl*. All [polkit](/index.php/Polkit "Polkit") actions like suspending the system or mounting external drives will work out of the box.

```
$ loginctl show-session $XDG_SESSION_ID

```

## Session configuration

Many display managers read available sessions from `/usr/share/xsessions/` directory. It contains standard [desktop entry files](http://standards.freedesktop.org/desktop-entry-spec/latest/) for each DM/WM.

To add/remove entries to your display manager's session list; create/remove the *.desktop* files in `/usr/share/xsessions/` as desired. A typical *.desktop* file will look something like:

```
[Desktop Entry]
Encoding=UTF-8
Name=Openbox
Comment=Log in using the Openbox window manager (without a session manager)
Exec=/usr/bin/openbox-session
TryExec=/usr/bin/openbox-session
Icon=openbox.png
Type=XSession

```

### Run ~/.xinitrc as a session

Installing [xinit-xsession](https://aur.archlinux.org/packages/xinit-xsession/) will provide an option to run your .xinitrc as a session.

### Starting applications without a window manager

You can also launch an application without any decoration, desktop, or window management. For example to launch [google-chrome](https://aur.archlinux.org/packages/google-chrome/) create a `web-browser.desktop` file in `/usr/share/xsessions/` like this:

```
[Desktop Entry]
Encoding=UTF-8
Name=Web Browser
Comment=Use a web browser as your session
Exec=/usr/bin/google-chrome --auto-launch-at-startup
TryExec=/usr/bin/google-chrome --auto-launch-at-startup
Icon=google-chrome

```

In this case, once you login, the application set with `Exec` will be launched immediately. When you close the application, you will be taken back to the login manager (same as logging out of a normal DE/WM).

It is important to remember that most graphical applications are not intended to be launched this way and you might have manual tweaking to do or limitations to live with (there is no window manager, so do not expect to be able to move or resize *any* windows, including dialogs; nonetheless, you might be able to set the window geometry in the application's configuration files).

See also [xinitrc#Starting applications without a window manager](/index.php/Xinitrc#Starting_applications_without_a_window_manager "Xinitrc").

## Tips and tricks

### Autostarting

Most display managers source `/etc/xprofile`, `~/.xprofile` and `/etc/X11/xinit/xinitrc.d/`. For more details, see [xprofile](/index.php/Xprofile "Xprofile").

### Set the language

For display managers that use [AccountsService](http://freedesktop.org/wiki/Software/AccountsService/) the display manager [locale](/index.php/Locale "Locale") can be set by editing `/var/lib/AccountsService/users/$USER`:

```
[User]
Language=*your_locale*

```

where *your_locale* is a value such as `en_GB.UTF-8`.

Restart your display manager for the changes to take effect.

## Known issues

### Incompatibility with systemd

*Affected DMs: Entrance, MDM*

Some display managers are not fully compatible with systemd, because they reuse the [PAM](/index.php/PAM "PAM") session process. It causes various problems on second login, e.g.:

*   NetworkManager applet does not work,
*   PulseAudio volume cannot be adjusted,
*   login failed into GNOME with another user.