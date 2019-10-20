<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Console](#Console)
    *   [1.1 Using a separate service](#Using_a_separate_service)
    *   [1.2 Extending getty@.service](#Extending_getty@.service)
    *   [1.3 Bash alternative](#Bash_alternative)
*   [2 X.org](#X.org)
    *   [2.1 startx](#startx)
    *   [2.2 MATE](#MATE)
    *   [2.3 KDE Plasma](#KDE_Plasma)
    *   [2.4 GDM](#GDM)
    *   [2.5 GNOME](#GNOME)
    *   [2.6 Xfce](#Xfce)
    *   [2.7 SDDM](#SDDM)
    *   [2.8 SLiM](#SLiM)
    *   [2.9 OpenBox](#OpenBox)
    *   [2.10 LightDM](#LightDM)
    *   [2.11 LXDM](#LXDM)
    *   [2.12 LXQt](#LXQt)

## Console

### Using a separate service

**Tip:** These steps can be automated by [installing](/index.php/Install "Install") the [systemd-numlockontty](https://aur.archlinux.org/packages/systemd-numlockontty/) package and [enabling](/index.php/Enabling "Enabling") the `numLockOnTty` service.

First create a script to set the numlock on relevant TTYs:

 `/usr/local/bin/numlock` 
```
#!/bin/bash

for tty in /dev/tty{1..6}
do
    /usr/bin/setleds -D +num < "$tty";
done

```

Then create and [enable](/index.php/Enable "Enable") a systemd service:

 `/etc/systemd/system/numlock.service` 
```
[Unit]
Description=numlock

[Service]
ExecStart=/usr/local/bin/numlock
StandardInput=tty
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

### Extending getty@.service

This is simpler than using a separate service and does not hardcode the number of VTs in a script. Create a [drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") for `getty@.service` which are applied on top of the original unit:

 `/etc/systemd/system/getty@.service.d/activate-numlock.conf` 
```
[Service]
ExecStartPre=/bin/sh -c 'setleds -D +num < /dev/%I'
```

**Note:** If you experience any problems, try replacing `ExecStartPre` with `ExecStartPost`, and/or disabling the hint as described below.

To disable the num-lock activation hint displaying on the login screen, [edit](/index.php/Edit "Edit") `getty@tty1.service` and add `--nohints` to *agetty* options:

```
[Service]
ExecStart=
ExecStart=-/sbin/agetty '-p -- \\u' --nohints --noclear %I $TERM

```

### Bash alternative

Add `setleds -D +num` to `~/.bash_profile`. Note that, unlike the other methods, this will not take effect until after you log in.

## X.org

Various methods are available.

### startx

Install the [numlockx](https://www.archlinux.org/packages/?name=numlockx) package and add it to the `~/.xinitrc` file before `exec`:

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#

numlockx &

exec window_manager

```

### MATE

By default, MATE saves the last state on logout and restores it during the next login. To enable Numlock on every login, you must change the following DCONF-Values:

```
dconf write org.mate.peripherals-keyboard remember-numlock-state false
dconf write org.mate.peripherals-keyboard numlock-state 'on'

```

### KDE Plasma

Go to *System Settings > Input Devices > Keyboard* and choose desired NumLock behavior in the *NumLock on Plasma Startup* section.

### GDM

**Note:** GDM does not execute scripts in `/etc/gdm/Init` anymore.

Make sure that you have [numlockx](https://www.archlinux.org/packages/?name=numlockx) installed then add the following code to [~/.xprofile](/index.php/Xprofile "Xprofile"):

```
if [ -x /usr/bin/numlockx ]; then
      /usr/bin/numlockx on
fi

```

### GNOME

Run the following command:

```
 $ gsettings set org.gnome.desktop.peripherals.keyboard numlock-state true

```

In order to remember last state of numlock key (whether you disabled or enabled), use:

```
 $ gsettings set org.gnome.desktop.peripherals.keyboard remember-numlock-state true

```

**Note:** The key `numlock-state` was moved from `org.gnome.settings-daemon.peripherals.keyboard` since GNOME 3.34[[1]](https://gitlab.gnome.org/GNOME/gnome-settings-daemon/merge_requests/107)

Alternatively, you can use add `numlockx on` (from [numlockx](https://www.archlinux.org/packages/?name=numlockx) to a startup script, like `~/.bashrc` (if using [Bash](/index.php/Bash "Bash")) or `~/.profile`.

### Xfce

In the file `~/.config/xfce4/xfconf/xfce-perchannel-xml/keyboards.xml`, make sure the following values are set to true:

```
<property name="Numlock" type="bool" value="true"/>
<property name="RestoreNumlock" type="bool" value="true"/>

```

**Note:** If the file does not exist then open Settings > Keyboard, then check and uncheck the `Restore num lock state on startup`. This will create the `keyboards.xml` file.

### SDDM

In the file `/etc/sddm.conf`, under the `[General]` section, set *Numlock* value to *on* :

```
[General]
...
Numlock=on

```

### SLiM

In the file `/etc/slim.conf` find the line and uncomment it (remove the `#`):

```
#numlock             on

```

### OpenBox

In the file `~/.config/openbox/autostart` add the line:

```
numlockx &

```

And then save the file.

### LightDM

See [LightDM#NumLock on by default](/index.php/LightDM#NumLock_on_by_default "LightDM").

### LXDM

Set the option in `/etc/lxdm/lxdm.conf`:

```
numlock=1

```

### LXQt

Set the option in `~/.config/lxqt/session.conf`:

```
[Keyboard]
numlock=true

```