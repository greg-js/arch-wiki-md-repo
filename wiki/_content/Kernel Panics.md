# Kernel Panics

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Last **major** update to this page was November 2009\. (Discuss in [Talk:Kernel Panics#](https://wiki.archlinux.org/index.php/Talk:Kernel_Panics))

This page describes how to repair a computer whose kernel panics at boot. This has to do with the very basic OS kernel and the first part of the boot routine. (For issues regarding graphical interface problems or program freeze-ups, etc., save yourself some wasted effort and time, and please look elsewhere.)

## Contents

*   [1 Definition](#Definition)
*   [2 What to do](#What_to_do)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 Option 1: Check bootloader configuration](#Option_1:_Check_bootloader_configuration)
*   [5 Option 2: Reinstall kernel](#Option_2:_Reinstall_kernel)
    *   [5.1 Start from the installation CD](#Start_from_the_installation_CD)
    *   [5.2 Mount your partitions](#Mount_your_partitions)
    *   [5.3 Gather your files for later troubleshooting](#Gather_your_files_for_later_troubleshooting)
    *   [5.4 Chroot to your normal root](#Chroot_to_your_normal_root)
    *   [5.5 Roll back to previous kernel version](#Roll_back_to_previous_kernel_version)
*   [6 Reboot](#Reboot)

## Definition

A decent definition of Kernel Panic comes to us from Wikipedia, which states in part; "A kernel panic is an action taken by an operating system upon detecting an internal fatal error from which it cannot safely recover; the term is largely specific to Unix and Unix-like systems. The equivalent in Microsoft Windows operating systems is the Blue Screen of Death."

See also [Wikipedia:Kernel panic](https://en.wikipedia.org/wiki/Kernel_panic "wikipedia:Kernel panic").

## What to do

Basically, the problem is that the operating system doesn't start correctly. Various behavior may be expressed, such as that one may get the computer to freeze, or the operating system may give an error message of some sort or one may not go to the place they were expecting (Command prompt, Desktop or whathaveyou). This will require some basic troubleshooting from the command line, if you can boot to it, or from a boot disk if it will get you a command prompt or your favorite interface.

## Troubleshooting

To make troubleshooting easier, ensure that the kernel is not in quiet mode. Remove 'quiet' from the kernel line in GRUB, if it is found there. Upon boot, check the output immediately before the panic, and decide whether there is any useful information. There are probably too many causes for a kernel panic to keep well-documented in this wiki. Make sure that your system's configuration in /boot is correct, and that none of the computer's hardware is faulty - it is good idea to run memtest from the Arch install/rescue CD or another utility (red entries are bad). If you believe the configuration in /boot may be erroneous, try Option 1 to repair your bootloader setup. If you believe the kernel panic is the fault of the kernel itself, follow Option 2 in order to reinstall the existing version or an earlier kernel.

## Option 1: Check bootloader configuration

Another possibility is an error in the [bootloader's configuration](/index.php/Boot_Loader#Configuration_files "Boot Loader"). For example, repartitioning hard drives can change partitions' order. GRUB users may recall whether repartitioning has occurred recently and make sure the _root_ and _kernel_ lines match up with the new partitioning scheme. And examine the file for typos and extraneous characters. An extra space, or a character in the wrong place will cause a kernel panic.

## Option 2: Reinstall kernel

Reinstalling the kernel is probably the best bet when no other major system modifications have taken place recently.

### Start from the installation CD

The first step is booting the installation CD. Once booted, you are presented with an automatically logged-in virtual console as the _root_ user.

### Mount your partitions

When booted, you are in a minimal but functional live GNU/Linux environment with some basic tools. Now, you have to mount your normal root disk (or partition) to `/mnt`.

```
# mount /dev/sdXY /mnt

```

If you are using legacy IDE drives, then use the command:

```
# mount /dev/hdXY /mnt

```

If you use a separate boot partition, do not forget to mount it with:

```
# mount /dev/sdXZ /mnt/boot

```

### Gather your files for later troubleshooting

This is a good point to stop and gather your information onto another drive or partition so that it can be analyzed and/or emailed for outside viewing before the files change again. Simply create a separate directory on your main partition or mount a USB drive to contain the files. Then you may copy any files you will need to keep unchanged during the next boot with your new kernel.

### Chroot to your normal root

Now, you will have to chroot to the partition mounted in `/mnt`. Newer kernels use an initial ramdisk to set up the kernel environment: when you reinstall a kernel, that initial ramdisk will be regenerated with [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"). One of mkinitcpio's features is that it does automatic detection to find out what kernel modules are required for starting up your computer. For this autodetection to work, `/dev`, `/sys`, and `/proc` need to mounted in your chroot; make sure to read [Change root](/index.php/Change_root "Change root").

To chroot to your normal root mounted at `/mnt`, run this command:

```
# arch-chroot /mnt /bin/bash

```

If you do not want to use the [Bash](/index.php/Bash "Bash") shell, remove `/bin/bash` from the `arch-chroot` command.

**Note:** You need the [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) package in order to use `arch-chroot`.

### Roll back to previous kernel version

If you keep your downloaded pacman packages, you now can easily roll back. If you did not keep them, you have to [find a way](/index.php/Downgrading_packages#Finding_your_older_version "Downgrading packages") to get a previous kernel version on your system now.

Let us suppose you kept the previous versions. We will now install the last working one.

First, you need to get the kernel details:

```
# find /var/cache/pacman/pkg -name 'linux-3*'

```

Now, use the kernel details in the command below.

```
# pacman -U /var/cache/pacman/pkg/linux-3._xx-x_.pkg.tar.xz

```

(Of course, make sure that you adapt this line to your own kernel version. You can find the ones you still have in your cache by examining the directory above.)

## Reboot

**Note:** If you choose to do anything else before you reboot, remember that you are still in the chroot environment and will likely have to exit and login again.

Now is the time to reboot and see if the system modifications have stopped the panic. If reverting to an older kernel works, do not forget to [check the arch-newspage](https://www.archlinux.org/news/) to check what went wrong with the kernel build. If there is no mention of the problem there, then go to the bug reporting area and search for it there. If you still do not find it, open a new bug report and attach those files you saved during the troubleshooting step above.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Kernel_Panics&oldid=376853](https://wiki.archlinux.org/index.php?title=Kernel_Panics&oldid=376853)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [System recovery](/index.php/Category:System_recovery "Category:System recovery")
*   [Kernel](/index.php/Category:Kernel "Category:Kernel")

Hidden category:

*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")