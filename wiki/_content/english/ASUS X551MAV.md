## Contents

*   [1 Model](#Model)
*   [2 Hardware](#Hardware)
    *   [2.1 lspci](#lspci)
    *   [2.2 lsusb](#lsusb)
    *   [2.3 lshw](#lshw)
    *   [2.4 LCD Panel information](#LCD_Panel_information)
*   [3 Settings](#Settings)
    *   [3.1 Video](#Video)
    *   [3.2 LAN](#LAN)
    *   [3.3 Wi-fi](#Wi-fi)
    *   [3.4 Audio](#Audio)
    *   [3.5 Touchpad](#Touchpad)
    *   [3.6 Brightness](#Brightness)
    *   [3.7 Webcam](#Webcam)
    *   [3.8 Card Reader](#Card_Reader)
*   [4 Dual boot with Windows](#Dual_boot_with_Windows)
*   [5 Slowdown on 4.x kernels](#Slowdown_on_4.x_kernels)

## Model

X551MAV-EB01-B

It is very similar to the X551MA, but lacks an optical drive, uses an Atheros Wifi chip, and lacks built-in Bluetooth support.

## Hardware

*   Platform: Bay Trail M (Atom)
*   CPU: Intel(R) Pentium(R) CPU N2830 @ 2.16GHz (dual core)
*   RAM: DDR3 1333MHz 4096 MB
*   VIDEO: Intel GMA HD (Bay Trail -- essentially mobile Ivy Bridge).
*   SCREEN: AU Optronics B156XTN02.0 15.6" TFT LCD panel, native/max resolution 1366x768.
*   HDD: 500 GB 5400RPM SATA
*   Wi-fi: Qualcomm AR9485 Wireless Network Adapter
*   Network: Realtek Semiconductor Co., Ltd. RTL8101/2/6E PCI Express Fast/Gigabit Ethernet controller (rev 06)
*   1xUSB 2.0, 1xUSB 3.0, 1xHDMI, 1xSVGA, 1xEthernet, Cardreader, Camera

### lspci

```
00:00.0 Host bridge: Intel Corporation Atom Processor Z36xxx/Z37xxx Series SoC Transaction Register (rev 0e)
00:02.0 VGA compatible controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Graphics & Display (rev 0e)
00:13.0 SATA controller: Intel Corporation Atom Processor E3800 Series SATA AHCI Controller (rev 0e)
00:1a.0 Encryption controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Trusted Execution Engine (rev 0e)
00:1b.0 Audio device: Intel Corporation Atom Processor Z36xxx/Z37xxx Series High Definition Audio Controller (rev 0e)
00:1c.0 PCI bridge: Intel Corporation Atom Processor E3800 Series PCI Express Root Port 1 (rev 0e)
00:1c.1 PCI bridge: Intel Corporation Atom Processor E3800 Series PCI Express Root Port 2 (rev 0e)
00:1c.3 PCI bridge: Intel Corporation Atom Processor E3800 Series PCI Express Root Port 4 (rev 0e)
00:1d.0 USB controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series USB EHCI (rev 0e)
00:1f.0 ISA bridge: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Power Control Unit (rev 0e)
00:1f.3 SMBus: Intel Corporation Atom Processor E3800 Series SMBus Controller (rev 0e)
02:00.0 Network controller: Qualcomm Atheros AR9485 Wireless Network Adapter (rev 01)
03:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5286 PCI Express Card Reader (rev 01)
03:00.2 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8101/2/6E PCI Express Fast/Gigabit Ethernet controller (rev 06)

```

### lsusb

```
Bus 001 Device 004: ID 0bda:57b5 Realtek Semiconductor Corp. 
Bus 001 Device 002: ID 8087:07e6 Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

### lshw

```
asus
    description: Notebook
    product: X551MA (ASUS-NotebookSKU)
    vendor: ASUSTeK COMPUTER INC.
    version: 1.0
    serial: EAN0CX600827439
    width: 4294967295 bits
    capabilities: smbios-2.8 dmi-2.8 smp vsyscall32
    configuration: boot=normal chassis=notebook family=X sku=ASUS-NotebookSKU uuid=E971900C-B843-4FDB-955C-382C4A827762
  *-core
       description: Motherboard
       product: X551MA
       vendor: ASUSTeK COMPUTER INC.
       physical id: 0
       version: 1.0
       serial: BSN12345678901234567
       slot: MIDDLE
     *-firmware
          description: BIOS
          vendor: American Megatrends Inc.
          physical id: 0
          version: X551MA.513
          date: 09/09/2014
          size: 64KiB
          capacity: 960KiB
          capabilities: pci upgrade shadowing cdboot bootselect socketedrom edd int13floppy1200 int13floppy720 int13floppy2880 int5printscreen int9keyboard int14serial int17printer acpi usb smartbattery biosbootspecification uefi
     *-memory
          description: System Memory
          physical id: b
          slot: System board or motherboard
          size: 4GiB
        *-bank:0
             description: DIMM DDR3 1333 MHz (0.8 ns)
             product: ASU16D3LS1KBG/4G
             vendor: Kingston
             physical id: 0
             serial: E4085AA8
             slot: A1_DIMM0
             size: 4GiB
             width: 64 bits
             clock: 1333MHz (0.8ns)
        *-bank:1
             description: DIMM [empty]
             product: Array1_PartNumber1
             vendor: A1_Manufacturer1
             physical id: 1
             serial: A1_SerNum1
             slot: A1_DIMM1
     *-cache:0
          description: L1 cache
          physical id: 12
          slot: CPU Internal L1
          size: 112KiB
          capacity: 112KiB
          capabilities: internal write-back
          configuration: level=1
     *-cache:1
          description: L2 cache
          physical id: 13
          slot: CPU Internal L2
          size: 1MiB
          capacity: 1MiB
          capabilities: internal write-back unified
          configuration: level=2
     *-cpu
          description: CPU
          product: Intel(R) Celeron(R) CPU  N2830  @ 2.16GHz
          vendor: Intel Corp.
          physical id: 14
          bus info: cpu@0
          version: Intel(R) Celeron(R) CPU N2830 @ 2.16GHz
          slot: SOCKET 0
          size: 2159MHz
          capacity: 2400MHz
          width: 64 bits
          clock: 83MHz
          capabilities: x86-64 fpu fpu_exception wp vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx rdtscp constant_tsc arch_perfmon pebs bts rep_good nopl xtopology tsc_reliable nonstop_tsc cpuid aperfmperf tsc_known_freq pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 cx16 xtpr pdcm sse4_1 sse4_2 movbe popcnt tsc_deadline_timer rdrand lahf_lm 3dnowprefetch epb tpr_shadow vnmi flexpriority ept vpid tsc_adjust smep erms dtherm ida arat cpufreq
          configuration: cores=2 enabledcores=2 threads=2
     *-pci
          description: Host bridge
          product: Atom Processor Z36xxx/Z37xxx Series SoC Transaction Register
          vendor: Intel Corporation
          physical id: 100
          bus info: pci@0000:00:00.0
          version: 0e
          width: 32 bits
          clock: 33MHz
          configuration: driver=iosf_mbi_pci
          resources: irq:0
        *-display
             description: VGA compatible controller
             product: Atom Processor Z36xxx/Z37xxx Series Graphics & Display
             vendor: Intel Corporation
             physical id: 2
             bus info: pci@0000:00:02.0
             version: 0e
             width: 32 bits
             clock: 33MHz
             capabilities: pm msi vga_controller bus_master cap_list rom
             configuration: driver=i915 latency=0
             resources: irq:91 memory:d0000000-d03fffff memory:c0000000-cfffffff ioport:f080(size=8) memory:c0000-dffff
        *-storage
             description: SATA controller
             product: Atom Processor E3800 Series SATA AHCI Controller
             vendor: Intel Corporation
             physical id: 13
             bus info: pci@0000:00:13.0
             version: 0e
             width: 32 bits
             clock: 66MHz
             capabilities: storage msi pm ahci_1.0 bus_master cap_list
             configuration: driver=ahci latency=0
             resources: irq:87 ioport:f070(size=8) ioport:f060(size=4) ioport:f050(size=8) ioport:f040(size=4) ioport:f020(size=32) memory:d0806000-d08067ff
        *-generic
             description: Encryption controller
             product: Atom Processor Z36xxx/Z37xxx Series Trusted Execution Engine
             vendor: Intel Corporation
             physical id: 1a
             bus info: pci@0000:00:1a.0
             version: 0e
             width: 32 bits
             clock: 33MHz
             capabilities: pm msi bus_master cap_list
             configuration: driver=mei_txe latency=0
             resources: irq:90 memory:d0500000-d05fffff memory:d0400000-d04fffff
        *-multimedia
             description: Audio device
             product: Atom Processor Z36xxx/Z37xxx Series High Definition Audio Controller
             vendor: Intel Corporation
             physical id: 1b
             bus info: pci@0000:00:1b.0
             version: 0e
             width: 64 bits
             clock: 33MHz
             capabilities: pm msi bus_master cap_list
             configuration: driver=snd_hda_intel latency=0
             resources: irq:92 memory:d0800000-d0803fff
        *-pci:0
             description: PCI bridge
             product: Atom Processor E3800 Series PCI Express Root Port 1
             vendor: Intel Corporation
             physical id: 1c
             bus info: pci@0000:00:1c.0
             version: 0e
             width: 32 bits
             clock: 33MHz
             capabilities: pci pciexpress msi pm normal_decode bus_master cap_list
             configuration: driver=pcieport
             resources: irq:16 ioport:1000(size=4096)
        *-pci:1
             description: PCI bridge
             product: Atom Processor E3800 Series PCI Express Root Port 2
             vendor: Intel Corporation
             physical id: 1c.1
             bus info: pci@0000:00:1c.1
             version: 0e
             width: 32 bits
             clock: 33MHz
             capabilities: pci pciexpress msi pm normal_decode bus_master cap_list
             configuration: driver=pcieport
             resources: irq:17 ioport:2000(size=4096) memory:d0700000-d07fffff
           *-network
                description: Wireless interface
                product: AR9485 Wireless Network Adapter
                vendor: Qualcomm Atheros
                physical id: 0
                bus info: pci@0000:02:00.0
                logical name: wlp2s0
                version: 01
                serial: 40:e2:30:46:4c:52
                width: 64 bits
                clock: 33MHz
                capabilities: pm msi pciexpress bus_master cap_list rom ethernet physical wireless
                configuration: broadcast=yes driver=ath9k driverversion=4.11.3-1-ARCH firmware=N/A ip=172.16.40.38 latency=0 link=yes multicast=yes wireless=IEEE 802.11
                resources: irq:17 memory:d0700000-d077ffff memory:d0780000-d078ffff
        *-pci:2
             description: PCI bridge
             product: Atom Processor E3800 Series PCI Express Root Port 4
             vendor: Intel Corporation
             physical id: 1c.3
             bus info: pci@0000:00:1c.3
             version: 0e
             width: 32 bits
             clock: 33MHz
             capabilities: pci pciexpress msi pm normal_decode bus_master cap_list
             configuration: driver=pcieport
             resources: irq:19 ioport:e000(size=4096) memory:d0600000-d06fffff
           *-generic
                description: Unassigned class
                product: RTS5286 PCI Express Card Reader
                vendor: Realtek Semiconductor Co., Ltd.
                physical id: 0
                bus info: pci@0000:03:00.0
                version: 01
                width: 32 bits
                clock: 33MHz
                capabilities: pm msi pciexpress msix vpd bus_master cap_list
                configuration: driver=rtsx_pci latency=0
                resources: irq:88 memory:d0600000-d060ffff
           *-network
                description: Ethernet interface
                product: RTL8101/2/6E PCI Express Fast/Gigabit Ethernet controller
                vendor: Realtek Semiconductor Co., Ltd.
                physical id: 0.2
                bus info: pci@0000:03:00.2
                logical name: enp3s0f2
                version: 06
                serial: 38:2c:4a:82:77:62
                size: 10Mbit/s
                capacity: 100Mbit/s
                width: 64 bits
                clock: 33MHz
                capabilities: pm msi pciexpress msix vpd bus_master cap_list ethernet physical tp mii 10bt 10bt-fd 100bt 100bt-fd autonegotiation
                configuration: autonegotiation=on broadcast=yes driver=r8169 driverversion=2.3LK-NAPI duplex=half firmware=rtl8402-1_0.0.1 10/26/11 latency=0 link=no multicast=yes port=MII speed=10Mbit/s
                resources: irq:89 ioport:e000(size=256) memory:d0614000-d0614fff memory:d0610000-d0613fff
        *-usb
             description: USB controller
             product: Atom Processor Z36xxx/Z37xxx Series USB EHCI
             vendor: Intel Corporation
             physical id: 1d
             bus info: pci@0000:00:1d.0
             version: 0e
             width: 32 bits
             clock: 33MHz
             capabilities: pm debug ehci bus_master cap_list
             configuration: driver=ehci-pci latency=0
             resources: irq:23 memory:d0805000-d08053ff
           *-usbhost
                product: EHCI Host Controller
                vendor: Linux 4.11.3-1-ARCH ehci_hcd
                physical id: 1
                bus info: usb@1
                logical name: usb1
                version: 4.11
                capabilities: usb-2.00
                configuration: driver=hub slots=8 speed=480Mbit/s
              *-usb
                   description: USB hub
                   vendor: Intel Corp.
                   physical id: 1
                   bus info: usb@1:1
                   version: 0.14
                   capabilities: usb-2.00
                   configuration: driver=hub slots=4 speed=480Mbit/s
                 *-usb:0
                      description: Keyboard
                      product: Dell KM632 Wireless Keyboard and Mouse
                      vendor: Dell
                      physical id: 2
                      bus info: usb@1:1.2
                      version: 1.30
                      capabilities: usb-2.00
                      configuration: driver=usbhid maxpower=100mA speed=12Mbit/s
                 *-usb:1
                      description: Video
                      product: USB Camera
                      vendor: 04081-00092400E9QF4Y
                      physical id: 4
                      bus info: usb@1:1.4
                      version: 0.12
                      serial: 200901010001
                      capabilities: usb-2.00
                      configuration: driver=uvcvideo maxpower=500mA speed=480Mbit/s
        *-isa
             description: ISA bridge
             product: Atom Processor Z36xxx/Z37xxx Series Power Control Unit
             vendor: Intel Corporation
             physical id: 1f
             bus info: pci@0000:00:1f.0
             version: 0e
             width: 32 bits
             clock: 33MHz
             capabilities: isa bus_master cap_list
             configuration: driver=lpc_ich latency=0
             resources: irq:0
        *-serial
             description: SMBus
             product: Atom Processor E3800 Series SMBus Controller
             vendor: Intel Corporation
             physical id: 1f.3
             bus info: pci@0000:00:1f.3
             version: 0e
             width: 32 bits
             clock: 33MHz
             capabilities: pm cap_list
             configuration: driver=i801_smbus latency=0
             resources: irq:18 memory:d0804000-d080401f ioport:f000(size=32)
     *-scsi
          physical id: 1
          logical name: scsi0
          capabilities: emulated
        *-disk
             description: ATA Disk
             product: TRO-SSD7-256GB-P
             physical id: 0.0.0
             bus info: scsi@0:0.0.0
             logical name: /dev/sda
             version: 6A
             serial: EL1603031001A47C5
             size: 238GiB (256GB)
             capabilities: gpt-1.00 partitioned partitioned:gpt
             configuration: ansiversion=5 guid=4e1f60f8-c618-4a40-89b8-949fcc2e2c9a logicalsectorsize=512 sectorsize=512
           *-volume:0
                description: Windows FAT volume
                vendor: mkfs.fat
                physical id: 1
                bus info: scsi@0:0.0.0,1
                logical name: /dev/sda1
                version: FAT16
                serial: 9af6-f0d5
                size: 510MiB
                capacity: 511MiB
                capabilities: boot fat initialized
                configuration: FATs=2 filesystem=fat name=EFI System
           *-volume:1
                description: EFI partition
                physical id: 2
                bus info: scsi@0:0.0.0,2
                logical name: /dev/sda2
                serial: d96b37e7-8f27-450b-b2bc-10428c0e1597
                size: 255MiB
                capacity: 255MiB
                width: 256 bits
                capabilities: encrypted luks initialized
                configuration: bits=256 cipher=aes filesystem=luks hash=sha256 mode=xts-plain64 name=Linux filesystem version=1
           *-volume:2
                description: LVM Physical Volume
                vendor: Linux
                physical id: 3
                bus info: scsi@0:0.0.0,3
                logical name: /dev/sda3
                serial: 5eaaa1a5-036d-4f23-ae3d-e48b3b31c61e
                size: 137GiB
                capacity: 137GiB
                width: 256 bits
                capabilities: multi encrypted luks initialized
                configuration: bits=256 cipher=aes filesystem=luks hash=sha256 mode=xts-plain64 name=Linux LVM version=1
           *-volume:3
                description: EFI partition
                vendor: Linux
                physical id: 4
                bus info: scsi@0:0.0.0,4
                logical name: /dev/sda4
                version: 1.0
                serial: 92804890-530e-4e1a-b2e0-0a17f7e7e983
                size: 99GiB
                capacity: 99GiB
                capabilities: extended_attributes large_files huge_files dir_nlink extents ext2 initialized
                configuration: filesystem=ext2 lastmountpoint=/home/ben/Storage modified=2017-06-14 11:20:59 mounted=2017-06-13 17:54:29 name=Linux filesystem state=clean

```

### LCD Panel information

Output of running `cat /sys/class/drm/card-eDP-1 | edid-decode`:

```
Extracted contents:
header:          00 ff ff ff ff ff ff 00
serial number:   06 af ec 20 00 00 00 00 00 17
version:         01 04
basic params:    90 22 13 78 02
chroma info:     c8 95 9e 57 54 92 26 0f 50 54
established:     00 00 00
standard:        01 01 01 01 01 01 01 01 01 01 01 01 01 01 01 01
descriptor 1:    14 1e 56 06 51 00 14 30 10 10 3e 00 58 c1 10 00 00 18
descriptor 2:    00 00 00 0f 00 00 00 00 00 00 00 00 00 00 00 00 00 20
descriptor 3:    00 00 00 fe 00 41 55 4f 0a 20 20 20 20 20 20 20 20 20
descriptor 4:    00 00 00 fe 00 42 31 35 36 58 54 4e 30 32 2e 30 20 0a
extensions:      00
checksum:        0b

Manufacturer: AUO Model 20ec Serial Number 0
Made week 0 of 2013
EDID version: 1.4
Digital display
6 bits per primary color channel
Digital interface is not defined
Maximum image size: 34 cm x 19 cm
Gamma: 2.20
Supported color formats: RGB 4:4:4
First detailed timing is preferred timing
Established timings supported:
Standard timings supported:
Detailed mode: Clock 77.000 MHz, 344 mm x 193 mm
               1366 1382 1398 1628 hborder 0
                768  771  785  788 vborder 0
               -hsync -vsync 
Manufacturer-specified data, tag 15
ASCII string: AUO
ASCII string: B156XTN02.0 
Checksum: 0xb (valid)
EDID block does NOT conform to EDID 1.3!
	Missing name descriptor
	Missing monitor ranges

```

Datasheet is available from here: [http://www.datasheet-pdf.com/datasheet-download.php?id=860457](http://www.datasheet-pdf.com/datasheet-download.php?id=860457)

## Settings

### Video

For Intel GMA HD (Bay Trail) acceleration install: [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel).

For Vulkan support, you can install [vulkan-intel](https://www.archlinux.org/packages/?name=vulkan-intel), but rendering of polygons on Bay Trail/Ivy Bridge is **extremely** buggy as of June 2017.

### LAN

Works out of the box, via `r8169` kernel driver. You may wish to remove the module if working on battery power and not using Ethernet, as the hardware consumes about 719mW even when not connected. This might be a NetworkManager issue -- testing needed.

### Wi-fi

Works out of the box, via `ath9k` kernel driver.

### Audio

Works out of the box.

### Touchpad

Works out of the box.

### Brightness

fn + F5 / fn + F6 - control brightness.

### Webcam

Works out of the box, via `uvcvideo` driver in kernel.

### Card Reader

Works out of the box.

## Dual boot with Windows

**Note:** This part is copied straight from the [ASUS X551MA](/index.php/ASUS_X551MA "ASUS X551MA") article. I have never attempted to run Windows in dual-boot setup on this laptop.

To boot Windows 7 it is needed to switch on `CSM` at BIOS. Otherwise Windows boot hangs at logo. Set the BIOS setting `OS Selection` in the `Advanced` menu to `Windows 7`.

## Slowdown on 4.x kernels

Using `pstate` CPU frequency governor sometimes causes the frequency to become locked to the lowest possible frequency, 500MHz. This seems to happen when the charger is unplugged. Add `intel_pstate=disable` to the kernel line in grub to avoid this, at the slight disadvantage of being locked out of the "boost" frequencies -- this comes down to having a max of 2.16GHz instead of 2.42GHz -- and possibly slightly worse power consumption.