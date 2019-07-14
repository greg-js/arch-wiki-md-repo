| **Device** | **Status** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| [Mobile internet](/index.php/ThinkPad_mobile_internet "ThinkPad mobile internet") |
| Fingerprint Sensor |
| 

1.  No working Linux driver for Fibocom L850-GL. See [this thread](https://forums.lenovo.com/t5/Linux-Discussion/X1C-gen-6-Fibocom-L850-GL-Ubuntu-18-04/m-p/4078413) and [this thread](https://forums.lenovo.com/t5/Linux-Discussion/Linux-support-for-WWAN-LTE-L850-GL-on-T580-T480/td-p/4067969) for more info.

 |

This article covers the installation and configuration of Arch Linux on a Lenovo T590 laptop. Everything seems to work pretty much out the box.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware](#Hardware)
*   [2 Graphics Card](#Graphics_Card)
*   [3 Suspend / Hibernation](#Suspend_/_Hibernation)
*   [4 TrackPoint and Touchpad](#TrackPoint_and_Touchpad)
*   [5 Power management/Throttling issues](#Power_management/Throttling_issues)
*   [6 UEFI/Firmware Updates](#UEFI/Firmware_Updates)
*   [7 UEFI booting](#UEFI_booting)
*   [8 Tools](#Tools)
    *   [8.1 Diagnostics](#Diagnostics)
*   [9 Tips and Tricks](#Tips_and_Tricks)

## Hardware

Using kernel 5.1.16-arch1-1-ARCH

```
Manufacturer: LENOVO
Product Name: 20N4CTO1WW
Version: ThinkPad T590

```

`lspci` returns:

```
00:00.0 Host bridge: Intel Corporation Device 3e34 (rev 0c)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (Whiskey Lake) (rev 02)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 0c)
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th Gen Core Processor Gaussian Mixture Model
00:12.0 Signal processing controller: Intel Corporation Cannon Point-LP Thermal Controller (rev 30)
00:14.0 USB controller: Intel Corporation Cannon Point-LP USB 3.1 xHCI Controller (rev 30)
00:14.2 RAM memory: Intel Corporation Cannon Point-LP Shared SRAM (rev 30)
00:14.3 Network controller: Intel Corporation Cannon Point-LP CNVi [Wireless-AC] (rev 30)
00:15.0 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP Serial IO I2C Controller #0 (rev 30)
00:16.0 Communication controller: Intel Corporation Cannon Point-LP MEI Controller #1 (rev 30)
00:16.3 Serial controller: Intel Corporation Device 9de3 (rev 30)
00:1c.0 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #1 (rev f0)
00:1c.4 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #5 (rev f0)
00:1d.0 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #9 (rev f0)
00:1d.4 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #13 (rev f0)
00:1f.0 ISA bridge: Intel Corporation Cannon Point-LP LPC Controller (rev 30)
00:1f.3 Audio device: Intel Corporation Cannon Point-LP High Definition Audio Controller (rev 30)
00:1f.4 SMBus: Intel Corporation Cannon Point-LP SMBus Controller (rev 30)
00:1f.5 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP SPI Controller (rev 30)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (6) I219-LM (rev 30)
01:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS522A PCI Express Card Reader (rev 01)
02:00.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
03:00.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
03:01.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
03:02.0 PCI bridge: Intel Corporation JHL6240 Thunderbolt 3 Bridge (Low Power) [Alpine Ridge LP 2016] (rev 01)
04:00.0 System peripheral: Intel Corporation JHL6240 Thunderbolt 3 NHI (Low Power) [Alpine Ridge LP 2016] (rev 01)
3a:00.0 USB controller: Intel Corporation Device 15c1 (rev 01)
3d:00.0 Non-Volatile memory controller: Intel Corporation SSDPEKNW020T8 [660p, 2TB] (rev 03)

```

`lsusb` returns:

```
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 002: ID 04f2:b604 Chicony Electronics Co., Ltd 
Bus 001 Device 003: ID 8087:0aaa Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Graphics Card

Integrated Intel graphics working out of the box. Discrete NVIDIA GeForce MX250 GDDR5 2GB not tested.

## Suspend / Hibernation

Suspend and Hibernation work out of the box.

## TrackPoint and Touchpad

Similar to the T490, the pointer occasionally jumps while pressing trackpad buttons

## Power management/Throttling issues

It is unclear if this model is affected or if current firmware has addressed the issue.

See

*   X1 Carbon Gen 6 [Power management/Throttling issues](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6)#Power_management.2FThrottling_issues "Lenovo ThinkPad X1 Carbon (Gen 6)")
*   ThinkPad T480s [Thermal Throttling Fix](/index.php/Lenovo_ThinkPad_T480s#Thermal_Throttling_Fix "Lenovo ThinkPad T480s")
*   [https://github.com/erpalma/throttled](https://github.com/erpalma/throttled)

## UEFI/Firmware Updates

Lenovo provides firmware updates for this device through the *Linux Vendor Firmware Service* (LVFS).

Available updates and changelogs can be found on the [LVFS website](https://fwupd.org/lvfs/search?value=Thinkpad+T590). These include security patches for the Intel Management Engine and the system firmware.

The updates can be installed using [fwupd](/index.php/Fwupd "Fwupd").

## UEFI booting

systemd-boot confirmed working with Secure Boot disabled

## Tools

### Diagnostics

`s-tui` ([s-tui](https://aur.archlinux.org/packages/s-tui/)): an aesthetically pleasing and useful curses-style interface that shows graphs of CPU frequency, utilization, temperature, and power consumption. It also has a built in stress tester.

`intel_gpu_top` ([intel-gpu-tools](https://www.archlinux.org/packages/?name=intel-gpu-tools)): gives you some top-like info for the integrated GPU. This can be quite useful in diagnosing GPU acceleration issues.

`powertop` ([powertop](https://www.archlinux.org/packages/?name=powertop)): provides detailed information about CPU power consumption and recommendations on how to improve it.

`tlp-stat` ([tlp](https://www.archlinux.org/packages/?name=tlp)): a much simpler alternative to remembering which `cat /sys/devices/system/*` to run in many cases. It can give very detailed, structured information about components like the battery, processor, graphics card, etc.

## Tips and Tricks