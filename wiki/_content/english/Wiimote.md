This article will go through the basic steps required to have a working Wiimote in Linux for general use. It will not go into much detail for some steps as there are many guides already written for some parts already.

**Note:** The approach shown on this page is based on software which is no longer developed upstream. There is a new effort on creating a Wii Remote driver based on the new Linux kernel Wii Remote driver. See [XWiimote](/index.php/XWiimote "XWiimote") if you want to test the new Wii Remote software stack.

## Contents

*   [1 Prerequisites](#Prerequisites)
*   [2 Connect the Wiimote](#Connect_the_Wiimote)
*   [3 Input Device](#Input_Device)
    *   [3.1 Infrared Sources](#Infrared_Sources)
    *   [3.2 Configuration](#Configuration)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Unable to open uinput](#Unable_to_open_uinput)
*   [5 See also](#See_also)

## Prerequisites

*   Bluetooth
*   [cwiid](https://www.archlinux.org/packages/?name=cwiid)
*   Wiimote

The most important piece required is [Bluetooth](/index.php/Bluetooth "Bluetooth"), this must already be configured and running without the help of this guide. This should be simple enough with any guide found on the internet. The 'cwiid' package is in [Community](/index.php/Community "Community"). This package contains all libraries and programs required for basic use of the Wiimote. Lastly you will need a Wiimote, this can include (although are not required) the Nunchuk and Classic Control attachments.

## Connect the Wiimote

First you need to make sure to load the `uinput` module:

```
# modprobe uinput

```

You should have a device in `/dev/uinput` now. For permanent use you can add it to the modules section in your [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf").

Thanks to cwiid you can scan for your Wiimote now:

```
(press the 1 and 2 buttons on your Wiimote)
$ hcitool scan
Scanning ...
       <MAC address>       Nintendo RVL-CNT-01

```

Once your Wiimote has been detected you can test if it is working by running the command `wmgui` and testing out various buttons and sensors through that interface.

## Input Device

The Wiimote can act as a regular input device like a mouse using `wminput`. If you have *no infrared source* simply run:

```
$ wminput -w

```

You can control your pointer now by tilting your Wiimote forward, backward or to the sides.

If you *have an infrared source* run:

```
$ wminput -c ir_ptr -w

```

### Infrared Sources

Possible infrared sources are bulbs

*   Nintendo Wii Sensor Bar
*   Wireless sensor bar - check eBay!
*   Normal light bulbs
*   Small candles (should have about 30cm distance)
*   Home made sensor bar ([[1]](http://doctabu.livejournal.com/64758.html))

### Configuration

The default configuration files are in `/etc/cwiid/wminput/`. They are a good starting point for your customized settings in `~/.cwiid/wminput` or `/usr/local/etc/cwiid/wminput`. The general syntax is:

```
Wiimote.Button = KEY_ON_KEYBOARD

```

All possible values for Wiimote.Buttons can be found here: [[2]](http://abstrakraft.org/cwiid/browser/doc/wminput.list), the possible values for KEY_ON_KEYBOARD in `/usr/include/linux/input-event-codes.h`.

## Troubleshooting

### Unable to open uinput

If wminput gives this error, leaving you unable to use the wiimote, try the following:

1\. Create a new file in `/etc/udev/rules.d/` (It does not matter what the name of the file is, so long as the extension is .rules)

2\. Add the following to the file:

```
KERNEL=="uinput", GROUP="wheel", MODE="0660"

```

3\. Reboot

This should solve the problem. Solution was found in the forums [here](https://bbs.archlinux.org/viewtopic.php?id=104348).

Solution 2:

1\. edit the `/etc/mkinitcpio.conf` add "uinput" in MODULES:

```
MODULES="uinput ...."

```

2\. as needed and re-generate the initramfs image with:

```
# mkinitcpio -p linux

```

3\. Reboot

## See also

*   [XWiimote](/index.php/XWiimote "XWiimote")