## Contents

*   [1 Console](#Console)
    *   [1.1 Using a separate service](#Using_a_separate_service)
    *   [1.2 Extending getty@.service](#Extending_getty.40.service)
    *   [1.3 Bash alternative](#Bash_alternative)
*   [2 X.org](#X.org)
    *   [2.1 startx](#startx)
    *   [2.2 KDM](#KDM)
    *   [2.3 KDE4 Users](#KDE4_Users)
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

## Console

### Using a separate service

*   [Install](/index.php/Install "Install") the package [systemd-numlockontty](https://aur.archlinux.org/packages/systemd-numlockontty/) from the [AUR](/index.php/AUR "AUR").
    Then [enable](/index.php/Enable "Enable") the `numLockOnTty` service.

*   Alternatively, if you do not want to install an aur package to implement this, you can simply create a service file in `/etc/systemd/system` like:
    ```
    [Unit]
    Description=Switch on numlock from tty1 to tty6

    [Service]
    ExecStart=/bin/bash -c 'for tty in /dev/tty{1..6};do /usr/bin/setleds -D +num < \"$tty\";done'

    [Install]
    WantedBy=multi-user.target
    ```

    **Note:** The filename should have a `.service` suffix, e.g. `numlock1to6.service`.
    Do not forget to [enable](/index.php/Enable "Enable") the service after you create it.

### Extending getty@.service

This is simpler than using a separate service (especially since systemd-198) and does not hardcode the number of VTs in a script. Create a directory for drop-in configuration files:

 `# mkdir /etc/systemd/system/getty@.service.d` 

Now add the following file in this directory.

 `activate-numlock.conf` 
```
[Service]
ExecStartPre=/bin/sh -c 'setleds +num < /dev/%I'

```

To disable the num-lock activation hint displaying on the login screen, edit /etc/systemd/system/getty.target.wants/getty@tty1.service. Add the option '--nohints' to the following line:

 `getty@tty1.service` 
```
ExecStart=-/sbin/agetty ....

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

### KDE4 Users

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

In the file `/etc/lxdm/lxdm.conf` uncomment the line:

```
#numlock=0

```

and change to:

```
numlock=1

```