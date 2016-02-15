This article is intended specifically for Macbook(4,2) (late September 2008) model. If you have other Macbook model, please see [here](/index.php/MacBook "MacBook").

## Contents

*   [1 The Model](#The_Model)
*   [2 Installation](#Installation)
    *   [2.1 Preliminaries](#Preliminaries)
        *   [2.1.1 Back up your data](#Back_up_your_data)
        *   [2.1.2 Install rEFIt](#Install_rEFIt)
        *   [2.1.3 Note for single-boot](#Note_for_single-boot)
    *   [2.2 Partitioning](#Partitioning)
        *   [2.2.1 Single-boot (Arch Linux Only)](#Single-boot_.28Arch_Linux_Only.29)
        *   [2.2.2 Dual-boot (Arch Linux + OS-X)](#Dual-boot_.28Arch_Linux_.2B_OS-X.29)
        *   [2.2.3 Triple-boot (Arch Linux + Windows + OS-X)](#Triple-boot_.28Arch_Linux_.2B_Windows_.2B_OS-X.29)
    *   [2.3 Install Arch Linux](#Install_Arch_Linux)
*   [3 System Configuration](#System_Configuration)
    *   [3.1 Xorg Setup](#Xorg_Setup)
        *   [3.1.1 Video](#Video)
        *   [3.1.2 Touchpad](#Touchpad)
        *   [3.1.3 Keyboard](#Keyboard)
    *   [3.2 Wireless Setup](#Wireless_Setup)

## The Model

To make sure that you have the right model, here is the list of system specifications for Macbook(4,2) [[1]](http://en.wikipedia.org/wiki/Macbook)

*   **Release Date**: October 14, 2008
*   **Model Numbers**: MB402*/B
*   **Display**: 13.3-inch glossy widescreen LCD, 1280 x 800 pixel resolution (WXGA, 16:10 = 8:5 aspect ratio)
*   **Front Side Bus**: 800 MHz
*   **CPU**: 2.1 GHz Intel Core 2 Duo (T8100)
*   **Memory**: 1 GB (two 512 MB) 667 MHz PC2-5300 - Expandable to 4 GB
*   **Graphics**: Intel GMA X3100 using 144 MB RAM
*   **Hard Drive**: 120 GB - Optional 160 GB or 250 GB
*   **Wireless**: Integrated 802.11a/b/g/n (Broadcom BCM4328 rev03)
*   **Slot Drive**: 4× DVD+R DL writes, 8× DVD±R read, 4× DVD±RW writes, 24× CD-R, and 10x CD-RW recording
*   **Included OS**: Mac OS X v10.5.4
*   **Battery**: 55-watt-hour removable lithium-polymer

## Installation

**Incomplete - Work in Progress**

### Preliminaries

#### Back up your data

You should backup before you begin the installation. It suffices to just backup the Users directory (/Users/_user_/ where _user_ is the name of the username in OSX) onto external hard drive or USB stick.

#### Install rEFIt

Before you begin, you should install [rEFIt](http://refit.sourceforge.net), the bootloader for EFI-based computer, such as the Intel Macbooks.

1.  Download the .dmg
2.  Install the program
3.  run:

```
cd /efi/refit; ./enable.sh

```

#### Note for single-boot

However, if you are going to erase OS-X and plan on single-boot, then you need to also back up

```
/System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns/AppleUSBVideoSupport.kext/Contents/MacOS/AppleUSBVideoSupport

```

You will need this for iSight functionality

### Partitioning

**TODO**

##### Single-boot (Arch Linux Only)

##### Dual-boot (Arch Linux + OS-X)

##### Triple-boot (Arch Linux + Windows + OS-X)

### Install Arch Linux

**TODO**

## System Configuration

**TODO**

### Xorg Setup

#### Video

#### Touchpad

#### Keyboard

### Wireless Setup

This model of Macbook has Broadcom BCM4328(rev03). There are two methods: (a) using [ndiswrapper](/index.php/Ndiswrapper "Ndiswrapper") or (b) using [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)

See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") for more information.