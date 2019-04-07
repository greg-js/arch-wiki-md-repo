The Latitude 7490 is virtually identical to the [Dell Latitude 7480](/index.php/Dell_Latitude_7480 "Dell Latitude 7480") with the exception of an upgrade to Kabylake-R processors (8th gen).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Components](#Components)
    *   [1.1 lscpu Output](#lscpu_Output)
    *   [1.2 lspci -k Output](#lspci_-k_Output)
    *   [1.3 lsusb Output](#lsusb_Output)
*   [2 What works](#What_works)
*   [3 What doesn't work](#What_doesn't_work)
*   [4 What was not tested](#What_was_not_tested)

## Components

*Note: This information is from my particular laptop (which does not have a webcam nor touchscreen). Other variants may have slightly different output but should generally behave similarly.*

### `lscpu` Output

```
Architecture:        x86_64
CPU op-mode(s):      32-bit, 64-bit
Byte Order:          Little Endian
Address sizes:       39 bits physical, 48 bits virtual
CPU(s):              8
On-line CPU(s) list: 0-7
Thread(s) per core:  2
Core(s) per socket:  4
Socket(s):           1
NUMA node(s):        1
Vendor ID:           GenuineIntel
CPU family:          6
Model:               142
Model name:          Intel(R) Core(TM) i5-8350U CPU @ 1.70GHz
Stepping:            10
CPU MHz:             1565.593
CPU max MHz:         1700.0000
CPU min MHz:         400.0000
BogoMIPS:            3793.00
Virtualization:      VT-x
L1d cache:           32K
L1i cache:           32K
L2 cache:            256K
L3 cache:            6144K
NUMA node0 CPU(s):   0-7
Flags:               fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf tsc_known_freq pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault epb invpcid_single pti ssbd ibrs ibpb stibp tpr_shadow vnmi flexpriority ept vpid ept_ad fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 erms invpcid rtm mpx rdseed adx smap clflushopt intel_pt xsaveopt xsavec xgetbv1 xsaves dtherm arat pln pts hwp hwp_notify hwp_act_window hwp_epp flush_l1d

```

### `lspci -k` Output

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 08)
        Subsystem: Dell Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers
        Kernel driver in use: skl_uncore
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (rev 07)
        DeviceName:  Onboard IGD
        Subsystem: Dell UHD Graphics 620
        Kernel driver in use: i915
        Kernel modules: i915
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 08)
        Subsystem: Dell Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem
        Kernel driver in use: proc_thermal
        Kernel modules: processor_thermal_device
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
        Subsystem: Dell Sunrise Point-LP USB 3.0 xHCI Controller
        Kernel driver in use: xhci_hcd
        Kernel modules: xhci_pci
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
        Subsystem: Dell Sunrise Point-LP Thermal subsystem
        Kernel driver in use: intel_pch_thermal
        Kernel modules: intel_pch_thermal
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 (rev 21)
        Subsystem: Dell Sunrise Point-LP Serial IO I2C Controller
        Kernel driver in use: intel-lpss
        Kernel modules: intel_lpss_pci
00:15.1 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #1 (rev 21)
        Subsystem: Dell Sunrise Point-LP Serial IO I2C Controller
        Kernel driver in use: intel-lpss
        Kernel modules: intel_lpss_pci
00:15.2 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #2 (rev 21)
        Subsystem: Dell Sunrise Point-LP Serial IO I2C Controller
        Kernel driver in use: intel-lpss
        Kernel modules: intel_lpss_pci
00:15.3 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #3 (rev 21)
        Subsystem: Dell Sunrise Point-LP Serial IO I2C Controller
        Kernel driver in use: intel-lpss
        Kernel modules: intel_lpss_pci
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
        Subsystem: Dell Sunrise Point-LP CSME HECI
        Kernel driver in use: mei_me
        Kernel modules: mei_me
00:16.3 Serial controller: Intel Corporation Device 9d3d (rev 21)
        Subsystem: Dell Device 081c
        Kernel driver in use: serial
00:17.0 SATA controller: Intel Corporation Sunrise Point-LP SATA Controller [AHCI mode] (rev 21)
        Subsystem: Dell Sunrise Point-LP SATA Controller [AHCI mode]
        Kernel driver in use: ahci
        Kernel modules: ahci
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
        Kernel driver in use: pcieport
00:1c.2 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #3 (rev f1)
        Kernel driver in use: pcieport
00:1f.0 ISA bridge: Intel Corporation Intel(R) 100 Series Chipset Family LPC Controller/eSPI Controller - 9D4E (rev 21)
        Subsystem: Dell Intel(R) 100 Series Chipset Family LPC Controller/eSPI Controller - 9D4E
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
        Subsystem: Dell Sunrise Point-LP PMC
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
        Subsystem: Dell Sunrise Point-LP HD Audio
        Kernel driver in use: snd_hda_intel
        Kernel modules: snd_hda_intel, snd_soc_skl
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
        Subsystem: Dell Sunrise Point-LP SMBus
        Kernel driver in use: i801_smbus
        Kernel modules: i2c_i801
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (4) I219-LM (rev 21)
        Subsystem: Dell Ethernet Connection (4) I219-LM
        Kernel driver in use: e1000e
        Kernel modules: e1000e
01:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)
        Subsystem: Dell RTS525A PCI Express Card Reader
        Kernel driver in use: rtsx_pci
        Kernel modules: rtsx_pci
02:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)
        Subsystem: Intel Corporation Wireless 8265 / 8275
        Kernel driver in use: iwlwifi
        Kernel modules: iwlwifi

```

### `lsusb` Output

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 8087:0a2b Intel Corp.                     # Bluetooth
Bus 001 Device 003: ID 0a5c:5834 Broadcom Corp.                  # Dell ControlVault (SmartCard, NFC, and fingerprint)
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## What works

Almost everything works:

*   Basic hardware (display, touchpad, trackpoint, keyboard, WiFi, Ethernet, Bluetooth, audio, suspend & resume from RAM and disk, etc.)
*   Keyboard backlight control
*   Screen backlight control
*   Fn/Hotkeys, including Fn-lock
*   Contact SmartCard reader
*   Qualcomm Snapdragon X7 LTE Modem
*   USB-C (connected to Android phone, was able to charge phone and read files)

## What doesn't work

*   Fingerprint reader (tracked at [https://gitlab.freedesktop.org/libfprint/libfprint/issues/88](https://gitlab.freedesktop.org/libfprint/libfprint/issues/88))
*   Presumably NFC

## What was not tested

*   Contactless SmartCard (probably works since it was detected by `pcsc_scan`
*   USB-C power delivery
*   DisplayPort Alternate Mode for USB-C
*   Thunderbolt 3.0 (my SKU doesn't have this)
*   TPM 2.0 (There is an error in dmesg, `tpm tpm0: A TPM error (2314) occurred attempting the self test`)