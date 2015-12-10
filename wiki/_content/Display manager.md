# Display manager

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Start X at login](/index.php/Start_X_at_login "Start X at login")

A [display manager](https://en.wikipedia.org/wiki/X_display_manager_(program_type) "wikipedia:X display manager (program type)"), or login manager, is typically a graphical user interface that is displayed at the end of the boot process in place of the default shell. There are various implementations of display managers, just as there are various types of [window managers](/index.php/Window_managers "Window managers") and [desktop environments](/index.php/Desktop_environments "Desktop environments"). There is usually a certain amount of customization and themeability available with each one.

## Contents

*   [1 List of display managers](#List_of_display_managers)
    *   [1.1 Console](#Console)
    *   [1.2 Graphical](#Graphical)
*   [2 Loading the display manager](#Loading_the_display_manager)
    *   [2.1 Using systemd-logind](#Using_systemd-logind)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Run ~/.xinitrc as a session](#Run_.7E.2F.xinitrc_as_a_session)
    *   [3.2 Session list](#Session_list)
    *   [3.3 Starting applications without a window manager](#Starting_applications_without_a_window_manager)
    *   [3.4 Autostarting](#Autostarting)
    *   [3.5 Set the language](#Set_the_language)
*   [4 Known issues](#Known_issues)
    *   [4.1 Incompatibility with systemd](#Incompatibility_with_systemd)

## List of display managers

### Console

*   **[CDM](/index.php/CDM "CDM")** — Ultra-minimalistic, yet full-featured login manager written in Bash.

[https://github.com/ghost1227/cdm](https://github.com/ghost1227/cdm) || [cdm-git](https://aur.archlinux.org/packages/cdm-git/)<sup><small>AUR</small></sup>

*   **[Console TDM](/index.php/Console_TDM "Console TDM")** — Extension for _xinit_ written in pure Bash.

[http://code.google.com/p/t-display-manager/](http://code.google.com/p/t-display-manager/) || [console-tdm](https://aur.archlinux.org/packages/console-tdm/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/console-tdm)]</sup>

*   **[nodm](/index.php/Nodm "Nodm")** — Minimalistic display manager for automatic logins.

[http://enricozini.org/sw/nodm/](http://enricozini.org/sw/nodm/) || [nodm](https://www.archlinux.org/packages/?name=nodm)

### Graphical

*   **[Entrance](/index.php/Enlightenment "Enlightenment")** — An EFL based display manager, highly experimental.

[http://enlightenment.org/](http://enlightenment.org/) || [entrance-git](https://aur.archlinux.org/packages/entrance-git/)<sup><small>AUR</small></sup>

*   **[GDM](/index.php/GDM "GDM")** — [GNOME](/index.php/GNOME "GNOME") display manager.

[https://wiki.gnome.org/Projects/GDM](https://wiki.gnome.org/Projects/GDM) || [gdm](https://www.archlinux.org/packages/?name=gdm)

*   **[KDM](/index.php/KDM "KDM")** — [KDE](/index.php/KDE "KDE") display manager.

[http://www.kde.org/](http://www.kde.org/) || [kdebase-workspace](https://www.archlinux.org/packages/?name=kdebase-workspace)

*   **[LightDM](/index.php/LightDM "LightDM")** — Cross-desktop display manager, can use various front-ends written in any toolkit.

[http://www.freedesktop.org/wiki/Software/LightDM](http://www.freedesktop.org/wiki/Software/LightDM) || [lightdm](https://www.archlinux.org/packages/?name=lightdm)

*   **[LXDM](/index.php/LXDM "LXDM")** — [LXDE](/index.php/LXDE "LXDE") display manager. Can be used independent of the LXDE desktop environment.

[http://sourceforge.net/projects/lxdm/](http://sourceforge.net/projects/lxdm/) || [lxdm](https://www.archlinux.org/packages/?name=lxdm)

*   **MDM** — MDM display manager, used in Linux Mint, a fork of GDM 2.

[https://github.com/linuxmint/mdm](https://github.com/linuxmint/mdm) || [mdm-display-manager](https://aur.archlinux.org/packages/mdm-display-manager/)<sup><small>AUR</small></sup>

*   **[Qingy](/index.php/Qingy "Qingy")** — Ultralight and very configurable graphical login independent on X Windows (uses DirectFB).

[http://qingy.sourceforge.net/](http://qingy.sourceforge.net/) || [qingy](https://aur.archlinux.org/packages/qingy/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/qingy)]</sup>

*   **[SDDM](/index.php/SDDM "SDDM")** — QML-based display manager and successor to KDE4's kdm; useful with Plasma.

[https://github.com/sddm/sddm](https://github.com/sddm/sddm) || [sddm](https://www.archlinux.org/packages/?name=sddm)

*   **[SLiM](/index.php/SLiM "SLiM")** — Lightweight and elegant graphical login solution.

[http://sourceforge.net/projects/slim.berlios/](http://sourceforge.net/projects/slim.berlios/) || [slim](https://www.archlinux.org/packages/?name=slim)

*   **[XDM](/index.php/XDM "XDM")** — X display manager with support for XDMCP, host chooser.

[http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html](http://www.x.org/archive/X11R7.5/doc/man/man1/xdm.1.html) || [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)

## Loading the display manager

To enable graphical login, [enable](/index.php/Enable "Enable") the appropriate systemd service. For example, for KDM, enable `kdm.service`.

This should work out of the box. If not, you might have to reset a custom `default.target` symlink to point to the default `graphical.target`.

After enabling KDM a symlink `display-manager.service` should be set in `/etc/systemd/system/`. You may need to use `--force` to override old symlinks.

 `$ ls -l /etc/systemd/system/display-manager.service`  `[...] /etc/systemd/system/display-manager.service -> /usr/lib/systemd/system/kdm.service` 

### Using systemd-logind

In order to check the status of your user session, you can use _loginctl_. All [polkit](/index.php/Polkit "Polkit") actions like suspending the system or mounting external drives will work out of the box.

```
$ loginctl show-session $XDG_SESSION_ID

```

## Tips and tricks

### Run ~/.xinitrc as a session

Installing [xinit-xsession](https://aur.archlinux.org/packages/xinit-xsession/)<sup><small>AUR</small></sup> will provide an option to run your .xinitrc as a session

### Session list

Many display managers read available sessions from `/usr/share/xsessions/` directory. It contains standard [desktop entry files](http://standards.freedesktop.org/desktop-entry-spec/latest/) for each DM/WM.

To add/remove entries to your display manager's session list; create/remove the _.desktop_ files in `/usr/share/xsessions/` as desired. A typical _.desktop_ file will look something like:

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

### Starting applications without a window manager

You can also launch an application without any decoration, desktop, or window management. For example to launch [google-chrome](https://aur.archlinux.org/packages/google-chrome/)<sup><small>AUR</small></sup> create a `web-browser.desktop` file in `/usr/share/xsessions/` like this:

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

It is important to remember that most graphical applications are not intended to be launched this way and you might have manual tweaking to do or limitations to live with (there is no window manager, so do not expect to be able to move or resize _any_ windows, including dialogs; nonetheless, you might be able to set the window geometry in the application's configuration files).

See also [xinitrc#Starting applications without a window manager](/index.php/Xinitrc#Starting_applications_without_a_window_manager "Xinitrc").

### Autostarting

Most of display managers sources `/etc/xprofile`, `~/.xprofile` and `/etc/X11/xinit/xinitrc.d/`. For more details, see [xprofile](/index.php/Xprofile "Xprofile").

### Set the language

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** This seems to change the locale of the user session but not of the DM itself. Probably better to link to [Locale#Setting the locale](/index.php/Locale#Setting_the_locale "Locale"). (Discuss in [Talk:Display manager#](https://wiki.archlinux.org/index.php/Talk:Display_manager))

For display managers that use [AccountsService](http://freedesktop.org/wiki/Software/AccountsService/) the display manager [locale](/index.php/Locale "Locale") can be set by editing `/var/lib/AccountsService/users/$USER`:

```
[User]
Language=_your_locale_

```

where _your_locale_ is a value such as `en_GB.UTF-8`.

Restart your display manager for the changes to take effect.

## Known issues

### Incompatibility with systemd

_Affected DMs: Entrance, MDM_

Some display managers are not fully compatible with systemd, because they reuse the PAM session process. It causes various problems on second login, e.g.:

*   NetworkManager applet does not work,
*   PulseAudio volume cannot be adjusted,
*   login failed into GNOME with another user.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Display_manager&oldid=411105](https://wiki.archlinux.org/index.php?title=Display_manager&oldid=411105)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Display managers](/index.php/Category:Display_managers "Category:Display managers")