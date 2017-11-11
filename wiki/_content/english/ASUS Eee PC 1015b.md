This page includes general information regarding Asus EEE PC 1015b and related notes on installing/using Arch Linux on it.

## Contents

*   [1 System specs](#System_specs)
*   [2 Summary](#Summary)
*   [3 Graphics](#Graphics)
*   [4 lspci](#lspci)
*   [5 Audio](#Audio)
*   [6 Powersaving](#Powersaving)

## System specs

*   **CPU:** AMD Fusion APU C30 1.2GHz (single core) **or** C50 1.0GHz (dual core) Processor

*   **RAM:** 1DDR3, 2 x SO-DIMM, 1GB/2GB (work with 4GB/8GB module)

*   **HDD:** 2.5" SATA 250GB/320GB/500GB HDD

*   **GPU:** Radeon HD 6250

*   **Display:** 10.1" LED backlit WSVGA (1024x600) Screen

*   **Ethernet:** Atheros AR8152 v2.0 Fast Ethernet

*   **Wireless:** Atheros WLAN 802.11 b/g/n@2.4GHz **or** Broadcom WLAN BCM4313 802.11 b/g/n@2.4GHz

*   **Bluetooth:** Bluetooth V2.1+EDR **or** Bluetooth V3.0+HS (both optional)

*   **Webcam:** Working (remenber to add yourself to video group)

*   **Card Reader:** SDHC Reader

*   **Extras:** 3 USB 2.0 ports **or** 1 x USB 3.0 port and 2 x USB 2.0 ports

## Summary

Things that "just work":

*   Wlan (ath9k is part of the kernel; some use brcmsmac)
*   Ethernet
*   Graphics (with kms and dri2, using the xf86-video-ati driver)
*   Webcam (using v4l)
*   Suspend-to-RAM (after installing acpid)
*   Cardreader (but keucr is in staging, thus **taints the kernel**. PyroPeter experienced **crashes** while he inserted or removed sd cards)
*   Bluetooth (after installing bluez)
*   CPU Frequency Scaling (Use acpi_cpufreq since linux 3.7)
*   TouchPad (support multi-touch after installing xf86-input-synaptics)
*   Video Acceleration (either [open source driver](/index.php/ATI#Enabling_video_acceleration "ATI") ([xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati)) or [ATI/AMD's propretary driver(catalyst)](/index.php/ATI_Catalyst#Video_acceleration "ATI Catalyst") work)

*/etc/modprobe.d/eeepc1015b.conf:*

```
# supposed to help against following msg in dmesg:
# SP5100 TCO timer: mmio address 0xbafe00 already in use
blacklist sp5100_tco

# if you don't need the sd-card reader you may want to blacklist
# keucr. it is in staging, thus taints the kernel
blacklist keucr

# if you find "*ACPI: resource piix4_smbus [io 0x0b00-0x0b07]*
# *conflicts with ACPI region SMRG [io 0xb00-0xb0f]*" 
# in /var/log/messages.log ,try to uncomment the following line
#blacklist i2c_piix4

```

## Graphics

The open source drivers will work adequately. For AMD [catalyst](/index.php/Catalyst "Catalyst") drivers, please use the catalyst and catalyst-utils packages from the AUR.

## lspci

```
00:00.0 Host bridge: Advanced Micro Devices [AMD] Family 14h Processor Root Complex
00:01.0 VGA compatible controller: Advanced Micro Devices [AMD] nee ATI Device 9805
00:01.1 Audio device: Advanced Micro Devices [AMD] nee ATI Wrestler HDMI Audio [Radeon HD 6250/6310]
00:04.0 PCI bridge: Advanced Micro Devices [AMD] Family 14h Processor Root Port
00:05.0 PCI bridge: Advanced Micro Devices [AMD] Family 14h Processor Root Port
00:11.0 SATA controller: Advanced Micro Devices [AMD] nee ATI SB7x0/SB8x0/SB9x0 SATA Controller [AHCI mode]
00:12.0 USB controller: Advanced Micro Devices [AMD] nee ATI SB7x0/SB8x0/SB9x0 USB OHCI0 Controller
00:12.2 USB controller: Advanced Micro Devices [AMD] nee ATI SB7x0/SB8x0/SB9x0 USB EHCI Controller
00:13.0 USB controller: Advanced Micro Devices [AMD] nee ATI SB7x0/SB8x0/SB9x0 USB OHCI0 Controller
00:13.2 USB controller: Advanced Micro Devices [AMD] nee ATI SB7x0/SB8x0/SB9x0 USB EHCI Controller
00:14.0 SMBus: Advanced Micro Devices [AMD] nee ATI SBx00 SMBus Controller (rev 42)
00:14.2 Audio device: Advanced Micro Devices [AMD] nee ATI SBx00 Azalia (Intel HDA) (rev 40)
00:14.3 ISA bridge: Advanced Micro Devices [AMD] nee ATI SB7x0/SB8x0/SB9x0 LPC host controller (rev 40)
00:14.4 PCI bridge: Advanced Micro Devices [AMD] nee ATI SBx00 PCI to PCI Bridge (rev 40)
00:15.0 PCI bridge: Advanced Micro Devices [AMD] nee ATI SB700/SB800/SB900 PCI to PCI bridge (PCIE port 0)
00:18.0 Host bridge: Advanced Micro Devices [AMD] Family 12h/14h Processor Function 0 (rev 43)
00:18.1 Host bridge: Advanced Micro Devices [AMD] Family 12h/14h Processor Function 1
00:18.2 Host bridge: Advanced Micro Devices [AMD] Family 12h/14h Processor Function 2
00:18.3 Host bridge: Advanced Micro Devices [AMD] Family 12h/14h Processor Function 3
00:18.4 Host bridge: Advanced Micro Devices [AMD] Family 12h/14h Processor Function 4
00:18.5 Host bridge: Advanced Micro Devices [AMD] Family 12h/14h Processor Function 6
00:18.6 Host bridge: Advanced Micro Devices [AMD] Family 12h/14h Processor Function 5
00:18.7 Host bridge: Advanced Micro Devices [AMD] Family 12h/14h Processor Function 7
01:00.0 Network controller: Atheros Communications Inc. AR9285 Wireless Network Adapter (PCI-Express) (rev 01)
02:00.0 Ethernet controller: Atheros Communications Inc. AR8152 v2.0 Fast Ethernet (rev c1)

```

On models with ASMedia USB 3.0 chip, replace last 2 line with:

```
01:00.0 Network controller: Broadcom Corporation BCM4313 802.11b/g/n Wireless LAN Controller (rev 01)
02:00.0 Ethernet controller: Atheros Communications Inc. AR8152 v2.0 Fast Ethernet (rev c1)
03:00.0 USB controller: ASMedia Technology Inc. Device 1040

```

lsusb:

```
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 002 Device 002: ID 13d3:5702 IMC Networks UVC VGA Webcam

```

## Audio

After running alsaconf the graphics card was the default audio output, so I had to create `/etc/asound.conf` with the following contents:

```
defaults.ctl.card 1
defaults.pcm.card 1
defaults.timer.card 1

```

Volume function key for alsa:

 `/etc/acpi/handler.sh` 
```
......
        open)
            #echo "LID opend!">/dev/tty5
            ;;
    esac
    ;;
## volume control key ##
button/mute)
  case "$2" in
    MUTE) amixer set Master toggle ;;
  esac
  ;;
button/volumedown)
  case "$2" in
    VOLDN) amixer set Master 2%- ;;
  esac
  ;;
button/volumeup)
  case "$2" in
    VOLUP) amixer set Master 2%+ ;;
  esac
  ;;
## volume control key end ##
*)
  logger "ACPI group/action underfined: $1 /$2"
  ;;
esac
```

## Powersaving

When system is idle, [ATI/AMD's propretary driver(catalyst)](/index.php/ATI_Catalyst "ATI Catalyst") saves 2.5W than xf86-video-ati.