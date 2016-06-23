From [GDM - GNOME Display Manager](https://wiki.gnome.org/Projects/GDM): "The GNOME Display Manager (GDM) is a program that manages graphical display servers and handles graphical user logins."

[Display managers](/index.php/Display_manager "Display manager") provide [X Window System](/index.php/X_Window_System "X Window System") and [Wayland](/index.php/Wayland "Wayland") users with a graphical login prompt.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Autostarting applications with GDM](#Autostarting_applications_with_GDM)
    *   [2.2 Log-in screen background image](#Log-in_screen_background_image)
    *   [2.3 DConf configuration](#DConf_configuration)
        *   [2.3.1 Log-in screen logo](#Log-in_screen_logo)
        *   [2.3.2 Changing the cursor theme](#Changing_the_cursor_theme)
        *   [2.3.3 Larger font for log-in screen](#Larger_font_for_log-in_screen)
        *   [2.3.4 Turning off the sound](#Turning_off_the_sound)
        *   [2.3.5 Make the power button interactive](#Make_the_power_button_interactive)
        *   [2.3.6 Enabling tap-to-click](#Enabling_tap-to-click)
    *   [2.4 GDM keyboard layout](#GDM_keyboard_layout)
        *   [2.4.1 GNOME Control Center](#GNOME_Control_Center)
        *   [2.4.2 GDM 2.x layout](#GDM_2.x_layout)
    *   [2.5 Change the language](#Change_the_language)
    *   [2.6 Automatic login](#Automatic_login)
    *   [2.7 Passwordless login](#Passwordless_login)
    *   [2.8 Passwordless shutdown for multiple sessions](#Passwordless_shutdown_for_multiple_sessions)
    *   [2.9 Add or edit GDM sessions](#Add_or_edit_GDM_sessions)
    *   [2.10 Enable root login in GDM](#Enable_root_login_in_GDM)
    *   [2.11 Hide user from login list](#Hide_user_from_login_list)
    *   [2.12 Rotate login screen](#Rotate_login_screen)
    *   [2.13 xrandr at login](#xrandr_at_login)
    *   [2.14 Configure X server access permission](#Configure_X_server_access_permission)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Failure to start with AMD Catalyst driver](#Failure_to_start_with_AMD_Catalyst_driver)
    *   [3.2 Failure on logout](#Failure_on_logout)
    *   [3.3 Xorg 1.16](#Xorg_1.16)
    *   [3.4 Use Xorg backend](#Use_Xorg_backend)
    *   [3.5 Incomplete removal of gdm](#Incomplete_removal_of_gdm)
*   [4 See also](#See_also)

## Installation

GDM can be [installed](/index.php/Installed "Installed") with the [gdm](https://www.archlinux.org/packages/?name=gdm) package, and it is installed as part of the [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group. To start GDM at boot time [enable](/index.php/Enable "Enable") `gdm.service`.

If you would prefer to use legacy GDM which was used in GNOME 2 and has its own configuration utility, install the [gdm-old](https://aur.archlinux.org/packages/gdm-old/) package. Note that the rest of this article discusses current GDM, not legacy GDM, unless indicated otherwise.

You might also wish to install the following:

*   **gdm3setup** — An interface to configure GDM3, autologin options and change Shell theme

	[https://github.com/Nano77/gdm3setup](https://github.com/Nano77/gdm3setup) || [gdm3setup](https://aur.archlinux.org/packages/gdm3setup/)

## Configuration

### Autostarting applications with GDM

See [Display manager#Autostarting](/index.php/Display_manager#Autostarting "Display manager"). Note that adding scripts to `/etc/gdm/Init` no longer works, see the [upstream bug report](https://bugzilla.gnome.org/show_bug.cgi?id=751602).

### Log-in screen background image

**Note:** Since GNOME 3.16, GNOME Shell themes are now stored binary files (gresource).

Firstly, you need to extract the existing GNOME Shell theme to a folder in your home directory. You can do this using the following script:

 `extractgst.sh` 
```
#!/bin/sh

workdir=${HOME}/shell-theme
if [ ! -d ${workdir}/theme ]; then
  mkdir -p ${workdir}/theme
fi
gst=/usr/share/gnome-shell/gnome-shell-theme.gresource

for r in `gresource list $gst`; do
        gresource extract $gst $r >$workdir/${r#\/org\/gnome\/shell/}
done
```

Navigate to the created directory. You should find that the theme files have been extracted to it. Now copy your preferred background image to this directory.

Next, you need to create a file in the directory with the following content:

 `gnome-shell-theme.gresource.xml` 
```
<?xml version="1.0" encoding="UTF-8"?>
<gresources>
  <gresource prefix="/org/gnome/shell/theme">
    <file>calendar-arrow-left.svg</file>
    <file>calendar-arrow-right.svg</file>
    <file>calendar-today.svg</file>
    <file>checkbox-focused.svg</file>
    <file>checkbox-off-focused.svg</file>
    <file>checkbox-off.svg</file>
    <file>checkbox.svg</file>
    <file>close-window.svg</file>
    <file>close.svg</file>
    <file>corner-ripple-ltr.png</file>
    <file>corner-ripple-rtl.png</file>
    <file>dash-placeholder.svg</file>
    <file>filter-selected-ltr.svg</file>
    <file>filter-selected-rtl.svg</file>
    <file>gnome-shell.css</file>
    <file>gnome-shell-high-contrast.css</file>
    <file>logged-in-indicator.svg</file>
    <file>**filename**</file>
    <file>more-results.svg</file>
    <file>no-events.svg</file>
    <file>no-notifications.svg</file>
    <file>noise-texture.png</file>
    <file>page-indicator-active.svg</file>
    <file>page-indicator-inactive.svg</file>
    <file>page-indicator-checked.svg</file>
    <file>page-indicator-hover.svg</file>
    <file>process-working.svg</file>
    <file>running-indicator.svg</file>
    <file>source-button-border.svg</file>
    <file>summary-counter.svg</file>
    <file>toggle-off-us.svg</file>
    <file>toggle-off-intl.svg</file>
    <file>toggle-on-hc.svg</file>
    <file>toggle-on-us.svg</file>
    <file>toggle-on-intl.svg</file>
    <file>ws-switch-arrow-up.png</file>
    <file>ws-switch-arrow-down.png</file>
  </gresource>
</gresources>
```

Replace **filename** with the filename of your background image.

Now, open the `gnome-shell.css` file in the directory and change the `#lockDialogGroup` definition as follows:

```
#lockDialogGroup {
  background: #2e3436 url(**filename**);
  background-size: **[WIDTH]**px **[HEIGHT]**px;
  background-repeat: no-repeat;
}

```

Set `background-size` to the resolution that GDM uses, this might not necessarily be the resolution of the image. For a list of display resolutions see [Display resolution](https://en.wikipedia.org/wiki/Display_resolution#Computer_monitors "wikipedia:Display resolution"). Again, set **filename** to be the name of the background image.

Finally, compile the theme using the following command:

```
$ glib-compile-resources gnome-shell-theme.gresource.xml

```

Then copy the resulting `gnome-shell-theme.gresource` file to the `/usr/share/gnome-shell` directory.

Restart GDM - you should find that it is using your preferred background image.

For more information, please see the following [forum thread](https://bbs.archlinux.org/viewtopic.php?id=197036).

### DConf configuration

Some GDM settings are stored in a DConf database. They can be configured either by adding *keyfiles* to the `/etc/dconf/db/gdm.d` directory and then recompiling the GDM database by running `dconf update` as root or by logging into the GDM user on the system and changing the setting directly using the *gsettings* command line tool. Note that for the former approach, a GDM profile file is required - this must be created manually as it is no longer shipped upstream, see below:

 `/etc/dconf/profile/gdm` 
```
user-db:user
system-db:gdm
file-db:/usr/share/gdm/greeter-dconf-defaults
```

For the latter approach, you can log into the GDM user with the command below:

```
# machinectl shell gdm@

```

#### Log-in screen logo

Either create the following keyfile

 `/etc/dconf/db/gdm.d/02-logo` 
```
[org/gnome/login-screen]
logo='*/path/to/logo.png*'
```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.login-screen logo '*/path/to/logo.png*'

```

#### Changing the cursor theme

GDM disregards [GNOME](/index.php/GNOME "GNOME") cursor theme settings and it also ignores the cursor theme set according to the [XDG specification](/index.php/Cursor_themes#XDG_specification "Cursor themes"). To change the cursor theme used in GDM, either create the following keyfile

 `/etc/dconf/db/gdm.d/10-cursor-settings` 
```
[org/gnome/desktop/interface]
cursor-theme='*theme-name'*

```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.desktop.interface cursor-theme '*theme-name*'

```

#### Larger font for log-in screen

Click on the accessibility icon at the top right of the screen (a white circle with the silhouette of a person in the centre) and check the *Large Text* option.

To set a specific scaling factor, you can create the following keyfile:

 `/etc/dconf/db/gdm.d/03-scaling` 
```
[org/gnome/desktop/interface]
text-scaling-factor='*1.25*'
```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.desktop.interface text-scaling-factor '*1.25*'

```

#### Turning off the sound

This tweak disables the audible feedback heard when the system volume is adjusted (via keyboard) on the login screen.

Either create the following keyfile:

 `/etc/dconf/db/gdm.d/04-sound` 
```
[org/gnome/desktop/sound]
event-sounds='false'
```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.desktop.sound event-sounds 'false'

```

#### Make the power button interactive

The behaviour of the power buttons can be configured in GDM. The example below will configure the power and hibernate buttons to *Show dialog*:

Create the following keyfile:

 `/etc/dconf/db/gdm.d/05-power` 
```
[org/gnome/settings-daemon/plugins/power button]
power='interactive'
hibernate='interactive'
```

and then recompile the GDM database.

**Warning:** Please note that the [acpid](/index.php/Acpid "Acpid") daemon also handles the "power button" and "hibernate button" events. Running both systems at the same time may lead to unexpected behaviour.

#### Enabling tap-to-click

Tap-to-click is disabled in GDM (and GNOME) by default, but you can easily enable it with a dconf setting.

**Note:** If you want to do this under X, you have to first set up correct X server access permissions - see [#Configure X server access permission](#Configure_X_server_access_permission).

To directly enable tap-to-click, use:

 `# sudo -u gdm gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true` 

If you prefer to do this with a GUI, use:

 `# sudo -u gdm dconf-editor` 

To check the if it was set correctly, use:

 `$ sudo -u gdm gsettings get org.gnome.desktop.peripherals.touchpad tap-to-click` 

### GDM keyboard layout

See [Keyboard configuration in Xorg#Using X configuration files](/index.php/Keyboard_configuration_in_Xorg#Using_X_configuration_files "Keyboard configuration in Xorg").

**Tip:** See [Wikipedia:ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1 "wikipedia:ISO 3166-1") for a list of keymaps.

#### GNOME Control Center

If the package [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) is installed, the keyboard layout(s) can be configured using a graphical frontend. Start *gnome-control-center* and navigate to *Keyboard -> Input Sources*. Then, in the header bar, hit the *Login Screen* toggle button to configure the keyboard layout for GDM specifically.

#### GDM 2.x layout

Users of legacy GDM may need to follow the instructions below:

Edit `~/.dmrc`:

 `~/.dmrc` 
```
[Desktop]
Language=de_DE.UTF-8   # change to your default lang
Layout=de   nodeadkeys # change to your keyboard layout
```

### Change the language

To change the GDM language, ensure that [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) is installed. Then, start *gnome-control-center* and choose *Region & Language*. In the header bar, check the *Login Screen* toggle button. Finally, click on *Language* and choose your language from the list. You will be prompted for your root password.

Alternatively, edit the file `/var/lib/AccountsService/users/gdm` and change the language line using the correct UTF-8 value for your language. You should see something similar to the text below:

 `/var/lib/AccountsService/users/gdm` 
```
[User]
Language=fr_FR.UTF-8
XSession=
SystemAccount=true
```

Now just reboot your computer.

Once you have rebooted, if you look at the `/var/lib/AccountsService/users/gdm` file again, you will see that the language line is cleared — do not worry, the language change has been preserved.

### Automatic login

To enable automatic login with GDM, add the following to `/etc/gdm/custom.conf` (replace *username* with your own):

 `/etc/gdm/custom.conf` 
```
# Enable automatic login for user
[daemon]
AutomaticLogin=*username*
AutomaticLoginEnable=True
```

**Tip:** If GDM fails after adding these lines, comment them out from a TTY.

or for an automatic login with a delay:

 `/etc/gdm/custom.conf` 
```
[daemon]

TimedLoginEnable=true
TimedLogin=*username*
TimedLoginDelay=1
```

### Passwordless login

If you want to bypass the password prompt in GDM then simply add the following line on the first line of `/etc/pam.d/gdm-password`:

```
auth sufficient pam_succeed_if.so user ingroup nopasswdlogin

```

Then, add the group `nopasswdlogin` to your system. See [Groups](/index.php/Groups "Groups") for group descriptions and group management commands.

Now, add your user to the `nopasswdlogin` group and you will only have to click on your username to login.

**Warning:**

*   Do **not** do this for a **root** account.
*   You won't be able to change your session type at login with GDM anymore. If you want to change your default session type, you will first need to remove your user from the `nopasswdlogin` group.

### Passwordless shutdown for multiple sessions

GDM uses polkit and logind to gain permissions for shutdown. You can shutdown the system when multiple users are logged in by setting:

 `/etc/polkit-1/localauthority.conf.d/org.freedesktop.logind.policy` 
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE policyconfig PUBLIC
 "-//freedesktop//DTD PolicyKit Policy Configuration 1.0//EN"
 "[http://www.freedesktop.org/standards/PolicyKit/1.0/policyconfig.dtd](http://www.freedesktop.org/standards/PolicyKit/1.0/policyconfig.dtd)">

<policyconfig>

  <action id="org.freedesktop.login1.power-off-multiple-sessions">
    <description>Shutdown the system when multiple users are logged in</description>
    <message>System policy prevents shutting down the system when other users are logged in</message>
    <defaults>
      <allow_inactive>yes</allow_inactive>
      <allow_active>yes</allow_active>
    </defaults>
  </action>

</policyconfig>
```

You can find all available logind options (e.g. reboot-multiple-sessions) [here](http://www.freedesktop.org/wiki/Software/systemd/logind#Security).

### Add or edit GDM sessions

Each session is a `.desktop` file located at `/usr/share/xsessions/`.

**To add a new session:**

1\. Copy an existing `.desktop` file to use as a template for a new session:

```
$ cd /usr/share/xsessions
# cp gnome.desktop other.desktop

```

2\. Modify the template `.desktop` file to open the required window manager:

```
# nano other.desktop

```

If you happen to have KDM installed in parallel, you can alternatively open the new session in KDM which will create the new `.desktop` file. Then return to using GDM and the new session will be available.

See also [Display manager#Session list](/index.php/Display_manager#Session_list "Display manager").

### Enable root login in GDM

It is not advised to login as root, but if necessary you can edit `/etc/pam.d/gdm-password` and add the following line before the line `auth required pam_deny.so`:

`/etc/pam.d/gdm-password`

```
auth            sufficient      pam_succeed_if.so uid eq 0 quiet

```

The file should look something like this:

`/etc/pam.d/gdm-password`

```
...
auth            sufficient      pam_succeed_if.so uid eq 0 quiet
auth            sufficient      pam_succeed_if.so uid >= 1000 quiet
auth            required        pam_deny.so
...

```

You should be able to login as root after restarting GDM.

### Hide user from login list

The users for the gdm user list are gathered by accountsservice. It will automatically hide system users (UID < 1000). To hide ordinary users from the login list create or edit a file named after the user to hide in `/var/lib/AccountsService/users/` to contain at least:

 `/var/lib/AccountsService/users/<username>` 
```
[User]
SystemAccount=true
```

### Rotate login screen

If you have your monitors setup as you like (orientation, primary and so on) in `~/.config/monitors.xml` and want GDM to honor those settings:

```
# cp ~/.config/monitors.xml /var/lib/gdm/.config/monitors.xml

```

Changes will take effect on logout. This is necessary because GDM does not respect `xorg.conf`.

**Note:** Wayland backend may be [ignoring](https://bbs.archlinux.org/viewtopic.php?id=196219) `/var/lib/gdm/.config/monitors.xml` file. See [#Use Xorg backend](#Use_Xorg_backend) to learn how to disable Wayland backend.

### xrandr at login

If you want to run a script using xrandr that affects the login screen you must add a script in `/etc/X11/xinit/xinitrc.d`.

For example, to select automatically a external screen connected through HDMI:

```
#!/bin/sh
EXTERNAL_OUTPUT="HDMI1"
INTERNAL_OUTPUT="eDP1"
if (xrandr | grep $EXTERNAL_OUTPUT | grep " connected "); then
    xrandr --output $INTERNAL_OUTPUT --off --output $EXTERNAL_OUTPUT --auto
else
    xrandr --output $INTERNAL_OUTPUT --auto
fi

```

### Configure X server access permission

You can use the `xhost` command to configure X server access permissions.

For instance, to grant GDM the right to access the X server, use the following command:

 `# xhost +SI:localuser:gdm` 

## Troubleshooting

### Failure to start with AMD Catalyst driver

Downgrade the [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) package or try to use another [display manager](/index.php/Display_manager "Display manager") like [LightDM](/index.php/LightDM "LightDM").

### Failure on logout

If GDM starts up properly on boot, but fails after repeated attempts on logout, try adding this line to the daemon section of `/etc/gdm/custom.conf`:

```
GdmXserverTimeout=60

```

### Xorg 1.16

See [Xorg#Rootless Xorg (v1.16)](/index.php/Xorg#Rootless_Xorg_.28v1.16.29 "Xorg").

### Use Xorg backend

The [Wayland](/index.php/Wayland "Wayland") backend is used by default and the [Xorg](/index.php/Xorg "Xorg") backend is used only if the Wayland backend cannot be started. As the Wayland backend has been [reported](https://bugzilla.redhat.com/show_bug.cgi?id=1199890) to cause problems for some users, use of the Xorg backend may be necessary. To use the Xorg backend by default, edit the `/etc/gdm/custom.conf` file and uncomment the following line:

```
#WaylandEnable=false

```

### Incomplete removal of gdm

After removing gdm (say it was a build dependancy), systemd may report the following:

```
user 'gdm': directory '/var/lib/gdm' does not exist

```

To remove this warning, login as root and delete the primary user "gdm" and then delete the group "gdm":

```
#userdel gdm
#groupdel gdm

```

Verify that gdm is successfully removed via `pwck` and `grpck`. To round it off, you may want to double-check no [unowned files](/index.php/Pacman/Tips_and_tricks#Identify_files_not_owned_by_any_package "Pacman/Tips and tricks") for gdm remain.

## See also

*   [GDM Reference Manual](https://help.gnome.org/admin/gdm/stable/index.html.en)