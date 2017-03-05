**Warning:** The SliM project has been abandoned (the [project homepage](http://slim.berlios.de/) is down, leaving a [github mirror](https://github.com/data-modul/slim)), and is not fully compatible with [systemd](/index.php/Systemd "Systemd"), including *logind* sessions. Consider using a different [Display manager](/index.php/Display_manager "Display manager") or [Xinitrc](/index.php/Xinitrc "Xinitrc").

[SLiM](http://sourceforge.net/projects/slim.berlios/) is an acronym for **S**imple **L**og**i**n **M**anager. Lightweight and easily configurable, SLiM requires minimal dependencies, and none from the [GNOME](/index.php/GNOME "GNOME") or [KDE](/index.php/KDE "KDE") desktop environments. It therefore contributes towards a lightweight system for users that also like to use lightweight desktops such as [Xfce](/index.php/Xfce "Xfce"), [Openbox](/index.php/Openbox "Openbox"), and [Fluxbox](/index.php/Fluxbox "Fluxbox").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Enabling SLiM](#Enabling_SLiM)
    *   [2.2 Environments](#Environments)
    *   [2.3 Set default username](#Set_default_username)
    *   [2.4 Enable Autologin](#Enable_Autologin)
    *   [2.5 Theming](#Theming)
        *   [2.5.1 Dual screen setup](#Dual_screen_setup)
*   [3 Other options](#Other_options)
    *   [3.1 Changing the cursor](#Changing_the_cursor)
    *   [3.2 Match SLiM and Desktop Wallpaper](#Match_SLiM_and_Desktop_Wallpaper)
    *   [3.3 Shutdown, reboot, suspend, exit, launch terminal from SLiM](#Shutdown.2C_reboot.2C_suspend.2C_exit.2C_launch_terminal_from_SLiM)
    *   [3.4 Power-off error with Splashy](#Power-off_error_with_Splashy)
    *   [3.5 Power-off tray icon fails](#Power-off_tray_icon_fails)
    *   [3.6 Login information with SLiM](#Login_information_with_SLiM)
    *   [3.7 Custom SLiM Login Commands](#Custom_SLiM_Login_Commands)
    *   [3.8 Gnome Keyring](#Gnome_Keyring)
    *   [3.9 Setting DPI with SLiM](#Setting_DPI_with_SLiM)
    *   [3.10 Use a random theme](#Use_a_random_theme)
    *   [3.11 Move the whole session to another VT](#Move_the_whole_session_to_another_VT)
    *   [3.12 Automatically mount your encrypted /home on login](#Automatically_mount_your_encrypted_.2Fhome_on_login)
    *   [3.13 Change Keyboard Layout](#Change_Keyboard_Layout)
*   [4 All Slim Options](#All_Slim_Options)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Shutdown or Reboot Stalled](#Shutdown_or_Reboot_Stalled)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [slim](https://www.archlinux.org/packages/?name=slim) package.

## Configuration

**Note:** SLiM no longer supports a 'default' session where multiple sessions have been enabled. This is most noticable where attempting to log out and back in again to the same session.

SLiM can automatically detect installed desktop environments and window managers through the use of `sessiondir /usr/share/xsessions/` in `/etc/slim.conf`. Those upgrading from a version before 1.3.6-2 must amend `/etc/slim.conf` and [xinitrc](/index.php/Xinitrc "Xinitrc"), accordingly. See below.

### Enabling SLiM

**Note:** [slim](https://www.archlinux.org/packages/?name=slim) relies on *systemd-logind*.

[Enable](/index.php/Enable "Enable") the SLiM service `slim.service`. This assumes a previously enabled display manager was disabled first. Otherwise, change the [default target](/index.php/Systemd#Change_default_target_to_boot_into "Systemd").

### Environments

**Note:** Available sessions for selection can be cycled through by pressing the **F1** key.

**Tip:** Users that have installed a previous version of SLiM can replace `session` with a hashed `sessiondir /usr/share/xsessions/`

To configure SLiM 1.3.6-2 (or later) to load a particular environment, it will be necessary to edit both `/etc/slim.conf` and `~/.xinitrc`.

First, edit `/etc/slim.conf` in order to hash out `sessiondir /usr/share/xsessions/`. This will consequently disable automatic detection of installed environments:

```
# Set directory that contains the xsessions.
# slim reads xsesion from this directory, and be able to select.
# sessiondir            /usr/share/xsessions/

```

Users who installed a prior version of SLiM will have to replace `sessions` with the new command.

Second, edit [xinitrc](/index.php/Xinitrc "Xinitrc").

Users who installed a prior version of SLiM will have to replace `case $1 in [...] esac`, where used. To clarify, below is an example of the deprecated method to select multiple sessions. The entire code provided below would simply be replaced with `exec $1`:

```
DEFAULTSESSION=openbox-session

case "$1" in
    openbox) exec openbox-session ;;
     xfce) exec xfce4-session ;;
     gnome3) exec gnome-session ;;
     kde) exec startkde ;;
     cinnamon) exec gnome-session-cinnamon ;;
     razor-qt) exec razor-session ;;
     lxde) exec lxsession ;;
     mate) exec mate-session ;;
     *) exec $DEFAULTSESSION ;;
esac

```

### Set default username

SLiM can be configured to automatically set a desired username, which will therefore already be completed. The password field will also already be focused by default. Change the following line in `/etc/slim.conf`:

```
# default_user        simone

```

Uncomment this line, and change "simone" to the username of choice:

```
default_user        *your username*

```

### Enable Autologin

**Note:** It will be necessary to have first set SLiM to use a single desktop environment, as well as a default username.

**Warning:** Do **not** set this for the **root** account.

**Warning:** If auto login is enabled, the GNOME keyring will not be unlocked automatically on login. This will cause dependent applications, such as Chrome/Chromium and NetworkManager, to misbehave (see [https://bbs.archlinux.org/viewtopic.php?id=167579](https://bbs.archlinux.org/viewtopic.php?id=167579)).

Edit `/etc/slim.conf` to uncomment the `auto_login` command and replace `no` with `yes`:

```
auto_login          yes

```

### Theming

[Install](/index.php/Install "Install") the [slim-themes](https://www.archlinux.org/packages/?name=slim-themes) package. The [archlinux-themes-slim](https://www.archlinux.org/packages/?name=archlinux-themes-slim) packages contains several different themes ([slimthemes.png](https://sr.ht/bbe6.png)). Look in the directory of `/usr/share/slim/themes` to see the themes available. Enter the theme name on the `current_theme` line in `/etc/slim.conf`:

```
#current_theme       default
current_theme       archlinux-simplyblack

```

To preview a theme run while an instance of the Xorg server is running by:

```
$ slim -p /usr/share/slim/themes/<theme name>

```

To close, type "exit" in the Login line and press Enter.

Additional theme packages can be found in the [AUR](/index.php/AUR "AUR").

#### Dual screen setup

You can customize the slim theme in `/usr/share/slim/themes/<your-theme>/slim.theme` to turn these percents values. The box itself is 450 pixels by 250 pixels:

```
input_panel_x           50%
input_panel_y           50%

```

into pixels values:

```
# These settings set the "archlinux-simplyblack" panel in the center of a 1440x900 screen
input_panel_x           495
input_panel_y           325

```

```
# These settings set the "archlinux-retro" panel in the center of a 1680x1050 screen
input_panel_x           615
input_panel_y           400

```

If your theme has a background picture you should use the background_style setting ('stretch', 'tile', 'center' or 'color') to get it correctly displayed. Have a look at the [very simple and clear official documentation about slim themes](https://web.archive.org/web/20140414001555/http://slim.berlios.de/themes_howto.php) for further details.

## Other options

### Changing the cursor

After installing, edit `/etc/slim.conf` and uncomment the line:

```
cursor   left_ptr

```

This will give you a normal arrow instead. This setting is forwarded to `xsetroot -cursor_name`. You can look up the possible cursor names [here](http://cvsweb.xfree86.org/cvsweb/*checkout*/xc/lib/X11/cursorfont.h?rev=HEAD&content-type=text/plain) or in `/usr/share/icons/<your-cursor-theme>/cursors/`.

To change the cursor theme being used at the login screen, see [Cursor themes#Using an index.theme file .28recommended.29](/index.php/Cursor_themes#Using_an_index.theme_file_.28recommended.29 "Cursor themes").

### Match SLiM and Desktop Wallpaper

To share a wallpaper between SLiM and your desktop, rename the used theme background, then create a link from your desktop wallpaper file to the default SLiM theme:

```
# mv /usr/share/slim/themes/default/background.jpg{,.bck}
# ln -s /path/to/mywallpaper.jpg /usr/share/slim/themes/default/background.jpg

```

### Shutdown, reboot, suspend, exit, launch terminal from SLiM

You may shutdown, reboot, suspend, exit or even launch a terminal from the SLiM login screen. To do so, use the values in the username field, and the root password in the password field:

*   To launch a terminal, enter **console** as the username (defaults to xterm which must be installed separately... edit `/etc/slim.conf` to change terminal preference)
*   For shutdown, enter **halt** as the username
*   For reboot, enter **reboot** as the username
*   To exit to bash, enter **exit** as the username
*   For suspend, enter **suspend** as the username. Suspend is disabled by default, edit `/etc/slim.conf` as root to uncomment the `suspend_cmd` line and, if necessary, modify the suspend command itself (by e.g. changing `/usr/sbin/suspend` to `sudo /usr/sbin/pm-suspend`).

### Power-off error with Splashy

If you use Splashy and SLiM, sometimes you cannot power-off or reboot from menu in GNOME, Xfce, LXDE or others. Check your `/etc/slim.conf` and `/etc/splash.conf`; set the `DEFAULT_TTY=7` same as `xserver_arguments vt07`.

### Power-off tray icon fails

If your power off tray icon fails, it could be due to not having root privileges. To start a tray icon with root privileges, be sure to have SLiM start the program. Edit `/etc/slim.conf` as follows:

```
sessionstart_cmd 	/path/to/tray/icon/program &

```

### Login information with SLiM

By default, SLiM fails to log logins to utmp and wtmp which causes who, last, etc. to misreport login information. To fix this edit your `slim.conf` as follows:

```
 sessionstart_cmd    /usr/bin/sessreg -a -l $DISPLAY %user
 sessionstop_cmd     /usr/bin/sessreg -d -l $DISPLAY %user

```

### Custom SLiM Login Commands

You can also use the sessionstart_cmd/sessionstop_cmd in `/etc/slim.conf` to log specific infomation, such as the session, user, or theme used by slim:

```
 sessionstop_cmd /usr/bin/logger -i -t ASKAPACHE "(sessionstop_cmd: u:%user s:%session t:%theme)"
 sessionstart_cmd /usr/bin/logger -i -t ASKAPACHE "(sessionstart_cmd: u:%user s:%session t:%theme)"

```

Or if you want to play a song when slim loads (and you have the beep program installed)

```
 sessionstart_cmd /usr/bin/beep -f 659 -l 460 -n -f 784 -l 340 -n -f 659 -l 230 -n -f 659 -l 110

```

### Gnome Keyring

**Note:** slim 1.3.5-1 ships with `/etc/pam.d/slim` preconfigured to unlock keyring upon login. Users no longer need to modify the file.

**Warning:** If auto login is enabled, the GNOME keyring will not be unlocked automatically on login. This will cause dependent applications, such as Chrome/Chromium and NetworkManager, to misbehave (see [https://bbs.archlinux.org/viewtopic.php?id=167579](https://bbs.archlinux.org/viewtopic.php?id=167579)).

See [GNOME Keyring#Use without GNOME, and without a display manager](/index.php/GNOME_Keyring#Use_without_GNOME.2C_and_without_a_display_manager "GNOME Keyring") to use GNOME Keyring in a custom session.

### Setting DPI with SLiM

The Xorg server generally picks up the DPI but if it does not you can specify it to SLiM. If you set the DPI with the argument -dpi 96 in `/etc/X11/xinit/xserverrc` it will not work with SLiM. To fix this change your `slim.conf` from:

```
 xserver_arguments   -nolisten tcp vt07 

```

to

```
 xserver_arguments   -nolisten tcp vt07 -dpi 96

```

### Use a random theme

Use the `current_theme` variable as a comma separated list to specify a set from which to choose. Selection is random.

### Move the whole session to another VT

If tty terminals 3-6 are not used and commented out (You may use screen and therefore only need one terminal), change `/etc/slim.conf` to move the X server:

```
xserver_arguments -nolisten tcp vt07

```

Simply change the vt07 to for example vt03 as no agetty is started there.

### Automatically mount your encrypted /home on login

See [pam_mount](/index.php/Pam_mount#SLiM "Pam mount").

### Change Keyboard Layout

Edit `/etc/X11/xorg.conf.d/10-evdev.conf`, find the following section, add the two bolded lines, and replace *dvorak* with your preferred keymap:

```
Section  "InputClass"
          Identifier "evdev keyboard catchall"
          MatchIsKeyboard "on"
          MatchDevicePath "/dev/input/event*"
          Driver "evdev"

          **# Keyboard layouts**
          **Option "XkbLayout" "*dvorak*"**
EndSection

```

## All Slim Options

Here is a list of all the slim configuration options and their default values.

**Note:** `welcome_msg` allows 2 variables **%host** and **%domain**

`sessionstart_cmd` allows **%user** (executed right before login_cmd) and it is also allowed in `sessionstop_cmd`

`login_cmd` allows **%session** and **%theme**

| Option Name | Default Value |
| default_path | `/bin:/usr/bin:/usr/local/bin` |
| default_xserver | `/usr/bin/X` |
| xserver_arguments | `vt07 -auth /var/run/slim.auth` |
| numlock |
| daemon | `yes` |
| xauth_path | `/usr/bin/xauth` |
| login_cmd | `exec /bin/bash -login ~/.xinitrc %session` |
| halt_cmd | `/sbin/shutdown -h now` |
| reboot_cmd | `/sbin/shutdown -r now` |
| suspend_cmd |
| sessionstart_cmd |
| sessionstop_cmd |
| console_cmd | `/usr/bin/xterm -C -fg white -bg black +sb -g %dx%d+%d+%d -fn %dx%d -T` |
| screenshot_cmd | `import -window root /slim.png` |
| welcome_msg | `Welcome to %host` |
| session_msg | `Session:` |
| default_user |
| focus_password | `no` |
| auto_login | `no` |
| current_theme | `default` |
| lockfile | `/var/run/slim.lock` |
| logfile | `/var/log/slim.log` |
| authfile | `/var/run/slim.auth` |
| shutdown_msg | `The system is halting...` |
| reboot_msg | `The system is rebooting...` |
| sessiondir | `/usr/share/xsessions/` |
| hidecursor | `false` |
| input_panel_x | `50%` |
| input_panel_y | `40%` |
| input_name_x | `200` |
| input_name_y | `154` |
| input_pass_x | `-1` |
| input_pass_y | `-1` |
| input_font | `Verdana:size=11` |
| input_color | `#000000` |
| input_cursor_height | `20` |
| input_maxlength_name | `20` |
| input_maxlength_passwd | `20` |
| input_shadow_xoffset | `0` |
| input_shadow_yoffset | `0` |
| input_shadow_color | `#FFFFFF` |
| welcome_font | `Verdana:size=14` |
| welcome_color | `#FFFFFF` |
| welcome_x | `-1` |
| welcome_y | `-1` |
| welcome_shadow_xoffset | `0` |
| welcome_shadow_yoffset | `0` |
| welcome_shadow_color | `#FFFFFF` |
| intro_msg |
| intro_font | `Verdana:size=14` |
| intro_color | `#FFFFFF` |
| intro_x | `-1` |
| intro_y | `-1` |
| background_style | `stretch` |
| background_color | `#CCCCCC` |
| username_font | `Verdana:size=12` |
| username_color | `#FFFFFF` |
| username_x | `-1` |
| username_y | `-1` |
| username_msg | `Please enter your username` |
| username_shadow_xoffset | `0` |
| username_shadow_yoffset | `0` |
| username_shadow_color | `#FFFFFF` |
| password_x | `-1` |
| password_y | `-1` |
| password_msg | `Please enter your password` |
| msg_color | `#FFFFFF` |
| msg_font | `Verdana:size=16:bold` |
| msg_x | `40` |
| msg_y | `40` |
| msg_shadow_xoffset | `0` |
| msg_shadow_yoffset | `0` |
| msg_shadow_color | `#FFFFFF` |
| session_color | `#FFFFFF` |
| session_font | `Verdana:size=16:bold` |
| session_x | `50%` |
| session_y | `90%` |
| session_shadow_xoffset | `0` |
| session_shadow_yoffset | `0` |
| session_shadow_color | `#FFFFFF` |

## Troubleshooting

### Shutdown or Reboot Stalled

There is a bug or known issue with the combination of SLiM, Xfce and systemd that does not let the system to properly shutdown and systemd waits for the SLiM service to end, but eventually is terminated.

To accelerate the shutdown process these lines might help when added to /usr/lib/systemd/system/slim.service:

```
[Service]
ExecStart=/usr/bin/slim -nodaemon
Restart=on-failure
TimeoutStopSec=5s
IgnoreSIGPIPE=no
ExecStop=/bin/kill -TERM -${MAINPID}

```

See [FS#32380](https://bugs.archlinux.org/task/32380).

## See also

*   [SLiM on SourceForge](http://sourceforge.net/projects/slim.berlios/)
*   [SLiM on GitHub](https://github.com/data-modul/slim)