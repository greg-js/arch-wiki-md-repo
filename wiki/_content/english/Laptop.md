This **Laptop main page** contains links to article (sections) needed for configuring a laptop for the best experience. Setting up a laptop is in many ways the same as setting up a desktop. However, there are a few key differences. Arch Linux provides all the tools and programs necessary to take complete control of your laptop. These programs and utilities are highlighted below, with appropriate tips tutorials.

To gain an overview of the reported/achieved Linux hardware compatibility of a particular laptop model, see the results per vendor of below subpages.

| **Laptop main page** |
| [Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - [Other](/index.php/Laptop/Other "Laptop/Other") |

If there are laptop model specific instructions, the respective article is crosslinked in the first column of the vendor subpages. In case the model is not listed in the vendor table, existing instructions of similar models via the [Category:Laptops](/index.php/Category:Laptops "Category:Laptops") vendor subcategory may help.

## Contents

*   [1 Power management](#Power_management)
    *   [1.1 Battery state](#Battery_state)
        *   [1.1.1 ACPI](#ACPI)
        *   [1.1.2 hibernate on low battery level](#hibernate_on_low_battery_level)
            *   [1.1.2.1 Testing events](#Testing_events)
    *   [1.2 Suspend and Hibernate](#Suspend_and_Hibernate)
    *   [1.3 Hard drive spin down problem](#Hard_drive_spin_down_problem)
*   [2 Hardware support](#Hardware_support)
    *   [2.1 Screen brightness](#Screen_brightness)
    *   [2.2 Touchpad](#Touchpad)
    *   [2.3 Fingerprint Reader](#Fingerprint_Reader)
    *   [2.4 Webcam](#Webcam)
    *   [2.5 Hard disk shock protection](#Hard_disk_shock_protection)
    *   [2.6 Hybrid graphics](#Hybrid_graphics)
*   [3 Network time syncing](#Network_time_syncing)
*   [4 See also](#See_also)

## Power management

**Note:** You should read the main article [Power management](/index.php/Power_management "Power management"). Additional laptop-specific features are described below.

Power management is very important for anyone who wishes to make good use of their battery capacity. The following tools and programs help to increase battery life and keep your laptop cool and quiet.

### Battery state

Reading battery state can be done in multiple ways. Classical method is some daemon periodically polling battery level using ACPI interface. On some systems, the battery sends events to [udev](/index.php/Udev "Udev") whenever it (dis)charges by 1%, this event can be connected to some action using a udev rule.

#### ACPI

Battery state can be read using ACPI utilities from the terminal. ACPI command line utilities are provided via the [acpi](https://www.archlinux.org/packages/?name=acpi) package. See [ACPI modules](/index.php/ACPI_modules "ACPI modules") for more information.

*   [cbatticon](https://www.archlinux.org/packages/?name=cbatticon) is a lightweight and fast battery icon that sits in the system tray.
*   [batterymon-clone](https://aur.archlinux.org/packages/batterymon-clone/) is a simple battery monitor that sits in the system tray, similar to batti.

#### hibernate on low battery level

If your battery sends events to [udev](/index.php/Udev "Udev") whenever it (dis)charges by 1%, you can use this udev rule to automatically hibernate the system when battery level is critical, and thus prevent all unsaved work from being lost.

 `/etc/udev/rules.d/99-lowbat.rules` 
```
# Suspend the system when battery level drops to 5% or lower
SUBSYSTEM=="power_supply", ATTR{status}=="Discharging", ATTR{capacity}=="[0-5]", RUN+="/usr/bin/systemctl hibernate"

```

Batteries can jump to a lower value instead of discharging continuously, therefore a udev string matching pattern for all capacities 0 through 5 is used.

Other rules can be added to perform different actions depending on power supply status and/or capacity.

If your system has no or missing ACPI events, use [cron](/index.php/Cron "Cron") with the following script:

```
#!/bin/sh
acpi -b | awk -F'[,:%]' '{print $2, $3}' | {
	read -r status capacity

	if [ "$status" = Discharging -a "$capacity" -lt 5 ]; then
		logger "Critical battery threshold"
		systemctl hibernate
	fi
}

```

##### Testing events

One way to test udev rules is to have them create a file when they are run. For example:

 `/etc/udev/rules.d/98-discharging.rules` 
```
SUBSYSTEM=="power_supply", ATTR{status}=="Discharging", RUN+="/usr/bin/touch /home/example/discharging"

```

This creates a file at `/home/example/discharging` when the laptop charger is unplugged. You can test whether the rule worked by unplugging your laptop and looking for this file. For more advanced udev rule testing, see [Udev#Testing rules before loading](/index.php/Udev#Testing_rules_before_loading "Udev").

### Suspend and Hibernate

Manually suspending the operating system, either to memory (standby) or to disk (hibernate) sometimes provides the most efficient way to optimize battery life, depending on the usage pattern of the laptop.

See the main article [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

### Hard drive spin down problem

Documented [here](https://bugs.launchpad.net/ubuntu/+source/acpi-support/+bug/59695).

To prevent your laptop hard drive from spinning down too often, set less aggressive power management as described in [hdparm#Power management configuration](/index.php/Hdparm#Power_management_configuration "Hdparm"). Even the default values may be too aggressive.

## Hardware support

### Screen brightness

See [Backlight](/index.php/Backlight "Backlight").

### Touchpad

To get your touchpad working properly, see the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") page. Note that your laptop may have an ALPS touchpad (such as the DELL Inspiron 6000), and not a Synaptics touchpad. In either case, see the link above.

### Fingerprint Reader

See [Fingerprint-gui](/index.php/Fingerprint-gui "Fingerprint-gui"), [fprint](/index.php/Fprint "Fprint") and [ThinkFinger](/index.php/ThinkFinger "ThinkFinger") (for ThinkPads).

### Webcam

See [Webcam setup](/index.php/Webcam_setup "Webcam setup").

### Hard disk shock protection

There are several laptops from different vendors featuring shock protection capabilities. As manufacturers have refused to support open source development of the required software components so far, Linux support for shock protection varies considerably between different hardware implementations.

Currently, two projects, named [HDAPS](/index.php/HDAPS "HDAPS") and [Hpfall](/index.php/Hpfall "Hpfall") (available in the [AUR](/index.php/AUR "AUR")), support this kind of protection. HDAPS is for IBM/Lenovo Thinkpads and hpfall for HP/Compaq laptops.

### Hybrid graphics

The laptop manufacturers developed new technologies involving two graphic cards in an single computer, enabling both high performance and power saving usages. These laptops usually use an Intel chip for display by default, so an [Intel graphics](/index.php/Intel_graphics "Intel graphics") driver is needed first. Then you can [choose methods](/index.php/Hybrid_graphics "Hybrid graphics") to utilize the second graphics chip.

## Network time syncing

For a laptop, it may be a good idea to use [Chrony](/index.php/Chrony "Chrony") as an alternative to [NTPd](/index.php/NTPd "NTPd") or [OpenNTPD](/index.php/OpenNTPD "OpenNTPD") to sync your clock over the network. Chrony is designed to work well even on systems with no permanent network connection (such as laptops), and is capable of much faster time synchronisation than standard ntp. Chrony has several advantages when used in systems running on virtual machines, such as a larger range for frequency correction to help correct quickly drifting clocks, and better response to rapid changes in the clock frequency. It also has a smaller memory footprint and no unnecessary process wakeups, improving power efficiency.

## See also

	General

*   [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") is a technology used primarily by notebooks which enables the OS to scale the CPU frequency up or down, depending on the current system load and/or power scheme.
*   [Display Power Management Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling") describes how to automatically turn off the laptop screen after a specified interval of inactivity (not just blanked with a screensaver but completely shut off).
*   [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") provides information about setting up wireless connection.
*   [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") describes configuration of Media keys.
*   [acpid](/index.php/Acpid "Acpid") which is a flexible and extensible daemon for delivering ACPI events.

	Pages specific to certain laptop types

*   See [Category:Laptops](/index.php/Category:Laptops "Category:Laptops") and its subcategories for pages dedicated to specific models/vendors.
*   Battery tweaks for ThinkPads can be found in [TLP](/index.php/TLP "TLP") and the [tp_smapi](/index.php/Tp_smapi "Tp smapi") article.
*   [acerhdf](/index.php/Acer_Aspire_One#acerhdf "Acer Aspire One") is a kernel module for controlling fan speed on Acer Aspire One and some Packard Bell Notebooks.

	External resources

*   [http://www.linux-on-laptops.com/](http://www.linux-on-laptops.com/)
*   [http://www.linlap.com/](http://www.linlap.com/)