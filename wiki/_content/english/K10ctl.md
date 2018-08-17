**Note:** The last release was in 2009.[[1]](https://sourceforge.net/projects/k10ctl/files/)

[k10ctl](https://sourceforge.net/projects/k10ctl/) allows you to overclock and undervolt an AMD K10 processor (e.g. Phenom, Phenom II) by changing its P-States.

Lowering the voltage saves energy and leads to less heat and noise.

**Warning:** Use this program at your own risk. It may damage your hardware.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 k10ctl.conf](#k10ctl.conf)
    *   [2.2 Pre-Configuration](#Pre-Configuration)
    *   [2.3 How to calculate values](#How_to_calculate_values)
    *   [2.4 Enable k10ctl permanently](#Enable_k10ctl_permanently)
*   [3 Tips and tricks](#Tips_and_tricks)

## Installation

k10ctl is available in the AUR: [k10ctl](https://aur.archlinux.org/packages/k10ctl/)

## Configuration

### k10ctl.conf

 `/etc/conf.d/k10ctl` 
```
# For information how to calculate the following values see:
# http://www.ztex.de/misc/k10ctl.e.html#c1

# Change to "true" after you configurated the settings for your CPU
# WARNING: Be SURE that the following values are correct and safe for
# your system before doing this!
CONFIGURATED=false

# Number of cores for your CPU
CORES=4

# List of P-states you want to change.
# NOTE: all following arrays must have the same size!
PSTATES=( 0 1 2 3 )

# List of Northbridge VIDs
NBVID=( 45 45 45 45 )

# List of CPU VIDs
CPUVID=( 36 45 55 68 )

# List of CPU FIDs
FID=( 12 5 0 0 )

# List of CPU DIDs
DID=( 0 0 0 1 )

```

### Pre-Configuration

k10ctl needs the kernel module **msr**, so run

```
# modprobe msr

```

Now you have to find out the default values of the P-States for your CPU.

```
# k10ctl 0-3

```

0-3 are the CPU cores so if you have less, decrease the second number.

Adjust your config with the correct numbers from the output.

**Tip:** The important lines are "P-State 0" - "P-State X".

When you are sure everything is correct, set "CONFIGURATED" to "true" and restart k10ctl:

```
# systemctl start k10ctl

```

Up to now k10ctl should work with the default values of your CPU.

### How to calculate values

Check "VID interface mode" to know how to calculate your settings.

```
# k10ctl 0-3 -> first line

```

Parallel VID interface mode:

```
 if vid>=64 then U=375 mV
 else if vid>=32 then U=1162.5mV - vid=12.5 mV
 else U=1550mV - vid*25 mV

```

Serial VID interface mode:

```
 if vid>=124 then U=0 mV
 else U=1550mV - vid*12.5 mV

```

Finally you can modify your P-States in `/etc/conf.d/k10ctl`.

**Note:** All arrays in the config must have the same size.

Restart k10ctl and check "k10ctl 0-3" again.

```
# systemctl start k10ctl

```

```
# k10ctl 0-3

```

### Enable k10ctl permanently

```
# systemctl enable k10ctl

```

For the module 'msr' take a look at [Kernel modules#Automatic_module_handling](/index.php/Kernel_modules#Automatic_module_handling "Kernel modules").

## Tips and tricks

Use [mprime](https://aur.archlinux.org/packages/mprime/) to test the stability of your computer.