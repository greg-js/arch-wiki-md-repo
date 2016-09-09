| **Device** | **Status** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [ALSA](/index.php/ALSA "ALSA") | no beep |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| Fingerprint Sensor | No |
| [Mobile Broadband](/index.php/ThinkPad_mobile_internet "ThinkPad mobile internet") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| Smartcard Reader | Yes |

This article covers the installation and configuration of Arch Linux on a Lenovo T460s laptop.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 Hardware](#Hardware)
*   [2 Configuration](#Configuration)
    *   [2.1 Touchpad/TrackPoint](#Touchpad.2FTrackPoint)
    *   [2.2 Suspend / Resume](#Suspend_.2F_Resume)
    *   [2.3 Hibernate / Resume](#Hibernate_.2F_Resume)
    *   [2.4 Fingerprint Sensor](#Fingerprint_Sensor)
    *   [2.5 ALSA Beep](#ALSA_Beep)
    *   [2.6 Function keys](#Function_keys)
    *   [2.7 Video Issues](#Video_Issues)
    *   [2.8 Smartcard Reader](#Smartcard_Reader)
*   [3 See also](#See_also)

## Hardware

`lspci` returns something like:

```
00:00.0 Host bridge: Intel Corporation Skylake Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 520 (rev 07)
00:08.0 System peripheral: Intel Corporation Skylake Gaussian Mixture Model
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:16.3 Serial controller: Intel Corporation Device 9d3d (rev 21)
00:1c.0 PCI bridge: Intel Corporation Device 9d10 (rev f1)
00:1c.2 PCI bridge: Intel Corporation Device 9d12 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-LP LPC Controller (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection I219-LM (rev 21)
02:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS522A PCI Express Card Reader (rev 01)
04:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)
05:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller (rev 01)

```

`lsusb` returns something like:

```
Bus 002 Device 002: ID 17ef:1012 Lenovo 
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 008: ID 138a:0090 Validity Sensors, Inc. 
Bus 001 Device 007: ID 04f2:b52c Chicony Electronics Co., Ltd 
Bus 001 Device 005: ID 8087:0a2b Intel Corp. 
Bus 001 Device 003: ID 058f:9540 Alcor Micro Corp. AU9540 Smartcard Reader
Bus 001 Device 006: ID 192f:0416 Avago Technologies, Pte. ADNS-5700 Optical Mouse Controller (3-button)
Bus 001 Device 004: ID 17ef:1011 Lenovo 
Bus 001 Device 002: ID 17ef:1012 Lenovo 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Configuration

The [linux-t460s](https://aur.archlinux.org/packages/linux-t460s/) package includes kernel patches that fix the mouse and suspend issues described below, which can be useful until [linux](https://www.archlinux.org/packages/?name=linux) includes these patches. Alternatively, [linux-git](https://aur.archlinux.org/packages/linux-git/) can be used.

### Touchpad/TrackPoint

With kernels older than 4.5.1, there is a [kernel bug](https://bugzilla.kernel.org/show_bug.cgi?id=114321) which causes the physical mouse button (belonging to the TrackPoint) to report release events immediately even when pressing and holding the button. This prevents drag and drop and similar actions from working. This bug was fixed in linux-4.5.1.

### Suspend / Resume

With kernels older than 4.6, suspending the T460s by closing the lid when running on battery causes the machine to freeze up entirely. This can be worked around by setting the "intel_pstate=no_hwp" kernel parameter or by compiling the kernel with the patch attached to the [kernel bug](https://bugzilla.kernel.org/show_bug.cgi?id=113551) tracking this issue.

### Hibernate / Resume

A long standing kernel bug caused resume from hibernation to fail with a probability that depended on the amount of allocated RAM. This bug is fixed by [this patch](https://bugzilla.kernel.org/show_bug.cgi?id=104771), and is included in the [linux-t460s](https://aur.archlinux.org/packages/linux-t460s/) package.

### Fingerprint Sensor

The fingerprint sensor built into the T460s is currently not supported by [Fprint](/index.php/Fprint "Fprint").

### ALSA Beep

There is no "beep" input to the snd_hda_intel device, so beeps generated by terminal emulators etc. are not played. As a workaround, PulseAudio can be configured to pick up X11 bell events, see [PulseAudio#X11 Bell Events](/index.php/PulseAudio#X11_Bell_Events "PulseAudio").

### Function keys

Fn+Esc to enable FnLk which will make your function keys work.

### Video Issues

With newer kernels (>= 4.5), there seems to be video flickering, i.e. the screen occasionally goes black for what seems to be a single frame. See bug reports: [[1]](https://bugs.freedesktop.org/show_bug.cgi?id=95010) [[2]](https://bugs.freedesktop.org/show_bug.cgi?id=91393).

This can be worked around by using the `i915.enable_rc6=0` kernel parameter [[3]](https://bugs.freedesktop.org/show_bug.cgi?id=95010) (cf. [Intel graphics#Skylake support](/index.php/Intel_graphics#Skylake_support "Intel graphics"))

### Smartcard Reader

```
Bus 001 Device 003: ID 058f:9540 Alcor Micro Corp. AU9540 Smartcard Reader

```
[Install](/index.php/Install "Install") the [ccid](https://www.archlinux.org/packages/?name=ccid) and [pscs-tools](https://www.archlinux.org/packages/?name=pscs-tools) packages, and [enable](/index.php/Enable "Enable") the `pcscd` service. The reader should be visible when running `pcsc_scan`:
```
pcsc_scan
PC/SC device scanner
V 1.4.27 (c) 2001-2011, Ludovic Rousseau <ludovic.rousseau@free.fr>
Compiled with PC/SC lite version: 1.8.16
Using reader plug'n play mechanism
Scanning present readers...
0: Alcor Micro AU9560 00 00

Wed Sep  7 16:48:42 2016
Reader 0: Alcor Micro AU9560 00 00
  Card state: Card removed,

```

## See also

*   [Lenovo Support Page](http://support.lenovo.com/us/en/products/Laptops-and-netbooks/ThinkPad-T-Series-laptops/ThinkPad-T460s?beta=false)
*   [Dual boot install with bootctl](https://www.youtube.com/watch?v=fnYZAr-BaK0&list=PLiKgVPlhUNuxgKwoVH4MMUy5MLqjAE2ux&index=3)