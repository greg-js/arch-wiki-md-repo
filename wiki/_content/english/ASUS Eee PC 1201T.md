| **Device** | **Status** | **Modules** |
| Graphics | **Working** | radeon |
| Ethernet | **Working** | atl1c |
| Wireless | **Working** | rtl8192se (kernel) |
| Audio | **Working** | snd_hda_intel |
| Camera | **Working** | uvcvideo |
| Card Reader | **Working** | usb-storage |
| Function Keys | **Working** | acpi-eeepc-generic |
| Suspend2RAM | **Working** | pm-utils |
| Hibernate | **Working** | pm-utils |
| Multi-input touchpad | **Working** |

## Contents

*   [1 Hardware](#Hardware)
*   [2 Graphics](#Graphics)
*   [3 Wireless](#Wireless)
*   [4 Function keys](#Function_keys)
*   [5 Camera](#Camera)
*   [6 Card reader](#Card_reader)
*   [7 Suspend](#Suspend)

## Hardware

```
 $ lspci
 00:00.0 Host bridge: Advanced Micro Devices [AMD] RS780 Host Bridge
 00:01.0 PCI bridge: ASUSTeK Computer Inc. RS880 PCI to PCI bridge (int gfx)
 00:04.0 PCI bridge: Advanced Micro Devices [AMD] RS780 PCI to PCI bridge (PCIE port 0)
 00:05.0 PCI bridge: Advanced Micro Devices [AMD] RS780 PCI to PCI bridge (PCIE port 1)
 00:11.0 SATA controller: ATI Technologies Inc SB700/SB800 SATA Controller [AHCI mode]
 00:12.0 USB Controller: ATI Technologies Inc SB700/SB800 USB OHCI0 Controller
 00:12.1 USB Controller: ATI Technologies Inc SB700 USB OHCI1 Controller
 00:12.2 USB Controller: ATI Technologies Inc SB700/SB800 USB EHCI Controller
 00:13.0 USB Controller: ATI Technologies Inc SB700/SB800 USB OHCI0 Controller
 00:13.2 USB Controller: ATI Technologies Inc SB700/SB800 USB EHCI Controller
 00:14.0 SMBus: ATI Technologies Inc SBx00 SMBus Controller (rev 3c)
 00:14.1 IDE interface: ATI Technologies Inc SB700/SB800 IDE Controller
 00:14.2 Audio device: ATI Technologies Inc SBx00 Azalia (Intel HDA)
 00:14.3 ISA bridge: ATI Technologies Inc SB700/SB800 LPC host controller
 00:14.4 PCI bridge: ATI Technologies Inc SBx00 PCI to PCI Bridge
 00:14.5 USB Controller: ATI Technologies Inc SB700/SB800 USB OHCI2 Controller
 00:18.0 Host bridge: Advanced Micro Devices [AMD] K8 [Athlon64/Opteron] HyperTransport Technology Configuration
 00:18.1 Host bridge: Advanced Micro Devices [AMD] K8 [Athlon64/Opteron] Address Map
 00:18.2 Host bridge: Advanced Micro Devices [AMD] K8 [Athlon64/Opteron] DRAM Controller
 00:18.3 Host bridge: Advanced Micro Devices [AMD] K8 [Athlon64/Opteron] Miscellaneous Control
 01:05.0 VGA compatible controller: ATI Technologies Inc RS780M/RS780MN [Radeon HD 3200 Graphics]
 02:00.0 Network controller: Realtek Semiconductor Co., Ltd. Device 8171 (rev 10)
 03:00.0 Ethernet controller: Atheros Communications Atheros AR8132 / L1c Gigabit Ethernet Adapter (rev c0)

```

## Graphics

See [Xorg](/index.php/Xorg "Xorg") and [ATI](/index.php/ATI "ATI").

## Wireless

Linux kernel has a very good native driver for the RTL8192SE.

## Function keys

First, make sure the ACPI is working properly. The kernel module "buttons" gives the kernel access to lid closure and power button events. To have access to the function key events, you need to load the kernel module eeepc_laptop. Try running acpi_listen and pressing Fn+F10, Fn+F11, etc. to see whether the function keys are detected. Then install acpi-eeepc-generic package from the AUR. Go to /etc/acpi/eeepc/models/ and copy acpi-eeepc-1000HE-events.conf into acpi-eeepc-1201T-events.conf. You might want to modify the events slightly. For example, instead of EEEPC_SCREEN_OFF=$KEY_Fn_F7 (which toggles bluetooth for some reason) use EEEPC_BLANK=$KEY_Fn_F7 and make sure package xorg-xset is installed. Also, the event code for Fn_F9 is 37, not 12, but it is supposed to toggle the touchpad anyway.

Finally, edit /etc/conf.d/acpi-eeepc-generic.conf, following the directions inside. Use "r8192se_pci" for WIFI_DRIVERS, pm-suspend for SUSPEND2RAM_COMMANDS, and 1201T for EEEPC_MODEL, not forgetting to put in "yes" for EEEPC_CONF_DONE.

Replace the line which says COMMANDS_SCREEN_OFF=("${COMMANDS_BLUETOOTH_TOGGLE[@]}") with COMMANDS_SCREEN_OFF=("@xset dpms force off")

This will allow to turn the screen off with Fn+F7.

This configuration will allow using the blue function buttons to change volume, change/turn off screen brightness, toggle wireless, and toggle SHE to reduce power consumption.

## Camera

The built-in webcam works with the uvcvideo module, as per instructions in [Webcam setup](/index.php/Webcam_setup "Webcam setup"), if only a bit laggy.

## Card reader

Just insert a SD card; the reader will behave like a pendrive (the card will be presented at /dev/sd*; check dmesg to see the correct device).

## Suspend

Suspend works as of kernel version 2.6.34\. The power management applet takes care of the power button, sleep Fn+F1 button, and the lid close events. The acpi-eeepc-generic functions conflict with these, for example causing the laptop to go to sleep twice upon sleep button press. If you want to keep acpi-eeepc-generic to handle volume buttons etc., but want to prevent these conflicts, edit /etc/conf.d/acpi-eeepc-generic.conf to comment out the COMMANDS_SLEEP and the COMMANDS_POWER_BUTTON lines, and put in "no" for COMMANDS_ON_LID_CLOSE.

With kernel 3.1.x, suspend causes kernel panic. A workaround, described [here](https://bbs.archlinux.org/viewtopic.php?pid=1029848#p1029848), is to make a new file */etc/pm/config.d/rtl8192se-workaround* with this content:

```
SUSPEND_MODULES="rtl8192se"

```