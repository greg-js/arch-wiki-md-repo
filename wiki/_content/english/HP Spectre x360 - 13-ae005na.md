| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | iwlwifi |
| Bluetooth | Working | bluetooth |
| Audio | Partially Working | snd_hda_intel |
| Touchpad | Working |  ? |
| Touchscreen | Working | hid_multitouch |
| Pen input | Working |  ? |
| Webcam | working | uvcvideo |
| Card Reader | Working | rtsx_pci |
| Wireless Switch | Working |  ? |
| Function/Multimedia Keys | Working |  ? |
| Suspend/Resume | Working |  ? |
| Fingerprint sensor | Untested |  ? |

This article covers specific configuation of this laptop. Currently based on experience with Gnome, running on Wayland.

## Contents

*   [1 Hardware Info](#Hardware_Info)
    *   [1.1 Hardware Options](#Hardware_Options)
    *   [1.2 lspci for 13-ae005na](#lspci_for_13-ae005na)
    *   [1.3 lsusb for 13-ae005na](#lsusb_for_13-ae005na)
*   [2 Installation](#Installation)
*   [3 Issues and Further Configuration](#Issues_and_Further_Configuration)
    *   [3.1 Audio](#Audio)
    *   [3.2 Mute Button](#Mute_Button)
    *   [3.3 HiDPI](#HiDPI)
    *   [3.4 Auto Rotation](#Auto_Rotation)

## Hardware Info

### Hardware Options

This is the 2018 edition of the Spectre x360 from HP.

*   Intel i7-8550U Kaby Lake Refresh
*   8GB Ram
*   512 GB NvMe SSD
*   4K IPS touchsceen with Elantech pen
*   4 Speaker Sound
*   2 USB-C, Thunderbolt 3 Ports
*   1 USB 3
*   TPM 2
*   Synaptics Fingerprint Sensor

### lspci for 13-ae005na

```
00:00.0 Host bridge: Intel Corporation Device 5914 (rev 08)
00:02.0 VGA compatible controller: Intel Corporation Device 5917 (rev 07)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 08)
00:13.0 Non-VGA unclassified device: Intel Corporation Sunrise Point-LP Integrated Sensor Hub (rev 21)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
00:1c.1 PCI bridge: Intel Corporation Device 9d11 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1e.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO UART Controller #0 (rev 21)
00:1e.2 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO SPI Controller #0 (rev 21)
00:1f.0 ISA bridge: Intel Corporation Device 9d4e (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
01:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)
02:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)
6e:00.0 Non-Volatile memory controller: Toshiba America Info Systems Device 0115 (rev 01)

```

### lsusb for 13-ae005na

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 8087:0a2b Intel Corp. 
Bus 001 Device 002: ID 05c8:0815 Cheng Uei Precision Industry Co., Ltd (Foxlink) 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Installation

Installation is very straightfoward. You will need to disable secureboot in BIOS (ESC to bring up menu, then F10 for BIOS and/or F9 for Boot options). Using the 2018-01-01 Arch ISO and following the [installation guide](/index.php/Installation_guide "Installation guide") presented no issues.

## Issues and Further Configuration

### Audio

The laptop has a Realtek ALC295 Codec with a 4 speaker system built in. Currently only the 2 speakers on the underside of the machine will work. More information at [https://bugzilla.kernel.org/show_bug.cgi?id=189331](https://bugzilla.kernel.org/show_bug.cgi?id=189331)

### Mute Button

Most of the media keys work without configuration in Gnome, but in order to get the Mute button to function properly, you must add the following line to `/etc/modprobe.d/alsa-base.conf` (create `alsa-base.conf` if it doesn't exist) and then reboot. The button should now work and allow feedback of the mute state to Gnome, however the LED within the mute button does not illuminate.

```
options snd-hda-intel model=hp-led-gpio

```

### HiDPI

Follow [HiDPI](/index.php/HiDPI "HiDPI") for recommendations here. Gnome works out of the box, but other software may need more configuration.

### Auto Rotation

See [Tablet PC#Automatic rotation](/index.php/Tablet_PC#Automatic_rotation "Tablet PC") for common methods of achieving this. Installing [iio-sensor-proxy](https://aur.archlinux.org/packages/iio-sensor-proxy/) worked with no further configuration needed on Gnome.