Related articles

*   [PHC](/index.php/PHC "PHC")
*   [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling")
*   [Improving performance](/index.php/Improving_performance "Improving performance")
*   [Benchmarking](/index.php/Benchmarking "Benchmarking")
*   [Fan speed control](/index.php/Fan_speed_control "Fan speed control")

Undervolting is a process through which voltage to computer processors and components is decreased dynamically on run-time. It is a process within dynamic voltage scaling that enables conserving electric voltage to reduce energy consumption and heat produced by computing components without affecting their performance.

## Contents

*   [1 Overview](#Overview)
*   [2 Tools](#Tools)
    *   [2.1 intel-undervolt](#intel-undervolt)
        *   [2.1.1 Installation](#Installation)
        *   [2.1.2 Configuration and usage](#Configuration_and_usage)

## Overview

*   [PHC](/index.php/PHC "PHC") - a tool to undervolt some old generation Intel and AMD processors. **Not** compatible with `intel_pstate` [CPU frequency driver](/index.php/CPU_frequency_scaling#CPU_frequency_driver "CPU frequency scaling").
*   [#intel-undervolt](#intel-undervolt) - a tool for undervolting Haswell and newer Intel CPU using MSR. Compatible with `intel_pstate`.

## Tools

### intel-undervolt

intel-undervolt is a tool for undervolting Haswell and newer Intel CPU using MSR. This tool is based on the content of this [article](https://github.com/mihic/linux-intel-undervolt). This tool also allow to alter power limits and temperature limit using MSR and MCHBAR registers.

#### Installation

The tool can be installed as [intel-undervolt](https://aur.archlinux.org/packages/intel-undervolt/).

#### Configuration and usage

The following command prints *in use* voltage settings:

```
# intel-undervolt read

```

Now edit the configuration file `/etc/intel-undervolt.conf`. Example config with undervolted CPU Cache by -100mV:

**Note:** Looks like 'CPU' and 'GPU' values does not have any effect (at least on [ASUS Zenbook UX430UQ](/index.php/ASUS_Zenbook_UX430/UX530 "ASUS Zenbook UX430/UX530") laptop).
 `/etc/intel-undervolt.conf` 
```
...
apply 0 'CPU' 0
apply 1 'GPU' 0
apply 2 'CPU Cache' -100
apply 3 'System Agent' 0
apply 4 'Analog I/O' 0
...

```

Once you saved configuration file - test it:

```
# intel-undervolt apply

```

It will print *Success* if settings were applied. You can double check *in use* configuration using the following command:

```
# intel-undervolt read

```

Once you find stable configuration, you can also [enable](/index.php/Enable "Enable") `intel-undervolt.service` to make changes persistent.