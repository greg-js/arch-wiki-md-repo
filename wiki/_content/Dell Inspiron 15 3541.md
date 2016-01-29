# Dell Inspiron 15 3541

[![Tango-emblem-symbolic-link.png](/images/f/f9/Tango-emblem-symbolic-link.png)](/index.php/File:Tango-emblem-symbolic-link.png)

[![Tango-emblem-symbolic-link.png](/images/f/f9/Tango-emblem-symbolic-link.png)](/index.php/File:Tango-emblem-symbolic-link.png)

**This article is being considered for redirection to [Laptop/Dell](/index.php/Laptop/Dell "Laptop/Dell").**

**Notes:** If no special action needed, this page should be redirect to general page. There is no need to list hardware info in Archwiki. (Discuss in [Talk:Dell Inspiron 15 3541#](https://wiki.archlinux.org/index.php/Talk:Dell_Inspiron_15_3541))

This page describes the hardware and Linux support of the Dell Inspiron 15 3000 Series (Model 3541) laptop.

See the [Laptop/Dell](/index.php/Laptop/Dell "Laptop/Dell") chart for information on other Dell laptops.

## System Specifications

lspci output:

```
00:00.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 1566
00:01.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] Mullins [Radeon R2 Graphics]
00:01.1 Audio device: Advanced Micro Devices, Inc. [AMD/ATI] Kabini HDMI/DP Audio
00:02.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 156b
00:02.1 PCI bridge: Advanced Micro Devices, Inc. [AMD] Family 16h Processor Functions 5:1
00:02.2 PCI bridge: Advanced Micro Devices, Inc. [AMD] Family 16h Processor Functions 5:1
00:02.3 PCI bridge: Advanced Micro Devices, Inc. [AMD] Family 16h Processor Functions 5:1
00:08.0 Encryption controller: Advanced Micro Devices, Inc. [AMD] Device 1537
00:10.0 USB controller: Advanced Micro Devices, Inc. [AMD] FCH USB XHCI Controller (rev 11)
00:11.0 SATA controller: Advanced Micro Devices, Inc. [AMD] FCH SATA Controller [AHCI mode]
00:12.0 USB controller: Advanced Micro Devices, Inc. [AMD] FCH USB EHCI Controller (rev 39)
00:13.0 USB controller: Advanced Micro Devices, Inc. [AMD] FCH USB EHCI Controller (rev 39)
00:14.0 SMBus: Advanced Micro Devices, Inc. [AMD] FCH SMBus Controller (rev 42)
00:14.2 Audio device: Advanced Micro Devices, Inc. [AMD] FCH Azalia Controller (rev 02)
00:14.3 ISA bridge: Advanced Micro Devices, Inc. [AMD] FCH LPC Bridge (rev 11)
00:18.0 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 1580
00:18.1 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 1581
00:18.2 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 1582
00:18.3 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 1583
00:18.4 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 1584
00:18.5 Host bridge: Advanced Micro Devices, Inc. [AMD] Device 1585
02:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8101E/RTL8102E PCI Express Fast Ethernet controller (rev 07)
03:00.0 Network controller: Qualcomm Atheros QCA9565 / AR9565 Wireless Network Adapter (rev 01)
```

lsusb output:

```
Bus 004 Device 005: ID 0c45:6a04 Microdia
Bus 004 Device 006: ID 0cf3:0036 Atheros Communications, Inc.
Bus 004 Device 003: ID 0bda:0129 Realtek Semiconductor Corp. RTS5129 Card Reader Controller
Bus 004 Device 002: ID 0438:7900 Advanced Micro Devices, Inc.
Bus 004 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 002: ID 0438:7900 Advanced Micro Devices, Inc.
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

Contents of `/proc/cpuinfo`:

```
processor       : 0
vendor_id       : AuthenticAMD
cpu family      : 22
model           : 48
model name      : AMD E1-6010 APU with AMD Radeon R2 Graphics
stepping        : 1
microcode       : 0x7030105
cpu MHz         : 1200.000
cache size      : 1024 KB
physical id     : 0
siblings        : 2
core id         : 0
cpu cores       : 2
apicid          : 0
initial apicid  : 0
fpu             : yes
fpu_exception   : yes
cpuid level     : 13
wp              : yes
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc extd_apicid aperfmperf eagerfpu pni pclmulqdq monitor ssse3 cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw ibs skinit wdt topoext perfctr_nb bpext perfctr_l2 arat hw_pstate npt lbrv svm_lock nrip_save tsc_scale flushbyasid decodeassists pausefilter pfthreshold vmmcall bmi1 xsaveopt
bugs            : fxsave_leak sysret_ss_attrs
bogomips        : 2696.31
TLB size        : 1024 4K pages
clflush size    : 64
cache_alignment : 64
address sizes   : 40 bits physical, 48 bits virtual
power management: ts ttp tm 100mhzsteps hwpstate [12] [13]

processor       : 1
vendor_id       : AuthenticAMD
cpu family      : 22
model           : 48
model name      : AMD E1-6010 APU with AMD Radeon R2 Graphics
stepping        : 1
microcode       : 0x7030105
cpu MHz         : 1000.000
cache size      : 1024 KB
physical id     : 0
siblings        : 2
core id         : 1
cpu cores       : 2
apicid          : 1
initial apicid  : 1
fpu             : yes
fpu_exception   : yes
cpuid level     : 13
wp              : yes
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl nonstop_tsc extd_apicid aperfmperf eagerfpu pni pclmulqdq monitor ssse3 cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand lahf_lm cmp_legacy svm extapic cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw ibs skinit wdt topoext perfctr_nb bpext perfctr_l2 arat hw_pstate npt lbrv svm_lock nrip_save tsc_scale flushbyasid decodeassists pausefilter pfthreshold vmmcall bmi1 xsaveopt
bugs            : fxsave_leak sysret_ss_attrs
bogomips        : 2696.31
TLB size        : 1024 4K pages
clflush size    : 64
cache_alignment : 64
address sizes   : 40 bits physical, 48 bits virtual
power management: ts ttp tm 100mhzsteps hwpstate [12] [13]
```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dell_Inspiron_15_3541&oldid=416925](https://wiki.archlinux.org/index.php?title=Dell_Inspiron_15_3541&oldid=416925)"