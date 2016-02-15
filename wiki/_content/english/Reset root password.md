This guide will show you how to reset a forgotten root password. Several methods are listed to help you accomplish this.

**Warning:** An attacker could use the methods mentioned below to break into your system. No matter how secure the operating system is or how good passwords are, having physical access amounts to loading an alternate OS and exposing your data, unless you use [disk encryption](/index.php/Disk_encryption "Disk encryption").

## Contents

*   [1 Using a LiveCD](#Using_a_LiveCD)
    *   [1.1 Change root](#Change_root)
*   [2 Using GRUB to invoke bash](#Using_GRUB_to_invoke_bash)
*   [3 See also](#See_also)

## Using a LiveCD

With a LiveCD a couple methods are available: change root and use the `passwd` command, or erase the password field entry directly editing the password file. Any Linux capable LiveCD can be used, albeit to change root it must match your installed architecture type. Here we only describe how to reset your password with chroot, since manual editing the password file is significantly more risky.

### Change root

1.  Boot the LiveCD and [mount](/index.php/Mount "Mount") the root partition of your main system.
2.  Enter the [chroot](/index.php/Chroot "Chroot") session.
3.  Use the `passwd` command to set the new password (you won't be prompted for an old one).
4.  Exit chroot session.
5.  Unmount the root partition.
6.  Reboot, and enter your new password. If you can't remember it, go to step 1.

## Using GRUB to invoke bash

1.  Select the appropriate boot entry in the GRUB menu and press `e` to edit the line.
2.  Select the kernel line and press `e` again to edit it.
3.  Append `init=/bin/bash` at the end of line.
4.  Press `b` to boot (this change is only temporary and will not be saved to your menu.lst). After booting you will be at the bash prompt.
5.  Your root file system is mounted as readonly now, so remount it as read/write `mount -n -o remount,rw /`.
6.  Use the `passwd` command to create a new root password.
7.  Reboot and do not lose your password again!

**Note:** Some keyboards may not be loaded properly by the init system with this method and you will not be able to type anything at the bash prompt. If this is the case, you will have to use another method.

## See also

*   [this guide](http://www.howtoforge.com/how-to-reset-a-forgotten-root-password-with-knoppix-p2) for an example.