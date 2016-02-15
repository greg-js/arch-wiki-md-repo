| **Device** | **Status** | **Modules** |
| Intel | **Working** | xf86-video-intel |
| AMD | **Working** | ati-dri |
| Ethernet | **Working** | atl1c |
| Wireless | **Working** | iwlwifi |
| Audio | **Working** | snd_hda_intel |
| Touchpad | **Working** | synaptics |
| Camera | **Working** |
| Card Reader | **Working** | rts5229 |

## Contents

*   [1 Hardware](#Hardware)
*   [2 Configuration](#Configuration)
    *   [2.1 Video](#Video)
    *   [2.2 Audio](#Audio)
    *   [2.3 SD Card Reader](#SD_Card_Reader)

# Hardware

| **CPU** | Intel Core i7-2670QM (2.2GHz Quad-core) |
| **RAM** | 8 GB (2x4GB) |
| **Display** | 17.3" LCD |
| **Integrated Graphics** | Intel HD 3000 |
| **Discrete Graphics** | AMD Radeon HD 7690 (1 GB) |
| **Sound** | Intel HD Audio |
| **Ethernet** | Atheros AR8151 v2.0 Gigabit Ethernet |
| **Wireless** | Intel Centrino Advanced-N 6235 |
| **Hard Disk** | 750 GB 7200rpm SATA |
| **Touchpad** | Synaptics ClickPad |

# Configuration

This is based on the 2012 HP Envy 17.

## Video

Works by following [http://www.reddit.com/r/linux/comments/1nu4pc/muxless_graphics_cards_on_linux/](http://www.reddit.com/r/linux/comments/1nu4pc/muxless_graphics_cards_on_linux/). I strongly recommend switching to linux-mainline ([AUR](https://aur.archlinux.org/packages/linux-mainline/)) to take advantage of power-management built into 3.12.

## Audio

`hdajackretask` in the package `extra/alsa-tools` can be used to remap the unconnected 0x10 pin to the subwoofer (Internal Speaker LFE).

## SD Card Reader

**As of 3.8 a third party module is not needed, device is accessible @ /dev/mmcX**

The module **for pre 3.8** `rts5229` is in the [AUR](https://aur.archlinux.org/packages/rts5229/).