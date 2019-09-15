| **Device** | **Working** | **Modules** |
| Intel graphics | Yes | i915 |
| HDMI | Not tested | - |
| Audio | Yes | snd_hda_intel |
| USB 3.0 | Yes | - |
| Ethernet | Yes | r8169 |
| Wireless | Yes | rtl8723be |
| Bluetooth | Yes | bluetooth |
| Touchpad | Yes | psmouse |
| Backlight control | Yes | - |
| Function keys | Yes | - |
| Card reader | Yes | - |
| Webcam | Yes | uvcvideo |

This article covers specific configuration of this laptop.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware Info](#Hardware_Info)
    *   [1.1 Hardware Options](#Hardware_Options)
    *   [1.2 lspci for 15-ab214nt](#lspci_for_15-ab214nt)
    *   [1.3 lsusb for 15-ab214nt](#lsusb_for_15-ab214nt)
*   [2 Notes](#Notes)
    *   [2.1 Installation](#Installation)
    *   [2.2 Dual boot (with Windows)](#Dual_boot_(with_Windows))
    *   [2.3 Bluetooth](#Bluetooth)
    *   [2.4 Camera](#Camera)
    *   [2.5 Function keys](#Function_keys)
    *   [2.6 Hybrid Graphics](#Hybrid_Graphics)
    *   [2.7 Hpfall](#Hpfall)
    *   [2.8 Sensors](#Sensors)
    *   [2.9 Secure Boot](#Secure_Boot)
    *   [2.10 Other](#Other)

## Hardware Info

### Hardware Options

This is the 2015 Pavilion 15-ab214nt

*   Intel i5-6200U (Skylake)
*   8GB RAM
*   Nvidia GeForce 940M
*   1TB SATA HDD (WD)
*   1366x768 LED Display (LG)
*   Dual Speakers
*   2 USB 3.0, single USB 2, HDMI output, SD Card port, Ethernet port, A optical disk drive and an audio jack

### lspci for 15-ab214nt

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation Skylake GT2 [HD Graphics 520] (rev 07)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 08)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:17.0 SATA controller: Intel Corporation Sunrise Point-LP SATA Controller [AHCI mode] (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
00:1c.5 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #6 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-LP LPC Controller (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
01:00.0 3D controller: NVIDIA Corporation GM108M [GeForce 940M] (rev a2)
02:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS522A PCI Express Card Reader (rev 01)
03:00.0 Network controller: Realtek Semiconductor Co., Ltd. RTL8723BE PCIe Wireless Network Adapter
04:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL810xE PCI Express Fast Ethernet controller (rev 0a)

```

### lsusb for 15-ab214nt

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 0bda:b006 Realtek Semiconductor Corp. Bluetooth Radio
Bus 001 Device 003: ID 0408:50b0 Quanta Computer, Inc. HP Truevision HD
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Notes

### Installation

You have to disable Secure Boot. repeatedly press F10 during boot to bring up the BIOS setup, navigate to the boot section and disable Secure Boot.

To prevent the system from booting in Legacy mode, i also recommend to disable CSM/Legacy mode

Before booting, you need to put `pci=nomsi` as a [kernel parameter](/index.php/Kernel_parameters#Parameter_list "Kernel parameters"), or there will be an infinite amount of PCI bus error's and the system will hang during or after boot. Don't forget to put it after the installation too.

### Dual boot (with Windows)

Works fine. Shrink the Windows partition from Windows first, then install Linux on the free space.

### Bluetooth

Works out of the box.

### Camera

The camera is detected and works out of the box.

### Function keys

All function keys work, the mute LED also works.

### Hybrid Graphics

Works with [PRIME](/index.php/PRIME "PRIME") GPU Offloading with nouveau, and Reverse PRIME with the proprietary NVIDIA drivers.

### Hpfall

Installed [hpfall-git](https://aur.archlinux.org/packages/hpfall-git/), followed [Hpfall](/index.php/Hpfall "Hpfall") and tested it, works great.

### Sensors

```
pch_skylake-virtual-0
Adapter: Virtual device
temp1:        +48.0°C

coretemp-isa-0000
Adapter: ISA adapter
Package id 0:  +50.0°C  (high = +100.0°C, crit = +100.0°C)
Core 0:        +50.0°C  (high = +100.0°C, crit = +100.0°C)
Core 1:        +50.0°C  (high = +100.0°C, crit = +100.0°C)

nouveau-pci-0100
Adapter: PCI adapter
GPU core:     +0.90 V  (min =  +0.60 V, max =  +1.20 V)

acpitz-acpi-0
Adapter: ACPI interface
temp1:        +51.0°C
```

### Secure Boot

[Secure Boot](/index.php/Secure_Boot "Secure Boot"), if set properly works with [GRUB](/index.php/GRUB "GRUB") and [shim](/index.php/Secure_Boot#shim "Secure Boot").

UEFI on this laptop is a bit on the broken side, i do not recommend anyone to play with it too much.

### Other

On previous kernels, some ACPI errors, although not harmful, were logged at boot. But on recent kernels this seems to be fixed.

If the boot entry for Linux is gone (because of a Windows or a BIOS update), repeatedly press F9 after pressing the power button, navigate and select "Boot from EFI file", then select the .efi file of your boot manager.

The system will not allow changing to boot order when there is BIOS administrator password set.

While trying to get Secure Boot with [rEFInd](/index.php/REFInd "REFInd") working, i have permanently broken something and the laptop refuses to boot the rEFInd from the boot order now. It will delete the entry even if Secure Boot is off.