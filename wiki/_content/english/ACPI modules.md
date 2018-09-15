Related articles

*   [acpid](/index.php/Acpid "Acpid")
*   [DSDT](/index.php/DSDT "DSDT")

From [ACPI site](http://www.acpi.info/):

	*ACPI (Advanced Configuration and Power Interface) is an open industry specification co-developed by Hewlett-Packard, Intel, Microsoft, Phoenix, and Toshiba.*

ACPI modules are kernel modules for different ACPI parts. They enable special ACPI functions or add information to `/proc` or `/sys`. These information can be parsed by [acpid](/index.php/Acpid "Acpid") for events or other monitoring applications.

## Contents

*   [1 Which modules are available?](#Which_modules_are_available.3F)
*   [2 How to select the correct ones](#How_to_select_the_correct_ones)
*   [3 Getting information](#Getting_information)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 DSDT fix](#DSDT_fix)
    *   [4.2 ACPI fix for notebooks](#ACPI_fix_for_notebooks)
*   [5 See also](#See_also)

## Which modules are available?

This is a small list and summary of ACPI kernel modules:

*   ac (power connector status)
*   asus-laptop (useful on ASUS/medion laptops)
*   battery (battery status)
*   bay (bay status)
*   button (catch button events, like LID or POWER BUTTON)
*   container (container status)
*   dock (docking station status)
*   fan (fan status)
*   i2c_ec (EC SMBUs driver)
*   thinkpad_acpi (useful on Lenovo Thinkpad laptops)
*   processor (processor status)
*   sbs (smart battery status)
*   thermal (status of thermal sensors)
*   toshiba_acpi (useful for Toshiba laptops)
*   video (status of video devices)

complete list of your running kernel:

 `$ ls -l /usr/lib/modules/$(uname -r)/kernel/drivers/acpi` 
```
total 112
-rw-r--r-- 1 root root  2808 Aug 29 23:58 ac.ko.gz
-rw-r--r-- 1 root root  3021 Aug 29 23:58 acpi_ipmi.ko.gz
-rw-r--r-- 1 root root  3354 Aug 29 23:58 acpi_memhotplug.ko.gz
-rw-r--r-- 1 root root  4628 Aug 29 23:58 acpi_pad.ko.gz
drwxr-xr-x 2 root root  4096 Aug 29 23:59 apei
-rw-r--r-- 1 root root  7120 Aug 29 23:58 battery.ko.gz
-rw-r--r-- 1 root root  3700 Aug 29 23:58 button.ko.gz
-rw-r--r-- 1 root root  2181 Aug 29 23:58 container.ko.gz
-rw-r--r-- 1 root root  1525 Aug 29 23:58 custom_method.ko.gz
-rw-r--r-- 1 root root  1909 Aug 29 23:58 ec_sys.ko.gz
-rw-r--r-- 1 root root  2001 Aug 29 23:58 fan.ko.gz
-rw-r--r-- 1 root root  1532 Aug 29 23:58 hed.ko.gz
-rw-r--r-- 1 root root  3241 Aug 29 23:58 pci_slot.ko.gz
-rw-r--r-- 1 root root 17742 Aug 29 23:58 processor.ko.gz
-rw-r--r-- 1 root root  3073 Aug 29 23:58 sbshc.ko.gz
-rw-r--r-- 1 root root  7098 Aug 29 23:58 sbs.ko.gz
-rw-r--r-- 1 root root  6311 Aug 29 23:58 thermal.ko.gz
-rw-r--r-- 1 root root  8891 Aug 29 23:58 video.ko.gz

```

## How to select the correct ones

You have to try yourself which module works for your machine:

 `# modprobe <yourmodule>` 

then check if the module is supported on your hardware by using

 `$ dmesg` 
**Tip:** It may help to add a grep text search to narrow your results.

```
$ dmesg | grep acpi
[    0.000000] ACPI: LAPIC (acpi_id[0x00] lapic_id[0x00] enabled)
[    0.000000] ACPI: LAPIC (acpi_id[0x01] lapic_id[0x04] enabled)
[    0.000000] ACPI: LAPIC (acpi_id[0x02] lapic_id[0x01] enabled)
[    0.000000] ACPI: LAPIC (acpi_id[0x03] lapic_id[0x05] enabled)
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x00] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x01] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x02] high edge lint[0x1])
[    0.000000] ACPI: LAPIC_NMI (acpi_id[0x03] high edge lint[0x1])
[    5.066752] ACPI: acpi_idle yielding to intel_idle
[    5.438998] acpi device:04: registered as cooling_device4

```

Add the working ones to configuration files in `/etc/modules-load.d`. `/etc/modules-load.d` is described in [Kernel modules#Automatic module handling](/index.php/Kernel_modules#Automatic_module_handling "Kernel modules").

## Getting information

To read out battery information, you can simply [install](/index.php/Install "Install") the package [acpi](https://www.archlinux.org/packages/?name=acpi) in the [official repositories](/index.php/Official_repositories "Official repositories") and run:

```
acpi -i

```

Using `/proc` to store ACPI information has been discouraged and deprecated since Linux 2.6.24\. The same data is available in `/sys` now, and interested parties can (should) subscribe to ACPI events from the kernel via netlink. For example, for battery:

```
/sys/class/power_supply/BAT0/

```

## Troubleshooting

### DSDT fix

If problems with power management persist despite having loaded the proper modules, a Linux-unfriendly [DSDT](https://en.wikipedia.org/wiki/DSDT#ACPI_Tables "wikipedia:DSDT") might be the cause. See the wiki article on [DSDT](/index.php/DSDT "DSDT").

### ACPI fix for notebooks

Sometimes you see "ACPI: EC: input buffer is not empty, aborting transaction". This is a problem with ACPI, more specifically an incompatibility of the BIOS. There may be four ways to solve this issue:

*   If available, update the BIOS.

*   Use `acpi=off` as [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), however this will kill all ACPI functionality like battery charging and power saving.

*   In some cases disabling [DPMS](/index.php/DPMS "DPMS") has been reported to solve the issue [[1]](https://ubuntuforums.org/showthread.php?p=8030130#10). However, screen brightness may no longer be fully controllable: `$ xset dpms force off` 

*   Build a custom [kernel](/index.php/Kernel "Kernel") with patches of [bugs.launchpad.net](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/578506).

## See also

*   [Wikipedia:Advanced Configuration and Power Interface](https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface "wikipedia:Advanced Configuration and Power Interface")