Related articles

*   [Display manager](/index.php/Display_manager "Display manager")
*   [KDE](/index.php/KDE "KDE")

The [Simple Desktop Display Manager](https://github.com/sddm/sddm/) (SDDM) is the preferred [display manager](/index.php/Display_manager "Display manager") for [KDE](/index.php/KDE "KDE") Plasma desktop.

From [Wikipedia:Simple Desktop Display Manager](https://en.wikipedia.org/wiki/Simple_Desktop_Display_Manager "wikipedia:Simple Desktop Display Manager"):

	Simple Desktop Display Manager (SDDM) is a display manager (a graphical login program) for X11 and Wayland windowing systems. SDDM was written from scratch in C++11 and supports theming via QML. KDE chose SDDM to be the successor of the KDE Display Manager for KDE Plasma 5.

**Note:** The Wayland windowing system is not yet fully supported [[1]](https://github.com/sddm/sddm/issues/440). Wayland sessions are listed, but SDDM runs on X11.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Autologin](#Autologin)
    *   [2.2 Unlock KDE Wallet automatically on login](#Unlock_KDE_Wallet_automatically_on_login)
    *   [2.3 Theme settings](#Theme_settings)
        *   [2.3.1 Current theme](#Current_theme)
        *   [2.3.2 Editing themes](#Editing_themes)
        *   [2.3.3 Testing (Previewing) a Theme](#Testing_(Previewing)_a_Theme)
        *   [2.3.4 Mouse cursor](#Mouse_cursor)
        *   [2.3.5 User Icon (Avatar)](#User_Icon_(Avatar))
    *   [2.4 Numlock](#Numlock)
    *   [2.5 Rotate display](#Rotate_display)
    *   [2.6 DPI settings](#DPI_settings)
    *   [2.7 Enable HiDPI](#Enable_HiDPI)
    *   [2.8 Using a fingerprint reader](#Using_a_fingerprint_reader)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Blank screen with cursor, but no greeter shows](#Blank_screen_with_cursor,_but_no_greeter_shows)
    *   [3.2 Long load time before SDDM shows the greeter](#Long_load_time_before_SDDM_shows_the_greeter)
    *   [3.3 Hangs after login](#Hangs_after_login)
    *   [3.4 SDDM starts on tty1 instead of tty7](#SDDM_starts_on_tty1_instead_of_tty7)
    *   [3.5 One or more users do not show up on the greeter](#One_or_more_users_do_not_show_up_on_the_greeter)
    *   [3.6 SDDM loads only US keyboard layout](#SDDM_loads_only_US_keyboard_layout)
    *   [3.7 Screen resolution is too low](#Screen_resolution_is_too_low)
    *   [3.8 Long load time on autofs home directory](#Long_load_time_on_autofs_home_directory)

## Installation

[Install](/index.php/Install "Install") the [sddm](https://www.archlinux.org/packages/?name=sddm) package. Optionally install [sddm-kcm](https://www.archlinux.org/packages/?name=sddm-kcm) for the [KDE Config Module](/index.php/KDE#KCM "KDE").

Follow [Display manager#Loading the display manager](/index.php/Display_manager#Loading_the_display_manager "Display manager") to start SDDM at boot.

## Configuration

The default configuration file for SDDM can be found at `/usr/lib/sddm/sddm.conf.d/default.conf`. For any changes, create configuration file(s) in `/etc/sddm.conf.d/`. See [sddm.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sddm.conf.5) for all options.

The [sddm-kcm](https://www.archlinux.org/packages/?name=sddm-kcm) package (included in the [plasma](https://www.archlinux.org/groups/x86_64/plasma/) group) provides a GUI to configure SDDM in Plasma's system settings. There is also a [Qt](/index.php/Qt "Qt")-based [sddm-config-editor-git](https://aur.archlinux.org/packages/sddm-config-editor-git/) available in the [AUR](/index.php/AUR "AUR").

Everything should work out of the box, since Arch Linux uses [systemd](/index.php/Systemd "Systemd") and SDDM defaults to using `systemd-logind` for session management.

### Autologin

SDDM supports automatic login through its configuration file, for example:

 `/etc/sddm.conf.d/autologin.conf` 
```
[Autologin]
User=john
Session=plasma.desktop
```

This configuration causes a KDE Plasma session to be started for user `john` when the system is booted. Available session types can be found in `/usr/share/xsessions/` directory.

An option to autologin into KDE Plasma while simultaneously locking the session is not available [[2]](https://github.com/sddm/sddm/issues/306)

You can add a script that activates the screensaver of KDE to the autostart as a workaround:

```
#!/bin/sh
/usr/bin/dbus-send --session --type=method_call --dest=org.freedesktop.ScreenSaver /ScreenSaver org.freedesktop.ScreenSaver.Lock &

```

### Unlock KDE Wallet automatically on login

See [KDE Wallet#Unlock KDE Wallet automatically on login](/index.php/KDE_Wallet#Unlock_KDE_Wallet_automatically_on_login "KDE Wallet").

### Theme settings

Theme settings can be changed in the `[Theme]` section. If you use Plasma's system settings, themes may show previews.

Set to `breeze` for the default Plasma theme.

Some themes are available in the [AUR](/index.php/AUR "AUR"), for example [archlinux-themes-sddm](https://aur.archlinux.org/packages/archlinux-themes-sddm/).

#### Current theme

Set the current theme through the `Current` value, e.g. `Current=archlinux-simplyblack`.

#### Editing themes

The default SDDM theme directory is `/usr/share/sddm/themes/`. You can add your custom made themes to that directory under a separate subdirectory. Note that SDDM requires these subdirectory names to be the same as the theme names. Study the files installed to modify or create your own theme.

#### Testing (Previewing) a Theme

You can preview an SDDM theme if needed. This is especially helpful if you are not sure how the theme would look if selected or just edited a theme and want to see how it would look without logging out. You can run something like this:

```
$ sddm-greeter --test-mode --theme /usr/share/sddm/themes/breeze

```

This should open a new window for every monitor you have connected and show a preview of the theme.

**Note:** This is just a preview. In this mode, some actions like shutdown, suspend or login will have no effect.

#### Mouse cursor

To set the mouse cursor theme, set `CursorTheme` to your preferred cursor theme.

Valid [Plasma](/index.php/Plasma "Plasma") mouse cursor theme names are `breeze_cursors`, `Breeze_Snow` and `breeze-dark`.

#### User Icon (Avatar)

SDDM reads the user icon (a.k.a. "avatar") as a PNG image from either `~/.face.icon` for each user, or the common location for all users specified by `FacesDir` in an SDDM configuration file. The configuration setting can be placed in either `/etc/sddm.conf` directly, or, better, a file under `/etc/sddm.conf.d/` such as `/etc/sddm.conf.d/avatar.conf`.

To use the `FacesDir` location option, place a PNG image for each user named as `*username*.face.icon` into location specified in for `FacesDir` in the configuration file. The default location for `FacesDir` is `/usr/share/sddm/faces/`. You can change the default `FacesDir` location to match your requirements. Here is an example:

 `/etc/sddm.conf.d/avatar.conf` 
```
[Theme]
FacesDir=/var/lib/AccountsService/icons/
```

The other option is to put a PNG image named `.face.icon` at the root of your home directory. In this case, no changes to any SDDM configuration file is required. However, you need to make sure that `sddm` user can read the PNG image file(s) for the user icon(s).

**Note:** In many KDE versions, the user icon image file is `~/.face` and `~/.face.icon` is a symlink to that file. If the user icon images are symlinks, you need to set proper file permissions to the target files.

To [set proper permissions](/index.php/Access_Control_Lists#Set_ACL "Access Control Lists") run:

```
$ setfacl -m u:sddm:x ~/
$ setfacl -m u:sddm:r ~/.face.icon

```

You can [check permissions](/index.php/Access_Control_Lists#Show_ACL "Access Control Lists") with:

```
$ getfacl ~/
$ getfacl ~/.face.icon

```

See [SDDM README: No User Icon](https://github.com/sddm/sddm#no-user-icon).

### Numlock

If you want to enforce Numlock to be enabled, set `Numlock=on` in the `[General]` section.

### Rotate display

See [Xrandr#Configuration](/index.php/Xrandr#Configuration "Xrandr").

### DPI settings

Sometimes it is useful to set up correct monitor's PPI settings on a "Display Manager" level. To do so you need to find `ServerArguments` parameter in `sddm.conf` and add `-dpi *your_dpi*` at the end of the string.

For example:

 `/etc/sddm.conf.d/dpi.conf` 
```
[X11]
ServerArguments=-nolisten tcp -dpi 94
```

### Enable HiDPI

Create the following file:

 `/etc/sddm.conf.d/hidpi.conf` 
```
[Wayland]
EnableHiDPI=true

[X11]
EnableHiDPI=true
```

### Using a fingerprint reader

**Note:** Make sure that your fingerprint is registered before making these changes. Fingerprint support is not completely working properly yet, and it seems logging in with only a password no longer works using this method.

SDDM works with a fingerprint reader when using [fprint](/index.php/Fprint "Fprint"). After installing fprint and adding fingerprint signatures, add the line `auth sufficient pam_fprintd.so` at the beginning of `/etc/pam.d/sddm`.

**Tip:** To make it work in KDE's lock screen, also add the same line at the beginning of `/etc/pam.d/kde`.

If you now press enter in the empty password field, the fingerprint reader should start working.

## Troubleshooting

### Blank screen with cursor, but no greeter shows

Check your disk space with `df -h`. If no available space, greeter will crash.

### Long load time before SDDM shows the greeter

A low entropy pool can cause long SDDM load time ([Bug report](https://github.com/sddm/sddm/issues/1036)). See [Random number generation](/index.php/Random_number_generation "Random number generation") for suggestions to increase the entropy pool.

### Hangs after login

Try removing `~/.Xauthority` and logging in again without rebooting. Rebooting without logging in creates the file again and the problem will persist.

### SDDM starts on tty1 instead of tty7

SDDM follows the [systemd convention](http://0pointer.de/blog/projects/serial-console.html) of starting the first graphical session on tty1\. If you prefer the old convention where tty1 through tty6 are reserved for text consoles, change the default value of `MinimumVT` variable, which comes under the `[X11]` section:

 `/etc/sddm.conf.d/tty.conf` 
```
[X11]
MinimumVT=7
```

### One or more users do not show up on the greeter

**Warning:** Users set with a lower or higher `UID` range should generally not be exposed to a [Display manager](/index.php/Display_manager "Display manager").

SDDM only displays users with a UID in the range of 1000 to 65000 by default, if the UIDs of the desired users are below this value then you will have to modify this range. For example, for a UID of 501, say:

 `/etc/sddm.conf.d/uid.conf` 
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

SDDM may also incorrectly display the layout as US but will immediately change to the correct layout after you start typing your password [[3]](https://github.com/sddm/sddm/issues/202#issuecomment-76001543). This seems to not be a bug in SDDM but in [libxcb](https://www.archlinux.org/packages/?name=libxcb) (version 1.13-1 as of 2018) [[4]](https://github.com/sddm/sddm/issues/202#issuecomment-133628462).

### Screen resolution is too low

Issue may be caused by HiDPI usage for monitors with corrupted [EDID](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data "wikipedia:Extended Display Identification Data") [[5]](https://github.com/sddm/sddm/issues/692). If you have [enabled HiDPI](#Enable_HiDPI), try to disable it.

If even the above fails, you can try setting your screen size in a Xorg configuration file:

 `/etc/X11/xorg.conf.d/90-monitor.conf` 
```
Section "Monitor"
        Identifier      "<default monitor>"
        DisplaySize     345 194 # in millimeters
EndSection
```

### Long load time on autofs home directory

SDDM by default tries to display avatars of users by accessing `~/.face.icon` file. If your home directory is an *autofs*, for example if you use [dm-crypt](/index.php/Dm-crypt "Dm-crypt"), this will make it wait for 60 seconds, until autofs reports that the directory cannot be mounted.

You can disable avatars by editing `/etc/sddm.conf`:

 `/etc/sddm.conf` 
```
[Theme]
EnableAvatars=false
```