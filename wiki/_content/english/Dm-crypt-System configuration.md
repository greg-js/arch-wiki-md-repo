Back to [Dm-crypt](/index.php/Dm-crypt "Dm-crypt").

**Tip:** If in need to remotely unlock root or other early-boot filesystems (headless machine, distant servers...), follow the specific instructions from [Dm-crypt/Specialties#Remote unlocking of encrypted root](/index.php/Dm-crypt/Specialties#Remote_unlocking_of_the_root_.28or_other.29_partition "Dm-crypt/Specialties").

## Contents

*   [1 mkinitcpio](#mkinitcpio)
*   [2 Boot loader](#Boot_loader)
    *   [2.1 cryptdevice](#cryptdevice)
    *   [2.2 root](#root)
    *   [2.3 resume](#resume)
    *   [2.4 cryptkey](#cryptkey)
    *   [2.5 crypto](#crypto)
*   [3 crypttab](#crypttab)
    *   [3.1 Mounting at boot time](#Mounting_at_boot_time)

## mkinitcpio

When encrypting a system it is necessary to regenerate the initial ramdisk after properly configuring [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"). Depending on the particular scenarios, a subset of the following hooks will have to be enabled:

*   `encrypt`: always needed when encrypting the root partition, or a partition that needs to be mounted *before* root. It is not needed in all the other cases, as system initialization scripts like `/etc/crypttab` take care of unlocking other encrypted partitions.
*   `shutdown`: recommended before *mkinitcpio 0.16* to ensure controlled unmounting during system shutdown. It is still functional, but not deemed necessary [anymore](https://mailman.archlinux.org/pipermail/arch-dev-public/2013-December/025742.html).
*   `keymap`: provides support for foreign keymaps for typing encryption passwords; it must come *before* the `encrypt` hook.
*   `keyboard`: needed to make USB keyboards work in early userspace.
    *   `usbinput`: deprecated, but can be given a try in case `keyboard` does not work.

Other hooks needed should be clear from other manual steps followed during the installation of the system.

## Boot loader

In order to enable booting an encrypted root partition, a subset of the following kernel parameters need to be set: see [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for instructions specific to your [boot loader](/index.php/Boot_loader "Boot loader").

For example using [GRUB](/index.php/GRUB#Root_partition "GRUB") the relevant parameters are best added to `/etc/default/grub` before generating the boot configuration. See also [GRUB#Warning when installing in chroot](/index.php/GRUB#Warning_when_installing_in_chroot "GRUB") as another point to be aware of when installing the GRUB loader.

### cryptdevice

This parameter will make the system prompt for the passphrase to unlock the device containing the encrypted root on a cold boot. It is parsed by the `encrypt` hook to identify which device contains the encrypted system:

```
cryptdevice=*device*:*dmname*

```

*   `*device*` is the path to the raw encrypted device. Usage of [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") is advisable.
*   `*dmname*` is the **d**evice-**m**apper name given to the device after decryption, which will be available as `/dev/mapper/*dmname*`.
*   If a LVM contains the [encrypted root](/index.php/Dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM "Dm-crypt/Encrypting an entire system"), the LVM gets activated first and the volume group containing the logical volume of the encrypted root serves as *device*. It is then followed by the respective volume group to be mapped to root. The parameter follows the form of `cryptdevice=*/dev/vgname/lvname*:*dmname*`.

### root

The `root=` parameter specifies the `*device*` of the actual (decrypted) root file system:

```
root=*device*

```

*   If the file system is formatted directly on the decrypted device file this will be `/dev/mapper/*dmname*`.
*   If a LVM gets activated first and contains an [encrypted logical rootvolume](/index.php/Dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM "Dm-crypt/Encrypting an entire system"), the above form applies as well.
*   If the root file system is contained in a logical volume of a fully [encrypted LVM](/index.php/Encrypted_LVM "Encrypted LVM"), the device mapper for it will be in the general form of `root=/dev/mapper/*volumegroup*-*logicalvolume*`.

**Tip:** This parameter is not needed to be specified manually when using [GRUB](/index.php/GRUB "GRUB"). Executing *grub-mkconfig* is meant to determine the correct UUID of the decrypted root filesystem and specify it in the generated `grub.cfg` automatically.

### resume

```
resume=*device*

```

*   `*device*` is the device file of the decrypted (swap) filesystem used for suspend2disk. If swap is on a separate partition, it will be in the form of `/dev/mapper/swap`. See also [Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

### cryptkey

This parameter is required by the `*encrypt*` hook for reading a keyfile to unlock the `*cryptdevice*`. It can have three parameter sets, depending on whether the keyfile exists as a file in a particular device, a bitstream starting on a specific location, or a file in the initramfs.

For a file in a device the format is:

```
cryptkey=*device*:*fstype*:*path*

```

*   `*device*` is the raw block device where the key exists.
*   `*fstype*` is the filesystem type of `*device*` (or auto).
*   `*path*` is the absolute path of the keyfile within the device.

Example: `cryptkey=/dev/usbstick:vfat:/secretkey`

For a bitstream on a device the key's location is specified with the following:

```
cryptkey=*device*:*offset*:*size* 

```

Example: `cryptkey=/dev/sdZ:0:512` reads a 512 bit keyfile starting at the beginning of the device.

For a file [included](/index.php/Mkinitcpio#BINARIES_and_FILES "Mkinitcpio") in the initramfs the format is[[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/encrypt_hook?h=packages/cryptsetup#n14):

```
cryptkey=rootfs:*path*

```

Example: `cryptkey=rootfs:/secretkey`

Also note that if `cryptkey` is not specified, it defaults to `/crypto_keyfile.bin` (in the initramfs).[[2]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/encrypt_hook?h=packages/cryptsetup#n8)

See also [Dm-crypt/Device encryption#Keyfiles](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption").

### crypto

This parameter is specific to pass *dm-crypt* plain mode options to the *encrypt* hook.

It takes the form

 `crypto=<hash>:<cipher>:<keysize>:<offset>:<skip>` 

The arguments relate directly to the *cryptsetup* options. See [Dm-crypt/Device encryption#Encryption options for plain mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_plain_mode "Dm-crypt/Device encryption").

For a disk encrypted with just *plain* default options, the `crypto` arguments must be specified, but each entry can be left blank:

 `crypto=::::` 

A specific example of arguments is

 `crypto=sha512:twofish-xts-plain64:512:0:` 

## crypttab

The `/etc/crypttab` (encrypted device table) file is similar to the [fstab](/index.php/Fstab "Fstab") file and contains a list of encrypted devices to be unlocked during system boot up. This file can be used for automatically mounting encrypted swap devices or secondary file systems.

`crypttab` is read *before* `fstab`, so that dm-crypt containers can be unlocked before the file system inside is mounted. Note that `crypttab` is read *after* the system has booted up, therefore it is not a replacement for unlocking encrypted partitions by using [mkinitcpio](#mkinitcpio) hooks and [boot loader options](#Boot_loader) as in the case of [encrypting the root partition](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system"). `crypttab` processing at boot time is made by the `systemd-cryptsetup-generator` automatically.

See the `crypttab` [man page](http://linux.die.net/man/5/crypttab) for details, read below for some examples, and the [#Mounting at boot time](#Mounting_at_boot_time) section for instructions on how to use UUIDs to mount an encrypted device.

**Warning:** There are issues with [systemd](/index.php/Systemd "Systemd") when processing `crypttab` entries for *dm-crypt* [plain mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_plain_mode "Dm-crypt/Device encryption") (`--type plain`) devices:

*   For `--type plain` devices with a keyfile, it is necessary to add the `hash=plain` option to crypttab due to a [systemd incompatibility](https://bugs.freedesktop.org/show_bug.cgi?id=52630). **Do not** use `systemd-cryptsetup` manually for device creation to work around it.

*   It may be further required to add the `plain` option explicitly to force `systemd-cryptsetup` to recognize a `--type plain`) device at boot. [GitHub issue in question.](https://github.com/systemd/systemd/issues/442)

 `/etc/crypttab` 
```
 # Example crypttab file. Fields are: name, underlying device, passphrase, cryptsetup options.

 # Mount /dev/lvm/swap re-encrypting it with a fresh key each reboot
 swap	/dev/lvm/swap	/dev/urandom	swap,cipher=aes-xts-plain64,size=256

 # Mount /dev/lvm/tmp as /dev/mapper/tmp using plain dm-crypt with a random passphrase, making its contents unrecoverable after it is dismounted.
 tmp	/dev/lvm/tmp	/dev/urandom	tmp,cipher=aes-xts-plain64,size=256 

 # Mount /dev/lvm/home as /dev/mapper/home using LUKS, and prompt for the passphrase at boot time.
 home   /dev/lvm/home

 # Mount /dev/sdb1 as /dev/mapper/backup using LUKS, with a passphrase stored in a file.
 backup /dev/sdb1       /home/alice/backup.key

```

### Mounting at boot time

If you want to mount an encrypted drive at boot time, enter the device's UUID in `/etc/crypttab`. You get the UUID (partition) by using the command `lsblk -f` and adding it to `crypttab` in the form:

 `/etc/crypttab` 
```
 externaldrive         UUID=2f9a8428-ac69-478a-88a2-4aa458565431        none    luks,timeout=180

```

The first parameter is your preferred device mapper's name for the encrypted drive. The option `none` will trigger a prompt during boot to type the passphrase for unlocking the partition. The `timeout` option defines a timeout in seconds for entering the decryption password during boot.

A [keyfile](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") can also be set up and referenced instead of `none`. This results in an automatic unlocking, if the keyfile is accessible during boot. Since LUKS offers the option to have multiple keys, the chosen option can also be changed later.

Use the device mapper's name you've defined in `/etc/crypttab` in `/etc/fstab` as follows:

 `/etc/fstab` 
```
 /dev/mapper/externaldrive      /mnt/backup               ext4    defaults,errors=remount-ro  0  2

```

Since `/dev/mapper/externaldrive` already is the result of a unique partition mapping, there is no need to specify an UUID for it. In any case, the mapper with the filesystem will have a different UUID than the partition it is encrypted in.

**Tip:** The systemd generators also automatically process stacked block devices at boot.

For example, you can create a [RAID](/index.php/RAID "RAID") setup, use cryptsetup to encrypt it and create an [LVM](/index.php/LVM "LVM") logical volume with respective filesystem inside the encrypted block device. A resulting:

 `# lsblk -f` 
```
─sdXX                  linux_raid_member    
│ └─md0                 crypto_LUKS   
│   └─cryptedbackup     LVM2_member 
│     └─vgraid-lvraid   ext4              /mnt/backup
└─sdYY                  linux_raid_member    
  └─md0                 crypto_LUKS       
    └─cryptedbackup     LVM2_member 
      └─vgraid-lvraid   ext4              /mnt/backup

```

will ask for the passphrase and mount automatically at boot.

Since `/etc/crypttab` processing applies to non-root mounts only, there is no need to add additional mkinitcpio hooks/configuration, given you specify the correct corresponding crypttab (e.g. UUID for the `crypto_LUKS` device) and fstab (`/dev/mapper/vgraid-lvraid`) entries.