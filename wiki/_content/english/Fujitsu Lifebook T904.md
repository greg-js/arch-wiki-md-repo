## Contents

*   [1 Troubleshooting](#Troubleshooting)
    *   [1.1 Wacom Digitizer (056a:5002)](#Wacom_Digitizer_.28056a:5002.29)
    *   [1.2 Fingerprint reader](#Fingerprint_reader)
    *   [1.3 Fan noise](#Fan_noise)
*   [2 Hardware modules](#Hardware_modules)
    *   [2.1 Wacom Digitizer](#Wacom_Digitizer)
        *   [2.1.1 X11 wacom input](#X11_wacom_input)
        *   [2.1.2 Wacom Kernel Module](#Wacom_Kernel_Module)

## Troubleshooting

### Wacom Digitizer (056a:5002)

Requires a custom module not currently avalable in the stock 3.14.4-1-ARCH kernel.

```
   See [Hardware Modules](#Wacom_Digitizer) for how to enable the digitizer

```

### Fingerprint reader

According to the [Fprint wiki](/index.php/Fprint "Fprint"), the reader does not appear to be a [supported model](http://www.freedesktop.org/wiki/Software/fprint/libfprint/Supported_devices/). If the reader is unused, it is recommended that the device be physically disabled in the bios.

### Fan noise

Fan noise was an issue on initial BIOS revisions. The change log for BIOS version 1.08 noted a fan settings update which has since resolved the fan noise issue.

User confirmations of the fix may be found after post #540 [[1]](http://forum.tabletpcreview.com/fujitsu/61570-official-t904-thread-54.html#post391747)

## Hardware modules

### Wacom Digitizer

The wacom kernel module (wacom.ko) loaded by default in the 3.14.4-1-ARCH kernel does not support the T904's integrated digitizer 056A:5002 (VendorID:DeviceID). However, the [Linuxwacom project](http://sourceforge.net/apps/mediawiki/linuxwacom/index.php?title=Linuxwacom) has included support in their upstream kernel module and xf86-input-wacom-git package which are not yet available in the official arch repositories.

Until future updates are released, users may obtain a functional digitizer by installing *xf86-input-wacom-git* and building the kernel module as described below:

#### X11 wacom input

Install *xf86-input-wacom-git* via [building from source](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") or using an [AUR helper](/index.php/AUR_helper "AUR helper"))

#### Wacom Kernel Module

The non-functional default wacom kernel module (wacom.ko) is located in /lib/modules/*3.14.-4-1-ARCH*/kernel/drivers/input/tablet/wacom.ko This module must be replaced with the latest [Linuxwacom](http://sourceforge.net/apps/mediawiki/linuxwacom/index.php?title=Linuxwacom) project module as follows:

First, ensure that *git* and *linux-headers* are installed:

```
# pacman -S git linux-headers

```

Create a new directory to build the wacom.ko module in:

```
$ mkdir ~/builds
$ cd ~/builds

```

Download the latest module source from the Linuxwacom project:

```
git clone [git://git.code.sf.net/p/linuxwacom/input-wacom](git://git.code.sf.net/p/linuxwacom/input-wacom)

```

Build the module with autogen.sh:

```
# bash ~/builds/input-wacom/autogen.sh

```

As described in the autogen.sh output, copy the module to the appropriate directory:

```
# cp ~/builds/input-wacom/3.7/wacom.ko /lib/modules/3.14.4-1-ARCH/kernel/drivers/input/tablet

```

In case the old wacom module was previously loaded, ensure it is removed:

```
# rmmod wacom.ko

```

Insert the new module:

```
# insmod ~/builds/input-wacom/3.7/wacom.ko

```

Ensure modprobe has the correct aliases:

```
# depmod -a

```

**Note:** A reboot will likely be required for functional xorg touch/pen input.