## Contents

*   [1 About the laptop](#About_the_laptop)
*   [2 Compatibility](#Compatibility)
    *   [2.1 Webcam Flipping](#Webcam_Flipping)
*   [3 Powersaving](#Powersaving)
*   [4 Fun](#Fun)
*   [5 Freezes while/after booting](#Freezes_while.2Fafter_booting)
*   [6 lspci](#lspci)
*   [7 lsusb](#lsusb)

## About the laptop

*   13.3" LED Screen 1366 x 768\.
*   4GB DDR3
*   1.3Ghz Dual core.
*   320GB HDD.
*   8-cell battery 84wh.
*   HDMI

## Compatibility

Everything in this laptop is Linux compatible, therefore you will not have any issues installing Linux. I recommend [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") for sound buttons. Every other fn-X button works. Suspend, wifi, brightness works. The video out button does not work, use xrandr instead. HDMI works as well. The battery is properly read. Use [laptop-mode-tools](/index.php/Laptop#Laptop_mode_tools "Laptop") for power saving. You can run xorg without config file. xf86-video-intel is the package you need. I could not run x with vesa on this chipset, it just froze completely. HDMI and VGA out works, but not via fn-F8\. You can use lxrandr, GUI for xrandr for setting up video out. You can make fn-f8 work by configuring [Acpid](/index.php/Acpid "Acpid").

### Webcam Flipping

Written by [MessedUpHare](https://bbs.archlinux.org/profile.php?id=49720)

Some models supposedly have their webcams mounted upside down (not confirmed) causing the image to display upside down, this at least affects Skype and Google Hangout.

**Google Hangout in Chromium on x86_64**

```
$ LD_PRELOAD=/usr/lib32/libv4l/v4l1compat.so /opt/google/talkplugin/GoogleTalkPlugin & chromium

```

the above solution requires lib32-v4l-utils from multilib, I have also installed google-talkplugin from AUR

## Powersaving

See [power saving](/index.php/Power_saving "Power saving").

## Fun

This computer has an extra power button on the left, you can configure this with [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") and run something useful. Like I use it for switching songs. The extra button is originally for powering up with Asus Express gate.

## Freezes while/after booting

On my UL30A current Arch or Manjaro install won't boot (freeze somewhere along the process) unless I pass `processor.nocst` as kernel parameter. This deactivates a certain APIC feature to determine the C-state but shouldn't affect performance or stability since a legacy one is used instead. Don't forget to add that to your GRUB config afterwards as well.

Other things I pass to the kernel to improve battery life are `nmi_watchdog=0` and `pcie_aspm=force`. You have to see how well those work for you.

In general if you encounter freezes during boot APIC and ACPI should be looked into and deactivated if a solution can't be found.

## lspci

```
[brain@Brain_NoteBook ~]$ lspci
00:00.0 Host bridge: Intel Corporation Mobile 4 Series Chipset Memory Controller Hub (rev 07)
00:02.0 VGA compatible controller: Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller (rev 07)
00:02.1 Display controller: Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller (rev 07)
00:1a.0 USB controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #4 (rev 03)
00:1a.1 USB controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #5 (rev 03)
00:1a.2 USB controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #6 (rev 03)
00:1a.7 USB controller: Intel Corporation 82801I (ICH9 Family) USB2 EHCI Controller #2 (rev 03)
00:1b.0 Audio device: Intel Corporation 82801I (ICH9 Family) HD Audio Controller (rev 03)
00:1c.0 PCI bridge: Intel Corporation 82801I (ICH9 Family) PCI Express Port 1 (rev 03)
00:1c.1 PCI bridge: Intel Corporation 82801I (ICH9 Family) PCI Express Port 2 (rev 03)
00:1c.5 PCI bridge: Intel Corporation 82801I (ICH9 Family) PCI Express Port 6 (rev 03)
00:1d.0 USB controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #1 (rev 03)
00:1d.1 USB controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #2 (rev 03)
00:1d.2 USB controller: Intel Corporation 82801I (ICH9 Family) USB UHCI Controller #3 (rev 03)
00:1d.7 USB controller: Intel Corporation 82801I (ICH9 Family) USB2 EHCI Controller #1 (rev 03)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev 93)
00:1f.0 ISA bridge: Intel Corporation ICH9M-E LPC Interface Controller (rev 03)
00:1f.2 SATA controller: Intel Corporation 82801IBM/IEM (ICH9M/ICH9M-E) 4 port SATA Controller [AHCI mode] (rev 03)
02:00.0 Network controller: Intel Corporation WiMAX/WiFi Link 5150
03:00.0 Ethernet controller: Atheros Communications Inc. AR8132 Fast Ethernet (rev c0)

```

## lsusb

```
[brain@Brain_NoteBook ~]$ lsusb
Bus 001 Device 003: ID 064e:a136 Suyin Corp. Asus Integrated Webcam [CN031B]
Bus 001 Device 004: ID 8086:0180 Intel Corp. WiMAX Connection 2400m
Bus 002 Device 002: ID 0b05:1751 ASUSTek Computer, Inc. BT-253 Bluetooth Adapter
Bus 005 Device 002: ID 0458:00b5 KYE Systems Corp. (Mouse Systems) 
Bus 008 Device 003: ID 058f:6366 Alcor Micro Corp. Multi Flash Reader
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 005 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 006 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 007 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 008 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```