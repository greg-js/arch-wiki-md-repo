| **Device** | **Status** | **Modules** |
| Video | Working, see tweaks | i915 |
| Wireless | Working, see issues | iwlwifi |
| Bluetooth | Working | bluetooth |
| Audio | Working | snd_hda_intel |
| Touchpad | Working |  ? |
| Touchscreen | Working | hid_multitouch |
| Webcam | Working | uvcvideo |
| Card Reader | Working | rtsx_pci |
| Wireless switch | Working, see issues | intel-hid |
| Function/Multimedia Keys | Working |  ? |

This article covers hardware specific configuration of this laptop, some minor issues remain after customization. These can be performed after an installation of Arch Linux has been finished and the machine rebooted into it.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 Hardware info](#Hardware_info)
    *   [1.1 Hardware options](#Hardware_options)
    *   [1.2 lspci on a 4231](#lspci_on_a_4231)
*   [2 Installation](#Installation)
*   [3 Tweaks](#Tweaks)
    *   [3.1 Brightness / backlight](#Brightness_.2F_backlight)
    *   [3.2 Gnome scaling](#Gnome_scaling)
    *   [3.3 ICC screen calibration (enhanced brightness)](#ICC_screen_calibration_.28enhanced_brightness.29)
    *   [3.4 Video driver](#Video_driver)
*   [4 Issues](#Issues)

## Hardware info

### Hardware options

The HP Spectre x360 name has been used for a number of models over the years. While the overall look & feel of the brick hasn't changed, some hardware configuration changed a lot.

This model was released in November 2015 to replace the 13-4100.

Specifications:

*   Intel i7 Skylake 6560U with Intel Iris 540 graphics (compared to i7 6500 with Intel HD 520 graphics on a 4100)
*   OLED touch screen running at 2560x1440 (compared to LED 1920x1080 on a 4100)
*   500 GB M.2 SDD
*   8 GB RAM

This model has now been succeeded by the [HP Spectre x360 13-w023dx](/index.php/HP_Spectre_x360_13-w023dx "HP Spectre x360 13-w023dx").

### lspci on a 4231

```
00:00.0 Host bridge: Intel Corporation Skylake Host Bridge/DRAM Registers (rev 09)
00:02.0 VGA compatible controller: Intel Corporation Skylake Integrated Graphics (rev 0a)
00:13.0 Non-VGA unclassified device: Intel Corporation Device 9d35 (rev 21)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Device 9d10 (rev f1)
00:1c.1 PCI bridge: Intel Corporation Device 9d11 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-LP LPC Controller (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Multimedia audio controller: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
01:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5227 PCI Express Card Reader (rev 01)
02:00.0 Network controller: Intel Corporation Wireless 7265 (rev 61)
03:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller (rev 01)

```

## Installation

Installing arch is straight forward for everything (disable secure boot, F10 for BIOS, F9 for boot options) but one thing: you may have to disable a BIOS option called "fast boot". While this option is activated in BIOS the machine may boot into Windows no matter what you select. If you make to boot into the latest arch ISO (June 2016) on a USB, arch EFI boot menu hangs. After you installed arch on HDD and moved all of M$ Windows to /dev/null, you may activate that option again. Although no difference in boot performance could be observed with the option activated or deactivated.

## Tweaks

### Brightness / backlight

`/sys/class/backlight/intel_backlight` exists but is not working as of kernel 4.6 and 4.7rc6\. Proposed kernel parameters (such as `acpi_os`) do not remedy the issue. It may be helpful to know that OLED displays by their nature do not have backlight. xrandr offers some neat feature to change brightness of your screen. Depending on your driver (modesetting driver included in Xorg or xf86-video-intel, see [Intel graphics](/index.php/Intel_graphics "Intel graphics")) your screen is named eDP-1 or eDP1\. Use `xrandr` to determine the correct name if in doubt. The following statement changes brightness to 50%.

```
$ xrandr --output eDP1 --brightness .5

```

While this may probably work on non-OLED displays as well, it won't reduce power consumption on non-OLED displays at all. Without in-depth tests and measurements done, it seems like lowering brightness from the default 100% to something more regular 50% extends battery life by some hours.
Since the hotkeys are performing updates on `/sys/class/backlight/intel_backlight` you may use `inotify` to enable brightness adjustment using the hotkeys (see [Backlight#sysfs modified but no brightness change](/index.php/Backlight#sysfs_modified_but_no_brightness_change "Backlight")). The following script does the job:

```
#!/bin/sh

path=/sys/class/backlight/intel_backlight

luminance() {
    read -r level < "$path"/actual_brightness
    bc <<< "scale=10;$level/$max"
}

read -r max < "$path"/max_brightness
xrandr --output eDP1 --brightness "$(luminance)"

inotifywait -me modify --format '' "$path"/actual_brightness | while read; do
    echo $(luminance)
    xrandr --output eDP1 --brightness "$(luminance)"
done

```

The script requires package `bc` to actually calculate the brightness factor. If you store the script at `/usr/share/bin/brightness` (see [Arch filesystem hierarchy](/index.php/Arch_filesystem_hierarchy "Arch filesystem hierarchy")), you may use the following file at `~/.config/autostart/brightness.desktop` to run the script at login to gnome:

```
[Desktop Entry]
Name=brightness
GenericName=brightness
Comment=adjust brightness using hotkeys 
Exec=/usr/local/bin/brightness
Terminal=false
Type=Application
X-GNOME-Autostart-enabled=true

```

While all this fixes brightness issues on the brick quite well, there are still some issues to be solved:

*   Chromium and some other programs reset brightness to 100% upon their first start since reboot.
*   Hotkeys aren't working prior to login.

### Gnome scaling

The screen natively runs at 2560x1440\. Gnome by default assumes a scaling factor of 2 since the screen resolution at y-axis is greater than 1200 [1](https://wiki.gnome.org/HowDoI/HiDpi). With this, at first glance all controls are quite over sized. xrandr offers some nice workaround:

```
xrandr --output eDP1 --scale 1.25x1.25
xrandr --output eDP1 --panning 3200x1800

```

Those commands should be executed in two steps tho. Gnome doesn't adjust size for sure each time. Setting those changes in an autostart script after login is not very reliable if some other programs are started at the same time. Even adding some sleep does not improve reliability to an acceptable level. Testing will be continued since this is a perfect resolution.

### ICC screen calibration (enhanced brightness)

By default the screen colors are well balanced. Default brightness is a major issue: it equals the enormous bright maximum. The scripts described in chapter Brightness / backlight provide some basic brightness control. Unfortunately there is still some brightness reset to maximum on certain events. This can be circumvented by applying an appropriate [ICC calibration profile](/index.php/ICC_profiles "ICC profiles").
Generating such profile requires a colorimeter and [displaycal](https://www.archlinux.org/packages/?name=displaycal) (which is based on [argyllcms](https://www.archlinux.org/packages/?name=argyllcms)). Gnome offers some color calibration [gnome-color-manager](https://www.archlinux.org/packages/?name=gnome-color-manager) as well. Unfortunately Gnome color calibration crashes when using a x-rite Colormunki Display.
[ICC profiles](/index.php/ICC_profiles "ICC profiles") can be obtained from AUR: [icc-x360-qhd](https://aur.archlinux.org/packages/icc-x360-qhd/). Those profiles have been created on a 4231 model (see hardware options for details). Since there are only a few screen manufacturers those ICC profiles should be valid for all QHD (2560x1440) screen models. Be advised to not apply those profiles on any other (incompatible) screen.
The profile is currently based on 406 patches only. Improved profiles will be made available in a later update. Main advantage of applying such profile is the default brightness used. The 120 cdm² profil is best for regular enviroments. Use system settings to apply the profiles.

### Video driver

As mentioned in [Intel graphics](/index.php/Intel_graphics "Intel graphics") some people recommend to stay with the modesetting driver included in Xorg. As of Xorg 1.18.2, Mesa before 12.0 the performance of this driver is inacceptable when it comes to simple tasks like web browsing, scrolling documents or anything alike. On this machine installing [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) improves performance a lot.

## Issues

Issues for which no resolution could be found:

*   Wifi is working. The hotkey for the airplane mode works. Although something strange is going on with the hotkey:
    *   Booting to console leads to some spam of ^@ for like 10 seconds. After this it suddenly stops and you can log in.
    *   Booting to GDM makes the hotkey for airplane mode work. Nothing special. You can login immediately.
    *   Right after login to Gnome the hotkey is spammed and thus airplane mode turned off and on for like 7 seconds. `dmesg` shows some hard faults caused by wifi module being unexpectedly unavailable but nothing else suspicious.
    *   If you wait in GDM for a while, the spam hotkey spam won't happen after login. I.e. the timer is running already while you are in GDM.