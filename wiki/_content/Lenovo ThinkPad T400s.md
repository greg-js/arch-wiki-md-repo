# Lenovo ThinkPad T400s

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Lenovo ThinkPad T400](/index.php/Lenovo_ThinkPad_T400 "Lenovo ThinkPad T400")

Before reading, a good starting point for Arch Linux installation on notebooks is the main [laptop](/index.php/Laptop "Laptop") article.

The article describes the installation of Arch Linux on a ThinkPad T400s.

## Contents

*   [1 Hardware identification](#Hardware_identification)
    *   [1.1 2815-W3F](#2815-W3F)
        *   [1.1.1 PCI devices](#PCI_devices)
        *   [1.1.2 USB devices](#USB_devices)
    *   [1.2 2815RH1](#2815RH1)
        *   [1.2.1 CPU architecture](#CPU_architecture)
        *   [1.2.2 PCI devices](#PCI_devices_2)
        *   [1.2.3 USB devices](#USB_devices_2)
*   [2 Hardware configuration](#Hardware_configuration)
    *   [2.1 Graphics](#Graphics)
    *   [2.2 Input devices](#Input_devices)
        *   [2.2.1 Touchpad](#Touchpad)
        *   [2.2.2 TrackPoint](#TrackPoint)
    *   [2.3 Network](#Network)
        *   [2.3.1 Bluetooth](#Bluetooth)
        *   [2.3.2 Ethernet](#Ethernet)
        *   [2.3.3 UMTS](#UMTS)
            *   [2.3.3.1 Activate the UMTS device](#Activate_the_UMTS_device)
            *   [2.3.3.2 Restrict communication to GSM](#Restrict_communication_to_GSM)
            *   [2.3.3.3 Restrict communication to WCDMA](#Restrict_communication_to_WCDMA)
            *   [2.3.3.4 Deactivate the UMTS card](#Deactivate_the_UMTS_card)
            *   [2.3.3.5 Setup the UMTS card as modem](#Setup_the_UMTS_card_as_modem)
                *   [2.3.3.5.1 Setup the UMTS card as GPRS modem](#Setup_the_UMTS_card_as_GPRS_modem)
                *   [2.3.3.5.2 Setup the UMTS card as CDC ethernet interface](#Setup_the_UMTS_card_as_CDC_ethernet_interface)
            *   [2.3.3.6 Setup the UMTS card as GPS receiver](#Setup_the_UMTS_card_as_GPS_receiver)
        *   [2.3.4 Wireless](#Wireless)
    *   [2.4 Web camera](#Web_camera)
    *   [2.5 Sound](#Sound)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 9 seconds reboot delay](#9_seconds_reboot_delay)
*   [4 See also](#See_also)
    *   [4.1 General](#General)
    *   [4.2 References](#References)
    *   [4.3 Linux on a ThinkPad T400s](#Linux_on_a_ThinkPad_T400s)
    *   [4.4 Reviews](#Reviews)

## Hardware identification

To idenitfy your model, see `/sys/class/dmi/id/product_name`

### 2815-W3F

*   Model: Lenovo T400s 2815-W3F
*   Processor: Intel® Core™ 2 Duo SP9400 (2.40 GHz), 1066 MHz Front Side Bus, 6 MB-L2-Cache
*   Chipset: ?
*   Memory: PC3-8500 DDR3-SDRAM 1066 MHz, 1x2 GB (8 GB maximum)
*   Harddrive: 250 GB, 1.8", SATA interface
*   Screen: 14.1" WSXGA LED backlight, maximum 1440 x 900 bp
*   Graphic: Intel Graphics Media Accelerator X4500MHD, up to 384 MB
*   Optical drive: DVD-RAM/RW drive
*   Bluetooth: ThinkPad Bluetooth with Enhanced Data Rate (BDC-2) v.2.0+EDR
*   Network: Intel 82567LM Ethernet adapter (10/100/1000 Mbps)
*   WiFi: Intel Wireless 5300 a/g/n
*   USB ports: 2 + 1 combined eSATA/USB port
*   Webcam: Yes
*   Fingerprintr.: Yes
*   Battery: Lithium Ion in 6 cell (~3 hours)
*   Dimensions: 337 (width) x 241 (dept) x 21.1-25.9 (height) mm
*   Weight: 1.77 kg

#### PCI devices

 `lspci` 

```
00:00.0 Host bridge: Intel Corporation Mobile 4 Series Chipset Memory Controller Hub (rev 07)
00:02.0 VGA compatible controller: Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller (rev 07)
00:02.1 Display controller: Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller (rev 07)
00:03.0 Communication controller: Intel Corporation Mobile 4 Series Chipset MEI Controller (rev 07)
00:03.3 Serial controller: Intel Corporation Mobile 4 Series Chipset AMT SOL Redirection (rev 07)
00:19.0 Ethernet controller: Intel Corporation 82567LM Gigabit Network Connection (rev 03)
00:1a.0 USB Controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #4 (rev 03)
00:1a.1 USB Controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #5 (rev 03)
00:1a.2 USB Controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #6 (rev 03)
00:1a.7 USB Controller: Intel Corporation 82801I (ICH9 Family) USB2 EHCI Controller #2 (rev 03)
00:1b.0 Audio device: Intel Corporation 82801I (ICH9 Family) HD Audio Controller (rev 03)
00:1c.0 PCI bridge: Intel Corporation 82801I (ICH9 Family) PCI Express Port 1 (rev 03)
00:1c.1 PCI bridge: Intel Corporation 82801I (ICH9 Family) PCI Express Port 2 (rev 03)
00:1c.3 PCI bridge: Intel Corporation 82801I (ICH9 Family) PCI Express Port 4 (rev 03)
00:1d.0 USB Controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #1 (rev 03)
00:1d.1 USB Controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #2 (rev 03)
00:1d.2 USB Controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #3 (rev 03)
00:1d.7 USB Controller: Intel Corporation 82801I (ICH9 Family) USB2 EHCI Controller #1 (rev 03)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev 93)
00:1f.0 ISA bridge: Intel Corporation ICH9M-E LPC Interface Controller (rev 03)
00:1f.2 SATA controller: Intel Corporation ICH9M/M-E SATA AHCI Controller (rev 03)
00:1f.3 SMBus: Intel Corporation 82801I (ICH9 Family) SMBus Controller (rev 03)
03:00.0 Network controller: Intel Corporation Wireless WiFi Link 5300
05:00.0 SD Host controller: Ricoh Co Ltd Device e822 (rev 01)
05:00.1 System peripheral: Ricoh Co Ltd Device e230 (rev 01)

```

#### USB devices

 `lsusb` 

```
Bus 006 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 007 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 008 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 003: ID 0a5c:2145 Broadcom Corp. 
Bus 004 Device 002: ID 147e:2016 Upek Biometric Touchchip/Touchstrip Fingerprint Sensor
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 002 Device 002: ID 0bdb:1900 Ericsson Business Mobile Networks BV 
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 004: ID 17ef:480d Lenovo 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### 2815RH1

#### CPU architecture

 `lscpu` 

```
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                2
On-line CPU(s) list:   0,1
Thread(s) per core:    1
Core(s) per socket:    2
Socket(s):             1
NUMA node(s):          1
Vendor ID:             GenuineIntel
CPU family:            6
Model:                 23
Stepping:              10
CPU MHz:               2401.000
BogoMIPS:              4789.47
Virtualization:        VT-x
L1d cache:             32K
L1i cache:             32K
L2 cache:              6144K
NUMA node0 CPU(s):     0,1

```

#### PCI devices

 `lspci` 

```
00:00.0 Host bridge: Intel Corporation Mobile 4 Series Chipset Memory Controller Hub (rev 07)
00:02.0 VGA compatible controller: Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller (rev 07)
00:02.1 Display controller: Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller (rev 07)
00:03.0 Communication controller: Intel Corporation Mobile 4 Series Chipset MEI Controller (rev 07)
00:03.3 Serial controller: Intel Corporation Mobile 4 Series Chipset AMT SOL Redirection (rev 07)
00:19.0 Ethernet controller: Intel Corporation 82567LM Gigabit Network Connection (rev 03)
00:1a.0 USB controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #4 (rev 03)
00:1a.1 USB controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #5 (rev 03)
00:1a.2 USB controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #6 (rev 03)
00:1a.7 USB controller: Intel Corporation 82801I (ICH9 Family) USB2 EHCI Controller #2 (rev 03)
00:1b.0 Audio device: Intel Corporation 82801I (ICH9 Family) HD Audio Controller (rev 03)
00:1c.0 PCI bridge: Intel Corporation 82801I (ICH9 Family) PCI Express Port 1 (rev 03)
00:1c.1 PCI bridge: Intel Corporation 82801I (ICH9 Family) PCI Express Port 2 (rev 03)
00:1c.3 PCI bridge: Intel Corporation 82801I (ICH9 Family) PCI Express Port 4 (rev 03)
00:1d.0 USB controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #1 (rev 03)
00:1d.1 USB controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #2 (rev 03)
00:1d.2 USB controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #3 (rev 03)
00:1d.7 USB controller: Intel Corporation 82801I (ICH9 Family) USB2 EHCI Controller #1 (rev 03)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev 93)
00:1f.0 ISA bridge: Intel Corporation ICH9M-E LPC Interface Controller (rev 03)
00:1f.2 SATA controller: Intel Corporation ICH9M/M-E SATA AHCI Controller (rev 03)
00:1f.3 SMBus: Intel Corporation 82801I (ICH9 Family) SMBus Controller (rev 03)
03:00.0 Network controller: Intel Corporation Centrino Wireless-N 1000
05:00.0 SD Host controller: Ricoh Co Ltd MMC/SD Host Controller (rev 01)
05:00.1 System peripheral: Ricoh Co Ltd Memory Stick Host Controller (rev 01)

```

#### USB devices

 `lsusb` 

```
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 006 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 007 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 008 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 004: ID 17ef:480d Lenovo Integrated Webcam [R5U877]
Bus 004 Device 002: ID 147e:2016 Upek Biometric Touchchip/Touchstrip Fingerprint Sensor
Bus 004 Device 003: ID 0a5c:2145 Broadcom Corp. Bluetooth with Enhanced Data Rate II

```

## Hardware configuration

### Graphics

See [Intel graphics](/index.php/Intel_graphics "Intel graphics").

### Input devices

#### Touchpad

Touchpad is SynPS/2 Synaptics TouchPad. `evdev` input driver provides basic functionality, but for tapping, scrolling and other advanced functions [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) should be installed.

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

#### TrackPoint

See [TrackPoint](/index.php/TrackPoint "TrackPoint").

### Network

#### Bluetooth

See [Bluetooth](/index.php/Bluetooth "Bluetooth").

#### Ethernet

Ethernet controller is identified as `00:19.0 Ethernet controller: Intel Corporation 82567LM Gigabit Network Connection (rev 03)` and works out of the box. The corresponding [kernel module](/index.php/Kernel_module "Kernel module") is `e1000e`.

#### UMTS

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Lenovo ThinkPad T400s#](https://wiki.archlinux.org/index.php/Talk:Lenovo_ThinkPad_T400s))

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [[]].**

**Notes:** Out of scope, move to a page in [Category:Modems](/index.php/Category:Modems "Category:Modems")? (Discuss in [Talk:Lenovo ThinkPad T400s#](https://wiki.archlinux.org/index.php/Talk:Lenovo_ThinkPad_T400s))

The UMTS device is a Ericsson F3507g MiniPCIe WWAN/GPS card. The vendor identifier is 0bdb, while the device identifier is 1900 (both values are hexadecimal values). You can get more information about the card by using lsusb/usbview. In order to use the UTMS modem you will have to activate the device. You can edit and verify the settings of your UMTS modem by using minicom or another terminal emulation program like [picocom](http://code.google.com/p/picocom/) or [dterm](http://www.knossos.net.nz/dterm.html). I've used [tinycom](http://brokestream.com/tinyserial.html) which is inspired by the well known FreeBSD program 'tips'.

##### Activate the UMTS device

Open a connection to the device:

```
# ./com /dev/ttyACM1 [115200]

```

Check whenever the SIM is protected by PIN by sending

```
AT+CPIN?

```

If the answer is:

```
+CPIN: SIM PIN

```

you will have to unlock the device with your PIN:

```
AT+CPIN="YOUR-PIN-NUMBER"

```

The device can be activated now by sending:

```
AT+CFUN=1

```

The answer of the device should be:

```
+PACSP0

```

##### Restrict communication to GSM

Normally you do not want to restrict your communication to GSM only. If desired, you can send:

```
AT+CFUN=5

```

##### Restrict communication to WCDMA

As before, it is unusual to restrict your communication to WCDMA only. Type:

```
AT+CFUN=6

```

##### Deactivate the UMTS card

You can deactivate the card by typing

```
AT+CFUN=4

```

and if you want to remove all power from the card, type:

```
AT+CFUN=0

```

##### Setup the UMTS card as modem

There are two ways to use the UMTS card as modem. The first one just uses the card as GPRS modem, the second one uses the card as CDC ethernet interface.

###### Setup the UMTS card as GPRS modem

The GPRS modem settings are configured by [wvdial](http://alumnit.ca/wiki/index.php?page=WvDial). Please note that there are provider specific namings for access point names (APN). You can find an appropriate APN over [here](http://forums.pinstack.com/f24/tcp_apn_wap_gateway_and_port_carrier_settings-360/).

###### Setup the UMTS card as CDC ethernet interface

##### Setup the UMTS card as GPS receiver

While the UMTS card is activated, we can use it to get GPS info via NMEA protocol. In order to use the NMEA protocol, a few things have to be configured

```
AT*E2GPSCTL=X,Y,Z

```

The parameter x activates/deactivates the NMEA stream. Legal values are 0 (off) or 1 (on). The frequency how often the card emits the NMEA sentences is set by the Y parameter. Legal values are in a range between 1 upto 60\. The last parameter sets DGPS off or on. The value 0 turns it off, the value 1 turns it on. If you want to activate the NMEA stream and DPGS and to update the position every 42 seconds you would type the following:

```
AT*E2GPSCTL=1,42,1

```

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Lenovo ThinkPad T400s#](https://wiki.archlinux.org/index.php/Talk:Lenovo_ThinkPad_T400s))

#### Wireless

Both 'Intel Corporation Wireless WiFi Link 5300' (2815W3F) and 'Intel Corporation Centrino Wireless-N 1000' (2815RH1) adapters are supported by [iwlwifi](http://intellinuxwireless.org).

See [Wireless network configuration#iwlwifi](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration").

### Web camera

Web camera (USB ID `17ef:480d`, Lenovo Integrated Webcam [R5U877]) works out of the box. It is supported by `uvcvideo` [kernel module](/index.php/Kernel_module "Kernel module").

See [Webcam setup](/index.php/Webcam_setup "Webcam setup"), [Integrated camera](http://www.thinkwiki.org/wiki/Integrated_camera).

### Sound

Sound works out of the box. The corresponding kernel module is `snd-hda-intel`.

As of September 2010 the module must be loaded with the option `model=thinkpad` in order to get the earphones work:

 `/etc/modprobe.d/alsa-base.conf`  `options snd-hda-intel model=thinkpad` 

This is due to the update to kernel 2.6.35\. See [[1]](https://bbs.archlinux.org/viewtopic.php?pid=822626) and [[2]](http://groups.google.com/group/linux.kernel/browse_thread/thread/379459c155b31b20/f4c6ebddbdfc5806?show_docid=f4c6ebddbdfc5806). This also enables muting of the internal speakers when a speaker is attached to the **docking station**.

## Troubleshooting

### 9 seconds reboot delay

You may want to append `reboot=pci` to the kernel parameters list.

See:

*   [https://lkml.org/lkml/2010/6/7/83](https://lkml.org/lkml/2010/6/7/83)
*   [http://www.gossamer-threads.com/lists/linux/kernel/1250554](http://www.gossamer-threads.com/lists/linux/kernel/1250554)

## See also

### General

*   Lenovo [Hardware Maintenance Manual](http://download.lenovo.com/ibmdl/pub/pc/pccbbs/mobiles_pdf/45m2271.pdf) of the ThinkPad T400s
*   [EFI](http://www.engadget.com/2009/09/24/video-phoenix-instant-boot-bios-starts-loading-windows-in-under/3#comments) on a Lenovo ThinkPad T400s.

### References

*   [Hard Drive Active Protection System Installation Guide](/index.php/HDAPS "HDAPS")
*   General Arch Linux related [installation information on latops](/index.php/Laptop "Laptop")
*   [Thinkpad Fan Control Guide](/index.php/Thinkpad_Fan_Control "Thinkpad Fan Control")
*   [Thinkpad OSD Guide](/index.php/ThinkPad_OSD "ThinkPad OSD")
*   [Thinkpad Fingerprintreader Guide](/index.php/ThinkFinger "ThinkFinger")
*   [Thinkpad Smart API Guide](/index.php/Tp_smapi "Tp smapi")

### Linux on a ThinkPad T400s

There are a few installation guides for Linux on a Lenovo ThinkPad T400s.

*   [Ubuntu 9.10 (Karmic Koala)](http://www.thinkwiki.org/wiki/Install_Ubuntu_9.10_%28Karmic_Koala%29_on_a_ThinkPad_T400s)
*   [Debian 5.0.2](http://wiki.debianforum.de/LenovoThinkpadT400s)
*   [ArchLinux](http://www.2xlc.de/t400s.html)

### Reviews

*   English [review](http://hothardware.com/Articles/Lenovo-ThinkPad-T400s-Notebook-Review/) by [hothardware.com](http://hothardware.com/)
*   A german [review](http://www.notebookcheck.com/Test-Lenovo-ThinkPad-T400s-Notebook.20960.0.html) by [notebookcheck.com](http://www.notebookcheck.com/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T400s&oldid=412562](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T400s&oldid=412562)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")

Hidden categories:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")
*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")
*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")