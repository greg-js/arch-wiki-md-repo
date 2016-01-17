# Chrome OS devices

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Chrome OS devices/Chromebook](/index.php/Chrome_OS_devices/Chromebook "Chrome OS devices/Chromebook")
*   [Chrome OS devices/Custom firmware](/index.php/Chrome_OS_devices/Custom_firmware "Chrome OS devices/Custom firmware")
*   [Beginner's guide](/index.php/Beginner%27s_guide "Beginner's guide")
*   [Installation guide](/index.php/Installation_guide "Installation guide")
*   [Laptop](/index.php/Laptop "Laptop")

**Warning:** This article relies on third-party scripts and modifications, and may irreparably damage your hardware or data. Proceed at your own risk.

This article was created to provide information on how to get Arch installed on the series of Chrome OS devices built by Acer, HP, Samsung, Toshiba, and Google. Currently this page is being overhauled, and more model specific pages are being built with some of the information listed below.

## Contents

*   [1 Introduction](#Introduction)
    *   [1.1 Legacy boot](#Legacy_boot)
        *   [1.1.1 Models without SeaBIOS](#Models_without_SeaBIOS)
    *   [1.2 Firmware write protection intro](#Firmware_write_protection_intro)
    *   [1.3 Prerequisites](#Prerequisites)
*   [2 Chrome OS devices](#Chrome_OS_devices)
    *   [2.1 General hardware recommendations and remarks](#General_hardware_recommendations_and_remarks)
*   [3 Installation](#Installation)
    *   [3.1 Enabling developer mode](#Enabling_developer_mode)
    *   [3.2 Accessing the superuser shell](#Accessing_the_superuser_shell)
        *   [3.2.1 Accessing the superuser shell without Chrome OS configuration](#Accessing_the_superuser_shell_without_Chrome_OS_configuration)
        *   [3.2.2 Accessing the superuser shell with Chrome OS configuration](#Accessing_the_superuser_shell_with_Chrome_OS_configuration)
    *   [3.3 Enabling SeaBIOS](#Enabling_SeaBIOS)
        *   [3.3.1 Boot to SeaBIOS by default](#Boot_to_SeaBIOS_by_default)
    *   [3.4 Flashing a custom firmware](#Flashing_a_custom_firmware)
    *   [3.5 Installing Arch Linux](#Installing_Arch_Linux)
        *   [3.5.1 Preparing the installation media](#Preparing_the_installation_media)
        *   [3.5.2 Booting the installation media](#Booting_the_installation_media)
        *   [3.5.3 Alternative installation, Install Arch Linux in addition to Chrome OS](#Alternative_installation.2C_Install_Arch_Linux_in_addition_to_Chrome_OS)
            *   [3.5.3.1 Re-partition the drive](#Re-partition_the_drive)
            *   [3.5.3.2 Fixing the filesystem](#Fixing_the_filesystem)
            *   [3.5.3.3 Continue the installation process](#Continue_the_installation_process)
            *   [3.5.3.4 Choosing between Arch Linux and Chrome OS](#Choosing_between_Arch_Linux_and_Chrome_OS)
*   [4 Post installation configuration](#Post_installation_configuration)
    *   [4.1 Patched kernels](#Patched_kernels)
    *   [4.2 Video driver](#Video_driver)
    *   [4.3 Touchpad and touchscreen](#Touchpad_and_touchscreen)
        *   [4.3.1 Touchpad and touchscreen kernel modules](#Touchpad_and_touchscreen_kernel_modules)
            *   [4.3.1.1 What to do if your touchpad or touchscreen is not supported?](#What_to_do_if_your_touchpad_or_touchscreen_is_not_supported.3F)
        *   [4.3.2 Touchpad configuration](#Touchpad_configuration)
        *   [4.3.3 Chromium OS input drivers](#Chromium_OS_input_drivers)
    *   [4.4 Fixing suspend](#Fixing_suspend)
        *   [4.4.1 With kernel parameters](#With_kernel_parameters)
        *   [4.4.2 With systemd](#With_systemd)
    *   [4.5 Fixing audio](#Fixing_audio)
        *   [4.5.1 Haswell based models](#Haswell_based_models)
        *   [4.5.2 Chromebook Pixel 2015](#Chromebook_Pixel_2015)
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

### Legacy boot

Some of the newer Chrome OS devices (Intel's Haswell and Broadwell based models) feature a "legacy boot" mode that makes it easier to boot Linux and other operating systems. The legacy boot mode is provided by the [SeaBIOS](http://www.coreboot.org/SeaBIOS) payload of [Coreboot](http://www.coreboot.org/), which is the firmware for the Intel based Chrome OS devices (with the exception of the first generation of Chromebooks). SeaBIOS behaves like a traditional BIOS that boots into the MBR of the disk, and from there into standard bootloaders like Syslinux and GRUB.

On the Chrome OS devices that shipped with SeaBIOS, the installation process of Arch Linux should be similar with a few minor adjustments.

#### Models without SeaBIOS

One of the following approaches can be taken in order to install Arch Linux on Chrome OS devices that did not shipped with SeaBIOS as part of the installed firmware:

*   With a very few models it is possible to only flash a SeaBIOS payload to the `RW_LEGACY` part of the firmware flash memory (e.g. Acer C740, Acer C910 and Google Chromebook Pixel 2), it is possible to update the `RW_LEGACY` manually with Chrome OS' `flashrom` or leave it to John Lewis' `flash_chromebook_rom.sh` script to flash SeaBIOS if the script support for a specific device is limited to `RW_LEGACY` update, the advantage with this method is that the stock firmware is not changed (as `RW_LEGACY` was missing).
*   Flash a full [custom firmware](/index.php/Custom_firmware_for_Chrome_OS_devices "Custom firmware for Chrome OS devices") which includes a SeaBIOS payload.
*   Only write to the `BOOT_STUB` part of the firmware flash memory, this method adds a SeaBIOS payload and update the firmware to only load this payload, it is a much safer approach than flashing the full firmware but there might be some limitations (e.g. no support in suspend or VMX), this is the `Modify ROM to run SeaBIOS exclusively` option in John Lewis' `flash_chromebook_rom.sh` script.
*   Take the ChrUbuntu approach which uses the Chrome OS kernel and modules.
*   Build and sign your own kernel, see [[1]](https://plus.google.com/+OlofJohansson/posts/34PYU79eUqP) [[2]](http://pomozok.wordpress.com/2014/10/11/building-chromeos-kernel-without-chroot/) [[3]](https://github.com/drsn0w/chromebook_kernel_tools/blob/master/install_linux.md).

The [Installation](#Installation) process described on this page tries to cover the method of installing Arch Linux on these non SeaBIOS models by flashing a custom firmware.

### Firmware write protection intro

All Chrome OS devices features a firmware write protection. It is important to be aware of it as one might need to disable the write protection as part of the installation process (to update GBB flags or flash a custom firmware).

For more details see [Firmware write protection](/index.php/Custom_firmware_for_Chrome_OS_devices#Firmware_write_protection "Custom firmware for Chrome OS devices").

### Prerequisites

*   You should claim your free 100GB-1TB of Google Drive space before you install Arch. This needs to happen from ChromeOS(version > 23), not linux. This will sync/backup ChromeOS, as designed
*   Visit the ArchWiki page for your [Chrome OS device](#Chrome_OS_devices).
*   If there is no ArchWiki page for your device then before proceeding, gather information about the device and if you succeed in installing Arch Linux, then consider adding a new ArchWiki page for your model (you can use the [Acer C720](/index.php/Acer_C720_Chromebook "Acer C720 Chromebook") as an example for device shipped with SeaBios or the [Acer C710](/index.php/Acer_C710_Chromebook "Acer C710 Chromebook") as device that did not shipped with it).
*   Read this guide completely and make sure you understand all the steps before making any changes.

## Chrome OS devices

See [Chromebook models](/index.php/Chrome_OS_devices/Chromebook "Chrome OS devices/Chromebook") for hardware comparison with details about SeaBIOS availability and storage expansion.

### General hardware recommendations and remarks

*   MyDigitalSSD M.2 NGFF SSD drives are probably the most popular choice when upgrading the internal SSD of a Chrome OS device. There are multiple accounts of failing MyDigitalSSD SSD drives at the Acer C720 topic on the Arch forums [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1461993#p1461993) [[5]](https://bbs.archlinux.org/viewtopic.php?pid=1474680#p1474680) [[6]](https://bbs.archlinux.org/viewtopic.php?pid=1460460#p1460460) and much more on the web. If the SSD was upgraded to a MyDigitalSSD model then it is highly recommended to backup the system and data frequently. It might be advisable to upgrade the SDD with a different brand. Notice that this might be due to a SSD firmware issue so updating the SSD firmware is highly recommended.
*   Transcend MTS400 M.2 NGFF SSD drives are failing (at least with stock Coreboot firmware) when ALPM is enabled, ATM there is no SSD firmware update that fixing this bug, so it is highly advisable to disabled ALPM if a power management daemon has been installed (which enabled it), see [Resolving SATA power management related errors](/index.php/Solid_State_Drives#Resolving_SATA_power_management_related_errors "Solid State Drives") and [how to disable ALPM in Chrome OS](http://superuser.com/questions/887916/transcend-mts400-ssd-crashes-my-acer-c720-chromebook-how-to-disable-sata-power).

## Installation

**Warning:** Installation on Chrome OS devices that do not ship with SeaBIOS requires flashing a custom firmware, a process that may brick your device. Proceed at your own risk.

**Note:** While the following information should fit all the Chrome OS devices with Coreboot firmware (shipped with SeaBIOS payload or without), it is possible that with some models you may need to make further adjustments.

The general installation procedure:

*   Enable developer mode.
*   Chrome OS device with SeaBIOS:
    *   Enable legacy boot / SeaBIOS.
    *   Set SeaBIOS as default (optional but recommended, requires disabling the write protection).
*   Chrome OS device without SeaBIOS:
    *   Flash a custom firmware.
*   Prepare the installation media.
*   Boot Arch Linux installation media and install Arch.

### Enabling developer mode

[Developer Mode](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices/acer-c720-chromebook#TOC-Developer-Mode) is necessary in order to access the superuser shell inside Chrome OS, which is required for making changes to the system like allow booting through SeaBIOS.

**Warning:** Enabling Developer Mode will wipe all of your data.

To enable developer mode:

*   Turn on the Chrome OS device.
*   Press and hold the `Esc + F3 (Refresh)` keys, then press the `Power` button. This enters Recovery Mode.
*   Press `Ctrl + D` (no prompt). It will ask you to confirm, then the system will revert its state and enable Developer Mode.

**Note:** Press `Ctrl + D` (or wait 30 seconds for the beep and boot) at the white boot splash screen to enter Chrome OS.

### Accessing the superuser shell

After you have enabled the Developer Mode you will need to access the superuser shell. How you do this depends on whether you have configured Chrome OS or not.

#### Accessing the superuser shell without Chrome OS configuration

If you have not configured Chrome OS, just press `Ctrl + Alt + F2` (F2 is the "forward" arrow on the top row, →), you will see a login prompt.

*   Use `chronos` as the username, it should not prompt you for a password.
*   Become superuser with `sudo bash`.

#### Accessing the superuser shell with Chrome OS configuration

If you have configured Chrome OS already:

*   Open a crosh window with `Ctrl + Alt + T`.
*   Open a bash shell with the `shell` command.
*   Become superuser with `sudo bash`

### Enabling SeaBIOS

If your Chrome OS device did not ship with SeaBIOS or you prefer to install a custom firmware, then continue to [Flashing a custom firmware](#Flashing_a_custom_firmware).

This method will allow you to access the pre-installed version of SeaBIOS through the Developer Mode screen in Coreboot.

*   Inside your superuser shell enter:

```
# crossystem dev_boot_usb=1 dev_boot_legacy=1

```

*   Reboot the machine.

You can now start SeaBIOS by pressing `Ctrl + L` at the white boot splash screen.

**Note:** If you intend to stay using pre-installed SeaBIOS route and think you will not appreciate having to press `Ctrl + L` every time you boot to reach SeaBIOS then you can set Coreboot to boot to SeaBIOS by default. This currently must be done inside of Chrome OS and requires disabling the write protection (hardware and software), it might be a good idea to do this now so that you will not have to re-install Chrome OS later with recovery install media. If you are choosing to keep Chrome OS (installing Arch on external storage or [on the internal storage side by side with Chrome OS](#Alternative_installation.2C_Install_Arch_Linux_in_addition_to_Chrome_OS) then set SeaBIOS to default later.

You should now have SeaBIOS enabled on your Chrome OS device, if you choose to not set it as default then you can continue to [Installing Arch Linux](#Installing_Arch_Linux).

#### Boot to SeaBIOS by default

To boot SeaBIOS by default, you will need to run [`set_gbb_flags.sh`](https://chromium.googlesource.com/chromiumos/platform/vboot_reference/+/master/scripts/image_signing/set_gbb_flags.sh) in Chrome OS (already included in Chrome OS, it will not work correctly in Arch Linux).

**Warning:** If you do not set the GBB flags then your system might become corrupted on empty battery, resetting `dev_boot_usb` `dev_boot_legacy` to their default values, forcing you to recover Chrome OS and wiping your Arch Linux installation on the internal storage, though it might be possible to modify Chrome OS recovery image to set these values again [[7]](http://dev.chromium.org/chromium-os/developer-information-for-chrome-os-devices/workaround-for-battery-discharge-in-dev-mode).

**Warning:** If you do not disable the write protection before setting the GBB flags you endanger wiping out the RW-LEGACY part of the firmware (i.e. SeaBIOS) and your system might not boot (should be recoverable with Chrome OS recovery media). Updated versions of [`set_gbb_flags.sh`](https://chromium.googlesource.com/chromiumos/platform/vboot_reference/+/master/scripts/image_signing/set_gbb_flags.sh) will not let you set the GBB flags without disabling the write protection.

*   Disable the hardware write protection.

To find the location of the hardware write-protect screw/switch/jumper and how to disable it visit the ArchWiki page for your [Chrome OS device](#Chrome_OS_devices). If there is no information about your device on the ArchWiki then turn to [Information for Chrome OS Devices](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devicesDeveloper) and [Coreboot's Chromebooks page](http://www.coreboot.org/Chromebooks).

More information about the firmware protection available at the [Custom firmware for Chrome OS devices](/index.php/Custom_firmware_for_Chrome_OS_devices#Firmware_write_protection "Custom firmware for Chrome OS devices") page.

*   Inside your [superuser shell](#Accessing_the_superuser_shell) enter:

```
# sudo su

```

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
# set_gbb_flags.sh

```

**Note:** Recent versions of Chrome OS have moved the script to /usr/share/vboot/bin/set_gbb_flags.sh which is not in $PATH by default.

*   Make sure you get the following output, see [[8]](https://johnlewis.ie/how-to-make-seabios-the-default-on-your-acer-c720/).

```
GBB_FLAG_DEV_SCREEN_SHORT_DELAY 0x00000001
GBB_FLAG_FORCE_DEV_SWITCH_ON 0x00000008
GBB_FLAG_FORCE_DEV_BOOT_LEGACY 0x00000080
GBB_FLAG_DEFAULT_DEV_BOOT_LEGACY 0x00000400

```

*   Now set SeaBIOS as default.

```
# set_gbb_flags.sh 0x489

```

*   Enable back the software write protection.

```
# flashrom --wp-enable

```

Your Chrome OS device now will boot to SeaBIOS by default, you can continue to [Installing Arch Linux](#Installing_Arch_Linux), if your device is booting correctly then you should re-enable the hardware write protection.

### Flashing a custom firmware

**Note:** The following steps explain how to flash a custom firmware from Chrome OS, for information on how to flash a custom firmware from Arch Linux visit the [Custom firmware for Chrome OS devices](/index.php/Custom_firmware_for_Chrome_OS_devices "Custom firmware for Chrome OS devices") page

*   Disable the hardware write protection.

To find the location of the hardware write-protect screw/switch/jumper and how to disable it visit the ArchWiki page for your [Chrome OS device](#Chrome_OS_devices). If there is no information about your device on the ArchWiki then turn to [Information for Chrome OS Devices](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devicesDeveloper) and [Coreboot's Chromebooks page](http://www.coreboot.org/Chromebooks).

More information about the firmware protection available at the [Custom firmware for Chrome OS devices](/index.php/Custom_firmware_for_Chrome_OS_devices#Firmware_write_protection "Custom firmware for Chrome OS devices") page.

*   Enter the command shown on the [Download ROM page at John Lewis site](https://johnlewis.ie/custom-chromebook-firmware/rom-download/).

**Note:** The reason for not posting here is to force you to visit the site and read the page before proceeding.

*   After the script exited copy the backed up firmware to an external storage before rebooting the system.

You should now have a custom firmware installed on your device, cross your fingers and reboot.

After flashing the firmware you can continue to [Installing Arch Linux](#Installing_Arch_Linux).

### Installing Arch Linux

#### Preparing the installation media

Create an [Arch Linux Installer USB drive](https://wiki.archlinux.org/index.php/USB_Flash_Installation_Media).

#### Booting the installation media

*   Plug the USB drive to the Chrome OS device and start SeaBIOS with `Ctrl + L` at the white boot splash screen (if SeaBIOS is not set as default).
*   Press `Esc` to get a boot menu and select the number corresponding to your USB drive.

The Arch Linux installer boot menu should appear and the installation process can [proceed as normal](/index.php/Beginners%27_guide#Installation "Beginners' guide").

**Note:** For now choose [GRUB](/index.php/Beginners%27_guide#For_BIOS_motherboards "Beginners' guide") as your bootloader: you can choose MBR or GPT [partitioning schemes](/index.php/Beginners%27_Guide#Partition_schemes "Beginners' Guide"). If you choose GPT then do not forget to add a [BIOS Boot Partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB"). Also see [Known Issues](#Syslinux).

After finishing installing Arch Linux continue by following the [Post Installation Configuration](#Post_installation_configuration).

#### Alternative installation, Install Arch Linux in addition to Chrome OS

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** needs more details and convert the use of the script to manually re-partitioning steps with cgpt (Discuss in [Talk:Chrome OS devices#](https://wiki.archlinux.org/index.php/Talk:Chrome_OS_devices))

It is possible to have both Arch Linux and Chrome OS installed on the internal drive.

##### Re-partition the drive

In order to partition the drive, we will run the first stage of the ChruBuntu script in Chrome OS. After logging in, open a shell with `Ctrl + Alt + T`, run `shell`, then `cd ~/` to enter the home directory. Once there, run the following:

```
curl -L -O [http://goo.gl/9sgchs](http://goo.gl/9sgchs); sudo bash 9sgchs

```

It will ask how much space to partition for the alternate partition. 8GB is a safe number for the 16GB SSD. More than 9 may not work.

##### Fixing the filesystem

Reboot the system so Chrome OS will repair the filesystem after the previous re-partitioning process. Once this is done, verify that the disk space has been reduced by opening a file manager and clicking the gear in the top right of the window.

##### Continue the installation process

[Continue the installation process](#Installing_Arch_Linux) but instead of wiping the internal drive and creating a new filesystem you should install Arch to the existing empty partition that we designated for Arch in the previous step.

So after booting the installation media:

*   Run the command `fdisk -l` to list drives and partitions. Find the internal drive and note the name of the partition matching the size you specified in the ChrUbuntu script.
*   Use `mkfs.ext4 /dev/sdxY` (where xY is drive letter and partition number, eg. /dev/sda7) This will create the filesystem for arch.
*   Following the [instructions for installing GRUB on GPT](https://wiki.archlinux.org/index.php/GRUB2#GUID_Partition_Table_.28GPT.29_specific_instructions), use gdisk to create a 1007kb partition and set the type to EF02.

**Note:** Contrary to what some people say, the grub partition does NOT need to be the first partition on the disk. The existing ChromeOS partitions make this difficult to do anyways.

##### Choosing between Arch Linux and Chrome OS

Reboot your system and press `Ctrl + l` to load SeaBIOS in order to boot into Arch, or press `Ctrl + d` in order to boot into ChromeOS.

Now you can also [set SeaBIOS as default](#Boot_to_SeaBIOS_by_default) (or even later as you are keeping Chrome OS).

## Post installation configuration

### Patched kernels

**Note:** You can most likely ignore this section unless your device requires patched kernel support.

It is recommended to use the official [linux](https://www.archlinux.org/packages/?name=linux) package for most Chrome OS devices with the exception being newer devices which might need patched kernel support such as the Chromebook Pixel 2015.

[linux-samus4](https://aur.archlinux.org/packages/linux-samus4/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): package not found]</sup> provides patches for the Chromebook Pixel 2015 to fix touchpad, touchscreen, and sound functionality which has not been merged into upstream linux yet. More information is available at [its GitHub page](https://github.com/raphael/linux-samus).

If your devices requires a patched kernel, it is advised to review the list of patches and decide if the patch list is getting decidedly small enough that you no longer require a patched kernel and instead you can use the official [linux](https://www.archlinux.org/packages/?name=linux) package instead.

See [kernels](/index.php/Kernels "Kernels") for more information.

### Video driver

See [Intel graphics](/index.php/Intel_graphics "Intel graphics").

### Touchpad and touchscreen

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") and [Touchscreen](/index.php/Touchscreen "Touchscreen").

#### Touchpad and touchscreen kernel modules

Since kernel 3.17 all the related patches merged into the upstream sources, meaning the [linux](https://www.archlinux.org/packages/?name=linux) package in core supports these devices.

##### What to do if your touchpad or touchscreen is not supported?

*   Review the list of patches in [linux-chromebook](https://aur.archlinux.org/packages/linux-chromebook/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/linux-chromebook)]</sup>, if a related patch for your Chromebook model exist then [install this package](#Patched_kernels).
*   If there is no such patch do not worry as the developers should be able to add it by request as the Chromium OS sources includes the related changes.
*   You can also try to find the related commits by yourself and create a proper patch, some hints:
    *   Dig into your Chrome OS system, look at the obvious suspects like boot log, `/proc/bus/input/devices` and `/sys/devices`.
    *   The Linux kernel sources for Chromium OS are at [[9]](https://chromium.googlesource.com/chromiumos/third_party/kernel).
    *   Each kernel source for the latest Chromium OS release has its own branch, name convention: `release-R*-*-chromeos-KERNELVER`, where `R*-*` is the Chromium OS release and `KERNELVER` is the kernel version.
    *   Review the git log of `drivers/platform`, `drivers/i2c/busses` and `drivers/input/touchscreen`.
*   [linux-samus4](https://aur.archlinux.org/packages/linux-samus4/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): package not found]</sup> includes touchpad and touchscreen support for the Chromebook Pixel 2015\. More information is available at [its GitHub page](https://github.com/raphael/linux-samus).

#### Touchpad configuration

There are few options how to set the touchpad:

*   Visit the ArchWiki page for your Chromebook model (see [Chromebook models](#Chromebook_Models)) for touchpad xorg.conf.d file.
*   Use a [touchpad configuration tool](/index.php/Touchpad_Synaptics#Configuration_on_the_fly "Touchpad Synaptics") like [Synaptics](/index.php/Touchpad_Synaptics#Graphical_tools "Touchpad Synaptics") for [KDE](/index.php/KDE "KDE"), although it is said to be currently unmaintained and seems to crash under KDE 4.11, it works well with KDE 4.12.2\. Another utility, [kcm_touchpad](https://aur.archlinux.org/packages/kcm_touchpad/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kcm_touchpad)]</sup>, does not work at all.

#### Chromium OS input drivers

[xf86-input-cmt](https://aur.archlinux.org/packages/xf86-input-cmt/)<sup><small>AUR</small></sup> offers a port of the Chromium OS input driver: [xf86-input-cmt](https://github.com/hugegreenbug/xf86-input-cmt) as an alternative for the [Synaptics input driver](/index.php/Synaptics "Synaptics"). It provides tweaked configuration files for most devices, and provides functionality that the [Synaptics input driver](/index.php/Synaptics "Synaptics") does not such as palm rejection. Additionally, it enables functionality not enabled by default in the Chromium OS input driver such as tap-to-drag.

Please note, the input driver does not work under [some circumstances](https://github.com/hugegreenbug/xf86-input-cmt/issues/5) where you have insufficient permissions to access `/dev/input/event` This will affect you if you use [startx](https://wiki.archlinux.org/index.php/Xinitrc) to load a DE/WM session. If this is the case or if the driver does not load for any other cases, you should run:

```
# usermod -a -G input $USER

```

Where $USER is the current user wanting to use the input driver.

It should also be noted that some users have reported the driver does not work in [GDM](https://wiki.archlinux.org/index.php/GDM) but works normally after log in. If you are affected by this, you should run:

```
# usermod -a -G input gdm

```

After reboot, you should be able to use the touchpad normally.

### Fixing suspend

**Note:** Lid suspend might not work directly after boot, you might need to wait a little.

The following are instructions to fix the suspend functionality. Even if you are using a pre-installed SeaBIOS or John Lewis' pre-built SeaBIOS you will still need this fix.

There have been a few alternatives discussed and those may work better for some. [[10]](https://bbs.archlinux.org/viewtopic.php?pid=1364376#p1364376) [[11]](https://bbs.archlinux.org/viewtopic.php?pid=1364521#p1364521)

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

First start the service.

```
# systemctl start suspend-fix.service

```

If it properly starts, then allow it to be started on bootup.

```
# systemctl enable suspend-fix.service

```

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

#### Haswell based models

One or more of followings might help solving audio related issues, setting `snd_hda_intel` module index reported the most useful. It is highly possible that you will not need to make any change.

*   Create `/etc/modprobe.d/alsa.conf`, the option `index` will make sure the analog output is the default (and not HDMI), the option `model` will notify the driver our board model which will make the built-in microphone usable (you can try instead `model=alc283-sense-combo`).

 `/etc/modprobe.d/alsa.conf`  `options snd_hda_intel index=1 model=alc283-dac-wcaps` 

*   Use the `~/.asoundrc` file from [[12]](https://gist.githubusercontent.com/dhead666/52d6d7d97eff76935713/raw/5b32ee11a2ebbe7a3ee0f928e49b980361a57548/.asoundrc).

*   If having problems with headphones (perhaps no audio playing), try `alsactl restore` in terminal. Now, ALSA should automatically switch between channels when using headphones/speakers.

*   To fix [Flash](/index.php/Flash "Flash") audio with PulseAudio, use the `~/.asoundrc` file from [[13]](https://gist.githubusercontent.com/dhead666/0eebff16cd9578c5e035/raw/d4c974fcd50565bf116c57b1884170ecb47f8bf6/.asoundrc).

#### Chromebook Pixel 2015

[linux-samus4](https://aur.archlinux.org/packages/linux-samus4/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): package not found]</sup> includes a patch for Broadwell SoC sound devices. [Its GitHub page](https://github.com/raphael/linux-samus) includes additional instructions for initializing the sound device.

### Hotkeys

[The Chromebook function keys](https://support.google.com/chromebook/answer/1047364?hl=en) recognized as standard F1-F10 by the kernel, it is preferable to map them accordingly to their appearance. It would also be nice to get the keys `Delete, Home, End, PgUp, PgDown` which in Chrome OS mapped to `Alt + : BackSpace, Right, Left, Up, Down`.

#### xkeyboard configuration

[xkeyboard-config 2.16-1](https://www.archlinux.org/packages/extra/any/xkeyboard-config/) added a <tt>chromebook</tt> model that enables the Chrome OS style functions for the function keys. You can, for example, set this using <tt>localectl set-x11-keymap us chromebook</tt>. See the <tt>chromebook</tt> definition in <tt>/usr/share/X11/xkb/symbols/inet</tt> for the full mappings.

#### Sxhkd configuration

One way to set the hotkeys would be by using the [Sxhkd](/index.php/Sxhkd "Sxhkd") daemon. Besides [sxhkd](https://www.archlinux.org/packages/?name=sxhkd), this also requires [amixer](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture"), [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight), and [xautomation](https://www.archlinux.org/packages/?name=xautomation).

*   See [[14]](https://gist.github.com/dhead666/191722ec04842d8d330b) for an example configuration in `~/.config/sxhkd/sxhkdrc`.

#### Xbindkeys configuration

Another way to configure hotkeys would be by using [Xbindkeys](/index.php/Xbindkeys "Xbindkeys"). Besides [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys) this requires [amixer](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture") and [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) and [xvkbd](https://www.archlinux.org/packages/?name=xvkbd).

*   See [[15]](https://gist.github.com/dhead666/08562a9a760b18b6e758) for an example configuration in `~/.xbindkeysrc`.
*   See [vilefridge's xbindkeys configuration](https://bbs.archlinux.org/viewtopic.php?id=173418&p=3) for another example.

##### Alternate xbindkeys configuration

[Volchange](http://pastie.org/9550960) (originated in the [Debian User Forums](http://www.debianuserforums.org/viewtopic.php?f=55&t=1453#p14351))) can manipulate the volume with PulseAudio instead of using [amixer](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture"). Besides [Volchange](http://pastie.org/9550960) this requires [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) and [xvkbd](https://www.archlinux.org/packages/?name=xvkbd).

*   Download the script from [[16]](http://pastie.org/9550960).
*   Make it executable

```
$ chmod u+x ~/.local/bin/volchange

```

See [[17]](https://gist.github.com/dhead666/4e23b506441ad424e26e) for a matching `~/.xbindkeysrc`.

#### Patch xkeyboard-config

Another option is to install [xkeyboard-config-chromebook](https://aur.archlinux.org/packages/xkeyboard-config-chromebook/)<sup><small>AUR</small></sup>, for more details visit [[18]](https://github.com/dhead666/archlinux-pkgbuilds/tree/master/xkeyboard-config-chromebook).

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

[Install](/index.php/Install "Install") [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool), open the Tweak Tool and under Power change the Power Button Action.

## Known issues

### Syslinux

Follow Syslinux installation instructions carefully. Try manual installation to see where the problem comes from. If you see [Missing Operation System](/index.php/Syslinux#Missing_operating_system "Syslinux") then it may be because you need to use correct bootloader binary. If syslinux does not work try other bootloader such as GRUB.

## See also

*   [Developer Information for Chrome OS Devices at the Chromium Projects site](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices)
*   [BBS topic about the Acer C720](https://bbs.archlinux.org/viewtopic.php?id=173418) which include generic information on Haswell Based Chromebooks.
*   Re-partitioning in Chrome OS [[19]](http://chromeos-cr48.blogspot.co.uk/2012/04/chrubuntu-1204-now-with-double-bits.html), [[20]](http://goo.gl/i817v)
*   [Brent Sullivan's the always updated list of Chrome OS devices](http://bit.ly/NewChromebooks)
*   [Google Chromebook Comparison Chart](http://prodct.info/chromebooks/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Chrome_OS_devices&oldid=415648](https://wiki.archlinux.org/index.php?title=Chrome_OS_devices&oldid=415648)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Laptops](/index.php/Category:Laptops "Category:Laptops")

Hidden category:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")