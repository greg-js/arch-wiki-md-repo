# KDM

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** KDM is no longer available in the official repositories.[[1]](https://www.archlinux.org/news/dropping-plasma-4/) (Discuss in [Talk:KDM#](https://wiki.archlinux.org/index.php/Talk:KDM))

Related articles

*   [Display manager](/index.php/Display_manager "Display manager")
*   [KDE](/index.php/KDE "KDE")

KDM (KDE Display Manager) is the login manager of [KDE](/index.php/KDE "KDE"). It supports themes, auto-logging, session type choice, and numerous other features.

**Note:** **KDM** is not available anymore in Plasma 5\. Using [SDDM](/index.php/SDDM "SDDM") as DM is recommended, as it provides better integration with the Plasma 5 theme.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Themes](#Themes)
    *   [2.2 Themes creation](#Themes_creation)
        *   [2.2.1 ServerArgsLocal](#ServerArgsLocal)
        *   [2.2.2 Allow root login](#Allow_root_login)
        *   [2.2.3 SessionsDirs](#SessionsDirs)
        *   [2.2.4 Session](#Session)
        *   [2.2.5 Restart X server menu option](#Restart_X_server_menu_option)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Keyboard maps](#Keyboard_maps)
    *   [3.2 Slow KDM start](#Slow_KDM_start)
    *   [3.3 KDM and Gnome-keyring](#KDM_and_Gnome-keyring)
    *   [3.4 User picture not displayed](#User_picture_not_displayed)
    *   [3.5 Input freeze while locking screen](#Input_freeze_while_locking_screen)

## Installation

[Install](/index.php/Install "Install") the [kdebase-workspace](https://www.archlinux.org/packages/?name=kdebase-workspace).

Then follow [Display manager#Loading the display manager](/index.php/Display_manager#Loading_the_display_manager "Display manager") to start KDM at boot.

## Configuration

The configuration file for KDM can be found at `/usr/share/config/kdm/kdmrc`. See `/usr/share/doc/HTML/en/kdm/kdmrc-ref.docbook` for all options.

You can visit _System Settings > Login Screen_ and make your changes. Whenever you press _Apply_, a _KDE Polkit authorization_ window appears which will ask you to give your root password in order to finish the changes.

If you seem not to be able to edit KDM's settings when launching System Settings as user, you can use _kdesu_:

```
$ kdesu kcmshell4 kdm

```

In the pop-up _kdesu_ window, enter your root password and wait for System Settings to be launched. Then go to "Login Screen".

**Note:** Since you have launched it as root, be careful when changing your settings. All settings configuration in root-launched System Settings are saved under `/root/.kde4` and not under `~/.kde4` (your home location).

### Themes

Arch Linux KDM themes can be installed through [archlinux-themes-kdm](https://www.archlinux.org/packages/?name=archlinux-themes-kdm) package.

Many other KDM 4 themes are available at [http://kde-look.org/index.php?xcontentmode=41](http://kde-look.org/index.php?xcontentmode=41). Choose between the installed themes in System Settings (run as root) as described above.

### Themes creation

Themes files are in `/usr/share/apps/kdm/themes`.

The theme format is the same one as GDM, a documentation can be found here: [Detailed Description of Theme XML format](http://projects.gnome.org//gdm/docs/2.18/thememanual.html#descofthemeformat).

#### ServerArgsLocal

To force the number of dots per inch of the X server, add a -dpi option to ServerArgsLocal. A commonly used value is 96 dpi.

 `/usr/share/config/kdm/kdmrc` 

```
[...]
ServerArgsLocal=-dpi 96 -nolisten tcp
[...]
```

#### Allow root login

To allow root login in KDM do:

```
# sed -ie 's/AllowRootLogin=false/AllowRootLogin=true/' /usr/share/config/kdm/kdmrc

```

#### SessionsDirs

This variable stores a list of directories containing session type definitions in `.desktop` format, ordered by falling priority. In Arch Linux some [window managers](/index.php/Window_managers "Window managers") install such files in `/usr/share/xsessions`. Add that to the list in order to be able to select them in KDM:

 `/usr/share/config/kdm/kdmrc` 

```
[...]
SessionsDirs=/usr/share/config/kdm/sessions,/usr/share/apps/kdm/sessions,/usr/share/xsessions
[...]
```

#### Session

The Session variable is the name of a program which is run as the user who logs in. It is supposed to interpret the session argument (see SessionsDirs) and start the session as desired for that argument. One may wish to customize this for window manager sessions, for example to set a wallpaper and start a screensaver. To do this in a way which will survive pacman updates (which clobber Xsession) do as follows:

```
# cp /usr/share/config/kdm/Xsession /usr/share/config/kdm/Xsession.custom

```

In `kdmrc` set:

 `/usr/share/config/kdm/kdmrc` 

```
[...]
Session=/usr/share/config/kdm/Xsession.custom
[...]
```

And then edit `Xsession.custom` as desired.

#### Restart X server menu option

To allow users to restart the X server from KDM, edit this option in `kdmrc`:

 `/usr/share/config/kdm/kdmrc` 

```
[X-:*-Greeter]
[...]
# Show the "Restart X Server"/"Close Connection" action in the greeter.
# Default is true
AllowClose=true
[...]
```

This feature will be available in the menu drop-down options. The option also includes a hotkey of `Alt+e`.

## Troubleshooting

### Keyboard maps

KDM keyboard keymap can be set through the configuration system (login screen section).

If setting the language in the configuration system does not affect keyboard map, you can try to edit /usr/share/config/kdm/Xsetup and add command:

```
setxkbmap cz

```

where `cz` is the Czech keyboard layout. Since the file may get overwritten on the next upgrade, you may want to protect it in /etc/pacman.conf:

```
NoUpgrade = usr/share/config/kdm/Xsetup

```

**Note:** The leading slash (`/`) must not be there.

### Slow KDM start

If KDM is taking a long time to display the login screen (e.g. 15-30 seconds) you may try rebuilding the X font caches:

```
# fc-cache -fv

```

### KDM and Gnome-keyring

To automatically unlock the [Gnome-keyring](/index.php/Gnome-keyring "Gnome-keyring") upon login in KDM add the following line to your `/etc/pam.d/kde` right after the `auth include system-login` line:

```
auth            optional        pam_gnome_keyring.so

```

and add

```
session         optional        pam_gnome_keyring.so auto_start

```

after `session include system-login`

To automatically re-unlock the keyring when you unlock your screensaver open `/etc/pam.d/kscreensaver` and add

```
auth            optional        pam_gnome_keyring.so

```

as the last line.

### User picture not displayed

For KDM to able to display user picture set in Account Information, proper source must be set in `System Settings > Login Screen > Users > User Image Source`, user's home directory must be world executable and `~/.face.icon` must be world readable [[2]](http://docs.kde.org/stable/en/kde-workspace/kdm/kdm-files.html#option-facesource):

```
$ chmod o+x ~/
$ chmod o+r ~/.face.icon

```

### Input freeze while locking screen

If the input freezes while starting the lock screen you can unlock it by switching to another virtual console (CTRL-ALT-F1 for example) and restarting KDM:

```
$ systemctl stop kdm && systemctl start kdm

```

Switch back to your original virtual console and you should be able to unlock the screen. This behaviour is due to [bug 314663](https://bugs.kde.org/show_bug.cgi?id=314663).

As a workaround you disable background opacity for `kscreenlocker` and `kscreenlocker_greet`.

For `qt-curve`, go to `System Settings > Application Appearance > Style > Configure > Applications` and add `kscreenlocker` and `kscreenlocker_greet` to "No background opacity".

Retrieved from "[https://wiki.archlinux.org/index.php?title=KDM&oldid=411733](https://wiki.archlinux.org/index.php?title=KDM&oldid=411733)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [KDE](/index.php/Category:KDE "Category:KDE")
*   [Display managers](/index.php/Category:Display_managers "Category:Display managers")