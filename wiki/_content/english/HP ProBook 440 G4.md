| **Device** | **Working** |
| Intel graphics | Yes |
| HDMI | Yes |
| VGA | Not tested |
| Audio | Yes |
| USB 3.0 | Yes |
| Ethernet | Yes |
| WLAN | Yes |
| Bluetooth | Yes |
| Touchpad | Yes |
| Backlight control | Yes |
| Function keys | Yes |
| Hardware switches | Yes |
| Card reader | Yes |
| Webcam | Yes |
| USB 3.0 Type-C™ port | Yes |
| Fingerprint Reader | Not tested |

## Device information

Basic information for the new [HP ProBook 440 G4](http://www.notebookcheck.net/HP-updates-the-mainstream-ProBook-400-series.174476.0.html) model. Hardware works out of the box. No configuration was needed. Information for the "Not tested" units will be posted additionally.

 `lspci -v` 
```
{{
00:00.0 Host bridge: Intel Corporation Device 5904 (rev 02)
	Subsystem: Hewlett-Packard Company Device 822e
	Flags: bus master, fast devsel, latency 0
	Capabilities: <access denied>

00:02.0 VGA compatible controller: Intel Corporation Device 5916 (rev 02) (prog-if 00 [VGA controller])
	Subsystem: Hewlett-Packard Company Device 822e
	Flags: bus master, fast devsel, latency 0, IRQ 129
	Memory at 1ffe000000 (64-bit, non-prefetchable) [size=16M]
	Memory at d0000000 (64-bit, prefetchable) [size=256M]
	I/O ports at 4000 [size=64]
	[virtual] Expansion ROM at 000c0000 [disabled] [size=128K]
	Capabilities: <access denied>
	Kernel driver in use: i915
	Kernel modules: i915

00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21) (prog-if 30 [XHCI])
	Subsystem: Hewlett-Packard Company Device 822e
	Flags: bus master, medium devsel, latency 0, IRQ 127
	Memory at e0300000 (64-bit, non-prefetchable) [size=64K]
	Capabilities: <access denied>
	Kernel driver in use: xhci_hcd
	Kernel modules: xhci_pci

00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
	Subsystem: Hewlett-Packard Company Device 822e
	Flags: fast devsel, IRQ 18
	Memory at 1fff016000 (64-bit, non-prefetchable) [size=4K]
	Capabilities: <access denied>
	Kernel driver in use: intel_pch_thermal
	Kernel modules: intel_pch_thermal

00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
	Subsystem: Hewlett-Packard Company Device 822e
	Flags: bus master, fast devsel, latency 0, IRQ 128
	Memory at 1fff015000 (64-bit, non-prefetchable) [size=4K]
	Capabilities: <access denied>
	Kernel driver in use: mei_me
	Kernel modules: mei_me

00:17.0 SATA controller: Intel Corporation Sunrise Point-LP SATA Controller [AHCI mode] (rev 21) (prog-if 01 [AHCI 1.0])
	Subsystem: Hewlett-Packard Company Device 822e
	Flags: bus master, 66MHz, medium devsel, latency 0, IRQ 126
	Memory at e0314000 (32-bit, non-prefetchable) [size=8K]
	Memory at e0317000 (32-bit, non-prefetchable) [size=256]
	I/O ports at 4080 [size=8]
	I/O ports at 4088 [size=4]
	I/O ports at 4060 [size=32]
	Memory at e0316000 (32-bit, non-prefetchable) [size=2K]
	Capabilities: <access denied>
	Kernel driver in use: ahci
	Kernel modules: ahci

00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1) (prog-if 00 [Normal decode])
	Flags: bus master, fast devsel, latency 0, IRQ 122
	Bus: primary=00, secondary=01, subordinate=01, sec-latency=0
	I/O behind bridge: 00003000-00003fff
	Memory behind bridge: e0200000-e02fffff
	Capabilities: <access denied>
	Kernel driver in use: pcieport
	Kernel modules: shpchp

00:1c.5 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #6 (rev f1) (prog-if 00 [Normal decode])
	Flags: bus master, fast devsel, latency 0, IRQ 123
	Bus: primary=00, secondary=02, subordinate=02, sec-latency=0
	Memory behind bridge: e0100000-e01fffff
	Capabilities: <access denied>
	Kernel driver in use: pcieport
	Kernel modules: shpchp

00:1d.0 PCI bridge: Intel Corporation Device 9d18 (rev f1) (prog-if 00 [Normal decode])
	Flags: bus master, fast devsel, latency 0, IRQ 124
	Bus: primary=00, secondary=03, subordinate=03, sec-latency=0
	I/O behind bridge: 00005000-00005fff
	Memory behind bridge: e0000000-e00fffff
	Prefetchable memory behind bridge: 0000001c00000000-0000001c001fffff
	Capabilities: <access denied>
	Kernel driver in use: pcieport
	Kernel modules: shpchp

00:1f.0 ISA bridge: Intel Corporation Device 9d58 (rev 21)
	Subsystem: Hewlett-Packard Company Device 822e
	Flags: bus master, fast devsel, latency 0

00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
	Subsystem: Hewlett-Packard Company Device 822e
	Flags: fast devsel
	Memory at e0310000 (32-bit, non-prefetchable) [disabled] [size=16K]

00:1f.3 Audio device: Intel Corporation Device 9d71 (rev 21) (prog-if 80)
	Subsystem: Hewlett-Packard Company Device 822e
	Flags: bus master, fast devsel, latency 64, IRQ 132
	Memory at 1fff010000 (64-bit, non-prefetchable) [size=16K]
	Memory at 1fff000000 (64-bit, non-prefetchable) [size=64K]
	Capabilities: <access denied>
	Kernel driver in use: snd_hda_intel
	Kernel modules: snd_hda_intel, snd_soc_skl

00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
	Subsystem: Hewlett-Packard Company Device 822e
	Flags: medium devsel, IRQ 16
	Memory at 1fff014000 (64-bit, non-prefetchable) [size=256]
	I/O ports at efa0 [size=32]
	Kernel driver in use: i801_smbus
	Kernel modules: i2c_i801

01:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 15)
	Subsystem: Hewlett-Packard Company Device 822e
	Flags: bus master, fast devsel, latency 0, IRQ 131
	I/O ports at 3000 [size=256]
	Memory at e0204000 (64-bit, non-prefetchable) [size=4K]
	Memory at e0200000 (64-bit, non-prefetchable) [size=16K]
	Capabilities: <access denied>
	Kernel driver in use: r8169
	Kernel modules: r8169

02:00.0 Network controller: Intel Corporation Wireless 7265 (rev 59)
	Subsystem: Intel Corporation Dual Band Wireless-AC 7265
	Flags: bus master, fast devsel, latency 0, IRQ 130
	Memory at e0100000 (64-bit, non-prefetchable) [size=8K]
	Capabilities: <access denied>
	Kernel driver in use: iwlwifi
	Kernel modules: iwlwifi

03:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS522A PCI Express Card Reader (rev 01)
	Subsystem: Hewlett-Packard Company Device 822e
	Physical Slot: 8
	Flags: bus master, fast devsel, latency 0, IRQ 125
	Memory at e0000000 (32-bit, non-prefetchable) [size=4K]
	Capabilities: <access denied>
	Kernel driver in use: rtsx_pci
	Kernel modules: rtsx_pci
}}

```