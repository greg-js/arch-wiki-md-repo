Related articles

*   [Improving performance](/index.php/Improving_performance "Improving performance")
*   [Silent boot](/index.php/Silent_boot "Silent boot")
*   [Daemon](/index.php/Daemon "Daemon")
*   [e4rat](/index.php/E4rat "E4rat")
*   [Kexec](/index.php/Kexec "Kexec")

Improving the boot performance of a system can provide reduced boot wait times and a means to learn more about how certain system files and scripts interact with one another. This article attempts to aggregate methods on how to improve the boot performance of an Arch Linux system.

## Contents

*   [1 Analyzing the boot process](#Analyzing_the_boot_process)
    *   [1.1 Using systemd-analyze](#Using_systemd-analyze)
    *   [1.2 Using systemd-bootchart](#Using_systemd-bootchart)
    *   [1.3 Using bootchart2](#Using_bootchart2)
*   [2 Compiling a custom kernel](#Compiling_a_custom_kernel)
*   [3 Initramfs](#Initramfs)
*   [4 Early start for services](#Early_start_for_services)
*   [5 Staggered spin-up](#Staggered_spin-up)
*   [6 Filesystem mounts](#Filesystem_mounts)
*   [7 Less output during boot](#Less_output_during_boot)
*   [8 Suspend to RAM](#Suspend_to_RAM)

## Analyzing the boot process

### Using systemd-analyze

[systemd](/index.php/Systemd "Systemd") provides a tool called `systemd-analyze` that can be used to show timing details about the boot process, including an svg plot showing units waiting for their dependencies. You can see which unit files are causing your boot process to slow down. You can then optimize your system accordingly.

To see how much time was spent in kernelspace and userspace on boot, simply use:

```
$ systemd-analyze

```

**Tip:** If you boot via [UEFI](/index.php/UEFI "UEFI") and use a boot loader which implements systemd's [Boot Loader Interface](http://www.freedesktop.org/wiki/Software/systemd/BootLoaderInterface) (which currently [systemd-boot](/index.php/Systemd-boot "Systemd-boot") and [GRUB](/index.php/GRUB "GRUB") do), *systemd-analyze* can additionally show you how much time was spent in the EFI firmware and the boot loader itself.

To list the started unit files, sorted by the time each of them took to start up:

```
$ systemd-analyze blame

```

At some points of the boot process, things can not proceed until a given unit succeeds. To see which units find themselves at these critical points in the startup chain, do:

```
$ systemd-analyze critical-chain

```

You can also create an SVG file which describes your boot process graphically, similiar to [Bootchart](/index.php/Bootchart "Bootchart"):

```
$ systemd-analyze plot > plot.svg

```

See [systemd-analyze(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-analyze.1) for details.

### Using systemd-bootchart

Bootchart has been merged into **systemd** since Oct. 2012, and you can use it to boot just as you would with the original bootchart. Add this to your kernel line:

```
initcall_debug printk.time=y init=/usr/lib/systemd/systemd-bootchart

```

After collecting a certain amount of data (configurable) the logging stops and a graph is generated from the logged information. This graph contains vital clues as to which resources are being used (by default I/O, CPU utilization and kernel init threads), in which order, and where possible problems exist in the startup sequence of the system. It is essentially a more detailed version of the systemd-analyze plot function.

Bootchart graphs are by default written time-stamped in /run/log and saved to the journal with MESSAGE_ID=9f26aa562cf440c2b16c773d0479b518\. Journal field BOOTCHART= contains the bootchart in SVG format.

See the [manpage](http://www.freedesktop.org/software/systemd/man/systemd-bootchart.html) for more information.

### Using bootchart2

You could also use a version of bootchart to visualize the boot sequence. Since you are not able to put a second init into the kernel command line you won't be able to use any of the standard bootchart setups. However the [bootchart2-git](https://aur.archlinux.org/packages/bootchart2-git/) package from [AUR](/index.php/AUR "AUR") comes with an undocumented **systemd** service. After you've installed bootchart2 do:

```
# systemctl enable bootchart2

```

You can visualize the results by opening */var/log/bootchart.png*, or if you would like more features by launching

```
$ pybootchartgui -i

```

Read the [bootchart2 documentation](https://github.com/mmeeks/bootchart) for further details on using this version of bootchart.

## Compiling a custom kernel

Compiling a custom kernel can reduce boot time and memory usage. Though with the standardization of the 64 bit architecture and the modular nature of the Linux kernel, these benefits may not be as great as expected. [Read more about compiling a kernel](/index.php/Kernel_Compilation "Kernel Compilation").

## Initramfs

In a similar approach to [#Compiling a custom kernel](#Compiling_a_custom_kernel), the initramfs can be slimmed down. A simple way is to include the [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") `autodetect` hook. If you want to go further than that, see [Minimal initramfs](/index.php/Minimal_initramfs "Minimal initramfs").

## Early start for services

One central feature of systemd is [D-Bus](/index.php/D-Bus "D-Bus") and socket activation. This causes services to be started when they are first accessed and is generally a good thing. However, if you know that a service (like [UPower](/index.php/UPower "UPower")) will always be started during boot, then the overall boot time might be reduced by starting it as early as possible. This can be achieved (if the service file is set up for it, which in most cases it is) by issuing:

```
# systemctl enable upower

```

This will cause systemd to start UPower as soon as possible, without causing races with the socket or D-Bus activation.

## Staggered spin-up

Some hardware implements [staggered spin-up](https://en.wikipedia.org/wiki/Spin-up#Staggered_spin-up "wikipedia:Spin-up"), which causes the OS to probe ATA interfaces serially, which can spin up the drives one-by-one and reduce the peak power usage. This slows down the boot speed, and on most consumer hardware provides no benefits at all since the drives will already spin-up immediately when the power is turned on. To check if SSS is being used:

```
$ dmesg | grep SSS

```

If it wasn't used during boot, there will be no output.

To disable it, add `libahci.ignore_sss=1` to the [kernel line](/index.php/Kernel_line "Kernel line").

## Filesystem mounts

Thanks to [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")'s `fsck` hook, you can avoid a possibly costly remount of the root partition by changing `ro` to `rw` on the kernel line and removing it from `/etc/fstab`. Options can be set with `rootflags=mount options...` on the kernel line. Remember to remove the entry from your `/etc/fstab` file, else the `systemd-remount-fs.service` will continue to try to apply those settings. Alternatively, one could try to mask that unit.

If btrfs is in use for the root filesystem, there is no need for a fsck on every boot like other filesystems. If this is the case, [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")'s `fsck` hook can be removed. You may also want to mask the `systemd-fsck-root.service`, or tell it not to fsck the root filesystem from the kernel command line using `fsck.mode=skip`. Without [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")'s `fsck` hook, systemd will still fsck any relevant filesystems with the `systemd-fsck@.service`

You can also remove API filesystems from `/etc/fstab`, as systemd will mount them itself (see `pacman -Ql systemd | grep '\.mount$'` for a list). It is not uncommon for users to have a /tmp entry carried over from sysvinit, but you may have noticed from the command above that systemd already takes care of this. Ergo, it may be safely removed.

Other filesystems like `/home` can be mounted with custom mount units. Adding `noauto,x-systemd.automount` to mount options will buffer all access to that partition, and will fsck and mount it on first access, reducing the number of filesystems it must fsck/mount during the boot process.

**Note:**

*   This will make your `/home` filesystem type `autofs`, which is ignored by [mlocate](/index.php/Mlocate "Mlocate") by default. The speedup of automounting `/home` may not be more than a second or two, depending on your system, so this trick may not be worth it.
*   If the system is installed into a [Btrfs](/index.php/Btrfs "Btrfs") subvolume (specifically: the root directory `/` itself is a subvolume) and `/home` is a separate file system, you may also want to prevent the creation of a `/home` subvolume. Mask the `home.conf` tmpfile: `ln -s /dev/null /etc/tmpfiles.d/home.conf`.

## Less output during boot

For some systems, particularly those with an SSD, the slow performance of the TTY is actually a bottleneck, and so less output means faster booting. See the [Silent boot](/index.php/Silent_boot "Silent boot") article for suggestions.

## Suspend to RAM

The best way to reduce boot time is not booting at all. Consider [suspending your system to RAM](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate") instead.