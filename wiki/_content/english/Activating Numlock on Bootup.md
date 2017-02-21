## Contents

*   [1 Console](#Console)
    *   [1.1 Using a separate service](#Using_a_separate_service)
    *   [1.2 Extending getty@.service](#Extending_getty.40.service)
    *   [1.3 Bash alternative](#Bash_alternative)
*   [2 X.org](#X.org)
    *   [2.1 startx](#startx)
    *   [2.2 KDM](#KDM)
    *   [2.3 KDE Plasma Users](#KDE_Plasma_Users)
        *   [2.3.1 Alternate Method](#Alternate_Method)
        *   [2.3.2 Alternate Method 2](#Alternate_Method_2)
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

 `/usr/bin/numlock` 
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
ExecStart=/usr/bin/numlock
StandardInput=tty
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

### Extending getty@.service

This is simpler than using a separate service (especially since systemd-198) and does not hardcode the number of VTs in a script. Create a drop-in snippet for getty@.service which are applied on top of the original unit:

 `# systemctl edit getty\@.service` 
```
[Service]
ExecStartPre=/bin/sh -c 'setleds +num < /dev/%I'

```

To disable the num-lock activation hint displaying on the login screen, edit getty@tty1.service and add `--nohints` to agetty options:

 `# systemctl edit getty@tty1.service` 
```
[Service]
ExecStart=
ExecStart=-/sbin/agetty --nohints --noclear %I $TERM

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

### KDM

If you use KDM as a login manager, add:

```
numlockx on

```

to the `/usr/share/config/kdm/Xsetup`, or the `/opt/kde/share/config/kdm/Xsetup` for KDM3.

Note that this file will be overwritten on update without creating a `.pacnew` file. To prevent this, add the following line to `/etc/pacman.conf` file (omit the leading slash in the path):

```
NoUpgrade = usr/share/config/kdm/Xsetup

```

### KDE Plasma Users

Go to System Settings, under the Hardware/Input Devices/Keyboard item you will find an option to select the behavior of NumLock.

#### Alternate Method

Alternatively, add the script the `~/.kde4/Autostart/numlockx.sh` containing:

```
#!/bin/sh
numlockx on

```

And make it executable:

```
$ chmod +x ~/.kde4/Autostart/numlockx.sh

```

#### Alternate Method 2

This method enables num lock in KDM login screen (e.g. numeric password)

1) Disable "Themed Greeter" in System Settings -> Login Screen

2) in file /usr/share/config/kdm/kdmrc find section

```
 [X-*-Greeter]

```

Right after that line, add this:

```
 NumLock=On

```

### GDM

First make sure that you have [numlockx](https://www.archlinux.org/packages/?name=numlockx) (from extra) installed then add the following code to `/etc/gdm/Init/Default`:

```
if [ -x /usr/bin/numlockx ]; then
      /usr/bin/numlockx on
fi

```

### GNOME

When not using the GDM login manager, numlockx can be added to GNOME's start-up applications.

[Install](/index.php/Install "Install") [numlockx](https://www.archlinux.org/packages/?name=numlockx) from the [official repositories](/index.php/Official_repositories "Official repositories"). Then, add a start-up command to launch `numlockx`.

```
$ gnome-session-properties

```

The above command opens the **Startup Applications Preferences** applet. Click ***Add*** and enter the following:

| Name: | *Numlockx* |
| Command: | */usr/bin/numlockx on* |
| Comment: | *Turns on numlock.* |

**Note:** This is not a system-wide change, repeat these steps for each user wishing to activate NumLock after logging in.

### Xfce

In the file `~/.config/xfce4/xfconf/xfce-perchannel-xml/keyboards.xml`, make sure the following values are set to true:

```
<property name="Numlock" type="bool" value="true"/>
<property name="RestoreNumlock" type="bool" value="true"/>

```

### SDDM

In the file `/etc/sddm.conf`, add the following line under the `[General]` section:

```
[General]
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

Set the option in `~/.config/lqxt/session.conf`:

```
numlock=true

```