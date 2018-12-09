Related articles

*   [Lenovo ThinkPad X1 Carbon (Gen 6)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6) "Lenovo ThinkPad X1 Carbon (Gen 6)")

The Lenovo ThinkPad X1 Yoga, 3th generation is a 2-in-1 convertible laptop introduced in early 2018\. Its design is closely related to the [Lenovo ThinkPad X1 Carbon (Gen 6)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6) "Lenovo ThinkPad X1 Carbon (Gen 6)"). It features a 14" screen, 8th-gen Intel Core processors and integrated [Intel UHD 620 graphics](/index.php/Intel_graphics "Intel graphics").

To ensure you have this version, [install](/index.php/Install "Install") the package [dmidecode](https://www.archlinux.org/packages/?name=dmidecode) and run:

```
# dmidecode -t system | grep Version
	Version: ThinkPad X1 Yoga 3rd

```

| **Device** | **Working** | **Modules** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes | i915, (intel_agp) |
| [Wireless network](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") | Yes | iwlmvm |
| Native Ethernet with [included dongle](https://www3.lenovo.com/us/en/accessories-and-monitors/cables-and-adapters/adapters/CABLE-BO-TP-OneLink%2B-to-RJ45-Adapter/p/4X90K06975) | Yes | ? |
| Mobile broadband | No¹ | ? |
| Audio | Yes | snd_hda_intel |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes | psmouse, rmi_smbus, i2c_i801 |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes | psmouse, rmi_smbus, i2c_i801 |
| TouchScreen | Yes | x86-input-wacom, libwacom |
| Stylus | Yes | x86-input-wacom, libwacom |
| Camera | Yes | uvcvideo |
| Fingerprint Reader | No² | ? |
| [Power management](/index.php/Power_management "Power management") | Partial³ | ? |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes | btusb |
| microSD card reader | Yes | scsi_mod |
| Keyboard Backlight | Yes | thinkpad_acpi |
| Function/Multimedia Keys | Yes | ? |
| 

1.  No working Linux driver for Fibocom L850-GL. See [this thread](https://forums.lenovo.com/t5/Linux-Discussion/X1C-gen-6-Fibocom-L850-GL-Ubuntu-18-04/m-p/4078413) and [this thread](https://forums.lenovo.com/t5/Linux-Discussion/Linux-support-for-WWAN-LTE-L850-GL-on-T580-T480/td-p/4067969) for more info.
2.  [The Validity90 project](https://github.com/nmikhailov/Validity90) began reverse engineering the reader, but updates have stopped recently.
3.  S3 suspend requires BIOS modification - see section on [suspend issues](#Suspend_issues).

 |

## Contents

*   [1 BIOS](#BIOS)
    *   [1.1 Thunderbolt BIOS assist potential brick issue](#Thunderbolt_BIOS_assist_potential_brick_issue)
    *   [1.2 EC Fan issues under Linux](#EC_Fan_issues_under_Linux)
    *   [1.3 Updates](#Updates)
        *   [1.3.1 Automatic (Linux Vendor Firmware Service)](#Automatic_(Linux_Vendor_Firmware_Service))
        *   [1.3.2 Manual](#Manual)
*   [2 Suspend issues](#Suspend_issues)
    *   [2.1 Verifying S3](#Verifying_S3)
    *   [2.2 Enabling S3](#Enabling_S3)
    *   [2.3 Enabling S2idle](#Enabling_S2idle)
*   [3 Tablet Functions](#Tablet_Functions)
    *   [3.1 Stylus](#Stylus)
    *   [3.2 Screen Rotation](#Screen_Rotation)
        *   [3.2.1 With Screen Rotator](#With_Screen_Rotator)

## BIOS

### Thunderbolt BIOS assist potential brick issue

Several linux users reported their systems were bricked after enabling "Thunderbolt BIOS assist" in the UEFI menu. Lenovo has released BIOS version 1.27 which prevents this issue. See this [thread](https://forums.lenovo.com/t5/ThinkPad-X-Series-Laptops/Thinkpad-X1-Yoga-3rd-Gen-Stuck-at-Black-Screen-After-Enabling/td-p/4106952%7Cthis) on the Lenovo forums for details.

### EC Fan issues under Linux

Under BIOS version 1.24 the embedded controller will no longer spin the fan up properly during high system load causing CPU throttling issues. Reverting to version 1.21 will restore normal functions or you can use the [ThinkFan](https://aur.archlinux.org/packages/ThinkFan/) package to control it via the OS. See [Fan speed control#ThinkPad laptops](/index.php/Fan_speed_control#ThinkPad_laptops "Fan speed control") for details.

### Updates

#### Automatic (Linux Vendor Firmware Service)

[In August of 2018 Lenovo has joined](https://blogs.gnome.org/hughsie/2018/08/06/please-welcome-lenovo-to-the-lvfs/) the [Linux Vendor Firmware Service (LVFS)](https://fwupd.org/) project, which enables firmware updates from within the OS. BIOS updates (and possibly other firmware such as the Thunderbolt controller) can be queried for and installed through [fwupd](/index.php/Fwupd "Fwupd").

#### Manual

Download the latest BIOS image from the [Lenovo Thinkpad X1 Yoga 3rd Gen downloads page](https://pcsupport.lenovo.com/ar/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-yoga-3rd-gen-type-20ld-20le-20lf-20lg/downloads). Obtain [geteltorito](https://aur.archlinux.org/packages/geteltorito/) and run `geteltorito.pl -o bios-update.img xxxxxxxx.iso` on the downloaded ISO file to create a valid [El Torito](https://en.wikipedia.org/wiki/El_Torito_(CD-ROM_standard) image file, then flash this file on a USB drive via `dd` like you would flash [Arch installation media](/index.php/USB_flash_installation_media "USB flash installation media"). For further information see [flashing BIOS from Linux](/index.php/Flashing_BIOS_from_Linux#Bootable_optical_disk_emulation "Flashing BIOS from Linux").

The ThinkPad X1 Yoga supports setting a custom splash image at the earliest boot stage (instead of the red "Lenovo" logo), more information can be found in the `README.TXT` located in the `FLASH` folder of the update image.

## Suspend issues

The 3rd Generation X1 Yoga supports S0i3 (also known as Windows Modern Standby), but not S3 by default. Missing S3 also causes hybrid-suspend to go directly to hibernate. Lenovo included a BIOS option to enable S3 fro BIOS 1.30 onward for the [Lenovo ThinkPad X1 Carbon (Gen 6)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6) "Lenovo ThinkPad X1 Carbon (Gen 6)"), but there is no equivalent option for the X1 Yoga as of BIOS version 1.27 (2018-10-21).

### Verifying S3

To check whether S3 is recognized and usable by Linux, run:

```
 dmesg | grep -i "acpi: (supports"

```

and check for `S3` in the list.

### Enabling S3

Untested: there is an automatic patching script for the Carbon X1 Gen.6 [x1carbon2018s3](https://github.com/fiji-flo/x1carbon2018s3), that was written with full instructions on both enabling S3 and verifying the patch worked.

### Enabling S2idle

**Note:** Since [kernel version 4.18](https://patchwork.kernel.org/patch/10550647/) acpi.ec_no_wakeup=1 is set by default

From [the Lenovo forums](https://forums.lenovo.com/t5/Linux-Discussion/X1-Carbon-Gen-6-cannot-enter-deep-sleep-S3-state-aka-Suspend-to/m-p/4016317/highlight/true#M10682): Add the following [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") to enable S2idle support:

```
 acpi.ec_no_wakeup=1

```

For example, for GRUB, one might edit `/etc/default/grub` and edit `GRUB_CMDLINE_LINUX_DEFAULT`:

```
 GRUB_CMDLINE_LINUX_DEFAULT="quiet acpi.ec_no_wakeup=1"

```

then perform

```
 sudo update-grub

```

and restart the system.

**Note:** This supports only S2idle state, not S0i3 state as some seem to have been led to believe!

The power consumption might still be higher than that of the S3 state in this case.

## Tablet Functions

For the most part, the touch screen and stylus work under Xorg after installing [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) package with no issues. See [Tablet PC](/index.php/Tablet_PC "Tablet PC") for further information.

### Stylus

The default stylus buttons are mapped by the wacom driver as follows:

| **Physical Button** | **Xorg mouse number** |
| Top | 2 |
| Bottom | "Eraser" |

These can be changed with xsetwacom. To set the top button of the stylus to the equivalent of a middle click or Xorg mouse button 3:

```
 xsetwacom --set "Wacom Pen and multitouch sensor Pen stylus" Button 2 3

```

To register the "eraser" as a right click use:

```
 xsetwacom --set "Wacom Pen and multitouch sensor Pen eraser" Button 1 2

```

### Screen Rotation

#### With Screen Rotator

Automatic screen rotation works well with ScreenRotator which has no configuration necessary. The touchscreen two finger swipe does not follow rotation at this time. Install [iio-sensor-proxy-git](https://aur.archlinux.org/packages/iio-sensor-proxy-git/) and [screenrotator-git](https://aur.archlinux.org/packages/screenrotator-git/).

**Note:** [ScreenRotator](https://github.com/GuLinux/screenrotator) is in early development stages.