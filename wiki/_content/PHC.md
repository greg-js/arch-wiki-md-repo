# PHC

PHC is an acpi-cpufreq patch built with the purpose of enabling undervolting on your processor. This can potentially divide the power consumption of your processor by two or more, and in turn increase battery life and reduce fan noise noticiably. PHC works only if your processor's architecture supports undervolting.

## Contents

*   [1 Alternative to PHC](#Alternative_to_PHC)
*   [2 Supported CPUs](#Supported_CPUs)
    *   [2.1 Intel](#Intel)
    *   [2.2 AMD](#AMD)
*   [3 Installing the necessary packages](#Installing_the_necessary_packages)
    *   [3.1 Automatic module generation with DKMS](#Automatic_module_generation_with_DKMS)
*   [4 Configuring PHC](#Configuring_PHC)
    *   [4.1 Finding safe low voltages](#Finding_safe_low_voltages)
    *   [4.2 Editing the configuration](#Editing_the_configuration)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Module loading](#Module_loading)
    *   [5.2 Hardware recognition](#Hardware_recognition)
    *   [5.3 Voltage controlling](#Voltage_controlling)
    *   [5.4 System stability](#System_stability)
*   [6 Links](#Links)

## Alternative to PHC

[cpupowerd](https://aur.archlinux.org/packages/cpupowerd/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/cpupowerd)]</sup> is a userland solution to replace the in-kernel cpufreq governors and also enable undervolting, only on AMD processors. Like PHC, it requires the user to find safe voltages.

## Supported CPUs

PHC supports the following processor families:

### Intel

**Note:** Current Intel core i CPUs use Intel P-states instead of acpi_cpufreq and are therefor not compatible with PHC.

*   Mobile Centrino
*   Atom (N2xx)
*   Core / Core2 (T and P Series)
*   Core i (2nd generation and older, tested on Core i3 550)

**Note:** Frequency locking does not seem to be working on Core i3 with the current stable 0.3.2 release of PHC, so finding the best vids for all but the highest frequency might be difficult or impossible.

### AMD

*   K8 series

## Installing the necessary packages

Install from the [AUR](/index.php/AUR "AUR") either [phc-intel](https://aur.archlinux.org/packages/phc-intel/)<sup><small>AUR</small></sup> if you have an Intel processor, or [phc-k8](https://aur.archlinux.org/packages/phc-k8/)<sup><small>AUR</small></sup> if you have an AMD-K8-series one.

Next you need to compile the module for your kernel; this will also be necessary after a kernel update (but see the section below on using DKMS to automate this).

You need to have [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) and/or [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers) installed to be able to build the module.

Type:

```
# phc-intel setup

```

or

```
# phc-k8 setup

```

depending on processor.

If the [_acpi-cpufreq_](/index.php/CPU_frequency_scaling#CPU_frequency_driver "CPU frequency scaling") module is not already being loaded at boot, create the appropriate file in `/etc/modules-load.d/`. See [this](/index.php/Kernel_modules#Loading "Kernel modules") wiki article for more information.

**Note:** In the case of [phc-intel](https://aur.archlinux.org/packages/phc-intel/)<sup><small>AUR</small></sup>, the _acpi-cpufreq_ module is automatically loaded by `/usr/lib/modprobe.d/phc-intel.conf`.

### Automatic module generation with DKMS

The [dkms-phc-intel](https://aur.archlinux.org/packages/dkms-phc-intel/)<sup><small>AUR</small></sup> package uses DKMS to automatically update the module after a kernel update. This is done at shutdown time to ensure that the kernel and kernel-headers are in sync (which is not necessarily the case during a system upgrade, depending on the order at which updates are installed).

To enable the systemd service, type:

```
# systemctl enable dkms-phc-intel

```

## Configuring PHC

### Finding safe low voltages

To automatically find the best voltages, you can use the [mprime-phc-setup](https://bbs.archlinux.org/viewtopic.php?pid=1141702#p1141702) script ([source-code](https://bitbucket.org/stqn/shell-tools/src/)). Just copy the code into a text file, chmod +x it to make it executable and run it. You need to install [mprime](https://aur.archlinux.org/packages/mprime/)<sup><small>AUR</small></sup> or [mprime-bin](https://aur.archlinux.org/packages/mprime-bin/)<sup><small>AUR</small></sup> first (it is used to check that the CPU is stable). This script has not been tested on many systems yet, but should be safe.

You can also try [linux-phc-optimize](https://aur.archlinux.org/packages/linux-phc-optimize/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/linux-phc-optimize)]</sup>, although it has produced unsafe vids on [some setups](https://bbs.archlinux.org/viewtopic.php?pid=1044323#p1044323). The script progressively lowers the values until the system crashes, and adds two to the values for stability. Because the system will crash, do not do anything else during the tests. Run it once for each value, then check `/usr/share/linux-phc-optimize/phc_tweaked_vids`.

### Editing the configuration

After the phc module is compiled and the lowest voltages are found, they need to be added to the configuration file at `/etc/default/phc-intel` or `/etc/default/phc-k8`.

For example:

```
VIDS="25 22 15 8 5"

```

Simply restart the system and the modules will be loaded automatically by systemd.

## Troubleshooting

### Module loading

Run:

```
$ dmesg | grep acpi-cpufreq

```

If you see errors regarding this module, something has gone wrong OR you cannot use PHC.

### Hardware recognition

There should be some files in `/sys/devices/system/cpu/cpu0/cpufreq/` beginning with "phc_". To check whether PHC is working or not, just type:

```
$ cat /sys/devices/system/cpu/cpu0/cpufreq/phc_controls

```

you should read some values. If the values do not appear, then PHC is probably not supported by your CPU.

### Voltage controlling

You can easily check whether PHC is working or not by looking at the cpu voltages: if the voltages are lower than the normal ones, then PHC has done its job. You can also manually set voltages, for example:

```
# echo 34 26 18 12 8 5 > /sys/devices/system/cpu/cpu0/cpufreq/phc_vids

```

### System stability

To make sure that your undervolted CPU is stable, you can run long sessions of [mprime](https://aur.archlinux.org/packages/mprime/)<sup><small>AUR</small></sup> and/or [linpack](https://aur.archlinux.org/packages/linpack/)<sup><small>AUR</small></sup> (Intel-only).

## Links

*   [PHC homepage](http://www.linux-phc.org/)
*   [PHC official wiki](http://www.linux-phc.org/wiki/doku.php)

Retrieved from "[https://wiki.archlinux.org/index.php?title=PHC&oldid=410635](https://wiki.archlinux.org/index.php?title=PHC&oldid=410635)"