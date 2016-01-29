# Dell Precision M4800

The Dell Precision M4800 laptop is a mobile workstation released in late 2013.

**Note:** The author of this article ordered the system pre-installed with Ubuntu, so some assumptions made in this article may differ if your system came pre-installed with Windows (e.g. Secure Boot).

## Contents

*   [1 System specifications](#System_specifications)
    *   [1.1 Parts list](#Parts_list)
    *   [1.2 lspci](#lspci)
    *   [1.3 lsusb](#lsusb)
*   [2 Pre-installation notes](#Pre-installation_notes)
*   [3 What does not work](#What_does_not_work)

## System specifications

### Parts list

**CPU:** Intel Core i7-4800MQ Processor (Quad Core, 6 MB Cache, 2.7 GHz, w/HD Graphics 4600)

**Memory:** 16 GB (2x8 GB) 1600 MHz DDR3L

**Storage:** Samsung 840 EVO 1 TB Solid State Drive

**Display:** 39.6cm (15.6") UltraSharp QHD+ (3200x1800) Wide View Anti-Glare LED-backlit Premium Panel

**Graphics:** NVIDIA Quadro K2100M w/2GB GDDR5

**Optical:** 8X DVD+/-RW Drive Slot Load

**Wireless networking:** Dell Wireless 1601 2x2 802.11n+BT+60GHz (WiGig)

**Keyboard:** Internal English Backlit Dual Pointing Keyboard

### lspci

 `# lspci` 

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor DRAM Controller (rev 06)
00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor PCI Express x16 Controller (rev 06)
00:14.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB xHCI (rev 04)
00:16.0 Communication controller: Intel Corporation 8 Series/C220 Series Chipset Family MEI Controller #1 (rev 04)
00:19.0 Ethernet controller: Intel Corporation Ethernet Connection I217-LM (rev 04)
00:1a.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB EHCI #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 8 Series/C220 Series Chipset High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #1 (rev d4)
00:1c.2 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #3 (rev d4)
00:1c.3 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #4 (rev d4)
00:1c.4 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #5 (rev d4)
00:1c.6 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #7 (rev d4)
00:1c.7 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #8 (rev d4)
00:1d.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB EHCI #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation QM87 Express LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 8 Series/C220 Series Chipset Family 6-port SATA Controller 1 [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 8 Series/C220 Series Chipset Family SMBus Controller (rev 04)
01:00.0 VGA compatible controller: NVIDIA Corporation GK106GLM [Quadro K2100M] (rev a1)
01:00.1 Audio device: NVIDIA Corporation GK106 HDMI Audio Controller (rev a1)
03:00.0 PCI bridge: Wilocity Ltd. Wil6200 PCI Express Root Port (rev 04)
04:00.0 PCI bridge: Wilocity Ltd. Wil6200 PCI Express Port (rev 04)
04:02.0 PCI bridge: Wilocity Ltd. Wil6200 Wireless PCI Express Port (rev 14)
04:03.0 PCI bridge: Wilocity Ltd. Wil6200 Wireless PCI Express Port (rev 14)
05:00.0 Network controller: Qualcomm Atheros AR9462 Wireless Network Adapter (rev 01)
15:00.0 SD Host controller: O2 Micro, Inc. Device 8520 (rev 01)

```

### lsusb

 `# lsusb` 

```
Bus 004 Device 003: ID 0a5c:5800 Broadcom Corp. BCM5880 Secure Applications Processor
Bus 004 Device 002: ID 8087:8000 Intel Corp.
Bus 004 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 003: ID 0c45:64d0 Microdia
Bus 003 Device 002: ID 8087:8008 Intel Corp.
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Pre-installation notes

The M4800 comes with a legacy BIOS and UEFI. The Arch installation media, version 2014.04.01, may not properly boot or install if using legacy BIOS and/or a MS-DOS partition table. Using the UEFI option with a GPT-partitioned hard drive was required to successfully complete the installation process.

The M4800 _will not_ give you a usable system _unless_ `nomodeset` is added to the kernel command line. This is required for both the Arch installation media and post-installation. Because `nomodeset` is required even after booting, use of the [Nouveau](/index.php/Nouveau "Nouveau") driver is not possible because Nouveau requires KMS.

If following [SSD memory cell clearing](/index.php/SSD_memory_cell_clearing "SSD memory cell clearing"), after boot the SSD drive (SK hynix SH920 2.5 7MM 512GB) may be set to the `frozen` state. Ejecting the SSD and then re-inserting the SSD cleared the `frozen` state. After clearing the `frozen` state, the instructions in [SSD memory cell clearing](/index.php/SSD_memory_cell_clearing "SSD memory cell clearing") were followed successfully and the drive was cleared.

## What does not work

*   The brightness up/down buttons do not work in [Cinnamon](/index.php/Cinnamon "Cinnamon") or at the virtual console without X (untested on other [desktop environments](/index.php/Desktop_environments "Desktop environments")). Interestingly, [redshift](https://www.archlinux.org/packages/?name=redshift) is able to adjust the display brightness.
*   When Cinnamon locks the screen due to inactivity, pressing keys or moving the mouse does not automatically turn the display back on to allow unlocking the screen. A workaround is to press `Ctrl+Alt+F2` followed by `Ctrl+Alt+F1`, which switches from TTY1 to TTY2 and back again.
*   Switching TTYs with `Ctrl+Alt+F_X_` after X has started does not present the user with a usable TTY.
*   When closing the GUI (e.g. by logging out of Cinnamon), the screen goes black, and the virtual console does not appear like it should.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dell_Precision_M4800&oldid=384393](https://wiki.archlinux.org/index.php?title=Dell_Precision_M4800&oldid=384393)"