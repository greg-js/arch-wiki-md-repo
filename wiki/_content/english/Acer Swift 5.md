| **Device** | **Status** | **Modules** |
| Intel graphics | **Working** | i915 |
| Wireless | **Working** | iwlwifi |
| Bluetooth | **Working** | btintel |
| Audio | **Working** | snd_hda_intel |
| Touchpad | **Working** | xf86-input-synaptics |
| TouchScreen | **Working** |
| Camera | **Working** | uvcvideo |
| Fingerprint scanner | **Not detected** |

General info about the **Acer Swift 5 SF515-51T** laptop. Everything pretty much works out of the box, follow standard documentation for details.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Disabling UEFI Secure Boot](#Disabling_UEFI_Secure_Boot)
*   [2 Hardware](#Hardware)
    *   [2.1 CPU](#CPU)
*   [3 Configuration](#Configuration)
    *   [3.1 Kernel boot parameters](#Kernel_boot_parameters)
    *   [3.2 Kernel modules parameters](#Kernel_modules_parameters)
*   [4 See also](#See_also)

## Disabling UEFI Secure Boot

To disable Secure Boot, set the [supervisor password](https://acer.custhelp.com/app/answers/detail/a_id/29349/) in the BIOS settings. Then you should be able to disable Secure Boot and boot Arch.

## Hardware

**Note:** This may differ from your laptop configuration.
 `# lspci` 
```
00:00.0 Host bridge: Intel Corporation Device 3e34 (rev 0b)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (Whiskey Lake)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 0b)
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th Gen Core Processor Gaussian Mixture Model
00:12.0 Signal processing controller: Intel Corporation Cannon Point-LP Thermal Controller (rev 30)
00:14.0 USB controller: Intel Corporation Cannon Point-LP USB 3.1 xHCI Controller (rev 30)
00:14.2 RAM memory: Intel Corporation Cannon Point-LP Shared SRAM (rev 30)
00:14.3 Network controller: Intel Corporation Cannon Point-LP CNVi [Wireless-AC] (rev 30)
00:15.0 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP Serial IO I2C Controller #0 (rev 30)
00:15.1 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP Serial IO I2C Controller #1 (rev 30)
00:16.0 Communication controller: Intel Corporation Cannon Point-LP MEI Controller #1 (rev 30)
00:17.0 RAID bus controller: Intel Corporation 82801 Mobile SATA Controller [RAID mode] (rev 30)
00:19.0 Serial bus controller [0c80]: Intel Corporation Device 9dc5 (rev 30)
00:1d.0 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #9 (rev f0)
00:1d.4 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #13 (rev f0)
00:1f.0 ISA bridge: Intel Corporation Cannon Point-LP LPC Controller (rev 30)
00:1f.3 Multimedia audio controller: Intel Corporation Cannon Point-LP High Definition Audio Controller (rev 30)
00:1f.4 SMBus: Intel Corporation Cannon Point-LP SMBus Controller (rev 30)
00:1f.5 Serial bus controller [0c80]: Intel Corporation Cannon Point-LP SPI Controller (rev 30)
02:00.0 Non-Volatile memory controller: SK hynix Device 1327

```

### CPU

 `$ lscpu` 
```
Architecture:                    x86_64
CPU op-mode(s):                  32-bit, 64-bit
Byte Order:                      Little Endian
Address sizes:                   39 bits physical, 48 bits virtual
CPU(s):                          8
On-line CPU(s) list:             0-7
Thread(s) per core:              2
Core(s) per socket:              4
Socket(s):                       1
NUMA node(s):                    1
Vendor ID:                       GenuineIntel
CPU family:                      6
Model:                           142
Model name:                      Intel(R) Core(TM) i7-8565U CPU @ 1.80GHz
Stepping:                        11
CPU MHz:                         902.195
CPU max MHz:                     4600.0000
CPU min MHz:                     400.0000
BogoMIPS:                        3985.00
Virtualization:                  VT-x
L1d cache:                       128 KiB
L1i cache:                       128 KiB
L2 cache:                        1 MiB
L3 cache:                        8 MiB
NUMA node0 CPU(s):               0-7
Vulnerability L1tf:              Not affected
Vulnerability Mds:               Vulnerable: Clear CPU buffers attempted, no microcode; SMT vulnerable
Vulnerability Meltdown:          Not affected
Vulnerability Spec store bypass: Mitigation; Speculative Store Bypass disabled via prctl and seccomp
Vulnerability Spectre v1:        Mitigation; usercopy/swapgs barriers and __user pointer sanitization
Vulnerability Spectre v2:        Mitigation; Full generic retpoline, IBPB conditional, IBRS_FW, STIBP conditional, RSB filling
Flags:                           fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr s
                                 se sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good n
                                 opl xtopology nonstop_tsc cpuid aperfmperf tsc_known_freq pni pclmulqdq dtes64 monitor ds_cpl vmx e
                                 st tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes 
                                 xsave avx f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault epb invpcid_single ssbd ibrs ibpb stibp
                                  tpr_shadow vnmi flexpriority ept vpid ept_ad fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid 
                                 mpx rdseed adx smap clflushopt intel_pt xsaveopt xsavec xgetbv1 xsaves dtherm ida arat pln pts hwp 
                                 hwp_notify hwp_act_window hwp_epp flush_l1d arch_capabilities

```

## Configuration

### Kernel boot parameters

The following parameters can be added to boot arguments as explained in [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters"):

*   `acpi_backlight=video` to enable backlight setting from keyboard function keys
*   `acpi_osi=Linux` to enable multimedia special function keys
*   `pci=nocrs` to discard pci ACPI informations, may fix boot problems
*   `i915.i915_enable_rc6=1` to enable deeper sleep states (power saving)
*   `i915.i915_enable_fbc=1` to enable framebuffer compression (power saving)

### Kernel modules parameters

The following parameters enable headset micro detection for sound capture, sound power saving and backlight control:

 `/etc/modprobe.d/swift5.conf` 
```
options snd-hda-intel model=dell-headset-multi
options snd-hda-intel power_save=1
options i915 enable_dpcd_backlight
```

## See also

*   [Drivers and Manuals](https://www.acer.com/ac/en/US/content/support-product/7852?b=1) Official support page
*   [notebook check](https://www.notebookcheck.net/Acer-Swift-5-SF515-51T-i7-8565U-SSD-FHD-Laptop-Review.406346.0.html) Laptop review