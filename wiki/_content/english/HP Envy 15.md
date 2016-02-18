| **Device** | **Status** | **Modules** |
| Intel | **Working** | xf86-video-intel |
| nVdia | **Working** | nvidia |
| Ethernet | **Working** | r8169 |
| Wireless | **Working** | iwlwifi *or* rt2800pci |
| Audio | **Working** | snd_hda_intel |
| Touchpad | **Working** | synaptics |
| Camera | **Working** | uvcvideo |
| Card Reader | **Working** |
| Bluetooth | **Working** | rtbth |
| Fingerprint Reader | **Working** |

## Contents

*   [1 Hardware](#Hardware)
*   [2 Configuration](#Configuration)
    *   [2.1 Video -- *j013sg and j082sf*](#Video_--_j013sg_and_j082sf)
    *   [2.2 Audio -- *j013sg and j082sf*](#Audio_--_j013sg_and_j082sf)
    *   [2.3 WIFI Button -- *j082sf*](#WIFI_Button_--_j082sf)
    *   [2.4 Fingerprint Reader -- *j082sf*](#Fingerprint_Reader_--_j082sf)
    *   [2.5 Wifi -- *j013sg and j082sf*](#Wifi_--_j013sg_and_j082sf)
    *   [2.6 Bluetooth -- *j082sf*](#Bluetooth_--_j082sf)

# Hardware

| **CPU** | Intel Core i7-4702MQ (2.2GHz Quad-core + HT) |
| **RAM** | 16 GB (2x8GB) |
| **Display** | 15.6" LCD |
| **Integrated Graphics** | Intel HD 4600 |
| **Discrete Graphics** | NVIDIA GeForce GT 750M (2G) |
| **Sound** | Intel HD Audio |
| **Ethernet** | Realtek RTL8168/8111g Gigabit Ethernet |
| **Wireless** | **j013sg :** Intel Centrino Wireless-N 2230 |
 **j082sf :** Ralink RT3290 (bluetooth + wifi) |
| **Bluetooth** | **j013sg :** None |
 **j082sf :** Ralink RT3290 (bluetooth + wifi) |
| **Hard Disk** | 1 TB 5400rpm SATA |
| **Touchpad** | Synaptics ClickPad |

[[Schematic diagram](https://framapic.org/HHmPmSh9DV1r/S04qJm6r)]

# Configuration

This is based on the HP Envy 15 j013sg (E8N68EA) and HP Envy j082sf

## Video -- *j013sg and j082sf*

xf86-video-modesetting and bumblebee setups work. nouveau untested Works by folllowing [https://wiki.archlinux.org/index.php/Optimus](https://wiki.archlinux.org/index.php/Optimus)

## Audio -- *j013sg and j082sf*

`hdajackretask` in the package `extra/alsa-tools` can be used to remap the unconnected 0x0f pin to Internal Speaker, and the 0x10 pin to the subwoofer (Internal Speaker LFE).

## WIFI Button -- *j082sf*

The `hp-wireless` module landed in kernel version 3.14\. This button will not work with [rt3290sta-dkms](https://aur.archlinux.org/packages/rt3290sta-dkms/) AUR package.

## Fingerprint Reader -- *j082sf*

Works fine with this package : [https://github.com/payden/libfprint](https://github.com/payden/libfprint)

## Wifi -- *j013sg and j082sf*

Works out of the box for both of them. If you have issues with j082sf, you can use [rt3290sta-dkms](https://aur.archlinux.org/packages/rt3290sta-dkms/) AUR package

## Bluetooth -- *j082sf*

Works fine with [rtbth-dkms](https://aur.archlinux.org/packages/rtbth-dkms/) AUR package.