# Dell Studio XPS 13

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

I have just bought a new Dell Studio XPS 13\. I have not been able to find any information for installing Arch Linux on this machine. It is a very nice looking laptop, and runs fast and smooth. I have had a successful install (32-bit only, 64-bit). I still have a few things to get working, like the Bluetooth, and media buttons.

System Specs:

*   **Processor**
    *   Intel(R) Core(TM)2 Duo CPU P8600 @ 2.40GHz
*   **RAM Memory**
    *   4 GB DDR3
*   **Webcam**
    *   2.0 Megapixel Webcam
*   **Hard Disk**
    *   320GB SATA 7200 rpm HDD
    *   500GB SATA 7200 rpm HDD
*   **Video Card**
    *   NVIDIA 9400M
    *   NVIDIA 9500M (9400M G + 9200M GS)
*   **Wireless**
    *   Broadcom Corporation BCM4322 802.11a/b/g/n Wireless LAN Controller
    *   Atheros Communications Inc. AR928X Wireless Network Adapter

The basic installation performs normally, with the core cd, also the wireless modules ( Atheros wifi card ) were well recognised and worked out of the box.

## Contents

*   [1 Power Management](#Power_Management)
    *   [1.1 HDD important issue](#HDD_important_issue)
    *   [1.2 Hybernation - Suspend](#Hybernation_-_Suspend)
*   [2 Touchpad](#Touchpad)

## Power Management

### HDD important issue

See [Laptop#Hard drive spin down problem](/index.php/Laptop#Hard_drive_spin_down_problem "Laptop").

### Hybernation - Suspend

This feature works very well, See [pm-utils](/index.php/Pm-utils "Pm-utils")

Make sure acpid is installed and running. You can add it to the DAEMONS array in /etc/rc.conf.

Then edit these files...

/etc/acpi/actions/lm_lid.sh:

```
sh ~/bin/suspend

```

(Taken from [http://www.linux.com/news/hardware/laptops/8253-how-to-suspend-and-hibernate-a-laptop-under-linux](http://www.linux.com/news/hardware/laptops/8253-how-to-suspend-and-hibernate-a-laptop-under-linux) [+] with a little modification)

~/bin/suspend:

```
#!/bin/sh

# discover video card's ID
ME=`whoami`
if [ "$ME" != "root" ]; then
    echo "You must be root!"
    exit 1
fi

ID=`lspci | grep VGA | awk '{ print $1 }' | sed -e 's@0000:@@' -e 's@:@/@'`

# securely create a temporary file

TMP_FILE=`mktemp /var/tmp/video_state.XXXXXX`trap 'rm -f $TMP_FILE' 0 1 15

# switch to virtual terminal 1 to avoid graphics
# corruption in X

chvt 1

# write all unwritten data (just in case)

sync

# dump current data from the video card to the
# temporary filecat 

/proc/bus/pci/$ID > $TMP_FILE

# suspend

echo -n mem > /sys/power/state

# restore video card data from the temporary file
# on resume

cat $TMP_FILE > /proc/bus/pci/$ID

# switch back to virtual terminal 7 (running X)
chvt 7

# remove temporary file
rm -f $TMP_FILE

```

This should suspend your laptop to RAM when the lid is closed.

## Touchpad

The touchpad does not work completely out of the box. By default only the mouse buttons are working. To get the touchpad working, especially the area to move the mouse, follow the instructions described on the wiki page [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics"). Just installing the package and an X restart should do the trick.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dell_Studio_XPS_13&oldid=399593](https://wiki.archlinux.org/index.php?title=Dell_Studio_XPS_13&oldid=399593)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Dell](/index.php/Category:Dell "Category:Dell")