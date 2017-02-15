## Contents

*   [1 Installation](#Installation)
*   [2 Drivers](#Drivers)
    *   [2.1 Nvidia/Optimus](#Nvidia.2FOptimus)
    *   [2.2 Touchpad](#Touchpad)
    *   [2.3 Networking](#Networking)
        *   [2.3.1 Wireless](#Wireless)
    *   [2.4 Audio](#Audio)
    *   [2.5 SteelSeries Keyboard](#SteelSeries_Keyboard)
*   [3 Misc](#Misc)
    *   [3.1 BIOS](#BIOS)

## Installation

Standard installation works per the [Installation guide](/index.php/Installation_guide "Installation guide") using [Systemd-boot](/index.php/Systemd-boot "Systemd-boot") when the laptop is in UEFI mode.

## Drivers

### Nvidia/Optimus

It is possible to use [Bumblebee](/index.php/Bumblebee "Bumblebee") to make the Nvidia GPU in this laptop usable. In order to avoid issues caused by the BIOS in the GS63VR when using bbswitch, add `acpi_osi=! acpi_osi="Windows 2009"` to the kernel options at boot (per [NVIDIA_Optimus#Lockup_issue_.28lspci_hangs.29](/index.php/NVIDIA_Optimus#Lockup_issue_.28lspci_hangs.29 "NVIDIA Optimus")).

For HDMI/DP ouput: [Bumblebee#Output_wired_to_the_NVIDIA_chip](/index.php/Bumblebee#Output_wired_to_the_NVIDIA_chip "Bumblebee").

### Touchpad

This laptop uses an Elantech touchpad, and as such [libinput](/index.php/Libinput "Libinput") works well.

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