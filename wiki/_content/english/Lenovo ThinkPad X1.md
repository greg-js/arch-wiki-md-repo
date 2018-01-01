## Contents

*   [1 Model description](#Model_description)
*   [2 Installation method](#Installation_method)
    *   [2.1 Legacy-BIOS](#Legacy-BIOS)
    *   [2.2 UEFI](#UEFI)
*   [3 Hardware](#Hardware)
    *   [3.1 Fingerprint Reader](#Fingerprint_Reader)
    *   [3.2 Adjusting Backlight Brightness](#Adjusting_Backlight_Brightness)
    *   [3.3 Bluetooth](#Bluetooth)
*   [4 Power management](#Power_management)
*   [5 Extra Keys](#Extra_Keys)
*   [6 USB3 Issues](#USB3_Issues)

## Model description

Lenovo ThinkPad X1, Sandy Bridge (Core i5, 2,5 GHz), NWG2MRT This model has SSD 80/HDD 320 pair. Comes without optical drive. Has UEFI BIOS with BIOS-legacy fallback mode.

## Installation method

**Note:** If you'd like to create Windows recovery flash drive, do it before Arch installation with the help of autorun located at recovery partition, from your installed Windows system.

Due to the fact that there is no optical drive, you need to [install Arch from USB stick](/index.php/USB_Installation_Media "USB Installation Media").

### Legacy-BIOS

This procedure is far less involved then UEFI and works perfectly.

In order to turn off UEFI booting you will need to boot into your BIOS and change the boot mode to Legacy. Afterward, follow the [Installation guide](/index.php/Installation_guide "Installation guide") for standard installation instructions.

### UEFI

Installation from UEFI bootable USB works with the default bootloader, so rEFInd is unnecessary. In the BIOS under Startup, set "UEFI/Legacy Boot" to UEFI only. The default partition table (and Windows installation) uses MBR. For UEFI, reformat the disk as GPT.

Booting using an [efibootmgr entry](/index.php/UEFI_Bootloaders#Using_efibootmgr_entry "UEFI Bootloaders") works well. The warnings about incompatibility and embedding arguments to do not apply.

## Hardware

Almost everything works out of the box. Install synaptics and video-intel drivers.

### Fingerprint Reader

[fingerprint-gui](/index.php/Fingerprint-gui "Fingerprint-gui") from the [AUR](/index.php/AUR "AUR") is already patched to work with the X1's newer fingerprint reader.

It has been seen that the relevant udev rules do not get set properly. To do this, open `/usr/lib/udev/rules.d/40-libbsapi.rules` with your favorite text editor to add (or create with) the following lines:

 `/usr/lib/udev/rules.d/40-libbsapi.rules` 
```
ATTRS{idVendor}==”147e”, ATTRS{idProduct}==”2020″,   SYMLINK+=”input/touchchip-%k”, MODE=”0664″, GROUP=”plugdev”
ATTRS{idVendor}==”147e”, ATTRS{idProduct}==”2020″,   ATTR{power/control}==”*”, ATTR{power/control}=”auto”

```

Restart your computer for the udev change to take effect.

### Adjusting Backlight Brightness

Add `acpi_osi="!Windows 2012"` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") (see [https://bbs.archlinux.org/viewtopic.php?id=158775](https://bbs.archlinux.org/viewtopic.php?id=158775)).

### Bluetooth

Laptop has a Broadcom BCM20702 bluetooth chip. There are no drivers for this chip in any package. When you try to enable bluetooth you get the message `bluetooth hci0: Direct firmware load for brcm/BCM20702A1-0a5c-21e6.hcd failed with error -2` The file /lib/firmware/brcm/BCM20702A1-0a5c-21e6.hcd can be generated with the help of this guide [http://www.slackwiki.com/Btfirmware-nonfree](http://www.slackwiki.com/Btfirmware-nonfree) Those who don't want to hassle around can download the file from [here](https://yadi.sk/d/SeZeFsvJtt9YE) Don't forget to read the [Bluetooth](/index.php/Bluetooth "Bluetooth") page to finalize bluetooth setup to make it work.

## Power management

Just consult [Laptop](/index.php/Laptop "Laptop") and [Power management](/index.php/Power_management "Power management") pages.

Tp_smapi does not seem to work at all.

Suspend works fine, even with status indicator.

## Extra Keys

The sleep, wifi, brightness, and keyboard backlight keys all work out of the box. All of the others (volume, media, etc.) can be bound as described in [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys").

## USB3 Issues

With some external devices the USB3 hubs fails to hotplug and can be unstable and only reboots make external drives appear. The only solution I found is a firmware update of the NEC Corporation uPD720200 USB 3.0 Host Controller (rev 04) without official files from Lenovo!

The Firmware and it's installer can be found on station-drivers.com: [[1]](http://www.station-drivers.com/index.php/downloads/Drivers/Renesas-Nec/USB-3.0/Renesas-Nec-uPD720200a-USB-3.0-Controller-Firmware-Version-4.0.2.1.0.3/)

**Note:**

*   The Website is mostly in FRENCH! Télécharger means Download!!
*   The Installation can only be done from a 64bit Windows! so no 32bit BartPE Windows XP livecd will work and 64 Windows (tested with 64bit Win 7 Pro) has to be installed on the Laptop once to install the Firmware!
*   Since this is not officially propagated from Lenovo proceed with caution!