## Contents

*   [1 General Information](#General_Information)
*   [2 Installing the Base System](#Installing_the_Base_System)
*   [3 Configuring Xorg for Intel Graphics and Synaptics Touchpad](#Configuring_Xorg_for_Intel_Graphics_and_Synaptics_Touchpad)
*   [4 Keyboard and Hotkeys](#Keyboard_and_Hotkeys)
*   [5 Boot Booster](#Boot_Booster)
*   [6 Control the VGA Output](#Control_the_VGA_Output)

## General Information

The ASUS Eee PC 1001HA is a netbook personal computer.

Hardware:

*   CPU: Intel Atom N270 @ 1.60 GHz
*   RAM: 1 GB DDR2 533 MHz SODIMM, one slot, can be upgraded to maximum 2 GB
*   Graphics: Intel GMA950, integrated in the northbridge
*   Sound: Intel HD Audio, two integrated speakers, microphone, headphones out, microphone in
*   Chipset: Intel 945GSE northbridge, ICH7 southbridge
*   Hard disk: 160 GB, Seagate ST9160301AS, 5400 rpm
*   Display: 10.1", LED backlight, resolution: 1024x600
*   Wired network: Atheros AR8132 10/100 Fast Ethernet
*   Wireless: Ralink RT3090 802.11n, mini PCIe card

Since the processor doesn't support 64-bit software, you can install the 32-bit version of Arch Linux.

When you turn on the computer, to enter the BIOS settings menu, press the F2 key repeatedly until the BIOS menu appears. To show the boot menu so you may start the system from an external CD/DVD drive or an USB flash drive, press the Escape key repeatedly until this menu appears.

## Installing the Base System

Please refer to the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") for a detailed step-by-step guide for installing Arch to your Eee PC. If you are more technically inclined, refer to the short [Installation guide](/index.php/Installation_guide "Installation guide").

## Configuring Xorg for Intel Graphics and Synaptics Touchpad

The 1001HA has an Intel GMA950 integrated graphics located in the northbridge and cooled by the netbook's fan. You use the Synaptics touchpad to move the pointer on the screen.

If you plan to use a desktop environment or a window manager, you need to install and configure [Xorg](/index.php/Xorg "Xorg") and the [Intel](/index.php/Intel "Intel") and [Synaptics](/index.php/Synaptics "Synaptics") drivers.

## Keyboard and Hotkeys

See [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") for basic configuration.

Hotkeys allow the user to change volume, brightness, put the netbook to sleep etc. They are activated by holding the Fn key and then pressing one of the function keys (F1-F12) and Space.

By default, these keys work:

*   Fn F1: Suspend-to-RAM (puts the netbook to sleep, low power mode)
*   Fn F2: turns on/off the wireless card
*   Fn F5: lowers the backlight intensity
*   Fn F6: rises the backlight intensity

To configure the other keys, refer to the desktop environment's control panel, or in case you use a window manager such as Openbox, edit its configuration file. Please refer to [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys").

## Boot Booster

The Boot Booster allows your laptop to start instantly by skipping the POST startup test and caching BIOS settings on the hard disk. If you consider using this feature, create a primary partition at the end of the hard disk that is 50 MB in size. It must be a primary partition and it must be the last on the disk. Use a tool such as [GParted](/index.php/GParted "GParted") or fdisk to do this and set the partition type to 0xef (EFI FAT Partition) - use fdisk for this (expert mode - be careful!).

First deactivate this option in the BIOS Boot settings, then turn off your computer properly. Turn on the computer, enable the Boot Booster in BIOS, turn off your computer properly and the Boot Booster will work afterwards, when you turn on the computer next time.

## Control the VGA Output

You can use graphical tools such as lxrandr, arandr or a command line tools, such as [xrandr](/index.php/Xrandr "Xrandr").