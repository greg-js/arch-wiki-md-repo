Related articles

*   [GNOME](/index.php/GNOME "GNOME")
*   [Display manager](/index.php/Display_manager "Display manager")

From [GDM - GNOME Display Manager](https://wiki.gnome.org/Projects/GDM): "The GNOME Display Manager (GDM) is a program that manages graphical display servers and handles graphical user logins."

[Display managers](/index.php/Display_manager "Display manager") provide [X Window System](/index.php/X_Window_System "X Window System") and [Wayland](/index.php/Wayland "Wayland") users with a graphical login prompt.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Starting](#Starting)
    *   [2.1 Autostarting applications](#Autostarting_applications)
*   [3 Configuration](#Configuration)
    *   [3.1 Log-in screen background image](#Log-in_screen_background_image)
    *   [3.2 DConf configuration](#DConf_configuration)
        *   [3.2.1 Log-in screen logo](#Log-in_screen_logo)
        *   [3.2.2 Changing the cursor theme](#Changing_the_cursor_theme)
        *   [3.2.3 Larger font for log-in screen](#Larger_font_for_log-in_screen)
        *   [3.2.4 Turning off the sound](#Turning_off_the_sound)
        *   [3.2.5 Configure power button behavior](#Configure_power_button_behavior)
        *   [3.2.6 Enabling tap-to-click](#Enabling_tap-to-click)
        *   [3.2.7 Disable/Enable Accessibility Menu](#Disable/Enable_Accessibility_Menu)
    *   [3.3 Keyboard layout](#Keyboard_layout)
    *   [3.4 Change the language](#Change_the_language)
    *   [3.5 Users and login](#Users_and_login)
        *   [3.5.1 Automatic login](#Automatic_login)
        *   [3.5.2 Passwordless login](#Passwordless_login)
        *   [3.5.3 Passwordless shutdown for multiple sessions](#Passwordless_shutdown_for_multiple_sessions)
        *   [3.5.4 Enable root login in GDM](#Enable_root_login_in_GDM)
        *   [3.5.5 Hide user from login list](#Hide_user_from_login_list)
    *   [3.6 Setup default monitor settings](#Setup_default_monitor_settings)
    *   [3.7 Configure X server access permission](#Configure_X_server_access_permission)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Wayland and the proprietary NVIDIA driver](#Wayland_and_the_proprietary_NVIDIA_driver)
    *   [4.2 Failure on logout](#Failure_on_logout)
    *   [4.3 Rootless Xorg](#Rootless_Xorg)
    *   [4.4 Use Xorg backend](#Use_Xorg_backend)
    *   [4.5 GDM freezes with systemd](#GDM_freezes_with_systemd)
    *   [4.6 GDM does not start until input is provided](#GDM_does_not_start_until_input_is_provided)
    *   [4.7 Incomplete removal of gdm](#Incomplete_removal_of_gdm)
    *   [4.8 GDM auto-suspend (GNOME 3.28)](#GDM_auto-suspend_(GNOME_3.28))
    *   [4.9 GDM ignore Wayland and use X.Org by default](#GDM_ignore_Wayland_and_use_X.Org_by_default)
*   [5 See also](#See_also)

## Installation

GDM can be [installed](/index.php/Install "Install") with the [gdm](https://www.archlinux.org/packages/?name=gdm) package, and it is installed as part of the [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group.

If you would prefer to use legacy GDM which was used in GNOME 2 and has its own configuration utility, install the [gdm-old](https://aur.archlinux.org/packages/gdm-old/) package. Note that the rest of this article discusses current GDM, not legacy GDM, unless indicated otherwise.

You might also wish to install the following:

*   **gdm3setup** — An interface to configure GDM3, autologin options and change Shell theme

	[https://github.com/Nano77/gdm3setup](https://github.com/Nano77/gdm3setup) || [gdm3setup-utils](https://aur.archlinux.org/packages/gdm3setup-utils/)

## Starting

To start GDM at boot time [enable](/index.php/Enable "Enable") `gdm.service`.

### Autostarting applications

One might want to autostart certain commands, such as *xrandr* for instance, on login. This can be achieved by adding a command or script to a location that is sourced by the display manager. See [Display manager#Autostarting](/index.php/Display_manager#Autostarting "Display manager") for a list of supported locations.

**Note:** The `/etc/gdm/Init` directory is no longer a supported location, see [[1]](https://bugzilla.gnome.org/show_bug.cgi?id=751602#c2).

## Configuration

### Log-in screen background image

**Note:**

*   Since GNOME 3.16, GNOME Shell themes are now stored as binary files (gresource).
*   This change will be overwritten on subsequent updates of [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell).

Firstly, you need to extract the existing GNOME Shell theme to a folder in your home directory. You can do this using the following script:

 `extractgst.sh` 
```
#!/bin/sh
gst=/usr/share/gnome-shell/gnome-shell-theme.gresource
workdir=${HOME}/shell-theme

for r in `gresource list $gst`; do
	r=${r#\/org\/gnome\/shell/}
	if [ ! -d $workdir/${r%/*} ]; then
	  mkdir -p $workdir/${r%/*}
	fi
done

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
    <file>calendar-today.svg</file>
    <file>checkbox-focused.svg</file>
    <file>checkbox-off-focused.svg</file>
    <file>checkbox-off.svg</file>
    <file>checkbox.svg</file>
    <file>dash-placeholder.svg</file>
    <file>gnome-shell.css</file>
    <file>gnome-shell-high-contrast.css</file>
    <file>icons/message-indicator-symbolic.svg</file>
    <file>icons/pointer-double-click-symbolic.svg</file>
    <file>icons/pointer-drag-symbolic.svg</file>
    <file>icons/pointer-primary-click-symbolic.svg</file>
    <file>icons/pointer-secondary-click-symbolic.svg</file>
    <file>key-enter.svg</file>
    <file>key-hide.svg</file>
    <file>key-layout.svg</file>
    <file>key-shift-latched-uppercase.svg</file>
    <file>key-shift.svg</file>
    <file>key-shift-uppercase.svg</file>
    <file>no-events.svg</file>
    <file>noise-texture.png</file>
    <file>**filename**</file>
    <file>no-notifications.svg</file>
    <file>pad-osd.css</file>
    <file>process-working.svg</file>
    <file>toggle-off-dark.svg</file>
    <file>toggle-off-hc.svg</file>
    <file>toggle-off.svg</file>
    <file>toggle-on-dark.svg</file>
    <file>toggle-on-hc.svg</file>
    <file>toggle-on.svg</file>
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

Then restart `gdm.service` (note that simply logging out is not enough) and you should find that it is using your preferred background image.

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
# machinectl shell gdm@ /bin/bash

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

Change the cursor theme by typing the following, replacing the last word:

```
# sudo -u gdm dbus-launch gsettings set org.gnome.desktop.interface cursor-theme ExampleCursorTheme

```

If this did not work, continue reading this section

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

#### Configure power button behavior

**Note:**

*   The [logind settings](/index.php/Power_management#ACPI_events "Power management") for the power button are overriden by GNOME Settings Daemon. [[2]](https://bugzilla.gnome.org/show_bug.cgi?id=755953#c4)
*   As of GDM 3.18, the power button cannot be set to *interactive*. [[3]](https://bugzilla.gnome.org/show_bug.cgi?id=753713#c6)
*   In some cases, this setting will be ignored and hardcoded defaults will be used. [[4]](https://bugzilla.gnome.org/show_bug.cgi?id=755953#c17)

**Warning:** Please note that the [acpid](/index.php/Acpid "Acpid") daemon also handles the "power button" and "hibernate button" events. Running both systems at the same time may lead to unexpected behaviour.

Either create the following keyfile:

 `/etc/dconf/db/gdm.d/05-power` 
```
[org/gnome/settings-daemon/plugins/power]
power-button-action='*action*'
```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.settings-daemon.plugins.power power-button-action '*action*'

```

where *action* can be one of `nothing`, `suspend` or `hibernate`.

#### Enabling tap-to-click

Tap-to-click is disabled in GDM (and GNOME) by default, but you can easily enable it with a dconf setting.

**Note:** If you want to do this under X, you have to first set up correct X server access permissions - see [#Configure X server access permission](#Configure_X_server_access_permission).

To enable tap-to-click, either create the following keyfile:

 `/etc/dconf/db/gdm.d/06-tap-to-click` 
```
[org/gnome/desktop/peripherals/touchpad]
tap-to-click='true'
```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click 'true'

```

#### Disable/Enable Accessibility Menu

To disable or enable the Accessibility Menu, either create the following keyfile:

 `/etc/dconf/db/gdm.d/07-accessibility` 
```
[org/gnome/desktop/interface]
toolkit-accessibility='*boolean*'
```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.desktop.interface toolkit-accessibility '*boolean*'

```

The menu is disabled when the key is `false`, enabled when it is `true`.

### Keyboard layout

The system keyboard layout will be applied to GDM. See [Keyboard configuration in Xorg#Using X configuration files](/index.php/Keyboard_configuration_in_Xorg#Using_X_configuration_files "Keyboard configuration in Xorg").

**Tip:** See [Wikipedia:ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1 "wikipedia:ISO 3166-1") for a list of keymaps.

If a system has multiple users, it is possible to specify a keyboard layout for GDM to use which is different from the system keyboard layout. Firstly, ensure the package [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) is installed. Then start *gnome-control-center* and navigate to *Region & Language -> Input Sources*. In the header bar, hit the *Login Screen* toggle button and then choose a keyboard layout from the list. Note that the *Login Screen* button will not be visible in the header bar unless multiple users are present on the system [[5]](https://bugzilla.gnome.org/show_bug.cgi?id=741500).

Users of GDM 2.x (legacy GDM) may need to edit `~/.dmrc` as shown below:

 `~/.dmrc` 
```
[Desktop]
Language=de_DE.UTF-8   # change to your default lang
Layout=de   nodeadkeys # change to your keyboard layout
```

### Change the language

The system language will be applied to GDM. If a system has multiple users, it is possible to set a language for GDM different to the system language. In this case, firstly ensure that [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) is installed. Then, start *gnome-control-center* and choose *Region & Language*. In the header bar, check the *Login Screen* toggle button. Finally, click on *Language* and choose your language from the list. You will be prompted for your root password. Note that the *Login Screen* button will not be visible in the header bar unless multiple users are present on the system [[6]](https://bugzilla.gnome.org/show_bug.cgi?id=741500).

**Tip:** By adding 2 different input languages, logging out then selecting your default language GDM will remember your choice once the second option is removed.

### Users and login

#### Automatic login

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

You can set the session used for automatic login (replace `gnome-xorg` with desired session):

 `/var/lib/AccountsService/users/*username*`  `XSession=gnome-xorg` 

#### Passwordless login

If you want to bypass the password prompt in GDM then simply add the following line on the first line of `/etc/pam.d/gdm-password`:

```
auth sufficient pam_succeed_if.so user ingroup nopasswdlogin

```

Then, add the group `nopasswdlogin` to your system. See [User group](/index.php/User_group "User group") for group descriptions and group management commands.

Now, add your user to the `nopasswdlogin` group and you will only have to click on your username to login.

**Warning:**

*   Do **not** do this for a **root** account.
*   You won't be able to change your session type at login with GDM anymore. If you want to change your default session type, you will first need to remove your user from the `nopasswdlogin` group.

#### Passwordless shutdown for multiple sessions

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

#### Enable root login in GDM

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

#### Hide user from login list

The users for the gdm user list are gathered by [AccountsService](https://www.freedesktop.org/wiki/Software/AccountsService/). It will automatically hide system users (UID < 1000). To hide ordinary users from the login list create or edit a file named after the user to hide in `/var/lib/AccountsService/users/` to contain at least:

 `/var/lib/AccountsService/users/*username*` 
```
[User]
SystemAccount=true
```

### Setup default monitor settings

Some [desktop environments](/index.php/Desktop_environments "Desktop environments") store display settings in `~/.config/monitors.xml`. *xrandr* commands are then generated on the base of the file content. GDM has a similar file stored in `/var/lib/gdm/.config/monitors.xml`.

If you have your monitors setup as you like (orientation, scaling, primary and so on) in `~/.config/monitors.xml` and want GDM to honor those settings:

```
$ sudo cp ~/.config/monitors.xml /var/lib/gdm/.config/
$ sudo chown gdm:gdm /var/lib/gdm/.config/monitors.xml

```

The relevant parts of `monitors.xml` for screen rotation and scaling are:

```
<monitors version="2">
  <configuration>
    <logicalmonitor>
      ...
      <scale>2</scale>
      ...
      <transform>
        <rotation>right</rotation>
        <flipped>no</flipped>
      </transform>
      ...
    </logicalmonitor>
  </configuration>
</monitors>

```

Changes will take effect on logout. This is necessary because GDM does not respect `xorg.conf`.

**Note:** If you use GDM under Wayland, you must also use a `monitors.xml` that was created under Wayland. See [GDM bug 224](https://gitlab.gnome.org/GNOME/gdm/issues/224) for more info. Alternatively, you can force GDM to [#Use Xorg backend](#Use_Xorg_backend), and use a `monitors.xml` that was created under Xorg.

### Configure X server access permission

You can use the `xhost` command to configure X server access permissions.

For instance, to grant GDM the right to access the X server, use the following command:

 `# xhost +SI:localuser:gdm` 

## Troubleshooting

### Wayland and the proprietary NVIDIA driver

GDM doesn't work well in Wayland mode with the proprietary [NVIDIA](/index.php/NVIDIA "NVIDIA") driver. When using this driver, GDM will use Xorg instead.[[7]](https://gitlab.gnome.org/GNOME/gdm/merge_requests/46)

To force-enable Wayland, disable the [udev](/index.php/Udev "Udev") rule responsible for disabling Wayland in GDM:

```
# ln -s /dev/null /etc/udev/rules.d/61-gdm.rules

```

### Failure on logout

If GDM starts up properly on boot, but fails after repeated attempts on logout, try adding this line to the daemon section of `/etc/gdm/custom.conf`:

```
GdmXserverTimeout=60

```

### Rootless Xorg

See [Xorg#Rootless Xorg](/index.php/Xorg#Rootless_Xorg "Xorg").

### Use Xorg backend

The [Wayland](/index.php/Wayland "Wayland") backend is used by default, and the [Xorg](/index.php/Xorg "Xorg") backend is used only if the Wayland backend cannot be started. You may wish to use the Xorg backend instead if, for example:

*   The screen [flickers](https://bugzilla.redhat.com/show_bug.cgi?id=1199890)
*   GDM [crashes](https://bbs.archlinux.org/viewtopic.php?id=249334)

To use the Xorg backend by default, uncomment the following line in `/etc/gdm/custom.conf`:

```
#WaylandEnable=false

```

### GDM freezes with systemd

If GDM gets hang-up with `systemctl enable gdm` and `systemctl start gdm` works as expected, apply the config with `systemctl edit gdm` as below:

```
 [Service]
 Type=idle

```

### GDM does not start until input is provided

If, after booting, the screen stays black and GDM does not start until the mouse is moved or something is typed on the keyboard, it may be due to a lack of entropy required for random number generation. To confirm, check that the following line appears inside *systemd-random-seed*’s log (which can be read using `journalctl --unit systemd-random-seed`):

```
Kernel entropy pool is not initialized yet, waiting until it is.

```

To fix this, you can pass the `random.trust_cpu=on` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") if your CPU supports the *RDRAND* instruction, or you can use [haveged](/index.php/Haveged "Haveged") which also provides entropy, albeit it is of allegedly low quality. See [Debian’s article on the topic](https://wiki.debian.org/BoottimeEntropyStarvation "debian:BoottimeEntropyStarvation") for other solutions.

### Incomplete removal of gdm

After removing [gdm](https://www.archlinux.org/packages/?name=gdm), [systemd](/index.php/Systemd "Systemd") may report the following:

```
user 'gdm': directory '/var/lib/gdm' does not exist

```

To remove this warning, login as root and delete the primary user "gdm" and then delete the group "gdm":

```
# userdel gdm
# groupdel gdm

```

Verify that gdm is successfully removed via `pwck` and `grpck`. To round it off, you may want to double-check no [unowned files](/index.php/Pacman/Tips_and_tricks#Identify_files_not_owned_by_any_package "Pacman/Tips and tricks") for gdm remain.

### GDM auto-suspend (GNOME 3.28)

GDM uses a separate dconf database to control power management. You can make GDM behave the same way as user sessions by copying the user settings to GDM's dconf database.

```
$ IFS=$'
'; for x in $(sudo -u *username* gsettings list-recursively org.gnome.settings-daemon.plugins.power); do eval "sudo -u gdm dbus-launch gsettings set $x"; done; unset IFS

```

where `*username*` is your user's name.

Or to simply disable auto-suspend (also run the command with `ac` replaced with `battery` to also disable it while running on battery):

```
$ sudo -u gdm dbus-launch gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type 'nothing'

```

### GDM ignore Wayland and use X.Org by default

Wayland requires Kernel Mode Setting (KMS) running in order to work, and on some machines the GDM process start earlier than KMS, resulting in GDM unable to see Wayland and working only with X.Org. This might result in messages like the following showing up in your log:

```
 gnome-shell[569]: Failed to open gpu '/dev/dri/card0': GDBus.Error:org.freedesktop.DBus.Error.AccessDenied: Operation not permitted
 gnome-shell[569]: Failed to create backend: No GPUs found
 systemd[505]: gnome-shell-wayland.service: Failed with result 'protocol'.
 systemd[505]: Failed to start GNOME Shell on Wayland.

```

You can solve this problem by [starting KMS earlier](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting").

## See also

*   [GDM Reference Manual](https://help.gnome.org/admin/gdm/stable/index.html.en)