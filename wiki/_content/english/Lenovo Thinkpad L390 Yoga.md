| **Device** | **Status** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |
| Fingerprint Sensor | No |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |

## Hardware

Using kernel 5.2.11.

```
Release Date: 07/29/2019
Product Name: 20NUS01W00
SKU Number: LENOVO_MT_20NU_BU_Think_FM_ThinkPad L390

```

`lspci` returns:

```
00:00.0 Host bridge: Intel Corporation Device 3e34 (rev 0c)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (Whiskey Lake) (rev 02)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 0c)
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th Gen Core Processor Gaussian Mixture Model
00:12.0 Signal processing controller: Intel Corporation Cannon Point-LP Thermal Controller (rev 11)
00:13.0 Serial controller: Intel Corporation Cannon Point-LP Integrated Sensor Hub (rev 11)
00:14.0 USB controller: Intel Corporation Cannon Point-LP USB 3.1 xHCI Controller (rev 11)
00:14.2 RAM memory: Intel Corporation Cannon Point-LP Shared SRAM (rev 11)
00:14.3 Network controller: Intel Corporation Cannon Point-LP CNVi [Wireless-AC] (rev 11)
00:15.0 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP Serial IO I2C Controller #0 (rev 11)
00:15.1 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP Serial IO I2C Controller #1 (rev 11)
00:15.2 Serial bus controller [0c80]: Intel Corporation Device 9dea (rev 11)
00:16.0 Communication controller: Intel Corporation Cannon Point-LP MEI Controller #1 (rev 11)
00:1d.0 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #9 (rev f1)
00:1d.4 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #13 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Cannon Point-LP LPC Controller (rev 11)
00:1f.3 Audio device: Intel Corporation Cannon Point-LP High Definition Audio Controller (rev 11)
00:1f.4 SMBus: Intel Corporation Cannon Point-LP SMBus Controller (rev 11)
00:1f.5 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP SPI Controller (rev 11)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (6) I219-V (rev 11)
03:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM981/PM981/PM983
04:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS522A PCI Express Card Reader (rev 01)

```

`lsusb` returns:

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 06cb:00a2 Synaptics, Inc. 
Bus 001 Device 003: ID 056a:5158 Wacom Co., Ltd Pen and multitouch sensor
Bus 001 Device 002: ID 04ca:7070 Lite-On Technology Corp. Integrated Camera
Bus 001 Device 005: ID 8087:0aaa Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### Fingerprint reader

Fingerprint sensor 06cb:002a is not supported by libfprint right now. There is a github issue to reverse engineer the driver - [https://github.com/nmikhailov/Validity90/issues/47](https://github.com/nmikhailov/Validity90/issues/47) .