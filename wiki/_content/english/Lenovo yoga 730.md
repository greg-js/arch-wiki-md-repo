**Note:** This is work in progress

## Contents

*   [1 Install](#Install)
    *   [1.1 Grub 2](#Grub_2)
    *   [1.2 Systemd boot](#Systemd_boot)
    *   [1.3 Packages](#Packages)
*   [2 Suspend](#Suspend)
*   [3 Backlight](#Backlight)
    *   [3.1 Fingerprint reader](#Fingerprint_reader)
    *   [3.2 Thunderbolt 3](#Thunderbolt_3)
    *   [3.3 OpenCL](#OpenCL)
    *   [3.4 Tablet mode](#Tablet_mode)
    *   [3.5 Pen](#Pen)
    *   [3.6 External display](#External_display)
*   [4 Issues](#Issues)
    *   [4.1 USB-C Charging](#USB-C_Charging)

## Install

### Grub 2

Boot failed for some reason - this might be a strange issue with left over windows "repairing" the boot process

### Systemd boot

This worked after a cold boot - rebooting after install initially failed with a black screen.

### Packages

<caption>Packages to install</caption>
| Package | purpose |
| [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy) | Auto brightness |
| [bolt](https://www.archlinux.org/packages/?name=bolt) | Thunderbolt 3 |
| [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) | Digitiser/Pen support |

## Suspend

Closing the lid doesn't suspend. In `/etc/systemd/logind.conf` uncomment the following:

 `/etc/systemd/logind.conf/etc/systemd/logind.conf` 
```
HandleSuspendKey=suspend
HandleLidSwitch=suspend
```

## Backlight

Works in gnome but can be reduced so far that it goes off, leaving the screen black.

Possible parameters:

 `kernel parameters` 
```

 **Template error:** are you trying to use the = sign? Visit [Help:Template#Escape template-breaking characters](/index.php/Help:Template#Escape_template-breaking_characters "Help:Template") for workarounds.

```

Installing [iio-sensor-proxy](https://www.archlinux.org/packages/?name=iio-sensor-proxy) does auto brightness.

### Fingerprint reader

The device is `Bus 001 Device 005: ID 06cb:0081 Synaptics, Inc.` Nether [fprint](https://www.archlinux.org/packages/?name=fprint) nor [thinkfinger](https://www.archlinux.org/packages/?name=thinkfinger) work, but there is a prototype driver [here](https://github.com/nmikhailov/Validity90).

### Thunderbolt 3

Works once you install [bolt](https://www.archlinux.org/packages/?name=bolt).
**Note:** TODO: Add links to authoritative information on tb3

### OpenCL

add key with
```
gpg2 --recv-key 702353E0F7E48EDB
pacman -S compute-runtime-bin ocl-icd

```

[blender](/index.php/Blender "Blender") doesn't currently support Intel OpenCL

### Tablet mode

Try gnome extension slide-for-keyboard, keyboard automatically disables under gnome.

### Pen

install `xf86-input-wacom`

### External display

HDMI on USB-C adaptor just works

## Issues

### USB-C Charging

With the Gigabyte Aorus 1070 Gaming box, the charging sometimes stops. Doesn't seem to happen in Windows.