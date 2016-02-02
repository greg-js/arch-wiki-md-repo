# ChipKit

[ChipKit](http://chipkit.net/started-mplab-ide/) is a Microprocessor platform produced by Digilent Inc. which provides an [Arduino](/index.php/Arduino "Arduino") like environment and a physically compatible board, but runs the much quicker and more powerful PIC32 series of Processors.

There are two boards, the Uno32 which has 128k of Flash and 16k of RAM, and the Max32 which has 512k of Flash and 128k of RAM. Both boards run at 80Mhz. Prices are $27 and $50 respectively, so comparable with standard and advanced Arduinos.

This install was for a 64-bit machine and an Uno32\. I do not have a Max32 or a 32-bit machine, but the process should be identical for the hardware change, and simpler for the software change. However, the 32 bit install has not been verified.

At the time of installation I was running Java 7 and Kernel 3.0.1

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Requirements (all architectures)](#Requirements_.28all_architectures.29)
        *   [1.1.1 Requirements (32 bit versions)](#Requirements_.2832_bit_versions.29)
        *   [1.1.2 Requirements (64 bit versions)](#Requirements_.2864_bit_versions.29)
    *   [1.2 Software Install](#Software_Install)
*   [2 Running the IDE](#Running_the_IDE)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 Links](#Links)

## Installation

### Requirements (all architectures)

Install rxtx from the [AUR](/index.php/AUR "AUR").

At the time of writing, it is necessary to edit the PKGBUILD which refers to kernel26-headers so it refers to linux-headers.

Install binutils-avr from the repositories.

This is required only because the ChipKit software needs the program avr-size. It comes with the rest of its own software. If you use [Arduino](/index.php/Arduino "Arduino") on Arch you will know there is a nasty bug which means the current gcc-avr and binutils-avr do not work correctly. In that case do not install the new binutils-avr but use these PKGBUILDs [here](http://www.cyquiz.com/arduino-packagebuilds.tar.gz) (untar them in /var/abs/local) which produce versions that do work correctly. You will need to add gcc-avr and binutils-avr to IgnorePkg = in /etc/pacman.conf to stop pacman upgrading them.

#### Requirements (32 bit versions)

libusb and libusb-compat are required, but may well be installed by default.

#### Requirements (64 bit versions)

For mpide to communicate with the microprocessor board via USB, install the required USB packages.

```
$ sudo pacman -S libusb-compat libusbx

```

The following packages are required by `mpide`:

```
$ sudo pacman -S java-rxtx avrdude avr-binutils avr-gcc avr-gdb avr-lib

```

### Software Install

Download the current Linux install from [here](https://github.com/chipKIT32/chipKIT32-MAX/downloads). This was tested using file mpide-0022-chipkit-linux32-20110619.tgz

Untar the file in an appropriate location, I was using /aux. Note the use of the 'p' to preserve the flags for the file.

```
cd /aux
tar xzvfp mpide-0022-chipkit-linux32-20110619.tgz

```

## Running the IDE

You can run the ChipKit environment by changing to that directory and running mpide

```
cd /aux/mpide-0022-chipkit-linux32-20110619
./mpide

```

This brings up the familiar Arduino IDE. You can set the Board Type to Uno32 or Max32 as you would when selecting a different Arduino board. The simplest way to test it is by using Example Blinky and changing the delay times so the LED is on for only 200ms (for example).

## Troubleshooting

```
Exception in thread "main" java.lang.NoClassDefFoundError: gnu/io/CommPortIdentifier

```

MPIDE ships only with a 64 bit version of librxtxSerial.so, if you're on 32 bit, copy the librxtxSerial.so from the official arduino IDE into your lib/ folder, or obtain it from the rxtx website. Do not use the rxtx AUR packages, they are all utterly broken (require kernel 2.6) and even if you get them to work, mpide will not find the .so files installed by them.

## Links

*   [Uno32 page at Digilent](http://www.digilentinc.com/Products/Detail.cfm?NavPath=2,719,896&Prod=CHIPKIT-UNO32)
*   [Max32 page at Digilent](http://www.digilentinc.com/Products/Detail.cfm?NavPath=2,719,895&Prod=CHIPKIT-MAX32)

Retrieved from "[https://wiki.archlinux.org/index.php?title=ChipKit&oldid=325954](https://wiki.archlinux.org/index.php?title=ChipKit&oldid=325954)"