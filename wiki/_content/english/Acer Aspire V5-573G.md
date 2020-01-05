| **Device** | **Status** | **Modules** |
| Intel graphics | **Working** | i915 |
| Nvidia graphics | **Working, see below** | nvidia, bumblebee |
| Graphic outputs | **Working** | i915 |
| Ethernet | **Working** | r8169 |
| Wireless | **Working** | ath9k |
| Bluetooth | **Working** | ath3k |
| Audio | **Working** | snd_hda_intel |
| Touchpad | **Working** | xf86-input-synaptics |
| Camera | **Working** | uvcvideo |

General info about the **Acer Aspire V5-573G** laptop. Everything pretty much works out of the box, follow standard documentation for details.

**Note:** Most of this should also apply to the **Acer Aspire V7-582PG** and **Acer Aspire V7-582G** - those are higher tier models of the same, confirmed to be the same motherboard. Touchscreen wasn't tested on those.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

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

To disable Secure Boot, set the [supervisor password](https://us.answers.acer.com/app/answers/detail/a_id/29349/) in the BIOS settings. Then you should be able to disable Secure Boot and boot Arch.

## mSATA Slot

Laptop has an empty mSATA [SSD](/index.php/SSD "SSD") slot, which can be used for almost anything you want to. For example, you can use it as your `/` [partition](/index.php/Partition "Partition"), which will improve boot and application startup times, with `/home` and possibly `/var` located on your HDD. However, it can't be used as the primary boot device, so you will have to create a `/boot` partition on the HDD and install your [bootloader](/index.php/Bootloader "Bootloader") there.

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

*   [Drivers and Manuals](http://www.acer.com/ac/en/GB/content/support-product/4843?b=1) Official support page
*   [Acer Aspire V5-573G](http://wiki.gentoo.org/wiki/Acer_Aspire_V5-573G) Gentoo Wiki