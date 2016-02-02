# Dell Inspiron 5547

This is an install and configuration guide for the Dell Inspiron 15 000 Series (Model 5547) laptop, testing with the manjaro 4.1.15-2-MANJARO kernel.

See the [Laptop/Dell](/index.php/Laptop/Dell "Laptop/Dell") chart for information on other Dell laptops.

## Contents

*   [1 Hardware Details](#Hardware_Details)
*   [2 Installation](#Installation)
*   [3 Hardware](#Hardware)
    *   [3.1 Audio](#Audio)
    *   [3.2 Microphone](#Microphone)
    *   [3.3 Video](#Video)
    *   [3.4 Keyboard](#Keyboard)
    *   [3.5 Touchpad](#Touchpad)
    *   [3.6 Wireless](#Wireless)
    *   [3.7 USB, SD card slot, ethernet, HDMI, webcam and mediakeys](#USB.2C_SD_card_slot.2C_ethernet.2C_HDMI.2C_webcam_and_mediakeys)
*   [4 Power Management](#Power_Management)

## Hardware Details

lspci output:

```
 00:00.0 Host bridge: Intel Corporation Haswell-ULT DRAM Controller (rev 0b)
 00:02.0 VGA compatible controller: Intel Corporation Haswell-ULT Integrated Graphics Controller (rev 0b)
 00:03.0 Audio device: Intel Corporation Haswell-ULT HD Audio Controller (rev 0b)
 00:14.0 USB controller: Intel Corporation 8 Series USB xHCI HC (rev 04)
 00:16.0 Communication controller: Intel Corporation 8 Series HECI #0 (rev 04)
 00:1b.0 Audio device: Intel Corporation 8 Series HD Audio Controller (rev 04)
 00:1c.0 PCI bridge: Intel Corporation 8 Series PCI Express Root Port 3 (rev e4)
 00:1c.3 PCI bridge: Intel Corporation 8 Series PCI Express Root Port 4 (rev e4)
 00:1c.4 PCI bridge: Intel Corporation 8 Series PCI Express Root Port 5 (rev e4)
 00:1d.0 USB controller: Intel Corporation 8 Series USB EHCI #1 (rev 04)
 00:1f.0 ISA bridge: Intel Corporation 8 Series LPC Controller (rev 04)
 00:1f.2 SATA controller: Intel Corporation 8 Series SATA Controller 1 [AHCI mode] (rev 04)
 00:1f.3 SMBus: Intel Corporation 8 Series SMBus Controller (rev 04)
 01:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8101E/RTL8102E PCI Express Fast Ethernet controller (rev 07)
 02:00.0 Network controller: Qualcomm Atheros QCA9565 / AR9565 Wireless Network Adapter (rev 01)
 03:00.0 Display controller: Advanced Micro Devices, Inc. [AMD/ATI] Topaz XT [Radeon R7 M260/M265]

```

lsusb output:

```
 Bus 001 Device 006: ID 064e:c231 Suyin Corp. 
 Bus 001 Device 005: ID 0bda:0129 Realtek Semiconductor Corp. RTS5129 Card Reader Controller
 Bus 001 Device 004: ID 04f3:2013 Elan Microelectronics Corp. 
 Bus 001 Device 007: ID 0cf3:e005 Atheros Communications, Inc. 
 Bus 001 Device 002: ID 8087:8000 Intel Corp. 
 Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
 Bus 003 Device 002: ID 1058:0748 Western Digital Technologies, Inc. My Passport (WDBKXH, WDBY8L)
 Bus 003 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
 Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Installation

Tested with dual boots Windows 10/Manjaro 15-2. Step: Installation from a USB key. Create one following [this page](/index.php/USB_flash_installation_media "USB flash installation media"). Installed with UEFI mode enabled ([Boot installation](/index.php/Beginners%27_guide#Boot_the_installation_medium "Beginners' guide")).

## Hardware

### Audio

Sound should work out of the box with Intel HD Audio and [PulseAudio](/index.php/PulseAudio "PulseAudio").

### Microphone

Need to configure [PulseAudio](/index.php/PulseAudio/Troubleshooting#Microphone_not_detected_by_PulseAudio "PulseAudio/Troubleshooting") If the built-in microphone is static, [setting the sample rate in PulseAudio](/index.php/PulseAudio/Troubleshooting#Static_noise_in_microphone_recording "PulseAudio/Troubleshooting") may solve the problem.

### Video

The notebook comes two GPUs, one power-efficent (Intel Corporation Haswell-ULT Integrated Graphics) and one more powerful and more power-hungry (AMD Radeon R7 M265). Work with [video-hybrid-intel-ati-bumblebee](https://www.archlinux.org/packages/?name=video-hybrid-intel-ati-bumblebee) but you need to read [Hybrid graphics/AMD Dynamic Switchable Graphics](/index.php/ATI#Hybrid_graphics.2FAMD_Dynamic_Switchable_Graphics "ATI") (proper use of hybrid graphics). This has not be testing yet.

[AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") not tested.

### Keyboard

Keyboard worked out of the box.

### Touchpad

Touchpad worked out of the box. To enable scroll and more, install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics). With the default configuration file it will work well, but if you want to fine tune the behaviour, read [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

### Wireless

Wireless worked out of the box.

### USB, SD card slot, ethernet, HDMI, webcam and mediakeys

**USB:** work out of the box. **SD card slotnor:** not tested **Ethernet:** work out of the box. **HDMI:** work out of the box, need configuration to auto-switch between video/sound laptop/hdmi(TV,...). **Mediakeys:** almost all work. Wifi off/on not working, switch between monitor not working

## Power Management

Not tested.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dell_Inspiron_5547&oldid=418334](https://wiki.archlinux.org/index.php?title=Dell_Inspiron_5547&oldid=418334)"