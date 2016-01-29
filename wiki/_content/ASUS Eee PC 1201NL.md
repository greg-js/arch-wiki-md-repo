# ASUS Eee PC 1201NL

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Asus Eee PC 1201n](/index.php/Asus_Eee_PC_1201n "Asus Eee PC 1201n").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:ASUS Eee PC 1201NL#](https://wiki.archlinux.org/index.php/Talk:ASUS_Eee_PC_1201NL))

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Does not comply with [Help:Style](/index.php/Help:Style "Help:Style"). (Discuss in [Talk:ASUS Eee PC 1201NL#](https://wiki.archlinux.org/index.php/Talk:ASUS_Eee_PC_1201NL))

| **Device** | **Status** | **Modules** |
| Nvidia GeForce 9400M | **Working** | nvidia |
| Ethernet | **Working** | atl1e |
| Wireless | **Working** | rtl8192se |
| Audio | **Working** | snd_hda_intel |
| Camera | **Working** |
| Card Reader | **Working** |
| Function Keys | **Working** | acpi-eeepc-generic |
| Suspend2RAM | **Working** | pm-utils |
| Hibernate | **Working** | uswsusp-git |
| Multi-input touchpad | **Only emulation** |

**This is just a draft - more detailed instructions coming up soon + more detailed tests**

Netbook works flawlessly with Arch Linux (if you encounter freezes see Troubleshooting below)

## Contents

*   [1 HDD important issue](#HDD_important_issue)
*   [2 Graphics](#Graphics)
*   [3 Wireless](#Wireless)
*   [4 ACPI Functions](#ACPI_Functions)
    *   [4.1 Function Keys](#Function_Keys)
*   [5 Power management](#Power_management)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Machine does not resume after suspend2ram](#Machine_does_not_resume_after_suspend2ram)
    *   [6.2 After suspending the machine immediately resumes](#After_suspending_the_machine_immediately_resumes)
*   [7 Tips](#Tips)
    *   [7.1 1366x768 in console with NVIDIA proprietary driver](#1366x768_in_console_with_NVIDIA_proprietary_driver)

# HDD important issue

See [Laptop#Hard drive spin down problem](/index.php/Laptop#Hard_drive_spin_down_problem "Laptop").

# Graphics

See either [NVIDIA](/index.php/NVIDIA "NVIDIA") for the proprietary driver or [nouveau](/index.php/Nouveau "Nouveau") for the open-source driver.

# Wireless

There is native support from 3.0 kernel version with rtl8192se module.

# ACPI Functions

In order to use the function keys and extend battery life, you can set up the ACPI Driver, then install and configure the tools below.

The driver for the ACPI functions of the 1201N is called eeepc_laptop. It is part of the mainline kernel, so all that needs to be done is to load the module:

```
modprobe eeepc_laptop

```

If the command fails with such error message:

```
FATAL: Error inserting eeepc_laptop (/lib/modules/2.6.32-ARCH/kernel/drivers/platform/x86/eeepc-laptop.ko): No such device

```

you need to add _acpi_osi=Linux_ to kernel parameters in your bootloader configuration.

## Function Keys

You must have [acpid](/index.php/Acpid "Acpid") installed to use the Function keys.

After installing acpid, you will have to add it to your DAEMONS array in rc.conf.

Then, you need to install [acpi-eeepc-generic](https://aur.archlinux.org/packages/acpi-eeepc-generic/)<sup><small>AUR</small></sup> package from AUR and edit file **/etc/conf.d/acpi-eeepc-generic.conf**:

```
EEEPC_MODEL="1201N"

```

Comment out EEEPC_CONF_DONE option:

```
#EEEPC_CONF_DONE="no"

```

If you are using linux drivers for wifi you should also edit the WIFI_DRIVERS array:

```
WIFI_DRIVERS=("r8192se_pci")

```

Otherwise the wifi toggle button won't work.

Afterward, you must restart acipd:

```
/etc/rc.d/acpid restart

```

# Power management

See [Power management](/index.php/Power_management "Power management") and [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

# Troubleshooting

## Machine does not resume after suspend2ram

You have to unload r8192se_pci module right before suspending. See Suspend2RAM section of this article for details.

## After suspending the machine immediately resumes

You have to unload usb module(s) before suspending. See Suspend2RAM section of this article for details.

# Tips

## 1366x768 in console with NVIDIA proprietary driver

Load kernel with parameter acpi_osi=Linux

Reboot

Load kernel with parameters acpi_osi=Linux vga=0x034d

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_1201NL&oldid=408674](https://wiki.archlinux.org/index.php?title=ASUS_Eee_PC_1201NL&oldid=408674)"