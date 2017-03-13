The Dell Chromebook 11 (and newer chromebooks in general) features a "legacy boot" mode that makes it easy to boot Linux and other operating systems. The legacy boot mode is provided by the [SeaBIOS](http://www.coreboot.org/SeaBIOS) payload of coreboot. SeaBIOS behaves like a traditional BIOS that boots into the MBR of a disk, and from there into your standard bootloaders like Syslinux and GRUB.

The instructions for getting Arch Linux to work on this machine are similar to the [Acer C720 Chromebook](/index.php/Acer_C720_Chromebook "Acer C720 Chromebook"), with a few differences.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Enabling Developer Mode](#Enabling_Developer_Mode)
    *   [1.2 Patching SeaBIOS](#Patching_SeaBIOS)
    *   [1.3 Enabling SeaBIOS](#Enabling_SeaBIOS)
    *   [1.4 Installing Arch Linux](#Installing_Arch_Linux)
*   [2 Post Installation Configuration](#Post_Installation_Configuration)
    *   [2.1 Touchpad Configuration](#Touchpad_Configuration)
*   [3 Hardware](#Hardware)
    *   [3.1 Locating the Write-Protect Screw](#Locating_the_Write-Protect_Screw)
    *   [3.2 Removing the back of the laptop](#Removing_the_back_of_the_laptop)
*   [4 Known Issues](#Known_Issues)
    *   [4.1 Touchpad right-click not functioning in X11](#Touchpad_right-click_not_functioning_in_X11)
    *   [4.2 Unable to boot into Linux after exhausting battery](#Unable_to_boot_into_Linux_after_exhausting_battery)

## Installation

First enable legacy boot / SeaBIOS from the developer mode of Chrome OS. Then install and boot Linux as you would on a traditional x86 BIOS system.

### Enabling Developer Mode

See the [Chromebook page](/index.php/Chromebook#Enabling_developer_mode "Chromebook").

### Patching SeaBIOS

**Warning:** **This may screw up the RW part of your firmware! If this happens, you must use a ChromeOS recovery stick to reset it.**

The version of SeaBIOS that ships with the Dell Chromebook doesn't work properly, and therefore you must patch it in order to get it to work.

*   Open a crosh window with `Ctrl+Alt+T`.
*   Open a bash shell with the `shell` command.
*   Become superuser with `sudo bash`
*   Download the patched seabios.cbfs from [[1]](https://code.google.com/p/chromium/issues/detail?id=348403#c30), and save it to Downloads.
*   Patch SeaBIOS with the following commands:

```
# cd ~/Downloads
# flashrom -r image.rom
# dd if=seabios.cbfs of=image.rom seek=2 bs=2M conv=notrunc
# flashrom -w image.rom -i RW_LEGACY

```

### Enabling SeaBIOS

Continue by following [Enabling SeaBIOS](/index.php/Chromebook#Enabling_SeaBIOS "Chromebook") on the [Chromebook](/index.php/Chromebook "Chromebook") page.

### Installing Arch Linux

Continue by following the [Installation](/index.php/Chromebook#Installation "Chromebook") guide on the [Chromebook](/index.php/Chromebook "Chromebook") page.

## Post Installation Configuration

For information on general Chromebook post installation configuration (hotkeys, power key handling ...) see [Post installation configuration](/index.php/Chromebook#Post_installation_configuration "Chromebook") on the [Chromebook](/index.php/Chromebook "Chromebook") page.

### Touchpad Configuration

*   Edit Xorg touchpad configuration file

Add the Xorg touchpad configuration below for better usability (increases touchpad sensitivity).

 `/etc/X11/xorg.conf.d/50-cros-touchpad.conf` 
```
Section "InputClass" 
    Identifier      "touchpad wolf cyapa" 
    MatchIsTouchpad "on" 
    MatchDevicePath "/dev/input/event*" 
    MatchProduct    "cyapa" 
    Option          "FingerLow" "5" 
    Option          "FingerHigh" "10" 
EndSection
```

If you want to remove the "Right Click" behavior from the touchpad from the bottom right area (you can still right click with two finger clicks), you should comment out the following section from `/etc/X11/xorg.conf.d/50-synaptics.conf`

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
#Section "InputClass"
#        Identifier "Default clickpad buttons"
#        MatchDriver "synaptics"
#        Option "SoftButtonAreas" "50% 0 82% 0 0 0 0 0"
#       To disable the bottom edge area so the buttons only work as buttons,
#       not for movement, set the AreaBottomEdge
#       Option "AreaBottomEdge" "82%"
#EndSection

```

## Hardware

### Locating the Write-Protect Screw

Visit [the Dell Chromebook 11 page on The Chromium Projects](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices/dell-chromebook-11).

### Removing the back of the laptop

[This video](https://www.youtube.com/watch?v=rIdcS-efsio) describes the process of removing the back of the Dell Chromebook 11.

## Known Issues

### Touchpad right-click not functioning in X11

If the "Right Click" behavior of the touchpad is not working or it frequently fails to register left mouse clicks, try using the alternative X11 touchpad driver 'Mtrack' found [[2]](https://aur.archlinux.org/packages/xf86-input-mtrack/%7Chere).

### Unable to boot into Linux after exhausting battery

This is due to the 'dev_boot_legacy' flag being stored in volatile memory, and so being lost when the power runs out. This can be solved by enabling [booting to SeaBIOS by default](/index.php/Chromebook#Boot_to_SeaBIOS_by_default "Chromebook").