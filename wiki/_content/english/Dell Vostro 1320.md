This page is about setting up Arch Linux on the Dell Vostro 1320 laptop, which has replaced the former [Dell Vostro 1310](/index.php/Dell_Vostro_1310 "Dell Vostro 1310"). Basically it runs just fine, although there are some things you should know. Furthermore is is advisable to read the article about [laptops](/index.php/Laptop "Laptop") to get a idea about the topic in general.

## Contents

*   [1 Installation](#Installation)
*   [2 Hardware](#Hardware)
    *   [2.1 Overview](#Overview)
    *   [2.2 CPU](#CPU)
    *   [2.3 Graphics](#Graphics)
        *   [2.3.1 NVIDIA® GeForce™ 9300M GS](#NVIDIA.C2.AE_GeForce.E2.84.A2_9300M_GS)
        *   [2.3.2 GMA X4500 HD](#GMA_X4500_HD)
    *   [2.4 Multimedia](#Multimedia)
        *   [2.4.1 Audio](#Audio)
        *   [2.4.2 Webcam](#Webcam)
        *   [2.4.3 Biometric Fingerprint Reader](#Biometric_Fingerprint_Reader)
        *   [2.4.4 Extra Keyboard Keys](#Extra_Keyboard_Keys)
        *   [2.4.5 Card Reader](#Card_Reader)
    *   [2.5 Wireless](#Wireless)
    *   [2.6 Bluetooth](#Bluetooth)
        *   [2.6.1 Dell™ Wireless 355 Bluetooth® Module ROW](#Dell.E2.84.A2_Wireless_355_Bluetooth.C2.AE_Module_ROW)
*   [3 Issues](#Issues)
    *   [3.1 Framebuffer](#Framebuffer)
    *   [3.2 Card Reader](#Card_Reader_2)

# Installation

It is highly recommendable to setup Windows Vista first, because during the setup the region code of the dvd drive is set.

If you want to install Arch Linux over a wireless connection you have to setup the connection [manually](/index.php/Wireless_network_configuration#Manual_setup "Wireless network configuration"). Since kernel 2.6.24 and above are containing the appropriate drivers already, it should work with both the "Netinstall ISO" as well as the "Core ISO", although using the "Netinstall ISO" is the preferred install media for Arch Linux. Don't forget to choose the source "net" and the wlan interface (normally wlan0).

Apart from that you can follow the [Installation guide](/index.php/Installation_guide "Installation guide"), which should deliver you a good insight how to install Arch Linux.

Further attention has to be drawn during the partitioning, as Dell uses an uncommon partition table, which may you run into some trouble. You'll get a "FATAL ERROR", whenever you try to partition "/dev/sda" using the setup. Therefore switch to another terminal (Ctrl + Alt + F2, for instance) and delete the partition table using "fdisk /dev/sda". Follow the program options. More instructions can be found in the man page or the help option (m). It is sufficient to delete all partitions (and writing the table to the disc), from there on you can use the setup in the first terminal again (Ctrl + Alt + F1).

**Note:** When you remove *all* partitions the Dell Utility won't work anymore, so consider to leave the first partition, which contains the utility program. However the partition can be [recreated](http://www.goodells.net/dellutility/recreate.htm). You can also run the diagnostic utility from an usb stick or a cd.

# Hardware

This section is about getting the hardware of the Dell Vostro 1320 running properly. Generally speaking the hardware is supported just great, but due to the possibility of customisation (from Dell) not all of the components have been tested (yet).

## Overview

A quick overview which components do work correctly, and which don't. Look at the appropriate section in order to get more details about a component.

| **Dell Vostro 1320 - Overview of the hardware support** |
| ***Graphics*** |
| [NVIDIA® GeForce™ 9300M GS Graphic Card](#NVIDIA.C2.AE_GeForce.E2.84.A2_9300M_GS) | **working** |
| [Integrated GMA X4500 HD Graphics](#GMA_X4500_HD) | *untested* |
| ***Multimedia*** |
| Audio | **working** |
| [Webcam](#Webcam) | **working** |
| Biometric Fingerprint Reader | *untested* |
| Extra Keyboard Keys | *working* |
| [Card Reader](#Card_Reader) | *working* |
| ***Wireless LAN*** |
| [Dell Wireless 1397 Mini-Card (802.11 b/g)](#Dell_Wireless_1397_Mini-Card) | *reported working* |
| [Dell Wireless 1510 Mini-Card (802.11n)](#Dell_Wireless_1510_Mini-Card) | *reported working* |
| [Intel Pro Wireless Wi-Fi 5100 (802.11a/g/Draft-n)](#Intel_Pro_Wireless_Wi-Fi_5100) | **working** |
| [Intel WiFi Link 5300 Mini-Card (802.11 a/g/n)](#Intel_WiFi_Link_5300_Mini-Card) | **working** |
| ***Bluetooth*** |
| [Dell™ Wireless 355 Bluetooth® Module ROW](#Dell.E2.84.A2_Wireless_355_Bluetooth.C2.AE_Module_ROW) | *working* |

## CPU

As all of the available configurations are using a [Intel® Core™2 Duo](http://www.intel.com/cd/products/services/emea/deu/processors/core2duo/423591.htm) processor all of them should work just fine. Nevertheless you should take a look at the [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") article.

## Graphics

### NVIDIA® GeForce™ 9300M GS

Setting up the NVIDIA® GeForce™ 9300M GS graphic card is quite easy.

### GMA X4500 HD

Setting up the Integrated GMA X4500 HD graphics wasn't tested yet, but as it works fine for various other devices it should work just fine.

## Multimedia

### Audio

The audio works just fine out of the box using [ALSA](/index.php/ALSA "ALSA"). You need to have the "snd_hda_intel" module loaded, it is advisable to put it into your modules array in your /etc/rc.conf:

```
MODULES=(snd_hda_intel)

```

**Note:** There is just a mono built-in speaker , so do not wonder when you can't balance the channel properly.

### Webcam

The webcam works just fine out-of-the-box. If you have the automatic module loading disabled you have to load the module "uvcvideo".

### Biometric Fingerprint Reader

The Biometric Fingerprint Reader itself wasn't tested yet, but it should work following [these](/index.php/Dell_XPS_M1330#Fingerprint_reader "Dell XPS M1330") steps.

### Extra Keyboard Keys

Works, using keytouchd. Have a look at [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")

### Card Reader

Works out of the box, using the modules: mmc_block, mmc_core and sdhci

## Wireless

See [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

## Bluetooth

### Dell™ Wireless 355 Bluetooth® Module ROW

If your Vostro comes with Windows Vista installed (most of all), you need to update the bluetooth driver in Windows Vista. Among other things, the driver changes the firmware of the module. Only after that bluetooth will work under linux.

# Issues

## Framebuffer

You may experience some problems using the X server and console simultaneously, as soon as you work with different resolutions. In order to change the resolution of the console (using framebuffer) you should look at [Framebuffer#Framebuffer Resolution](/index.php/Framebuffer#Framebuffer_Resolution "Framebuffer"). For me adding "vga=0x0361" to the /boot/grub/menu.lst worked.

## Card Reader

It can be that some cards are not readable and you get the dmesg

```
[    8.790027] mmc0: error -110 whilst initialising SD card
[    8.790764] sdhci-pci 0000:1a:00.1: Will use DMA mode even though HW doesn't fully claim to support it.

```

This problem is easy to solve.Just add this line to your modprobe.conf

```
options sdhci debug_quirks=0x40

```

This will disable ADMA.