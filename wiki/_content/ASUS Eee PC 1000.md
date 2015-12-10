# ASUS Eee PC 1000

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

For now, this is just some notes on the Asus EeePC 1000\. The difference between the 1000 and the 901 are more subtle than just the screen size.

For more information, see other pages:

*   [ASUS Eee PC 901](/index.php/ASUS_Eee_PC_901 "ASUS Eee PC 901")
*   [Installing Arch Linux on the Asus EEE PC](/index.php/Installing_Arch_Linux_on_the_Asus_EEE_PC "Installing Arch Linux on the Asus EEE PC")
*   [ASUS Eee PC](/index.php/ASUS_Eee_PC "ASUS Eee PC")
*   [Asus Eee PC 900A](/index.php/Asus_Eee_PC_900A "Asus Eee PC 900A")
*   [Array.org EeePC Ubuntu Repository](http://array.org/ubuntu/status.html)

## Contents

*   [1 Wireless](#Wireless)
*   [2 Xorg](#Xorg)
*   [3 Touchpad](#Touchpad)
*   [4 ACPI](#ACPI)
    *   [4.1 Notes](#Notes)
        *   [4.1.1 Sleep](#Sleep)
        *   [4.1.2 Wifi](#Wifi)
        *   [4.1.3 Brightness](#Brightness)
*   [5 Hardware](#Hardware)
    *   [5.1 lspci](#lspci)
    *   [5.2 lsusb](#lsusb)

## Wireless

The card is a RaLink RT2860\. The driver is not in kernel yet (current is 2.6.28), so you need to compile it yourself from AUR: [rt2860](https://aur.archlinux.org/packages/rt2860/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/rt2860)]</sup>.

Wireless connection has been tested by me (big_gie) and works with netcfg (2.1.2-1), wicd (1.5.6-1) and [Networkmanager 0.7](/index.php/Networkmanager_0.7 "Networkmanager 0.7")(0.7.0-1) with unencrypted and WPA. Note that with my router (Dlink DIR-615) I had to disable completely WPA2 and AES. So I need to use exclusively WPA with TKIP.

If you are having trouble getting the wireless working with either the default kernel or the driver from the AUR, try [blacklisting](/index.php/Blacklisting "Blacklisting") the rt2800lib module. This fixed wireless for me (using kernel 2.6.33-ARCH).

## Xorg

Here is a working xorg.conf file. Note that it is minimal. Almost everything should be automatically configured.

```
Section "ServerLayout"
   Identifier	"ArchLinux"
   Screen	 0 "Screen0"
EndSection

Section "Device"
   Identifier  "IntelCard"
   Driver      "intel"
   VendorName  "Intel Corporation"
   BoardName   "Mobile 945GME Express Integrated Graphics Controller"
   BusID       "PCI:0:2:0"
EndSection

Section "Monitor"
   Identifier   "Monitor0"
   VendorName   "ASUS"
   ModelName    "eeePC 1000"
   Modeline     "1024x600"  48.96 1024 1064 1168 1312 600 601 604 622 -HSync +Vsync # 60 Hz
EndSection

Section "Screen"
   Identifier "Screen0"
   Device     "IntelCard"
   Monitor    "Monitor0"
   DefaultDepth     24
   SubSection "Display"
       Viewport   0 0
       Depth     8
   EndSubSection
   SubSection "Display"
       Viewport   0 0
       Depth     15
   EndSubSection
   SubSection "Display"
       Viewport   0 0
       Depth     16
   EndSubSection
   SubSection "Display"
       Viewport   0 0
       Depth     24
       #Virtual   2048 2048
       Virtual 1680 1050
   EndSubSection
EndSection

```

## Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

## ACPI

Be sure to load the kernel module "eeepc_laptop" to get acpi events. The 1000 does not send the same events as the 901.

I (big_gie) created a new acpi package to support the 1000 acpi events: [acpi-eeepc-generic](https://aur.archlinux.org/packages/acpi-eeepc-generic/)<sup><small>AUR</small></sup>.

If you look up "eee" on AUR, you will find a dozen or so packages. I inspired myself from them to create a generic one. It only support the 1000 for the moment, but it should only be a matter of copying the file "acpi-eeepc-1000-events.conf" to "acpi-eeepc-901-events.conf" for example to support a new model.

For the events created by the 1000, see the file "acpi-eeepc-1000-events.conf".

### Notes

#### Sleep

Fn+F1 or closing lid should put the 1000 to sleep. It calls "acpi-eeepc-generic-suspend2ram.sh".

#### Wifi

Pressing Fn+F2 will call "acpi-eeepc-generic-wifi-toggle.sh" which will toggle the wireless card. Be sure to load "rfkill" module for this to work.

#### Brightness

Note that the brightness codes depends on the actual brightness level. If at the darker, lower level (00000020) and the "brithness up" button is push, the next level event is generated (00000021). If the button is pushed again, again the next level is generated (00000022) until full brightness is reached (0000002f). So basically, the ACPI event generated depends on the actual level.

## Hardware

### lspci

```
00:00.0 Host bridge: Intel Corporation Mobile 945GME Express Memory Controller Hub (rev 03)
00:02.0 VGA compatible controller: Intel Corporation Mobile 945GME Express Integrated Graphics Controller (rev 03)
00:02.1 Display controller: Intel Corporation Mobile 945GM/GMS/GME, 943/940GML Express Integrated Graphics Controller (rev 03)
00:1b.0 Audio device: Intel Corporation 82801G (ICH7 Family) High Definition Audio Controller (rev 02)
00:1c.0 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 1 (rev 02)
00:1c.1 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 2 (rev 02)
00:1c.2 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 3 (rev 02)
00:1c.3 PCI bridge: Intel Corporation 82801G (ICH7 Family) PCI Express Port 4 (rev 02)
00:1d.0 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #1 (rev 02)
00:1d.1 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #2 (rev 02)
00:1d.2 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #3 (rev 02)
00:1d.3 USB Controller: Intel Corporation 82801G (ICH7 Family) USB UHCI Controller #4 (rev 02)
00:1d.7 USB Controller: Intel Corporation 82801G (ICH7 Family) USB2 EHCI Controller (rev 02)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev e2)
00:1f.0 ISA bridge: Intel Corporation 82801GBM (ICH7-M) LPC Interface Bridge (rev 02)
00:1f.2 IDE interface: Intel Corporation 82801GBM/GHM (ICH7 Family) SATA IDE Controller (rev 02)
00:1f.3 SMBus: Intel Corporation 82801G (ICH7 Family) SMBus Controller (rev 02)
01:00.0 Network controller: RaLink RT2860
04:00.0 Ethernet controller: Attansic Technology Corp. L1e Gigabit Ethernet Adapter (rev b0)

```

### lsusb

```
Bus 001 Device 002: ID 04f2:b071 Chicony Electronics Co., Ltd
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_1000&oldid=408670](https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_1000&oldid=408670)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ASUS](/index.php/Category:ASUS "Category:ASUS")