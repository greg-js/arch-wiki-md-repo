Related articles

*   [Chrome OS devices/Chromebook](/index.php/Chrome_OS_devices/Chromebook "Chrome OS devices/Chromebook")
*   [Chrome OS devices/Custom firmware](/index.php/Chrome_OS_devices/Custom_firmware "Chrome OS devices/Custom firmware")
*   [Installation guide](/index.php/Installation_guide "Installation guide")
*   [Laptop](/index.php/Laptop "Laptop")

**Warning:** This article relies on third-party scripts and modifications, and may irreparably damage your hardware or data. Proceed at your own risk.

This article was created to provide information on how to get Arch installed on the series of Chrome OS devices built by Acer, HP, Samsung, Toshiba, and Google. Currently this page is being overhauled, and more model specific pages are being built with some of the information listed below.

## Contents

*   [1 Introduction](#Introduction)
    *   [1.1 Legacy Boot Mode](#Legacy_Boot_Mode)
        *   [1.1.1 Models without Legacy Boot Mode/SeaBIOS](#Models_without_Legacy_Boot_Mode/SeaBIOS)
    *   [1.2 Firmware write protection intro](#Firmware_write_protection_intro)
    *   [1.3 Prerequisites](#Prerequisites)
*   [2 Chrome OS devices](#Chrome_OS_devices)
    *   [2.1 General hardware recommendations and remarks](#General_hardware_recommendations_and_remarks)
*   [3 Installation](#Installation)
    *   [3.1 Enabling developer mode](#Enabling_developer_mode)
    *   [3.2 Accessing the superuser shell](#Accessing_the_superuser_shell)
        *   [3.2.1 Accessing the superuser shell without logging into ChromeOS](#Accessing_the_superuser_shell_without_logging_into_ChromeOS)
        *   [3.2.2 Accessing the superuser shell when logged into ChromeOS](#Accessing_the_superuser_shell_when_logged_into_ChromeOS)
    *   [3.3 Enabling Legacy Boot Mode](#Enabling_Legacy_Boot_Mode)
        *   [3.3.1 Boot to SeaBIOS by default](#Boot_to_SeaBIOS_by_default)
    *   [3.4 Flashing a custom firmware](#Flashing_a_custom_firmware)
    *   [3.5 Installing Arch Linux](#Installing_Arch_Linux)
        *   [3.5.1 Preparing the installation media](#Preparing_the_installation_media)
        *   [3.5.2 Booting the installation media](#Booting_the_installation_media)
*   [4 Post installation configuration](#Post_installation_configuration)
    *   [4.1 Patched kernels](#Patched_kernels)
    *   [4.2 Video driver](#Video_driver)
    *   [4.3 Touchpad and touchscreen](#Touchpad_and_touchscreen)
        *   [4.3.1 Touchpad and touchscreen kernel modules](#Touchpad_and_touchscreen_kernel_modules)
            *   [4.3.1.1 What to do if your touchpad or touchscreen is not supported?](#What_to_do_if_your_touchpad_or_touchscreen_is_not_supported?)
        *   [4.3.2 Touchpad configuration](#Touchpad_configuration)
        *   [4.3.3 Chromium OS input drivers](#Chromium_OS_input_drivers)
    *   [4.4 Fixing suspend](#Fixing_suspend)
        *   [4.4.1 With kernel parameters](#With_kernel_parameters)
        *   [4.4.2 With systemd](#With_systemd)
    *   [4.5 Fixing audio](#Fixing_audio)
        *   [4.5.1 Baytrail based models](#Baytrail_based_models)
        *   [4.5.2 Haswell based models](#Haswell_based_models)
        *   [4.5.3 Chromebook Pixel 2015](#Chromebook_Pixel_2015)
    *   [4.6 Hotkeys](#Hotkeys)
        *   [4.6.1 xkeyboard configuration](#xkeyboard_configuration)
        *   [4.6.2 Sxhkd configuration](#Sxhkd_configuration)
        *   [4.6.3 Xbindkeys configuration](#Xbindkeys_configuration)
            *   [4.6.3.1 Alternate xbindkeys configuration](#Alternate_xbindkeys_configuration)
        *   [4.6.4 Patch xkeyboard-config](#Patch_xkeyboard-config)
        *   [4.6.5 Mapping in Gnome with gsettings set](#Mapping_in_Gnome_with_gsettings_set)
    *   [4.7 Power key and lid switch handling](#Power_key_and_lid_switch_handling)
        *   [4.7.1 Ignore using logind](#Ignore_using_logind)
        *   [4.7.2 Ignore by Gnome](#Ignore_by_Gnome)
*   [5 Known issues](#Known_issues)
    *   [5.1 Syslinux](#Syslinux)
*   [6 See also](#See_also)

## Introduction

### Legacy Boot Mode

All recent Intel-based Chrome OS devices (starting with the 2013 Chromebook Pixel) feature a Legacy Boot Mode, designed to allow the user to boot Linux. Legacy Boot Mode has a dedicated firmware region, `RW_LEGACY`, which is designed to be user-writeable (hence the 'RW' notation) and is completely separate from the ChromeOS portion of the firmware (ie, it is safe to update and cannot brick the device). It is enabled by the [SeaBIOS](http://www.coreboot.org/SeaBIOS) payload of [coreboot](http://www.coreboot.org/), the open-source firmware used for all Chrome OS devices (with the exception of the first generation of Chromebooks and a few early ARM models). SeaBIOS behaves like a traditional BIOS that boots into the MBR of the disk, and from there into standard bootloaders like Syslinux and GRUB.

Models with a Core-i based SoC (Haswell, Broadwell, Skylake, KabyLake) mostly ship with a functional Legacy Boot Mode payload; updating to a 3rd party build can provide bug fixes and additional features. Models with an Atom-based SoC (Baytrail, Braswell, Apollolake) have Legacy Boot Mode capability, but do not ship with a RW_LEGACY/SeaBIOS payload (that part of the firmware is blank). These models require a 3rd party RW_LEGACY firmware to be loaded for Legacy Boot Mode to be functional.

#### Models without Legacy Boot Mode/SeaBIOS

One of the following approaches can be taken in order to install Arch Linux on Chrome OS devices which did not ship with SeaBIOS as part of the installed firmware:

*   If the device supports Legacy Boot Mode, but does not ship with a functional `RW_LEGACY` payload (or doesn't ship with one at all), one can flash a SeaBIOS payload to the `RW_LEGACY` part of the firmware. This is 100% safe, as it writes to a user-writeable area of the firmware image which is completely separate from/does not affect ChromeOS. The easiest way to install/update the RW_LEGACY firmware on your ChromeOS device is via MrChromebox's [Firmware Utility Script](/index.php/Chrome_OS_devices/Custom_firmware#Flashing_with_MrChromebox.27s_Firmware_Utility_Script "Chrome OS devices/Custom firmware"), which supports the widest range of devices and offers the most up-to-date SeaBIOS builds; one can also update the `RW_LEGACY` firmware manually with Chrome OS' `flashrom` (requires downloading/compiling your own build), or use John Lewis' `flash_chromebook_rom.sh` script (no longer supported).

*   Flash a full [custom firmware](/index.php/Custom_firmware_for_Chrome_OS_devices "Custom firmware for Chrome OS devices") which includes either a SeaBIOS or UEFI payload, and removes all the ChromeOS-specific parts.

*   Flash the `BOOT_STUB` part of the firmware. This method replaces the stock ChromeOS payload (depthcharge) with SeaBIOS. This is theoretically a safer approach than flashing the full firmware but there might be some limitations (e.g. no support in suspend or VMX). This is the `Modify ROM to run SeaBIOS exclusively` option in John Lewis' `flash_chromebook_rom.sh` script and `Flash BOOT_STUB firmware` option in MrChromebox's.

*   Take the ChrUbuntu approach which uses the Chrome OS kernel and modules.

*   Build and sign your own kernel, see [[1]](https://plus.google.com/+OlofJohansson/posts/34PYU79eUqP) [[2]](http://pomozok.wordpress.com/2014/10/11/building-chromeos-kernel-without-chroot/) [[3]](https://github.com/drsn0w/chromebook_kernel_tools/blob/master/install_linux.md).

The [Installation](#Installation) process described on this page tries to cover the method of installing Arch Linux on models without SeaBIOS by flashing a custom firmware.

### Firmware write protection intro

All Chrome OS devices features firmware write protection, which restricts write access to certain regions of the flash chip. It is important to be aware of it as one might need to disable the hardware write protection as part of the installation process (to update GBB flags or flash a custom firmware).

For more details see [Firmware write protection](/index.php/Custom_firmware_for_Chrome_OS_devices#Firmware_write_protection "Custom firmware for Chrome OS devices").

### Prerequisites

*   You should claim your free 100GB-1TB of Google Drive space before you install Arch. This needs to happen from ChromeOS(version > 23), not linux. This will sync/backup ChromeOS, as designed
*   Visit the ArchWiki page for your [Chrome OS device](#Chrome_OS_devices).
*   If there is no ArchWiki page for your device then before proceeding, gather information about the device and if you succeed in installing Arch Linux, then consider adding a new ArchWiki page for your model (you can use the [Acer C720](/index.php/Acer_C720 "Acer C720") as an example for device shipped with SeaBios or the [Acer C710](/index.php/Acer_C710_Chromebook "Acer C710 Chromebook") as device that did not ship with it).
*   Read this guide completely and make sure you understand all the steps before making any changes.

## Chrome OS devices

See [Chromebook models](/index.php/Chrome_OS_devices/Chromebook "Chrome OS devices/Chromebook") for hardware comparison with details about SeaBIOS availability and storage expansion.

### General hardware recommendations and remarks

*   MyDigitalSSD M.2 NGFF SSD drives are probably the most popular choice when upgrading the internal SSD of a Chrome OS device. There are multiple accounts of failing MyDigitalSSD SSD drives at the Acer C720 topic on the Arch forums [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1461993#p1461993) [[5]](https://bbs.archlinux.org/viewtopic.php?pid=1474680#p1474680) [[6]](https://bbs.archlinux.org/viewtopic.php?pid=1460460#p1460460) and much more on the web. If the SSD was upgraded to a MyDigitalSSD model then it is highly recommended to backup the system and data frequently. It might be advisable to upgrade the SDD with a different brand. Notice that this might be due to a SSD firmware issue so updating the SSD firmware is highly recommended.
*   Transcend MTS400 M.2 NGFF SSD drives are failing (at least with stock Coreboot firmware) when ALPM is enabled, ATM there is no SSD firmware update that fixing this bug, so it is highly advisable to disabled ALPM if a power management daemon has been installed (which enabled it), see [Resolving SATA power management related errors](/index.php/Solid_State_Drives#Resolving_SATA_power_management_related_errors "Solid State Drives") and [how to disable ALPM in Chrome OS](http://superuser.com/questions/887916/transcend-mts400-ssd-crashes-my-acer-c720-chromebook-how-to-disable-sata-power).

## Installation

**Warning:** Installation on ChromeOS devices that do not ship with SeaBIOS requires flashing a custom firmware, certain types of which have the potential to brick your device. Proceed at your own risk.

**Note:** While the following information should fit all the ChromeOS devices with coreboot firmware (shipped with SeaBIOS payload or without), it is possible that with some models you may need to make further adjustments.

The general installation procedure:

*   Enable developer mode.
*   ChromeOS device with functional Legacy Boot Mode/SeaBIOS:
    *   Enable Legacy Boot Mode.
    *   Set SeaBIOS as default (optional but highly recommended, requires disabling the write protection).
*   ChromeOS device without functional Legacy Boot Mode:
    *   Flash one of the following types of custom firmware
        *   Flash RW_LEGACY firmware (zero risk)
        *   Flash BOOT_STUB firmware (very low risk).
        *   Flash Full custom firmware (low risk).
*   Prepare the installation media.
*   Boot Arch Linux installation media and install Arch.

### Enabling developer mode

[Developer Mode](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices/acer-c720-chromebook#TOC-Developer-Mode) is necessary in order to access the superuser shell inside ChromeOS, which is required for making changes to the system like allow booting through SeaBIOS.

**Warning:** Enabling Developer Mode will wipe all of your data.

To enable developer mode:

*   Press and hold the `Esc + F3 (Refresh)` keys, then press the `Power` button. This enters Recovery Mode.
    *   Chromeboxes have a dedicated Recovery button, which should be pressed/held while powering on
*   Press `Ctrl + D` (no prompt). It will ask you to confirm, then the system will revert its state and enable Developer Mode.

**Note:** Press `Ctrl + D` (or wait 30 seconds for the beep and boot) at the white boot splash screen to enter ChromeOS.

### Accessing the superuser shell

After you have enabled the Developer Mode you will need to access the superuser shell. How you do this depends on whether you have configured ChromeOS or not.

#### Accessing the superuser shell without logging into ChromeOS

If you have not configured ChromeOS, just press `Ctrl + Alt + F2` (F2 is the "forward" arrow on the top row, →), you will see a login prompt.

*   Use `chronos` as the username, it should not prompt you for a password.
*   Become superuser with [sudo](/index.php/Sudo "Sudo"), use the command `sudo su -`.

#### Accessing the superuser shell when logged into ChromeOS

If you have configured ChromeOS already:

*   Open a crosh window with `Ctrl + Alt + T`.
*   Open a bash shell with the `shell` command.
*   Become superuser with [sudo](/index.php/Sudo "Sudo"), use the command `sudo su -` to accomplish that.

### Enabling Legacy Boot Mode

If your ChromeOS device did not ship with Legacy Boot Mode support via SeaBIOS, or you prefer to install a custom firmware, then continue to [Flashing a custom firmware](#Flashing_a_custom_firmware).

This will enable the pre-installed version of SeaBIOS through the Developer Mode screen in coreboot.

*   Inside your superuser shell enter:

```
# crossystem dev_boot_legacy=1

```

*   Reboot the machine.

You can now start SeaBIOS by pressing `Ctrl + L` at the white boot splash screen.

**Note:** If you intend to stay using pre-installed SeaBIOS route and think you will not appreciate having to press `Ctrl + L` every time you boot to reach SeaBIOS, then you can set coreboot to boot to SeaBIOS by default. This requires disabling the hardware firmware write protection.

You should now have SeaBIOS enabled on your ChromeOS device, if you choose to not set it as default then you can continue to [Installing Arch Linux](#Installing_Arch_Linux).

#### Boot to SeaBIOS by default

To boot SeaBIOS by default, you will need to run the [`set_gbb_flags.sh`](https://chromium.googlesource.com/chromiumos/platform/vboot_reference/+/master/scripts/image_signing/set_gbb_flags.sh) script, which is part of ChromeOS. The script uses flashrom and gbb_utility to read the RO_GBB firmware region, modify the flags, and write it back to flash. The GBB flags can also be set using MrChromebox's [Firmware Utility Script](https://mrchromebox.tech/#fwscript) under either ChromeOS or Arch (the latter requiring booting with specific kernel parameters to relax memory access restrictions).

**Warning:** If you do not set the GBB flags, then a fully discharged or disconnected battery will reset `dev_boot_legacy` crossystem flag to its default value, removing the ability to boot in Legacy Boot Mode. While this used to require you to recover Chrome OS and wipe your Arch Linux installation on the internal storage, the GalliumOS developers have created a set of "fixflags" recovery images, which rather than wiping internal storage, will instead simply re-set the `dev_boot_legacy` crossystem flag. See [galliumos.org/fixflags](https://galliumos.org/fixflags)

*   Disable the hardware write protection.

To find the location of the hardware write-protect screw/switch/jumper and how to disable it visit the ArchWiki page for your [ChromeOS device](#Chrome_OS_devices). If there is no information about your device on the ArchWiki then turn to [Developer Information for ChromeOS Devices](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices) and [coreboot's Chromebooks page](http://www.coreboot.org/Chromebooks).

More information about the firmware protection available at the [Custom firmware for ChromeOS devices](/index.php?title=Custom_firmware_for_ChromeOS_devices&action=edit&redlink=1 "Custom firmware for ChromeOS devices (page does not exist)") page.

*   Switch to the [superuser shell](#Accessing_the_superuser_shell).

*   Disable the software write protection.

```
# flashrom --wp-disable

```

*   Check that write protection is disabled.

```
# flashrom --wp-status

```

*   Run `set_gbb_flags.sh` with no parameters.

```
# /usr/share/vboot/bin/set_gbb_flags.sh

```

*   This will list all of the available flags. The ones of interest to us are:

```
GBB_FLAG_DEV_SCREEN_SHORT_DELAY 0x00000001
GBB_FLAG_FORCE_DEV_SWITCH_ON 0x00000008
GBB_FLAG_FORCE_DEV_BOOT_LEGACY 0x00000080
GBB_FLAG_DEFAULT_DEV_BOOT_LEGACY 0x00000400

```

*   So, to set SeaBIOS as default, with a 1s timeout, prevent accidentally exiting Developer Mode via spacebar, and ensure Legacy Boot Mode remains enabled in the event of battery drain/disconnect, we set the flags as such:

```
# /usr/share/vboot/bin/set_gbb_flags.sh 0x489

```

*   Enable back the software write protection.

```
# flashrom --wp-enable

```

**Note:** All of these steps are automated by MrChromebox's Firmware Utility Script, so if using that to install/update your RW_LEGACY firmware, easiest to just set the flags via the script as well.

Your ChromeOS device now will boot to SeaBIOS by default, you can continue to [Installing Arch Linux](#Installing_Arch_Linux), if your device is booting correctly then you can optionally re-enable the hardware write protection.

### Flashing a custom firmware

**Note:** The following steps explain how to flash a custom firmware from ChromeOS, for information on how to flash a custom firmware from Arch Linux visit the [Custom firmware for ChromeOS devices](/index.php?title=Custom_firmware_for_ChromeOS_devices&action=edit&redlink=1 "Custom firmware for ChromeOS devices (page does not exist)") page

*   Disable the hardware write protection.

To find the location of the hardware write-protect screw/switch/jumper and how to disable it visit the ArchWiki page for your [ChromeOS device](#Chrome_OS_devices). If there is no information about your device on the ArchWiki then turn to [Information for ChromeOS Devices](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devicesDeveloper) and [coreboot's Chromebooks page](http://www.coreboot.org/Chromebooks).

More information about the firmware protection available at the [Custom firmware for ChromeOS devices](/index.php?title=Custom_firmware_for_ChromeOS_devices&action=edit&redlink=1 "Custom firmware for ChromeOS devices (page does not exist)") page.

*   Enter the command to run either MrChromebox's or John Lewis's firmware script.

**Note:** The reason for not posting here is to force you to visit the site and read the instructions before proceeding.

*   After the exiting the script, be sure to copy the backed up firmware to an external storage before rebooting the system (if the script doesn't provide that option for you).

You should now have a custom firmware installed on your device, cross your fingers and reboot.

After flashing the firmware you can continue to [Installing Arch Linux](#Installing_Arch_Linux).

### Installing Arch Linux

#### Preparing the installation media

Create an [Arch Linux Installer USB drive](/index.php/USB_flash_installation_media "USB flash installation media").

**Note:** If the USB loads but fails to boot into Arch, it may be due a bug in the syslinux the current (2017.03.01) installer uses. The 2016.11.01 version from the [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive") will work until the issue is resolved.

#### Booting the installation media

*   Plug the USB drive to the ChromeOS device and start SeaBIOS with `Ctrl + L` at the white boot splash screen (if SeaBIOS is not set as default).
*   Press `Esc` to get a boot menu and select the number corresponding to your USB drive.

The Arch Linux installer boot menu should appear and the [installation](/index.php/Installation_guide "Installation guide") process can proceed as normal.

**Note:** For now choose [GRUB](/index.php/GRUB "GRUB") as your bootloader: you can choose MBR or GPT: [Partitioning](/index.php/Partitioning "Partitioning"). If you choose GPT then do not forget to add a [BIOS Boot Partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB"). Also see [Known Issues](#Syslinux).

After finishing installing Arch Linux continue by following the [Post Installation Configuration](#Post_installation_configuration).

## Post installation configuration

### Patched kernels

**Note:** You can most likely ignore this section unless your device requires patched kernel support.

It is recommended to use the official [linux](https://www.archlinux.org/packages/?name=linux) package for most Chrome OS devices with the exception being newer devices which might need patched kernel support such as the Chromebook Pixel 2015.

[linux-samus4](https://aur.archlinux.org/packages/linux-samus4/) provides patches for the Chromebook Pixel 2015 to fix touchpad, touchscreen, and sound functionality which has not been merged into upstream linux yet. More information is available at [its GitHub page](https://github.com/raphael/linux-samus).

If your devices requires a patched kernel, it is advised to review the list of patches and decide if the patch list is getting decidedly small enough that you no longer require a patched kernel and instead you can use the official [linux](https://www.archlinux.org/packages/?name=linux) package instead.

See [kernels](/index.php/Kernels "Kernels") for more information.

### Video driver

See [Intel graphics](/index.php/Intel_graphics "Intel graphics").

### Touchpad and touchscreen

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics"), [libinput](/index.php/Libinput "Libinput"), and [Touchscreen](/index.php/Touchscreen "Touchscreen").

#### Touchpad and touchscreen kernel modules

Since kernel 3.17 all the related patches merged into the upstream sources, meaning the [linux](https://www.archlinux.org/packages/?name=linux) package in core supports these devices.

##### What to do if your touchpad or touchscreen is not supported?

*   Review the list of patches in [linux-chromebook](https://aur.archlinux.org/packages/linux-chromebook/), if a related patch for your Chromebook model exist then [install this package](#Patched_kernels).
*   If there is no such patch do not worry as the developers should be able to add it by request as the Chromium OS sources includes the related changes.
*   You can also try to find the related commits by yourself and create a proper patch, some hints:
    *   Dig into your Chrome OS system, look at the obvious suspects like boot log, `/proc/bus/input/devices` and `/sys/devices`.
    *   The Linux kernel sources for Chromium OS are at [[7]](https://chromium.googlesource.com/chromiumos/third_party/kernel).
    *   Each kernel source for the latest Chromium OS release has its own branch, name convention: `release-R*-*-chromeos-KERNELVER`, where `R*-*` is the Chromium OS release and `KERNELVER` is the kernel version.
    *   Review the git log of `drivers/platform`, `drivers/i2c/busses` and `drivers/input/touchscreen`.
*   [linux-samus4](https://aur.archlinux.org/packages/linux-samus4/) includes touchpad and touchscreen support for the Chromebook Pixel 2015\. More information is available at [its GitHub page](https://github.com/raphael/linux-samus).

#### Touchpad configuration

There are few options how to set the touchpad:

*   Visit the ArchWiki page for your Chromebook model (see [Chromebook models](#Chromebook_Models)) for touchpad xorg.conf.d file.
*   Use a [touchpad configuration tool](/index.php/Touchpad_Synaptics#Configuration_on_the_fly "Touchpad Synaptics").

#### Chromium OS input drivers

[xf86-input-cmt](https://aur.archlinux.org/packages/xf86-input-cmt/) offers a port of the Chromium OS input driver: [xf86-input-cmt](https://github.com/hugegreenbug/xf86-input-cmt) as an alternative for the [Synaptics input driver](/index.php/Synaptics "Synaptics"). It provides tweaked configuration files for most devices, and provides functionality that the [Synaptics input driver](/index.php/Synaptics "Synaptics") does not such as palm rejection. Additionally, it enables functionality not enabled by default in the Chromium OS input driver such as tap-to-drag.

Please note, the input driver does not work under [some circumstances](https://github.com/hugegreenbug/xf86-input-cmt/issues/5) where you have insufficient permissions to access `/dev/input/event` This will affect you if you use [startx](/index.php/Startx "Startx") to load a DE/WM session. If this is the case or if the driver does not load for any other cases, you should run:

```
# usermod -a -G input $USER

```

Where $USER is the current user wanting to use the input driver.

It should also be noted that some users have reported the driver does not work in [GDM](/index.php/GDM "GDM") but works normally after log in. If you are affected by this, you should run:

```
# usermod -a -G input gdm

```

After reboot, you should be able to use the touchpad normally.

### Fixing suspend

**Note:** Lid suspend might not work directly after boot, you might need to wait a little.

The following are instructions to fix the suspend functionality. Users of a pre-installed SeaBIOS or John Lewis' pre-built SeaBIOS you will need this fix. This procedure is not needed with Matt DeVillier's custom firmware since problematic ACPI wake devices (such as `TPAD`) are firmware-disabled.

There have been a few alternatives discussed and those may work better for some. [[8]](https://bbs.archlinux.org/viewtopic.php?pid=1364376#p1364376) [[9]](https://bbs.archlinux.org/viewtopic.php?pid=1364521#p1364521)

To fix suspend, the general idea is to disable the EHCI_PCI module, which interferes with the suspend cycle. There are multiple ways to achieve this.

#### With kernel parameters

Add the following to your GRUB configuration:-

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX_DEFAULT="modprobe.blacklist=ehci_pci"` 

Then [rebuild your grub config](/index.php/GRUB#Generate_the_main_configuration_file "GRUB"). After rebuilding your GRUB config, reboot your computer.

#### With systemd

Sometimes the synaptics touchpad, and various other parts of the laptop are used as wakeup devices causing certain movements of the laptop during suspend to end suspend. In order to disable all wakeup devices except for the laptop lid sensor, create the following `suspend-device-fix.sh` file.

 `/usr/local/sbin/suspend-device-fix.sh` 
```
#!/bin/bash

awk '{if ($1 != "LID0" && $3 == "*enabled") print $1}' < /proc/acpi/wakeup | while read NAME
do echo "$NAME" > /proc/acpi/wakeup
done

exit 0

```

Now give the file executable permissions:

```
# chmod +x /usr/local/sbin/suspend-device-fix.sh

```

Create a systemd service to execute the script on every boot.

 `/etc/systemd/system/suspend-fix.service` 
```
[Unit]
Description=Suspend Fix

[Service]
Type=simple
ExecStart=/usr/local/sbin/suspend-device-fix.sh

[Install]
WantedBy=multi-user.target
```

First [start](/index.php/Start "Start") `suspend-fix.service`. If it properly starts, then [enable](/index.php/Enable "Enable") it to be started on bootup.

Add the following line at the end of `/etc/rc.d/rc.local` (if it does not exist, just create it) to prevent bad handling of EHCI USB:

 `/etc/rc.d/rc.local` 
```
echo 1 > /sys/devices/pci0000\:00/0000\:00\:1d.0/remove

```

Then, create the following `cros-sound-suspend.sh` file. Only the Ath9k binding/unbinding lines are listed below; see the alternatives linked above for additional sound suspend handling if you experience issues.

 `/usr/lib/systemd/system-sleep/cros-sound-suspend.sh` 
```
#!/bin/bash

case $1/$2 in
  pre/*)
    # Unbind ath9k for preventing error and full sleep mode (wakeup by LID after hibernating) 
    echo -n "0000:01:00.0" | tee /sys/bus/pci/drivers/ath9k/unbind
    # Unbind snd_hda_intel for sound
    echo -n "0000:00:1b.0" | tee /sys/bus/pci/drivers/snd_hda_intel/unbind
    echo -n "0000:00:03.0" | tee /sys/bus/pci/drivers/snd_hda_intel/unbind
    ;;
  post/*)
    # Bind ath9k for preventing error and and full sleep mode (wakeup by LID after hibernating) 
    echo -n "0000:01:00.0" | tee /sys/bus/pci/drivers/ath9k/bind
    # bind snd_hda_intel for sound
    echo -n "0000:00:1b.0" | tee /sys/bus/pci/drivers/snd_hda_intel/bind
    echo -n "0000:00:03.0" | tee /sys/bus/pci/drivers/snd_hda_intel/bind
    ;;
esac
```

Make sure to make the script executable:

```
# chmod +x /usr/lib/systemd/system-sleep/cros-sound-suspend.sh

```

Then [rebuild your grub config](/index.php/GRUB#Generate_the_main_configuration_file "GRUB").

### Fixing audio

#### Baytrail based models

Most baytrail models *worked* on [linux](https://www.archlinux.org/packages/?name=linux) but a regression introduced in 4.18.15 broke it, see bug report [[10]](https://lkml.org/lkml/2018/10/30/676). Either, rollback to 4.18.14, compile your own kernel using this patch [[11]](https://patchwork.kernel.org/patch/10667953), or, install linux-max98090 from unofficial user repo [[12]](https://github.com/duffydack/linux-max98090). It is likely that you will also need to use `alsamixer` from [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) to turn on "Left Speaker Mixer Left DAC" and "Right Speaker Mixer Right DAC". For more information, see [[13]](https://bugs.archlinux.org/task/48936).

#### Haswell based models

One or more of followings might help solving audio related issues, setting `snd_hda_intel` module index reported the most useful. It is highly possible that you will not need to make any change.

*   Create `/etc/modprobe.d/alsa.conf`, the option `index` will make sure the analog output is the default (and not HDMI), the option `model` will notify the driver our board model which will make the built-in microphone usable (you can try instead `model=alc283-sense-combo` or `model=,alc283-dac-wcaps`).

 `/etc/modprobe.d/alsa.conf`  `options snd_hda_intel index=1 model=,alc283-chrome` 

*   Use the `~/.asoundrc` file from [[14]](https://gist.githubusercontent.com/dhead666/52d6d7d97eff76935713/raw/5b32ee11a2ebbe7a3ee0f928e49b980361a57548/.asoundrc).

*   If having problems with headphones (perhaps no audio playing), try `alsactl restore` in terminal. Now, ALSA should automatically switch between channels when using headphones/speakers.

*   To fix [Flash](/index.php/Flash "Flash") audio with PulseAudio, use the `~/.asoundrc` file from [[15]](https://gist.githubusercontent.com/dhead666/0eebff16cd9578c5e035/raw/d4c974fcd50565bf116c57b1884170ecb47f8bf6/.asoundrc).

#### Chromebook Pixel 2015

[linux-samus4](https://aur.archlinux.org/packages/linux-samus4/) includes a patch for Broadwell SoC sound devices. [Its GitHub page](https://github.com/raphael/linux-samus) includes additional instructions for initializing the sound device.

### Hotkeys

[The Chromebook function keys](https://support.google.com/chromebook/answer/1047364?hl=en) recognized as standard F1-F10 by the kernel, it is preferable to map them accordingly to their appearance. It would also be nice to get the keys `Delete, Home, End, PgUp, PgDown` which in Chrome OS mapped to `Alt + : BackSpace, Right, Left, Up, Down`.

#### xkeyboard configuration

[xkeyboard-config](https://www.archlinux.org/packages/?name=xkeyboard-config) 2.16-1 added a `chromebook` model that enables the Chrome OS style functions for the function keys. You can, for example, set this using `localectl set-x11-keymap us chromebook`. See the `chromebook` definition in `/usr/share/X11/xkb/symbols/inet` for the full mappings.

#### Sxhkd configuration

One way to set the hotkeys would be by using the [Sxhkd](/index.php/Sxhkd "Sxhkd") daemon. Besides [sxhkd](https://www.archlinux.org/packages/?name=sxhkd), this also requires [amixer](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture"), [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight), and [xautomation](https://www.archlinux.org/packages/?name=xautomation).

*   See [[16]](https://gist.github.com/dhead666/191722ec04842d8d330b) for an example configuration in `~/.config/sxhkd/sxhkdrc`.

#### Xbindkeys configuration

Another way to configure hotkeys would be by using [Xbindkeys](/index.php/Xbindkeys "Xbindkeys"). Besides [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys) this requires [amixer](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture") and [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) and [xvkbd](https://aur.archlinux.org/packages/xvkbd/).

*   See [[17]](https://gist.github.com/dhead666/08562a9a760b18b6e758) for an example configuration in `~/.xbindkeysrc`.
*   See [vilefridge's xbindkeys configuration](https://bbs.archlinux.org/viewtopic.php?id=173418&p=3) for another example.

##### Alternate xbindkeys configuration

[Volchange](http://pastie.org/9550960) (originated in the [Debian User Forums](http://www.debianuserforums.org/viewtopic.php?f=55&t=1453#p14351))) can manipulate the volume with PulseAudio instead of using [amixer](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture"). Besides [Volchange](http://pastie.org/9550960) this requires [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) and [xvkbd](https://aur.archlinux.org/packages/xvkbd/).

*   Download the script from [[18]](http://pastie.org/9550960).
*   Make it executable

```
$ chmod u+x ~/.local/bin/volchange

```

See [[19]](https://gist.github.com/dhead666/4e23b506441ad424e26e) for a matching `~/.xbindkeysrc`.

#### Patch xkeyboard-config

Another option is to install [xkeyboard-config-chromebook](https://aur.archlinux.org/packages/xkeyboard-config-chromebook/), for more details visit [[20]](https://github.com/dhead666/archlinux-pkgbuilds/tree/master/xkeyboard-config-chromebook).

#### Mapping in Gnome with gsettings set

Some of the function keys can be mapped in Gnome with the advantage of HUD notifications on changes (like volume and brightness changes) which can supplement one of the mapping methods mentioned above. This [linked example](https://gist.github.com/dhead666/0b9c1cc9def939705594) maps the brightness and volume actions. Notice that [xdotool](https://www.archlinux.org/packages/?name=xdotool) is required.

### Power key and lid switch handling

#### Ignore using logind

Out of the box, `systemd-logind` will catch power key and lid switch events and handle them: it will shut down the Chromebook on a power key press, and a suspend on a lid close. However, this policy might be a bit harsh given that the power key is an ordinary key at the top right of the keyboard that might be pressed accidentally.

To configure logind to ignore power key presses and lid switches, add the lines to `logind.conf` below.

 `/etc/systemd/logind.conf` 
```
HandlePowerKey=ignore
HandleLidSwitch=ignore
```

Then [restart](/index.php/Restart "Restart") logind for the changes to take effect.

Power key and lid switch events will still be logged to journald by logind. See [Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management").

#### Ignore by Gnome

[Install](/index.php/Install "Install") [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks), open the Tweak Tool and under Power change the Power Button Action.

## Known issues

### Syslinux

Follow Syslinux installation instructions carefully. Try manual installation to see where the problem comes from. If you see [Missing Operation System](/index.php/Syslinux#Missing_operating_system "Syslinux") then it may be because you need to use correct bootloader binary. If syslinux does not work try another [bootloader](/index.php/Bootloader "Bootloader") such as [GRUB](/index.php/GRUB "GRUB").

## See also

*   [Developer Information for Chrome OS Devices at the Chromium Projects site](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices)
*   [BBS topic about the Acer C720](https://bbs.archlinux.org/viewtopic.php?id=173418) which include generic information on Haswell Based Chromebooks.
*   Re-partitioning in Chrome OS [[21]](http://chromeos-cr48.blogspot.co.uk/2012/04/chrubuntu-1204-now-with-double-bits.html), [[22]](http://goo.gl/i817v)
*   [Brent Sullivan's the always updated list of Chrome OS devices](http://bit.ly/NewChromebooks)
*   [Google Chromebook Comparison Chart](http://prodct.info/chromebooks/)