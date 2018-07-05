Not to be confused with [MSI GS63VR](/index.php/MSI_GS63VR "MSI GS63VR")

## Contents

*   [1 Introduction](#Introduction)
*   [2 Compatibility](#Compatibility)
*   [3 Installation](#Installation)
*   [4 Workarounds and fixes](#Workarounds_and_fixes)
    *   [4.1 Audio](#Audio)
    *   [4.2 GPU Switching](#GPU_Switching)
*   [5 Miscellaneous](#Miscellaneous)

## Introduction

The GE63VR series of laptops was revealed mid-2017 by MSI. They feature a relatively thin (for gaming laptops) metal-alloy chassis, 7th generation Intel processors (Kaby lake), a 120Hz/3 ms built-in screen, and a per-key RGB keyboard backlighting.

Only the variant GE63VR-7RE (or GE63VR Raider-215) was tested. Its specifications are :

*   CPU : i7-7700HQ 2.8 Ghz (Turbo up to 3.8 Ghz)
*   RAM : 16 GB DDR4
*   GPU : Integrated HD Graphics 630 + Dedicated NVidia GTX 1060 (6 GB)
*   Storage : Samsung NVMe SSD 512 GB
*   Built-in screen : Full HD 3 ms 120 Hz

The laptop was last tested with official kernel 4.17.2-1.

## Compatibility

| Feature | Works ? | Comments |
| Touchpad | Yes | Two-fingers scrolling works, both horizontal and vertical. |
| Camera and integrated microphone | Yes | Default volume settings for the microphone result in horribly distorted input, you may need to adjust them in the **alsamixer** console. |
| Function keys | Yes | Some function keys are specific to MSI and do not work since they require a special driver. Standard function keys (such as volume, brightness, toggle external monitor, etc) work. |
| Audio | Yes with workaround | Plugging in headphones mutes audio, see below for fix.

Not tested : plugging an external microphone, audio through HDMI.

 |
| WiFi | Yes |
| Bluetooth | Yes |
| HDMI display | Partially | Only works if the dedicated GPU is powered on. You either have to run the whole X session on the NVidia card with proprietary drivers, or use [Reverse PRIME](/index.php/PRIME#Reverse_PRIME "PRIME") with the **nouveau** driver, or use [intel-virtual-output](/index.php/Bumblebee#Output_wired_to_the_NVIDIA_chip "Bumblebee"). The last two solutions have not been tested. |
| DisplayPort | Not tested |
| USB-C | Not tested |
| Dedicated GPU | Yes |
| GPU switching | Yes with workaround | Starting X on integrated graphics with the dedicated GPU turned off causes the system to hang. See below for fix. **bumblebee** has not been tested. |
| Screen backlighting control | Yes |
| Keyboard backlighting control | Partially | Function keys can control the brightness but not the color or the pattern of the backlighting.

Open-source tools such as [MSIKLM](https://github.com/Gibtnix/MSIKLM) do not work for this particular laptop model.

 |
| SD card reader | Not tested | A "wrong version" warning is thrown at boot about the SD controller. |
| Sleep/Resume | Partially | When running the X server from the dedicated GPU, resuming from sleep causes garbled rendering in opened applications. The kernel also throws errors about the NVidia card. |
| Hibernation to disk | Not tested |

## Installation

You have to disable **Fast Boot** and **Intel CPU P-States** in the BIOS. Then follow the [Installation guide](https://en.wikipedia.org/wiki/Arch_Linux "wikipedia:Arch Linux") to install in UEFI mode.

## Workarounds and fixes

### Audio

By default, [ALSA](https://en.wikipedia.org/wiki/Arch_Linux "wikipedia:Arch Linux") reports **Headphone** and **Speaker** channels separately. However, on this laptop, the **Speaker** channel actually controls both the speakers and the plugged-in headphones, while the **Headphone** channel does not control anything. This is a problem because [PulseAudio](https://en.wikipedia.org/wiki/Arch_Linux "wikipedia:Arch Linux") automatically sets the **Speaker** channel to zero when headphones are plugged in, which causes all outputs to be muted in this case.

The proposed fix is to disable the auto-mute feature ([https://bbs.archlinux.org/viewtopic.php?id=237456](https://bbs.archlinux.org/viewtopic.php?id=237456)). Edit the file `/usr/share/pulseaudio/alsa-mixer/paths/analog-output-headphones.conf` and replace the section

```
[Element Speaker]
switch = off
volume = off

```

by

```
[Element Speaker]
switch = off
volume = merge

```

### GPU Switching

The system will hang if you try to start the X server while the NVidia GPU is turned off via **bbswitch**. To fix it, add `acpi_osi=! acpi_osi="Windows 2009"` to your kernel parameters. Beware of the quotes `"` : for instance, if you use [rEFInd](https://en.wikipedia.org/wiki/Arch_Linux "wikipedia:Arch Linux") as you bootloader, you will have to escape the quotes as `""` since rEFInd already uses quotes in its configuration file.

To run the whole X session on the NVidia card, follow the guide in [NVIDIA Optimus#Using nvidia](/index.php/NVIDIA_Optimus#Using_nvidia "NVIDIA Optimus").

To enable PRIME synchronisation for the built-in monitor, [enable DRM kernel mode setting for the NVidia driver](/index.php/NVIDIA#DRM_kernel_mode_setting "NVIDIA").

## Miscellaneous

The following error sometimes appears in kernel messages, but seems harmless :

```
ACPI Error: No handler for Region [VRTC] (00000000e51c2f4b) [SystemCMOS] (20180313/evregion-132)
ACPI Error: Region SystemCMOS (ID=5) has no handler (20180313/exfldio-265)
ACPI Error: Method parse/execution failed \_SB.PCI0.LPCB.EC._Q9A, AE_NOT_EXIST (20180313/psparse-516)

```