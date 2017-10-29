## Contents

*   [1 Introduction](#Introduction)
*   [2 Installation](#Installation)
*   [3 Drivers](#Drivers)
    *   [3.1 Nvidia/Optimus](#Nvidia.2FOptimus)
    *   [3.2 Touchpad](#Touchpad)
    *   [3.3 Networking](#Networking)
        *   [3.3.1 Wireless](#Wireless)
    *   [3.4 Audio](#Audio)
    *   [3.5 SteelSeries Keyboard](#SteelSeries_Keyboard)
*   [4 Misc](#Misc)
    *   [4.1 BIOS](#BIOS)

## Introduction

The GS series of MSI laptops is considered to be a thin gaming laptop. Although it is not thin as ultrabooks, it is still very thin for a *gaming* laptop. As of October 5th 2017, the 2016 model works fine with the latest kernel. The 2017 model has a bug concerning the eDP LCD display. There is a fix from intel here: [https://github.com/freedesktop/drm-tip/commit/0501a3b0eb01ac2209ef6fce76153e5d6b07034e.patch](https://github.com/freedesktop/drm-tip/commit/0501a3b0eb01ac2209ef6fce76153e5d6b07034e.patch)

This issue was discussed in this thread: [https://bbs.archlinux.org/viewtopic.php?id=230541](https://bbs.archlinux.org/viewtopic.php?id=230541)

| **Device** | **GS63 (2016)** | **GS63 (2017)** | **GS73 (2016)** |
| [Display](/index.php?title=Display&action=edit&redlink=1 "Display (page does not exist)") | -- | Full HD 120Hz/3ms | -- |
| [Intel IGU](/index.php?title=Intel_IGU&action=edit&redlink=1 "Intel IGU (page does not exist)") | Yes | (with patch) i915 |  ?? |
| [Nvidia GPU](/index.php?title=Nvidia_GPU&action=edit&redlink=1 "Nvidia GPU (page does not exist)") | Yes | Yes nvidia |  ?? |
| [Network](/index.php/Network "Network") | Yes | Yes |  ?? |
| Atheros Wireless | Yes | Yes |  ?? |
| [ALSA](/index.php/ALSA "ALSA") | Yes | Yes |  ?? |
| [Touchpad](/index.php/Touchpad "Touchpad") | Manual | Yes |  ?? |
| [Webcam](/index.php/Webcam "Webcam") | Yes | Yes |  ?? |
| Card Reader | Yes | mmc warning |  ?? |
| [Power management](/index.php/Power_management "Power management") | Yes | No |  ?? |

## Installation

Standard installation works per the [Installation guide](/index.php/Installation_guide "Installation guide") using [Systemd-boot](/index.php/Systemd-boot "Systemd-boot") when the laptop is in UEFI mode.

## Drivers

### Nvidia/Optimus

It is possible to use [Bumblebee](/index.php/Bumblebee "Bumblebee") to make the Nvidia GPU in this laptop usable. In order to avoid issues caused by the BIOS in the GS63VR when using bbswitch, add `acpi_osi=! acpi_osi="Windows 2009"` to the kernel options at boot (per [NVIDIA Optimus#Lockup issue (lspci hangs)](/index.php/NVIDIA_Optimus#Lockup_issue_.28lspci_hangs.29 "NVIDIA Optimus")).

For HDMI/DP ouput: [Bumblebee#Output wired to the NVIDIA chip](/index.php/Bumblebee#Output_wired_to_the_NVIDIA_chip "Bumblebee").

### Touchpad

This laptop uses an Elantech touchpad, and as such [libinput](/index.php/Libinput "Libinput") works well.

Note* As of 2017.04.18, some multitouch aspects of the touchpad do not seem to be working (two finger scroll, for instance). This bug has been reported [here](https://bugs.freedesktop.org/show_bug.cgi?id=100696).

### Networking

#### Wireless

[NetworkManager](/index.php/NetworkManager "NetworkManager") works out of the box for wifi on both 2.4GHz and 5GHz networks.

### Audio

The headphone jack always acts as SPDIF out and subsequently has no volume control and does not mute the speakers when a device is plugged in. [Link to a description of the issue on the ALSA mailing list](https://sourceforge.net/p/alsa/mailman/message/35292536/).

As a workaround it is possible to reassign a microphone input jack using hdajackretask to behave as an audio output.

### SteelSeries Keyboard

To set color to Steel Series Keyboard use [MSIKLM](https://github.com/Gibtnix/MSIKLM)

## Misc

### BIOS

To access the BIOS, from a cold shutdown, repeatedly press the `delete` key immediately after pressing the power button.