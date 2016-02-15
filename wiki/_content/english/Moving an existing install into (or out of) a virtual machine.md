This article describes how to transfer your current Arch Linux installation in or out of a virtual environment (i.e. QEMU, VirtualBox, VMware), and is heavily based on the [Full system backup with rsync](/index.php/Full_system_backup_with_rsync "Full system backup with rsync") article. A virtual machine ("VM", for short) uses different hardware, which needs to be addressed by re-generating the initramfs image and possibly adjusting the fstab – especially if it is an [SSD](/index.php/SSD "SSD").

## Contents

*   [1 Moving out of a VM](#Moving_out_of_a_VM)
    *   [1.1 Set up a shared folder](#Set_up_a_shared_folder)
    *   [1.2 Transfer the system](#Transfer_the_system)
    *   [1.3 Chroot and reinstall the bootloader](#Chroot_and_reinstall_the_bootloader)
    *   [1.4 Adjust the fstab](#Adjust_the_fstab)
    *   [1.5 Re-generate the initramfs image](#Re-generate_the_initramfs_image)
*   [2 Moving into a VM](#Moving_into_a_VM)
    *   [2.1 Create the container](#Create_the_container)
    *   [2.2 Transfer the system](#Transfer_the_system_2)
    *   [2.3 Convert the container to a compatible format](#Convert_the_container_to_a_compatible_format)
    *   [2.4 Chroot and reinstall the bootloader](#Chroot_and_reinstall_the_bootloader_2)
    *   [2.5 Adjust the fstab](#Adjust_the_fstab_2)
    *   [2.6 Disable any Xorg-related files](#Disable_any_Xorg-related_files)
    *   [2.7 Re-generate the initramfs image](#Re-generate_the_initramfs_image_2)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 "mount: special device /dev/loop5p1 does not exist"](#.22mount:_special_device_.2Fdev.2Floop5p1_does_not_exist.22)
    *   [3.2 "Waiting 10 seconds for device /dev/sda1; ERROR: Unable to find root device '/dev/sda1'"](#.22Waiting_10_seconds_for_device_.2Fdev.2Fsda1.3B_ERROR:_Unable_to_find_root_device_.27.2Fdev.2Fsda1.27.22)
    *   [3.3 "Missing operating system. FATAL: INT18: BOOT FAILURE"](#.22Missing_operating_system._FATAL:_INT18:_BOOT_FAILURE.22)
    *   [3.4 I'm asked for the root password, for maintenance](#I.27m_asked_for_the_root_password.2C_for_maintenance)

## Moving out of a VM

Moving out of a virtual environment is relatively easy.

### Set up a shared folder

Setting up a shared folder between the guest virtual machine and the host depends on the hypervisor you use. Please thus refer to their specific wiki page or manual.

If you do not already have an ext4 partition, see [Beginners' guide#Prepare the storage devices](/index.php/Beginners%27_guide#Prepare_the_storage_devices "Beginners' guide").

If you are on Windows, install [Ext2Fsd](http://www.ext2fsd.com/) to be able to mount ext volumes.

### Transfer the system

From the virtual machine, open a terminal and [transfer](/index.php/Full_system_backup_with_rsync "Full system backup with rsync") the system:

```
# rsync -aAXv /* /path/to/shared/folder --exclude={/dev/*,/proc/*,/sys/*,/tmp/*,/run/*,/mnt/*,/media/*,/lost+found,/home/*/.gvfs}

```

### Chroot and reinstall the bootloader

Boot a "live" GNU/Linux distribution, mount the root partition and [chroot](/index.php/Chroot "Chroot") into it. See [Beginners' guide#Configure the base system](/index.php/Beginners%27_guide#Configure_the_base_system "Beginners' guide").

Reinstall your bootloader/boot manager: either [Syslinux](/index.php/Syslinux "Syslinux"), [GRUB](/index.php/GRUB "GRUB") or [Gummiboot](/index.php/Gummiboot "Gummiboot"), following [Beginners' guide#Install and configure a bootloader](/index.php/Beginners%27_guide#Install_and_configure_a_bootloader "Beginners' guide"). Do not forget to update the configuration file: `syslinux.cfg` for Syslinux, `grub.cfg` for Grub, or the Gummiboot boot entries located in `/boot/loader/entries/`.

### Adjust the fstab

Since your entire root tree has been transferred to a single partition, edit the [/etc/fstab](/index.php//etc/fstab "/etc/fstab") file to reflect the right partition(s).

Check with the `blkid` command, since `lsblk` is not very useful inside a chroot.

### Re-generate the initramfs image

Because the hardware has changed, while you are still in the chroot, re-generate the initramfs image:

```
# mkinitcpio -p linux 

```

And that is about it.

You will most likely need to set up the network, since the virtual machine was probably piggybacking on the host OS's network settings. See [Beginners' guide#Configure the network](/index.php/Beginners%27_guide#Configure_the_network "Beginners' guide").

## Moving into a VM

Moving _into_ a virtual environment takes a little more effort.

### Create the container

This will create a 10 GB raw image:

```
# dd if=/dev/zero of=/media/Backup/backup.img bs=1024 count=10482381

```

**Tip:** Using `fallocate` is much faster:

```
# fallocate -l 10GiB -o 1024 /media/Backup/backup.img

```

If you want to create one the exact size of your root partition, run `fdisk -l` and use the value from the `Blocks` column for the `count=` parameter. Note that you will transfer your entire root tree, so that includes the `/boot` and `/home` folders. If you have any separate partitions for those, you need to take them into account when creating the container.

Now load the necessary module and mount it as a loopback device, on `/dev/loop5` (for example):

```
# modprobe loop
# losetup /dev/loop5 /media/Backup/backup.img

```

Next, partition the `/dev/loop5` device by running your favourite [partitioning tool](/index.php/Partitioning#Partitioning_tools "Partitioning"). Create a partition table on it (e.g. `msdos`), choose the [partition scheme](/index.php/Partitioning#Partition_scheme "Partitioning") and create the partitions. Then create a [file system](/index.php/File_system "File system") on the partitions, which will appear as `/dev/loop5p1`, `/dev/loop5p2`, etc.

### Transfer the system

Mount the loopback device and [transfer](/index.php/Full_system_backup_with_rsync "Full system backup with rsync") the system:

**Note:** If the container was saved somewhere other than `/mnt` or `/media`, do not forget to add it to the exclude list.

```
# mkdir /mnt/Virtual
# mount /dev/loop5p1 /mnt/Virtual
# rsync -aAXv /* /mnt/Virtual --exclude={/dev/*,/proc/*,/sys/*,/tmp/*,/run/*,/mnt/*,/media/*,/lost+found,/home/*/.gvfs}

```

### Convert the container to a compatible format

Change directory to where the loopback file is located and choose the appropriate command for your virtual machine:

```
$ cd /media/Backup
$ qemu-img convert -c -f raw -O qcow backup.img backup.qcow2
$ VBoxManage convertfromraw --format VDI backup.img backup.vdi
$ VBoxManage convertfromraw --format VMDK backup.img backup.vmdk

```

### Chroot and reinstall the bootloader

Connect the container to the VM, along with a Linux LiveCD (e.g. the latest Arch Linux ISO) in the VM's virtual CD-ROM, then start the VM and [chroot](/index.php/Chroot "Chroot") into it:

```
# mount /dev/sda1 /mnt
# arch-chroot /mnt /bin/bash

```

Reinstall either Syslinux or GRUB, following [Beginners' guide#Install and configure a bootloader](/index.php/Beginners%27_guide#Install_and_configure_a_bootloader "Beginners' guide"). Do not forget to update its configuration file:

*   For Syslinux, it should be `APPEND root=/dev/sda1 ro` in `syslinux.cfg`.

*   For GRUB, it is recommended that you automatically re-generate a `grub.cfg`.

### Adjust the fstab

Since your entire root tree has been transferred to a single partition, edit the [fstab](/index.php/Fstab "Fstab") file. You may use the UUID or label if you want, but those are more useful in multi-drive, multi-partition configurations (to avoid confusions). For now, `/dev/sda1` for your entire system is just fine.

 `/etc/fstab` 

```
tmpfs                    /tmp      tmpfs     nodev,nosuid          0   0
/dev/sda1                /         ext4      defaults,noatime      0   1
```

### Disable any Xorg-related files

Having an `nvidia`, `nouveau`, `radeon`, `intel`, etc., entry in the `Device` section from one of the Xorg configuration files will prevent it from starting, since you will be using _emulated_ hardware (including the video card). So it is recommended that you move/rename or delete the following:

```
# mv /etc/X11/xorg.conf /etc/X11/xorg.conf.bak
# mv /etc/X11/xorg.conf.d/10-monitor /etc/X11/xorg.conf.d/10-monitor.bak

```

### Re-generate the initramfs image

Because the hardware has changed, while you are still in the chroot, re-generate the initramfs image and do a proper shutdown:

```
# mkinitcpio -p linux
# exit
# umount -R /mnt
# poweroff

```

Finally, pull out the LiveCD (the ISO file), so that you don't boot back into it, and start the virtual machine.

Enjoy your new virtual environment.

## Troubleshooting

### "mount: special device /dev/loop5p1 does not exist"

First, check the loopback device with `fdisk` for the starting block:

 `# fdisk -l /dev/loop5` 

```
Disk /dev/loop5: 10.7 GB, 10733958144 bytes
255 heads, 63 sectors/track, 1304 cylinders, total 20964762 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x000b45e8

      Device Boot      Start         End      Blocks   Id  System
/dev/loop5p1   *        2048    20963327    10480640   83  Linux
```

Then use it as an offset when mounting it:

```
# mount -o offset=$((**2048** * 512)) /dev/loop5 /mnt/Virtual/

```

### "Waiting 10 seconds for device /dev/sda1; ERROR: Unable to find root device '/dev/sda1'"

```
Waiting 10 seconds for device /dev/sda1 ...
ERROR: Unable to find root device '/dev/sda1'.
You are being dropped to a recovery shell
    Type 'exit' to try and continue booting
sh: cannot access tty; job control turned off
[rootfs /]# _

```

It most likely means that you did not run `poweroff` like _you were instructed to_, and closed the VM with the "close" button, which is the equivalent of a power outage. Now you need to regenerate your initramfs image. To do that, you can start the VM using the Fallback entry. If you do not have a Fallback entry, press `Tab` (for Syslinux) or `e` (for GRUB) and rename it `initramfs-linux-fallback.img`. After it boots, open up a terminal and run:

```
# mkinitcpio -p linux
# poweroff

```

### "Missing operating system. FATAL: INT18: BOOT FAILURE"

*   You either need to install or reinstall a bootloader. See [Boot loaders](/index.php/Boot_loaders "Boot loaders").

*   You are using a [Btrfs](/index.php/Btrfs "Btrfs") filesystem with compression for `/boot`, for which [Syslinux](/index.php/Syslinux "Syslinux") currently cannot boot from.

*   The boot order from the BIOS or from the VM's settings is not properly set up. Make sure that the drive containing the bootloader is the first one to boot.

### I'm asked for the root password, for maintenance

```
:: Checking Filesystems                        [BUSY]
fsck.ext4: Unable to resolve '...'

```

This means that you forgot to add the drive's UUID, label or device name in `/etc/fstab`. The UUID is different every time you format it (or in this case, create one from scratch), and they likely do not match. Check with `blkid`.