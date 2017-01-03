| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | iwlwifi |
| Bluetooth | Working | bluetooth |
| Audio | Partially working | snd_hda_intel |
| Touchpad | Working with tweaks |  ? |
| Webcam | Working | uvcvideo |

This article covers hardware specific configuration of this laptop, some minor issues remain after customization. These can be performed after an installation of Arch Linux has been finished and the machine rebooted into it.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 Hardware info](#Hardware_info)
    *   [1.1 Hardware options](#Hardware_options)
    *   [1.2 lspci on a 4231](#lspci_on_a_4231)
*   [2 Installation](#Installation)
*   [3 Issues](#Issues)
    *   [3.1 Audio](#Audio)
    *   [3.2 Touchpad](#Touchpad)

## Hardware info

### Hardware options

This is the model of HP Spectre x360 released in late 2016\. Distinctive features include two thunderbolt ports and no digitizer. The main hardware components are

*   Intel i7 Kabylake 7500U
*   OLED touch screen running at 1920x1080
*   500 GB M.2 SDD
*   16 GB RAM
*   4 speakers

### lspci on a 4231

```
00:00.0 Host bridge: Intel Corporation Device 5904 (rev 02)
00:02.0 VGA compatible controller: Intel Corporation Device 5916 (rev 02)
00:04.0 Signal processing controller: Intel Corporation Device 1903 (rev 02)
00:13.0 Non-VGA unclassified device: Intel Corporation Device 9d35 (rev 21)
00:14.0 USB controller: Intel Corporation Device 9d2f (rev 21)
00:14.2 Signal processing controller: Intel Corporation Device 9d31 (rev 21)
00:15.0 Signal processing controller: Intel Corporation Device 9d60 (rev 21)
00:16.0 Communication controller: Intel Corporation Device 9d3a (rev 21)
00:1c.0 PCI bridge: Intel Corporation Device 9d11 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Device 9d14 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Device 9d18 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Device 9d58 (rev 21)
00:1f.2 Memory controller: Intel Corporation Device 9d21 (rev 21)
00:1f.3 Audio device: Intel Corporation Device 9d71 (rev 21)
00:1f.4 SMBus: Intel Corporation Device 9d23 (rev 21)
01:00.0 Network controller: Intel Corporation Device 24fd (rev 78)
6d:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd Device a802 (rev 01)

```

## Installation

Installing arch is straight forward for everything (disable secure boot, F10 for BIOS, F9 for boot options) but one thing: you may have to disable a BIOS option called "fast boot". While this option is activated in BIOS the machine may boot into Windows no matter what you select. If you make to boot into the latest arch ISO (June 2016) on a USB, arch EFI boot menu hangs. After you installed arch on HDD and moved all of M$ Windows to /dev/null, you may activate that option again. Although no difference in boot performance could be observed with the option activated or deactivated.

## Issues

### Audio

Codec has changed from the previous version, now it's Realtek ALC295:

```
# aplay -l
**** List of PLAYBACK Hardware Devices ****
card 0: PCH [HDA Intel PCH], device 0: ALC295 Analog [ALC295 Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0

```

In best case scenario just one speaker is going to work. There's a bug for that: [https://bugzilla.kernel.org/show_bug.cgi?id=189331](https://bugzilla.kernel.org/show_bug.cgi?id=189331)

### Touchpad

When using synaptics X11 drivers touchpad works but fails to detect palm, which causes problems when typing. Dell XPS13 had similar issue and they fixed it, but HP is not going to do that. Refer to [https://github.com/advancingu/XPS13Linux/issues/3](https://github.com/advancingu/XPS13Linux/issues/3)

When using libinput drivers palm detection works out of the box.