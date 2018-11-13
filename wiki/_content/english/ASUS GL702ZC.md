This page is about the Laptop ROG Strix AMD laptop. Runs pretty good out of the box, with some minor issues.

## Contents

*   [1 Backlight](#Backlight)
*   [2 Fans](#Fans)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Secure Boot](#Secure_Boot)
    *   [3.2 Fans turn 100% and computer becomes unresponsive after long idle time](#Fans_turn_100%_and_computer_becomes_unresponsive_after_long_idle_time)
    *   [3.3 Bluetooth device not found](#Bluetooth_device_not_found)

## Backlight

This ASUS model comes with Radeon RX580\. Backlight with `xbacklight` will not work; since Radeon cards don't support RandR. The relevant module seems to be `amdgpu_bl0`, and `asus::kbd_backlight` for the keyboard backlight.

You need to set the permissions for the `/sys/class/backlight/amdgpu_bl0/brightness` and the keyboard version, as they are only editable by root. The page [Keyboard backlight](/index.php/Keyboard_backlight "Keyboard backlight") suggests a systemd unit or a dbus daemon (that doesn't compile). You can write a DBus daemon yourself, or change permissions some other way. I suggest the following udev rule;

 `/etc/udev/rules.d/backlight.rules` 
```
ACTION=="add", SUBSYSTEM=="backlight", KERNEL=="amdgpu_bl0", RUN+="/bin/chgrp video /sys/class/backlight/%k/brightness"
ACTION=="add", SUBSYSTEM=="backlight", KERNEL=="amdgpu_bl0", RUN+="/bin/chmod g+w /sys/class/backlight/%k/brightness"

```

Then adding the user to the `video` and `input` group. (Default udev rules override for kbd_backlight, so you can't set them to video as well) [brightnessctl](https://aur.archlinux.org/packages/brightnessctl/) is a nice script that can increase and decrease brightness, which can be bound to the media keys.

## Fans

Fans don't have OS control, and handled by ACPI. Upshot is works out of the box, downside is can't configure them.

## Troubleshooting

### Secure Boot

The BIOS has an utility to load your own BIOS keys, which was glitching for my FAT32 formatted USB drive. Tried using keytool, which bricked the computer. I suggest further work into this.

### Fans turn 100% and computer becomes unresponsive after long idle time

Haven't found a fix for this, but reporting this issue nontheless.

### Bluetooth device not found

A patch has been applied for the bluetooth controller, that will prob roll in the 4.18 kernel. See this forum thread; [https://bbs.archlinux.org/viewtopic.php?id=234603](https://bbs.archlinux.org/viewtopic.php?id=234603)