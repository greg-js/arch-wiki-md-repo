| **Device** | **Status** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless](/index.php/Wireless "Wireless") | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| Smartcard Reader | Yes |

This article covers the installation and configuration of Arch Linux on a Lenovo T470s laptop.

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 bios](#bios)
*   [2 lspci and lsusb](#lspci_and_lsusb)
    *   [2.1 lspci](#lspci)
    *   [2.2 lsusb](#lsusb)
*   [3 Configuration](#Configuration)
    *   [3.1 Smartcard Reader](#Smartcard_Reader)
*   [4 See also](#See_also)

## bios

As of writing, the current bios version is 1.0.7\. By visiting the downloads section (for the type HG/HF T470s) an iso can be downloaded and burned to disk which will perform the update [[1]](http://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-t-series-laptops/thinkpad-t470s/downloads)

## lspci and lsusb

On kernel '4.11.0-rc6-mainline' via [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/) on a *20HG* T470s

### lspci

```
00:00.0 Host bridge: Intel Corporation Device 5904 (rev 02)
00:02.0 VGA compatible controller: Intel Corporation Device 5916 (rev 02)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:16.3 Serial controller: Intel Corporation Device 9d3d (rev 21)
00:1c.0 PCI bridge: Intel Corporation Device 9d10 (rev f1)
00:1c.2 PCI bridge: Intel Corporation Device 9d12 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Device 9d4e (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Device 9d71 (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (4) I219-LM (rev 21)
3a:00.0 Network controller: Intel Corporation Device 24fd (rev 78)
3c:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd Device a804

```

### lsusb

```
Bus 002 Device 003: ID 0bda:0316 Realtek Semiconductor Corp. 
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 006: ID 138a:0097 Validity Sensors, Inc. 
Bus 001 Device 005: ID 5986:111c Acer, Inc 
Bus 001 Device 008: ID 1199:9079 Sierra Wireless, Inc. 
Bus 001 Device 002: ID 058f:9540 Alcor Micro Corp. AU9540 Smartcard Reader
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Configuration

### Smartcard Reader

```
Bus 001 Device 002: ID 058f:9540 Alcor Micro Corp. AU9540 Smartcard Reader

```

## See also

*   [Lenovo Support Page](http://support.lenovo.com/us/en/products/Laptops-and-netbooks/ThinkPad-T-Series-laptops/ThinkPad-T470s?beta=false)