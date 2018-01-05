| **Device** | **Status** | **Modules** |
| Intel | Working | xf86-video-intel |
| Nvidia | Partially Working | nvidia *or* nvidia-dkms |
| Wireless | Working | mwifiex |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | xf86-input-synaptics |
| Touchscreen | Working | intel_ipts |
| Camera | Not Working |
| Card Reader | Working |
| Bluetooth | Working | btusb |
| Battery Stats | Not Working |

This page contains instructions, tips, pointers, and links for installing and configuring Arch Linux on Microsoft Surface Book 2 devices.

## Contents

*   [1 Compatibility](#Compatibility)
    *   [1.1 What works?](#What_works.3F)
    *   [1.2 What doesn't work?](#What_doesn.27t_work.3F)
    *   [1.3 Nvidia](#Nvidia)
*   [2 UEFI Setup and Secure Boot](#UEFI_Setup_and_Secure_Boot)
*   [3 Booting](#Booting)
    *   [3.1 Boot from USB](#Boot_from_USB)
*   [4 Graphics Drivers](#Graphics_Drivers)
*   [5 Console fonts](#Console_fonts)

## Compatibility

The laptop works surprisingly well with Arch Linux, but requires a customized kernel with updated drivers and modules, [available on Github](https://github.com/jakeday/linux-surface) or in an AUR package, [linux-surface4](https://aur.archlinux.org/packages/linux-surface4/).

### What works?

**Note:** Touchscreen only works in a Window Manager or Desktop Environment that has full support for it. It's recognized as a mouse click otherwise.

*   Touchscreen
    *   Requires customized kernel.
*   Pen Input
    *   Requires customized kernel.
*   Removal of keyboard base
    *   A few seconds slower in Linux than in Windows
    *   May cause touchscreen to stop working until reboot
    *   May cause issues with dedicated graphics (if equipped)
*   Keyboard function and media keys, including volume and brightness adjustment of the keyboard and screen backlights.
*   Wireless Networking
*   Dedicated Nvidia graphics (If equipped)
    *   With big caveats, detailed below.

### What doesn't work?

*   Cameras
*   Battery Stats
*   Nvidia card is thermally throttled and the fan speed defaults to read-only zero keeping the throttle extremely low.

### Nvidia

The Nvidia 1050 and 1060 cards in the Surface Book 2 Performance Base are recognized by the kernel and supported by `nvidia` and `nvidia-dkms` drivers. However, when a load is put on the Nvidia graphics hardware, it immediately and severely throttles down to around 139MHz. The reason, as reported by `nvidia-smi`, is software thermal throttling. The cause is that, apparently, the fan cannot be controlled automatically, nor through `nvidia-smi` or `nvidia-settings`, even when the nvidia xorg `Coolbits` option is set to 8.

## UEFI Setup and Secure Boot

Follow [The manufacturer's directions](https://support.microsoft.com/en-us/help/4023531) for accessing UEFI setup:

1.  Shut down your Surface and wait about 10 seconds to be sure it is off.
2.  Press and hold the volume-up button on your Surface, and, at the same time, press and release the power button.
3.  When you see the Surface logo, release the volume-up button. The UEFI menu will appear within a few seconds.

Disabling Secure Boot is not necessary, but makes things easier.

## Booting

The information in [Boot loaders](/index.php/Boot_loaders "Boot loaders") applies here. [refind-efi](https://www.archlinux.org/packages/?name=refind-efi) works well.

### Boot from USB

Booting from USB is possible by reordering boot devices in the UEFI setup.

## Graphics Drivers

The standard [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver works with the Surface Book devices.

For devices equipped with dedicated Nvidia graphics, the [nvidia](https://www.archlinux.org/packages/?name=nvidia) driver supports the dedicated GPU.

## Console fonts

Because of the screen's resolution, the console font is barely readable - refer to [Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts") on how to change them.