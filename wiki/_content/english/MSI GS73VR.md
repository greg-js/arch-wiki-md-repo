This page is work in progress

This page is about MSI GS73VR hardware configuration

## Contents

*   [1 System Settings](#System_Settings)
    *   [1.1 Official Specifications](#Official_Specifications)
    *   [1.2 Specifications according to uname, lspci and lsusb](#Specifications_according_to_uname.2C_lspci_and_lsusb)
        *   [1.2.1 Microarchitecture, processor and platform](#Microarchitecture.2C_processor_and_platform)
        *   [1.2.2 PCI buses and devices](#PCI_buses_and_devices)
        *   [1.2.3 USB devices](#USB_devices)
*   [2 Hardware Setup](#Hardware_Setup)
    *   [2.1 Special Function Keys](#Special_Function_Keys)

# System Settings

### Official Specifications

*   **Processor:** Intel 6th/7th Generation Core Processor
*   **Chipset:** Intel HM170/HM175
*   **Memory:** Up to 32 GiB of DDR4
*   **Video Cards**
    *   **Integrated Video Card:** Intel HD graphics
    *   **Dedicated Video Card:** NVIDIA Corporation GP106M [GeForce GTX 1060
    *   **Display:** 17.3" FHD(1920x1080) or UHD(3840x2160) wired to Intel HD
*   **Audio and Speakers:**
    *   **Sound Card:** Realtek ALC898 Analog
    *   **Speakers:** 4 speakers and 1 subwoofer
*   **M.2 Drives:** M.2 driver connected to PCIe 3.0 x4
*   **Hard Drives:** SATA 3 port for 2.5" HDDs
*   **Ethernet:**
*   **Wireless:**
*   **WebCam:**
*   **Card Reader:**
*   **Ports:**
    *   (1) Microphone
    *   (1) Headphone JACK with SPID/F
    *   (1) Intel Thunderbolt 3 attached to PCIe 3.0 x4
    *   (1) USB 2.0
    *   (3) USB 3.0
    *   (1) AC adapter connector

### Specifications according to uname, lspci and lsusb

#### Microarchitecture, processor and platform

 `uname -mpi` 
```
x86_64 unknown unknown

```

#### PCI buses and devices

 `lspci` 
```
00:00.0 Host bridge: Intel Corporation Device 5910 (rev 05)
00:01.0 PCI bridge: Intel Corporation Skylake PCIe Controller (x16) (rev 05)
00:02.0 VGA compatible controller: Intel Corporation Device 591b (rev 04)
00:14.0 USB controller: Intel Corporation Sunrise Point-H USB 3.0 xHCI Controller (rev 31)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-H Thermal subsystem (rev 31)
00:16.0 Communication controller: Intel Corporation Sunrise Point-H CSME HECI #1 (rev 31)
00:17.0 SATA controller: Intel Corporation Sunrise Point-H SATA Controller [AHCI mode] (rev 31)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #1 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #5 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #9 (rev f1)
00:1d.5 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #14 (rev f1)
00:1d.6 PCI bridge: Intel Corporation Sunrise Point-H PCI Express Root Port #15 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-H LPC Controller (rev 31)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-H PMC (rev 31)
00:1f.3 Audio device: Intel Corporation Device a171 (rev 31)
00:1f.4 SMBus: Intel Corporation Sunrise Point-H SMBus (rev 31)
01:00.0 VGA compatible controller: NVIDIA Corporation GP106M [GeForce GTX 1060] (rev a1)
3c:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd Device a804
3d:00.0 Ethernet controller: Qualcomm Atheros Device e0b1 (rev 10)
3e:00.0 Network controller: Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter (rev 32)

```

#### USB devices

 `lsusb` 
```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 1770:ff00  
Bus 001 Device 002: ID 0bda:0129 Realtek Semiconductor Corp. RTS5129 Card Reader Controller
Bus 001 Device 005: ID 5986:0547 Acer, Inc 
Bus 001 Device 004: ID 0cf3:e300 Qualcomm Atheros Communications 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

# Hardware Setup

## Special Function Keys

Onlywo keys can be remaped to use on DE, Fn+F4 (P1 key) and Fn+F5 (ECO key). Other Fn keys work out of the box, but Fn+F7 (SHIFT key) and Fn+F10 (Airplane Mode) can't be recognized.

 `Fn keys Scancodes` 
```
0xef # P1 key
0xce # ECO key

```

One method to remap it is as systemd service:

 `/etc/systemd/system/multi-user.target.wants/setp1key.service` 
```
[Unit]
Description=Setkeycode P1 Key

[Service]
Type=oneshot
ExecStart=/usr/bin/setkeycodes 0xef 202

[Install]
WantedBy=multi-user.target

```