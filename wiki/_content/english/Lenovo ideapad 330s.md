The [Lenovo IdeaPad 330s (Ryzen)](https://www.notebookcheck.net/Lenovo-IdeaPad-330-15-Ryzen-5-2500U-Laptop-Review.329434.0.html) is a laptop computer with a 15" screen, AMD Ryzen™ 2500U processor.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

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

## PCI Devices

```
$ lspci
00:00.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 15d0
00:00.2 IOMMU: Advanced Micro Devices, Inc. [AMD] Device 15d1
00:01.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-0fh) PCIe Dummy Host Bridge
00:01.2 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15d3
00:01.3 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15d3
00:08.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Family 17h (Models 00h-0fh) PCIe Dummy Host Bridge
00:08.1 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15db
00:08.2 PCI bridge: Advanced Micro Devices, Inc. [AMD] Device 15dc
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
01:00.0 Network controller: Qualcomm Atheros QCA9377 802.11ac Wireless Network Adapter (rev 31)
02:00.0 SD Host controller: O2 Micro, Inc. SD/MMC Card Reader Controller (rev 01)
03:00.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] Raven Ridge [Radeon Vega Series / Radeon Vega Mobile Series] (rev c4)
03:00.1 Audio device: Advanced Micro Devices, Inc. [AMD/ATI] Device 15de
03:00.2 Encryption controller: Advanced Micro Devices, Inc. [AMD] Device 15df
03:00.3 USB controller: Advanced Micro Devices, Inc. [AMD] Device 15e0
03:00.4 USB controller: Advanced Micro Devices, Inc. [AMD] Device 15e1
03:00.5 Multimedia controller: Advanced Micro Devices, Inc. [AMD] Device 15e2
03:00.6 Audio device: Advanced Micro Devices, Inc. [AMD] Device 15e3
04:00.0 SATA controller: Advanced Micro Devices, Inc. [AMD] FCH SATA Controller [AHCI mode] (rev 61)

```

## USB Devices

```
$ lsusb
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 003: ID 0cf3:e500 Qualcomm Atheros Communications 
Bus 003 Device 002: ID 5986:2115 Acer, Inc 
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Hardware Support

### UEFI

Before installing, disable [Secure Boot](/index.php/Secure_Boot "Secure Boot") in the BIOS. You can access the BIOS by pressing F2 at the Splash screen. The boot menu can also be accessed by pressing F12.

### Video

X works natively with a current [linux](https://www.archlinux.org/packages/?name=linux) and [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu).

### Sound

Sound works.

### Webcam

Works out of the box.

### Ethernet

(No RJ45, use any working USB (A or C) dongle.)

### Wireless

Wi-Fi and Bluetooth work.

### Touchpad

Doesn't work by default and prevents the system from booting. Add `ivrs_ioapic[32]=00:14.0` to the kernel command line arguments to make it work, and to be able to boot. You need to add this parameter to the kernel command line arguments for the live image as well.