The following are examples of common scenarios of full system encryption with *dm-crypt*. They explain all the adaptations that need to be done to the normal [installation procedure](/index.php/Installation_guide "Installation guide"). All the necessary tools are on the [installation image](https://www.archlinux.org/download/).

## Contents

*   [1 Overview](#Overview)
*   [2 Simple partition layout with LUKS](#Simple_partition_layout_with_LUKS)
    *   [2.1 Preparing the disk](#Preparing_the_disk)
    *   [2.2 Preparing non-boot partitions](#Preparing_non-boot_partitions)
    *   [2.3 Preparing the boot partition](#Preparing_the_boot_partition)
    *   [2.4 Mounting the devices](#Mounting_the_devices)
    *   [2.5 Configuring mkinitcpio](#Configuring_mkinitcpio)
    *   [2.6 Configuring the boot loader](#Configuring_the_boot_loader)
*   [3 LVM on LUKS](#LVM_on_LUKS)
    *   [3.1 Preparing the disk](#Preparing_the_disk_2)
    *   [3.2 Preparing the logical volumes](#Preparing_the_logical_volumes)
    *   [3.3 Preparing the boot partition](#Preparing_the_boot_partition_2)
    *   [3.4 Configuring mkinitcpio](#Configuring_mkinitcpio_2)
    *   [3.5 Configuring the boot loader](#Configuring_the_boot_loader_2)
*   [4 LUKS on LVM](#LUKS_on_LVM)
    *   [4.1 Preparing the disk](#Preparing_the_disk_3)
    *   [4.2 Preparing the logical volumes](#Preparing_the_logical_volumes_2)
    *   [4.3 Preparing the boot partition](#Preparing_the_boot_partition_3)
    *   [4.4 Configuring mkinitcpio](#Configuring_mkinitcpio_3)
    *   [4.5 Configuring the boot loader](#Configuring_the_boot_loader_3)
    *   [4.6 Configuring fstab and crypttab](#Configuring_fstab_and_crypttab)
    *   [4.7 Encrypting logical volume /home](#Encrypting_logical_volume_.2Fhome)
*   [5 LUKS on software RAID](#LUKS_on_software_RAID)
    *   [5.1 Preparing the disks](#Preparing_the_disks)
    *   [5.2 Building the RAID array](#Building_the_RAID_array)
    *   [5.3 Preparing the block devices](#Preparing_the_block_devices)
    *   [5.4 Configuring the boot loader](#Configuring_the_boot_loader_4)
    *   [5.5 Creating the keyfiles](#Creating_the_keyfiles)
    *   [5.6 Configuring the system](#Configuring_the_system)
*   [6 Plain dm-crypt](#Plain_dm-crypt)
    *   [6.1 Preparing the disk](#Preparing_the_disk_4)
    *   [6.2 Preparing the non-boot partitions](#Preparing_the_non-boot_partitions)
    *   [6.3 Preparing the boot partition](#Preparing_the_boot_partition_4)
    *   [6.4 Configuring mkinitcpio](#Configuring_mkinitcpio_4)
    *   [6.5 Configuring the boot loader](#Configuring_the_boot_loader_5)
    *   [6.6 Post-installation](#Post-installation)
*   [7 Encrypted boot partition (GRUB)](#Encrypted_boot_partition_.28GRUB.29)
    *   [7.1 Preparing the disk](#Preparing_the_disk_5)
    *   [7.2 Preparing the logical volumes](#Preparing_the_logical_volumes_3)
    *   [7.3 Preparing the boot partition](#Preparing_the_boot_partition_5)
    *   [7.4 Configuring mkinitcpio](#Configuring_mkinitcpio_5)
    *   [7.5 Configuring the boot loader](#Configuring_the_boot_loader_6)
    *   [7.6 Configuring fstab and crypttab](#Configuring_fstab_and_crypttab_2)
*   [8 Btrfs subvolumes with swap](#Btrfs_subvolumes_with_swap)
    *   [8.1 Preparing the disk](#Preparing_the_disk_6)
    *   [8.2 Preparing the system partition](#Preparing_the_system_partition)
        *   [8.2.1 Create LUKS container](#Create_LUKS_container)
        *   [8.2.2 Unlock LUKS container](#Unlock_LUKS_container)
        *   [8.2.3 Format mapped device](#Format_mapped_device)
        *   [8.2.4 Mount mapped device](#Mount_mapped_device)
    *   [8.3 Creating btrfs subvolumes](#Creating_btrfs_subvolumes)
        *   [8.3.1 Layout](#Layout)
        *   [8.3.2 Create top-level subvolumes](#Create_top-level_subvolumes)
        *   [8.3.3 Mount top-level subvolumes](#Mount_top-level_subvolumes)
        *   [8.3.4 Create nested subvolumes](#Create_nested_subvolumes)
        *   [8.3.5 Mount ESP](#Mount_ESP)
    *   [8.4 Configuring mkinitcpio](#Configuring_mkinitcpio_6)
        *   [8.4.1 Create keyfile](#Create_keyfile)
        *   [8.4.2 Edit mkinitcpio.conf](#Edit_mkinitcpio.conf)
    *   [8.5 Configuring the boot loader](#Configuring_the_boot_loader_7)
    *   [8.6 Configuring swap](#Configuring_swap)

## Overview

Securing a root filesystem is where *dm-crypt* excels, feature and performance-wise. Unlike selectively encrypting non-root filesystems, an encrypted root filesystem can conceal information such as which programs are installed, the usernames of all user accounts, and common data-leakage vectors such as [mlocate](/index.php/Mlocate "Mlocate") and `/var/log/`. Furthermore, an encrypted root filesystem makes tampering with the system far more difficult, as everything except the [boot loader](/index.php/Boot_loader "Boot loader") and (usually) the kernel is encrypted.

All scenarios illustrated in the following share these advantages, other pros and cons differentiating them are summarized below:

| Scenarios | Advantages | Disadvantages |
| [#Simple partition layout with LUKS](#Simple_partition_layout_with_LUKS)

shows a basic and straight-forward set-up for a fully LUKS encrypted root.

 | 

*   Simple partitioning and setup

 | 

*   Inflexible; disk-space to be encrypted has to be pre-allocated

 |
| [#LVM on LUKS](#LVM_on_LUKS)

achieves partitioning flexiblity by using LVM inside a single LUKS encrypted partition.

 | 

*   Simple partitioning with knowledge of LVM
*   Only one key required to unlock all volumes (e.g. easy resume-from-disk setup)
*   Volume layout not transparent when locked
*   Easiest method to allow [suspension to disk](/index.php/Dm-crypt/Swap_encryption#With_suspend-to-disk_support "Dm-crypt/Swap encryption")

 | 

*   LVM adds an additional mapping layer and hook
*   Less useful, if a singular volume should receive a separate key

 |
| [#LUKS on LVM](#LUKS_on_LVM)

uses dm-crypt only after the LVM is setup.

 | 

*   LVM can be used to have encrypted volumes span multiple disks
*   Easy mix of un-/encrypted volume groups

 | 

*   Complex; changing volumes requires changing encryption mappers too
*   Volumes require individual keys
*   LVM layout is transparent when locked

 |
| [#LUKS on software RAID](#LUKS_on_software_RAID)

uses dm-crypt only after RAID is setup.

 | 

*   Analogous to LUKS on LVM

 | 

*   Analogous to LUKS on LVM

 |
| [#Plain dm-crypt](#Plain_dm-crypt)

uses dm-crypt plain mode, i.e. without a LUKS header and its options for multiple keys.
This scenario also employs USB devices for `/boot` and key storage, which may be applied to the other scenarios.

 | 

*   Data resilience for cases where a LUKS header may be damaged
*   Allows [Full Disk Encryption](https://en.wikipedia.org/wiki/Disk_encryption#Full_disk_encryption "wikipedia:Disk encryption")
*   Helps addressing [problems](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") with SSDs

 | 

*   High care to all encryption parameters is required
*   Single encryption key and no option to change it

 |
| [#Encrypted boot partition (GRUB)](#Encrypted_boot_partition_.28GRUB.29)

shows how to encrypt the boot partition using the GRUB bootloader.
This scenario also employs an ESP partition, which may be applied to the other scenarios.

 | 

*   Same advantages as the scenario the installation is based on (LVM on LUKS for this particular example)
*   Less data is left unencrypted, i.e. the boot loader and the ESP partition, if present

 | 

*   Same disadvantages as the scenario the installation is based on (LVM on LUKS for this particular example)
*   More complicated configuration
*   Not supported by other boot loaders

 |
| [#Btrfs subvolumes with swap](#Btrfs_subvolumes_with_swap)

shows how to encrypt a [Btrfs](/index.php/Btrfs "Btrfs") system, including the `/boot` directory, also adding a partition for swap, on UEFI hardware.

 | 

*   Similar advantages as [#Encrypted boot partition (GRUB)](#Encrypted_boot_partition_.28GRUB.29)
*   Availability of Btrfs' features

 | 

*   Similar disadvantages as [#Encrypted boot partition (GRUB)](#Encrypted_boot_partition_.28GRUB.29)

 |

While all above scenarios provide much greater protection from outside threats than encrypted secondary filesystems, they also share a common disadvantage: any user in possession of the encryption key is able to decrypt the entire drive, and therefore can access other users' data. If that is of concern, it is possible to use a combination of blockdevice and stacked filesystem encryption and reap the advantages of both. See [Disk encryption](/index.php/Disk_encryption "Disk encryption") to plan ahead.

See [Dm-crypt/Drive preparation#Partitioning](/index.php/Dm-crypt/Drive_preparation#Partitioning "Dm-crypt/Drive preparation") for a general overview of the partitioning strategies used in the scenarios.

Another area to consider is whether to set up an encrypted swap partition and what kind. See [Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") for alternatives.

If you anticipate to protect the system's data not only against physical theft, but also have a requirement of precautions against logical tampering, see [Dm-crypt/Specialties#Securing the unencrypted boot partition](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties") for further possibilities after following one of the scenarios.

**Warning:** In any scenario, never use file system repair software such as [fsck](/index.php/Fsck "Fsck") directly on an encrypted volume, or it will destroy any means to recover the key used to decrypt your files. Such tools must be used on the decrypted (opened) device instead.

## Simple partition layout with LUKS

This example covers a full system encryption with *dmcrypt* + LUKS in a simple partition layout:

```
+--------------------+--------------------------+--------------------------+
|Boot partition      |LUKS encrypted system     |Optional free space       |
|                    |partition                 |for additional partitions |
|/dev/sdaY           |/dev/sdaX                 |or swap to be setup later |
+--------------------+--------------------------+--------------------------+

```

The first steps can be performed directly after booting the Arch Linux install image.

### Preparing the disk

Prior to creating any partitions, you should inform yourself about the importance and methods to securely erase the disk, described in [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

Then create the needed partitions, at least one for `/` (e.g. `/dev/sdaX`) and `/boot` (`/dev/sdaY`). See [Partitioning](/index.php/Partitioning "Partitioning").

### Preparing non-boot partitions

The following commands create and mount the encrypted root partition. They correspond to the procedure described in detail in [Dm-crypt/Encrypting a non-root file system#Partition](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Partition "Dm-crypt/Encrypting a non-root file system") (which, despite the title, *can* be applied to root partitions, as long as [mkinitcpio](#Configuring_mkinitcpio) and the [boot loader](#Configuring_the_boot_loader) are correctly configured). If you want to use particular non-default encryption options (e.g. cipher, key length), see the [encryption options](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") before executing the first command:

```
# cryptsetup -y -v luksFormat --type luks2 /dev/sdaX
# cryptsetup open /dev/sdaX cryptroot
# mkfs.ext4 /dev/mapper/cryptroot
# mount /dev/mapper/cryptroot /mnt

```

Check the mapping works as intended:

```
# umount /mnt
# cryptsetup close cryptroot
# cryptsetup open /dev/sdaX cryptroot
# mount /dev/mapper/cryptroot /mnt

```

If you created separate partitions (e.g. `/home`), these steps have to be adapted and repeated for all of them, *except* for `/boot`. See [Dm-crypt/Encrypting a non-root file system#Automated unlocking and mounting](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Automated_unlocking_and_mounting "Dm-crypt/Encrypting a non-root file system") on how to handle additional partitions at boot.

Note that each blockdevice requires its own passphrase. This may be inconvenient, because it results in a separate passphrase to be input during boot. An alternative is to use a keyfile stored in the system partition to unlock the separate partition via `crypttab`. See [Dm-crypt/Device encryption#Using LUKS to format partitions with a keyfile](/index.php/Dm-crypt/Device_encryption#Using_LUKS_to_format_partitions_with_a_keyfile "Dm-crypt/Device encryption") for instructions.

### Preparing the boot partition

What you do have to setup is a non-encrypted `/boot` partition, which is needed for a encrypted root. For a standard [MBR/non-EFI](/index.php/EFI "EFI") `/boot` partition, for example, execute:

```
# mkfs.ext4 /dev/sdaY
# mkdir /mnt/boot
# mount /dev/sdaY /mnt/boot

```

### Mounting the devices

At [Installation guide#Mount the file systems](/index.php/Installation_guide#Mount_the_file_systems "Installation guide") you will have to mount the mapped devices, not the actual partitions. Of course `/boot`, which is not encrypted, will still have to be mounted directly.

Afterwards continue with the installation procedure up to the mkinitcpio step.

### Configuring mkinitcpio

Add the `keyboard`, `keymap` and `encrypt` hooks to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"). If the default US keymap is fine for you, you can omit the `keymap` hook.

 `/etc/mkinitcpio.conf`  `HOOKS=(... **keyboard** **keymap** block **encrypt** ... filesystems ...)` 

Depending on which other hooks are used, the order may be relevant. See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details and other hooks that you may need.

### Configuring the boot loader

In order to unlock the encrypted root partition at boot, the following kernel parameters need to be set by the boot loader:

```
cryptdevice=UUID=*<device-UUID>*:cryptroot root=/dev/mapper/cryptroot

```

See [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") for details.

The `*<device-UUID>*` refers to the UUID of `/dev/sdaX`. See [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") for details.

## LVM on LUKS

The straight-forward method is to set up [LVM](/index.php/LVM "LVM") on top of the encrypted partition instead of the other way round. Technically the LVM is setup inside one big encrypted blockdevice. Hence, the LVM is not transparent until the blockdevice is unlocked and the underlying volume structure is scanned and mounted during boot.

The disk layout in this example is:

```
+-----------------------------------------------------------------------+ +----------------+
| Logical volume1       | Logical volume2       | Logical volume3       | |                |
|/dev/mapper/MyVol-swap |/dev/mapper/MyVol-root |/dev/mapper/MyVol-home | | Boot partition |
|_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _| | (may be on     |
|                                                                       | | other device)  |
|                        LUKS encrypted partition                       | |                |
|                          /dev/sdaX                                    | | /dev/sdbY      |
+-----------------------------------------------------------------------+ +----------------+

```

**Warning:** This method does not allow you to span the logical volumes over multiple disks easily; see [Dm-crypt/Specialties#Modifying the encrypt hook for multiple partitions](/index.php/Dm-crypt/Specialties#Modifying_the_encrypt_hook_for_multiple_partitions "Dm-crypt/Specialties").

**Tip:** Three variants of this setup:

*   Instructions at [dm-crypt/Specialties#Encrypted system using a detached LUKS header](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_detached_LUKS_header "Dm-crypt/Specialties") use this setup with a detached LUKS header on a USB device to achieve a two factor authentication with it.
*   Instructions at [Pavel Kogan's blog](http://www.pavelkogan.com/2014/05/23/luks-full-disk-encryption/) show how to encrypt the `/boot` partition while keeping it on the main LUKS partition when using GRUB.
*   Instructions at [Dm-crypt/Specialties#Encrypted /boot and a detached LUKS header on USB](/index.php/Dm-crypt/Specialties#Encrypted_.2Fboot_and_a_detached_LUKS_header_on_USB "Dm-crypt/Specialties") use this setup with a detached LUKS header, encrypted `/boot` partition, and encrypted keyfile all on a USB device.

### Preparing the disk

Prior to creating any partitions, you should inform yourself about the importance and methods to securely erase the disk, described in [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

When using the [GRUB](/index.php/GRUB "GRUB") bootloader together with [GPT](/index.php/GPT "GPT"), create a BIOS Boot Partition as explained in [GRUB#BIOS systems](/index.php/GRUB#BIOS_systems "GRUB").

Create a partition to be mounted at `/boot` of type `8300` with a size of 100 MB or more.

Create a partition of type `8E00`, which will later contain the encrypted container.

Create the LUKS encrypted container at the "system" partition. Enter the chosen password twice.

```
# cryptsetup luksFormat --type luks2 /dev/*sdaX*

```

For more information about the available cryptsetup options see the [LUKS encryption options](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") prior to above command.

Open the container:

```
# cryptsetup open /dev/*sdaX* cryptolvm

```

The decrypted container is now available at `/dev/mapper/cryptolvm`.

### Preparing the logical volumes

Create a physical volume on top of the opened LUKS container:

```
# pvcreate /dev/mapper/cryptolvm

```

Create the volume group named `MyVol` (or whatever you want), adding the previously created physical volume to it:

```
# vgcreate MyVol /dev/mapper/cryptolvm

```

Create all your logical volumes on the volume group:

```
# lvcreate -L 8G MyVol -n swap
# lvcreate -L 15G MyVol -n root
# lvcreate -l 100%FREE MyVol -n home

```

Format your filesystems on each logical volume:

```
# mkfs.ext4 /dev/mapper/MyVol-root
# mkfs.ext4 /dev/mapper/MyVol-home
# mkswap /dev/mapper/MyVol-swap

```

Mount your filesystems:

```
# mount /dev/mapper/MyVol-root /mnt
# mkdir /mnt/home
# mount /dev/mapper/MyVol-home /mnt/home
# swapon /dev/mapper/MyVol-swap

```

### Preparing the boot partition

The bootloader loads the kernel, [initramfs](/index.php/Initramfs "Initramfs"), and its own configuration files from the `/boot` directory. This directory must be located on a separate unencrypted filesystem.

Create an Ext2 filesystem on the partition intended for `/boot`. Any filesystem that can be read by the bootloader is eligible.

```
# mkfs.ext2 /dev/*sdbY*

```

Create the directory `/mnt/boot`:

```
# mkdir /mnt/boot

```

Mount the partition to `/mnt/boot`:

```
# mount /dev/*sdbY* /mnt/boot

```

Afterwards continue with the installation procedure up to the `mkinitcpio` step.

### Configuring mkinitcpio

Add the `keyboard`, `encrypt` and `lvm2` hooks to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

 `/etc/mkinitcpio.conf`  `HOOKS=(... **keyboard** **keymap** block **encrypt** **lvm2** ... filesystems ...)` 

See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details and other hooks that you may need.

### Configuring the boot loader

In order to unlock the encrypted root partition at boot, the following kernel parameter needs to be set by the boot loader:

```
cryptdevice=UUID=*device-UUID*:cryptolvm root=/dev/mapper/MyVol-root

```

The `*<device-UUID>*` refers to the UUID of `/dev/sdaX`. See [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") for details.

See [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") for details.

## LUKS on LVM

To use encryption on top of [LVM](/index.php/LVM "LVM"), the LVM volumes are set up first and then used as the base for the encrypted partitions. This way, a mixture of encrypted and non-encrypted volumes/partitions is possible as well.

**Tip:** Unlike [#LVM on LUKS](#LVM_on_LUKS), this method allows normally spanning the logical volumes over multiple disks.

The following short example creates a LUKS on LVM setup and mixes in the use of a key-file for the /home partition and temporary crypt volumes for `/tmp` and `/swap`. The latter is considered desirable from a security perspective, because no potentially sensitive temporary data survives the reboot, when the encryption is re-initialised. If you are experienced with LVM, you will be able to ignore/replace LVM and other specifics according to your plan. If you want to span a logical volume over multiple disks during setup already, a procedure to do so is described in [Dm-crypt/Specialties#Expanding LVM on multiple disks](/index.php/Dm-crypt/Specialties#Expanding_LVM_on_multiple_disks "Dm-crypt/Specialties").

### Preparing the disk

Partitioning scheme:

```
+----------------+-----------------------------------------------------------------------+
|                | LUKS encrypted volume | LUKS encrypted volume | LUKS encrypted volume |
|                | /dev/mapper/swap      | /dev/mapper/root      | /dev/mapper/home      |
|                |_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _|
|                | Logical volume1       | Logical volume2       | Logical volume3       |
|                |/dev/mapper/MyVol-swap |/dev/mapper/MyVol-root |/dev/mapper/MyVol-home |
|                |_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _|
| Boot partition |                                                                       |
|   /dev/sda1    |                               /dev/sda2                               |
+----------------+-----------------------------------------------------------------------+

```

Randomise `/dev/sda2` according to [Dm-crypt/Drive preparation#dm-crypt wipe on an empty disk or partition](/index.php/Dm-crypt/Drive_preparation#dm-crypt_wipe_on_an_empty_disk_or_partition "Dm-crypt/Drive preparation").

### Preparing the logical volumes

```
# pvcreate /dev/sda2
# vgcreate MyVol /dev/sda2
# lvcreate -L 10G -n lvroot MyVol
# lvcreate -L 500M -n swap MyVol
# lvcreate -L 500M -n tmp MyVol
# lvcreate -l 100%FREE -n home MyVol

```

```
# cryptsetup luksFormat --type luks2 -c aes-xts-plain64 -s 512 /dev/mapper/MyVol-lvroot
# cryptsetup open /dev/mapper/MyVol-lvroot root
# mkfs.ext4 /dev/mapper/root
# mount /dev/mapper/root /mnt

```

More information about the encryption options can be found in [Dm-crypt/Device encryption#Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption"). Note that `/home` will be encrypted in [#Encrypting logical volume /home](#Encrypting_logical_volume_.2Fhome). Further, note that if you ever have to access the encrypted root from the Arch-ISO, the above `open` action will allow you to after the [LVM shows up](/index.php/LVM#Logical_Volumes_do_not_show_up "LVM").

### Preparing the boot partition

```
# dd if=/dev/zero of=/dev/sda1 bs=1M status=progress
# mkfs.ext4 /dev/sda1
# mkdir /mnt/boot
# mount /dev/sda1 /mnt/boot

```

Now after setup of the encrypted LVM partitioning, it would be time to install: [Arch Install Scripts](/index.php/Installation_guide#Mount_the_file_systems "Installation guide").

### Configuring mkinitcpio

Add the `keyboard`, `lvm2` and `encrypt` hooks to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

 `/etc/mkinitcpio.conf`  `HOOKS=(... **keyboard** **keymap** block **lvm2** **encrypt** ... filesystems ...)` 

See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details and other hooks that you may need.

### Configuring the boot loader

In order to unlock the encrypted root partition at boot, the following kernel parameters need to be set by the boot loader:

```
cryptdevice=/dev/mapper/MyVol-lvroot:root root=/dev/mapper/root

```

See [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") for details.

### Configuring fstab and crypttab

 `/etc/fstab` 
```
/dev/mapper/root        /       ext4            defaults        0       1
/dev/sda1               /boot   ext4            defaults        0       2
/dev/mapper/tmp         /tmp    tmpfs           defaults        0       0
/dev/mapper/swap        none    swap            sw              0       0

```

The following [crypttab](/index.php/Crypttab "Crypttab") options will re-encrypt the temporary filesystems each reboot:

 `/etc/crypttab` 
```
swap	/dev/mapper/MyVol-swap	/dev/urandom	swap,cipher=aes-xts-plain64,size=256
tmp	/dev/mapper/MyVol-tmp	/dev/urandom	tmp,cipher=aes-xts-plain64,size=256

```

### Encrypting logical volume /home

Since this scenario uses LVM as the primary and dm-crypt as secondary mapper, each encrypted logical volume requires its own encryption. Yet, unlike the temporary filesystems configured with volatile encryption above, the logical volume for `/home` should be persistent, of course. The following assumes you have rebooted into the installed system, otherwise you have to adjust paths. To safe on entering a second passphrase at boot for it, a [keyfile](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") is created:

```
# mkdir -m 700 /etc/luks-keys
# dd if=/dev/random of=/etc/luks-keys/home bs=1 count=256 status=progress

```

The logical volume is encrypted with it:

```
# cryptsetup luksFormat --type luks2 -v -s 512 /dev/mapper/MyVol-home /etc/luks-keys/home
# cryptsetup -d /etc/luks-keys/home open /dev/mapper/MyVol-home home
# mkfs.ext4 /dev/mapper/home
# mount /dev/mapper/home /home

```

The encrypted mount is configured in [crypttab](/index.php/Crypttab "Crypttab"):

 `/etc/crypttab` 
```
home	/dev/mapper/MyVol-home   /etc/luks-keys/home

```
 `/etc/fstab` 
```
/dev/mapper/home        /home   ext4        defaults        0       2

```

and setup is done.

If you want to expand the logical volume for `/home` (or any other volume) at a later point, it is important to note that the LUKS encrypted part has to be resized as well. For a procedure see [Dm-crypt/Specialties#Expanding LVM on multiple disks](/index.php/Dm-crypt/Specialties#Expanding_LVM_on_multiple_disks "Dm-crypt/Specialties").

## LUKS on software RAID

This example is based on a real-world setup for a workstation class laptop equipped with two SSDs of equal size, and an additional HDD for bulk storage. The end result is LUKS based full disk encryption (including `/boot`) for all drives, with the SSDs in a [RAID0](/index.php/RAID "RAID") array, and keyfiles used to unlock all encryption after [GRUB](/index.php/GRUB "GRUB") is given a correct passphrase at boot. [TRIM](/index.php/TRIM "TRIM") support is enabled on the SSDs, but you may wish to review the security implications detailed at [Dm-crypt/Specialties#Discard/TRIM support for solid state drives (SSD)](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") before considering using this.

This setup utilizes a very simplistic partitioning scheme, with all the available RAID storage being mounted at `/` (no separate `/boot` partition), and the decrypted HDD being mounted at `/mnt/data`. It is also worth mentioning that the system in this example boots in BIOS mode and the drives are partitioned with [GPT](/index.php/Partitioning "Partitioning") partitions.

Please note that regular [backups](/index.php/System_backup "System backup") are very important in this setup. If either of the SSDs fail, the data contained in the RAID array will be practically impossible to recover. You may wish to select a different [RAID level](/index.php/RAID#Standard_RAID_levels "RAID") if fault tolerance is important to you.

The encryption is not deniable in this setup.

For the sake of the instructions below, the following block devices are used:

```
/dev/sda = first SSD
/dev/sdb = second SSD
/dev/sdc = HDD

```

Be sure to substitue them with the appropriate device designations for your setup, as they may be different.

### Preparing the disks

Prior to creating any partitions, you should inform yourself about the importance and methods to securely erase the disk, described in [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

When using the [GRUB](/index.php/GRUB "GRUB") bootloader together with [GPT](/index.php/GPT "GPT"), create a BIOS Boot Partition as explained in [GRUB#BIOS systems](/index.php/GRUB#BIOS_systems "GRUB"). For this setup, this includes a 1M partition for "BIOS boot" at `/dev/sda1` and the remaining space on the drive being partitioned for "Linux RAID" at `/dev/sda2`.

Once partitions have been created on `/dev/sda`, the following commands can be used to clone them to `/dev/sdb`.

```
# sfdisk -d /dev/sda > sda.dump
# sfdisk /dev/sdb < sda.dump

```

The HDD is prepared with a single Linux partition covering the whole drive at `/dev/sdc1`.

### Building the RAID array

Create the RAID array for the SSDs. This example utilizes RAID0, you may wish to substitute a different level based on your preferences or requirements.

```
# mdadm --create --verbose --level=0 --metadata=1.2 --raid-devices=2 /dev/md0 /dev/sda2 /dev/sdb2

```

### Preparing the block devices

As explained in [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation"), the devices are wiped with random data utilizing `/dev/zero` and a crypt device with a random key. Alternatively, you could use `dd` with `/dev/random` or `/dev/urandom`, though it will be much slower.

```
# cryptsetup open --type plain /dev/md0 container --key-file /dev/random
# dd if=/dev/zero of=/dev/mapper/container bs=1M status=progress
# cryptsetup close container

```

And repeat above for the HDD (`/dev/sdc1` in this example).

Set up encryption for `/dev/md0`:

```
# cryptsetup -y -v luksFormat --type luks2 -c aes-xts-plain64 -s 512 /dev/md0
# cryptsetup open /dev/md0 cryptroot
# mkfs.ext4 /dev/mapper/cryptroot
# mount /dev/mapper/cryptroot /mnt

```

And repeat for the HDD:

```
# cryptsetup -y -v luksFormat --type luks2 -c aes-xts-plain64 -s 512 /dev/sdc1
# cryptsetup open /dev/sdc1 cryptdata
# mkfs.ext4 /dev/mapper/cryptdata
# mkdir -p /mnt/mnt/data
# mount /dev/mapper/cryptdata /mnt/mnt/data

```

### Configuring the boot loader

Configure [GRUB](/index.php/GRUB "GRUB") for the encrypted system by editing `/etc/default/grub` with the following. Note that the `:allow-discards` option enables TRIM support on the SSDs, if you do not wish to use it you should omit this.

```
GRUB_CMDLINE_LINUX="cryptdevice=/dev/md0:cryptroot:allow-discards root=/dev/mapper/cryptroot"
GRUB_ENABLE_CRYPTODISK=y

```

See [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") and [GRUB#Boot partition](/index.php/GRUB#Boot_partition "GRUB") for details.

Complete the GRUB install to both SSDs (in reality, installing only to `/dev/sda` will work).

```
# grub-install --target=i386-pc /dev/sda
# grub-install --target=i386-pc /dev/sdb
# grub-mkconfig -o /boot/grub/grub.cfg

```

### Creating the keyfiles

The next steps save you from entering your passphrase twice when you boot the system (once so GRUB can unlock the encryption, and second time once the initramfs assumes control of the system). This is done by creating a [keyfile](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") for the encryption and adding it to the initramfs image to allow the encrypt hook to unlock the root device. See [dm-crypt/Device encryption#With a keyfile embedded in the initramfs](/index.php/Dm-crypt/Device_encryption#With_a_keyfile_embedded_in_the_initramfs "Dm-crypt/Device encryption") for details.

*   Create the [keyfile](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") and add the key to `/dev/md0`.
*   Create another keyfile for the HDD (`/dev/sdc1`) so it can also be unlocked at boot. For convenience, leave the passphrase created above in place as this can make recovery easier if you ever need it. Edit `/etc/crypttab` to decrypt the HDD at boot. See [dm-crypt/Device encryption#Unlocking a secondary partition at boot](/index.php/Dm-crypt/Device_encryption#Unlocking_a_secondary_partition_at_boot "Dm-crypt/Device encryption").

### Configuring the system

Edit [/etc/fstab](/index.php/Fstab "Fstab") to mount the cryptroot and cryptdata block devices; if you are not enabling TRIM support, delete the `discard` mount option:

```
/dev/mapper/cryptroot  /           ext4    rw,noatime,discard  0   1 
/dev/mapper/cryptdata  /mnt/data   ext4    defaults            0   2  

```

Save the RAID configuration:

```
# mdadm --detail --scan > /etc/mdadm.conf 

```

Edit [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") to include your keyfile and add the proper hooks:

```
FILES=(/crypto_keyfile.bin)
HOOKS=( ... **keyboard** **keymap** block **mdadm_udev** **encrypt** filesystems ... )

```

See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details.

## Plain dm-crypt

Contrary to LUKS, dm-crypt *plain* mode does not require a header on the encrypted device: this scenario exploits this feature to set up a system on an unpartitioned, encrypted disk that will be indistinguishable from a disk filled with random data, which could allow [deniable encryption](https://en.wikipedia.org/wiki/Deniable_encryption "wikipedia:Deniable encryption"). See also [wikipedia:Disk encryption#Full disk encryption](https://en.wikipedia.org/wiki/Disk_encryption#Full_disk_encryption "wikipedia:Disk encryption").

Note that if full-disk encryption is not required, the methods using LUKS described in the sections above are better options for both system encryption and encrypted partitions. LUKS features like key management with multiple passphrases/key-files or re-encrypting a device in-place are unavailable with *plain* mode.

*Plain* dm-crypt encryption can be more resilient to damage than LUKS, because it does not rely on an encryption master-key which can be a single-point of failure if damaged. However, using *plain* mode also requires more manual configuration of encryption options to achieve the same cryptographic strength. See also [Disk encryption#Cryptographic metadata](/index.php/Disk_encryption#Cryptographic_metadata "Disk encryption"). Using *plain* mode could also be considered if concerned with the problems explained in [Dm-crypt/Specialties#Discard/TRIM support for solid state drives (SSD)](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties").

**Tip:** If headerless encryption is your goal but you are unsure about the lack of key-derivation with *plain* mode, then two alternatives are:

*   [dm-crypt LUKS mode with a detached header](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_detached_LUKS_header "Dm-crypt/Specialties") by using the *cryptsetup* `--header` option. It cannot be used with the standard *encrypt* hook, but the hook may be modified.
*   [tcplay](/index.php/Tcplay "Tcplay") which offers headerless encryption but with the PBKDF2 function.

The scenario uses two USB sticks:

*   one for the boot device, which also allows storing the options required to open/unlock the plain encrypted device in the boot loader configuration, since typing them on each boot would be error prone;
*   another for the encryption key file, assuming it stored as raw bits so that to the eyes of an unaware attacker who might get the usbkey the encryption key will appear as random data instead of being visible as a normal file. See also [Wikipedia:Security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity "wikipedia:Security through obscurity"), follow [Dm-crypt/Device encryption#Keyfiles](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") to prepare the keyfile.

The disk layout is:

```
+--------------------+------------------+--------------------+ +---------------+ +---------------+
|Volume 1:           |Volume 2:         |Volume 3:           | |Boot device    | |Encryption key |
|                    |                  |                    | |               | |file storage   |
|root                |swap              |home                | |/boot          | |(unpartitioned |
|                    |                  |                    | |               | |in example)    |
|/dev/store/root     |/dev/store/swap   |/dev/store/home     | |/dev/sdY1      | |/dev/sdZ       |
|--------------------+------------------+--------------------| |---------------| |---------------|
|disk drive /dev/sdaX encrypted using plain mode and LVM     | |USB stick 1    | |USB stick 2    |
+------------------------------------------------------------+ +---------------+ +---------------+

```

**Tip:**

*   It is also possible to use a single usb key by copying the keyfile to the initram directly. An example keyfile `/etc/keyfile` gets copied to the initram image by setting `FILES=(/etc/keyfile)` in `/etc/mkinitcpio.conf`. The way to instruct the `encrypt` hook to read the keyfile in the initram image is using `rootfs:` prefix before the filename, e.g. `cryptkey=rootfs:/etc/keyfile`.
*   Another option is using a passphrase with good [entropy](/index.php/Disk_encryption#Choosing_a_strong_passphrase "Disk encryption").

### Preparing the disk

It is vital that the mapped device is filled with data. In particular this applies to the scenario usecase we apply here.

See [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation") and [Dm-crypt/Drive preparation#dm-crypt specific methods](/index.php/Dm-crypt/Drive_preparation#dm-crypt_specific_methods "Dm-crypt/Drive preparation")

### Preparing the non-boot partitions

See [Dm-crypt/Device encryption#Encryption options for plain mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_plain_mode "Dm-crypt/Device encryption") for details.

Using the device `/dev/sd*X*`, with the twofish-xts cipher with a 512 bit key size and using a keyfile we have the following options for this scenario:

 `# cryptsetup --hash=sha512 --cipher=twofish-xts-plain64 --offset=0 --key-file=/dev/sd*Z* --key-size=512 open --type=plain /dev/sdX enc` 

Unlike encrypting with LUKS, the above command must be executed *in full* whenever the mapping needs to be re-established, so it is important to remember the cipher, hash and key file details.

We can now check a mapping entry has been made for `/dev/mapper/enc`:

```
# fdisk -l

```

Next, we setup [LVM](/index.php/LVM "LVM") logical volumes on the mapped device. See [LVM#Installing Arch Linux on LVM](/index.php/LVM#Installing_Arch_Linux_on_LVM "LVM") for further details:

```
# pvcreate /dev/mapper/enc
# vgcreate store /dev/mapper/enc
# lvcreate -L 20G store -n root
# lvcreate -L 10G store -n swap
# lvcreate -l 100%FREE store -n home

```

We format and mount them and activate swap. See [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") for further details:

```
# mkfs.ext4 /dev/store/root
# mkfs.ext4 /dev/store/home
# mount /dev/store/root /mnt
# mkdir /mnt/home
# mount /dev/store/home /mnt/home
# mkswap /dev/store/swap
# swapon /dev/store/swap

```

### Preparing the boot partition

The `/boot` partition can be installed on the standard vfat partition of a USB stick, if required. But if manual partitioning is needed, then a small 200MB partition is all that is required. Create the partition using a [partitioning tool](/index.php/Partitioning#Partitioning_tools "Partitioning") of your choice.

We choose a non-journalling file system to preserve the flash memory of the `/boot` partition, if not already formatted as vfat:

```
# mkfs.ext2 /dev/sd*Y*1
# mkdir /mnt/boot
# mount /dev/sd*Y*1 /mnt/boot

```

### Configuring mkinitcpio

Add the `keyboard`, `encrypt` and `lvm2` hooks to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

 `etc/mkinitcpio.conf`  `HOOKS=(... **keyboard** **keymap** block **encrypt** **lvm2** ... filesystems ...)` 

See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details and other hooks that you may need.

### Configuring the boot loader

In order to boot the encrypted root partition, the following kernel parameters need to be set by the boot loader:

```
cryptdevice=/dev/sd*X*:enc cryptkey=/dev/sd*Z*:0:512 crypto=sha512:twofish-xts-plain64:512:0:

```

**Note:** If using sd-encrypt instead of encrypt, respectively use the options specified in *systemd-cryptsetup-generator(8)*.

See [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") for details and other parameters that you may need.

**Tip:** If using GRUB, you can install it on the same USB as the `/boot` partition with:
```
# grub-install --recheck /dev/sd*Y*

```

### Post-installation

You may wish to remove the USB sticks after booting. Since the `/boot` partition is not usually needed, the `noauto` option can be added to the relevant line in `/etc/fstab`:

 `/etc/fstab` 
```
# /dev/sd*Yn*
/dev/sd*Yn* /boot ext2 **noauto**,rw,noatime 0 2

```

However, when an update to the kernel or bootloader is required, the `/boot` partition must be present and mounted. As the entry in `fstab` already exists, it can be mounted simply with:

```
# mount /boot

```

## Encrypted boot partition (GRUB)

This setup utilizes the same partition layout and configuration for the system's root partition as the previous [#LVM on LUKS](#LVM_on_LUKS) section, with two distinct differences:

1.  The setup is performed for an [UEFI](/index.php/UEFI "UEFI") system and
2.  A special feature of the [GRUB](/index.php/GRUB "GRUB") bootloader is used to additionally encrypt the boot partition `/boot`. See also [GRUB#Boot partition](/index.php/GRUB#Boot_partition "GRUB").

The disk layout in this example is:

```
+---------------+----------------+----------------+----------------+----------------+
|ESP partition: |Boot partition: |Volume 1:       |Volume 2:       |Volume 3:       |
|               |                |                |                |                |
|/boot/efi      |/boot           |root            |swap            |home            |
|               |                |                |                |                |
|               |                |/dev/store/root |/dev/store/swap |/dev/store/home |
|/dev/sdaX      |/dev/sdaY       +----------------+----------------+----------------+
|**un**encrypted    |LUKS encrypted  |/dev/sdaZ encrypted using LVM on LUKS             |
+---------------+----------------+--------------------------------------------------+

```

**Tip:** All scenarios are intended as examples. It is, of course, possible to apply both of the two above distinct installation steps with the other scenarios as well. See also the variants linked in [#LVM on LUKS](#LVM_on_LUKS).

**Note:** You can use `cryptboot` script from [cryptboot](https://aur.archlinux.org/packages/cryptboot/) package for simplified encrypted boot management (mounting, unmounting, upgrading packages) and as a defense against [Evil Maid](https://www.schneier.com/blog/archives/2009/10/evil_maid_attac.html) attacks with [UEFI Secure Boot](/index.php/Secure_Boot#Using_your_own_keys "Secure Boot"). For more informations and limitations see [cryptboot project](https://github.com/xmikos/cryptboot) page.

### Preparing the disk

Prior to creating any partitions, you should inform yourself about the importance and methods to securely erase the disk, described in [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

Create an [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") with an appropriate size, it will later be mounted at `/boot/efi`.

Create a partition to be mounted at `/boot` of type `8300` with a size of 100 MB or more.

**Tip:** When using the [GRUB](/index.php/GRUB "GRUB") bootloader together with a BIOS/[GPT](/index.php/GPT "GPT"), create a BIOS Boot Partition as explained in [GRUB#BIOS systems](/index.php/GRUB#BIOS_systems "GRUB") instead of the ESP.

Create a partition of type `8E00`, which will later contain the encrypted container.

Create the LUKS encrypted container at the "system" partition.

```
# cryptsetup luksFormat --type luks2 /dev/*sdaZ*

```

For more information about the available cryptsetup options see the [LUKS encryption options](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") prior to above command.

Your partition layout should look similar to this:

 `# gdisk /dev/sda` 
```
Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048         1050623   512.0 MiB   EF00  EFI System
   2         1050624         1460223   200.0 MiB   8300  Linux filesystem
   3         1460224        41943006   19.3 GiB    8E00  Linux LVM

```

Open the container:

```
# cryptsetup open /dev/*sdaZ* lvm

```

The decrypted container is now available at `/dev/mapper/lvm`.

### Preparing the logical volumes

The LVM logical volumes of this example follow the exact layout as the previous scenario. Therefore, please follow [Preparing the logical volumes](#Preparing_the_logical_volumes) above or adjust as required.

### Preparing the boot partition

The bootloader loads the kernel, [initramfs](/index.php/Initramfs "Initramfs"), and its own configuration files from the `/boot` directory.

First, create the LUKS container where the files will be located and installed into:

```
# cryptsetup luksFormat /dev/sda*Y*

```

Next, open it:

```
# cryptsetup open /dev/sda*Y* cryptboot

```

Create a filesystem on the partition intended for `/boot`. Any filesystem that can be read by the bootloader is eligible:

```
# mkfs.ext2 /dev/mapper/*cryptboot*

```

Create the directory `/mnt/boot`:

```
# mkdir /mnt/boot

```

Mount the partition to `/mnt/boot`:

```
# mount /dev/mapper/*cryptboot* /mnt/boot

```

Create a mountpoint for the [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") at `/boot/efi` for compatibility with `grub-install` and mount it:

```
# mkdir /mnt/boot/efi
# mount /dev/*sdaX* /mnt/boot/efi

```

At this point, you should have the following partitions and logical volumes inside of `/mnt`:

 `$ lsblk` 
```
NAME              	  MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT
sda                       8:0      0   200G  0 disk
├─sda1                    8:1      0   512M  0 part  /boot/efi
├─sda2                    8:2      0   200M  0 part
│ └─boot		  254:0    0   198M  0 crypt /boot
└─sda3                    8:3      0   100G  0 part
  └─lvm                   254:1    0   100G  0 crypt
    ├─MyStorage-swapvol   254:2    0     8G  0 lvm   [SWAP]
    ├─MyStorage-rootvol   254:3    0    15G  0 lvm   /
    └─MyStorage-homevol   254:4    0    77G  0 lvm   /home

```

Afterwards continue with the installation procedure up to the mkinitcpio step.

### Configuring mkinitcpio

Add the `keyboard`, `encrypt` and `lvm2` hooks to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

 `/etc/mkinitcpio.conf`  `HOOKS=(... **keyboard** **keymap** block **encrypt** **lvm2** ... filesystems ...)` 

See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details and other hooks that you may need.

### Configuring the boot loader

Configure GRUB to recognize the LUKS encrypted `/boot` partition and unlock the encrypted root partition at boot:

 `/etc/default/grub` 
```
GRUB_CMDLINE_LINUX="... cryptdevice=UUID=*<device-UUID>*:lvm ..."
GRUB_ENABLE_CRYPTODISK=y
```

See [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") and [GRUB#Boot partition](/index.php/GRUB#Boot_partition "GRUB") for details. The `*<device-UUID>*` refers to the UUID of `/dev/sdaZ` (the partition which holds the lvm containing the root filesystem). See [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

Generate GRUB's [configuration](/index.php/GRUB#Generate_the_main_configuration_file "GRUB") file and [install](/index.php/GRUB#Installation_2 "GRUB") to the mounted ESP:

```
# grub-mkconfig -o /boot/grub/grub.cfg
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=grub --recheck

```

If this finished without errors, GRUB should prompt for the passphrase to unlock the `/boot` partition after the next reboot.

### Configuring fstab and crypttab

This section deals with extra configuration to let the system **mount** the encrypted `/boot`.

While GRUB asks for a passphrase to unlock the encrypted `/boot` after above instructions, the partition unlock is not passed on to the initramfs. Hence, `/boot` will not be available after the system has re-/booted, because the `encrypt` hook only unlocks the system's root.

If you used the *genfstab* script during installation, it will have generated `/etc/fstab` entries for the `/boot` and `/boot/efi` mount points already, but the system will fail to find the generated device mapper for the boot partition. To make it available, add it to [crypttab](/index.php/Crypttab "Crypttab"). For example:

 `/etc/crypttab` 
```
cryptboot  /dev/sdaY      none        luks

```

will make the system ask for the passphrase again (i.e. you have to enter it twice at boot: once for GRUB and once for systemd init). To avoid the double entry for unlocking `/boot`, follow the instructions at [Dm-crypt/Device encryption#Keyfiles](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") to:

1.  Create a [randomtext keyfile](/index.php/Dm-crypt/Device_encryption#Storing_the_keyfile_on_a_filesystem "Dm-crypt/Device encryption"),
2.  Add the keyfile to the (`/dev/sdaY`) [boot partition's LUKS header](/index.php/Dm-crypt/Device_encryption#Configuring_LUKS_to_make_use_of_the_keyfile "Dm-crypt/Device encryption") and
3.  Check the `/etc/fstab` entry and add the `/etc/crypttab` line to [unlock it automatically at boot](/index.php/Dm-crypt/Device_encryption#Unlocking_a_secondary_partition_at_boot "Dm-crypt/Device encryption").

If for some reason the keyfile fails to unlock the boot partition, systemd will fallback to ask for a passphrase to unlock and, in case that is correct, continue booting.

**Tip:** Optional post-installation steps:

*   It may be worth considering to add the GRUB bootloader to the ignore list of `/etc/pacman.conf` in order to take particular control of when the bootloader (which includes its own encryption modules) is updated.
*   If you want to encrypt the `/boot` partition to protect against offline tampering threats, the [mkinitcpio-chkcryptoboot](/index.php/Dm-crypt/Specialties#mkinitcpio-chkcryptoboot "Dm-crypt/Specialties") hook has been contributed to help.

## Btrfs subvolumes with swap

The following example creates a full system encryption with LUKS using [Btrfs](/index.php/Btrfs "Btrfs") subvolumes to [simulate partitions](/index.php/Btrfs#Mounting_subvolumes "Btrfs").

If using UEFI, an [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") (ESP) is required. `/boot` itself may reside on `/` and be encrypted; however, the ESP itself cannot be encrypted. In this example layout, the ESP is `/dev/sda*Y*` and is mounted at `/boot/efi`. `/boot` itself is located on the system partition, `/dev/sda*X*`.

Since `/boot` resides on the encrypted `/`, [GRUB](/index.php/GRUB "GRUB") must be used as the bootloader because only GRUB can load modules necessary to decrypt `/boot` (e.g., crypto.mod, cryptodisk.mod and luks.mod) [[1]](http://www.pavelkogan.com/2014/05/23/luks-full-disk-encryption/).

Additionally an optional plain-encrypted [swap](/index.php/Swap "Swap") partition is shown.

**Warning:** Do not use a [swap file](/index.php/Swap_file "Swap file") instead of a separate partition, because this may result in data loss. See [Btrfs#Swap file](/index.php/Btrfs#Swap_file "Btrfs").

```
+--------------------------+--------------------------+--------------------------+
|ESP                       |System partition          |Swap partition            |
|**un**encrypted               |LUKS-encrypted            |plain-encrypted           |
|                          |                          |                          |
|/boot/efi                 |/                         |                          |
|/dev/sda*Y*                 |/dev/sda*X*                 |/dev/sda*Z*                 |
|--------------------------+--------------------------+--------------------------+

```

### Preparing the disk

**Note:** It is not possible to use btrfs partitioning as described in [Btrfs#Partitionless Btrfs disk](/index.php/Btrfs#Partitionless_Btrfs_disk "Btrfs") when using LUKS. Traditional partitioning must be used, even if it is just to create one partition.

Prior to creating any partitions, you should inform yourself about the importance and methods to securely erase the disk, described in [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation"). If you are using [UEFI](/index.php/UEFI "UEFI") create an [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") with an appropriate size. It will later be mounted at `/boot/efi`. If you are going to create an encrypted swap partition, create the partition for it, but do **not** mark it as swap, since plain *dm-crypt* will be used with the partition.

Create the needed partitions, at least one for `/` (e.g. `/dev/sda*X*`). See the [Partitioning](/index.php/Partitioning "Partitioning") article.

### Preparing the system partition

#### Create LUKS container

Follow [dm-crypt/Device encryption#Encrypting devices with LUKS mode](/index.php/Dm-crypt/Device_encryption#Encrypting_devices_with_LUKS_mode "Dm-crypt/Device encryption") to setup `/dev/sda*X*` for LUKS. See the [Dm-crypt/Device encryption#Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") before doing so for a list of encryption options.

#### Unlock LUKS container

Now follow [Dm-crypt/Device encryption#Unlocking/Mapping LUKS partitions with the device mapper](/index.php/Dm-crypt/Device_encryption#Unlocking.2FMapping_LUKS_partitions_with_the_device_mapper "Dm-crypt/Device encryption") to unlock the LUKS container and map it.

#### Format mapped device

Proceed to format the mapped device as described in [Btrfs#File system on a single device](/index.php/Btrfs#File_system_on_a_single_device "Btrfs"), where `*/dev/partition*` is the name of the mapped device (i.e., `cryptroot`) and **not** `/dev/sda*X*`.

#### Mount mapped device

Finally, [mount](/index.php/Mount "Mount") the now-formatted mapped device (i.e., `/dev/mapper/cryptroot`) to `/mnt`.

**Tip:** You may want to use the `compress=lzo` mount option. See [Btrfs#Compression](/index.php/Btrfs#Compression "Btrfs") for more information.

### Creating btrfs subvolumes

#### Layout

[Subvolumes](/index.php/Btrfs#Subvolumes "Btrfs") will be used to simulate partitions, but other (nested) subvolumes will also be created. Here is a partial representation of what the following example will generate:

```
subvolid=5 (/dev/sda*X*)
   |
   ├── @ (mounted as /)
   |       |
   |       ├── /bin (directory)
   |       |
   |       ├── /home (mounted @home subvolume)
   |       |
   |       ├── /usr (directory)
   |       |
   |       ├── /.snapshots (mounted @snapshots subvolume)
   |       |
   |       ├── /var/cache/pacman/pkg (nested subvolume)
   |       |
   |       ├── ... (other directories and nested subvolumes)
   |
   ├── @snapshots (mounted as /.snapshots)
   |
   ├── @home (mounted as /home)
   |
   └── @... (additional subvolumes you wish to use as mount points)

```

This section follows the [Snapper#Suggested filesystem layout](/index.php/Snapper#Suggested_filesystem_layout "Snapper"), which is most useful when used with [Snapper](/index.php/Snapper "Snapper"). You should also consult [Btrfs Wiki SysadminGuide#Layout](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Layout).

#### Create top-level subvolumes

Here we are using the convention of prefixing `@` to subvolume names that will be used as mount points, and `@` will be the subvolume that is mounted as `/`.

Following the [Btrfs#Creating a subvolume](/index.php/Btrfs#Creating_a_subvolume "Btrfs") article, create subvolumes at `/mnt/@`, `/mnt/@snapshots`, and `/mnt/@home`.

Create any additional subvolumes you wish to use as mount points now.

#### Mount top-level subvolumes

Unmount the system partition at `/mnt`.

Now mount the newly created `@` subvolume which will serve as `/` to `/mnt` using the `subvol=` mount option. Assuming the mapped device is named `cryptroot`, the command would look like:

```
# mount -o compress=lzo,subvol=@ /dev/mapper/cryptroot /mnt

```

See [Btrfs#Mounting subvolumes](/index.php/Btrfs#Mounting_subvolumes "Btrfs") for more details.

Also mount the other subvolumes to their respective mount points: `@home` to `/mnt/home` and `@snapshots` to `/mnt/.snapshots`.

#### Create nested subvolumes

Create any subvolumes you do **not** want to have snapshots of when taking a snapshot of `/`. For example, you probably do not want to take snapshots of `/var/cache/pacman/pkg`. These subvolumes will be nested under the `@` subvolume, but just as easily could have been created earlier at the same level as `@` according to your preference.

Since the `@` subvolume is mounted at `/mnt` you will need to [create a subvolume](/index.php/Create_a_subvolume "Create a subvolume") at `/mnt/var/cache/pacman/pkg` for this example. You may have to create any parent directories first.

Other directories you may wish to do this with are `/var/abs`, `/var/tmp`, and `/srv`.

#### Mount ESP

If you prepared an EFI system partition earlier, create its mount point and mount it now.

**Note:** Btrfs snapshots will exclude `/boot/efi`, since it is not a btrfs file system.

At the [pacstrap](/index.php/Installation_guide#Install_the_base_packages "Installation guide") installation step, the [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) must be installed in addition to the base group.

### Configuring mkinitcpio

#### Create keyfile

In order for GRUB to open the LUKS partition without having the user enter his passphrase twice, we will use a keyfile embedded in the initramfs. Follow [Dm-crypt/Device encryption#With a keyfile embedded in the initramfs](/index.php/Dm-crypt/Device_encryption#With_a_keyfile_embedded_in_the_initramfs "Dm-crypt/Device encryption") making sure to add the key to `/dev/sda*X*` at the *luksAddKey* step.

#### Edit mkinitcpio.conf

After creating, adding, and embedding the key as described above, add the `encrypt` hook to [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") as well as any other hooks you require. See [Dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for detailed information. Be sure to regenerate the initial ramdisk when finished.

**Tip:** You may want to add `BINARIES=(/usr/bin/btrfs)` to your `mkinitcpio.conf`. See the [Btrfs#Corruption recovery](/index.php/Btrfs#Corruption_recovery "Btrfs") article.

### Configuring the boot loader

Install [GRUB](/index.php/GRUB "GRUB") to `/dev/sda`. Then, edit `/etc/default/grub` as instructed in the [GRUB#Encryption](/index.php/GRUB#Encryption "GRUB") article, following both the instructions for an encrypted root and boot partition. Finally, generate the GRUB configuration file.

### Configuring swap

If you created a partition to be used for encrypted swap, now is the time to configure it. Follow the instructions at [Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

After completing this step, continue configuring your system as normal according to the [installation guide](/index.php/Installation_guide#Reboot "Installation guide").