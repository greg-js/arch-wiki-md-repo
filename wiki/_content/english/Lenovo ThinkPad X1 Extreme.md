| **Device** | **Status** | **Modules** |
| Intel UHD 630 Graphics | Working | i965 |
| Nvidia GTX 1050 Ti (Max-Q) | Working | nvidia |
| Intel I219-V Ethernet | Working | e1000e |
| Intel 9560 wireless | Working | iwlwifi |
| Realtek ALC285 audio | Working | snd_hda_intel |
| Synaptics touchpad | Working | synaptics + libinput |
| SunplusIT camera | Working | uvcvideo |
| Card reader | Working | xhci_hcd |
| Intel 9560 Bluetooth | Working | btusb |
| Intel JHL7540 Thunderbolt | Untested |
| Synaptics fingerprint reader | Not working |

The [ThinkPad X1 Extreme](https://www.lenovo.com/us/en/laptops/thinkpad/thinkpad-x/ThinkPad-X1-Extreme/p/20MF000DUS) is a thin-and-light 15.6" workstation/multimedia laptop from Lenovo's 2018 ThinkPad X lineup.

This page specifically concerns the specifics of running Arch Linux on this laptop. See [Laptop](/index.php/Laptop "Laptop") for generic laptop-related information, or [ThinkPad](/index.php/ThinkPad "ThinkPad") for other ThinkPad laptops.

**Note:** The ThinkPad P1 is a workstation version of the same laptop, using extremely similar hardware. The information on this page should be applicable to P1 models as well, but that has not been confirmed.

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 BIOS update](#BIOS_update)
    *   [1.2 Graphics](#Graphics)
    *   [1.3 Other notes](#Other_notes)
*   [2 Specifications](#Specifications)

## Configuration

### BIOS update

Despite not being required for an Arch Linux install, a BIOS update is strongly recommended for general use of the laptop - the initial 1.13 version devices seem to ship with contains multiple bugs that can result in bricking the laptop: [Reddit thread discussing the issue](https://www.reddit.com/r/thinkpad/comments/a2g0k4/warning_do_not_change_from_hybrid_graphics_to/); [another Reddit thread discussing a different bricking issue](https://www.reddit.com/r/thinkpad/comments/9qreoj/psa_do_not_enable_bios_support_for_thunderbolt/).

BIOS updates are normally available via [fwupd](/index.php/Fwupd "Fwupd"), however, the latest BIOS update version 1.17 is only available from [Lenovo's website](https://pcsupport.lenovo.com/en/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-extreme/downloads) as of late December 2018\. You can use the bootable version if you don't have access to a Windows install.

### Graphics

Text mode works out of the box. Starting X11 requires configuring the right card ID in [Xorg.conf](/index.php/Xorg.conf "Xorg.conf"), e.g.:

```
Section "Device"
       Identifier  "Card1"
       Driver      "modesetting"
       BusID       "PCI:0:2:0"
EndSection

```

Hybrid graphics works via [Bumblebee](/index.php/Bumblebee "Bumblebee"). Nvidia-only mode has not been tested as of this writing.

The HDMI port is wired to the Nvidia chip, see [Bumblebee#Output_wired_to_the_NVIDIA_chip](/index.php/Bumblebee#Output_wired_to_the_NVIDIA_chip "Bumblebee") for details.

### Other notes

The webcam works out of the box, though it appears connected at all times, no matter the slider state (the camera appears "disconnected" in Windows when the protective slider is closed) - however, when the slider is closed, a completely black image is reported by the camera.

The fingerprint scanner is currently not supported in libfprint - a reverse engineering effort was ongoing [here](https://github.com/nmikhailov/Validity90), but seems to have stalled. Upstream libfprint bug is tracked [here](https://gitlab.freedesktop.org/libfprint/libfprint/issues/134).

The Thunderbolt port has been reported to work on other distributions, but has not been tested on Arch as of December 2018.

Everything else works correctly out of the box.

## Specifications

All information on this page has been tested on laptop part number 20MF000BUS, with the following specifications:

*   Intel Core i7-8750H CPU
*   Hybrid Intel UHD 630/Nvidia GTX 1050 Ti Max-Q graphics
*   Innolux N156HCE-EN1 1920x1080/60Hz IPS screen (other vendors may be used)
*   16GB RAM
*   Intel 7600p series 512GB NVMe SSD drive (other vendors may be used)