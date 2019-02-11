| **Device** | **Status** | **Modules** |
| Intel | Working | xf86-video-intel |
| Nvidia | Working | nvidia *or* nvidia-dkms |
| Wireless | Working | mwifiex |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | xf86-input-synaptics |
| Touchscreen | Working | intel_ipts |
| Camera | Not Working |
| Card Reader | Working |
| Bluetooth | Working | btusb |
| Battery Stats | Working |

This page contains instructions, tips, pointers, and links for installing and configuring Arch Linux on Microsoft Surface Book 2 devices.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Compatibility](#Compatibility)
    *   [1.1 What works?](#What_works?)
    *   [1.2 What doesn't work?](#What_doesn't_work?)
    *   [1.3 Nvidia](#Nvidia)
*   [2 UEFI Setup and Disabling Secure Boot](#UEFI_Setup_and_Disabling_Secure_Boot)
*   [3 Booting](#Booting)
    *   [3.1 Boot from USB](#Boot_from_USB)
*   [4 Graphics Drivers](#Graphics_Drivers)
*   [5 Audio](#Audio)
*   [6 WiFi](#WiFi)
*   [7 Console fonts](#Console_fonts)
*   [8 Hibernation](#Hibernation)

## Compatibility

The laptop works surprisingly well with Arch Linux, but requires a kernel with modules and updated drivers, [available on Github](https://github.com/jakeday/linux-surface) or in an AUR package, [linux-surface4](https://aur.archlinux.org/packages/linux-surface4/) or via a separately maintained [PKGBULD on Github](https://github.com/dmhacker/arch-linux-surface) (whichever you choose, make sure to check that you'll get the latest version of the jakeday kernel [linux-surface4](https://aur.archlinux.org/packages/linux-surface4/) seems to be a bit behind).

### What works?

**Note:** Touchscreen only works in a Window Manager or Desktop Environment that has full support for it. It's recognized as a mouse click otherwise.

*   Touchscreen
    *   Requires kernel with modules/drivers in link above.
*   Pen Input
    *   Requires kernel with modules/drivers in link above.
*   Removal of keyboard base
    *   A few seconds slower in Linux than in Windows
    *   May cause touchscreen to stop working until reboot
    *   May cause issues with dedicated graphics (if equipped)
*   Keyboard function and media keys, including volume and brightness adjustment of the keyboard and screen backlights.
*   Wireless Networking
    *   May need a tweak from [#WiFi](#WiFi) if Wireless Networking hardware disconnects during use
*   Speakers / Headphones
    *   Speakers sometimes have a hissing noise that can be fixed, details in [#Audio](#Audio)
*   Dedicated Nvidia graphics (If equipped)
*   Hibernation
    *   Only when the touchscreen is disabled, see [#Hibernation](#Hibernation)
*   ACPI, Battery stats, power saving, etc.

### What doesn't work?

*   Cameras

### Nvidia

The Nvidia 1050 and 1060 cards in the Surface Book 2 Performance Base are recognized by the kernel and supported by `nvidia` and `nvidia-dkms` drivers. Without the kernel ([linux-surface4](https://aur.archlinux.org/packages/linux-surface4/)), there **was** a bug which causes it to be effectively useless because when a load is put on the Nvidia graphics hardware, it immediately and severely throttles down to around 139MHz. The reason, as reported by `nvidia-smi`, is software thermal throttling. The cause is that, apparently, the fan cannot be controlled automatically, nor through `nvidia-smi` or `nvidia-settings`, even when the nvidia xorg `Coolbits` option is set to 8.

## UEFI Setup and Disabling Secure Boot

Disabling Secure Boot is not necessary, but makes things easier.

Follow [The manufacturer's directions](https://support.microsoft.com/en-us/help/4023531) for accessing UEFI setup:

1.  Shut down your Surface and wait about 10 seconds to be sure it is off.
2.  Press and hold the volume-up button on your Surface, and, at the same time, press and release the power button.
3.  When you see the Surface logo, release the volume-up button. The UEFI menu will appear within a few seconds.

## Booting

The information in [Boot loaders](/index.php/Boot_loader "Boot loader") applies here. [refind-efi](https://www.archlinux.org/packages/?name=refind-efi) and [Systemd-boot](/index.php/Systemd-boot "Systemd-boot") work well.

### Boot from USB

Booting from USB is possible by reordering boot devices in the UEFI setup.

## Graphics Drivers

The standard [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver works with the Surface Book devices.

For devices equipped with dedicated Nvidia graphics, the [nvidia](https://www.archlinux.org/packages/?name=nvidia) or [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms) driver supports the dedicated GPU.

## Audio

Surface Book 2 devices exhibit a hissing noise at times. This can be fixed by installing [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) and running the following commands:

```
amixer -c 0 sset 'Auto-Mute Mode' Disabled
sudo alsactl store

```

## WiFi

Since September 2018, Surface Book 2 WiFi may power off during use. When this happens, it is not visible in lspci and rebooting is a way to get it back on. However, this behavior can be prevented (temporarily) by installing [iw](https://www.archlinux.org/packages/?name=iw) and running the following command as root:

```
# iw dev wlp1s0 set power_save off

```

To permanently fix the issue with NetworkManager, add this to your [NetworkManager](/index.php/NetworkManager "NetworkManager") config. (Such as /etc/NetworkManager/NetworkManager.conf)

```
[connection]
wifi.powersave = 2
[device]
wifi.scan-rand-mac-address=false

```

## Console fonts

Because of the screen's resolution, the console font is barely readable - refer to [Linux console#Fonts](/index.php/Linux_console#Fonts "Linux console") on how to change them.

Using [terminus-font](https://www.archlinux.org/packages/?name=terminus-font) with 32pt looks good on Surface Book 2 on the vconsole (add `FONT=ter-m32n` to `/etc/vconsole.conf` after installing).

## Hibernation

Hibernation with the jakeday kernel only works when the touchscreen firmware loading is disabled (adding `i915.enable_guc=0` to the kernel parameters).