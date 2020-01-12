| **Device** | **Status** | **Modules** |
| Intel UHD 630 Graphics | Working | i915 |
| NVIDIA Quadro T1000/T2000 | Working | nvidia |
| Intel AX200 Wifi | Working | iwlwifi |
| Intel HDA | Working | snd_hda_intel |
| Synaptics touchpad | Working | libinput |
| Chicony Electronics | Working | uvcvideo |
| Card reader | Unknown | xhci_hcd |
| Intel AX200 Bluetooth | Working | btusb |
| Intel Thunderbolt | Unknown | thunderbolt |
| Synaptics fingerprint reader | Experimental |

The [[1]](https://www.lenovo.com/us/en/laptops/thinkpad/thinkpad-p/P1-Gen-2/p/22WS2WPP102) is a thin-and-light 15.6" workstation/multimedia laptop from Lenovo's 2019 ThinkPad P lineup.

The P1 (Gen 2) is very similar to the [Lenovo ThinkPad X1 Extreme (Gen 2)](/index.php/Lenovo_ThinkPad_X1_Extreme_(Gen_2) "Lenovo ThinkPad X1 Extreme (Gen 2)"), please look there.

## lspci

`lspci` returns this on P1 Gen 2 model 20QT:

```
00:00.0 Host bridge: Intel Corporation Device 3e20 (rev 0d)
00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor PCIe Controller (x16) (rev 0d)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 630 (Mobile) (rev 02)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 0d) 
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th/8th Gen Core Processor Gaussian Mixture Model 
00:12.0 Signal processing controller: Intel Corporation Cannon Lake PCH Thermal Controller (rev 10) 
00:14.0 USB controller: Intel Corporation Cannon Lake PCH USB 3.1 xHCI Host Controller (rev 10) 
00:14.2 RAM memory: Intel Corporation Cannon Lake PCH Shared SRAM (rev 10)
00:15.0 Serial bus controller [0c80]: Intel Corporation Cannon Lake PCH Serial IO I2C Controller #0 (rev 10) 
00:16.0 Communication controller: Intel Corporation Cannon Lake PCH HECI Controller (rev 10) 
00:1b.0 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port #17 (rev f0)
00:1b.4 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port #21 (rev f0)
00:1c.0 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port #1 (rev f0)
00:1d.0 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port #9 (rev f0)
00:1d.6 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port #15 (rev f0)
00:1e.0 Communication controller: Intel Corporation Device a328 (rev 10)
00:1f.0 ISA bridge: Intel Corporation Device a30e (rev 10)
00:1f.3 Audio device: Intel Corporation Cannon Lake PCH cAVS (rev 10)
00:1f.4 SMBus: Intel Corporation Cannon Lake PCH SMBus Controller (rev 10)
00:1f.5 Serial bus controller [0c80]: Intel Corporation Cannon Lake PCH SPI Controller (rev 10)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (7) I219-LM (rev 10)
01:00.0 VGA compatible controller: NVIDIA Corporation TU117GLM [Quadro T2000 Mobile / Max-Q] (rev a1)
01:00.1 Audio device: NVIDIA Corporation Device 10fa (rev a1)
02:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM981/PM981/PM983
52:00.0 Network controller: Intel Corporation Wi-Fi 6 AX200 (rev 1a)
53:00.0 SD Host controller: Genesys Logic, Inc Device 9755

```

## lsusb

`lsusb` returns something like this on P1 Gen 2 model 20QT:

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 06cb:00bd Synaptics, Inc.
Bus 001 Device 002: ID 04f2:b67c Chicony Electronics Co., Ltd Integrated Camera
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```