Related articles

*   [Display manager](/index.php/Display_manager "Display manager")
*   [GDM](/index.php/GDM "GDM")
*   [LXDM](/index.php/LXDM "LXDM")

[LightDM](http://www.freedesktop.org/wiki/Software/LightDM) is a cross-desktop [display manager](/index.php/Display_manager "Display manager"). Its key features are:

*   Cross-desktop - supports different desktop technologies.
*   Supports different display technologies (X, Mir, Wayland ...).
*   Lightweight - low memory usage and high performance.
*   Supports guest sessions.
*   Supports remote login (incoming - XDMCP, VNC, outgoing - XDMCP, pluggable).
*   Comprehensive test suite.
*   Low code complexity.

More details about LightDM's design can be found [here](http://www.freedesktop.org/wiki/Software/LightDM/Design).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Greeter](#Greeter)
*   [2 Enabling LightDM](#Enabling_LightDM)
*   [3 Command line tool](#Command_line_tool)
    *   [3.1 User switching](#User_switching)
*   [4 Testing](#Testing)
*   [5 Optional configuration and tweaks](#Optional_configuration_and_tweaks)
    *   [5.1 X session wrapper](#X_session_wrapper)
        *   [5.1.1 Environment variables](#Environment_variables)
        *   [5.1.2 Keymap](#Keymap)
    *   [5.2 Changing background images/colors](#Changing_background_images.2Fcolors)
        *   [5.2.1 GTK+ greeter](#GTK.2B_greeter)
            *   [5.2.1.1 GTK3 Theme](#GTK3_Theme)
        *   [5.2.2 Webkit2 greeter](#Webkit2_greeter)
        *   [5.2.3 Unity greeter](#Unity_greeter)
        *   [5.2.4 KDE greeter](#KDE_greeter)
        *   [5.2.5 Slick Greeter](#Slick_Greeter)
    *   [5.3 Changing your avatar](#Changing_your_avatar)
    *   [5.4 Sources of Arch-centric 64x64 icons](#Sources_of_Arch-centric_64x64_icons)
    *   [5.5 Enabling autologin](#Enabling_autologin)
    *   [5.6 Enabling interactive passwordless login](#Enabling_interactive_passwordless_login)
    *   [5.7 Hiding system and services users](#Hiding_system_and_services_users)
    *   [5.8 Migrating from SLiM](#Migrating_from_SLiM)
    *   [5.9 Login using ~/.xinitrc](#Login_using_.7E.2F.xinitrc)
    *   [5.10 NumLock on by default](#NumLock_on_by_default)
    *   [5.11 Default session](#Default_session)
    *   [5.12 Adjusting the login window's position](#Adjusting_the_login_window.27s_position)
        *   [5.12.1 GTK+ greeter](#GTK.2B_greeter_2)
    *   [5.13 VNC Server](#VNC_Server)
    *   [5.14 Lock the screen using light-locker](#Lock_the_screen_using_light-locker)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Wrong locale displayed](#Wrong_locale_displayed)
    *   [6.2 Missing icons with GTK greeter](#Missing_icons_with_GTK_greeter)
    *   [6.3 LightDM freezes on login attempt](#LightDM_freezes_on_login_attempt)
    *   [6.4 LightDM displaying in wrong monitor](#LightDM_displaying_in_wrong_monitor)
    *   [6.5 LightDM does not appear or monitor only displays TTY output](#LightDM_does_not_appear_or_monitor_only_displays_TTY_output)
    *   [6.6 Pulseaudio not starting automatically](#Pulseaudio_not_starting_automatically)
    *   [6.7 Long pause before LightDM shows up when home is encrypted](#Long_pause_before_LightDM_shows_up_when_home_is_encrypted)
    *   [6.8 Boot hangs on "[ OK ] Reached target Graphical Interface."](#Boot_hangs_on_.22.5B_OK_.5D_Reached_target_Graphical_Interface..22)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [lightdm](https://www.archlinux.org/packages/?name=lightdm) package.

**Tip:** Stable releases are even-numbered (1.8, 1.10) while development releases are odd-numbered (1.9, 1.11). These development releases are available with [lightdm-devel](https://aur.archlinux.org/packages/lightdm-devel/). Also available is [lightdm-git](https://aur.archlinux.org/packages/lightdm-git/).

### Greeter

You will probably want to install a greeter. A greeter is a GUI that prompts the user for credentials, lets the user select a session, and so on. It is possible to use LightDM without a greeter, but only if an automatic login is configured, otherwise you will need to install [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) and one of the greeter packages below.

The official repositories contain the following greeters:

*   [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter): this is the **default** greeter LightDM attempts to use when started unless configured to do otherwise.
*   lightdm-deepin-greeter ([deepin-session-ui](https://www.archlinux.org/packages/?name=deepin-session-ui)): A greeter from the [Deepin](/index.php/Deepin "Deepin") project.

Other alternative greeters are available in the [AUR](/index.php/AUR "AUR"):

*   [lightdm-slick-greeter](https://aur.archlinux.org/packages/lightdm-slick-greeter/): A GTK+ Based greeter that is preferred over the [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) by distro creators
*   [lightdm-webkit2-greeter](https://www.archlinux.org/packages/?name=lightdm-webkit2-greeter): A greeter that uses Webkit2 for theming. It supersedes [lightdm-webkit-greeter](https://aur.archlinux.org/packages/lightdm-webkit-greeter/).
*   [lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/): The greeter used by Ubuntu's [Unity](/index.php/Unity "Unity").
*   [lightdm-pantheon-greeter](https://aur.archlinux.org/packages/lightdm-pantheon-greeter/): A greeter from the elementary OS project.
*   [lightdm-mini-greeter](https://aur.archlinux.org/packages/lightdm-mini-greeter/): A minimal, configurable, single-user greeter.

You can set the default greeter by changing the `[Seat:*]` section of the LightDM configuration file, like so:

 `/etc/lightdm/lightdm.conf` 
```
[Seat:*]
...
greeter-session=lightdm-*yourgreeter*-greeter
...
```

One way to check which greeters are available is to list the files in the `/usr/share/xgreeters` directory; each *.desktop* file represents an available greeter. In this example, the `lightdm-gtk-greeter` and `lightdm-kde-greeter` greeters are available:

```
$ ls -1 /usr/share/xgreeters/
lightdm-gtk-greeter.desktop
lightdm-kde-greeter.desktop

```

## Enabling LightDM

Make sure to [enable](/index.php/Enable "Enable") `lightdm.service` so LightDM will be started at boot, see also [Display manager#Loading the display manager](/index.php/Display_manager#Loading_the_display_manager "Display manager").

## Command line tool

LightDM offers a command line tool, `dm-tool`, which can be used to lock the current seat, switch sessions, etc, which is useful with 'minimalist' window managers and for testing. To see a list of available commands, execute:

```
$ dm-tool --help

```

### User switching

**Warning:** The use of lightDM's built-in screen lockers like `dm-tool lock` or `dm-tool switch-to-greeter` are [**not** recommended](https://bbs.archlinux.org/viewtopic.php?pid=1712213#p1712213). Use [light-locker](#Lock_the_screen_using_light-locker) or something from [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security").

LightDM's *dm-tool* command can be used to allow multiple users to be logged in on separate ttys. The following will send a signal requesting that the current session be locked and then will initiate a switch to LightDM's greeter, allowing a new user to log in to the system.

```
$ dm-tool switch-to-greeter

```

## Testing

First, [install](/index.php/Install "Install") [xorg-server-xephyr](https://www.archlinux.org/packages/?name=xorg-server-xephyr) from the [official repositories](/index.php/Official_repositories "Official repositories").

Then, run LightDM as an X application:

```
$ lightdm --test-mode --debug

```

## Optional configuration and tweaks

LightDM can be configured by modifying its config file, `/etc/lightdm/lightdm.conf`.

Some greeters have their own configuration files. For example:

[lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter): `/etc/lightdm/lightdm-gtk-greeter.conf`

[lightdm-webkit2-greeter](https://www.archlinux.org/packages/?name=lightdm-webkit2-greeter): `/etc/lightdm/lightdm-webkit2-greeter.conf`

[lightdm-kde-greeter](https://www.archlinux.org/packages/?name=lightdm-kde-greeter): `/etc/lightdm/lightdm-kde-greeter.conf`

### X session wrapper

If you are migrating from [xinit](/index.php/Xinit "Xinit"), you will notice that the display is not launched by your shell. This is because, as opposed to your shell starting the display (and the display inheriting the environment of your shell), LightDM starts your display and does not source your shell. LightDM launches the display by running a wrapper script and that finally exec's your graphic environment. By default, `/etc/lightdm/Xsessions.conf` is run.

#### Environment variables

The script checks and sources `/etc/profile`, `~/.profile`, `/etc/xprofile` and `~/.xprofile`, in that order. If you are using a shell that does not source any of these files, you can create an `~/.xprofile` to do so. (In this example, the login shell is [zsh](/index.php/Zsh "Zsh"))

 `~/.xprofile` 
```
#!/bin/sh
[[ -f ~/.config/zsh/.zshenv ]] && source ~/.config/zsh/.zshenv
```

If you have shell variables that are important for your display (such as Gtk or QT themes, GNUPG location, config overrides, etc.) this will let your graphic environment have access to your environment without having to be launched by your login shell.

#### Keymap

The script runs [Xkbmap](/index.php/Xkbmap "Xkbmap") with arguments provided in files `/etc/X11/Xkbmap`, `~/.Xkbmap`. If those files are not found, it runs [xmodmap](/index.php/Xmodmap "Xmodmap") with `/etc/X11/Xmodmap`, `~/.Xmodmap`. If using xkbmap, the files are parsed using cat. The following example works

 `~/.xprofile`  `-model pc105 -layout us,us,tr -variant ,dvorak,f -option grp:caps_toggle` 

### Changing background images/colors

You can set the background to a hex color or an image. Some greeters offer more robust background options like background selection from the login screen, random backgrounds, etc.

#### GTK+ greeter

You can use the [lightdm-gtk-greeter-settings](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter-settings) gui.

Users wishing to customize the wallpaper on the greeter screen need to edit `/etc/lightdm/lightdm-gtk-greeter.conf` and define the `background` variable under the `[greeter]` section. For example:

 `/etc/lightdm/lightdm-gtk-greeter.conf` 
```
[greeter]
background=/usr/share/pixmaps/black_and_white_photography-wallpaper-1920x1080.jpg
```

**Note:** It is recommended to place the PNG or JPG file in `/usr/share/pixmaps` since the LightDM user needs read access to the wallpaper file.

##### GTK3 Theme

GTK3 themes can be specified with the `theme-name` variable in the `[greeter]` section of `/etc/lightdm/lightdm-gtk-greeter.conf` For example, `theme-name=Adwaita-dark`.

#### Webkit2 greeter

The [lightdm-webkit2-greeter](https://www.archlinux.org/packages/?name=lightdm-webkit2-greeter) allows you to choose a background image directly on the login screen. It also offers an option to display a random image each time it starts if you use the [Material theme](https://github.com/artur9010/lightdm-webkit-material). By default, images are sourced from `/usr/share/backgrounds`. You can change the background images directory by editing `lightdm-webkit2-greeter.conf`. For example:

 `/etc/lightdm/lightdm-webkit2-greeter.conf` 
```
[branding]
background_images = /usr/share/backgrounds
```

**Note:** The background images directory must be accessible to the LightDM user so it should not be located anywhere under `/home`.

#### Unity greeter

Users using the [lightdm-unity-greeter](https://aur.archlinux.org/packages/lightdm-unity-greeter/) must edit the `/usr/share/glib-2.0/schemas/com.canonical.unity-greeter.gschema.xml` file and then execute:

```
# glib-compile-schemas /usr/share/glib-2.0/schemas/

```

According to [this](https://bbs.archlinux.org/viewtopic.php?id=149945) page.

#### KDE greeter

Go to *System Settings > Login Screen (LightDM)* and change the background image for your theme.

Alternatively, you can edit the `Background` variable in `lightdm-kde-greeter.conf` :

 `/etc/lightdm/lightdm-kde-greeter.conf` 
```
[greeter]
theme-name=classic

[greeter-settings]
Background=/usr/share/archlinux/wallpaper/archlinux-underground.jpg
BackgroundKeepAspectRatio=true
GreetMessage=Welcome to %hostname%
```

#### Slick Greeter

Use the [lightdm-settings](https://aur.archlinux.org/packages/lightdm-settings/) GUI

### Changing your avatar

**Tip:** If you are using KDE, you can change your avatar in KDE System Settings.

First, make sure the [accountsservice](https://www.archlinux.org/packages/?name=accountsservice) package from the [official repositories](/index.php/Official_repositories "Official repositories") is installed, then set it up as follows, replacing `*username*` with the desired user's login name.

*   Create the file `/var/lib/AccountsService/icons/*username*.png` using a 96x96 PNG image file. Different image file formats are possible too, e.g., JPEG.

*   Edit or create the account settings file `/var/lib/AccountsService/users/*username*`, and add the lines

```
[User]
Icon=/var/lib/AccountsService/icons/*username*.png

```

The filename here should point to the icon created in the first step, so adjust the filename extension if necessary.

**Note:** Make sure that both created files have 644 permissions, use [chmod](/index.php/Chmod "Chmod") to correct them.

### Sources of Arch-centric 64x64 icons

The [archlinux-artwork](https://aur.archlinux.org/packages/archlinux-artwork/) package contains some nice examples that install to `/usr/share/archlinux/icons` and that can be copied to `/usr/share/icons/hicolor/64x64/devices` as follows:

```
# find /usr/share/archlinux/icons -name "*64*" -exec cp {} /usr/share/icons/hicolor/64x64/devices \;

```

After copying, the [archlinux-artwork](https://aur.archlinux.org/packages/archlinux-artwork/) package can be removed.

### Enabling autologin

Edit the LightDM configuration file and ensure these lines are uncommented and correctly configured:

 `/etc/lightdm/lightdm.conf` 
```
[Seat:*]
autologin-user=*username*
```

You must be part of the `autologin` group to be able to login automatically without entering your password:

```
# groupadd -r autologin
# gpasswd -a *username* autologin

```

LightDM logs in using the session specified in the `~/.dmrc` of the user getting logged in automatically. To override this file, specify `autologin-session` in `lightdm.conf`:

 `/etc/lightdm/lightdm.conf` 
```
[Seat:*]
autologin-user=*username*
autologin-session=*session*
```

You will also need to ensure you have the [accountsservice](https://www.archlinux.org/packages/?name=accountsservice) package installed, otherwise LightDM will fail to start, and running it from the command line will show `Error getting user list from org.freedesktop.Accounts`.

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
# gpasswd -a *username* nopasswdlogin

```

**Note:** GNOME users, and by extension any gnome-keyring user may have to follow the instructions at the end of the previous section on enabling autologin.

To create a new user account that logs in automatically and additionally able to login again without a password the user can be created with supplementary membership of both groups, e.g.:

```
# useradd -mG autologin,nopasswdlogin -s /bin/bash *username*

```

### Hiding system and services users

To prevent system users from showing-up in the login, install the optional dependency [accountsservice](https://www.archlinux.org/packages/?name=accountsservice), or add the user names to `/etc/lightdm/users.conf` under `hidden-users`. The first option has the advantage of not needing to update the list when more users are added or removed.

### Migrating from SLiM

Move the contents of [xinitrc](/index.php/Xinitrc "Xinitrc") to [xprofile](/index.php/Xprofile "Xprofile"), removing the call to start the [window manager](/index.php/Window_manager "Window manager") or [desktop environment](/index.php/Desktop_environment "Desktop environment").

### Login using ~/.xinitrc

See [Display manager#Run ~/.xinitrc as a session](/index.php/Display_manager#Run_.7E.2F.xinitrc_as_a_session "Display manager").

### NumLock on by default

Install the [numlockx](https://www.archlinux.org/packages/?name=numlockx) package and then edit `/etc/lightdm/lightdm.conf`:

 `/etc/lightdm/lightdm.conf` 
```
[Seat:*]
greeter-setup-script=/usr/bin/numlockx on
```

### Default session

Lightdm, like other DMs, stores the last-selected xsession in `~/.dmrc`. See [Display manager#Session configuration](/index.php/Display_manager#Session_configuration "Display manager") for more info.

### Adjusting the login window's position

#### GTK+ greeter

Users need to edit `/etc/lightdm/lightdm-gtk-greeter.conf` and enter a value for the `position` variable. It accepts `x` and `y` values, either absolute (in pixels) or relative (in percent). Each value can also have an additional anchor location for the window, `start`, `center` and `end` separated from the value by a comma.

Example:

```
position=200,start 50%,center

```

### VNC Server

Lightdm can also be used to connect to via VNC. Make sure to install [tigervnc](https://www.archlinux.org/packages/?name=tigervnc) on the server side and optionally as your VNC client on the client PC.

Setup an authentication password on the server as root:

```
# vncpasswd /etc/vncpasswd

```

Edit the LightDM configuration file as shown below. Note that `listen-address` configures the VNC to only listen to connections from localhost. This is used to only allow connections via [SSH and port forwarding](/index.php/TigerVNC#On_the_client "TigerVNC"). On the SSH client, make sure that you use `localhost:5900` for the tunnel destination; using `127.0.0.1:5900` or `::1:5900` is not reliable on dual stack network connections. If you want to allow insecure connections you can disable this setting.

 `/etc/lightdm/lightdm.conf` 
```
[VNCServer]
enabled=true
command=Xvnc -rfbauth /etc/vncpasswd
port=5900
listen-address=localhost
width=1024
height=768
depth=24
```

Now open an SSH tunnel and connect to localhost as described in [TigerVNC#On the client](/index.php/TigerVNC#On_the_client "TigerVNC").

**Note:** If you get a blank screen upon opening the VNC connection, try a different LightDM greeter.

### Lock the screen using light-locker

[light-locker](https://www.archlinux.org/packages/?name=light-locker) is a simple screen locker using LightDM to authenticate the user. Once it is installed and running you can lock your session using

```
$ light-locker-command -l

```

This requires `light-locker` to be started at the beginning of your session - see [Autostarting](/index.php/Autostarting "Autostarting").

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

Alternatively if you want LightDM and its greeters to be in a language other than your set system locale, you can use the `Environment=` option in [Systemd#Drop-in files](/index.php/Systemd#Drop-in_files "Systemd").

### Missing icons with GTK greeter

If you are using [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) as a greeter and it shows placeholder images as icons, make sure valid icon themes and themes are installed and configured. Check the following file:

 `/etc/lightdm/lightdm-gtk-greeter.conf` 
```
[greeter]
theme-name=mate      # this should be the name of a directory under /usr/share/themes/
icon-theme-name=mate # this should be the name of a fully featured icons set directory under /usr/share/icons/
```

### LightDM freezes on login attempt

You may find that after entering the correct username and password and attempting to log in, LightDM freezes and you are unable to continue to the desktop. To fix the issue, reinstall the [gdk-pixbuf2](https://www.archlinux.org/packages/?name=gdk-pixbuf2) package. See [this forum thread](https://bbs.archlinux.org/viewtopic.php?id=179031).

### LightDM displaying in wrong monitor

If you are using multiple monitors, LightDM may display in the wrong one (e.g. if your primary monitor is on the right). To force the LightDM login screen to display on a specific monitor, edit `/etc/lightdm/lightdm.conf` and change the *display-setup-script* parameter like this:

 `/etc/lightdm/lightdm.conf`  `display-setup-script=xrandr --output *HDMI1* --primary` 

Replace *HDMI1* with your real monitor ID, which you can find from **xrandr** command output.

Alternatively, if you are using the GTK+ greeter, you can edit `/etc/lightdm/lightdm-gtk-greeter.conf` and add the *active-monitor* parameter like this:

 `/etc/lightdm/lightdm-gtk-greeter.conf` 
```
[greeter]
active-monitor=0
```

Replace 0 with the desired display number.

### LightDM does not appear or monitor only displays TTY output

It may happen that your system boots so fast that LightDM service is started before your graphics drivers are properly loaded. If this is your case, you will want to add the following config to your lightdm.conf file:

```
   [LightDM]
   logind-check-graphical=true

```

This setting will tell LightDM to wait until graphics devices are ready before spawning greeters/autostarting sessions on them.

### Pulseaudio not starting automatically

See [PulseAudio#Running](/index.php/PulseAudio#Running "PulseAudio").

### Long pause before LightDM shows up when home is encrypted

Some LightDM themes try to access the user avatar located in HOME. If your HOME is encrypted, LightDM cannot access it and hangs. To prevent this from happening, you can either:

*   Set your avatar as explained in [#Changing your avatar](#Changing_your_avatar)
*   for [lightdm-gtk-greeter](https://www.archlinux.org/packages/?name=lightdm-gtk-greeter) only: `hide-user-image = true` in `/etc/lightdm/lightdm-gtk-greeter.conf`

### Boot hangs on "[ OK ] Reached target Graphical Interface."

There is a possibility that user and group lookups fail if you modified /etc/nsswitch.conf. That happens when:

*   nsswitch.conf group: includes `ldap` without setting `nss_initgroups_ignoreusers ALLLOCAL` in `/etc/nslcd.conf`

## See also

*   [Ubuntu Wiki article](https://wiki.ubuntu.com/LightDM)
*   [Gentoo Wiki article](http://wiki.gentoo.org/wiki/LightDM)
*   [Launchpad Page](https://launchpad.net/lightdm) obsolete
*   [LightDM blog](http://www.mattfischer.com/blog/?tag=lightdm)
*   [LightDM on GitHub](https://github.com/CanonicalLtd/lightdm)