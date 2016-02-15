| **Device** | **Status** | **Module** |
| Intel | Working | xf86-video-intel |
| Nvidia | Working | nvidia |
| Ethernet | Working | r8169 |
| Wireless | Working | iwlwifi |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | xf86-input-synaptics |
| Camera | Working | uvcvideo |
| Card Reader | Working | rtsx_usb |
| Bluetooth | Working | bluetooth |

## Contents

*   [1 Hardware](#Hardware)
*   [2 Configuration](#Configuration)
    *   [2.1 Video](#Video)
    *   [2.2 Audio](#Audio)
    *   [2.3 Keyboard](#Keyboard)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 nouveau problems](#nouveau_problems)

# Hardware

This article covers hardware specific configuration for [ASUS N550JX](https://www.asus.com/Notebooks/N550JX/specifications/) laptop.

# Configuration

## Video

Laptop comes with two GPU's (main [INTEL](/index.php/Intel_graphics "Intel graphics") and dedicated [NVIDIA](/index.php/NVIDIA "NVIDIA")):

```
$ lspci | grep "VGA|3D"

```

```
00:02.0 VGA compatible controller: Intel Corporation 4th Gen Core Processor Integrated Graphics Controller (rev 06)
01:00.0 3D controller: NVIDIA Corporation GM107M [GeForce GTX 950M] (rev ff)
```

NVIDIA Optimus technology can be implemented and controlled using [Bumblebee](/index.php/Bumblebee "Bumblebee") software.

## Audio

Built-in speakers and headphones work out of the box with **snd_hda_intel** driver. External sub-woofer works after this patch is applied:

 `/etc/modprobe.d/snd-hda-intel-n550jx.conf`  `options snd-hda-intel patch=n550jx-lfe-fix,n550jx-lfe-fix`  `/lib/firmware/n550jx-lfe-fix` 

```
[codec]
0x10ec0668 0x104313df 0

[pincfg]
0x1a 0x00106111
```

You can install patch from [AUR](https://aur.archlinux.org/packages/asus-n550jx-subwoofer-fix/)

At the time of writing this article kernel [bug](https://bugzilla.kernel.org/show_bug.cgi?id=110001) is filled for this patch to be included in ALSA future releases.

## Keyboard

In order to make all keyboard function keys (FN+F{1..12}) generate correct signals - add [kernel parameter](/index.php/Kernel_parameters "Kernel parameters") 'acpi_osi=' (without quotation marks) to your bootloader.

# Troubleshooting

## nouveau problems

Installation media sometimes produces a lot of error messages during boot. This is a bug in the _nouveau_ driver. Just ignore hitting Enter few times. Later you can disable _nouveau_ module:

 `/etc/modprobe.d/blacklist-nouveau.conf`  `blacklist nouveau`