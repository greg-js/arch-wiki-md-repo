Related articles

*   [Laptop](/index.php/Laptop "Laptop")
*   [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling")
*   [Undervolting CPU](/index.php/Undervolting_CPU "Undervolting CPU")

PHC is an acpi-cpufreq patch built with the purpose of enabling undervolting on your processor. This can potentially divide the power consumption of your processor by two or more, and in turn increase battery life and reduce fan noise noticiably. PHC works only if your processor's architecture supports undervolting.

## Contents

*   [1 Supported CPUs](#Supported_CPUs)
    *   [1.1 Intel](#Intel)
    *   [1.2 AMD](#AMD)
*   [2 Installation](#Installation)
    *   [2.1 Automatic module generation with DKMS](#Automatic_module_generation_with_DKMS)
*   [3 Configuration](#Configuration)
    *   [3.1 Finding safe low voltages](#Finding_safe_low_voltages)
    *   [3.2 Editing the configuration](#Editing_the_configuration)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Module loading](#Module_loading)
    *   [4.2 Hardware recognition](#Hardware_recognition)
    *   [4.3 Voltage controlling](#Voltage_controlling)
    *   [4.4 System stability](#System_stability)
*   [5 Links](#Links)

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

## Installation

[Install](/index.php/Install "Install") the [phc-intel](https://aur.archlinux.org/packages/phc-intel/) package if you have an Intel processor, or [phc-k8](https://aur.archlinux.org/packages/phc-k8/) if you have an AMD-K8-series one.

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

If the [*acpi-cpufreq*](/index.php/CPU_frequency_scaling#CPU_frequency_driver "CPU frequency scaling") module is not already being loaded at boot, create the appropriate file in `/etc/modules-load.d/`. See [Kernel modules](/index.php/Kernel_modules "Kernel modules") for more information.

**Note:** In the case of [phc-intel](https://aur.archlinux.org/packages/phc-intel/), the *acpi-cpufreq* module is automatically loaded by `/usr/lib/modprobe.d/phc-intel.conf`.

### Automatic module generation with DKMS

The [phc-intel](https://aur.archlinux.org/packages/phc-intel/) package uses DKMS to automatically update the module after a kernel update. This is done at shutdown time to ensure that the kernel and kernel-headers are in sync (which is not necessarily the case during a system upgrade, depending on the order at which updates are installed).

[Enable](/index.php/Enable "Enable") `dkms-phc-intel.service`.

## Configuration

### Finding safe low voltages

To automatically find the best voltages, you can use the [mprime-phc-setup](https://bbs.archlinux.org/viewtopic.php?pid=1141702#p1141702) script ([source-code](https://bitbucket.org/stqn/shell-tools/src/)). Just copy the code into a text file, chmod +x it to make it executable and run it. You need to install [mprime](https://aur.archlinux.org/packages/mprime/) or [mprime-bin](https://aur.archlinux.org/packages/mprime-bin/) first (it is used to check that the CPU is stable). This script has not been tested on many systems yet, but should be safe.

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

To make sure that your undervolted CPU is stable, you can run long sessions of [mprime](https://aur.archlinux.org/packages/mprime/) and/or [linpack](https://aur.archlinux.org/packages/linpack/) (Intel-only).

## Links

*   [PHC homepage](http://www.linux-phc.org/)
*   [PHC official wiki](http://www.linux-phc.org/wiki/doku.php)