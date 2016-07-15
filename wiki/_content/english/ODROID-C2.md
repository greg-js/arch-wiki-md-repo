From [Arch Linux ARM ODROID-C2](https://archlinuxarm.org/platforms/armv8/amlogic/odroid-c2):

	The ODROID-C2 is a $40 quad-core computer, providing one of the most cost-effective ARMv8 AArch64 development boards available. Board dimensions are identical to the ODROID-C1, and it can use the same power supply or be powered through the micro USB port. It is based on an Amlogic S905 ARM Cortex-A53 2.0Ghz quad core CPU.

**Note:** Support for the ARM architecture is provided on [http://archlinuxarm.org](http://archlinuxarm.org) not through posts to the official Arch Linux Forum. Any posts related to ARM specific issues will be promptly closed per the [Code of conduct#Arch Linux distribution support *only*](/index.php/Code_of_conduct#Arch_Linux_distribution_support_.2Aonly.2A "Code of conduct") policy.

## Contents

*   [1 Installation](#Installation)
*   [2 CPU frequency scaling](#CPU_frequency_scaling)
    *   [2.1 Show online/offline cores](#Show_online.2Foffline_cores)
    *   [2.2 Read CPU temperature](#Read_CPU_temperature)
    *   [2.3 Read CPU frequency](#Read_CPU_frequency)
    *   [2.4 Read CPU governor](#Read_CPU_governor)
*   [3 See also](#See_also)

## Installation

See the installation instructions at the [Arch Linux ARM ODROID-C2](https://archlinuxarm.org/platforms/armv8/amlogic/odroid-c2#installation) page.

## CPU frequency scaling

The [cpupower](https://www.archlinux.org/packages/?name=cpupower) package can be used to select alternative CPU governors for power savings. Edit `/etc/default/cpupower` and set the *governor=* line followed by [start](/index.php/Start "Start") cpupower.service.

### Show online/offline cores

If using the *hotplug* governor, idle cores are switched off to reduce power consumption and head generation.

```
lscpu |grep line

```

### Read CPU temperature

```
awk '{printf "%3.1f°C
", $1/1000}' /sys/class/thermal/thermal_zone0/temp

```

### Read CPU frequency

```
awk '{printf "%3.1f MHz
", $1/1000}' /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq

```

### Read CPU governor

```
cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor

```

## See also

*   [Arch Linux ARM ODROID-C2](https://archlinuxarm.org/platforms/armv8/amlogic/odroid-c2)
*   [ODROID-C2 Hardkernel Product Page](http://www.hardkernel.com/main/products/prdt_info.php?g_code=G145457216438)