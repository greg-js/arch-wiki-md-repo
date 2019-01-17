The [RDP Thinbook 1310](https://www.rdp.online/budget-laptops) is an 11.6 inch budget, lightweight, Cherry Trail based laptop by [RDP](https://www.rdp.in/), an India based company. It comes with an Intel Atom x5-Z8350, paired with either 2 or 4GB of RAM, a 32GB internal eMMC, a 1366x768 11.6 inch screen and weighs 1.2 kilograms.

**Note:** All the original work to get great Linux support on this device was done by [Sundar Nagarajan](https://github.com/sundarnagarajan/rdp-thinbook-linux).

| **Device** | **Status** | **Modules** |
| Display | Working | xf86-video-intel |
| Wireless | Working | rtl8723bs |
| Touchpad | Working | libinput |
| Battery Status | Working |
| Camera | Working |
| Bluetooth | Working |
| MicroSD Reader | Not Tested |
| Power Management | Seems Fine |
| Lid/Keyboard | Working |

## Contents

*   [1 Hardware Information](#Hardware_Information)
    *   [1.1 lspci](#lspci)
    *   [1.2 lsusb](#lsusb)
    *   [1.3 Wireless Networking](#Wireless_Networking)
    *   [1.4 Bluetooth](#Bluetooth)
    *   [1.5 CPU](#CPU)
    *   [1.6 HDMI Out](#HDMI_Out)
    *   [1.7 Audio](#Audio)
    *   [1.8 Touch Pad](#Touch_Pad)
    *   [1.9 Webcam](#Webcam)
    *   [1.10 Storage](#Storage)
    *   [1.11 RAM](#RAM)
    *   [1.12 Battery](#Battery)
    *   [1.13 I/O Ports](#I/O_Ports)
    *   [1.14 Software Information](#Software_Information)

## Hardware Information

### lspci

```

00:00.0 Host bridge: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series SoC Transaction Register (rev 36)
00:02.0 VGA compatible controller: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series PCI Configuration Registers (rev 36)
00:03.0 Multimedia controller: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series Imaging Unit (rev ff)
00:0b.0 Signal processing controller: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series Power Management Controller (rev 36)
00:14.0 USB controller: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series USB xHCI Controller (rev 36)
00:1a.0 Encryption controller: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series Trusted Execution Engine (rev 36)
00:1f.0 ISA bridge: Intel Corporation Atom/Celeron/Pentium Processor x5-E8000/J3xxx/N3xxx Series PCU (rev 36)

```

### lsusb

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 058f:5608 Alcor Micro Corp. 
Bus 001 Device 006: ID 05e3:0718 Genesys Logic, Inc. IDE/SATA Adapter
Bus 001 Device 004: ID 05e3:0608 Genesys Logic, Inc. Hub
Bus 001 Device 003: ID 258a:000c  
Bus 001 Device 002: ID 0781:5567 SanDisk Corp. Cruzer Blade
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### Wireless Networking

[Wireless](/index.php/Wireless "Wireless") works out of the box since 4.12-rc1, when the rtl8723bs drivers were merged into the kernel staging tree. The device supports 802.11 b/g/n.

**Note:** Monitor / Promiscuous mode has not been tested yet.

**Note:** Wireless may not work after resuming from suspend.

### Bluetooth

[Bluetooth](/index.php/Bluetooth "Bluetooth") works out of the box.

### CPU

Intel(R) Atom(TM) x5-Z8350 CPU @ 1.44GHz

### HDMI Out

The laptop has a Mini-HDMI Output Port.

**Note:** HDMI has not been tested yet.

### Audio

If there is no audio output, the default output sink has to be changed. This can be done in [PulseAudio](/index.php/PulseAudio "PulseAudio") by running:

```
pactl set-default-sink alsa_output.platform-bytcht_es8316.HiFi__hw_bytchtes8316__sink

```

### Touch Pad

The [libinput](/index.php/Libinput "Libinput") library supports the touchpad.

**Note:** Multitouch and gestures has not been tested yet.

### Webcam

The 0.3MP webcam works out of the box.

### Storage

A 32GB eMMC is built in to the device. A 2.5" HDD/SSD expansion slot is available. Also, a microSD Card Slot is there, but the firmware doesn't allow booting from an SD card.

### RAM

Maximum RAM Supported is 8GB. The 4GB RAM model comes with a single SK Hynix 1066 MHz DDR3 Module built in. Another empty slot is available.

### Battery

A 10,000 mAh is provided with the laptop.

### I/O Ports

1x microSD Card Slot, 1x USB 2.0, 1x USB3.0, 1x 3.5mm jack, 1x Mini HDMI, 1x Power Port

### Software Information

The laptop comes with Windows 10 pre-installed. When the RDP logo appears on boot, press Escape to enter the UEFI Settings. The boot order can be changed to prioritize the external USB, from which Arch Linux can be installed.