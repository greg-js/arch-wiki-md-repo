# LightDM

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Display manager](/index.php/Display_manager "Display manager")
*   [GDM](/index.php/GDM "GDM")
*   [KDM](/index.php/KDM "KDM")
*   [LXDM](/index.php/LXDM "LXDM")

[LightDM](http://www.freedesktop.org/wiki/Software/LightDM) is a cross-desktop [display manager](/index.php/Display_manager "Display manager") that aims to be the standard display manager for the X server. Its key features are:

*   A lightweight codebase
*   Standards compliant (PAM, logind, etc)
*   A well defined interface between the server and the user interface.
*   Cross-desktop (user interfaces can be written in any toolkit).

More details about LightDM's design can be found [here](http://www.freedesktop.org/wiki/Software/LightDM/Design).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Greeter](#Greeter)
*   [2 Enabling LightDM](#Enabling_LightDM)
*   [3 Command line tool](#Command_line_tool)
*   [4 Testing](#Testing)
*   [5 Optional configuration and tweaks](#Optional_configuration_and_tweaks)
    *   [5.1 Changing background images/colors](#Changing_background_images.2Fcolors)
        *   [5.1.1 GTK+ greeter](#GTK.2B_greeter)
        *   [5.1.2 Unity greeter](#Unity_greeter)
        *   [5.1.3 KDE greeter](#KDE_greeter)
    *   [5.2 Changing your avatar](#Changing_your_avatar)
    *   [5.3 Sources of Arch-centric 64x64 icons](#Sources_of_Arch-centric_64x64_icons)
    *   [5.4 Enabling autologin](#Enabling_autologin)
    *   [5.5 Enabling interactive passwordless login](#Enabling_interactive_passwordless_login)
    *   [5.6 Hiding system and services users](#Hiding_system_and_services_users)
    *   [5.7 Migrating from SLiM](#Migrating_from_SLiM)
    *   [5.8 NumLock on by default](#NumLock_on_by_default)
    *   [5.9 User switching under Xfce4](#User_switching_under_Xfce4)
    *   [5.10 Default session](#Default_session)
    *   [5.11 Adjusting the login window's position](#Adjusting_the_login_window.27s_position)
        *   [5.11.1 GTK+ greeter](#GTK.2B_greeter_2)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Wrong locale displayed](#Wrong_locale_displayed)
    *   [6.2 Xresources not being parsed correctly](#Xresources_not_being_parsed_correctly)
    *   [6.3 Missing icons with GTK greeter](#Missing_icons_with_GTK_greeter)
    *   [6.4 LightDM freezes on login attempt](#LightDM_freezes_on_login_attempt)
    *   [6.5 LightDM displaying in wrong monitor](#LightDM_displaying_in_wrong_monitor)
    *   [6.6 LightDM doesn't appear](#LightDM_doesn.27t_appear)
    *   [6.7 Pulseaudio not starting automatically](#Pulseaudio_not_starting_automatically)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [lightdm](https://www.archlinux.org/packages/?name=lightdm). Note that stable releases are even-numbered (1.8, 1.10) while development releases are odd-numbered (1.9, 1.11). These development releases are available with [lightdm-devel](https://aur.archlinux.org/packages/lightdm-devel/)<sup><small>AUR</small></sup>. Also available is [lightdm-bzr](https://aur.archlinux.org/packages/lightdm-bzr/)<sup><small>AUR</small></sup>.

### Greeter

You will probably want to install a greeter. A greeter is a GUI that prompts the user for credentials, lets the user select a session and so on. It's also possible to use LightDM without a greeter, but only if an automatic login is configured. The reference greeter is [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter). LightDM attempts to use this greeter when started unless configured to do otherwise.

The official repositories contain an alternative greeter, [lightdm-kde-greeter](https://www.archlinux.org/packages/?name=lightdm-kde-greeter). It is Qt-based and integrates well with KDE. Other greeters can be installed from the [AUR](/index.php/AUR "AUR"):

*   lightdm-deepin-greeter ([deepin-session-ui](https://www.archlinux.org/packages/?name=deepin-session-ui)): A greeter from the [Deepin](/index.php/Deepin_Desktop_Environment "Deepin Desktop Environment") project.
*   [lightdm-webkit-greeter](https://aur.archlinux.org/packages/lightdm-webkit-greeter/)<sup><small>AUR</small></sup>: A greeter that uses Webkit for theming.
*   [lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/)<sup><small>AUR</small></sup>: The greeter used by Ubuntu's [Unity](/index.php/Unity "Unity").
*   [lightdm-pantheon-greeter](https://aur.archlinux.org/packages/lightdm-pantheon-greeter/)<sup><small>AUR</small></sup>: A greeter from the elementary OS project.

You can set the default greeter by changing the `[Seat:*]` section of the LightDM configuration file, like so:

 `/etc/lightdm/lightdm.conf` 

```
[Seat:*]
...
greeter-session=lightdm-yourgreeter-greeter
```

Which greeters are available? What values may be assigned to the `greeter-session` option? Each `.desktop` file in the `/usr/share/xgreeters` directory denotes an available greeter. In this example, the `lightdm-gtk-greeter` and `lightdm-kde-greeter` greeters are available:

```
$ ls -1 /usr/share/xgreeters/
lightdm-gtk-greeter.desktop
lightdm-kde-greeter.desktop

```

## Enabling LightDM

Make sure to [enable](/index.php/Enable "Enable") `lightdm.service` so LightDM will be started at boot.

## Command line tool

LightDM offers a command line tool, `dm-tool`, which can be used to lock the current seat, switch sessions, etc, which is useful with 'minimalist' window managers and for testing. To see a list of available commands, execute:

```
$ dm-tool --help

```

## Testing

First, [install](/index.php/Pacman "Pacman") [xorg-server-xephyr](https://www.archlinux.org/packages/?name=xorg-server-xephyr) from the [official repositories](/index.php/Official_repositories "Official repositories").

Then, run LightDM as an X application:

```
$ lightdm --test-mode --debug

```

## Optional configuration and tweaks

Some greeters have their own configuration files. For example, [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) has:

```
/etc/lightdm/lightdm-gtk-greeter.conf

```

and [lightdm-kde-greeter](https://www.archlinux.org/packages/?name=lightdm-kde-greeter) has:

```
/etc/lightdm/lightdm-kde-greeter.conf

```

as well as a section in KDE's System Settings (recommended).

LightDM can be configured by modifying its configuration script, `/etc/lightdm/lightdm.conf`.

### Changing background images/colors

Users wishing to have a flat color (no image) may simply set the `background` variable to a hex color.

Example:

```
background=#000000

```

If you want to use an image instead, see below.

#### GTK+ greeter

You can use the [lightdm-gtk-greeter-settings](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter-settings) gui.

Users wishing to customize the wallpaper on the greeter screen need to edit `/etc/lightdm/lightdm-gtk-greeter.conf` and define the `background` variable under the `[greeter]` section. For example:

 `/etc/lightdm/lightdm-gtk-greeter.conf` 

```
[greeter]
background=/usr/share/pixmaps/black_and_white_photography-wallpaper-1920x1080.jpg
```

**Note:** It is recommended to place the PNG or JPG file in `/usr/share/pixmaps` since the LightDM user needs read access to the wallpaper file.

#### Unity greeter

Users using the [lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/)<sup><small>AUR</small></sup> must edit the `/usr/share/glib-2.0/schemas/com.canonical.unity-greeter.gschema.xml` file and then execute:

```
# glib-compile-schemas /usr/share/glib-2.0/schemas/

```

According to [this](https://bbs.archlinux.org/viewtopic.php?id=149945) page.

#### KDE greeter

Go to _System Settings > Login Screen (LightDM)_ and change the background image for your theme.

Alternatively, you can edit the `Background` variable in `lightdm-kde-greeter.conf` :

 `/etc/lightdm/lightdm-kdm-greeter.conf` 

```
[greeter]
theme-name=classic

[greeter-settings]
Background=/usr/share/archlinux/wallpaper/archlinux-underground.jpg
BackgroundKeepAspectRatio=true
GreetMessage=Welcome to %hostname%
```

### Changing your avatar

**Tip:** If you are using KDE, you can change your avatar in KDE System Settings.

First, make sure the [accountsservice](https://www.archlinux.org/packages/?name=accountsservice) package from the [official repositories](/index.php/Official_repositories "Official repositories") is installed, then set it up as follows, replacing `_username_` with the desired user's login name. The _.png_ file extension should not be included in the filename.

*   Edit or create the file `/var/lib/AccountsService/users/_username_`, and add the lines

```
[User]
Icon=/var/lib/AccountsService/icons/_username_

```

*   Create the file `/var/lib/AccountsService/icons/_username_` using a 96x96 PNG image file.

**Note:** Make sure that both created files have 644 permissions, use [chmod](/index.php/Chmod "Chmod") to correct them.

### Sources of Arch-centric 64x64 icons

The [archlinux-artwork](https://aur.archlinux.org/packages/archlinux-artwork/)<sup><small>AUR</small></sup> package from the [AUR](/index.php/AUR "AUR") contains some nice examples that install to `/usr/share/archlinux/icons` and that can be copied to `/usr/share/icons/hicolor/64x64/devices` as follows:

```
# find /usr/share/archlinux/icons -name "*64*" -exec cp {} /usr/share/icons/hicolor/64x64/devices \;

```

After copying, the [archlinux-artwork](https://aur.archlinux.org/packages/archlinux-artwork/)<sup><small>AUR</small></sup> package can be removed.

### Enabling autologin

Edit the LightDM configuration file and ensure these lines are uncommented and correctly configured:

 `/etc/lightdm/lightdm.conf` 

```
[Seat:*]
pam-service=lightdm
pam-autologin-service=lightdm-autologin
autologin-user=_username_
autologin-user-timeout=0
session-wrapper=/etc/lightdm/Xsession
```

LightDM goes through PAM even when `autologin` is enabled. You must be part of the `autologin` group to be able to login automatically without entering your password:

```
# groupadd -r autologin
# gpasswd -a _username_ autologin

```

**Note:** GNOME users, and by extension any gnome-keyring user will have to set up a blank password to their keyring for it to be unlocked automatically.

### Enabling interactive passwordless login

LightDM goes through PAM so you must configure the lightdm configuration of PAM:

 `/etc/pam.d/lightdm` 

```
#%PAM-1.0
**auth        sufficient  pam_succeed_if.so user ingroup nopasswdlogin**
auth        include     system-login
...
```

You must then also be part of the `nopasswdlogin` group to be able to login interactively without entering your password:

```
# groupadd -r nopasswdlogin
# gpasswd -a _username_ nopasswdlogin

```

**Note:** GNOME users, and by extension any gnome-keyring user may have to follow the instructions at the end of the previous section on enabling autologin.

To create a new user account that logs in automatically and additionally able to login again without a password the user can be created with supplementary membership of both groups, e.g.:

```
# useradd -mG autologin,nopasswdlogin -s /bin/bash _username_

```

### Hiding system and services users

To prevent system users from showing-up in the login, install the optional dependency [accountsservice](https://www.archlinux.org/packages/?name=accountsservice), or add the user names to `/etc/lightdm/users.conf` under `hidden-users`. The first option has the advantage of not needing to update the list when more users are added or removed.

### Migrating from SLiM

Move the contents of [xinitrc](/index.php/Xinitrc "Xinitrc") to [xprofile](/index.php/Xprofile "Xprofile"), removing the call to start the [window manager](/index.php/Window_manager "Window manager") or [desktop environment](/index.php/Desktop_environment "Desktop environment").

### NumLock on by default

Install the [numlockx](https://www.archlinux.org/packages/?name=numlockx) package and the edit `/etc/lightdm/lightdm.conf` adding the following line:

```
greeter-setup-script=/usr/bin/numlockx on

```

### User switching under Xfce4

If you use the [Xfce](/index.php/Xfce "Xfce") desktop, the Switch User functionality of the Action Button found in your Application Launcher specifically looks for the _gdmflexiserver_ executable in order to enable itself. If you provide it with an executable shell script `/usr/bin/gdmflexiserver` consisting of

```
#!/bin/sh
/usr/bin/dm-tool switch-to-greeter

```

then user switching in Xfce should work with Lightdm.

Alternatively, if you use the Whisker Menu, you can go to Properties -> Commands and change the "Switch Users" command directly to:

```
 dm-tool switch-to-greeter

```

You can also switch users from the [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") lock screen - see [XScreenSaver#LightDM](/index.php/XScreenSaver#LightDM "XScreenSaver").

### Default session

Lightdm, like other DMs, stores the last-selected xsession in `~/.dmrc`. See [Display manager#Session list](/index.php/Display_manager#Session_list "Display manager") for more info.

### Adjusting the login window's position

#### GTK+ greeter

Users need to edit `/etc/lightdm/lightdm-gtk-greeter.conf` and enter a value for the `position` variable. It accepts `x` and `y` values, either absolute (in pixels) or relative (in percent). Each value can also have an additional anchor location for the window, `start`, `center` and `end` separated from the value by a comma.

Example:

```
position=200,start 50%,center

```

## Troubleshooting

If you encounter consistent screen flashing and ultimately no LightDM on boot, ensure that you have defined the greeter correctly in LightDM's config file. And if you have correctly defined the GTK greeter, make sure the `xsessions-directory` (default: `/usr/share/xsessions`) exists and contains at least one .desktop file.

The same error can happen on lightdm startup if the last used session is not available anymore (eg. you last used gnome and then removed the gnome-session package): the easiest workaround is to temporarily restore the removed package. Another solution might be:

```
# dbus-send --system --type=method_call --print-reply --dest=org.freedesktop.Accounts /org/freedesktop/Accounts/User1000 org.freedesktop.Accounts.User.SetXSession string:xfce

```

This example sets the session "xfce" as default for the user 1000.

### Wrong locale displayed

In case of your locale not being displayed correctly in Lightdm add your locale to `/etc/environment`

```
 LANG=pt_PT.utf8

```

### Xresources not being parsed correctly

LightDM has an [upstream bug](https://bugs.launchpad.net/lightdm/+bug/1084885) where your [Xresources](/index.php/Xresources "Xresources") file will not be loaded with a pre-processor. In practical terms, this means that variables set with `#define` are not expanded when called later. You may see this reflected as an all-pink screen if using a custom color set with urxvt. To fix it, edit `/etc/lightdm/Xsession` and search for the line:

```
xrdb -nocpp -merge "$file"

```

Change it to read:

```
xrdb -merge "$file"

```

Your Xresources will now be pre-processed so that variables are correctly expanded.

### Missing icons with GTK greeter

If you're using [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) as a greeter and it shows placeholder images as icons, make sure valid icon themes and themes are installed and configured. Check the following file:

 `/etc/lightdm/lightdm-gtk-greeter.conf` 

```
[greeter]
theme-name=mate      # this should be the name of a directory under /usr/share/themes/
icon-theme-name=mate # this should be the name of a fully featured icons set directory under /usr/share/icons/
```

### LightDM freezes on login attempt

You may find that after entering the correct username and password and attempting to log in, LightDM freezes and you are unable to continue to the desktop. To fix the issue, reinstall the [gdk-pixbuf2](https://www.archlinux.org/packages/?name=gdk-pixbuf2) package. See [this forum thread](https://bbs.archlinux.org/viewtopic.php?id=179031).

### LightDM displaying in wrong monitor

If you are using multiple monitors, LightDM may display in the wrong one (e.g. if your primary monitor is on the right). To force the LightDM login screen to display on a specific monitor, edit `/etc/lightdm/lightdm.conf` and change the _display-setup-script_ parameter like this:

 `/etc/lightdm/lightdm.conf`  `display-setup-script=xrandr --output _HDMI1_ --primary` 

Replace _HDMI1_ with your real monitor ID, which you can find from **xrandr** command output.

### LightDM doesn't appear

It may happen that your system boots so fast that LightDM service is started before your graphics drivers are properly loaded. If this is your case, you'll want to add the following config to your lightdm.conf file:

```
   [LightDM]
   logind-check-graphical=true

```

This setting will tell LightDM to wait until graphics devices are ready before spawning greeters/autostarting sessions on them.

### Pulseaudio not starting automatically

See [PulseAudio#Running](/index.php/PulseAudio#Running "PulseAudio").

## See also

*   [light-locker](https://www.archlinux.org/packages/?name=light-locker), a screen locker using LightDM.
*   [Ubuntu Wiki article](https://wiki.ubuntu.com/LightDM)
*   [Gentoo Wiki article](http://wiki.gentoo.org/wiki/LightDM)
*   [Launchpad Page](https://launchpad.net/lightdm)
*   [LightDM blog](http://www.mattfischer.com/blog/?tag=lightdm)

Retrieved from "[https://wiki.archlinux.org/index.php?title=LightDM&oldid=411852](https://wiki.archlinux.org/index.php?title=LightDM&oldid=411852)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Display managers](/index.php/Category:Display_managers "Category:Display managers")