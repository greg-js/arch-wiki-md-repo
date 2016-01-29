# MacBook5,2 (early-mid 2009)

Installing Archlinux on the Macbook5,2 (Polycarbonate, Mid-2009) has several pitfalls as of right now. I have written them into this article for people having trouble installing Archlinux on their 5,2 Macbook. This guide assumes you are also going to follow the [MacBook](/index.php/MacBook "MacBook") install guide, and will point out a few modifications to get it working on this Macbook. Review these suggestions and then follow the guide. This guide also assumes you have rEFIt installed before hand.

## Contents

*   [1 Installation](#Installation)
*   [2 Installing Grub 2](#Installing_Grub_2)
*   [3 Touchpad](#Touchpad)
*   [4 Audio](#Audio)
*   [5 Further Reference](#Further_Reference)

## Installation

I suggest formatting your Arch Linux Partition using a [GParted](http://gparted.sourceforge.net/livecd.php) live disc, which works just fine. You will more than likely format `/dev/sda3` to ext3\. You can also use parted from the install disc if you like. However, no matter which option you choose, after formatting, you MUST reboot your Macbook and use rEFIt to resync the partition tables.

The Macbook5,2 seems to have trouble in general with Grub (but not grub2). Unless you use the ISOLINUX install disc, you probably will not make it past the grub boot selection screen. Assuming you are using the ISOLINUX disc, boot with:

```
# arch maxcpus=1

```

Without this, when the installer attempts to initialize the second CPU in your laptop the screen will go blank and you will be unable to proceed. This is a well known issue with the Macbook5,2\. You can also boot the system with acpi=off. You will always need one of these options to boot, even after install.

```
# arch acpi=off

```

Install proceeds normally, except for during hard drive preparation. Manually select block devices, select `/dev/sda3` and the filesystem you selected. If you used the Gparted live disc, say that you do not need to create the partition. Ignore warnings about swap drive, That will be handled later. Install should go okay. Do NOT install Grub, it will not work. The next section describes how to use grub2 as your Boot Loader for the Macbook.

## Installing Grub 2

Some of this information is pulled from the [Grub2](/index.php/Grub2 "Grub2") article. As an aside, some triple boot guides suggest using LILO, but I could not get LILO to work.

*   Ensure the network is properly configured.
*   From the installer's live shell, chroot to the installed system:

```
# mount -o bind /dev /mnt/dev
# chroot /mnt bash

```

*   Install the GRUB2 package:

```
# pacman -S grub2

```

*   Install GRUB2 to the Archlinux partition (Do not install to /dev/sda!)

```
# grub-install --recheck /dev/sda3

```

GRUB2 will probably inform you that this is not a suggested action. However, it is what must be done to boot the system. Use the following to force GRUB2 to install to `/dev/sda3`

```
# grub-install --recheck --force /dev/sda3

```

I found that GRUB2's grub-mkconfig function does not work on the MacBook. I suggest reading the [Grub2](/index.php/Grub2 "Grub2") article for more advanced tips, but for convenience, here is my `/boot/grub/grub.cfg`:

```
/boot/grub/grub.cfg

```

```

set timeout=5
set default=0

menuentry "Arch Linux" {
set root=(hd0,3)
linux /boot/vmlinuz-linux root=/dev/sda3 ro maxcpus=1 reboot=pci irqpoll noapic
initrd /boot/initramfs-linux.img
}

```

If everything went alright, you should be looking at the command prompt.

## Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics"). Especially the "Advanced Policy Configuration" section. Increase the sensitivity, acceleration, min_speed, and max_speed greatly

## Audio

I found that to get Audio to work, you should use

```
# options snd_hda_intel model=mb5

```

In `/etc/modprobe.d/modprobe.conf`. This seems to work consistently across all MacBook5,2s

## Further Reference

[Ubuntu Guide For MacBook5,2](https://help.ubuntu.com/community/MacBook5-2/Karmic)

Retrieved from "[https://wiki.archlinux.org/index.php?title=MacBook5,2_(early-mid_2009)&oldid=376907](https://wiki.archlinux.org/index.php?title=MacBook5,2_(early-mid_2009)&oldid=376907)"