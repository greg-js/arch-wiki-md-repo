# Acer Aspire S7-392

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This page contains instructions, tips, pointers, and links for installing and configuring Arch Linux on the Acer Aspire S7-392 Laptop.

This page only applies to the 392 model (4th Gen Intel CPU), and may not be entirely correct for the 391 or 191 models (3rd Gen Intel CPU).

## Contents

*   [1 Compatibility](#Compatibility)
    *   [1.1 What works?](#What_works.3F)
    *   [1.2 What doesn't work, or is weird?](#What_doesn.27t_work.2C_or_is_weird.3F)
*   [2 BIOS Setup](#BIOS_Setup)
    *   [2.1 Disable Secure Boot](#Disable_Secure_Boot)
*   [3 Booting](#Booting)
    *   [3.1 Change Boot from UEFI to BIOS](#Change_Boot_from_UEFI_to_BIOS)
    *   [3.2 Boot from USB](#Boot_from_USB)
    *   [3.3 UEFI Boot Arch](#UEFI_Boot_Arch)
*   [4 Graphics Drivers](#Graphics_Drivers)
*   [5 Multitouch Gestures](#Multitouch_Gestures)
*   [6 Console fonts](#Console_fonts)
*   [7 Wifi instability](#Wifi_instability)

## Compatibility

The laptop works surprisingly well with Arch Linux, requiring minimal or no configuration hacking, depending on your desired setup.

### What works?

**Note:** Touchscreen only works in a Window Manager or Desktop Environment that has full support for it. It's recognized as a mouse click otherwise.

*   Touchscreen
*   Screen Brightness Adjustment
    *   Requres a window manager or desktop environment with the functionality, such as [Xfce](/index.php/Xfce "Xfce"), [GNOME](/index.php/GNOME "GNOME"), or [MATE](/index.php/MATE "MATE").
    *   Alternatively, a hotkey daemon such as [acpid](/index.php/Acpid "Acpid") may provide hotkey functionality (Not tested).
*   Keyboard Backlight (And adjustment)
*   Most Keyboard Hotkeys
    *   Wireless Toggle may not work. [acpid](/index.php/Acpid "Acpid") may work with it (Not tested)
*   Wireless Networking

### What doesn't work, or is weird?

*   Touchpad Multitouch Gestures
*   Touchscreen stops working after waking up from suspend

## BIOS Setup

The BIOS Setup utility is accessed by pressing Fn+2 at the Acer Logo screen during startup.

### Disable Secure Boot

In order to install Arch on the S7 you need to disable Secure Boot from the BIOS Setup. You need to do `Security > Set Supervisor Password` to set a supervisor password. Without it the option to disable Secure boot will be grayed out. Then go to `Boot > Secure Boot` and set it to `Disabled` and remove the supervisor password (by setting an empty one).

## Booting

The information in [Boot loaders](/index.php/Boot_loaders "Boot loaders") applies here. GRUB is confirmed to work.

### Change Boot from UEFI to BIOS

If desired, you can optionally select whether to use BIOS or UEFI when booting. This is an option in the BIOS Setup utility.

### Boot from USB

Booting from USB is possible by reordering boot devices in the BIOS setup, or by accessing the Boot Menu by pressing the "Fn" key and "=" key simultaneously (Translates to F12).

**Note:** The boot menu might be disabled - set `Main > F12 Boot Menu` to `Enabled` in BIOS Setup

### UEFI Boot Arch

One some dual-SSD machines the disk that BIOS boots from by default is identified as `/dev/sdb` rather than `/dev/sda`. If you're running a RAID it's recommended to leave a GPT partition on both disks. If you get an error after booting that BIOS cannot find a bootable media, but drops you in the boot menu where you can select HDD and it boots from there - you've installed grub on the wrong disk.

## Graphics Drivers

**Note:** With the default setup, there will be graphics tearing on the S7-392\. You can check the "Tear-free video" section of the [Intel graphics](/index.php/Intel_graphics "Intel graphics") page for information on fixing tearing

The standard [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver works with the laptop. For 32-bit games or other cases where necessary, you'll want to install [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) in addition to the xf86 driver.

## Multitouch Gestures

**Note:** Multitouch in Touchegg has broken since writing this. It doesn't work now

The touchpad works well with [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics), and with [touchegg](https://aur.archlinux.org/packages/touchegg/)<sup><small>AUR</small></sup> for advanced multitouch gestures.

**Note:** Contrary to what most of the internet says, you don't seem to need [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) to make Touchegg work.

## Console fonts

Since some of these come with HiDPI displays the default console font is barely readable - refer to [Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts") on how to change them.

## Wifi instability

This laptop uses Intel Corporation Wireless 7260 WiFi chipset. With the current firmware it might have issues connecting when signal is suboptimal. Disabling power save mode on the chip improves the connection times and connection speed. See [Wireless network configuration#Power saving](/index.php/Wireless_network_configuration#Power_saving "Wireless network configuration") on how to disable it and make it permanent.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Acer_Aspire_S7-392&oldid=376517](https://wiki.archlinux.org/index.php?title=Acer_Aspire_S7-392&oldid=376517)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Acer](/index.php/Category:Acer "Category:Acer")