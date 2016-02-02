# IceWM

According to [Wikipedia](https://en.wikipedia.org/wiki/Icewm "wikipedia:Icewm"):

	_IceWM is a window manager for the X Window System graphical infrastructure, written by Marko Maček. It was coded from scratch in C++ and is released under the terms of the GNU Lesser General Public License. It is relatively lightweight in terms of memory and CPU usage, and comes with themes that allow it to imitate the UI of Windows 95, OS/2, Motif, and other graphical user interfaces._

## Contents

*   [1 Installation](#Installation)
*   [2 Starting IceWM](#Starting_IceWM)
*   [3 Configuration](#Configuration)
    *   [3.1 Autostarting](#Autostarting)
    *   [3.2 Generating menu entries](#Generating_menu_entries)
    *   [3.3 Themes](#Themes)
    *   [3.4 Desktop icons](#Desktop_icons)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Compositing](#Compositing)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 No start menu icon (Intel graphics)](#No_start_menu_icon_.28Intel_graphics.29)
    *   [5.2 Unable to logout when PCManFM is managing the desktop](#Unable_to_logout_when_PCManFM_is_managing_the_desktop)
    *   [5.3 No shutdown or reboot options in logout menu](#No_shutdown_or_reboot_options_in_logout_menu)
*   [6 See also](#See_also)

## Installation

IceWM can be [installed](/index.php/Installed "Installed") with the [icewm](https://www.archlinux.org/packages/?name=icewm) package.

A forked version of IceWM exists on [GitHub](https://github.com/bbidulock/icewm). It can be installed from either of the following: [icewm2](https://aur.archlinux.org/packages/icewm2/)<sup><small>AUR</small></sup>, [icewm-git](https://aur.archlinux.org/packages/icewm-git/)<sup><small>AUR</small></sup>.

## Starting IceWM

**Graphical login**

Just select _IceWM_ from the session menu of your favourite [display manager](/index.php/Display_manager "Display manager").

**Manually**

For a basic session, append the following to `~/.xinitrc`

```
exec icewm

```

To run icewm, icewmbg and icewmtray with your IceWM session, append the following to `~/.xinitrc`

```
exec icewm-session

```

See [xinitrc](/index.php/Xinitrc "Xinitrc") for details, such as preserving the logind session.

## Configuration

Although IceWM configuration is originally text-based, there are GUI-based tools available, notably [icewm-utils](https://aur.archlinux.org/packages/icewm-utils/)<sup><small>AUR</small></sup> in the [AUR](/index.php/AUR "AUR"). However these tools are relatively old and most users prefer to simply edit the text configuration files. Configuration changes from defaults can be made either system wide (in `/etc/icewm/`) or on a user-specific basis (in `~/.icewm/`).

To change your icewm configuration from the default, simply copy the default configuration files from `/usr/share/icewm/` to `~/.icewm/`, for example:

**Note:** Do this as a regular user, not as root.

```
$ mkdir ~/.icewm/
$ cp -R /usr/share/icewm/* ~/.icewm/

```

*   `preferences` is the core configuration file for IceWM.
*   `menu` controls the contents of the IceWM application menu.
*   `keys` allows the user to customize keyboard shortcuts
*   `toolbar` row of launcher icons on the taskbar
*   `winoptions` behavior of individual applications
*   `theme` theme path/name
*   `startup` script or command (must be executable) executed on startup
*   `shutdown` the same for shutdown

### Autostarting

The `startup` script is **not** provided by the [icewm](https://www.archlinux.org/packages/?name=icewm) package so you will need to create it yourself.

```
$ touch ~/.icewm/startup
$ chmod +x ~/.icewm/startup

```

Then open the file in your favourite text editor and add the commands for the programs that you wish to start with the IceWM session.

**Note:** Startup commands that install system tray applets must be preceded by `sleep 1 &&`, otherwise IceWM will create an ugly black window that will prevent it from quitting; in that case, use xkill on the task bar.

Below is an example of an IceWM startup script which starts [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) and [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") with the IceWM session:

 `~/.icewm/startup` 

```
#!/bin/bash

sleep 1 &&
nm-applet &

xscreensaver -nosplash &

```

### Generating menu entries

*   [menumaker](https://www.archlinux.org/packages/?name=menumaker) from the official repositories is a Python script that automatically populates your applications menu based on what is installed in your system. Although this may result in a menu filled with many unwanted applications, it may still be preferable to manually editing the menu configuration file. When running MenuMaker, use the -f flag to overwrite an existing menu file:

```
$ mmaker -f icewm

```

You can avoid populating your menu with terminal based applications such as _alsamixer_ by running the following switches with the mmaker command: `--no-legacy` and `--no-debian`. For example:

```
$ mmaker -f --no-legacy --no-debian icewm

```

*   Alternatively, you can generate a menu using [Xdg-menu](/index.php/Xdg-menu "Xdg-menu"). See the [Xdg-menu#IceWM](/index.php/Xdg-menu#IceWM "Xdg-menu") section.

### Themes

A small number of themes are included in the [icewm](https://www.archlinux.org/packages/?name=icewm) package. These can supplemented by the themes available from the [icewm-themes](https://www.archlinux.org/packages/?name=icewm-themes) package. Many more themes can be downloaded from [box-look.org](http://www.box-look.org/index.php?xcontentmode=7311).

### Desktop icons

A file manager such as [PCManFM](/index.php/PCManFM "PCManFM") or Rox Filer can manage the wallpaper and add desktop icons. Alternatively, you could install [Idesk](/index.php/Idesk "Idesk"), a small program that can also add icons to the desktop.

## Tips and tricks

### Compositing

IceWM is not a compositing window manager. If you need compositing with IceWM, you have the option of using a standalone composite manager such as [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") or [Compton](/index.php/Compton "Compton").

## Troubleshooting

### No start menu icon (Intel graphics)

If you are using IceWM with [Intel graphics](/index.php/Intel_graphics "Intel graphics") you may find that the start menu in your taskbar has no icon. This is due to a recent change in the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver which means that the new, but rather unstable, SNA acceleration backend is used by default. To fix the start menu issue (and other possible graphical glitches) you need to switch back to the older UXA backend. See the following article: [Intel graphics#SNA issues](/index.php/Intel_graphics#SNA_issues "Intel graphics").

### Unable to logout when PCManFM is managing the desktop

If you use [PCManFM](/index.php/PCManFM "PCManFM") to manage the desktop you may find that the IceWM logout button no longer works. As a workaround, you can define a logout command. This should allow you to logout whilst PCManFM is managing the desktop. To do this, open `~/.icewm/preferences`, uncomment the following line: `# LogoutCommand=""` and enter a command which can be used to logout. For example: `LogoutCommand="pkill -u username"` where username is your username.

### No shutdown or reboot options in logout menu

*   Logout command has been defined:

Shutdown and reboot commands will be ignored if a logout command has been defined. If you want shutdown and reboot options in the logout menu then you must not define a logout command.

*   Logout command has not been defined:

If you have defined shutdown and reboot commands (such as systemctl poweroff and systemctl reboot) and you have not defined a logout command but you still find that there are no shutdown or reboot options in the logout menu then update to `icewm 1.3.8-2`. See [FS#37884](https://bugs.archlinux.org/task/37884) for more information.

## See also

*   [Official IceWM website](http://www.icewm.org/)
*   [IceWM - The Cool Window Manager](http://www.osnews.com/story.php/7774/IceWM--The-Cool-Window-Manager/) - Detailed introduction on OSNews
*   [IceWM - A desktop for Windows emigrants](http://polishlinux.org/apps/window-managers/icewm-a-desktop-for-windows-emmigrants/) - Overview and tutorial from polishlinux.org

Retrieved from "[https://wiki.archlinux.org/index.php?title=IceWM&oldid=380950](https://wiki.archlinux.org/index.php?title=IceWM&oldid=380950)"