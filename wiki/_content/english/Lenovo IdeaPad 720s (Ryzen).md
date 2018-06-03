The [Lenovo IdeaPad 720s (Ryzen)](https://www3.lenovo.com/us/en/laptops/ideapad/ideapad-700-series/Ideapad-720S-13-AMD/p/88IP70S0929) is a laptop computer with a 13.3" screen, AMD Ryzen™ processor, webcam, microphone, audio in/out, 80211ac wireless card with bluetooth 4.1, 1 USB 3.0 Type-C (DP & Power Delivery), 1 x USB 3.0 Type-C (DP), 2 USB3 ports, and a fingerprint reader. The 720s is currently better supported by the linux 4.15 kernel as many things relating to it's APU are broken or only semi-working. It uses an rtl8821ce WLAN and Bluetooth chip that is not built into Linux 4.14.15.

## Contents

*   [1 PCI Devices](#PCI_Devices)
*   [2 USB Devices](#USB_Devices)
*   [3 Hardware Support](#Hardware_Support)
    *   [3.1 UEFI](#UEFI)
    *   [3.2 Video](#Video)
    *   [3.3 Sound](#Sound)
    *   [3.4 Webcam](#Webcam)
    *   [3.5 Ethernet](#Ethernet)
    *   [3.6 Wireless](#Wireless)
    *   [3.7 Touchpad](#Touchpad)
    *   [3.8 Hardware keys](#Hardware_keys)
    *   [3.9 Finger Print Reader](#Finger_Print_Reader)
    *   [3.10 ACPI annoyances](#ACPI_annoyances)

## PCI Devices

```
$ lspci
00:00.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15d0
00:00.2 IOMMU: Advanced Micro Devices, Inc. [AMD] Device 15d1
00:01.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-0fh) PCIe Dummy Host Bridge
00:01.1 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15d3
00:01.2 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15d3
00:08.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-0fh) PCIe Dummy Host Bridge
00:08.1 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15db
00:14.0 SMBus: Advanced Micro Devices, Inc. [AMD] FCH SMBus Controller (rev 61)
00:14.3 ISA bridge: Advanced Micro Devices, Inc. [AMD] FCH LPC Bridge (rev 51)
00:18.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15e8
00:18.1 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15e9
00:18.2 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15ea
00:18.3 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15eb
00:18.4 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15ec
00:18.5 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15ed
00:18.6 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15ee
00:18.7 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15ef
01:00.0 Network controller: Realtek Semiconductor Co., Ltd. RTL8821CE 802.11ac PCIe Wireless Network Adapter
02:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd Device a808
03:00.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] Radeon Vega 8 Mobile (rev c4)
03:00.1 Audio device: Advanced Micro Devices, Inc. [AMD/ATI] Device 15de
03:00.2 Encryption controller: Advanced Micro Devices, Inc. [AMD] Device 15df
03:00.3 USB controller: Advanced Micro Devices, Inc. [AMD] Device 15e0
03:00.4 USB controller: Advanced Micro Devices, Inc. [AMD] Device 15e1
03:00.5 Multimedia controller: Advanced Micro Devices, Inc. [AMD] Device 15e2
03:00.6 Audio device: Advanced Micro Devices, Inc. [AMD] Device 15e3

```

## USB Devices

```
$ lsusb
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 005: ID 06cb:0081 Synaptics, Inc. 
Bus 003 Device 004: ID 0bda:c024 Realtek Semiconductor Corp. 
Bus 003 Device 003: ID 05e3:0608 Genesys Logic, Inc. Hub
Bus 003 Device 002: ID 04f2:b5da Chicony Electronics Co., Ltd 
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Hardware Support

### UEFI

Before installing, disable [Secure Boot](/index.php/Secure_Boot "Secure Boot") in the BIOS. You can access the BIOS by pressing F2 at the Splash screen. The boot menu can also be accessed by pressing F12.

### Video

X works natively with linux 4.15-1 from testing repos and admgpu.

### Sound

Sound works with PulseAudio in linux 4.15-1 from testing repos.

### Webcam

<untested>

### Ethernet

<untested>

### Wireless

The rtl8821ce wireless driver was required in order for wireless to work properly.

### Touchpad

Works out of the box with mutli-finger scrolling on linux 4.15-1 in X.

### Hardware keys

<untested>

### Finger Print Reader

Model: <Unknown>

<untested>

### ACPI annoyances

<pci=noaer suppresses a massive amount of complaints>