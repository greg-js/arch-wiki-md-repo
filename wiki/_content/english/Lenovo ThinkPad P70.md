This is a guide of steps aggregated from other sources to installation of Arch on the Lenovo ThinkPad P70\. This guide was written for ARCH_201604 ISO. The laptop features a 17.3" IPS display and has connectors for up to four SSDs (two M.2 [NVMe](/index.php/NVMe "NVMe"), two SATA).

| **Device** | **Status** | **Modules** |
| Intel | Working | xf86-video-intel |
| NVIDIA (Quadro M3000M, M4000M) | Working* | nvidia |
| HDMI | Working |
| Ethernet | Working |
| Wireless | Working | iwlwifi |
| Audio | Working |
| Trackpad | Working | xf86-input-libinput |
| Trackpoint | Working | xf86-input-libinput |
| Camera | Working |
| Card Reader | untested |
| Bluetooth | untested |

## Contents

*   [1 Hardware](#Hardware)
*   [2 Preliminaries](#Preliminaries)
*   [3 Installation](#Installation)
*   [4 Configuration](#Configuration)
    *   [4.1 Keyboard](#Keyboard)
    *   [4.2 Sound](#Sound)
    *   [4.3 Integrated Graphics](#Integrated_Graphics)
    *   [4.4 Dedicated Graphics](#Dedicated_Graphics)
    *   [4.5 External Displays](#External_Displays)
    *   [4.6 HiDPI](#HiDPI)

## Hardware

`lspci` returns something like:

```
00:00.0 Host bridge: Intel Corporation Skylake Host Bridge/DRAM Registers (rev 07)
00:01.0 PCI bridge: Intel Corporation Skylake PCIe Controller (x16) (rev 07)
00:02.0 VGA compatible controller: Intel Corporation Device 191d (rev 06)
00:14.0 USB controller: Intel Corporation Sunrise Point-H USB 3.0 xHCI Controller (rev 31)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-H Thermal subsystem (rev 31)
00:16.0 Communication controller: Intel Corporation Sunrise Point-H CSME HECI #1 (rev 31)
00:16.3 Serial controller: Intel Corporation Sunrise Point-H KT Redirection (rev 31)
00:17.0 SATA controller: Intel Corporation Sunrise Point-H SATA controller [AHCI mode] (rev 31)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #1 (rev f1)
00:1c.2 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #3 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #5 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #9 (rev f1)
00:1d.4 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #13 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-H LPC Controller (rev 31)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-H PMC (rev 31)
00:1f.3 Audio device: Intel Corporation Sunrise Point-H HD Audio (rev 31)
00:1f.4 SMBus: Intel Corporation Sunrise Point-H SMBus (rev 31)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (2) I219-LM (rev 31)
01:00.0 VGA compatible controller: NVIDIA Corporation GM204GLM [Quadro M3000M] (rev a1)
04:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)
70:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller (rev 01)
71:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)

```

`lsusb` returns something like:

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 138a:0090 Validity Sensors, Inc. 
Bus 001 Device 002: ID 04f2:b52c Chicony Electronics Co., Ltd 
Bus 001 Device 005: ID 0765:5010 X-Rite, Inc. 
Bus 001 Device 004: ID 058f:9540 Alcor Micro Corp. AU9540 Smartcard Reader
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Preliminaries

1.  Create a recovery device in Windows 10\. It required a USB-only (no SD card, no optical media?) flash drive greater than 8 GB. Formatting FAT32 works.
2.  [Update the BIOS.](https://support.lenovo.com/us/en/documents/yast-3jwkjx) At this time of writing, the latest BIOS is 2.15 (2017-05-30). Lenovo provides a bootable, standalone ["BIOS Update CD"](http://support.lenovo.com/us/en/downloads/ds106086) to perform this update outside of Windows.
3.  Getting **into** the BIOS is difficult, so [here are some instructions](https://support.lenovo.com/us/en/documents/sf13-t0025) that seemed to work. The easiest way was through Windows 10.
4.  In the BIOS, you will want to disable UEFI Secure Boot, change the boot order to look at USB devices first, allow `F12` to bypass the BIOS, and possibly enable the verbose mode because it is easier to press the appropriate buttons on time.

## Installation

This machine can boot either via EFI or grub.

This section assumes that you've successfully created bootable Arch install media to a USB drive. The label of the USB installer must be correct (ARCH_201604 in this case). Restart the computer boot from the USB drive. You may need to press `F12` at some point to trigger a boot order override.

You need an internet connection; this guide got both ethernet and wifi to work. Find the interfaces with `ip link`.

Ethernet: turn on DHCP with

```
# dhcpcd *<interface>* 

```

Wifi: wifi-menu worked here, the appropriate SSID was selected with the right password.

The font sizes will make you feel very far away. To deal with this, fonts are in `/usr/share/kbd/consolefonts`.

You can see the currently selected font with showconsolefont. The font was changed here to `sun12x22` with: `setfont sun12x22`. It is a little better.

Following the [Beginner's guide](/index.php/Beginner%27s_guide "Beginner's guide") to install Arch.

Shutdown, remove the USB drive, and then boot the computer, and make sure the installed drive is first in the BIOS.

## Configuration

### Keyboard

To control the keyboard backlight, you change the value using:

```
echo 1 | sudo dd of=/sys/class/leds/tpacpi\:\:kbd_backlight/brightness

```

for values 0–2.

### Sound

The status of audio output over HDMI, Thunderbolt, and/or Mini Displayport is unknown.

### Integrated Graphics

The integrated Intel GPU should work (mostly) without configuration using the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package. If you experience crashes or hangs, please see [Intel graphics#Skylake support](/index.php/Intel_graphics#Skylake_support "Intel graphics") for additional configuration.

### Dedicated Graphics

There is a BIOS option for turning off the Intel Integrated Graphics and only running the NVIDIA discrete card. While it is possible to get the console working with this configuration, there are no confirmed reports of X.org working in this setup.

[NVIDIA Optimus#Using nvidia](/index.php/NVIDIA_Optimus#Using_nvidia "NVIDIA Optimus") contains instructions on configuring Xorg to use your Nvidia Quadro GPU. Be sure to select the "Hybrid Graphics" in your BIOS. The official [nvidia](https://www.archlinux.org/packages/?name=nvidia) driver package supports hybrid GPU configuration without requiring the use of Noveau/PRIME or Bumblebee. The following example configuration enables the GPU using the proprietary driver. Pay close attention to the ConstrainCursor and AccelMethod directives.

 `/etc/X11/xorg.conf` 
```
# Server layout
Section "ServerLayout"
	Identifier "layout"
	Screen 0 "nvidia"
	Inactive "intel"
EndSection

# Intel
Section "Device"
	Identifier "Intel"
	Driver "modesetting"
	BusID "PCI:0@0:2:0"
	#Option "AccelMethod" "sna"
	Option "AccelMethod" "none"
EndSection

Section "Screen"
	Identifier "intel"
	Device "intel"
EndSection

# Nvidia
Section "Device"
	Identifier "nvidia"
	Driver "nvidia"
	BusID "PCI:1@0:0:0"
	Option "ConstrainCursor" "off"
EndSection

Section "Screen"
	Identifier "nvidia"
	Device "nvidia"
	Option "AllowEmptyInitialConfiguration" "on"
	Option "IgnoreDisplayDevices" "CRT"
EndSection
```

### External Displays

DisplayPort over USB-C, HDMI, and Mini DisplayPort outputs all work using the above configuration with the proprietary Nvidia driver. HDMI has also been confirmed to work using Bumblebee and `intel-virtual-output`.

Limited testing suggests that a maximum of 3 total displays from 2 output types may be used at one time. For example, two external DP/USB-C displays and the one internal display will achieve the maximum of three.

**Warning:** Hot-swapping between different external display types has been known to hardlock the Nvidia driver. Change outputs at your own risk!

### HiDPI