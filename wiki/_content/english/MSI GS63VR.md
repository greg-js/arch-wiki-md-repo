<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Introduction](#Introduction)
*   [2 Installation](#Installation)
*   [3 Drivers](#Drivers)
    *   [3.1 Nvidia/Optimus](#Nvidia/Optimus)
    *   [3.2 Touchpad](#Touchpad)
    *   [3.3 Networking](#Networking)
        *   [3.3.1 Wireless](#Wireless)
    *   [3.4 Audio](#Audio)
    *   [3.5 SteelSeries Keyboard](#SteelSeries_Keyboard)
        *   [3.5.1 GS63-8RE](#GS63-8RE)
    *   [3.6 Sleep](#Sleep)
    *   [3.7 Web Camera](#Web_Camera)
        *   [3.7.1 GS63-8RE](#GS63-8RE_2)
    *   [3.8 Power Management](#Power_Management)
        *   [3.8.1 GS63-8RE](#GS63-8RE_3)
*   [4 Misc](#Misc)
    *   [4.1 BIOS](#BIOS)

## Introduction

The GS series of MSI laptops is considered to be a thin gaming laptop. Although it is not thin as ultrabooks, it is still very thin for a *gaming* laptop. As of October 5th 2017, the 2016 model works fine with the latest kernel. The 2017 model has a bug concerning the eDP LCD display. There is a fix from intel here: [https://github.com/freedesktop/drm-tip/commit/0501a3b0eb01ac2209ef6fce76153e5d6b07034e.patch](https://github.com/freedesktop/drm-tip/commit/0501a3b0eb01ac2209ef6fce76153e5d6b07034e.patch)

This issue was discussed in this thread: [https://bbs.archlinux.org/viewtopic.php?id=230541](https://bbs.archlinux.org/viewtopic.php?id=230541)

As of 2018, the patch is now part of the mainstream kernel. Intel driver (i915) works, but without power management. It is only possible to run a graphical environment with the nvidia card ON. In order to get the maximum performance out of this notebook, it is recommended to use [nvidia-xrun](https://aur.archlinux.org/packages/nvidia-xrun-git). Bumblebee is not working on the 2017 model.

| **Device** | **[GS63-6RF](https://www.msi.com/Laptop/GS63VR-6RF-Stealth-Pro/Specification) (2016)** | **GS63 (2017)** | **[GS63-8RE](https://www.msi.com/Laptop/GS63-Stealth-8RE/Specification) (2018)** |
| CPU | Yes i7-6700HQ | Yes i7-7700HQ | Yes i7-8750H |
| Display | -- | Full HD 120Hz/3ms | Full HD 120Hz/3ms |
| Intel IGU | Yes Intel HD Graphics 530 | Yes HD Graphics 630 (i915) | Yes Intel HD Graphics 630 |
| Nvidia GPU | Yes GTX 1060 | Yes GTX 1070 | Yes GTX 1060 |
| [Network](/index.php/Network "Network") | Yes | Yes | Yes |
| Atheros Wireless | Yes | Yes | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes | Yes | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Manual | Yes | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes | Yes | Yes |
| Card Reader | Yes | mmc warning | Yes |
| [Power management](/index.php/Power_management "Power management") | Yes | No | Yes |

## Installation

Standard installation works flawlessly per the [Installation guide](/index.php/Installation_guide "Installation guide").

## Drivers

### Nvidia/Optimus

It is possible to use [Bumblebee](/index.php/Bumblebee "Bumblebee") to make the Nvidia GPU in this laptop usable. In order to avoid issues caused by the BIOS in the GS63VR when using bbswitch, add `acpi_osi=! acpi_osi="Windows 2009"` to the kernel options at boot (per [NVIDIA Optimus#Lockup issue (lspci hangs)](/index.php/NVIDIA_Optimus#Lockup_issue_(lspci_hangs) "NVIDIA Optimus")).

For HDMI/DP ouput: [Bumblebee#Output wired to the NVIDIA chip](/index.php/Bumblebee#Output_wired_to_the_NVIDIA_chip "Bumblebee").

As alternative, you can use [Optimus Manager](https://github.com/Askannz/optimus-manager). You can change between Intel and Nvidia restarting the X server and use external screen use nouveau driver.

### Touchpad

This laptop uses an Elantech touchpad, and as such [libinput](/index.php/Libinput "Libinput") works well. Two finger scrolling works out of the box (tested on GS63-6RF and GS63-8RE). Install [libinput-gestures](https://aur.archlinux.org/packages/libinput-gestures/) for more multitouch actions.

### Networking

#### Wireless

[NetworkManager](/index.php/NetworkManager "NetworkManager") works out of the box for wifi on both 2.4GHz and 5GHz networks.

### Audio

The headphone jack always acts as SPDIF out and subsequently has no volume control and does not mute the speakers when a device is plugged in. [Link to a description of the issue on the ALSA mailing list](https://sourceforge.net/p/alsa/mailman/message/35292536/).

As a workaround it is possible to reassign a microphone input jack using hdajackretask to behave as an audio output.

### SteelSeries Keyboard

To set color to Steel Series Keyboard use [MSIKLM](https://github.com/Gibtnix/MSIKLM)

#### GS63-8RE

Use the instructions on [MSI GS65#Lights](/index.php/MSI_GS65#Lights "MSI GS65") to install [msi-perkeyrgb](https://aur.archlinux.org/packages/msi-perkeyrgb/).

### Sleep

If the laptop doesn't fully enter sleep mode, bluetooth and mobile light stay on and sleep light does not come on. Then try reinstalling [TLP](/index.php/TLP "TLP").

### Web Camera

#### GS63-8RE

`Fn + F6` will toggle disable/ enable the web camera.

### Power Management

#### GS63-8RE

After installing [NVIDIA](/index.php/NVIDIA "NVIDIA"), [bumblebee](/index.php/Bumblebee "Bumblebee"), and [bbswitch](/index.php/Bbswitch "Bbswitch") while running [KDE](/index.php/KDE "KDE") power usage is down to ~7W or 9 hours according to [powertop](/index.php/Powertop "Powertop").

## Misc

### BIOS

To access the BIOS, from a cold shutdown, repeatedly press the `delete` key immediately after pressing the power button. To access the Boot Device Menu, from a cold shutdown, repeatedly press the `F11` key immediately after pressing the power button.