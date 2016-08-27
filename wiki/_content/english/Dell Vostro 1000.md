## Contents

*   [1 Hardware](#Hardware)
*   [2 Problems](#Problems)
    *   [2.1 "Unknown Key Pressed"](#.22Unknown_Key_Pressed.22)
    *   [2.2 High Temperature](#High_Temperature)
*   [3 Installation](#Installation)
*   [4 Xorg](#Xorg)
*   [5 Wireless](#Wireless)
*   [6 Suspend/Hibernate](#Suspend.2FHibernate)
    *   [6.1 Resume not working after suspend to RAM](#Resume_not_working_after_suspend_to_RAM)
    *   [6.2 Backlight does not come back after Resume](#Backlight_does_not_come_back_after_Resume)

## Hardware

| **Device** | **Status** | **Modules** |
| Ati Radeon Xpress | **Working** | fglrx (cataylst), radeon |
| Ethernet | **Working** | b44 |
| Wireless | **Working** | [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/), b43, ndiswrapper |
| Audio | **Working** | snd_hda_intel |
| Modem | **Untested** |
| PCMCIA Slot | **Untested** |
| Card Reader | **Working** |

## Problems

### "Unknown Key Pressed"

*   You may occasionally run across an error (occurring in an extremely high frequency) in your messages.log/dmesg:

```
 atkbd.c: Unknown key pressed (translated set 2, code 0xee on isa0060/serio0).
 atkbd.c: Use 'setkeycodes e06e <keycode>' to make it known.

```

*   The fix for this issue is fairly simple. Power down your dell laptop, and reseat the battery.
*   Another possible cause may be due to your AC adapter being unplugged from the outlet, yet attached to the back of your laptop.
*   Yet another suggested fix for the problem is updating your BIOS.. but since this is an extreme measure (found on the ubuntu forums.. so take it with a grain of salt), try the first two solutions before moving on to this potentially dangerous measure.

### High Temperature

After the installation you will see that the temperature is around 60°C (Too High). You can get the temperature through:

```
cat /proc/acpi/thermal_zone/THRM/temperature

```

or

```
cat /proc/acpi/thermal_zone/THM/temperature

```

This is because the CPU frequency is at full usage always... so before continuing with the install process install **cpufrequtils**, you can see further details on [Cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils")

*   Note: using lm_sensors 'sensors' utility, k8temp-pci-00c3 reports much more reasonable temperatures (more along the lines of what windows reports) compared to this Virtual Thermal Zone. [I](/index.php?title=User:Igneous&action=edit&redlink=1 "User:Igneous (page does not exist)") have noticed no issues running without cpu scaling while on AC.

## Installation

Follow the [Installation guide](/index.php/Installation_guide "Installation guide").

## Xorg

Follow [Xorg](/index.php/Xorg "Xorg"), [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") and [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys").

## Wireless

Follow [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") and [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless").

## Suspend/Hibernate

*   Suspend and Hibernate works with pm-utils
*   Also works by issuing `echo mem > /sys/power/state` 

### Resume not working after suspend to RAM

To workaround this issue edit the file `/boot/grub/menu.lst` and add the following to the kernel boot line: `hpet=disable` 

### Backlight does not come back after Resume

You may need a workaround because the backlight does not come back after Resuming.

Install [Pm-utils](/index.php/Pm-utils "Pm-utils"), and create this file:

	**/etc/pm/sleep.d/radeonlight**

```
#!/bin/bash
case $1 in
 hibernate)
  echo "Suspending to disk!"
 ;;
 suspend)
  echo "Suspending to RAM"
 ;;
 thaw)
  echo "Suspend to disk is over, Resuming. .."
 ;;
 resume)
  echo "Suspend to RAM is over, Resuming..."
  radeontool light on
  radeontool dac on
 ;;
 *)  echo "somebody is calling me totally wrong."
 ;;
esac

```

```
# chmod +x /etc/pm/sleep.d/radeonlight

```

Now to make it work you need [radeontool](https://www.archlinux.org/packages/?name=radeontool).

And **DONE**, you can suspend and resume with pm-utils normally.