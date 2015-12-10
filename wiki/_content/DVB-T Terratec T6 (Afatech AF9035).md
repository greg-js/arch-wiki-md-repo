# DVB-T Terratec T6 (Afatech AF9035)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

The TerraTec T6 is a dual [DVB-T](/index.php/DVB-T "DVB-T") USB-device. The device is supported by the kernel, but requires additional proprietary firmware to be loaded to function.

This tutorial was tested for a Terratec T6 with the [Afatech AF9035](http://www.linuxtv.org/wiki/index.php/Afatech_AF9035) chipset. There is a package in the AUR, but it does not work at this time.

## Identify chipset

Filter _dmesg_ to find out the exact chipset with the following command:

```
$ dmesg | grep dvb
usb 3-1: dvb_usb_af9035: prechip_version_00 chip_version_03 chip_type_3802 
usb 3-1: dvb_usb_af9035: prechip_version=00 chip_version=03 chip_type=3802 
usb 3-1: dvb_usb_v2: found a 'Afatech AF9035 reference design' in **cold state**}}

```

The **cold state** indicates it is not active, due to the missing firmware file.

## Download firmware

The firmware file in this case was made available at: [[1]](http://palosaari.fi/linux/v4l-dvb/firmware/af9035/)

Download the file of your choice and navigate to the download-folder.

## Install firmware

Without a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") the file cannot be installed (and tracked) with pacman. However, for a firmware the main step of an installation is to move the file into the `/lib/firmware` path.

If you move the file manually and re-plug the device, _dmesg_ should show the firmware loaded and the device is now in **warm state**:

```
$ dmesg |grep -e dvb -e af9033
usb 3-1: dvb_usb_af9035: prechip_version=00 chip_version=03 chip_type=3802
usb 3-1: dvb_usb_v2: found a 'Afatech AF9035 reference design' in cold state
usb 3-1: dvb_usb_v2: downloading firmware from file 'dvb-usb-af9035-02.fw'
usb 3-1: dvb_usb_af9035: firmware version=12.13.15.0
usb 3-1: dvb_usb_v2: found a 'Afatech AF9035 reference design' in **warm state**
usb 3-1: dvb_usb_v2: will pass the complete MPEG2 transport stream to the software demuxer
DVB: registering new adapter (Afatech AF9035 reference design)
calling  af9033_driver_init+0x0/0x1000 [af9033] @ 5364
initcall af9033_driver_init+0x0/0x1000 [af9033] returned 0 after 47 usecs
af9033 7-0038: **firmware version: LINK 12.13.15.0 - OFDM 6.20.15.0**
af9033 7-0038: Afatech AF9033 successfully attached
usb 3-1: DVB: registering adapter 0 frontend 0 (Afatech AF9033 (DVB-T))...

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=DVB-T_Terratec_T6_(Afatech_AF9035)&oldid=389743](https://wiki.archlinux.org/index.php?title=DVB-T_Terratec_T6_(Afatech_AF9035)&oldid=389743)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [TV cards](/index.php/Category:TV_cards "Category:TV cards")