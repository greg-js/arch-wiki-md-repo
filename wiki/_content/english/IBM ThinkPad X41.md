The X41 and X41t (tablet) are both SATA-based machines that include a SATA-PATA bridge allowing the use of PATA HDDs, see external links for modifications to use SATA HDDs and SSDs. The laptops utilise a Pentium M processor (either 1.5GHz or 1.6GHz), the [Linux-ck](/index.php/Linux-ck "Linux-ck") packages contain optimised packages for this architecture.

This article contains some useful tweaks to make the most of your machine, the tweaks are mainly powersaving biased. With vanilla Arch, around 3 hours battery life was achieved, following powersaving tweaks a bit over than 5 hours was achieved, this was performed with screen brightness at the second highest value.

## Contents

*   [1 Installation](#Installation)
*   [2 Useful packages](#Useful_packages)
    *   [2.1 System Packages](#System_Packages)
    *   [2.2 Applications](#Applications)
*   [3 Powersaving tweaks](#Powersaving_tweaks)
    *   [3.1 laptop-mode (kernel)](#laptop-mode_.28kernel.29)
    *   [3.2 SATA-ALPM (pm-utils)](#SATA-ALPM_.28pm-utils.29)
    *   [3.3 Powersaving on PCI devices](#Powersaving_on_PCI_devices)
    *   [3.4 i915 RC6 powersaving](#i915_RC6_powersaving)
    *   [3.5 Disable NMI watchdog](#Disable_NMI_watchdog)
    *   [3.6 PHC](#PHC)
*   [4 Tablet support](#Tablet_support)
    *   [4.1 Getting display keys to work](#Getting_display_keys_to_work)
*   [5 External links](#External_links)

## Installation

Grab the .iso file from [the download page](https://www.archlinux.org/download/), write this to a memory stick ` sudo dd if=archlinux-201x.xx.xx-dual.iso of=/dev/sdX bs=4M` Restart the computer and boot into it like any other Arch installation.

## Useful packages

Some useful packages for your IBM/Lenovo ThinkPad X41:

### System Packages

*   [acpi](https://www.archlinux.org/packages/?name=acpi) - provides /proc/acpi, interesting things like lid state, temperatures, volume, brightness etc.
*   [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) - Driver supporting Wacom tablet screen.
*   [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) - Xorg driver for the Intel 915GM graphics chip.
*   [tp_smapi](https://www.archlinux.org/packages/?name=tp_smapi) - Adds support for SMAPI functions (battery discharge control, battery information, hdaps acceloremeter support). If you're using [Linux-ck](/index.php/Linux-ck "Linux-ck") try [tp_smapi-dkms](https://aur.archlinux.org/packages/tp_smapi-dkms/) (AUR).
*   [thinkfinger](https://www.archlinux.org/packages/?name=thinkfinger) - Driver for fingerprint reader.
*   See [TrackPoint](/index.php/TrackPoint "TrackPoint") for track point support.

The IBM X41 comes with a "ipw2915" wireless Centrino (A, B and G) or ipw2200 wireless Centrino (B and G) module, the kernel provides support for these two devices. [netctl](https://www.archlinux.org/packages/?name=netctl) has been tested and works flawlessly with the "ipw2915". See [Wireless network configuration#ipw2100 and ipw2200](/index.php/Wireless_network_configuration#ipw2100_and_ipw2200 "Wireless network configuration")

### Applications

*   [powertop](https://www.archlinux.org/packages/?name=powertop) - Measure power usage.
*   [cellwriter](https://www.archlinux.org/packages/?name=cellwriter) - (X41t) on-screen tablet keyboard.

**Note:** Thinkfan seems to fail due to thinkpad_acpi not having a fan_control function

*   [thinkfan](https://aur.archlinux.org/packages/thinkfan/) - Control the utilisation of the fan.
*   [gpm](https://www.archlinux.org/packages/?name=gpm) - Linux console mouse server.

## Powersaving tweaks

Initially without any powersaving tweaks, the X41 uses quite a lot of power (this can be monitored using [powertop](https://www.archlinux.org/packages/?name=powertop), it also provides suggestions for reducing power consumption). Here are some modifications that I found considerable improved the battery life of the X41t.

### laptop-mode (kernel)

Laptop mode is included in the kernel, it buffers disk activities to reduce utilisation of your HDD therefore saving a considerable amount of power. The effect with SSDs is less pronounced, but still saves some power.

 `echo "vm.laptop_mode=5" | sudo tee /etc/sysctl.d/laptop_mode.conf` 

### SATA-ALPM (pm-utils)

ALPM - Aggressive Link Power Management allows the SATA host bus adapter to enter a low power state when inactive therefore reducing power consumption.

```
echo "SATA_ALPM_ENABLE=true" | sudo tee /etc/pm/config.d/sata_alpm
sudo chmod +x /etc/pm/config.d/sata_alpm
```

### Powersaving on PCI devices

Powersaving isn't automatically enabled on devices as sometimes it causes issues, this can save about 2W.

 `/etc/udev/rules.d/pci_powersaving.rules`  `ACTION=="add", SUBSYSTEM=="pci", ATTR{power/control}="auto"` 

### i915 RC6 powersaving

See [Intel graphics#Module-based Powersaving Options](/index.php/Intel_graphics#Module-based_Powersaving_Options "Intel graphics").

### Disable NMI watchdog

The NMI watchdog is a debugging feature of the linux kernel that is enabled by default. It is useless for normal operation and significantly increases the number of CPU wakeups/second.

```
echo "kernel.nmi_watchdog=0" | sudo tee /etc/sysctl.d/nmi_watchdog.conf

```

### PHC

[PHC](/index.php/PHC "PHC") - Processor Hardware Control. [phc-intel](https://aur.archlinux.org/packages/phc-intel/) supports the Mobile Centrino line of processors and hence the X41, this program allows you to undervolt your CPU. Undervolting reduces the voltage(V) the processor runs at, because P=IV this will reduce your power consumption, this has no effect on performance, any excess voltage will be dissipated as heat, your laptop will run cooler and the fan will activate less frequently.

## Tablet support

The X41t utilises a Wacom digitiser for input, `pacman -S xf86-input-wacom` provides support for it. Once installed the driver should be activated following the next reboot.

### Getting display keys to work

If the display keys (Rotate, Escape, Enter, Prev, Next,...) on your X41 tablet aren't working, add `atkbd.softraw=0` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") in your boot loader configuration. Once they're producing [scancodes](/index.php/Extra_keyboard_keys "Extra keyboard keys"), you can [map them to keycodes](/index.php/Map_scancodes_to_keycodes#Using_setkeycodes "Map scancodes to keycodes").

# External links

*   This report has been listed in the [Linux Laptop and Notebook Installation Survey: IBM](http://tuxmobil.org/ibm.html).
*   [SATA support modification](http://www.placaware.com/?page_id=120)
*   [ThinkWiki X41 page](http://www.thinkwiki.org/wiki/Category:X41)
*   [T43p Cooling - applicable to X41t](http://linuxfocus.org/~guido/gentoo-tpt43p/cooling/), I've added ~1mm thick copper sheet to both the CPU and northbridge heatsinks with no ill effects.
*   [A shell/zenity script for common X41t tasks](https://paste.ee/p/EoSef)