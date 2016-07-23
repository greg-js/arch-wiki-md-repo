The tablet can run the x86_64 version of Archlinux, but at the time of writing this page, hardware support is **terrible**, pretty much nothing works out of the box.

## Contents

*   [1 How to install](#How_to_install)
*   [2 What works out of the box](#What_works_out_of_the_box)
*   [3 What doesn't work](#What_doesn.27t_work)
    *   [3.1 Power management](#Power_management)
    *   [3.2 Touchscreen (needs hacking, works)](#Touchscreen_.28needs_hacking.2C_works.29)
    *   [3.3 Wifi (needs hacking)](#Wifi_.28needs_hacking.29)
    *   [3.4 Power and volume buttons](#Power_and_volume_buttons)
    *   [3.5 Sound card](#Sound_card)
    *   [3.6 Camera](#Camera)
    *   [3.7 Accelerometer](#Accelerometer)
    *   [3.8 Bluetooth](#Bluetooth)

## How to install

The tablet features the same uefi bios as a "standard" x86 pc, to enter it hook an USB keyboard through the OTG port and press "Canc" during boot, you should now be inside the bios.

To boot from a specific uefi partition go to the last page of the bios and select the partition inside the "boot override" section, you should be able to boot and do the installation normally from the live usb. Use an usb hub and a wifi or ethernet dongle to complete the installation.

Linux can be installed without issues on an external usb storage, or in the internal emmc, creating two partitions (boot and root) for Linux at the end of the internal drive was tested to be safe.

A way to boot Linux automatically or from the graphical bootloader is yet to be discovered, the only known way is to go in the bios and manually boot each time.

# What works out of the box

*   Video output (see below)
*   Screen backlight slider (the one inside kde at least)
*   USB OTG

With kernel 4.6 some crashes in the i915 driver were encountered, upgrading to linux-git (4.7 rc7) solved the issue, this renders unusable any form of graphical installation (an issue for other distros)

# What doesn't work

## Power management

No, battery level and charge state is totally absent

Probably related bug: [https://bugzilla.redhat.com/show_bug.cgi?id=1337627](https://bugzilla.redhat.com/show_bug.cgi?id=1337627)

## Touchscreen (needs hacking, works)

The touchscreen does not work out of the box, but it can be made to work with the following driver:

[https://github.com/sigboe/gslX68X](https://github.com/sigboe/gslX68X) (follow the links for instructions on how to handle the firmware)

I temporarily uploaded the firmware here, it's a base64 string

[https://gist.githubusercontent.com/Keziolio/caed197e8cff640b00e766aa55c7bea6/raw/104dde63bae574acf8143a7080bd7c95629e02df/firmware.base64](https://gist.githubusercontent.com/Keziolio/caed197e8cff640b00e766aa55c7bea6/raw/104dde63bae574acf8143a7080bd7c95629e02df/firmware.base64)

To get the firmware, execute this command:

```
$ wget -qO- [https://gist.githubusercontent.com/Keziolio/caed197e8cff640b00e766aa55c7bea6/raw/104dde63bae574acf8143a7080bd7c95629e02df/firmware.base64](https://gist.githubusercontent.com/Keziolio/caed197e8cff640b00e766aa55c7bea6/raw/104dde63bae574acf8143a7080bd7c95629e02df/firmware.base64) | base64 -d > firm.fw

```

The touchscreen will not be precise, touchscreen calibration is needed to get proper functionality. After the calibration it should work without major issues.

## Wifi (needs hacking)

No, not out of the box, the device is "Realtek RTL8723BS Wireless LAN 802.11n SDIO Network Adapter", this is a potential working driver:

[https://github.com/hadess/rtl8723bs](https://github.com/hadess/rtl8723bs)

But it needs some kernel patches applied, i have yet to get it to work, it's not tested.

## Power and volume buttons

No, totally unresponsive, more research is needed

## Sound card

No, the device name may be "es8316"

## Camera

No, the device name may be "Unicam ov2680"

## Accelerometer

Unknown, the device name is "Kionix KXCJ9 3-axis accelerometer SPB"

## Bluetooth

Unknown