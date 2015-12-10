# Acer Extensa 5200

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Acer Extensa 5200#](https://wiki.archlinux.org/index.php/Talk:Acer_Extensa_5200))

Basic informations about that laptop. Some parameters may be diffrent

## Contents

*   [1 Hardware](#Hardware)
*   [2 Kernel](#Kernel)
*   [3 Networking](#Networking)
    *   [3.1 Wireless](#Wireless)
*   [4 Power Management](#Power_Management)
    *   [4.1 ACPI](#ACPI)
    *   [4.2 CPU frequency scaling](#CPU_frequency_scaling)
    *   [4.3 Hibernate](#Hibernate)
*   [5 Xorg](#Xorg)
*   [6 External Resources](#External_Resources)

# Hardware

**Processor:** Intel Celeron M 440 @ 1.86

**Video:** Intel Corporation Mobile 915GM/GMS/910GML Express Integrated Graphics Controller (rev 03)

**Audio:** Intel Corporation 82801G (ICH7 Family) High Definition Audio Controller (rev 02)

**Wired NIC:** Broadcom Corporation BCM4401-B0 100Base-TX Ethernet (rev 02)

**Wireless NIC:** Broadcom Corporation Dell Wireless 1390 Wlan Mini-PCI Card (ref 01)

# Kernel

On default kernel everything seems to be ok, but if you want to hibernate you need kernel23-suspend2

# Networking

Ethernet works fine

## Wireless

See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless").

# Power Management

## ACPI

Just install [acpid](/index.php/Acpid "Acpid") and [acpitool](https://aur.archlinux.org/packages/acpitool/)<sup><small>AUR</small></sup>.

now everything should work fine. After reboot you can check it by

```
$ acpitool 
 Battery #1     : charged, 100.0%
 AC adapter     : on-line
 Thermal zone 1 : ok, 46 C
 Thermal zone 2 : ok, 46 C

```

## CPU frequency scaling

See [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling").

## Hibernate

Follow the manual about [Suspend to Disk](/index.php/Suspend_to_Disk "Suspend to Disk")

After configuration uncomment

```
Runi915resolution yes

```

# Xorg

install 915resolution by

```
pacman -S 915resolution

```

edit /etc/conf.d/915resolution and insert lines

```
MODE="38"
RESOLUTION="1280 800"

```

Add 915resolution to startup scripts in /etc/rc.conf

```
DAEMONS=( 915resolution )

```

Before you start binding your special keys you need set keymap. My keymap is [Here](/index.php/Acer_Extensa_5200/keymap "Acer Extensa 5200/keymap") . You need save it in the file, and load when you start Xorg.

```
xmodmap keymap

```

# External Resources

*   This report has been listed in the [Linux Laptop and Notebook Installation Guides Survey: Acer](http://tuxmobil.org/acer.html).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Acer_Extensa_5200&oldid=399423](https://wiki.archlinux.org/index.php?title=Acer_Extensa_5200&oldid=399423)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Acer](/index.php/Category:Acer "Category:Acer")