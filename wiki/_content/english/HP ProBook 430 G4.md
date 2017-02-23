| **Device** | **Working** |
| Intel graphics | Yes |
| HDMI | Not tested |
| VGA | Not tested |
| Audio | Yes |
| USB 3.0 | Yes |
| Ethernet | Not tested |
| WLAN | Yes |
| Bluetooth | Yes |
| Touchpad | Yes |
| Backlight control | Yes - only software control |
| Function keys | Yes |
| Hardware switches | Not tested |
| Card reader | Not tested |
| Webcam | Not tested |
| USB 3.0 Type-C™ port | Not tested |
| Fingerprint Reader | Not tested |

## Contents

*   [1 Device information](#Device_information)
*   [2 Backlight](#Backlight)
*   [3 ACPI errors](#ACPI_errors)
*   [4 Touchpad](#Touchpad)
*   [5 Graphic card setup](#Graphic_card_setup)
*   [6 other errors/bugs](#other_errors.2Fbugs)

## Device information

This is a work in progress with information about the HP ProBook 430 G4\. There are many configurations for these models of HP Probooks. Mine is a HP ProBook 430 G4/822C, BIOS P85 Ver. 01.03 12/05/2016, shipped with a Core i5-7200U, 8GB, 256GB SSD. I've added a 2nd 8GB memory rig and placed my old 64GB 2,5" SATA SSD into the 2nd slot. The UEFI bios allows legacy boot.

Basic information for the new [HP ProBook 430 G4](http://www.notebookcheck.net/HP-updates-the-mainstream-ProBook-400-series.174476.0.html) model. Hardware works out of the box. No configuration was needed. Information for the "Not tested" units will be posted additionally.

```
lspci -v
00:00.0 Host bridge: Intel Corporation Device 5904 (rev 02)
	Subsystem: Hewlett-Packard Company Device 822c
	Flags: bus master, fast devsel, latency 0
	Capabilities: [e0] Vendor Specific Information: Len=10 <?>

00:02.0 VGA compatible controller: Intel Corporation Device 5916 (rev 02) (prog-if 00 [VGA controller])
	Subsystem: Hewlett-Packard Company Device 822c
	Flags: bus master, fast devsel, latency 0, IRQ 129
	Memory at 1ffe000000 (64-bit, non-prefetchable) [size=16M]
	Memory at d0000000 (64-bit, prefetchable) [size=256M]
	I/O ports at 4000 [size=64]
	[virtual] Expansion ROM at 000c0000 [disabled] [size=128K]
	Capabilities: [40] Vendor Specific Information: Len=0c <?>
	Capabilities: [70] Express Root Complex Integrated Endpoint, MSI 00
	Capabilities: [ac] MSI: Enable+ Count=1/1 Maskable- 64bit-
	Capabilities: [d0] Power Management version 2
	Capabilities: [100] Process Address Space ID (PASID)
	Capabilities: [200] Address Translation Service (ATS)
	Capabilities: [300] Page Request Interface (PRI)
	Kernel driver in use: i915
	Kernel modules: i915

00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21) (prog-if 30 [XHCI])
	Subsystem: Hewlett-Packard Company Device 822c
	Flags: bus master, medium devsel, latency 0, IRQ 126
	Memory at e0300000 (64-bit, non-prefetchable) [size=64K]
	Capabilities: [70] Power Management version 2
	Capabilities: [80] MSI: Enable+ Count=1/8 Maskable- 64bit+
	Kernel driver in use: xhci_hcd
	Kernel modules: xhci_pci

00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
	Subsystem: Hewlett-Packard Company Device 822c
	Flags: bus master, fast devsel, latency 0, IRQ 18
	Memory at 1fff016000 (64-bit, non-prefetchable) [size=4K]
	Capabilities: [50] Power Management version 3
	Capabilities: [80] MSI: Enable- Count=1/1 Maskable- 64bit-
	Kernel driver in use: intel_pch_thermal
	Kernel modules: intel_pch_thermal

00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
	Subsystem: Hewlett-Packard Company Device 822c
	Flags: bus master, fast devsel, latency 0, IRQ 128
	Memory at 1fff015000 (64-bit, non-prefetchable) [size=4K]
	Capabilities: [50] Power Management version 3
	Capabilities: [8c] MSI: Enable+ Count=1/1 Maskable- 64bit+
	Kernel driver in use: mei_me
	Kernel modules: mei_me

00:17.0 SATA controller: Intel Corporation Sunrise Point-LP SATA Controller [AHCI mode] (rev 21) (prog-if 01 [AHCI 1.0])
	Subsystem: Hewlett-Packard Company Device 822c
	Flags: bus master, 66MHz, medium devsel, latency 0, IRQ 127
	Memory at e0314000 (32-bit, non-prefetchable) [size=8K]
	Memory at e0317000 (32-bit, non-prefetchable) [size=256]
	I/O ports at 4080 [size=8]
	I/O ports at 4088 [size=4]
	I/O ports at 4060 [size=32]
	Memory at e0316000 (32-bit, non-prefetchable) [size=2K]
	Capabilities: [80] MSI: Enable+ Count=1/1 Maskable- 64bit-
	Capabilities: [70] Power Management version 3
	Capabilities: [a8] SATA HBA v1.0
	Kernel driver in use: ahci
	Kernel modules: ahci

00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1) (prog-if 00 [Normal decode])
	Flags: bus master, fast devsel, latency 0, IRQ 122
	Bus: primary=00, secondary=01, subordinate=01, sec-latency=0
	I/O behind bridge: 00003000-00003fff
	Memory behind bridge: e0200000-e02fffff
	Capabilities: [40] Express Root Port (Slot+), MSI 00
	Capabilities: [80] MSI: Enable+ Count=1/1 Maskable- 64bit-
	Capabilities: [90] Subsystem: Hewlett-Packard Company Device 822c
	Capabilities: [a0] Power Management version 3
	Capabilities: [100] Advanced Error Reporting
	Capabilities: [140] Access Control Services
	Capabilities: [220] #19
	Kernel driver in use: pcieport
	Kernel modules: shpchp

00:1c.5 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #6 (rev f1) (prog-if 00 [Normal decode])
	Flags: bus master, fast devsel, latency 0, IRQ 123
	Bus: primary=00, secondary=02, subordinate=02, sec-latency=0
	Memory behind bridge: e0100000-e01fffff
	Capabilities: [40] Express Root Port (Slot+), MSI 00
	Capabilities: [80] MSI: Enable+ Count=1/1 Maskable- 64bit-
	Capabilities: [90] Subsystem: Hewlett-Packard Company Device 822c
	Capabilities: [a0] Power Management version 3
	Capabilities: [100] Advanced Error Reporting
	Capabilities: [140] Access Control Services
	Capabilities: [200] L1 PM Substates
	Capabilities: [220] #19
	Kernel driver in use: pcieport
	Kernel modules: shpchp

00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1) (prog-if 00 [Normal decode])
	Flags: bus master, fast devsel, latency 0, IRQ 124
	Bus: primary=00, secondary=03, subordinate=03, sec-latency=0
	I/O behind bridge: 00005000-00005fff
	Memory behind bridge: e0000000-e00fffff
	Prefetchable memory behind bridge: 0000001c00000000-0000001c001fffff
	Capabilities: [40] Express Root Port (Slot+), MSI 00
	Capabilities: [80] MSI: Enable+ Count=1/1 Maskable- 64bit-
	Capabilities: [90] Subsystem: Hewlett-Packard Company Device 822c
	Capabilities: [a0] Power Management version 3
	Capabilities: [100] Advanced Error Reporting
	Capabilities: [140] Access Control Services
	Capabilities: [200] L1 PM Substates
	Capabilities: [220] #19
	Kernel driver in use: pcieport
	Kernel modules: shpchp

00:1f.0 ISA bridge: Intel Corporation Device 9d58 (rev 21)
	Subsystem: Hewlett-Packard Company Device 822c
	Flags: bus master, fast devsel, latency 0

00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
	Subsystem: Hewlett-Packard Company Device 822c
	Flags: bus master, fast devsel, latency 0
	Memory at e0310000 (32-bit, non-prefetchable) [size=16K]

00:1f.3 Audio device: Intel Corporation Device 9d71 (rev 21) (prog-if 80)
	Subsystem: Hewlett-Packard Company Device 822c
	Flags: bus master, fast devsel, latency 64, IRQ 132
	Memory at 1fff010000 (64-bit, non-prefetchable) [size=16K]
	Memory at 1fff000000 (64-bit, non-prefetchable) [size=64K]
	Capabilities: [50] Power Management version 3
	Capabilities: [60] MSI: Enable+ Count=1/1 Maskable- 64bit+
	Kernel driver in use: snd_hda_intel
	Kernel modules: snd_hda_intel, snd_soc_skl

00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
	Subsystem: Hewlett-Packard Company Device 822c
	Flags: medium devsel, IRQ 16
	Memory at 1fff014000 (64-bit, non-prefetchable) [size=256]
	I/O ports at efa0 [size=32]
	Kernel driver in use: i801_smbus
	Kernel modules: i2c_i801

01:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 15)
	Subsystem: Hewlett-Packard Company Device 822c
	Flags: bus master, fast devsel, latency 0, IRQ 130
	I/O ports at 3000 [size=256]
	Memory at e0204000 (64-bit, non-prefetchable) [size=4K]
	Memory at e0200000 (64-bit, non-prefetchable) [size=16K]
	Capabilities: [40] Power Management version 3
	Capabilities: [50] MSI: Enable+ Count=1/1 Maskable- 64bit+
	Capabilities: [70] Express Endpoint, MSI 01
	Capabilities: [b0] MSI-X: Enable- Count=4 Masked-
	Capabilities: [100] Advanced Error Reporting
	Capabilities: [140] Virtual Channel
	Capabilities: [160] Device Serial Number 01-00-38-e7-e4-ff-d3-c8
	Capabilities: [170] Latency Tolerance Reporting
	Capabilities: [178] L1 PM Substates
	Kernel driver in use: r8169
	Kernel modules: r8169

02:00.0 Network controller: Intel Corporation Wireless 7265 (rev 59)
	Subsystem: Intel Corporation Dual Band Wireless-AC 7265
	Flags: bus master, fast devsel, latency 0, IRQ 131
	Memory at e0100000 (64-bit, non-prefetchable) [size=8K]
	Capabilities: [c8] Power Management version 3
	Capabilities: [d0] MSI: Enable+ Count=1/1 Maskable- 64bit+
	Capabilities: [40] Express Endpoint, MSI 00
	Capabilities: [100] Advanced Error Reporting
	Capabilities: [140] Device Serial Number 7c-b0-c2-ff-ff-33-94-6f
	Capabilities: [14c] Latency Tolerance Reporting
	Capabilities: [154] L1 PM Substates
	Kernel driver in use: iwlwifi
	Kernel modules: iwlwifi

03:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS522A PCI Express Card Reader (rev 01)
	Subsystem: Hewlett-Packard Company Device 822c
	Physical Slot: 8
	Flags: bus master, fast devsel, latency 0, IRQ 125
	Memory at e0000000 (32-bit, non-prefetchable) [size=4K]
	Capabilities: [40] Power Management version 3
	Capabilities: [50] MSI: Enable+ Count=1/1 Maskable- 64bit+
	Capabilities: [70] Express Endpoint, MSI 00
	Capabilities: [100] Advanced Error Reporting
	Capabilities: [140] Device Serial Number 00-00-00-01-00-4c-e0-00
	Capabilities: [150] Latency Tolerance Reporting
	Capabilities: [158] L1 PM Substates
	Kernel driver in use: rtsx_pci
	Kernel modules: rtsx_pci
```

## Backlight

I have not found a solution so far to control the backlight via kernel hardware control keys via kernel. So backlight control works only via software. It works out of the box under Xfce and under i3wm I use a custom command using " xbacklight -inc/-dec 10".

## ACPI errors

There are lots of acpi related error messages with kernel 4.9.x:

```
Feb 21 16:08:57 localhost kernel: ACPI Error: Field [CAP1] at 96 exceeds Buffer [NULL] size 64 (bits) (20160831/dsopcode-236)
Feb 21 16:08:57 localhost kernel: ACPI Error: Method parse/execution failed [\_SB._OSC] (Node ffff88041f8ef348), AE_AML_BUFFER_LIMIT (20
...
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Needed [Buffer/String/Package], found [Integer] ffff88041b43f750 (20160831/exresop-594)
Feb 21 16:09:01 laptop64 kernel: ACPI Exception: AE_AML_OPERAND_TYPE, While resolving operands for [OpcodeName unavailable] (20160831/ds
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WVPO] (Node ffff88041f89bcd0), AE_AML_OPERAND_TYPE
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WMPV] (Node ffff88041f89b780), AE_AML_OPERAND_TYPE
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Needed [Buffer/String/Package], found [Integer] ffff88041ce2e318 (20160831/exresop-594)
Feb 21 16:09:01 laptop64 kernel: ACPI Exception: AE_AML_OPERAND_TYPE, While resolving operands for [OpcodeName unavailable] (20160831/ds
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WVPO] (Node ffff88041f89bcd0), AE_AML_OPERAND_TYPE
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WMPV] (Node ffff88041f89b780), AE_AML_OPERAND_TYPE
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Needed [Buffer/String/Package], found [Integer] ffff88041b43f900 (20160831/exresop-594)
Feb 21 16:09:01 laptop64 kernel: ACPI Exception: AE_AML_OPERAND_TYPE, While resolving operands for [OpcodeName unavailable] (20160831/ds
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WVPO] (Node ffff88041f89bcd0), AE_AML_OPERAND_TYPE
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WMPV] (Node ffff88041f89b780), AE_AML_OPERAND_TYPE
Feb 21 16:09:01 laptop64 kernel: input: HP WMI hotkeys as /devices/virtual/input/input18
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Attempt to CreateField of length zero (20160831/dsopcode-168)
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WVPI] (Node ffff88041f89b280), AE_AML_OPERAND_VALU
Feb 21 16:09:01 laptop64 kernel: ACPI Error: Method parse/execution failed [\_SB.WMIV.WMPV] (Node ffff88041f89b780), AE_AML_OPERAND_VALU
```

## Touchpad

Middle click doesn't work so far.

## Graphic card setup

Either modesetting driver or Intel driver seem to work well. I'm using the Intel driver here. DRI3 seems to work well.

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
      Identifier  "Intel Graphics"

     #Driver      "modesetting"
     #Option      "AccelMethod"     "glamor"

      Driver      "intel"
      Option      "AccelMethod"     "sna"

     #Option      "DRI"             "2"

     Option      "Backlight"       "intel_backlight" # use your backlight that works here

EndSection
```

## other errors/bugs

```
Feb 21 16:08:58 localhost systemd-udevd[75]: Assertion '!d->current' failed at src/libsystemd/sd-event/sd-event.c:733, function event_un
...
Feb 21 16:09:01 laptop64 kernel: pcieport 0000:00:1d.0: PCIe Bus Error: severity=Corrected, type=Physical Layer, id=00e8(Receiver ID)
Feb 21 16:09:01 laptop64 kernel: pcieport 0000:00:1d.0:   device [8086:9d18] error status/mask=00000001/00002000
Feb 21 16:09:01 laptop64 kernel: pcieport 0000:00:1d.0:    [ 0] Receiver Error         (First)
```