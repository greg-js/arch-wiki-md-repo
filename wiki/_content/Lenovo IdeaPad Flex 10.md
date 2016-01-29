# Lenovo IdeaPad Flex 10

The Lenovo Flex 10 is a flexible dual-mode laptop computer with a 10.1" screen released in 2014\. It comes preinstalled with Windows 8/8.1\. The Flex 10 hardware is well supported in recent Linux kernels and enjoys good driver support for most of its components.

## Contents

*   [1 PCI Devices](#PCI_Devices)
*   [2 USB Devices](#USB_Devices)
*   [3 Hardware Support](#Hardware_Support)
    *   [3.1 UEFI](#UEFI)
    *   [3.2 Video](#Video)
    *   [3.3 Touchpad](#Touchpad)
    *   [3.4 Touchscreen](#Touchscreen)
*   [4 Issues](#Issues)
    *   [4.1 ALPM](#ALPM)
    *   [4.2 Touchscreen](#Touchscreen_2)

## PCI Devices

```
$ lspci
00:00.0 Host bridge: Intel Corporation Atom Processor Z36xxx/Z37xxx Series SoC Transaction Register (rev 0e)
00:02.0 VGA compatible controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Graphics & Display (rev 0e)
00:13.0 SATA controller: Intel Corporation Device 0f23 (rev 0e)
00:14.0 USB controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series USB xHCI (rev 0e)
00:1a.0 Encryption controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Trusted Execution Engine (rev 0e)
00:1b.0 Audio device: Intel Corporation Atom Processor Z36xxx/Z37xxx Series High Definition Audio Controller (rev 0e)
00:1c.0 PCI bridge: Intel Corporation Device 0f48 (rev 0e)
00:1f.0 ISA bridge: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Power Control Unit (rev 0e)
00:1f.3 SMBus: Intel Corporation Device 0f12 (rev 0e)
01:00.0 Network controller: Qualcomm Atheros QCA9565 / AR9565 Wireless Network Adapter (rev 01)

```

## USB Devices

```
$ lsusb
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 04f3:024b Elan Microelectronics Corp.
Bus 001 Device 006: ID 0cf3:3004 Atheros Communications, Inc. AR3012 Bluetooth 4.0
Bus 001 Device 003: ID 05e3:0610 Genesys Logic, Inc. 4-port hub
Bus 001 Device 002: ID 13d3:5614 IMC Networks
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Hardware Support

### UEFI

Before installing any other OS (other than the default Windows 8/8.1) it is required to disable the secure boot option in the boot setup menu.

### Video

Works natively with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). [SNA mode](https://wiki.archlinux.org/index.php/Intel_Graphics#SNA_issues), however, is unstable and can cause occasional screen freezes, using UXA mode is recommended instead.

### Touchpad

Works out of the box with [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics).

### Touchscreen

Does not work out of the box with [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev), the default behavior receives screen gestures as clicks, and registers scrolls as marking text. It is not yet clear whether xinput can emulate scrolling with evdev touch events at all [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1478128).

## Issues

### ALPM

When suspending to RAM with ALPM `link_power_management_policy` set to anything else than `max_performance` the device tends to lose connection to SATA storage devices at least while running kernel version 3.18.6\. This can be observed for example by entering a virtual console and executing `systemctl suspend` there. Even before the device enters to suspend state ATA related messages can be seen on the console and the device hangs on resume.

Check current policys with:

```
cat /sys/class/scsi_host/host0/link_power_management_policy /sys/class/scsi_host/host1/link_power_management_policy

```

Change policys to max_performance before suspending to RAM:

```
echo max_performance > /sys/class/scsi_host/host0/link_power_management_policy
echo max_performance > /sys/class/scsi_host/host1/link_power_management_policy

```

The easiest workaround is to use [TLP](https://wiki.archlinux.org/index.php/TLP) for power management governing with max_performance set for both SATA ALPM settings in `/etc/default/tlp`

```
# SATA aggressive link power management (ALPM):
#   min_power, medium_power, max_performance
SATA_LINKPWR_ON_AC=max_performance
SATA_LINKPWR_ON_BAT=max_performance

```

### Touchscreen

The Elan touchscreen in the Flex does not cope well with USB power management while running on Linux kernel version 3.18.6.

Enabling automatic power control for the usb device will immedietly result the touchscreen to stop responding to input. Your usb device ids may vary.

```
echo auto > '/sys/bus/usb/devices/1-4.4/power/control';

```

It seems to be possible to get the touchscreen back on it's feet by simply setting always power on option with

```
echo on > '/sys/bus/usb/devices/1-4.4/power/control';

```

Also after suspend or hibernate resume the touchscreen may appear as not responding. Weird enough just by reading some input from **/dev/input/mouse1** will get it back to working.

```
# dd if=/dev/input/mouse1 of=/dev/null bs=10 count=1

```

At the moment there is no known real touch input support in addition to the plain mouse emulation.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_IdeaPad_Flex_10&oldid=361082](https://wiki.archlinux.org/index.php?title=Lenovo_IdeaPad_Flex_10&oldid=361082)"