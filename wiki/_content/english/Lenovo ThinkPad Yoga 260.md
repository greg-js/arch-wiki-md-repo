## Contents

*   [1 Overview](#Overview)
*   [2 Installation](#Installation)
    *   [2.1 Booting the install USB](#Booting_the_install_USB)
*   [3 Configuration](#Configuration)
    *   [3.1 TrackPad](#TrackPad)
    *   [3.2 TrackPoint](#TrackPoint)
    *   [3.3 TouchScreen and Stylus](#TouchScreen_and_Stylus)
    *   [3.4 Video](#Video)
    *   [3.5 Card reader](#Card_reader)
    *   [3.6 Bluetooth](#Bluetooth)
*   [4 Hardware information](#Hardware_information)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 High CPU usage in idle](#High_CPU_usage_in_idle)
    *   [5.2 Blank screen after loading kernel](#Blank_screen_after_loading_kernel)
    *   [5.3 Screen rotation not working](#Screen_rotation_not_working)

## Overview

Most functionality works out of the box, although a kernel of version 4.3 or higher is necessary for the video card and the wifi adapter and a kernel of version 4.9 or higher for the accelerometer to be recognized. Suspending the machine also works.

| **Device** | **Status** | **Modules** |
| Graphics | **Working** | i915 |
| Wireless | **Working** | iwlwifi |
| Audio | **Working** | snd_hda_intel |
| Touchscreen | **Working** | wacom |
| Stylus | **Working** ¹ | wacom,usbhid |
| Accelerometer | **Working** | hid_sensor_accel_3d |
| Touchpad | **Working** | psmouse |
| Trackpoint | **Working** | psmouse |
| Camera | **Working** | uvcvideo |
| Card Reader | **Working** | mmc_core |
| Bluetooth | **Working** | btintel |
| Fingerprint Reader | **Working** ² |
| Smartcard reader | **Working** |

¹Pen-buttons can be assigned with xsetwacom, see [Wacom tablet#Remapping Buttons](/index.php/Wacom_tablet#Remapping_Buttons "Wacom tablet"). Device name is "Wacom Co.,Ltd. Pen and multitouch sensor Pen stylus".

²Using [https://github.com/3v1n0/libfprint](https://github.com/3v1n0/libfprint). Bug tracker for fingerprint sensor: [https://bugs.freedesktop.org/show_bug.cgi?id=94536](https://bugs.freedesktop.org/show_bug.cgi?id=94536)

## Installation

Newer kernels boot without problems and the wifi should be available. If you get a blank screen after booting, the power modes are not supported by your kernel; refer to Troubleshooting.

### Booting the install USB

To access the boot menu and BIOS, use "F1". Disable secure boot from the BIOS. UEFI boot mode works fine.

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

Touchscreen works with the Wacom driver (package: [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom)). Also using the Stylus, the bottom button of the pen is defined as the eraser and the top button works as a middle mouse button

**Note:** See [Tablet PC](/index.php/Tablet_PC "Tablet PC") for more info on optimizing the touchscreen experience.

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

The miniDP port works, at least when used with a VGA adapter. The connected display shows up in *xrandr* correctly. The HDMI output works with Xorg and xf86-video-intel 1:2.99.917+730.

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

## Troubleshooting

### High CPU usage in idle

If the Thinkpad has unusually high CPU usage in idle then it might be an acpi firmware issue. On Windows this behaviour stops after a regular update. On Linux you can workaround by disabling whatever device is interrupting excessively.

Find the interrupting source:

```
grep . -r /sys/firmware/acpi/interrupts

```

This might output something like this:

```
...
/sys/firmware/acpi/interrupts/gpe34:   30289   enabled  <-- this causes many interrupts
/sys/firmware/acpi/interrupts/gpe35:       3   enabled
...

```

Disable it (as root, not just sudo):

```
echo "disable" > /sys/firmware/acpi/interrupts/gpe34

```

Now the CPU should idle at 0-2% usage.

Unfortunately you have to do that on every startup. A systemd service can do that automatically for you.

Create `/etc/systemd/system/disable-interrupts.service`:

```
[Unit]
Description=Disable acpi interrupts
[Service]
ExecStart=/usr/bin/bash -c 'echo "disable" > /sys/firmware/acpi/interrupts/gpe34'
[Install]
WantedBy=multi-user.target

```

Then [enable](/index.php/Enable "Enable") the `disable-interrupts.service` systemd unit.

### Blank screen after loading kernel

This happens with older kernels because the Intel P-State driver had problems. The workaround is to disable the buggy part of the driver. To achieve this, add `intel_pstate=no_hwp` as a kernel parameter. If you use GRUB, edit your `/etc/default/grub` file and add the following:

```
GRUB_CMDLINE_LINUX="intel_pstate=no_hwp"

```

Don't forget to generate the config files with `grub-mkconfig`.

With a standard Arch-USB-ISO this can be done by pressing the Tabulator-Key on selecting the boot-menu-entry.

### Screen rotation not working

Enabling the option `"TearFree"` might break screen rotation: *xrandr -o left* will either result in a blank screen or in an error message (`xrandr: Configure crtc 0 failed`). The X.org Intel driver above version 1:2.99.917+641+ge4ef6e9 no longer has this bug. Either upgrade the driver or disable the tear-free playback.