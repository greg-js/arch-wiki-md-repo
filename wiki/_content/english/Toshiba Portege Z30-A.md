High-performance ultrabook laptop of Toshiba think for professionals and business. Portégé Z30-A is a long-lasting battery, full-size ports and Intel® Core™ processor laptop of 13.3" and 1.2Kg.

## Contents

*   [1 Specifications](#Specifications)
*   [2 Installation and configuration](#Installation_and_configuration)
    *   [2.1 CPU & Graphics](#CPU_.26_Graphics)
    *   [2.2 Touchpad](#Touchpad)
    *   [2.3 Bluetooth](#Bluetooth)
    *   [2.4 Wifi](#Wifi)
    *   [2.5 Smart Card Reader](#Smart_Card_Reader)
    *   [2.6 Display Backlight Control](#Display_Backlight_Control)
    *   [2.7 Keyboard Backlight control](#Keyboard_Backlight_control)
    *   [2.8 Fingerprint reader](#Fingerprint_reader)

## Specifications

| Name | Series Toshiba Portege Z30-A |
| Processor | Haswell microarchitecture (4th generation) |
| Screen | 13.3" 1366x768 Widescreen |
| RAM | 4-8-16GB |
| HDD | Toshiba SDD (128 [THNSNJ128GMCU], 256, 512 GB) |
| Optical Drive | none |
| Graphics | Haswell-ULT Integrated Graphics Controller (Intel® HD Graphics 4400) |
| Network | Ethernet - Intel I218-V, Wifi - Intel Wireless 3160 |
| Touchpad | ALPS (Trackstick+Mousepad) |
| Fingerprint reader | USB Validity Sensors |
| Smart Card Reader | O2 Micro, Inc. OZ776 |

## Installation and configuration

### CPU & Graphics

Works perfectly out of the box with the typical installation. More information: [Intel](/index.php/Intel "Intel") & [Microcode](/index.php/Microcode "Microcode")

### Touchpad

Works fully with 3.17+ kernel. For LTS kernel, use the [patch of vencik](https://github.com/vencik/psmouse-dkms-alpsv7) for the multi-touch support.

### Bluetooth

toshiba_bluetooth kernel module is auto-loaded but is not necessary and, in fact, it is counter-productive, since as soon as you disable bluetooth (e.g. with rfkill), it seems to attempt to re-load the Intel bluetooth firmware every few seconds. Just blacklist the module. Create `/etc/modprobe.d/toshiba-blacklist.conf` with:

```
blacklist toshiba_bluetooth

```

### Wifi

[linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) is needed for the correct working of wifi.

### Smart Card Reader

Works perfectly with [ccid](https://www.archlinux.org/packages/?name=ccid) & [opensc](https://www.archlinux.org/packages/?name=opensc) .

### Display Backlight Control

Control with the Fn buttons works correctly in 3.17 and 3.18 kernel. However, in 3.19 kernel, a minimum configuration is needed because `toshiba_acpi` kernel module add some non-necessary backlight control. For controlling with Fn, create `/etc/X11/xorg.conf.d/80-backlight.conf` with

```
Section "Device"
    Identifier "Intel Graphics"
    Driver "intel"
    Option "Backlight" "intel_backlight" # use your backlight that works here
EndSection

```

### Keyboard Backlight control

The backlight works correctly if it is configured on BIOS. `toshiba_acpi` kernel module add support for configuring the backlit of the keyboard. However, Fn-Z does not work. The modules can be changed in `/sys/devices/LNXSYSTM:00/LNXSYBUS:00/TOS6208:00/kbd_backlight_mode` with the modes: 2,8,16.

```
# tee /sys/devices/LNXSYSTM:00/LNXSYBUS:00/TOS6208:00/kbd_backlight_mode <<< 2

```

### Fingerprint reader

The last version of [fprintd](https://www.archlinux.org/packages/?name=fprintd) has support for it. However, the image usually is wrong (lengthened) and needs two, three or more tries to obtain verifications.