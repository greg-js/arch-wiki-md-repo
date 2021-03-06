Related articles

*   [PHC](/index.php/PHC "PHC")
*   [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling")
*   [Improving performance](/index.php/Improving_performance "Improving performance")
*   [Benchmarking](/index.php/Benchmarking "Benchmarking")
*   [Fan speed control](/index.php/Fan_speed_control "Fan speed control")

Undervolting is a process where voltage to CPU is reduced in order to reduce its energy consumption and heat without affecting performance. Note that most desktop motherboards allow tweaking CPU voltage settings in BIOS as well.

**Warning:** Misconfiguration of CPU voltage settings might result in permanently damaged hardware. You have been warned!

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Overview](#Overview)
*   [2 Tools](#Tools)
    *   [2.1 intel-undervolt](#intel-undervolt)
        *   [2.1.1 Installation](#Installation)
        *   [2.1.2 Configuration and usage](#Configuration_and_usage)
    *   [2.2 amdctl](#amdctl)
        *   [2.2.1 Installation](#Installation_2)

## Overview

*   [PHC](/index.php/PHC "PHC") - a tool to undervolt some old generation Intel and AMD processors. **Not** compatible with `intel_pstate` [CPU frequency driver](/index.php/CPU_frequency_scaling#CPU_frequency_driver "CPU frequency scaling").
*   [#intel-undervolt](#intel-undervolt) - a tool for undervolting Haswell and newer Intel CPU using MSR. Compatible with `intel_pstate`.
*   [#amdctl](#amdctl) - a tool for undervolting K10 and newer AMD CPUs.
*   [K10ctl](/index.php/K10ctl "K10ctl") - overclock and undervolt an AMD K10 processor (e.g. Phenom, Phenom II) by changing its P-States.

## Tools

### intel-undervolt

[Intel-undervolt](https://github.com/kitsunyan/intel-undervolt) is a tool based on this [article](https://github.com/mihic/linux-intel-undervolt) for undervolting Haswell and newer Intel CPUs using [MSR](https://en.wikipedia.org/wiki/Model-specific_register "wikipedia:Model-specific register") and MCHBAR registers. In addition, it also allows to change power and temperature limits.

#### Installation

The tool can be installed as [intel-undervolt](https://aur.archlinux.org/packages/intel-undervolt/).

#### Configuration and usage

The following command prints *in use* voltage settings:

```
# intel-undervolt read

```

Now edit the configuration file `/etc/intel-undervolt.conf`. Example config with undervolted CPU Cache by -100mV:

**Note:** Looks like 'CPU' and 'GPU' values does not have any effect (at least on [ASUS Zenbook UX430UQ](/index.php/ASUS_Zenbook_UX430UQ "ASUS Zenbook UX430UQ") laptop).
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

### amdctl

[amdctl](https://github.com/kevinlekiller/amdctl/) is a tool for undervolting K10 and newer AMD CPUs.

#### Installation

The tool can be installed as [amdctl-git](https://aur.archlinux.org/packages/amdctl-git/).