# SDDM

The [Simple Desktop Display Manager](https://en.wikipedia.org/wiki/Simple_Desktop_Display_Manager "wikipedia:Simple Desktop Display Manager") (SDDM) is the preferred [display manager](/index.php/Display_manager "Display manager") for [KDE](/index.php/KDE "KDE") Plasma desktop. From Wikipedia:

	_Simple Desktop Display Manager (SDDM) is a display manager (a graphical login program) for X11\. SDDM was written from scratch in C++11 and supports theming via QML. It is the successor of the KDE Display Manager and is used in conjunction with KDE Frameworks 5, KDE Plasma 5 and KDE Applications 5._

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Autologin](#Autologin)
    *   [2.2 Theme settings](#Theme_settings)
        *   [2.2.1 Main theme](#Main_theme)
        *   [2.2.2 Editing themes](#Editing_themes)
        *   [2.2.3 Mouse cursor](#Mouse_cursor)
        *   [2.2.4 Changing your avatar](#Changing_your_avatar)
    *   [2.3 Numlock](#Numlock)
    *   [2.4 Configuration GUI](#Configuration_GUI)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Hangs after login](#Hangs_after_login)
    *   [3.2 Incorrect, custom monitor resolution(s)](#Incorrect.2C_custom_monitor_resolution.28s.29)
    *   [3.3 SDDM starts on tty1 instead of tty7](#SDDM_starts_on_tty1_instead_of_tty7)
    *   [3.4 One or more users do not show up on the greeter](#One_or_more_users_do_not_show_up_on_the_greeter)
    *   [3.5 SDDM loads only US keyboard layout](#SDDM_loads_only_US_keyboard_layout)

## Installation

[Install](/index.php/Install "Install") the [sddm](https://www.archlinux.org/packages/?name=sddm) package.

Then follow [Display manager#Loading the display manager](/index.php/Display_manager#Loading_the_display_manager "Display manager") to start SDDM at boot.

## Configuration

The configuration file for SDDM can be found at `/etc/sddm.conf`. See `man sddm.conf` for all options.

On systems controlled by [systemd](/index.php/Systemd "Systemd"), everything should work out of the box, since SDDM defaults to using `systemd-logind` for session management. The configuration file will therefore not be created at package installation time. SDDM offers a command for generating a sample configuration file with the default settings if you really want one:

```
# sddm --example-config > /etc/sddm.conf

```

### Autologin

SDDM supports automatic login through its configuration file, for example:

 `/etc/sddm.conf` 

```
[Autologin]
User=john
Session=plasma.desktop
```

This configuration causes a KDE Plasma session to be started for user `john` when the system is booted. Available session types can be found in `/usr/share/xsessions/` directory.

An option to autologin into KDE Plasma while simultaneously locking the session is not available [[1]](https://github.com/sddm/sddm/issues/306)

You can add a script that activates the screensaver of KDE to the autostart as a workaround:

```
#!/bin/bash                                                                                                                                                         
/usr/bin/qdbus-qt4 org.kde.screensaver /ScreenSaver SetActive true &
exit 0

```

### Theme settings

Theme settings can be changed in the `[Theme]` section.

Set to `breeze` for the default Plasma theme.

Some themes are available in the [AUR](/index.php/AUR "AUR"), for example [archlinux-themes-sddm](https://aur.archlinux.org/packages/archlinux-themes-sddm/).

#### Main theme

Set the main theme through the `Current` value, e.g. `Current=archlinux-simplyblack`.

#### Editing themes

The default SDDM theme directory is `/usr/share/sddm/themes/`. You can add your custom made themes to that directory under a seperate subdirectory. Study the files installed to modify or create your own theme.

#### Mouse cursor

To set the mouse cursor theme, set `CursorTheme` to your preferred cursor theme.

Valid [Plasma](/index.php/Plasma "Plasma") mouse cursor theme names are `breeze_cursors`, `Breeze_Snow` and `breeze-dark`.

#### Changing your avatar

You can simply put a png image named `username.face.icon` into the default directory `/usr/share/sddm/faces/`. Alternatively you can change the default directory to match your desires:

 `/etc/sddm.conf` 

```
[Theme]
FacesDir=/var/lib/AccountsService/icons/
```

You can also put a png image named `.face.icon` at the root of your home directory. However, you need to make sure that `sddm` user can read that file.

**Note:** SDDM cannot read avatars which are symlinks.

### Numlock

If you want to enforce Numlock to be enabled, set `Numlock=on` in the `[General]` section.

### Configuration GUI

*   KDE Frameworks' System Settings contains an SDDM configuration module. Install [sddm-kcm](https://www.archlinux.org/packages/?name=sddm-kcm) package to use it.
*   There is a Qt-based [sddm-config-editor-git](https://aur.archlinux.org/packages/sddm-config-editor-git/) in the AUR.

## Troubleshooting

### Hangs after login

Try removing _~/.Xauthority_.

Alternatively, if your cursor turns to a black cross at the same time, and you are using zsh as your shell, you may be experiencing [this bug](https://github.com/sddm/sddm/issues/352). Follow the instructions in the previous link to fix the issue. This bug is expected to be fixed in the SDDM version subsequent to 0.11.0.

### Incorrect, custom monitor resolution(s)

To execute commands when starting [Xorg](/index.php/Xorg "Xorg"), edit the `/usr/share/sddm/scripts/Xsetup` file.

By using the output of a script generated by [arandr](https://www.archlinux.org/packages/?name=arandr), this may fix incorrect or help setup custom monitor resolutions.

### SDDM starts on tty1 instead of tty7

SDDM follows the [systemd convention](http://0pointer.de/blog/projects/serial-console.html) of starting the first graphical session on tty1\. If you prefer the old convention where tty1 through tty6 are reserved for text consoles, add the following to your `sddm.conf`:

 `/etc/sddm.conf` 

```
[XDisplay]
MinimumVT=7
```

### One or more users do not show up on the greeter

**Warning:** Users set with a lower or higher `UID` range should generally not be exposed to a [Display manager](/index.php/Display_manager "Display manager").

SDDM only displays users with a UID in the range of 1000 to 65000 by default, if the UIDs of the desired users are below this value then you will have to modify this range. Modify your `sddm.conf` to (for a UID of 501, say):

 `/etc/sddm.conf` 

```
[Users]
HideShells=/sbin/nologin,/bin/false
# Hidden users, this is if any system users fall within your range, see /etc/passwd on your system.
HideUsers=git,sddm,systemd-journal-remote,systemd-journal-upload

# Maximum user id for displayed users
MaximumUid=65000

# Minimum user id for displayed users
MinimumUid=500 #My UID is 501
```

### SDDM loads only US keyboard layout

SDDM loads the keyboard layout specified in `/etc/X11/xorg.conf.d/00-keyboard.conf`. You can generate this configuration file by `localectl set-x11-keymap` command. See [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") for more information.

Retrieved from "[https://wiki.archlinux.org/index.php?title=SDDM&oldid=416512](https://wiki.archlinux.org/index.php?title=SDDM&oldid=416512)"