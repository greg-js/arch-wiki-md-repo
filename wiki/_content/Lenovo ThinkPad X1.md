# Lenovo ThinkPad X1

## Contents

*   [1 Model description](#Model_description)
*   [2 Installation method](#Installation_method)
    *   [2.1 Legacy-BIOS](#Legacy-BIOS)
    *   [2.2 UEFI](#UEFI)
*   [3 Hardware](#Hardware)
    *   [3.1 Fingerprint Reader](#Fingerprint_Reader)
    *   [3.2 Adjusting Backlight Brightness](#Adjusting_Backlight_Brightness)
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

In order to turn off UEFI booting you will need to boot into your BIOS and change the boot mode to Legacy. Afterward, follow the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") for standard installation instructions.

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

## Power management

Just consult [Laptop](https://wiki.archlinux.org/index.php/Laptop) page to read about [tp_smapi](https://wiki.archlinux.org/index.php/tp_smapi), [pm-utils](https://wiki.archlinux.org/index.php/pm-utils), [uswsusp](https://wiki.archlinux.org/index.php/Uswsusp) and [acpid](https://wiki.archlinux.org/index.php/Acpid).

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X1&oldid=412571](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X1&oldid=412571)"