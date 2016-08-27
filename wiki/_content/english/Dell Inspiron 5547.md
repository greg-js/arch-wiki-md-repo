This is an install and configuration guide for the Dell Inspiron 15 000 Series (Model 5547) laptop.

See the [Laptop/Dell](/index.php/Laptop/Dell "Laptop/Dell") chart for information on other Dell laptops.

## Contents

*   [1 Hardware Details](#Hardware_Details)
*   [2 Installation](#Installation)
*   [3 Hardware](#Hardware)
    *   [3.1 Microphone](#Microphone)
    *   [3.2 Video](#Video)
        *   [3.2.1 Toggle between HDMI/Monitor](#Toggle_between_HDMI.2FMonitor)
    *   [3.3 Touchpad](#Touchpad)

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

See [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch")

## Hardware

### Microphone

See [PulseAudio/Troubleshooting#Microphone_not_detected_by_PulseAudio](/index.php/PulseAudio/Troubleshooting#Microphone_not_detected_by_PulseAudio "PulseAudio/Troubleshooting") and [PulseAudio/Troubleshooting#Static_noise_in_microphone_recording](/index.php/PulseAudio/Troubleshooting#Static_noise_in_microphone_recording "PulseAudio/Troubleshooting").

### Video

See [ATI Dynamic Switchable Graphics](/index.php/Hybrid_graphics#ATI_Dynamic_Switchable_Graphics "Hybrid graphics") and [forums](https://bbs.archlinux.org/viewtopic.php?id=190236).

#### Toggle between HDMI/Monitor

See [xrandr](/index.php/Xrandr "Xrandr").

### Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").