The [Lenovo IdeaPad 720s](https://www3.lenovo.com/de/de/laptops/ideapad/700-series/Ideapad-720S-13-Intel/p/88IP70S0893#tab-techspec) is a laptop computer with a 13.3" screen, 7th or 8th generation Intel Core i5/i7 processor, webcam, microphone, audio in/out, 802.11ac wireless card with bluetooth 4.1, 1 USB Type-C (DP & Power Delivery + Thunderbold), 1 x USB Type-C (Power Delivery + USB 3.0), 2 x USB3 ports and a fingerprint reader.

## Contents

*   [1 PCI Devices](#PCI_Devices)
*   [2 USB Devices](#USB_Devices)
*   [3 Hardware Support](#Hardware_Support)
    *   [3.1 UEFI Bios](#UEFI_Bios)
    *   [3.2 Battery Conservation Mode](#Battery_Conservation_Mode)

## PCI Devices

1.  lspci

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (rev 07)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 08)
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th Gen Core Processor Gaussian Mixture Model
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 (rev 21)
00:15.1 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #1 (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Device 9d13 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Device 9d4e (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
01:00.0 Network controller: Intel Corporation Dual Band Wireless-AC 3165 Plus Bluetooth (rev 99)
02:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM961/PM961

```

## USB Devices

```
# lsusb
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 8087:0a2a Intel Corp. 
Bus 001 Device 003: ID 5986:210d Acer, Inc 
Bus 001 Device 002: ID 06cb:0081 Synaptics, Inc. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Hardware Support

The only hardware not supported is the fingerprint reader (see remarks for USB ID 06cb:0081 at [Validity90 on GitHub](https://github.com/nmikhailov/Validity90)).

### UEFI Bios

Before installing, disable Secure Boot in BIOS. The BIOS can be accessed by pressing the NOVO button on the right hand side or by pressing `F2` during boot.The boot menu can be accessed by pressing `F12`.

### Battery Conservation Mode

Lenovo laptops come with a battery controller setting called "Battery Conservation Mode", which shifts the usual loading thresholds from 95/100% to 55/60% to reduce battery degradation. To enable this, install the [acpi_call](https://www.archlinux.org/packages/?name=acpi_call) package. The mode is enabled with:

```
$ echo '\_SB.PCI0.LPCB.EC0.VPC0.SBMC 3' | sudo tee /proc/acpi/call

```

It can be disable with:

```
$ echo '\_SB.PCI0.LPCB.EC0.VPC0.SBMC 5' | sudo tee /proc/acpi/call

```