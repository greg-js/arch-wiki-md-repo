# Dell Vostro 5470

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**Dell Vostro 5470**

This page deals with setting up Arch Linux on the Dell Vostro 5470 laptop.

I installed arch using Antergos.

## Contents

*   [1 CPU](#CPU)
*   [2 Touchscreen](#Touchscreen)
*   [3 GPU](#GPU)
    *   [3.1 Bumblebee and NVIDIA proprietary driver](#Bumblebee_and_NVIDIA_proprietary_driver)
*   [4 Networking](#Networking)
    *   [4.1 Ethernet](#Ethernet)
    *   [4.2 Wireless](#Wireless)

## CPU

This laptop has several CPU configurations and that will depend on the purchase. The one we are documenting has a Core i7-4500U CPU.

```
# uname -p

```

This CPU is capable of [frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling").

## Touchscreen

Worked out of the box.

## GPU

Card: NVIDIA Corporation GK208M [GeForce GT 740M]

### Bumblebee and NVIDIA proprietary driver

Install intel video driver

Install Bumblebee

Add yourself to bumblebee group

```
# systemctl enable bumblebeed

```

Install NVIDIA proprietary driver

[bbswitch](https://www.archlinux.org/packages/?name=bbswitch)

[primus](https://www.archlinux.org/packages/?name=primus)

## Networking

### Ethernet

Install [r8168](https://www.archlinux.org/packages/?name=r8168) kernel module.

Then blacklist the r8169:

 `/etc/modprobe.d/blacklist.conf`  `blacklist r8169` 

Restart or unload r8169:

```
# modprobe -r r8169

```

### Wireless

Worked out of the box

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dell_Vostro_5470&oldid=376414](https://wiki.archlinux.org/index.php?title=Dell_Vostro_5470&oldid=376414)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Dell](/index.php/Category:Dell "Category:Dell")