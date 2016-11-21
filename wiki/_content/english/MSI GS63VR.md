## Contents

*   [1 Installation](#Installation)
*   [2 Drivers](#Drivers)
    *   [2.1 Nvidia/Optimus](#Nvidia.2FOptimus)
    *   [2.2 Touchpad](#Touchpad)
    *   [2.3 Networking](#Networking)
        *   [2.3.1 Wireless](#Wireless)
*   [3 Misc](#Misc)
    *   [3.1 BIOS](#BIOS)

## Installation

Standard installation works per the [Installation guide](/index.php/Installation_guide "Installation guide") using [Systemd-boot](/index.php/Systemd-boot "Systemd-boot") when the laptop is in UEFI mode.

## Drivers

### Nvidia/Optimus

It is possible to use [Bumblebee](/index.php/Bumblebee "Bumblebee") to make the Nvidia GPU in this laptop usable. In order to avoid issues caused by the BIOS in the GS63VR when using bbswitch, add `acpi_osi=! acpi_osi="Windows 2009"` to the kernel options at boot (per [NVIDIA_Optimus#Lockup_issue_.28lspci_hangs.29](/index.php/NVIDIA_Optimus#Lockup_issue_.28lspci_hangs.29 "NVIDIA Optimus")).

### Touchpad

This laptop uses an Elantech touchpad, and as such [libinput](/index.php/Libinput "Libinput") works well.

### Networking

#### Wireless

[NetworkManager](/index.php/NetworkManager "NetworkManager") works out of the box for wifi on both 2.4GHz and 5GHz networks.

## Misc

### BIOS

To access the BIOS, from a cold shutdown, repeatedly press the `delete` key immediately after pressing the power button.