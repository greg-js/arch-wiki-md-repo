The Dell Latitude E5430 is a business line laptop made for corporate users who have a need for durability. This article will tell you how to get the basic components of the laptop running with Arch.

## Contents

*   [1 Hardware](#Hardware)
*   [2 Installation](#Installation)
*   [3 Wireless](#Wireless)
    *   [3.1 Broadcom BCM5761](#Broadcom_BCM5761)
*   [4 Graphic Interface Configuration](#Graphic_Interface_Configuration)
    *   [4.1 Issue with XKeyboardConfig](#Issue_with_XKeyboardConfig)
*   [5 General Configurations](#General_Configurations)
    *   [5.1 PC Speaker](#PC_Speaker)
    *   [5.2 Synaptics Touchpad](#Synaptics_Touchpad)

## Hardware

Modules found by hwdetect:

```
AGP      : intel-gtt 
ACPI     : ac battery button processor thermal video 
BLOCK    : scsi_mod sd_mod sr_mod ahci libahci libata uvcvideo usbcore ehci-hcd ehci-pci xhci-hcd usb-common 
BLUETOOTH: btusb bluetooth 
CDROM    : cdrom 
CPUFREQ  : acpi-cpufreq 
CRYPTO   : aes-x86_64 aesni-intel crc32-pclmul crc32c-intel crct10dif-pclmul ghash-clmulni-intel glue_helper ablk_helper crct10dif_common crct10dif_generic cryptd gf128mul lrw 
DRM      : drm drm_kms_helper i915 
HWMON    : coretemp hwmon 
I2C      : i2c-algo-bit i2c-i801 i2c-core 
INPUT    : evdev joydev atkbd psmouse mousedev i8042 libps2 serio serio_raw sparse-keymap hid-generic hid usbhid 
KVM      : kvm-intel kvm 
MEDIA    : media uvcvideo videobuf2-core videobuf2-memops videobuf2-vmalloc videodev 
NET      : tg3 libphy bluetooth 6lowpan_iphc rfkill 
PARPORT  : parport parport_pc 
SOUND    : pcspkr snd-hwdep snd-pcm snd-timer snd snd-hda-codec snd-hda-controller snd-hda-intel soundcore 
WATCHDOG : iTCO_vendor_support iTCO_wdt 
OTHER    : microcode dcdbas led-class mac_hid lpc_ich mei-me mei mmc_core sdhci-pci sdhci shpchp dell-laptop dell-wmi wmi intel_rapl pps_core ptp intel_powerclamp x86_pkg_temp_thermal crc-t10dif crc16

```

lspci output:

```
00:00.0 Host bridge: Intel Corporation 3rd Gen Core processor DRAM Controller (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 3rd Gen Core processor Graphics Controller (rev 09)
00:14.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller (rev 04)
00:16.0 Communication controller: Intel Corporation 7 Series/C210 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 1 (rev c4)
00:1c.1 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 2 (rev c4)
00:1c.2 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 3 (rev c4)
00:1c.3 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 4 (rev c4)
00:1c.5 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 6 (rev c4)
00:1c.6 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 7 (rev c4)
00:1d.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation HM77 Express Chipset LPC Controller (rev 04)
00:1f.2 RAID bus controller: Intel Corporation 82801 Mobile SATA Controller [RAID mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 7 Series/C210 Series Chipset Family SMBus Controller (rev 04)
02:00.0 Network controller: Broadcom Corporation BCM43228 802.11a/b/g/n
0b:00.0 SD Host controller: O2 Micro, Inc. OZ600FJ0/OZ900FJ0/OZ600FJS SD/MMC Card Reader Controller (rev 05)
0c:00.0 Ethernet controller: Broadcom Corporation NetXtreme BCM5761 Gigabit Ethernet PCIe (rev 10)

```

## Installation

You can follow the [Installation guide](/index.php/Installation_guide "Installation guide") to get yourself up and running. Just few exceptions mentioned below.

## Wireless

### Broadcom BCM5761

This card requires the proprietary [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) driver, available in AUR (alternatively, you can use its dkms version, [broadcom-wl-dkms](https://aur.archlinux.org/packages/broadcom-wl-dkms/)).

## Graphic Interface Configuration

### Issue with XKeyboardConfig

While starting the graphic interface, you might come across with the bug [#77504](https://bugs.freedesktop.org/show_bug.cgi?id=77504) reported in freedesktop bugzilla. It seems to apply to both Xorg and Xwayland. During the display server startup, the XKEYBOARD keymap compiler (xkbcomb) reports:

```
> Warning:          Compat map for group 2 redefined
>                   Using new definition
> Warning:          Compat map for group 3 redefined
>                   Using new definition
> Warning:          Compat map for group 4 redefined
>                   Using new definition
Errors from xkbcomp are not fatal to the X server

```

I (josephgbr) followed the solution provided in the forum topic [Xkeyboard/xkbcomp gives warnings](https://bbs.archlinux.org/viewtopic.php?pid=1105212) and it seems to work fine: Comment out the following lines in the file `/usr/share/X11/xkb/compat/basic`. The double forward-slash is the comment symbol.

```
 //    group 2 = AltGr;                                                                
 //    group 3 = AltGr;
 //    group 4 = AltGr; 
```

## General Configurations

### PC Speaker

The E5430 has an awfully loud PC speaker. To disable it, ensure the module `pcspkr` is not loaded during bootup:

 `/etc/modprobe.d/nobeep.conf` 

```
#Do not load the 'pcspkr' module on boot.

blacklist pcspkr
```

You should follow instructions for installing [cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils") and [pm-utils](/index.php/Pm-utils "Pm-utils"). There have been no problems with suspending and hibernating this laptop - just ensure you have enough swap.

### Synaptics Touchpad

Make sure you install the package [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) as it is required by the touchpad