# Dell Inspiron 1520

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 Intro](#Intro)
    *   [1.1 Summary](#Summary)
    *   [1.2 To do](#To_do)
    *   [1.3 Working](#Working)
    *   [1.4 Unknown / Untested](#Unknown_.2F_Untested)
*   [2 Installation](#Installation)
*   [3 Kernel](#Kernel)
*   [4 X.org](#X.org)
    *   [4.1 NVIDIA GeForce 8600M GT](#NVIDIA_GeForce_8600M_GT)
*   [5 Hardware](#Hardware)
    *   [5.1 Microphone](#Microphone)
    *   [5.2 lspci](#lspci)
*   [6 Power Management](#Power_Management)
    *   [6.1 Suspend and Resume](#Suspend_and_Resume)
    *   [6.2 CPU Frequency Scaling](#CPU_Frequency_Scaling)
    *   [6.3 ACPI](#ACPI)
*   [7 Links](#Links)
    *   [7.1 General](#General)
    *   [7.2 Linux on a Dell Inspiron 1520](#Linux_on_a_Dell_Inspiron_1520)

## Intro

### Summary

This is the wiki entry for the Dell XPS 1520 laptop. It's heavily under construction, and it's based on the Dell Inspiron 8500 page.

### To do

*   everything...

### Working

*   Ethernet: Broadcom chip, use b44 module
*   Wireless: Dell Wireless 1395 802.11g Mini Card (Broadcom BCM4311) Use [b43-firmware](https://aur.archlinux.org/packages.php?ID=21690) from the AUR.
*   Audio: intel8x0 (Sigmatel)
*   Display: 1440x900
*   Multimedia keys (set up xmodmap)
*   nVidia GeForce 8600M GT (256MB GDDR2)
*   SD card slot
*   Webcam: OmniVision Technologies, Inc. OV2640

### Unknown / Untested

*   Modem
*   Firewire

## Installation

Just follow the [Beginners' Guide](https://wiki.archlinux.org/index.php/Beginners%27_Guide)

## Kernel

Works with 2.6.39 out of the box.

## X.org

This is my working xorg.conf:

### NVIDIA GeForce 8600M GT

This config should work with all mobile GeForce chipsets. Install the synaptic package for the touchpad.

```
# **********************************************************************
# Modules section. This allows modules to be specified
# **********************************************************************

Section "Module"
       Load  "ddc"  # ddc probing of monitor
       Load  "dbe"
       Load  "dri"
       Load  "extmod"
       Load  "glx"
       Load  "bitmap" # bitmap-fonts
       Load  "type1"
       Load  "freetype"
       Load  "record"
       Load  "synaptics"
EndSection

# ******************************
# Files section
# ******************************

Section "Files"
       ModulePath   "/usr/lib/xorg/modules"
       FontPath     "/usr/share/fonts/misc"
       FontPath     "/usr/share/fonts/75dpi"
       FontPath     "/usr/share/fonts/100dpi"
       FontPath     "/usr/share/fonts/Type1"
       FontPath     "/usr/share/fonts/encodings"
       FontPath     "/usr/share/fonts/cyrillic"
EndSection

# ******************************
# Server flags section
# ******************************

Section "ServerFlags"

EndSection

# ******************************
# Core keyboard's InputDevice section
# ******************************

Section "InputDevice"
       Identifier  "Keyboard0"
       Driver      "keyboard"
       Option      "CoreKeyboard"
       Option "XkbRules" "xorg"
       Option "XkbModel" "pc105"
       Option "XkbLayout" "se"
EndSection

# ******************************
# Core Pointer's InputDevice section
# ******************************

Section "InputDevice"
       Identifier      "USB Mouse"
       Driver          "mouse"
       Option          "Device"                "/dev/input/mice"
       Option		"SendCoreEvents"	"true"
       Option          "Protocol"              "IMPS/2"
       Option          "ZAxisMapping"          "4 5"
       Option          "Buttons"               "5"
EndSection

Section "InputDevice"
       Identifier      "Touchpad"
       Driver          "synaptics"
       Option  "Device"        "/dev/input/mouse0"
       Option  "Protocol"      "auto-dev"
       Option  "LeftEdge"      "1700"
       Option  "RightEdge"     "5300"
       Option  "TopEdge"       "1700"
       Option  "BottomEdge"    "4200"
       Option  "FingerLow"     "25"
       Option  "FingerHigh"    "30"
       Option  "MaxTapTime"    "180"
       Option  "MaxTapMove"    "220"
       Option  "VertScrollDelta" "100"
       Option  "MinSpeed"      "0.06"
       Option  "MaxSpeed"      "0.12"
       Option  "AccelFactor" "0.0010"
       Option  "SHMConfig"     "on"
EndSection

# ******************************
# Monitor section
# ******************************

Section "Monitor"
       Identifier "Dell Inspiron 1520 WXGA+ LCD"
       Option "DPMS" "true"
EndSection

# ******************************
# Graphics device section
# ******************************

Section "Device"
       Identifier  "NVIDIA GeForce 8600M GT"
       Driver      "nvidia"
       VendorName  "NVIDIA"
       BoardName   "8600M GT"
       Option	"NoLogo"	"true"
       Option	"AllowGLXWithComposite"	"true"
       Option	"Coolbits"	"1"
       Option	"Triplebuffer"	"true"
       Option "OnDemandVBlankInterrupts" "true"
EndSection

# ******************************
# Screen sections
# ******************************

Section "Screen"
       Identifier "Screen0"
       Device     "NVIDIA GeForce 8600M GT"
       Monitor    "Dell Inspiron 1520 WXGA+ LCD"
       DefaultColorDepth 24
       SubSection "Display"
               Depth     24
               Modes "1440x900" "1280x800" "1280x768" "1280x720" "1024x768" "800x600" "640x480"
       EndSubSection
       SubSection "Display"
               Depth     32
               Modes "1440x900" "1280x800" "1280x768" "1280x720" "1024x768" "800x600" "640x480"
       EndSubSection
EndSection

# ******************************
# ServerLayout sections.
# ******************************

Section "ServerLayout"
       Identifier     "Xorg Configured"
       Screen      0  "Screen0" 0 0
       InputDevice    "Keyboard0" "CoreKeyboard"
       InputDevice	"USB Mouse"	"CorePointer"
       InputDevice    "Touchpad" "SendCoreEvents"
EndSection

# ******************************
# DRI extension options section
# ******************************

Section "DRI"
       Group "video"
       Mode 0666
EndSection

Section "Extensions"
       Option "Composite" "Enable"
EndSection

```

## Hardware

### Microphone

To activate the microphone with `alsamixer`, open `alsamixer` and press `Tab`. Now activate _Capture_ by pressing `Space`. If it does not work, play around with the other settings.

### lspci

```
00:00.0 Host bridge: Intel Corporation Mobile PM965/GM965/GL960 Memory Controller Hub (rev 0c)
00:01.0 PCI bridge: Intel Corporation Mobile PM965/GM965/GL960 PCI Express Root Port (rev 0c)
00:1a.0 USB Controller: Intel Corporation 82801H (ICH8 Family) USB UHCI Controller #4 (rev 02)
00:1a.1 USB Controller: Intel Corporation 82801H (ICH8 Family) USB UHCI Controller #5 (rev 02)
00:1a.7 USB Controller: Intel Corporation 82801H (ICH8 Family) USB2 EHCI Controller #2 (rev 02)
00:1b.0 Audio device: Intel Corporation 82801H (ICH8 Family) HD Audio Controller (rev 02)
00:1c.0 PCI bridge: Intel Corporation 82801H (ICH8 Family) PCI Express Port 1 (rev 02)
00:1c.1 PCI bridge: Intel Corporation 82801H (ICH8 Family) PCI Express Port 2 (rev 02)
00:1c.3 PCI bridge: Intel Corporation 82801H (ICH8 Family) PCI Express Port 4 (rev 02)
00:1d.0 USB Controller: Intel Corporation 82801H (ICH8 Family) USB UHCI Controller #1 (rev 02)
00:1d.1 USB Controller: Intel Corporation 82801H (ICH8 Family) USB UHCI Controller #2 (rev 02)
00:1d.2 USB Controller: Intel Corporation 82801H (ICH8 Family) USB UHCI Controller #3 (rev 02)
00:1d.7 USB Controller: Intel Corporation 82801H (ICH8 Family) USB2 EHCI Controller #1 (rev 02)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev f2)
00:1f.0 ISA bridge: Intel Corporation 82801HEM (ICH8M) LPC Interface Controller (rev 02)
00:1f.1 IDE interface: Intel Corporation 82801HBM/HEM (ICH8M/ICH8M-E) IDE Controller (rev 02)
00:1f.2 IDE interface: Intel Corporation 82801HBM/HEM (ICH8M/ICH8M-E) SATA IDE Controller (rev 02)
00:1f.3 SMBus: Intel Corporation 82801H (ICH8 Family) SMBus Controller (rev 02)
01:00.0 VGA compatible controller: nVidia Corporation G84 [GeForce 8600M GT] (rev a1)
03:00.0 Ethernet controller: Broadcom Corporation BCM4401-B0 100Base-TX (rev 02)
03:01.0 FireWire (IEEE 1394): Ricoh Co Ltd R5C832 IEEE 1394 Controller (rev 05)
03:01.1 SD Host controller: Ricoh Co Ltd R5C822 SD/SDIO/MMC/MS/MSPro Host Adapter (rev 22)
03:01.2 System peripheral: Ricoh Co Ltd R5C592 Memory Stick Bus Host Adapter (rev 12)
03:01.3 System peripheral: Ricoh Co Ltd xD-Picture Card Controller (rev 12)
0c:00.0 Network controller: Broadcom Corporation BCM4311 802.11b/g WLAN (rev 01)

```

## Power Management

I suggest you read [Gentoo Power Management Guide](http://www.gentoo.org/doc/en/power-management-guide.xml) for great information.

### Suspend and Resume

Suspend and resume works 100% with the default kernel.

Hibernation doesn't work, all it does is shut down the computer.

### CPU Frequency Scaling

See the main [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") article.

### ACPI

To turnoff the computer when you press the power button, put the following in /etc/acpi/handler.sh

```
button/power)
       case "$2" in
           PBTN)
                   logger "PowerButton pressed: $2"
                   halt
           ;;
           *)    logger "ACPI action undefined: $2" ;;
       esac

```

Replace the "halt" line with the shutdown command of your choice.

To turn off the backlight of an ATI Radeon Mobility card, put the following in /etc/acpi/handler.sh

```
button/lid)
       case "$2" in
           LID)
               logger "ACPI button/lid action"
               STATE=`radeontool light`
               case "$STATE" in
                   "The radeon backlight looks on") radeontool light off ;;
                   "The radeon backlight looks off") radeontool light on ;;
               esac
               ;;
       esac
       ;;

```

This requires that you have the radeontool package installed (it is in AUR). You also need to add "acpid" to the DAEMONS array in /etc/rc.conf.

## Links

### General

*   [Gentoo Power Management Guide](http://www.gentoo.org/doc/en/power-management-guide.xml)
*   [Gentoo Dell Inspiron 8500 Wiki](http://en.gentoo-wiki.com/Inspiron_8500)
*   [Software Suspend 2](http://www.suspend2.net/)
*   [Linux on Laptops](http://www.linux-on-laptops.com/dell.html)
*   This report is listed at the [TuxMobil: Linux Laptop and Notebook Installation Guides Survey: DELL](http://tuxmobil.org/dell.html).

### Linux on a Dell Inspiron 1520

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dell_Inspiron_1520&oldid=382903](https://wiki.archlinux.org/index.php?title=Dell_Inspiron_1520&oldid=382903)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Dell](/index.php/Category:Dell "Category:Dell")