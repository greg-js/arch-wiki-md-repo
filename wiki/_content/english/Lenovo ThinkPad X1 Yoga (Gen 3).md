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
| [Power management](/index.php/Power_management "Power management") | Yes | ? |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes | btusb |
| microSD card reader | Yes | scsi_mod |
| Keyboard Backlight | Yes | thinkpad_acpi |
| Function/Multimedia Keys | Yes | ? |
| 

1.  No working Linux driver for Fibocom L850-GL. See [this thread](https://forums.lenovo.com/t5/Linux-Discussion/X1C-gen-6-Fibocom-L850-GL-Ubuntu-18-04/m-p/4078413) and [this thread](https://forums.lenovo.com/t5/Linux-Discussion/Linux-support-for-WWAN-LTE-L850-GL-on-T580-T480/td-p/4067969) for more info.
2.  [The Validity90 project](https://github.com/nmikhailov/Validity90) began reverse engineering the reader, but updates have stopped recently.

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
    *   [2.2 Enabling S3 (with BIOS version 1.33 and after)](#Enabling_S3_(with_BIOS_version_1.33_and_after))
    *   [2.3 Enabling S3 (before BIOS version 1.33)](#Enabling_S3_(before_BIOS_version_1.33))
        *   [2.3.1 Manual method](#Manual_method)
    *   [2.4 Fix touchscreen after resume](#Fix_touchscreen_after_resume)
        *   [2.4.1 Disabling Thunderbolt](#Disabling_Thunderbolt)
        *   [2.4.2 Using s2idle](#Using_s2idle)
        *   [2.4.3 Other methods](#Other_methods)
    *   [2.5 Enabling S2idle](#Enabling_S2idle)
*   [3 Tablet Functions](#Tablet_Functions)
    *   [3.1 Stylus](#Stylus)
    *   [3.2 Screen Rotation](#Screen_Rotation)
        *   [3.2.1 Automatic Screen Rotation in Gnome](#Automatic_Screen_Rotation_in_Gnome)
        *   [3.2.2 With Screen Rotator](#With_Screen_Rotator)
*   [4 Configuration](#Configuration)
    *   [4.1 Fan Control](#Fan_Control)
    *   [4.2 Keyboard Fn Shortcuts](#Keyboard_Fn_Shortcuts)

## BIOS

### Thunderbolt BIOS assist potential brick issue

Several linux users reported their systems were bricked after enabling "Thunderbolt BIOS assist" in the UEFI menu. Lenovo has released BIOS version 1.27 which prevents this issue. See this [thread](https://forums.lenovo.com/t5/ThinkPad-X-Series-Laptops/Thinkpad-X1-Yoga-3rd-Gen-Stuck-at-Black-Screen-After-Enabling/td-p/4106952) on the Lenovo forums for details.

### EC Fan issues under Linux

Under BIOS version 1.24 the embedded controller will no longer spin the fan up properly during high system load causing CPU throttling issues. Reverting to version 1.21 will restore normal functions or you can use the [ThinkFan](https://aur.archlinux.org/packages/ThinkFan/) package to control it via the OS. See [Fan speed control#ThinkPad laptops](/index.php/Fan_speed_control#ThinkPad_laptops "Fan speed control") for details.

### Updates

#### Automatic (Linux Vendor Firmware Service)

[In August of 2018 Lenovo has joined](https://blogs.gnome.org/hughsie/2018/08/06/please-welcome-lenovo-to-the-lvfs/) the [Linux Vendor Firmware Service (LVFS)](https://fwupd.org/) project, which enables firmware updates from within the OS. BIOS updates (and possibly other firmware such as the Thunderbolt controller) can be queried for and installed through [fwupd](/index.php/Fwupd "Fwupd").

#### Manual

Download the latest BIOS image from the [Lenovo Thinkpad X1 Yoga 3rd Gen downloads page](https://pcsupport.lenovo.com/ar/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-yoga-3rd-gen-type-20ld-20le-20lf-20lg/downloads). Obtain [geteltorito](https://aur.archlinux.org/packages/geteltorito/) and run `geteltorito.pl -o bios-update.img xxxxxxxx.iso` on the downloaded ISO file to create a valid [El Torito](https://en.wikipedia.org/wiki/El_Torito_(CD-ROM_standard) image file, then flash this file on a USB drive via `dd` like you would flash [Arch installation media](/index.php/USB_flash_installation_media "USB flash installation media"). For further information see [flashing BIOS from Linux](/index.php/Flashing_BIOS_from_Linux#Bootable_optical_disk_emulation "Flashing BIOS from Linux").

The ThinkPad X1 Yoga supports setting a custom splash image at the earliest boot stage (instead of the red "Lenovo" logo), more information can be found in the `README.TXT` located in the `FLASH` folder of the update image.

## Suspend issues

In the past 3rd Generation X1 Yoga supports S0i3 (also known as Windows Modern Standby), but not S3 by default. This changed as of May, 17, 2019\. Lenovo included a BIOS option to enable S3 from BIOS 1.33 onward.

### Verifying S3

To check whether S3 is recognized and usable by Linux, run:

```
 dmesg | grep -i "acpi: (supports"

```

and check for `S3` in the list.

### Enabling S3 (with BIOS version 1.33 and after)

Since of May 17, 2019, Lenovo released firmware 1.33, which let you enable legacy S3 sleep in UEFI/BIOS. You can find the option in ThinkPad Setup: Config -> Power and disable the option "Optimized Sleep State for Modern Standby".

Optimized Sleep State for Modern Standby (after BIOS 1.35 the wording has changed to "Sleep State"):

*   Disabled: "legacy" S3 sleep (after BIOS 1.35 the wording has changed to "Linux")
*   Enabled: modern standby (after BIOS 1.35 the wording has changed to "Windows 10")

By setting this option to "Disabled", a warning will appear. The warning describes that a reinstallation of your OS might be mandatory. Accept the warning and both Windows and Linux should work fine. You can do this step even if you already installed a patch to enable s3 sleep. After disabling the optimized sleep state in the bios, and if you did the method to enable s3 sleep before the 1.33 bios update, it is best to remove `**GRUB_EARLY_INITRD_LINUX_CUSTOM="/acpi_override"**` in your /etc/default/grub (if you placed that there before), and regenerate the grub cfg using `sudo update-grub`. Don't forget to remove the acpi_override file as well.

Reboot and verify whether S3 is working by running:

```
 dmesg | grep -i "acpi: (supports"

```

You should now see something like this:

```
 [    0.230796] ACPI: (supports S0 S3 S4 S5)

```

### Enabling S3 (before BIOS version 1.33)

There is an automated script called x1carbon2018s3 by [fiji-flo](https://github.com/fiji-flo) that was originally intended for use for the X1 Carbon 6th Gen ([source](https://github.com/fiji-flo/x1carbon2018s3)). The script and documentation were updated and maintained by [lsmith77](https://github.com/lsmith77) to adapt it for the X1 Yoga 3rd Gen. The latest known version is in a fork by [ryankhart](https://github.com/ryankhart) currently awaiting a pull request. These scripts are recommended for debian-based distributions because of the script including debian-based bash commands.

(Optional) To check out this script and its history, visit these GitHub repositories:

*   [https://github.com/fiji-flo/x1carbon2018s3](https://github.com/fiji-flo/x1carbon2018s3)
    *   [https://github.com/lsmith77/x1carbon2018s3](https://github.com/lsmith77/x1carbon2018s3)
        *   [https://github.com/ryankhart/x1carbon2018s3](https://github.com/ryankhart/x1carbon2018s3)

#### Manual method

The manual method can be used in any distribution of Linux. Below is a modified version of [the source instructions](https://gist.github.com/javanna/38d019a373085e1ba0c784597bc7ec73/) because some things are hard to understand.

1\. Reboot, enter BIOS/UEFI. Go to Config - Thunderbolt (TM) 3 - set Thunderbolt BIOS Assist Mode to Enabled. Set also Security - Secure Boot to Disabled.

2\. Install iasl (Intel's compiler/decompiler for ACPI machine language) and cpio. iasl in Ubuntu and possibly other distributions probably do not have the latest release for it to fully work. To make sure you have the latest version, download the [source code](https://acpica.org/downloads/) and make install iasl. cpio can be installed normally with your distribution's package manager

3\. Get a dump of ACPI DSDT table: `cat /sys/firmware/acpi/tables/DSDT > dsdt.aml`

4\. Decompile the dump, which will generate a .dsl source based on the .aml ACPI machine language dump: `iasl -d dsdt.aml`

5\. Download the [patch]([http://kernel.dk/acpi.patch](http://kernel.dk/acpi.patch)) and apply it against dsdt.dsl: `patch --verbose < acpi.patch`

Hunk 2 failed for me, I manually looked for the following in dsdt.dsl:

```
   Name (SS1, 0x00)
   Name (SS2, 0x00)
   Name (SS3, One)
   One
   Name (SS4, One)
   One

```

and replaced it with the following (removing the two "One" lines):

```
   Name (SS1, 0x00)
   Name (SS2, 0x00)
   Name (SS3, One)
   Name (SS4, One)

```

6\. Recompile your patched version of the .dsl source: `iasl -ve -tc dsdt.dsl`

7\. Create a CPIO archive with the correct structure, which GRUB can load on boot. We name the final image acpi_override and copy it into /boot/:

```
 mkdir -p kernel/firmware/acpi
 cp dsdt.aml kernel/firmware/acpi
 find kernel | cpio -H newc --create > acpi_override
 cp acpi_override /boot

```

8\. GRUB needs to boot the kernel with a parameter setting the deep sleep state as default. Edit `/etc/default/grub` and add the following:

```
 `GRUB_CMDLINE_LINUX_DEFAULT="mem_sleep_default=deep"`
 `GRUB_EARLY_INITRD_LINUX_CUSTOM="/boot/acpi_override"`

```

9\. Regenerate the GRUB configuration: `sudo update-grub`

**If the second line of the previous step does not generate the grub to make the initrd lines look like "initrd /boot/acpi_override" in the beginning, then follow the next steps as normal. If it does generate those lines, skip to step 11**

10\. Tell GRUB to load the new DSDT table on boot in its configuration file usually located in `/boot/grub/grub.cfg`. Find the relevant GRUB menu entry and add the new image `/boot/acpi_override` to the initrd lines for the images that you want the s3 sleep to work in:

```
 Before:
 initrd /initramfs-4.17.4-200.fc28.x86_64.img

 After:
 initrd **/boot/acpi_override** /initramfs-4.17.4-200.fc28.x86_64.img

```

11\. Reboot and enjoy having a laptop running Linux again... close the lid and the battery does not get drained in a few hours, also the battery no longer stays warm in sleep mode. To verify that things are working:

```
 dmesg | grep ACPI | grep supports
 #[    0.195933] ACPI: (supports S0 S3 S4 S5)

  cat /sys/power/mem_sleep
 #s2idle [deep]

```

### Fix touchscreen after resume

These fixes were pulled from: [Lenovo Linux Forums](https://forums.lenovo.com/t5/Other-Linux-Discussions/X1Y3-Touchscreen-not-working-after-resume-on-Linux/td-p/4021200)

#### Disabling Thunderbolt

Some users have reported that disabling Thunderbolt in BIOS -> Security -> IO ports -> Thunderbolt permanently fixes the touchscreen issue. As a consequence, docking stations may have some features disabled.

#### Using s2idle

When the above fix is applied to allow S3 suspend, the touchscreen will not work upon resume from sleep.

The touchscreen functionality can be restored by freezing system (s2idle):

create a unit file:

```
 /etc/systemd/system/wake_wacom_hack.service 

```

with content:

```
 [Unit]
 Description= s2idle for 1 second after resume
 After=suspend.target
 [Service]
 Type=oneshot
 ExecStart=/usr/sbin/rtcwake -m freeze -s 1
[Install]
 WantedBy=suspend.target

```

enable in standard way:

```
 sudo systemctl enable wake_wacom_hack.service

```

#### Other methods

Some users have reported this temporary fix: quickly close and open the lid to enable sleep, and use the power button to resume from sleep.

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

#### Automatic Screen Rotation in Gnome

The iio-sensor-proxy package provides automatic screen rotation for me in Gnome. The package is available in the community repo

```
sudo pacman -S iio-sensor-proxy 

```

No configuration was needed for my machine.

#### With Screen Rotator

Automatic screen rotation works well with ScreenRotator which has no configuration necessary. The touchscreen two finger swipe does not follow rotation at this time. Install [iio-sensor-proxy-git](https://aur.archlinux.org/packages/iio-sensor-proxy-git/) and [screenrotator-git](https://aur.archlinux.org/packages/screenrotator-git/).

**Note:** [ScreenRotator](https://github.com/GuLinux/screenrotator) is in early development stages.

## Configuration

Many of the configuration options can be found in [Lenovo ThinkPad X1 Carbon (Gen 6)#Configuration](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6)#Configuration "Lenovo ThinkPad X1 Carbon (Gen 6)"), as the X1 Carbon 6 has a very similar structure to the X1 Yoga 3.

### Fan Control

See [Fan speed control#ThinkPad laptops](/index.php/Fan_speed_control#ThinkPad_laptops "Fan speed control")

### Keyboard Fn Shortcuts

| Keybind | XF86 Event | Keycode | Keysym |
| Fn | XF86WakeUp | 151 | 0x1008ff2b |
| Fn+F1 | XF86AudioMute | 121 | 0x1008ff12 |
| Fn+F2 | XF86AudioLowerVolume | 122 | 0x1008ff11 |
| Fn+F3 | XF86AudioRaiseVolume | 123 | 0x1008ff13 |
| Fn+F4 | XF86AudioMicMute | 198 | 0x1008ffb2 |
| Fn+F5 | XF86MonBrightnessDown | 232 | 0x1008ff03 |
| Fn+F6 | XF86MonBrightnessUp | 233 | 0x1008ff02 |
| Fn+F7 | XF86Display | 235 | 0x1008ff59 |
| Fn+F8 | XF86WLAN | 246 | 0x1008ff95 |
| Fn+F9 | XF86Tools | 179 | 0x1008ff81 |
| Fn+F10 | XF86Bluetooth | 245 | 0x1008ff94 |
| Fn+F11 | ?? |
| Fn+F12 | XF86Favorites | 164 | 0x1008ff30 |