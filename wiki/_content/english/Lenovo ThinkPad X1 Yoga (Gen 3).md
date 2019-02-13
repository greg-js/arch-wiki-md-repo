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

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 BIOS](#BIOS)
    *   [1.1 Thunderbolt BIOS assist potential brick issue](#Thunderbolt_BIOS_assist_potential_brick_issue)
    *   [1.2 EC Fan issues under Linux](#EC_Fan_issues_under_Linux)
    *   [1.3 Updates](#Updates)
        *   [1.3.1 Automatic (Linux Vendor Firmware Service)](#Automatic_(Linux_Vendor_Firmware_Service))
        *   [1.3.2 Manual](#Manual)
*   [2 Suspend issues](#Suspend_issues)
    *   [2.1 Verifying S3](#Verifying_S3)
    *   [2.2 Enabling S3](#Enabling_S3)
        *   [2.2.1 Bios settings [1]](#Bios_settings_[1])
        *   [2.2.2 Generate the override [2]](#Generate_the_override_[2])
        *   [2.2.3 Load the override on boot [3]](#Load_the_override_on_boot_[3])
        *   [2.2.4 Verify that S3 is working (See Verifying S3)](#Verify_that_S3_is_working_(See_Verifying_S3))
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

There is an automated script called x1carbon2018s3 by [fiji-flo](https://github.com/fiji-flo) that was originally intended for use for the X1 Carbon 6th Gen ([source](https://github.com/fiji-flo/x1carbon2018s3)). The script and documentation were updated and maintained by [lsmith77](https://github.com/lsmith77) to adapt it for the X1 Yoga 3rd Gen. The latest known version is in a fork by [ryankhart](https://github.com/ryankhart) currently awaiting a pull request.

(Optional) To check out this script and its history, visit these GitHub repositories:

*   [https://github.com/fiji-flo/x1carbon2018s3](https://github.com/fiji-flo/x1carbon2018s3)
    *   [https://github.com/lsmith77/x1carbon2018s3](https://github.com/lsmith77/x1carbon2018s3)
        *   [https://github.com/ryankhart/x1carbon2018s3](https://github.com/ryankhart/x1carbon2018s3)

**Note:** Be aware, that this may cause the touch screen and stylus to fail to wake up from suspend.

#### Bios settings [[1]](https://github.com/ryankhart/x1carbon2018s3#bios-settings)

Ensure that Boot Mode is set to `Quick` and not `Diagnostic`

Set `Thunderbolt BIOS Assist Mode` to Enabled (via Config → Thunderbolt 3).

Run:

```
 dmesg | grep -A3 'DSDT ACPI'

```

If you see all three of the following lines:

```
 [    0.000000] ACPI: DSDT ACPI table found in initrd [kernel/firmware/acpi/dsdt.aml][0x2338b]
 [    0.000000] Lockdown: ACPI table override is restricted; see man kernel_lockdown.7
 [    0.000000] ACPI: kernel is locked down, ignoring table override

```

rather than just the first line, disable `Secure Boot`

#### Generate the override [[2]](https://github.com/ryankhart/x1carbon2018s3#generating-the-override)

**Note:** The following GitHub repository is a fork of a fork. If any of the parent repositories get updated in the future consider updating all links to this repository

```
 git clone [https://github.com/ryankhart/x1carbon2018s3.git](https://github.com/ryankhart/x1carbon2018s3.git)
 cd x1carbon2018s3/
 chmod +x generate_and_apply_patch.sh
 ./generate_and_apply_patch.sh

```

#### Load the override on boot [[3]](https://github.com/ryankhart/x1carbon2018s3#loading-the-override-on-boot)

Edit your boot loader configuration and add /acpi_override to the initrd line. To ensure S3 is used as sleep default add mem_sleep_default=deep to you kernel parameters.

If you're using systemd-boot your `/boot/loader/entries/arch.conf` might look like this:

```
 title	Arch Linux ACPI
 linux	/vmlinuz-linux
 initrd /intel-ucode.img
 initrd /acpi_override
 initrd /initramfs-linux.img
 options root=/dev/nvme0n1p2 rw i915.enable_guc=3 mem_sleep_default=deep

```

If you're using grub edit `/etc/default/grub` and add the following:

```
 GRUB_EARLY_INITRD_LINUX_CUSTOM=acpi_override
 GRUB_CMDLINE_LINUX_DEFAULT="quiet mem_sleep_default=deep"

```

Then run:

```
 sudo update-grub

```

To verify the setting has been applied correctly run:

```
 sudo cat /boot/grub/grub.cfg | grep initrd

```

You should see:

```
 initrd  /boot/intel-ucode.img /boot/acpi_override /boot/initramfs-4.19-x86_64.img

```

#### Verify that S3 is working [(See Verifying S3)](#Verifying_S3)

Reboot and verify whether S3 is working by running:

```
 dmesg | grep -i "acpi: (supports"

```

You should now see something like this:

```
 [    0.230796] ACPI: (supports S0 S3 S4 S5)

```

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