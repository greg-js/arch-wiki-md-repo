At least four different versions of this laptop exist: AO1-131-C9PM and AO1-131-C620 with a 11" screen, and AO1-431-C2YR and AO1-431-C7F9 with a 14" screen. All of them also have slightly different hardware (e.g. wireless card).

## Contents

*   [1 Hardware](#Hardware)
    *   [1.1 AO1-431-C2YR](#AO1-431-C2YR)
    *   [1.2 AO1-431-C7F9 (possibly)](#AO1-431-C7F9_.28possibly.29)
    *   [1.3 AO1-431-C8G8](#AO1-431-C8G8)
    *   [1.4 BIOS configuration](#BIOS_configuration)
    *   [1.5 Kernel parameters](#Kernel_parameters)
    *   [1.6 Installation](#Installation)
*   [2 Installation (UEFI mode)](#Installation_.28UEFI_mode.29)
    *   [2.1 BIOS configuration](#BIOS_configuration_2)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 GDM](#GDM)
    *   [3.2 High load average on idle](#High_load_average_on_idle)
    *   [3.3 Bluetooth](#Bluetooth)

## Hardware

**Processor:** Intel Celeron N3050 @ 1.60GHz

**Video:** Intel Corporation Device 22b1 (rev 21)

**Audio:** Intel Corporation Device 2284 (rev 21)

### AO1-431-C2YR

| **Device** | **Working** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| Wireless | Yes |
| [Audio](/index.php/ALSA "ALSA") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| Card Reader | Yes |
| Bluetooth | Yes |

**Wireless NIC:** Qualcomm Atheros QCA9565 / AR9565 Wireless Network Adapter 802.11b/g/n (rev 01)

 `# lspci -nn` 
```
00:00.0 Host bridge [0600]: Intel Corporation Device [8086:2280] (rev 21)
00:02.0 VGA compatible controller [0300]: Intel Corporation Device [8086:22b1] (rev 21)
00:0b.0 Signal processing controller [1180]: Intel Corporation Device [8086:22dc] (rev 21)
00:14.0 USB controller [0c03]: Intel Corporation Device [8086:22b5] (rev 21)
00:1a.0 Encryption controller [1080]: Intel Corporation Device [8086:2298] (rev 21)
00:1b.0 Audio device [0403]: Intel Corporation Device [8086:2284] (rev 21)
00:1c.0 PCI bridge [0604]: Intel Corporation Device [8086:22c8] (rev 21)
00:1c.2 PCI bridge [0604]: Intel Corporation Device [8086:22cc] (rev 21)
00:1f.0 ISA bridge [0601]: Intel Corporation Device [8086:229c] (rev 21)
00:1f.3 SMBus [0c05]: Intel Corporation Device [8086:2292] (rev 21)
02:00.0 Network controller [0280]: Qualcomm Atheros QCA9565 / AR9565 Wireless Network Adapter [168c:0036] (rev 01)

```
 `# lsusb` 
```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 04ca:3014 Lite-On Technology Corp. Qualcoom Atheros Bluetooth
Bus 001 Device 003: ID 064e:9404 Suyin Corp.
Bus 001 Device 002: ID 0bda:0129 Realtek Semiconductor Corp. RTS5129 Card Reader Controller
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### AO1-431-C7F9 (possibly)

**Wireless NIC:** Intel Corporation Dual Band Wireless AC 3160 (rev 83)

 `# lspci -nn` 
```
00:00.0 Host bridge [0600]: Intel Corporation Device [8086:2280] (rev 21)
00:02.0 VGA compatible controller [0300]: Intel Corporation Device [8086:22b1] (rev 21)
00:0b.0 Signal processing controller [1180]: Intel Corporation Device [8086:22dc] (rev 21)
00:10.0 SD Host controller [0805]: Intel Corporation Device [8086:2294] (rev 21)
00:14.0 USB controller [0c03]: Intel Corporation Device [8086:22b5] (rev 21)
00:18.0 DMA controller [0801]: Intel Corporation Device [8086:22c0] (rev 21)
00:18.1 Serial bus controller [0c80]: Intel Corporation Device [8086:22c1] (rev 21)
00:1a.0 Encryption controller [1080]: Intel Corporation Device [8086:2298] (rev 21)
00:1b.0 Audio device [0403]: Intel Corporation Device [8086:2284] (rev 21)
00:1c.0 PCI bridge [0604]: Intel Corporation Device [8086:22c8] (rev 21)
00:1c.2 PCI bridge [0604]: Intel Corporation Device [8086:22cc] (rev 21)
00:1e.0 DMA controller [0801]: Intel Corporation Device [8086:2286] (rev 21)
00:1e.4 Communication controller [0780]: Intel Corporation Device [8086:228c] (rev 21)
00:1f.0 ISA bridge [0601]: Intel Corporation Device [8086:229c] (rev 21)
00:1f.3 SMBus [0c05]: Intel Corporation Device [8086:2292] (rev 21)
02:00.0 Network controller [0280]: Intel Corporation Wireless 3160 [8086:08b3] (rev 83)

```

### AO1-431-C8G8

 `# lspci -nn` 
```
00:00.0 Host bridge [0600]: Intel Corporation Device [8086:2280] (rev 21)
00:02.0 VGA compatible controller [0300]: Intel Corporation Device [8086:22b1] (rev 21)
00:0b.0 Signal processing controller [1180]: Intel Corporation Device [8086:22dc] (rev 21)
00:14.0 USB controller [0c03]: Intel Corporation Device [8086:22b5] (rev 21)
00:1a.0 Encryption controller [1080]: Intel Corporation Device [8086:2298] (rev 21)
00:1b.0 Audio device [0403]: Intel Corporation Device [8086:2284] (rev 21)
00:1c.0 PCI bridge [0604]: Intel Corporation Device [8086:22c8] (rev 21)
00:1c.2 PCI bridge [0604]: Intel Corporation Device [8086:22cc] (rev 21)
00:1f.0 ISA bridge [0601]: Intel Corporation Device [8086:229c] (rev 21)
00:1f.3 SMBus [0c05]: Intel Corporation Device [8086:2292] (rev 21)
02:00.0 Network controller [0280]: Intel Corporation Wireless 3160 [8086:08b3] (rev 83)

```
 `# lsusb` 
```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 8087:07dc Intel Corp. 
Bus 001 Device 003: ID 064e:9404 Suyin Corp. 
Bus 001 Device 002: ID 0bda:0129 Realtek Semiconductor Corp. RTS5129 Card Reader Controller
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### BIOS configuration

*   Touchpad: Basic
*   Boot Mode: Legacy
*   Boot priority order: the eMMC block device needs to have a lower boot priority than the USB bootable device.

Then save and exit.

### Kernel parameters

Without these options, the installation image will not load at all:

*   edd=off
*   noapic

Therefore these parameters needs to be added at the end of the kernel parameters' line of the boot launcher:

```
linux /vmlinuz-linux ... edd=off noapic

```

### Installation

*   Everything should function without any issues thanks to the previous kernel parameters, proceed to install the image as normal.
    *   The module for the wireless NIC is included with the kernel, so Wi-Fi works out of the box.
*   Do not forget to add **edd=off noapic** to the kernel parameters of the boot launcher's configuration file.

## Installation (UEFI mode)

No additional kernel parameters are needed.

### BIOS configuration

*   Touchpad: Basic
*   Boot Mode: UEFI
*   Boot priority order: the eMMC block device needs to have a lower boot priority than the USB bootable device.
*   Secure Boot: Disabled, or use BIOS menu to trust the Arch ISO bootloader.

Then save and exit.

## Troubleshooting

### GDM

If Gnome/GDM is installed and started, the login page will flicker up-to the point that it becomes nonfunctional. See [GDM#Use Xorg backend](/index.php/GDM#Use_Xorg_backend "GDM").

### High load average on idle

The kernel module **rtsx_usb_ms** is loaded at boot time yet is non-functional (the kernel thread associated to the module when inspecting with *top* is a zombified process) and unnecessary for the system to function. The module can safely be [blacklisted](/index.php/Blacklist "Blacklist").

### Bluetooth

At least in AO1-431-C8G8 bluetooth device is deactivated via RF-kill by default. After activating it works flawlessly with bluez.