## Contents

*   [1 Introduction](#Introduction)
*   [2 Hardware Identification](#Hardware_Identification)
*   [3 Unsupported Hardware & Features & Worarounds](#Unsupported_Hardware_.26_Features_.26_Worarounds)
*   [4 Kernel Parameters](#Kernel_Parameters)

## Introduction

This laptop features an Intel Core I7 processor and comes with 8 or 16G of RAM memory.

There is a bios bug (version 1.25) which prevents any Linux version from working (either 64 or 32 bits, UEFI or legacy). The system freezes as soon as the kernel boots, usually after the message "ACPI: unable to load the system description tables".

As of today (December, 2015), the only viable fix is to downgrade the BIOS: follow the steps described here -- [http://community.acer.com/t5/E-and-M-Series/Acer-Aspire-e5-573g-You-can-not-install-any-one-Linux/td-p/386009](http://community.acer.com/t5/E-and-M-Series/Acer-Aspire-e5-573g-You-can-not-install-any-one-Linux/td-p/386009) -- which guides you on how to downgrade to version 1.15, which will allow Arch (and any other linux) to run fine.

## Hardware Identification

USB Devices

 `lsusb` 
```
Bus 002 Device 005: ID 248a:8566  
Bus 002 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 018: ID 058f:6366 Alcor Micro Corp. Multi Flash Reader
Bus 001 Device 003: ID 058f:a014 Alcor Micro Corp. Asus Integrated Webcam
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

PCI Devices

 `lspci` 
```
00:00.0 Host bridge: Intel Corporation 2nd Generation Core Processor Family DRAM Controller (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 2nd Generation Core Processor Family Integrated Graphics Controller (rev 09)
00:16.0 Communication controller: Intel Corporation 6 Series/C200 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 6 Series/C200 Series Chipset Family USB Enhanced Host Controller #2 (rev 05)
00:1b.0 Audio device: Intel Corporation 6 Series/C200 Series Chipset Family High Definition Audio Controller (rev 05)
00:1c.0 PCI bridge: Intel Corporation 6 Series/C200 Series Chipset Family PCI Express Root Port 1 (rev b5)
00:1c.1 PCI bridge: Intel Corporation 6 Series/C200 Series Chipset Family PCI Express Root Port 2 (rev b5)
00:1c.5 PCI bridge: Intel Corporation 6 Series/C200 Series Chipset Family PCI Express Root Port 6 (rev b5)
00:1d.0 USB controller: Intel Corporation 6 Series/C200 Series Chipset Family USB Enhanced Host Controller #1 (rev 05)
00:1f.0 ISA bridge: Intel Corporation HM65 Express Chipset Family LPC Controller (rev 05)
00:1f.2 SATA controller: Intel Corporation 6 Series/C200 Series Chipset Family 6 port SATA AHCI Controller (rev 05)
00:1f.3 SMBus: Intel Corporation 6 Series/C200 Series Chipset Family SMBus Controller (rev 05)
02:00.0 Network controller: Qualcomm Atheros AR9285 Wireless Network Adapter (PCI-Express) (rev 01)
03:00.0 Ethernet controller: Qualcomm Atheros AR8151 v2.0 Gigabit Ethernet (rev c0)
```

CPU

 `lscpu` 
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
Model:                 42
Model name:            Intel(R) Core(TM) i5-2410M CPU @ 2.30GHz
Stepping:              7
CPU MHz:               875.078
CPU max MHz:           2900.0000
CPU min MHz:           800.0000
BogoMIPS:              4591.57
Virtualization:        VT-x
L1d cache:             32K
L1i cache:             32K
L2 cache:              256K
L3 cache:              3072K
NUMA node0 CPU(s):     0-3
Flags:                 fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx rdtscp lm constant_tsc arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc aperfmperf eagerfpu pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic popcnt tsc_deadline_timer xsave avx lahf_lm ida arat epb pln pts dtherm tpr_shadow vnmi flexpriority ept vpid xsaveopt
```

## Unsupported Hardware & Features & Worarounds

As of December, 2015, kernel 4.2.5-1-ARCH and still running BIOS v. 1.15, the following is happening:

*   the built in Bluetooth seems not to be supported -- it isn't detected;

*   suspending to RAM (S3 Sleep state) and hibernating to disk don't work when running on AC power. After debugging with [https://www.kernel.org/doc/Documentation/power/basic-pm-debugging.txt](https://www.kernel.org/doc/Documentation/power/basic-pm-debugging.txt) culprit revealed to be the non-boot online cpus. Sleeping (and, possibly hibernate also) works by issuing the commands:

```
for c in /sys/devices/system/cpu/cpu*/online; do echo 0 >$c; done
echo "mem" >/sys/power/state
for c in /sys/devices/system/cpu/cpu*/online; do echo 1 >$c; done

```

One might find useful to follow [Power management#Sleep hooks](/index.php/Power_management#Sleep_hooks "Power management") to configure systemd sleep, hibernate and wakeup hooks

All the rest works fine.

## Kernel Parameters

The following kernel boot parameters should minimize some warnings on dmesg and configure the hardware for good use:

```
intremap=no_x2apic_optout \
acpi_enforce_resources=lax

```

This additional kernel boot parameters were an unsuccessful attempt to get bluetooth to work (note the ath9k wireless driver says bluetooth cannot work with antenna diversity):

```
ath9k.btcoex_enable=1 \
ath9k.bt_ant_diversity=0 \
ath9k.ps_enable=1

```

This CPU may (should) be configured to install a micro code at boot time. This is done by loading the intel-ucode.img initrd image (present on intel-ucode) package before the usual initrd image:

```
linux	/vmlinuz-linux
initrd  /intel-ucode.img
initrd	/initramfs-linux.img

```