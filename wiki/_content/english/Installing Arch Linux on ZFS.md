This article details the steps required to install Arch Linux onto a ZFS root filesystem. It is a supplement to the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Embedding archzfs into archiso](#Embedding_archzfs_into_archiso)
*   [2 Partition the destination drive](#Partition_the_destination_drive)
    *   [2.1 Partition scheme](#Partition_scheme)
*   [3 Format the destination disk](#Format_the_destination_disk)
*   [4 Setup the ZFS filesystem](#Setup_the_ZFS_filesystem)
    *   [4.1 Create the root zpool](#Create_the_root_zpool)
    *   [4.2 Create your datasets](#Create_your_datasets)
    *   [4.3 Configure the root filesystem](#Configure_the_root_filesystem)
*   [5 Install and configure Arch Linux](#Install_and_configure_Arch_Linux)
*   [6 Install and configure the bootloader](#Install_and_configure_the_bootloader)
    *   [6.1 For BIOS motherboards](#For_BIOS_motherboards)
    *   [6.2 For UEFI motherboards](#For_UEFI_motherboards)
*   [7 Unmount and restart](#Unmount_and_restart)
*   [8 After the first boot](#After_the_first_boot)
*   [9 See also](#See_also)

## Installation

See [ZFS#Installation](/index.php/ZFS#Installation "ZFS") for installing the ZFS packages. If installing Arch Linux onto ZFS from the archiso, it would be easier to use the [demz-repo-archiso](/index.php/Unofficial_user_repositories#demz-repo-archiso "Unofficial user repositories") repository.

### Embedding archzfs into archiso

See [ZFS](/index.php/ZFS#Embed_the_archzfs_packages_into_an_archiso "ZFS") article.

## Partition the destination drive

Review [Beginners' guide#Prepare the storage devices](/index.php/Beginners%27_guide#Prepare_the_storage_devices "Beginners' guide") for information on determining the partition table type to use for ZFS. ZFS supports GPT and MBR partition tables.

ZFS manages its own partitions, so only a basic partition table scheme is required. The partition that will contain the ZFS filesystem should be of the type `bf00`, or "Solaris Root".

When using GRUB as your bootloader with an MBR partition table there is no need for a BIOS boot partition. Drives larger than 2TB require a GPT partition table and you should use [parted](https://www.archlinux.org/packages/?name=parted) to create the partitions for GPT. BIOS/GPT and UEFI/GPT configurations require a small (1/2MB) BIOS boot partition to store the bootloader. If you are using a UEFI-only bootloader you should use GPT.

Depending upon your choice of bootloader you may or may not require an EFI partition. GRUB, when installed on a BIOS machine (or a UEFI machine booting in legacy mode) using either MBR or GPT doesn't require an EFI partition. Consult [Boot loaders](/index.php/Boot_loaders "Boot loaders") for more info.

### Partition scheme

Here is an example of a basic partition scheme that could be employed for your ZFS root install on a BIOS/MBR installation using GRUB:

```
Part     Size   Type
----     ----   -------------------------
   1     XXXG   Solaris Root (bf00)

```

Using GRUB on a BIOS (or UEFI machine in legacy boot mode) machine but using a GPT partition table:

```
Part     Size   Type
----     ----   -------------------------
   1       2M   BIOS boot partition (ef02)
   2     XXXG   Solaris Root (bf00)

```

Another example, this time using a UEFI-specific bootloader (such as [rEFInd](/index.php/REFInd "REFInd")) and GPT:

```
Part     Size   Type
----     ----   -------------------------
   1       2M   BIOS boot partition (ef02)
   2     100M   EFI boot partition (ef00)
   3     XXXG   Solaris Root (bf00)

```

ZFS does not support swap files. If you require a swap partition, see [ZFS#Swap volume](/index.php/ZFS#Swap_volume "ZFS") for creating a swap ZVOL.

**Tip:** Bootloaders with support for ZFS are described in [#Install and configure the bootloader](#Install_and_configure_the_bootloader).

**Warning:** Several GRUB bugs ([bug #42861](https://savannah.gnu.org/bugs/?42861), [zfsonlinux/grub/issues/5](https://github.com/zfsonlinux/grub/issues/5)) complicate installing it on ZFS partitions, see [#Install and configure the bootloader](#Install_and_configure_the_bootloader) for a workaround

## Format the destination disk

If you have opted for a boot partition as well as any other non-ZFS system partitions then format them. Do not do anything to the Solaris partition nor to the BIOS boot partition. ZFS will manage the first, and your bootloader the second.

## Setup the ZFS filesystem

First, make sure the ZFS modules are loaded,

```
# modprobe zfs

```

### Create the root zpool

```
# zpool create -f zroot /dev/disk/by-id/*id-to-partition-partx*

```

**Warning:**

*   Always use id names when working with ZFS, otherwise import errors will occur.
*   The zpool command will normally activate all features. See [ZFS#GRUB-compatible pool creation](/index.php/ZFS#GRUB-compatible_pool_creation "ZFS") when using [GRUB](/index.php/GRUB "GRUB").

### Create your datasets

Instead of using conventional disk partitions, ZFS has the concept of datasets to manage your storage. Unlike disk partitions, datasets have no fixed size and allow for different attributes, such as compression, to be applied per dataset. Normal ZFS datasets are mounted automatically by ZFS whilst legacy datasets are required to be mounted using fstab or with the traditional mount command.

One of the most useful features of ZFS is boot environments. Boot environments allow you to create a bootable snapshot of your system that you can revert to at any time instantly by simply rebooting and booting from that boot environment. This can make doing system updates much safer and is also incredibly useful for developing and testing software. In order to be able to use [beadm](https://github.com/b333z/beadm) to manage boot environments your datasets must be configured properly. Key to this are that you split your data directories (such as `/home`) into datasets that are distinct from your system datasets and that you do not place data in the root of the pool as this cannot be moved afterwards.

You should always create a dataset for at least your root filesystem and in nearly all cases you will also want `/home` to be in a separate dataset. You may decide you want your logs to persist over boot environments. If you are a running any software that stores data outside of `/home` (such as is the case for database servers) you should structure your datasets so that the data directories of the software you want to run are separated out from the root dataset.

With these example commands, we will create a basic boot enviroment compatible configuration comprisng of just root and `/home` datasets:

```
# zfs create -o mountpoint=none zroot/data
# zfs create -o mountpoint=none zroot/ROOT
# zfs create -o mountpoint=/ zroot/ROOT/default
# zfs create -o mountpoint=/home zroot/data/home

```

### Configure the root filesystem

If you have just created your zpool, it will be mounted in a dir at the root of your tree named after the pool (ie /zroot) so first we need to unmount it:

```
# zfs umount -a

```

Now set the mount points of the datasets:

```
# zfs set mountpoint=/ zroot/ROOT/default
# zfs set mountpoint=legacy zroot/data/home

```

and put them in `/etc/fstab`

 `/etc/fstab` 
```
# <file system>        <dir>         <type>    <options>              <dump> <pass>
zroot/ROOT/default / zfs rw,relatime,xattr,noacl 0 0
zroot/data/home /home zfs rw,relatime,xattr,noacl 0 0
```

All legacy datasets must be listed in `/etc/fstab` or they will not be mounted at boot.

Set the bootfs property on the descendant root filesystem so the boot loader knows where to find the operating system.

```
# zpool set bootfs=zroot/ROOT/default zroot

```

Export the pool,

```
# zpool export zroot

```

**Warning:** Do not skip this, otherwise you will be required to use `-f` when importing your pools. This unloads the imported pool.

**Note:** This might fail if you added a swap partition. You need to turn it off with the *swapoff* command.

Finally, re-import the pool,

```
# zpool import -d /dev/disk/by-id -R /mnt zroot

```

**Note:** `-d` is not the actual device id, but the `/dev/by-id` directory containing the symbolic links.

If there is an error in this step, you can export the pool to redo the command. The ZFS filesystem is now ready to use.

Be sure to bring the `zpool.cache` file into your new system. This is required later for the ZFS daemon to start.

```
# cp /etc/zfs/zpool.cache /mnt/etc/zfs/zpool.cache

```

if you do not have `/etc/zfs/zpool.cache`, create it:

```
# zpool set cachefile=/etc/zfs/zpool.cache zroot

```

## Install and configure Arch Linux

Follow the following steps using the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide"). It will be noted where special consideration must be taken for ZFSonLinux.

*   First mount any legacy or non-ZFS boot or system partitions using the mount command.

*   Install the base system.

*   The procedure described in [Beginners' guide#Generate an fstab](/index.php/Beginners%27_guide#Generate_an_fstab "Beginners' guide") is usually overkill for ZFS. ZFS usually auto mounts its own partitions, so we do not need ZFS partitions in `fstab` file, unless the user made legacy datasets of system directories. To generate the `fstab` for filesystems, use:

```
# genfstab -U -p /mnt >> /mnt/etc/fstab

```

*   Edit the `/etc/fstab`:

**Note:**

*   If you chose to create legacy datasets for system directories, keep them in this `fstab`!
*   Comment out all non-legacy datasets apart from the root dataset, the swap file and the boot/EFI partition. It is a convention to replace the swap's uuid with `/dev/zvol/zroot/swap`.

*   You need to add the [Arch ZFS](/index.php/Unofficial_user_repositories#demz-repo-archiso "Unofficial user repositories") repository to `/etc/pacman.conf`, sign its key and [install](/index.php/Install "Install") **zfs-git** within the arch-chroot before you can update the ramdisk with ZFS support.

*   When creating the initial ramdisk, first edit `/etc/mkinitcpio.conf` and add `zfs` before filesystems. Also, move `keyboard` hook before `zfs` so you can type in console if something goes wrong. You may also remove fsck (if you are not using Ext3 or Ext4). Your `HOOKS` line should look something like this:

```
HOOKS="base udev autodetect modconf block keyboard zfs filesystems"

```

**Note:**

*   If you are using a separate dataset for `/usr` and have followed the instructions below, you must make sure you have the `usr` hook enabled after `zfs`, or your system will not boot.

*   [Regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

## Install and configure the bootloader

### For BIOS motherboards

Follow [GRUB#BIOS systems](/index.php/GRUB#BIOS_systems "GRUB") to install GRUB onto your disk. `grub-mkconfig` does not properly detect the ZFS filesystem, so it is necessary to edit `grub.cfg` manually:

 `/boot/grub/grub.cfg` 
```
set timeout=2
set default=0

# (0) Arch Linux
menuentry "Arch Linux" {
    linux /vmlinuz-linux zfs=zroot rw
    initrd /initramfs-linux.img
}

```

if you did not create a separate /boot partition, kernel and initrd paths have to be in the following format:

```
 /dataset/@/actual/path  

```

Example with Arch installed on the main dataset (not recommended - this will not allow for boot environments):

```
   linux /@/boot/vmlinuz-linux zfs=zroot rw
   initrd /@/boot/initramfs-linux.img

```

Example with Arch installed on a separate dataset zroot/ROOT/default:

```
   linux /ROOT/default/@/boot/vmlinuz-linux zfs=zroot/ROOT/default rw 
   initrd /ROOT/default/@/boot/initramfs-linux.img

```

When you come to installing GRUB, you are likely to get an error like:

```
Failed to get canonical path of /dev/ata-yourdriveid-partx

```

Until this gets fixed, the easiest workaround is to create a symbolic link from the regular Linux device name of the partition to the device name GRUB is looking for:

```
# ln -s /dev/sdax /dev/ata-yourdriveid-partx

```

### For UEFI motherboards

Use `EFISTUB` and `rEFInd` for the UEFI boot loader. See [Beginners' guide#For UEFI motherboards](/index.php/Beginners%27_guide#For_UEFI_motherboards "Beginners' guide"). The kernel parameters in `refind_linux.conf` for ZFS should include `zfs=bootfs` or `zfs=zroot` so the system can boot from ZFS. The `root` and `rootfstype` parameters are not needed.

## Unmount and restart

We are almost done!

```
# exit
# umount /mnt/boot (if you have a legacy boot partition)
# zfs umount -a
# zpool export zroot

```

Now reboot.

**Warning:** If you do not properly export the zpool, the pool will refuse to import in the ramdisk environment and you will be stuck at the busybox terminal.

## After the first boot

If everything went fine up to this point, your system will boot. Once. For your system to be able to reboot without issues, you need to enable the `zfs.target` to auto mount the pools and set the hostid.

For each pool you want automatically mounted execute:

```
# zpool set cachefile=/etc/zfs/zpool.cache <pool>

```

Enable the target with [systemd](/index.php/Systemd "Systemd"):

```
# systemctl enable zfs.target

```

When running ZFS on root, the machine's hostid will not be available at the time of mounting the root filesystem. There are two solutions to this. You can either place your spl hostid in the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") in your boot loader. For example, adding `spl.spl_hostid=0x00bab10c`, to get your number use the `hostid` command.

The other, and suggested, solution is to make sure that there is a hostid in `/etc/hostid`, and then regenerate the initramfs image which will copy the hostid into the initramfs image. To write the hostid file safely you need to use a small C program:

```
#include <stdio.h>
#include <errno.h>
#include <unistd.h>

int main() {
    int res;
    res = sethostid(gethostid());
    if (res != 0) {
        switch (errno) {
            case EACCES:
            fprintf(stderr, "Error! No permission to write the"
                         " file used to store the host ID.
"
                         "Are you root?
");
            break;
            case EPERM:
            fprintf(stderr, "Error! The calling process's effective"
                            " user or group ID is not the same as"
                            " its corresponding real ID.
");
            break;
            default:
            fprintf(stderr, "Unknown error.
");
        }
        return 1;
    }
    return 0;
}

```

Copy it, save it as `writehostid.c` and compile it with `gcc -o writehostid writehostid.c`, finally execute it and regenerate the initramfs image:

```
# ./writehostid
# mkinitcpio -p linux

```

You can now delete the two files `writehostid.c` and `writehostid`. Your system should work and reboot properly now.

## See also

*   [HOWTO install Ubuntu to a Native ZFS Root](https://github.com/dajhorn/pkg-zfs/wiki/HOWTO-install-Ubuntu-to-a-Native-ZFS-Root-Filesystem)
*   [ZFS cheatsheet](http://lildude.co.uk/zfs-cheatsheet)
*   [Funtoo ZFS install guide](http://www.funtoo.org/wiki/ZFS_Install_Guide)