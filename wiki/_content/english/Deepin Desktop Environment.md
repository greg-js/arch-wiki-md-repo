Related articles

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [GNOME](/index.php/GNOME "GNOME")
*   [LightDM](/index.php/LightDM "LightDM")

The [Deepin Desktop Environment](https://www.deepin.org/en/?language=en) (DDE) is the [desktop environment](/index.php/Desktop_environment "Desktop environment") of the Chinese [Deepin](https://en.wikipedia.org/wiki/Deepin "wikipedia:Deepin") Linux distribution.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Starting](#Starting)
    *   [2.1 Via a display manager](#Via_a_display_manager)
    *   [2.2 Via xinit](#Via_xinit)
*   [3 Configuration](#Configuration)
    *   [3.1 Customize touchpad gesture behavior](#Customize_touchpad_gesture_behavior)
    *   [3.2 Changing default deepin sounds](#Changing_default_deepin_sounds)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 No background after resuming from standby](#No_background_after_resuming_from_standby)
    *   [4.2 Wireless network does not connect](#Wireless_network_does_not_connect)
    *   [4.3 Bluetooth Menu does not show up / work](#Bluetooth_Menu_does_not_show_up_/_work)
*   [5 Bug reporting](#Bug_reporting)

## Installation

To get a minimal desktop interface, you may start by [installing](/index.php/Install "Install") [deepin](https://www.archlinux.org/groups/x86_64/deepin/) group. This will pull all the basic components.

The [deepin-extra](https://www.archlinux.org/groups/x86_64/deepin-extra/) groups contains some extra applications for a more complete desktop environment.

To be able to use the integrated network administration, the [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) package is required, and the `NetworkManager.service` must be [started and enabled](/index.php/Systemd#Using_units "Systemd").

## Starting

### Via a display manager

To use the default DDE's lightdm greeter you have to modify the configuration file under the `[Seat:*]` section, to state:.

 `/etc/lightdm/lightdm.conf` 
```
[Seat:*]
...
greeter-session=lightdm-deepin-greeter
```

Note that a valid home directory must exist for a user other than root for the greeter to work.

### Via xinit

To use Deepin via [xinit](/index.php/Xinit "Xinit"), you'll need to add the following to your .xinitrc file.

 `~/.xinitrc`  `exec startdde` 

## Configuration

### Customize touchpad gesture behavior

Deepin doesn't officially support customizing the gesture behaviors, but it is possible to manually change this by editing the configuration file. Configuration file directory:

```
/usr/share/dde-daemon/gesture.json

```

If you want to disable specific gesture activity. Set "Action" be "none". For example:

```
{
       "Name": "tap",
       "Direction": "none",
       "Fingers": 3,
       "Action": {
           "Type": "built-in",
           "Action": "none"
       }
   }

```

Reboot or re-login after you edit the file.

### Changing default deepin sounds

While this is not officially supported, it is possible to change or even remove the default sounds that are used by Deepin (ex. login sound). Simply replace the sounds in the directory:

```
/usr/share/sounds/deepin/stereo

```

Note: If you simply want to disable the sound effects entirely, it can be done from Deepin's system settings (sound section).

## Troubleshooting

### No background after resuming from standby

Because of the way the NVIDIA driver stores its FBOs [[1]](https://devtalk.nvidia.com/default/topic/787748/linux/-nvidia340xx-archlinux64-gnome3-14-the-background-of-desktop-and-lockscreen-mess-after-resume-from-/post/4367179/#4367179), it happens that after resuming from standby the background suddenly disappears, leaving only a white screen with possibly some color noise on it. The bug appears to be fixed in GNOME upstream, but the Deepin desktop environment still has it.

A possible workaround would be restarting the window manager every time the computer resumes from suspension. A way to do that would be creating the following systemd service

 `/etc/systemd/system/resume@.service` 
```
[Unit]
Description=User resume actions
After=suspend.target

[Service]
User=%I
Type=simple
ExecStart=/usr/bin/deepin-wm-restart.sh

[Install]
WantedBy=suspend.target

```

That executes the following script

 `/usr/bin/deepin-wm-restart.sh` 
```
#!/bin/bash
export DISPLAY=:0
deepin-wm --replace

```

Once those two files are created in the correct directories, in order to enable the script it's sufficient to run these commands:

```
# chmod +x /usr/bin/deepin-wm-restart.sh
# systemctl enable resume@*user*
# systemctl start resume@*user* 

```

The first command makes the script you created executable, the second makes sure that the service always start at boot and the last one starts the service immediately so you can test the workaround without having to reboot the system.

### Wireless network does not connect

NetworkManager sets the MAC address generated randomly. This was already enabled by default, to disable it add the following lines to the NetworkManager configuration file.

 `/etc/NetworkManager/NetworkManager.conf` 
```
[device]
wifi.scan-rand-mac-address=no

```

### Bluetooth Menu does not show up / work

Enable the `bluetooth.service`. This service is not enabled by default.

```
# systemctl enable bluetooth.service
# systemctl start bluetooth.service

```

## Bug reporting

Any upstream or Arch packaging related bugs should be reported [here](https://github.com/linuxdeepin/developer-center/issues). All the Deepin developers will see the bug reports and solve them as soon as possible.