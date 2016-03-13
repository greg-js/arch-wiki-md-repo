## Contents

*   [1 Overview](#Overview)
*   [2 Installation](#Installation)
    *   [2.1 Booting the install USB](#Booting_the_install_USB)
    *   [2.2 Network connection](#Network_connection)
*   [3 Boot manager](#Boot_manager)
*   [4 Configuration](#Configuration)
    *   [4.1 TrackPad](#TrackPad)
    *   [4.2 TrackPoint](#TrackPoint)
    *   [4.3 TouchScreen and Stylus](#TouchScreen_and_Stylus)
    *   [4.4 Video](#Video)
    *   [4.5 Card reader](#Card_reader)
    *   [4.6 Bluetooth](#Bluetooth)
*   [5 Hardware information](#Hardware_information)

## Overview

Most functionality works out of the box, although a kernel of version 4.3 or higher is necessary for the video card and the wifi adapter. Suspending the machine also works. The accelerometer does not show up.

| **Device** | **Status** | **Modules** |
| Graphics | **Working** | i915 |
| Wireless | **Working** | iwlwifi |
| Audio | **Working** | snd_hda_intel |
| Touchscreen | **Working** | wacom |
| Stylus | **Partial** ¹ | wacom,usbhid |
| Accelerometer | **Not Working** |
| Touchpad | **Working** | psmouse |
| Trackpoint | **Working** | psmouse |
| Camera | **Working** | uvcvideo |
| Card Reader | **Working** | mmc_core |
| Bluetooth | **Working** | btintel |
| Fingerprint Reader | **Unknown** |

¹Only one pen-button working

## Installation

In order to boot with a current kernel, you need to pass `intel_pstate=no_hwp` as kernel parameter. With a standard Arch-USB-ISO this can be done by pressing the Tabulator-Key on selecting the boot-menu-entry.

If you cannot manage to utilize the kernel parameter, installation gets difficult because you need to choose an old kernel (e.g., installation media from 2015.08 or before) and you do not have network access without additional RJ45 adapter, as the laptop does not have an RJ45 port.

### Booting the install USB

To access the boot menu and BIOS, use "F1". Disable secure boot from the BIOS. UEFI boot mode works fine.

### Network connection

If you have a OneLink+ dock or a USB Ethernet adapter, you can have wired connection. Otherwise, you need a workaround. Since you cannot edit the boot options on the USB stick, to pass `intel_pstate=no_hwp` to the kernel, you can either [remaster the install ISO](/index.php/Remastering_the_Install_ISO "Remastering the Install ISO") or install a bootstrap Linux, upgrade its kernel, edit its boot parameters, and continue [installing Arch from an existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux"). The latter was tested with Linux Mint 17.3 acting as the bootstrap system.

## Boot manager

The default ESP partition has ample space (260 MByte). Irrespective of which boot manager you choose, remember to add `intel_pstate=no_hwp` as a kernel parameter. If you use GRUB, edit your `/etc/default/grub` file and add the following:

```
GRUB_CMDLINE_LINUX="intel_pstate=no_hwp"

```

Don't forget to generate the config files with `grub-mkconfig`.

## Configuration

### TrackPad

TrackPad works fine with [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics).

### TrackPoint

See [TrackPoint](/index.php/TrackPoint "TrackPoint"). Sometimes the TrackPoint stops working and dmesg reports a stream of garbage when it is touched. Removing and probing the kernel module solves the problem:

```
# rmmod psmouse
# modprobe psmouse

```

### TouchScreen and Stylus

Touchscreen works with the Wacom driver (package: [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom)). Also using the Stylus, only one of the two buttons on the pen is usable.

### Video

The kernel supports HD Graphics 520 from version 4.3\. With default configuration, tearing is apparent when playing videos. DRI3 and glamor are supported. To solve tearing and use DRI3 and glamor, create the file `/etc/X11/xorg.conf.d/20-intel.conf` with the following content:

```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "AccelMethod"  "glamor"
   Option      "DRI"    "3"
   Option      "TearFree"    "true"
EndSection

```

Enabling the option `"TearFree"`, however, breaks screen rotation: *xrandr -o left* will either result in a blank screen or in an error message (`xrandr: Configure crtc 0 failed`).

The miniDP port works, at least when used with a VGA adapter. The connected display shows up in *xrandr* correctly..

### Card reader

The microSD-card reader works out of the box.

### Bluetooth

The Bluetooth adapter works out of the box. It was tested with Android tethering and file transfer.

## Hardware information

The output of *lspci* is

```
00:00.0 Host bridge: Intel Corporation Sky Lake Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation Sky Lake Integrated Graphics (rev 07)
00:08.0 System peripheral: Intel Corporation Sky Lake Gaussian Mixture Model
00:13.0 Non-VGA unclassified device: Intel Corporation Device 9d35 (rev 21)
00:14.0 USB controller: Intel Corporation Device 9d2f (rev 21)
00:14.2 Signal processing controller: Intel Corporation Device 9d31 (rev 21)
00:16.0 Communication controller: Intel Corporation Device 9d3a (rev 21)
00:17.0 SATA controller: Intel Corporation Device 9d03 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Device 9d10 (rev f1)
00:1c.2 PCI bridge: Intel Corporation Device 9d12 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Device 9d48 (rev 21)
00:1f.2 Memory controller: Intel Corporation Device 9d21 (rev 21)
00:1f.3 Audio device: Intel Corporation Device 9d70 (rev 21)
00:1f.4 SMBus: Intel Corporation Device 9d23 (rev 21)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection I219-V (rev 21)
02:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. Device 522a (rev 01)
04:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)

```

The output of *lsusb* is

```
Bus 001 Device 004: ID 138a:0090 Validity Sensors, Inc. 
Bus 001 Device 003: ID 13d3:5248 IMC Networks 
Bus 001 Device 002: ID 8087:0a2b Intel Corp. 
Bus 001 Device 005: ID 056a:5048 Wacom Co., Ltd 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```