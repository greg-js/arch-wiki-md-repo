The following are examples of encrypting a secondary, i.e. non-root, filesystem with dm-crypt.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Overview](#Overview)
*   [2 Partition](#Partition)
    *   [2.1 Manual mounting and unmounting](#Manual_mounting_and_unmounting)
    *   [2.2 Automated unlocking and mounting](#Automated_unlocking_and_mounting)
        *   [2.2.1 At boot time](#At_boot_time)
        *   [2.2.2 On user login](#On_user_login)
*   [3 Loop device](#Loop_device)
    *   [3.1 Without losetup](#Without_losetup)
    *   [3.2 Using losetup](#Using_losetup)
        *   [3.2.1 Manual mounting and unmounting](#Manual_mounting_and_unmounting_2)

## Overview

Encrypting a secondary filesystem usually protects only sensitive data, while leaving the operating system and program files unencrypted. This is useful for encrypting an external medium, such as a USB drive, so that it can be moved to different computers securely. One might also choose to encrypt sets of data separately according to who has access to it.

Because dm-crypt is a [block-level](/index.php/Disk_encryption#Block_device_encryption "Disk encryption") encryption layer, it only encrypts full devices, [full partitions](#Partition) and [loop devices](#Loop_device). To encrypt individual files requires a filesystem-level encryption layer, such as [eCryptfs](/index.php/ECryptfs "ECryptfs") or [EncFS](/index.php/EncFS "EncFS"). See [Disk encryption](/index.php/Disk_encryption "Disk encryption") for general information about securing private data.

## Partition

This example covers the encryption of the `/home` partition, but it can be applied to any other comparable non-root partition containing user data.

**Tip:** You can either have a single user's `/home` directory on a partition, or create a common partition for all user's `/home` directories.

First make sure the partition is empty (has no file system attached to it). Delete the partition and create an empty one if it has a file system. Then prepare the partition by securely erasing it, see [Dm-crypt/Drive preparation#Secure erasure of the hard disk drive](/index.php/Dm-crypt/Drive_preparation#Secure_erasure_of_the_hard_disk_drive "Dm-crypt/Drive preparation").

Create the partition which will contain the encrypted container.

Then setup the LUKS header with:

```
# cryptsetup *options* luksFormat *device*

```

Replace `*device*` with the previously created partition. See [Dm-crypt/Device encryption#Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") for details like the available `*options*`.

To gain access to the encrypted partition, unlock it with the device mapper, using:

```
# cryptsetup open *device* *name*

```

After unlocking the partition, it will be available at `/dev/mapper/*name*`. Now create a [file system](/index.php/File_system "File system") of your choice with:

```
# mkfs.*fstype* /dev/mapper/*name*

```

Mount the file system to `/home`, or if it should be accessible to only one user to `/home/*username*`, see [#Manual mounting and unmounting](#Manual_mounting_and_unmounting).

**Tip:** Unmount and mount once to verify that the mapping is working as intended.

### Manual mounting and unmounting

To mount the partition:

```
# cryptsetup open *device* *name*
# mount -t *fstype* /dev/mapper/*name* /mnt/home

```

To unmount it:

```
# umount /mnt/home
# cryptsetup close *name*

```

**Tip:** [GVFS](/index.php/GVFS "GVFS") can also mount encrypted partitions. One can use a file manager with gvfs support (e.g. [Thunar](/index.php/Thunar "Thunar")) to mount the partition, and a password dialog will pop-up. For other desktops, [zulucrypt](https://aur.archlinux.org/packages/zulucrypt/) also provides a GUI.

### Automated unlocking and mounting

There are three different solutions for automating the process of unlocking the partition and mounting its filesystem.

#### At boot time

Using the `/etc/crypttab` configuration file, unlocking happens at boot time by systemd's automatic parsing. This is the recommended solution if you want to use one common partition for all user's home partitions or automatically mount another encrypted block device.

See [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration") for references and [Dm-crypt/System configuration#Mounting at boot time](/index.php/Dm-crypt/System_configuration#Mounting_at_boot_time "Dm-crypt/System configuration") for an example set up.

#### On user login

Using *pam_exec* it is possible to unlock (*cryptsetup open*) the partition on user login: this is the recommended solution if you want to have a single user's home directory on a partition. See [dm-crypt/Mounting at login](/index.php/Dm-crypt/Mounting_at_login "Dm-crypt/Mounting at login").

Unlocking on user login is also possible with [pam_mount](/index.php/Pam_mount "Pam mount").

## Loop device

There are two methods for using a loop device as an encrypted container, one using `losetup` directly and one without.

### Without losetup

Using losetup directly can be avoided completely by doing the following [[1]](https://wiki.gentoo.org/wiki/Custom_Initramfs#Encrypted_keyfile):

```
$ dd if=/dev/urandom of=bigsecret.img bs=100M count=1 iflag=fullblock
$ cryptsetup luksFormat bigsecret.img

```

Before running `cryptsetup`, look at the [encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") and [ciphers and modes of operation](/index.php/Disk_encryption#Ciphers_and_modes_of_operation "Disk encryption") first to select your additional desired settings.

The instructions for opening the device and making the [file system](/index.php/File_system "File system") are the same as [#Partition](#Partition).

Creating a file smaller than the LUKS2 header (16 MiB) will give a `Requested offset is beyond real size of device bigsecret.img` error when trying to open the device.

Manual mounting and unmounting procedure is equivalent to [#Manual mounting and unmounting](#Manual_mounting_and_unmounting).

### Using losetup

A loop device enables to map a blockdevice to a file with the standard util-linux tool `losetup`. The file can then contain a filesystem, which can be used quite like any other filesystem. A lot of users know [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") as a tool to create encrypted containers. Just about the same functionality can be achieved with a loopback filesystem encrypted with LUKS and is shown in the following example.

First, start by creating an encrypted container, using an appropriate [random number generator](/index.php/Random_number_generator "Random number generator"):

```
$ dd if=/dev/urandom of=bigsecret.img bs=100M count=1 iflag=fullblock

```

This will create the file `bigsecret.img` with a size of 100 mebibytes.

**Note:** To avoid having to [resize](/index.php/Dm-crypt/Device_encryption#Loopback_filesystem "Dm-crypt/Device encryption") the container later on, make sure to make it larger than the total size of the files to be encrypted, in order to at least also host the associated metadata needed by the internal file system. If you are going to use LUKS mode, its metadata header alone requires up to 16 mebibytes.

Next create the device node `/dev/loop0`, so that we can mount/use our container:

```
# losetup /dev/loop0 bigsecret.img

```

**Note:** If it gives you the error `/dev/loop0: No such file or directory`, you need to first load the kernel module with `modprobe loop` as root. These days (Kernel 3.2) loop devices are created on demand. Ask for a new loop device with `losetup -f` as root.

From now on the procedure is the same as for [#Partition](#Partition), except for the fact that the container is already randomised and will not need another secure erasure.

**Tip:** Containers with *dm-crypt* can be very flexible. Have a look at the features and documentation of [Tomb](/index.php/Tomb "Tomb"). It provides a *dm-crypt* script wrapper for fast and flexible handling.

#### Manual mounting and unmounting

To unmount the container:

```
# umount /mnt/secret
# cryptsetup close secret
# losetup -d /dev/loop0

```

To mount the container again:

```
# losetup /dev/loop0 bigsecret.img
# cryptsetup open /dev/loop0 secret
# mount -t ext4 /dev/mapper/secret /mnt/secret

```