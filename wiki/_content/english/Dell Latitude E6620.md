The Dell Latitude E6220.

This article will tell you how to get the basic components of the laptop running with Arch.

## Contents

*   [1 Firmware upgrade](#Firmware_upgrade)
*   [2 Hardware](#Hardware)
    *   [2.1 Supported](#Supported)
    *   [2.2 Unsupported](#Unsupported)
    *   [2.3 Unchecked](#Unchecked)
*   [3 Installation](#Installation)
    *   [3.1 Touchpad](#Touchpad)
    *   [3.2 Wireless](#Wireless)

## Firmware upgrade

This part is optional but may improve stability/performance/compatibility. Although I have no proof for that.

*   Install BIOS A02 - [http://www.dell.com/support/home/us/en/19/Drivers/DriversDetails?driverId=9207V](http://www.dell.com/support/home/us/en/19/Drivers/DriversDetails?driverId=9207V)

*   Install BIOS A13 - [http://www.dell.com/support/home/us/en/19/Drivers/DriversDetails?driverId=9GRN4](http://www.dell.com/support/home/us/en/19/Drivers/DriversDetails?driverId=9GRN4)

## Hardware

Linux on this laptop works very well

### Supported

*   Hibernate / Resume
*   Volume keys (hardware keys)
*   Brightness keys (Fn + up/down arrows)

### Unsupported

*   Fingerprint reader

### Unchecked

*   Bluetooth

## Installation

The [Installation guide](/index.php/Installation_guide "Installation guide") should get you running. UEFI booting also works perfectly when enabled in the BIOS.

### Touchpad

For the TouchPad to work correctly install the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) package. The touchpad works really well and also supports two finger scroll.

### Wireless

To get the wireless working, see the Broadcom Wireless wiki page: [Broadcom wireless#Installation](/index.php/Broadcom_wireless#Installation "Broadcom wireless")