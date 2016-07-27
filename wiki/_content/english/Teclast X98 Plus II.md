Teclast X98 Plus II is a 2 in 1 tablet PC device, equipped with a 9.7 inch retina display that supports for 2048 x 1536 pixels. Besides, the Teclast X98 Plus II is a dual OS supporting device that allows users to take advantage of both Windows 10 and Android 5.1 operating systems on the device. It is powered by fifth-generation Intel Atom Z8300 graphics and eighth-generation Intel HD graphics, coupled with 4GB of RAM.

The tablet can run the x86_64 version of Archlinux, but at the time of writing this page, hardware support is **terrible**, pretty much nothing works out of the box.

## Contents

*   [1 How to install](#How_to_install)
*   [2 What works out of the box](#What_works_out_of_the_box)
*   [3 What does not work](#What_does_not_work)
    *   [3.1 Power management](#Power_management)
    *   [3.2 Touchscreen (needs hacking, works)](#Touchscreen_.28needs_hacking.2C_works.29)
    *   [3.3 WiFi (needs hacking)](#WiFi_.28needs_hacking.29)
    *   [3.4 Power and volume buttons](#Power_and_volume_buttons)
    *   [3.5 Sound card](#Sound_card)
    *   [3.6 Camera](#Camera)
    *   [3.7 Accelerometer](#Accelerometer)
    *   [3.8 Bluetooth](#Bluetooth)

## How to install

The tablet features the same uefi bios as a standard x86 pc, to enter it keep the "volume up" button pressed during boot, you should now be inside the bios, it can be navigated via touchscreen. Alternatively you can connect an USB keyboard through the otg adapter, press `CANC` and navigate normally with the cursor keys.

To boot from a specific uefi partition go to the last tab "Save & Exit" of the interface and select the partition inside the "Boot Override" section, you should be able to boot and do the installation normally from the live USB. Use an USB hub and a WiFi or Ethernet dongle to complete the installation.

Linux can be installed without issues on an external USB storage, or in the internal emmc, creating two additional partitions (boot and root) for Linux at the end of the internal memory was tested to be safe.

Systemd-boot seems to have issues, [GRUB](/index.php/GRUB "GRUB") works without problems.

A way to boot Linux automatically or from the graphical bootloader is yet to be discovered, the only known way is to go in the bios and manually boot each time.

## What works out of the box

*   Video output (see below)
*   Screen backlight slider (the one inside KDE at least)
*   USB OTG

With kernel 4.6 some crashes in the i915 driver were encountered, upgrading to Linux-git (4.7) solved the issue, this renders unusable any form of graphical installation based on older kernels (an issue for other distributions)

## What does not work

### Power management

No, battery level and charge state is totally absent

Probably related bug reports:

[https://bugs.launchpad.net/ubuntu/+bug/1569995](https://bugs.launchpad.net/ubuntu/+bug/1569995)

[https://bugzilla.redhat.com/show_bug.cgi?id=1337627](https://bugzilla.redhat.com/show_bug.cgi?id=1337627)

### Touchscreen (needs hacking, works)

The touchscreen does not work out of the box, but it can be made to work with the following driver:

[https://github.com/sigboe/gslX68X](https://github.com/sigboe/gslX68X) (follow the links for instructions on how to handle the firmware)

You can get the firmware by executing this command, it just downloads it as a base64 string from a temporarily link:

```
$ wget -qO- [https://gist.githubusercontent.com/Keziolio/caed197e8cff640b00e766aa55c7bea6/raw/104dde63bae574acf8143a7080bd7c95629e02df/firmware.base64](https://gist.githubusercontent.com/Keziolio/caed197e8cff640b00e766aa55c7bea6/raw/104dde63bae574acf8143a7080bd7c95629e02df/firmware.base64) | base64 -d > firm.fw

```

The touchscreen will not be precise, [touchscreen calibration](/index.php/Touchscreen#Calibration "Touchscreen") is needed to get proper functionality. After the calibration it should work without major issues.

### WiFi (needs hacking)

No, the device is "Realtek RTL8723BS Wireless LAN 802.11n SDIO Network Adapter", this is a potential working driver:

[https://github.com/hadess/rtl8723bs](https://github.com/hadess/rtl8723bs)

But it needs some kernel patches applied, it has yet to be tested.

### Power and volume buttons

No, totally unresponsive, more research is needed

### Sound card

No, the device name may be "es8316"

### Camera

Unknown, the device name may be "Unicam ov2680"

### Accelerometer

Unknown, the device name is "Kionix KXCJ9 3-axis accelerometer SPB"

### Bluetooth

Unknown