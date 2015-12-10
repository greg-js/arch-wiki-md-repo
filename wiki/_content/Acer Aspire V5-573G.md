# Acer Aspire V5-573G

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

<table class="wikitable" style="float: right;">

<tbody>

<tr>

<td>**Device**</td>

<td>**Status**</td>

<td>**Modules**</td>

</tr>

<tr>

<td>Intel graphics</td>

<td style="color:green">**Working**</td>

<td>i915</td>

</tr>

<tr>

<td>Nvidia graphics</td>

<td style="color:lightgreen">**Working, see below**</td>

<td>nvidia, bumblebee</td>

</tr>

<tr>

<td>Graphic outputs</td>

<td style="color:green">**Working**</td>

<td>i915</td>

</tr>

<tr>

<td>Ethernet</td>

<td style="color:green">**Working**</td>

<td>r8169</td>

</tr>

<tr>

<td>Wireless</td>

<td style="color:green">**Working**</td>

<td>ath9k</td>

</tr>

<tr>

<td>Bluetooth</td>

<td style="color:green">**Working**</td>

<td>ath3k</td>

</tr>

<tr>

<td>Audio</td>

<td style="color:green">**Working**</td>

<td>snd_hda_intel</td>

</tr>

<tr>

<td>Touchpad</td>

<td style="color:green">**Working**</td>

<td>xf86-input-synaptics</td>

</tr>

<tr>

<td>Camera</td>

<td style="color:green">**Working**</td>

<td>uvcvideo</td>

</tr>

</tbody>

</table>

General info about the **Acer Aspire V5-573G** laptop. Everything pretty much works out of the box, follow standard documentation for details.

**Note:** Most of this should also apply to the **Acer Aspire V7-582PG** and **Acer Aspire V7-582G** - those are higher tier models of the same, confirmed to be the same motherboard. Touchscreen wasn't tested on those.

## Contents

*   [1 Disabling UEFI Secure Boot](#Disabling_UEFI_Secure_Boot)
*   [2 mSATA Slot](#mSATA_Slot)
*   [3 Hardware](#Hardware)
    *   [3.1 CPU](#CPU)
    *   [3.2 Memory specifications](#Memory_specifications)
*   [4 Issues](#Issues)
    *   [4.1 NVIDIA breakage](#NVIDIA_breakage)
    *   [4.2 PulseAudio upmixing](#PulseAudio_upmixing)
*   [5 See also](#See_also)

## Disabling UEFI Secure Boot

To disable Secure Boot, set the [supervisor password](https://acer.custhelp.com/app/answers/detail/a_id/29349/) in the BIOS settings. Then you should be able to boot Arch.

## mSATA Slot

Laptop has an empty mSATA [SSD](/index.php/SSD "SSD") slot, which can be used for almost anything you want to. For example, you can [set](/index.php/Partitioning "Partitioning") it as your `/` partition, which will improve boot speed and overall perfomance, when `/home` and, probably, `/var` is located on your HDD. Although it can't be used as boot device, so you will have to create `/boot` partition on the HDD and install [bootloader](/index.php/Bootloader "Bootloader") there.

## Hardware

**Note:** This may differ from your laptop configuration.

 `# lspci` 

```
00:00.0 Host bridge: Intel Corporation Haswell-ULT DRAM Controller (rev 09)
00:02.0 VGA compatible controller: Intel Corporation Haswell-ULT Integrated Graphics Controller (rev 09)
00:03.0 Audio device: Intel Corporation Haswell-ULT HD Audio Controller (rev 09)
00:14.0 USB controller: Intel Corporation 8 Series USB xHCI HC (rev 04)
00:16.0 Communication controller: Intel Corporation 8 Series HECI #0 (rev 04)
00:1b.0 Audio device: Intel Corporation 8 Series HD Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 8 Series PCI Express Root Port 1 (rev e4)
00:1c.2 PCI bridge: Intel Corporation 8 Series PCI Express Root Port 3 (rev e4)
00:1c.3 PCI bridge: Intel Corporation 8 Series PCI Express Root Port 4 (rev e4)
00:1c.4 PCI bridge: Intel Corporation 8 Series PCI Express Root Port 5 (rev e4)
00:1d.0 USB controller: Intel Corporation 8 Series USB EHCI #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation 8 Series LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 8 Series SATA Controller 1 [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 8 Series SMBus Controller (rev 04)
01:00.0 3D controller: NVIDIA Corporation GK107M [GeForce GT 750M] (rev a1)
04:00.0 Network controller: Qualcomm Atheros AR9462 Wireless Network Adapter (rev 01)
05:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. Device 5287 (rev 01)
05:00.1 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 14)

```

### CPU

 `$ lscpu` 

```
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                4
On-line CPU(s) list:   0-3
Thread(s) per core:    2
Core(s) per socket:    2
Socket(s):             1
NUMA node(s):          1
Vendor ID:             GenuineIntel
CPU family:            6
Model:                 69
Model name:            Intel(R) Core(TM) i5-4200U CPU @ 1.60GHz
Stepping:              1
CPU MHz:               1714.488
CPU max MHz:           2600.0000
CPU min MHz:           800.0000
BogoMIPS:              4591.40
Virtualization:        VT-x
L1d cache:             32K
L1i cache:             32K
L2 cache:              256K
L3 cache:              3072K
NUMA node0 CPU(s):     0-3

```

### Memory specifications

Even though it says 1.5V on the motherboard, it's wrong[[1]](http://community.acer.com/t5/Ultra-Thin/V5-573g-memory-upgrade-failure/m-p/285446). If you want to upgrade RAM, you need to look for:

*   DDR3
*   PC3L-12800 (1600MHz)
*   1.35V (very important, higher will not work!)
*   SO-DIMM

## Issues

### NVIDIA breakage

In case you encounter issues with NVIDIA GPU initialization, see [Bumblebee troubleshooting section](/index.php/Bumblebee#Failed_to_initialize_the_NVIDIA_GPU_at_PCI:1:0:0_.28GPU_fallen_off_the_bus_.2F_RmInitAdapter_failed.21.29 "Bumblebee").

### PulseAudio upmixing

If you do not have 4.0 sound sources, you may want to make PulseAudio automatically upmix 2.0 to 4.0. To do this, add `default-sample-channels=4` to `~/.config/pulse/daemon.conf` (create the file if needed).

## See also

*   [Drivers and Manuals](http://www.acer.co.uk/ac/en/GB/content/drivers/4843;-;Aspire%20V5-573G) Official support page
*   [Acer Aspire V5-573G](http://wiki.gentoo.org/wiki/Acer_Aspire_V5-573G) Gentoo Wiki

Retrieved from "[https://wiki.archlinux.org/index.php?title=Acer_Aspire_V5-573G&oldid=394297](https://wiki.archlinux.org/index.php?title=Acer_Aspire_V5-573G&oldid=394297)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Acer](/index.php/Category:Acer "Category:Acer")