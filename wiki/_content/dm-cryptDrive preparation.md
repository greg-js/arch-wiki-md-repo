# dm-crypt/Drive preparation

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Back to [Dm-crypt](/index.php/Dm-crypt "Dm-crypt").

Before encrypting a drive, you should perform a secure erase of the disk by overwriting the entire drive with random data. To prevent cryptographic attacks or unwanted [file recovery](/index.php/File_recovery "File recovery"), this data is ideally indistinguishable from data later written by dm-crypt. For a more comprehensive discussion see [Disk encryption#Preparing the disk](/index.php/Disk_encryption#Preparing_the_disk "Disk encryption").

## Contents

*   [1 Secure erasure of the hard disk drive](#Secure_erasure_of_the_hard_disk_drive)
    *   [1.1 Generic methods](#Generic_methods)
    *   [1.2 dm-crypt specific methods](#dm-crypt_specific_methods)
        *   [1.2.1 dm-crypt wipe on an empty disk or partition](#dm-crypt_wipe_on_an_empty_disk_or_partition)
        *   [1.2.2 dm-crypt wipe free space after installation](#dm-crypt_wipe_free_space_after_installation)
        *   [1.2.3 Wipe LUKS header](#Wipe_LUKS_header)
*   [2 Partitioning](#Partitioning)
    *   [2.1 Physical partitions](#Physical_partitions)
    *   [2.2 Stacked block devices](#Stacked_block_devices)
    *   [2.3 Btrfs subvolumes](#Btrfs_subvolumes)
    *   [2.4 Boot partition (GRUB)](#Boot_partition_.28GRUB.29)

## Secure erasure of the hard disk drive

In deciding which method to use for secure erasure of a hard disk drive, remember that this needs only to be performed once for as long as the drive is used as an encrypted drive.

**Warning:** Make appropriate backups of valuable data prior to starting.

**Tip:** The process of filling an encrypted drive can take over a day to complete on a multi-terabyte disk. In order not to leave the machine unusable during the operation, it may be worth to do it from a system already installed on another drive, rather than from the live Arch installation system.

### Generic methods

For detailed instructions on how to erase and prepare a drive consult [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk").

### dm-crypt specific methods

The following two methods are specific for dm-crypt and are mentioned complementarily, because they are very fast and can be performed after a partition setup too.

The [cryptsetup FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects) mentions a very simple procedure to use an existing dm-crypt-volume to wipe all free space accessible on the underlying block device with random data by acting as a simple pseudorandom number generator. It is also claimed to protect against disclosure of usage patterns. That is because encrypted data is practically indistinguishable from random.

#### dm-crypt wipe on an empty disk or partition

First, create a temporary encrypted container on the partition (`sdXY`) or the full disk (`sdX`) you want to encrypt, e.g. using default encryption parameters and a random key via the `--key-file /dev/{u}random` option (see also [Random number generation](/index.php/Random_number_generation "Random number generation")):

```
# cryptsetup open --type plain /dev/sdXY container --key-file /dev/random

```

Second, check it exists

 `# fdisk -l` 

```
Disk /dev/mapper/container: 1000 MB, 1000277504 bytes
...
Disk /dev/mapper/container does not contain a valid partition table
```

Finally, wipe it with pseudorandom (because encrypted) data. A use of `if=/dev/urandom` is not required as the encryption cipher is used for randomness.

 `# dd if=/dev/zero of=/dev/mapper/container status=progress`  `dd: writing to ‘/dev/mapper/container’: No space left on device` 

**Tip:**

*   Using _dd_ with the `bs=` option, e.g. `bs=1M`, is frequently used to increase disk throughput of the operation.
*   If you want to perform a check of the operation, zero the partition before creating the wipe container. After the wipe command `blockdev --getsize64 _/dev/mapper/container_` can be used to get the exact container size as root. Now _od_ can be used to spotcheck whether the wipe overwrote the zeroed sectors, e.g. `od -j _containersize - blocksize_` to view the wipe completed to the end.

Now the next step is [#Partitioning](#Partitioning).

#### dm-crypt wipe free space after installation

If you did not have time for the wipe procedure before [installation](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system"), the same effect can be achieved once the encrypted system is booted and the filesystems mounted. However, consider if the concerned filesystem may have set up reserved space, e.g. for the root user, or another [disk quota](/index.php/Disk_quota "Disk quota") mechanism, that that may limit the wipe even when performed by the root user: some parts of the underlying block device might not get written to at all.

To execute the wipe, temporarily fill the remaining free space of the partition by writing to a file inside the encrypted container:

 `# dd if=/dev/zero of=/file/in/container status=progress`  `dd: writing to ‘/file/in/container’: No space left on device` 

Sync the cache to disk and then delete the file to reclaim the free space.

```
# sync
# rm /file/in/container

```

The above process has to be repeated for every partition blockdevice created and filesystem in it. For example, if you set-up [LVM on LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system"), the process has to be performed for every logical volume.

#### Wipe LUKS header

The partitions formatted with dm-crypt/LUKS contain a header with the cipher and crypt-options used, which is referred to `dm-mod` when opening the blockdevice. After the header the actual random data partition starts. Hence, when re-installing on an already randomised drive, or de-commissioning one (e.g. sale of PC, switch of drives, etc.) it _may_ be just enough to wipe the header of the partition, rather than overwriting the whole drive - which can be a lengthy process.

Wiping the LUKS header will delete the PBKDF2-encrypted (AES) master key, salts and so on.

**Note:** It is crucial to write to the LUKS encrypted partition (`/dev/sda**1**` in this example) and not directly to the disks device node. If you did set up encryption as a device-mapper layer on top of others, e.g. LVM on LUKS on RAID then write to RAID respectively.

A header with one single default 256 bit size keyslot is 1024KB in size. It is advised to also overwrite the first 4KB written by dm-crypt, so 1028KB have to be wiped. That is `1052672` Byte.

For zero offset use:

```
# head -c 1052672 /dev/urandom > /dev/sda1; sync

```

For 512 bit key length (e.g. for aes-xts-plain with 512 bit key) the header is 2MB.

If in doubt, just be generous and overwrite the first 10MB or so.

```
# dd if=/dev/urandom of=/dev/sda1 bs=512 count=20480

```

**Note:** With a backup-copy of the header data can get rescued but the filesystem was likely damaged as the first encrypted sectors were overwritten. See further sections on how to make a backup of the crucial header blocks.

When wiping the header with random data everything left on the device is encrypted data. An exception to this may occur for an SSD, because of cache blocks SSDs employ. In theory it may happen that the header was cached in these some time before and that copy may consequently be still available after wiping the original header. For strong security concerns, a secure ATA erase of the SSD should be done (procedure please see the cryptsetup [FAQ 5.19](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects)).

## Partitioning

This section only applies when encrypting an entire system. After the drive(s) has/have been securely overwritten, a proper partitioning scheme will have to be accurately chosen, taking into account the requirements of dm-crypt, and the effects that the various choices will have on the management of the resulting system.

It is important to note from now that in [almost](#Boot_partition_.28GRUB.29) every case there has to be a separate partition for `/boot` that must remain unencrypted, because the bootloader needs to access the `/boot` directory where it will load the initramfs/encryption modules needed to load the rest of the system (see [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") for details). If this raises security concerns, see [dm-crypt/Specialties#Securing the unencrypted boot partition](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties").

Another important factor to take into account is how the swap area and system suspension will be handled, see [dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

### Physical partitions

In the simplest case, the encrypted layers can be based directly on the physical partitions; see [Partitioning](/index.php/Partitioning "Partitioning") for the methods to create them. Just like in an unencrypted system, a root partition is sufficient, besides another for `/boot` as noted above. This method allows deciding which partitions to encrypt and which to leave unencrypted, and works the same regardless of the number of disks involved. It will also be possible to add or remove partitions in the future, but resizing a partition will be limited by the size of the disk that is hosting it. Finally note that separate passphrases or keys are required to open each encrypted partition, even though this can be automated during boot using the `crypttab` file, see [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration").

### Stacked block devices

If more flexibility is needed, though, dm-crypt can coexist with other stacked block devices like [LVM](/index.php/LVM "LVM") and [RAID](/index.php/RAID "RAID"). The encrypted containers can either reside below or on top of other stacked block devices:

*   If the LVM/RAID devices are created on top of the encrypted layer, it will be possible to add, remove and resize the file systems of the same encrypted partition liberally, and only one key or passphrase will be required for all of them. Since the encrypted layer resides on a physical partition, though, it will not be possible to exploit the ability of LVM and RAID to span multiple disks.
*   If the encrypted layer is created on top of LVM/RAID devices, it will still be possible to reorganize the file systems in the future, but with added complexity, since the encryption layers will have to be adjusted accordingly. Moreover, separate passphrases or keys will be required to open each encrypted device. This, however, is the only choice for systems that need encrypted file systems to span multiple disks.

### Btrfs subvolumes

[Btrfs](/index.php/Btrfs "Btrfs")'s built-in [subvolumes feature](/index.php/Btrfs#Sub-volumes "Btrfs") can be used with dm-crypt, fully replacing the need for LVM if no other file systems are required. However, note that an encrypted swap is not possible this way and swap files are [not supported](https://btrfs.wiki.kernel.org/index.php/FAQ#Does_btrfs_support_swap_files.3F) by btrfs up to now.

### Boot partition (GRUB)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** The GRUB bootloader's feature "early cryptodisks", allows for (a) an unlocking of a LUKS encrypted root partition to access the `/boot` mount point in it, or (b) an unlocking of a separate LUKS encrypted partition for `/boot`. Instructions to setup both should be added. Further, (c) the conversion of an existing unencrypted `/boot` partition to LUKS. (Discuss in [User_talk:Grazzolini](https://wiki.archlinux.org/index.php/User_talk:Grazzolini))

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dm-crypt/Drive_preparation&oldid=415900](https://wiki.archlinux.org/index.php?title=Dm-crypt/Drive_preparation&oldid=415900)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Encryption](/index.php/Category:Encryption "Category:Encryption")
*   [File systems](/index.php/Category:File_systems "Category:File systems")

Hidden category:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")