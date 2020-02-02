Related articles

*   [Uswsusp](/index.php/Uswsusp "Uswsusp")
*   [systemd](/index.php/Systemd "Systemd")
*   [Power management](/index.php/Power_management "Power management")

Currently there are three methods of suspending available: **suspend to RAM** (usually called just **suspend**), **suspend to disk** (usually known as **hibernate**), and **hybrid suspend** (sometimes aptly called **suspend to both**):

*   **Suspend to RAM** method cuts power to most parts of the machine aside from the RAM, which is required to restore the machine's state. Because of the large power savings, it is advisable for laptops to automatically enter this mode when the computer is running on batteries and the lid is closed (or the user is inactive for some time).

*   **Suspend to disk** method saves the machine's state into [swap space](/index.php/Swap_space "Swap space") and completely powers off the machine. When the machine is powered on, the state is restored. Until then, there is [zero](https://en.wikipedia.org/wiki/Standby_power "wikipedia:Standby power") power consumption.

*   **Suspend to both** method saves the machine's state into swap space, but does not power off the machine. Instead, it invokes usual suspend to RAM. Therefore, if the battery is not depleted, the system can resume from RAM. If the battery is depleted, the system can be resumed from disk, which is much slower than resuming from RAM, but the machine's state has not been lost.

There are multiple low level interfaces (backends) providing basic functionality, and some high level interfaces providing tweaks to handle problematic hardware drivers/kernel modules (e.g. video card re-initialization).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Low level interfaces](#Low_level_interfaces)
    *   [1.1 kernel (swsusp)](#kernel_(swsusp))
    *   [1.2 uswsusp](#uswsusp)
*   [2 High level interfaces](#High_level_interfaces)
    *   [2.1 systemd](#systemd)
*   [3 Hibernation](#Hibernation)
    *   [3.1 About swap partition/file size](#About_swap_partition/file_size)
    *   [3.2 Required kernel parameters](#Required_kernel_parameters)
        *   [3.2.1 Hibernation into swap file](#Hibernation_into_swap_file)
        *   [3.2.2 Hibernation into swap file on Btrfs](#Hibernation_into_swap_file_on_Btrfs)
    *   [3.3 Configure the initramfs](#Configure_the_initramfs)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 ACPI_OS_NAME](#ACPI_OS_NAME)
    *   [4.2 Suspend/hibernate does not work, or does not work consistently](#Suspend/hibernate_does_not_work,_or_does_not_work_consistently)
    *   [4.3 Wake-on-LAN](#Wake-on-LAN)
    *   [4.4 Instantaneous wakeups from suspend](#Instantaneous_wakeups_from_suspend)
    *   [4.5 System does not power off when hibernating](#System_does_not_power_off_when_hibernating)

## Low level interfaces

Though these interfaces can be used directly, it is advisable to use some of [high level interfaces](#High_level_interfaces) to suspend/hibernate. Using low level interfaces directly is significantly faster than using any high level interface, since running all the pre- and post-suspend hooks takes time, but hooks can properly set hardware clock, restore wireless etc.

### kernel (swsusp)

The most straightforward approach is to directly inform the in-kernel software suspend code (swsusp) to enter a suspended state; the exact method and state depends on the level of hardware support. On modern kernels, writing appropriate strings to `/sys/power/state` is the primary mechanism to trigger this suspend.

See [kernel documentation](https://www.kernel.org/doc/Documentation/power/states.txt) for details.

### uswsusp

The uswsusp ('Userspace Software Suspend') is a wrapper around the kernel's suspend-to-RAM mechanism, which performs some graphics adapter manipulations from userspace before suspending and after resuming.

See main article [Uswsusp](/index.php/Uswsusp "Uswsusp").

## High level interfaces

The end goal of these packages is to provide binaries/scripts that can be invoked to perform suspend/hibernate. Actually hooking them up to power buttons or menu clicks or laptop lid events is usually left to other tools. To automatically suspend/hibernate on certain power events, such as laptop lid close or battery depletion percentage, you may want to look into running [Acpid](/index.php/Acpid "Acpid").

### systemd

[systemd](/index.php/Systemd "Systemd") provides native commands for suspend, hibernate and a hybrid suspend, see [Power management#Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management") for details. This is the default interface used in Arch Linux.

See [Power management#Sleep hooks](/index.php/Power_management#Sleep_hooks "Power management") for additional information on configuring suspend/hibernate hooks. Also see [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1), [systemd-sleep(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-sleep.8), and [systemd.special(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.special.7).

## Hibernation

In order to use hibernation, you need to create a [swap](/index.php/Swap "Swap") partition or file. You will need to point the kernel to your swap using the `resume=` kernel parameter, which is configured via the boot loader. You will also need to [configure the initramfs](#Configure_the_initramfs). This tells the kernel to attempt resuming from the specified swap in early userspace. These three steps are described in detail below.

**Note:**

*   See [Dm-crypt/Swap encryption#With suspend-to-disk support](/index.php/Dm-crypt/Swap_encryption#With_suspend-to-disk_support "Dm-crypt/Swap encryption") when using [encryption](/index.php/Encryption "Encryption").
*   [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened) does not support hibernation, see [FS#63648](https://bugs.archlinux.org/task/63648).

### About swap partition/file size

Even if your swap partition is smaller than RAM, you still have a big chance of hibernating successfully. According to [kernel documentation](https://www.kernel.org/doc/Documentation/power/interface.txt):

	*`/sys/power/image_size` controls the size of the image created by the suspend-to-disk mechanism. It can be written a string representing a non-negative integer that will be used as an upper limit of the image size, in bytes. The suspend-to-disk mechanism will do its best to ensure the image size will not exceed that number. However, if this turns out to be impossible, it will try to suspend anyway using the smallest image possible. In particular, if "0" is written to this file, the suspend image will be as small as possible. Reading from this file will display the current image size limit, which is set to 2/5 of available RAM by default.*

You may either decrease the value of `/sys/power/image_size` to make the suspend image as small as possible (for small swap partitions), or increase it to possibly speed up the hibernation process. See [Systemd#Temporary files](/index.php/Systemd#Temporary_files "Systemd") to make this change persistent.

The suspend image cannot span multiple swap partitions and/or swap files. It must fully fit in one swap partition or one swap file.[[1]](https://www.kernel.org/doc/Documentation/power/swsusp.txt)

### Required kernel parameters

The [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `resume=*swap_device*` must be used. Any of the [persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") methods can be used as `*swap_device*`. For example:

*   `resume=UUID=4209c845-f495-4c43-8a03-5363dd433153`
*   `resume="PARTLABEL=Swap partition"`
*   `resume=/dev/archVolumeGroup/archLogicalVolume` -- if swap is on a [LVM](/index.php/LVM "LVM") logical volume

Generally, it is preferred to use the same naming method for both the `resume` and `root` parameters.

#### Hibernation into swap file

**Warning:** [Btrfs](/index.php/Btrfs#Swap_file "Btrfs") on Linux kernel before version 5.0 does not support swap files. Failure to heed this warning may result in file system corruption. While a swap file may be used on Btrfs when mounted through a loop device, this will result in severely degraded swap performance.

Using a swap file instead of a swap partition requires an additional kernel parameter `resume_offset=*swap_file_offset*`.

**Note:** The `resume` parameter must point to the [block device](/index.php/Block_device "Block device") where the swap file resides. For a stacked block device such as an encrypted container, RAID or LVM, it means that `resume` must point to the unlocked/mapped device that contains the file system with the swap file.

The value of `*swap_file_offset*` can be obtained by running `filefrag -v *swap_file*`, the output is in a table format and the required value is located in the first row of the `physical_offset` column. For example:

 `# filefrag -v /swapfile` 
```
Filesystem type is: ef53
File size of /swapfile is 4294967296 (1048576 blocks of 4096 bytes)
 ext:     logical_offset:        physical_offset: length:   expected: flags:
   0:        0..       0:      **38912**..     38912:      1:            
   1:        1..   22527:      38913..     61439:  22527:             unwritten
   2:    22528..   53247:     899072..    929791:  30720:      61440: unwritten
...

```

In the example the value of `*swap_file_offset*` is the first `38912` with the two periods.

**Tip:**

*   The following command may be used to identify `*swap_device*`: `findmnt -no SOURCE -T /swapfile`
*   The following command may be used to identify `*swap_file_offset*`: `filefrag -v /swapfile | awk '{ if($1=="0:"){print $4} }'`
*   The value of `*swap_file_offset*` can also be obtained by running `swap-offset *swap_file*`. The *swap-offset* binary is provided within the set of tools [uswsusp](/index.php/Uswsusp "Uswsusp"). If using this method, then these two parameters have to be provided in `/etc/suspend.conf` via the keys `resume device` and `resume offset`. No reboot is required in this case.

**Note:** The kernel parameters will only take effect after rebooting. To be able to hibernate right away, obtain the volume's major and minor device numbers from [lsblk](/index.php/Lsblk "Lsblk") and echo them in format `*major*:*minor*` to `/sys/power/resume` and the resume offset to `/sys/power/resume_offset`. For example, if the swap file is on volume `8:2` and has the offset `38912`:
```
# echo 8:2 > /sys/power/resume
# echo 38912 > /sys/power/resume_offset

```
See [https://www.kernel.org/doc/Documentation/power/swsusp.txt](https://www.kernel.org/doc/Documentation/power/swsusp.txt).

**Tip:** You might want to decrease the [swappiness](/index.php/Swappiness "Swappiness") for your swapfile if the only purpose is to be able to hibernate and not expand RAM.

#### Hibernation into swap file on Btrfs

**Note:** Since systemd 244, `systemctl hibernate` does not work with a swap file on Btrfs. The [systemd issue 14249](https://github.com/systemd/systemd/issues/14249) was fixed on 2020-01-08, but there is not any release since then.

Hibernation onto a swapfile is supported by recent versions of systemd [[2]](https://github.com/systemd/systemd/issues/9559).

The resume_offset number can be computed using the [tool btrfs_map_physical.c](https://github.com/osandov/osandov-linux/blob/master/scripts/btrfs_map_physical.c). Do not try to use the filefrag tool, on [Btrfs](/index.php/Btrfs "Btrfs") the "physical" offset you get from filefrag is not the real physical offset on disk; there is a virtual disk address space in order to support multiple devices. [[3]](https://bugzilla.kernel.org/show_bug.cgi?id=202803)

Download or copy the [tool btrfs_map_physical.c](https://github.com/osandov/osandov-linux/blob/master/scripts/btrfs_map_physical.c) into a file named `btrfs_map_physical.c`, then compile it,

```
$ gcc -O2 -o btrfs_map_physical btrfs_map_physical.c

```

and run it. An example output is shown below.

 `# ./btrfs_map_physical */path/to/swapfile*` 
```
FILE OFFSET  EXTENT TYPE  LOGICAL SIZE  LOGICAL OFFSET  PHYSICAL SIZE  DEVID  PHYSICAL OFFSET
0            regular      4096          2927632384      268435456      1      **4009762816**
4096         prealloc     268431360     2927636480      268431360      1      4009766912
268435456    prealloc     268435456     3251634176      268435456      1      4333764608
536870912    prealloc     268435456     3520069632      268435456      1      4602200064
805306368    prealloc     268435456     3788505088      268435456      1      4870635520
1073741824   prealloc     268435456     4056940544      268435456      1      5139070976
1342177280   prealloc     268435456     4325376000      268435456      1      5407506432
1610612736   prealloc     268435456     4593811456      268435456      1      5675941888

```

Note the the first physical offset returned by this tool. In this example, we use `4009762816`. Also note the pagesize that can be found with `getconf PAGESIZE`.

To compute the `resume_offset` value, divide the physical offset by the pagesize. In this example, it is `4009762816 / 4096 = 978946`.

### Configure the initramfs

*   When an [initramfs](/index.php/Initramfs "Initramfs") with the `base` hook is used, which is the default, the `resume` hook is required in `/etc/mkinitcpio.conf`. Whether by label or by UUID, the swap partition is referred to with a udev device node, so the `resume` hook must go *after* the `udev` hook. This example was made starting from the default hook configuration:

	 `HOOKS=(base udev autodetect keyboard modconf block filesystems **resume** fsck)` 

	Remember to [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") for these changes to take effect.

**Note:** [LVM](/index.php/LVM "LVM") users should add the `resume` hook after `lvm2`.

*   When an initramfs with the `systemd` hook is used, a resume mechanism is already provided, and no further hooks need to be added.

## Troubleshooting

### ACPI_OS_NAME

You might want to tweak your **DSDT table** to make it work. See [DSDT](/index.php/DSDT "DSDT") article

### Suspend/hibernate does not work, or does not work consistently

There have been many reports about the screen going black without easily viewable errors or the ability to do anything when going into and coming back from suspend and/or hibernate. These problems have been seen on both laptops and desktops. This is not an official solution, but switching to an older kernel, especially the LTS-kernel, will probably fix this.

Also problem may arise when using hardware watchdog timer (disabled by default, see `RuntimeWatchdogSec=` in [systemd-system.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-system.conf.5#OPTIONS)). Bugged watchdog timer may reset the computer before the system finished creating the hibernation image.

Sometimes the screen goes black due to device initialization from within the initramfs. Removing any modules you might have in [Mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") and rebuilding the initramfs, can possibly solve this issue, specially graphics drivers for [early KMS](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting"). Initializing such devices before resuming can cause inconsistencies that prevents the system resuming from hibernation. This does not affect resuming from RAM. Also, check the blog article [best practices to debug suspend issues](https://01.org/blogs/rzhang/2015/best-practice-debug-linux-suspend/hibernate-issues).

Moving from the [radeon](/index.php/Radeon "Radeon") video driver to the newer [AMDGPU](/index.php/AMDGPU "AMDGPU") driver could also help to make the hibernation and awakening process successful.

For Intel graphics drivers, enabling early KMS may help to solve the blank screen issue. Refer to [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") for details.

After upgrading to kernel 4.15.3, resume may fail with a static (non-blinking) cursor on a black screen. [Blacklisting](/index.php/Blacklisting "Blacklisting") the module `nvidiafb` might help. [[4]](https://bbs.archlinux.org/viewtopic.php?id=234646)

### Wake-on-LAN

If [Wake-on-LAN](/index.php/Wake-on-LAN "Wake-on-LAN") is active, the network interface card will consume power even if the computer is hibernated.

### Instantaneous wakeups from suspend

For some Intel Haswell systems with the LynxPoint and LynxPoint-LP chipset, instantaneous wakeups after suspend are reported. They are linked to erroneous BIOS ACPI implementations and how the `xhci_hcd` module interprets it during boot. As a work-around reported affected systems are added to a blacklist (named `XHCI_SPURIOUS_WAKEUP`) by the kernel case-by-case.[[5]](https://bugzilla.kernel.org/show_bug.cgi?id=66171#c6)

Instantaneous resume may happen, for example, if a USB device is plugged during suspend and ACPI wakeup triggers are enabled. A viable work-around for such a system, if it is not on the blacklist yet, is to disable the wakeup triggers. An example to disable wakeup through USB is described as follows.[[6]](https://bbs.archlinux.org/viewtopic.php?pid=1575617)

To view the current configuration:

 `$ cat /proc/acpi/wakeup` 
```
Device  S-state   Status   Sysfs node
...
EHC1      S3    *enabled  pci:0000:00:1d.0
EHC2      S3    *enabled  pci:0000:00:1a.0
XHC       S3    *enabled  pci:0000:00:14.0
...

```

The relevant devices are `EHC1`, `EHC2` and `XHC` (for USB 3.0). To toggle their state you have to echo the device name to the file as root.

```
# echo EHC1 > /proc/acpi/wakeup
# echo EHC2 > /proc/acpi/wakeup
# echo XHC > /proc/acpi/wakeup

```

This should result in suspension working again. However, this settings are only temporary and would have to be set at every reboot. To automate this take a look at [systemd#Writing unit files](/index.php/Systemd#Writing_unit_files "Systemd"). See [BBS thread](https://bbs.archlinux.org/viewtopic.php?pid=1575617#p1575617) for a possible solution and more information.

If you use `nouveau` driver, the reason of instantaneous wakeup may be a bug in that driver, which sometimes prevents graphics card from suspension. One possible workaround is unloading `nouveau` kernel module right before going to sleep and loading it back after wakeup. To do this, create the following script:

 `/usr/lib/systemd/system-sleep/10-nouveau.sh` 
```
#!/bin/bash

case $1/$2 in
  pre/*)
    # echo "Going to $2..."
    /usr/bin/echo "0" > /sys/class/vtconsole/vtcon1/bind
    /usr/bin/rmmod nouveau
    ;;
  post/*)
    # echo "Waking up from $2..."
    /usr/bin/modprobe nouveau
    /usr/bin/echo "1" > /sys/class/vtconsole/vtcon1/bind
    ;;
esac
```

The first echo line unbinds nouveaufb from the framebuffer console driver (fbcon). Usually it is `vtcon1` as in this example, but it may also be another `vtcon*`. See `/sys/class/vtconsole/vtcon*/name` which one of them is a "frame buffer device" [[7]](https://nouveau.freedesktop.org/wiki/KernelModeSetting/).

### System does not power off when hibernating

When you hibernate your system, the system should power off (after saving the state on the disk). Sometimes, you might see the power LED is still glowing. If that happens, it might be instructive to set the `HibernateMode` to `shutdown` in [sleep.conf.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sleep.conf.d.5):

 `/etc/systemd/sleep.conf.d/hibernatemode.conf` 
```
[Sleep]
HibernateMode=shutdown
```

With the above configuration, if every thing else is setup correctly, on invocation of a `systemctl hibernate` the machine will shutdown saving state to disk as it does so.