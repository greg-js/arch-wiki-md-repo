This page contains instructions, tips, pointers, and links for installing and configuring Arch Linux on the Asus Eee PC [1201N](https://www.asus.com/Laptops/Eee_PC_1201N_Seashell/) and [1201PN](https://www.asus.com/Laptops/Eee_PC_1201PN_Seashell/).

The Asus Eee PC [1201NL](https://www.asus.com/Laptops/Eee_PC_1201NL_Seashell/) should be similar, but has a 32-bit Intel Atom N270 CPU and thus requires [Arch Linux 32](https://archlinux32.org/).

## Contents

*   [1 Installing Wireless](#Installing_Wireless)
*   [2 1201N lspci output](#1201N_lspci_output)
*   [3 1201NL hardware status](#1201NL_hardware_status)
*   [4 ACPI Functions](#ACPI_Functions)
    *   [4.1 Function Keys](#Function_Keys)
*   [5 Power management](#Power_management)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Machine does not resume after suspend2ram](#Machine_does_not_resume_after_suspend2ram)
    *   [6.2 After suspending the machine immediately resumes](#After_suspending_the_machine_immediately_resumes)
*   [7 1366x768 in console with NVIDIA proprietary driver (1201NL)](#1366x768_in_console_with_NVIDIA_proprietary_driver_.281201NL.29)
*   [8 cpufrequtils (1201N)](#cpufrequtils_.281201N.29)
*   [9 HDD important issue (1201NL)](#HDD_important_issue_.281201NL.29)
*   [10 Function Keys/Power Saving (1201PN)](#Function_Keys.2FPower_Saving_.281201PN.29)

## Installing Wireless

*   The 1201N has a Realtek 8191 Wireless card, despite what lspci reports that the computer has a Realtek 8171 (rev 10). The wireless driver is included in the Linux kernel and should work out of the box.
*   The 1201PN uses Atheros 9k drivers. This may not be the case with all 1201PNs, but at the very least, run `lspci -v` and look for your Network controller. If it is AR9285 Wireless Network Adapter, you can follow the instructions at [ASUS Eee PC#Installation](/index.php/ASUS_Eee_PC#Installation "ASUS Eee PC"). If evdev (it should) is not detecting your card, you will need to add `ath9k` to your `MODULES` array in [rc.conf](/index.php/Rc.conf "Rc.conf").
*   The 1201NL has native support from 3.0 kernel version with rtl8192se module.

## 1201N lspci output

```
$ lspci
00:00.0 Host bridge: nVidia Corporation MCP79 Host Bridge (rev b1)
00:00.1 RAM memory: nVidia Corporation MCP79 Memory Controller (rev b1)
00:03.0 ISA bridge: nVidia Corporation MCP79 LPC Bridge (rev b3)
00:03.1 RAM memory: nVidia Corporation MCP79 Memory Controller (rev b1)
00:03.2 SMBus: nVidia Corporation MCP79 SMBus (rev b1)
00:03.3 RAM memory: nVidia Corporation MCP79 Memory Controller (rev b1)
00:03.5 Co-processor: nVidia Corporation MCP79 Co-processor (rev b1)
00:04.0 USB Controller: nVidia Corporation MCP79 OHCI USB 1.1 Controller (rev b1)
00:04.1 USB Controller: nVidia Corporation MCP79 EHCI USB 2.0 Controller (rev b1)
00:06.0 USB Controller: nVidia Corporation MCP79 OHCI USB 1.1 Controller (rev b1)
00:06.1 USB Controller: nVidia Corporation MCP79 EHCI USB 2.0 Controller (rev b1)
00:08.0 Audio device: nVidia Corporation MCP79 High Definition Audio (rev b1)
00:09.0 PCI bridge: nVidia Corporation MCP79 PCI Bridge (rev b1)
00:0b.0 IDE interface: nVidia Corporation MCP79 SATA Controller (rev b1)
00:10.0 PCI bridge: nVidia Corporation MCP79 PCI Express Bridge (rev b1)
00:16.0 PCI bridge: nVidia Corporation MCP79 PCI Express Bridge (rev b1)
00:18.0 PCI bridge: nVidia Corporation MCP79 PCI Express Bridge (rev b1)
05:00.0 VGA compatible controller: nVidia Corporation ION VGA [GeForce 9400M] (rev b1)
07:00.0 Network controller: Realtek Semiconductor Co., Ltd. RTL8191SEvA Wireless LAN Controller (rev 10)
09:00.0 Ethernet controller: Atheros Communications AR8132 Fast Ethernet (rev c0)

```

```
$ lsusb
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 003: ID 0b05:1788 ASUSTek Computer, Inc. BT-270 Bluetooth Adapter
Bus 004 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 002: ID 13d3:5111 IMC Networks Integrated Webcam
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub

```

```
$ hciconfig hci0 version
hci0:   Type: Primary  Bus: USB
        BD Address: XX:XX:XX:XX:XX:XX  ACL MTU: 1021:8  SCO MTU: 64:1
        HCI Version: 3.0 (0x5)  Revision: 0x1c1
        LMP Version: 3.0 (0x5)  Subversion: 0x4203
        Manufacturer: Broadcom Corporation (15)

```

## 1201NL hardware status

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

## ACPI Functions

In order to use the function keys and extend battery life, you can set up the ACPI Driver, then install and configure the tools below.

The driver for the ACPI functions of the 1201N is called eeepc_laptop. It is part of the mainline kernel, so all that needs to be done is to load the module:

```
modprobe eeepc_laptop

```

If the command fails with such error message:

```
FATAL: Error inserting eeepc_laptop (/lib/modules/2.6.32-ARCH/kernel/drivers/platform/x86/eeepc-laptop.ko): No such device

```

you need to add *acpi_osi=Linux* to kernel parameters in your bootloader configuration.

### Function Keys

You must have [acpid](/index.php/Acpid "Acpid") installed and running to use the Function keys.

Then, you need to install [acpi-eeepc-generic](https://aur.archlinux.org/packages/acpi-eeepc-generic/) package from AUR and edit file **/etc/conf.d/acpi-eeepc-generic.conf**:

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

Afterward, you must restart acipd.

## Power management

See [Power management](/index.php/Power_management "Power management") and [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

## Troubleshooting

### Machine does not resume after suspend2ram

You have to unload r8192se_pci module right before suspending. See Suspend2RAM section of this article for details.

### After suspending the machine immediately resumes

You have to unload usb module(s) before suspending. See Suspend2RAM section of this article for details.

## 1366x768 in console with NVIDIA proprietary driver (1201NL)

Load kernel with parameter acpi_osi=Linux

Reboot

Load kernel with parameters acpi_osi=Linux vga=0x034d

## cpufrequtils (1201N)

The Intel Atom 330 does not support cpufrequtils in any reasonable way, so it is not recommended that you use cpufrequtils. You can disable it in /etc/laptop-mode/conf.d/cpufreq.conf:

```
CONTROL_CPU_FREQUENCY=0

```

Because the Atom uses so little power anyway, controlling the FSB using the "SuperHybrid Engine" should provide significant gain in battery life without the need for CPU scaling.

## HDD important issue (1201NL)

See [Laptop#Hard drive spin down problem](/index.php/Laptop#Hard_drive_spin_down_problem "Laptop").

## Function Keys/Power Saving (1201PN)

BE CAREFUL with laptop power-mode settings. The default settings will spin your harddrive down every 20 seconds which is really bad. Read [this thread](https://bbs.archlinux.org/viewtopic.php?id=39258).

You can follow the instructions as outlined in the directions for the 1201NL to get your function keys working.

The acpi-generic-package scripts in the AUR are not necessary to get your function keys working. They are hardware agnostic, so they are nice to get things up and running quickly, but with the exception of the sleep/suspend scripts (which are useful) everything else can be done more quickly with a direct keybinding.

Disable the other settings and use your WMs default keybinding manager (or Xbindkeys) to handle your Wlan/Display/Volume settings.

[Xbindkeys](/index.php/Xbindkeys "Xbindkeys") Simply bind your keys to the necessary action.