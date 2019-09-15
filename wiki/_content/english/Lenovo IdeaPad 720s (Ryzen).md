The [Lenovo IdeaPad 720s (Ryzen)](https://www3.lenovo.com/us/en/laptops/ideapad/ideapad-700-series/Ideapad-720S-13-AMD/p/88IP70S0929) is a laptop computer with a 13.3" screen, AMD Ryzen™ processor, webcam, microphone, audio in/out, 80211ac wireless card with bluetooth 4.1, 1 USB 3.0 Type-C (DP & Power Delivery), 1 x USB 3.0 Type-C (DP), 2 USB3 ports, and a fingerprint reader.

CPU/APU-wise, Linux support for the 720s is in decent shape since kernel ~4.15 (CPU and GPU temperatures per [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors)); the more recent the better. Its rtl8821ce WLAN and Bluetooth chip has no mainlined driver (as of 4.17), but [rtl8821ce-dkms-git](https://aur.archlinux.org/packages/rtl8821ce-dkms-git/) comes to rescue here.

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
    *   [3.8 Hardware keys](#Hardware_keys)
    *   [3.9 Finger Print Reader](#Finger_Print_Reader)
    *   [3.10 ACPI annoyances](#ACPI_annoyances)
    *   [3.11 CPU soft lockup](#CPU_soft_lockup)
    *   [3.12 See also](#See_also)

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

X works natively with a current [linux](https://www.archlinux.org/packages/?name=linux) and [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu).

If you are having video issues with only the [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) installed, also install the AMD PRO package [amdgpu-pro-libgl](https://aur.archlinux.org/packages/amdgpu-pro-libgl/). See [AMDGPU](/index.php/AMDGPU "AMDGPU")

### Sound

Sound works with PulseAudio in linux 4.15-1 from testing repos.

### Webcam

Chicony EasyCamera (USB)

Works out of the box on linux 4.19.12.

### Ethernet

(No RJ45, use any working USB (A or C) dongle.)

### Wireless

The [rtl8821ce-dkms-git](https://aur.archlinux.org/packages/rtl8821ce-dkms-git/) wireless driver is required in order for WiFi and Bluetooth to work.

Sometimes upon reboot, rfkill may block wireless communications. To unblock, run : `rfkill unblock all`.

Active bluetooth may lock up the PC on lid close/suspend, then `rfkill block bluetooth`.

### Touchpad

Works out of the box with mutli-finger scrolling on linux 4.15-1 in X.

### Hardware keys

No dedicated keys. The Fn functions on the F{1..12} keys are correctly recognised by X11 and work out of the box (Touchpad on/off etc.). Fn state can be inverted in the BIOS menu.

### Finger Print Reader

Model: <Unknown>

<untested>

### ACPI annoyances

ttys get filled with massive amounts of ACPI complaints, and are unusable as such. Mitigate by passing the `pci=noaer` kernel commandline option.

### CPU soft lockup

The mwait cpu instruction can cause a CPU soft lockup.

To fix the issue, add `idle=nomwait` to kernel parameters.

### See also

*   [Random Freeze on Ryzen 2500U using amdgpu driver](https://bugzilla.redhat.com/show_bug.cgi?id=1562530)