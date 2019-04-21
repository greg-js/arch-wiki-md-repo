Not to be confused with [MSI GS63VR](/index.php/MSI_GS63VR "MSI GS63VR")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Introduction](#Introduction)
*   [2 Compatibility](#Compatibility)
*   [3 Installation](#Installation)
*   [4 Workarounds and fixes](#Workarounds_and_fixes)
    *   [4.1 Audio](#Audio)
    *   [4.2 GPU Switching](#GPU_Switching)
    *   [4.3 RGB keyboard backlighting](#RGB_keyboard_backlighting)
*   [5 Miscellaneous](#Miscellaneous)

## Introduction

The GE63VR series of laptops was revealed mid-2017 by MSI. They feature a relatively thin (for gaming laptops) metal-alloy chassis, 7th generation Intel processors (Kaby lake), a 120Hz/3 ms built-in screen, and a per-key RGB keyboard backlighting.

Only the variant GE63VR-7RE (or GE63VR Raider-215) was tested. Its specifications are :

*   CPU : i7-7700HQ 2.8 Ghz (Turbo up to 3.8 Ghz)
*   RAM : 16 GB DDR4
*   GPU : Integrated HD Graphics 630 + Dedicated NVidia GTX 1060 (6 GB)
*   Storage : Samsung NVMe SSD 512 GB
*   Built-in screen : Full HD 3 ms 120 Hz

The laptop was last tested with official kernel 4.18.5.

## Compatibility

| Feature | Works ? | Comments |
| Touchpad | Yes | Two and three fingers gestures work. |
| Camera and integrated microphone | Yes | Default volume settings for the microphone result in horribly distorted input, you may need to adjust them in the **alsamixer** console. |
| Function keys | Yes | Some function keys are specific to MSI and provide a shortcut for switching power modes on Windows. Of course they are inactive on Linux. They are recognized by the system though, and could probably be remapped by the user if wanted. Other standard function keys (such as volume, brightness, toggle external monitor, etc) work with no issues. |
| Audio | Yes with workaround | Plugging in headphones mutes audio, see below for fix.

Not tested : plugging an external microphone, audio through HDMI.

 |
| WiFi | Yes |
| Bluetooth | Yes |
| HDMI display | Partially | Only works if the dedicated GPU is powered on. You either have to run the whole X session on the NVidia card with proprietary drivers, or use [Reverse PRIME](/index.php/PRIME#Reverse_PRIME "PRIME") with the **nouveau** driver, or use [intel-virtual-output](/index.php/Bumblebee#Output_wired_to_the_NVIDIA_chip "Bumblebee"). The last two solutions have not been tested. |
| DisplayPort | Partially | Only works if the dedicated GPU is powered on. You either have to run the whole X session on the NVidia card with proprietary drivers, or use [Reverse PRIME](/index.php/PRIME#Reverse_PRIME "PRIME") with the **nouveau** driver, or use [intel-virtual-output](/index.php/Bumblebee#Output_wired_to_the_NVIDIA_chip "Bumblebee"). The last two solutions have not been tested. |
| USB-C | Yes | Tested with USB-C adapter Dell DA-200 (Ethernet OK; USB 3.0 OK; VGA not tested; HDMI not tested) |
| Dedicated GPU | Yes |
| GPU switching | Yes with workaround | Starting X on integrated graphics with the dedicated GPU turned off causes the system to hang. See below for fix. Once the fix has been applied, **bumblebee** and **PRIME** both work. |
| Screen backlighting control | Yes |
| Keyboard RGB backlighting control | Partially | Only partial control is available, see below. |
| SD card reader | Yes | A "wrong version" warning is thrown at boot about the SD controller, but it works. |
| Sleep/Resume | Yes |
| Hibernation to disk | Yes |

## Installation

You have to disable **Fast Boot** in the BIOS, then follow the [Installation guide](https://en.wikipedia.org/wiki/Arch_Linux "wikipedia:Arch Linux") to install in UEFI mode. If you run into CPU lockup errors, also disable **C-States**.

## Workarounds and fixes

### Audio

By default, [ALSA](https://en.wikipedia.org/wiki/Arch_Linux "wikipedia:Arch Linux") reports **Headphone** and **Speaker** channels separately. However, on this laptop, the **Speaker** channel actually controls both the speakers and the plugged-in headphones, while the **Headphone** channel does not control anything. This is a problem because [PulseAudio](https://en.wikipedia.org/wiki/Arch_Linux "wikipedia:Arch Linux") automatically sets the **Speaker** channel to zero when headphones are plugged in, which causes all outputs to be muted in this case.

The proposed fix is to disable the auto-mute feature ([https://bbs.archlinux.org/viewtopic.php?id=237456](https://bbs.archlinux.org/viewtopic.php?id=237456)). Edit the file `/usr/share/pulseaudio/alsa-mixer/paths/analog-output-headphones.conf` and replace the section

```
[Element Speaker]
switch = off
volume = off

```

with

```
[Element Speaker]
switch = off
volume = merge

```

Note : This change may get overwritten when PulseAudio is updated.

### GPU Switching

The system will hang if you try to start the X server while the NVidia GPU is turned off via **bbswitch**. To fix it, add `acpi_osi=! acpi_osi="Windows 2009"` to your kernel parameters. Beware of the quotes `"` : for instance, if you use [rEFInd](https://en.wikipedia.org/wiki/Arch_Linux "wikipedia:Arch Linux") as you bootloader, you will have to escape the quotes as `""` since rEFInd already uses quotes in its configuration file.

To run the whole X session on the NVidia card, follow the guide in [NVIDIA Optimus#Using nvidia](/index.php/NVIDIA_Optimus#Using_nvidia "NVIDIA Optimus").

To enable PRIME synchronisation for the built-in monitor, [enable DRM kernel mode setting for the NVidia driver](/index.php/NVIDIA#DRM_kernel_mode_setting "NVIDIA").

### RGB keyboard backlighting

On Windows, RGB keyboard backlighting can be configured with the SteelSeries Engine software, which is not available on Linux. As an alternative, the tool [msi-perkeyrgb](https://aur.archlinux.org/packages/msi-perkeyrgb/) provides partial control, specifically for MSI laptops with per-key RGB. Tools designed for models with region-based RGB, such as [MSIKLM](https://github.com/Gibtnix/MSIKLM), will not work.

Since the RGB settings are stored into the keyboard itself, another option for dual-boot owners is to configure the keyboard once in Windows, and then reboot into Linux.

## Miscellaneous

The following error sometimes appears in kernel messages, but seems harmless :

```
ACPI Error: No handler for Region [VRTC] (00000000e51c2f4b) [SystemCMOS] (20180313/evregion-132)
ACPI Error: Region SystemCMOS (ID=5) has no handler (20180313/exfldio-265)
ACPI Error: Method parse/execution failed \_SB.PCI0.LPCB.EC._Q9A, AE_NOT_EXIST (20180313/psparse-516)

```