Related articles

*   [Disk encryption#Preparing the disk](/index.php/Disk_encryption#Preparing_the_disk "Disk encryption")
*   [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk")

Before encrypting a drive, it is recommended to perform a secure erase of the disk by overwriting the entire drive with random data. To prevent cryptographic attacks or unwanted [file recovery](/index.php/File_recovery "File recovery"), this data is ideally indistinguishable from data later written by dm-crypt. For a more comprehensive discussion see [Disk encryption#Preparing the disk](/index.php/Disk_encryption#Preparing_the_disk "Disk encryption").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

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
    *   [2.4 Boot partition (GRUB)](#Boot_partition_(GRUB))

## Secure erasure of the hard disk drive

In deciding which method to use for secure erasure of a hard disk drive, remember that this needs only to be performed once for as long as the drive is used as an encrypted drive.

**Warning:** Make appropriate backups of valuable data prior to starting!

**Note:** When wiping large amount of data, the process will take several hours to several days to complete.

**Tip:**

*   The process of filling an encrypted drive can take over a day to complete on a multi-terabyte disk. In order not to leave the machine unusable during the operation, it may be worth to do it from a system already installed on another drive, rather than from the live Arch installation system.
*   For [SSDs](/index.php/SSD "SSD"), as a best effort to minimize [flash memory](/index.php/Securely_wipe_disk#Flash_memory "Securely wipe disk") cache artifacts, consider performing a [SSD memory cell clearing](/index.php/SSD_memory_cell_clearing "SSD memory cell clearing") *prior* to instructions below.

### Generic methods

For detailed instructions on how to erase and prepare a drive consult [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk").

### dm-crypt specific methods

The following two methods are specific for dm-crypt and are mentioned because they are very fast and can be performed after a partition setup too.

The [cryptsetup FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#2-setup) (item 2.19 "*How can I wipe a device with crypto-grade randomness?*") mentions a very simple procedure to use an existing dm-crypt-volume to wipe all free space accessible on the underlying block device with random data by acting as a simple pseudorandom number generator. It is also claimed to protect against disclosure of usage patterns. That is because encrypted data is practically indistinguishable from random.

#### dm-crypt wipe on an empty disk or partition

First, create a temporary encrypted container on the partition (using the form `sdXY`) or complete device (using the form `sdX`) to be encrypted:

```
# cryptsetup open --type plain -d /dev/urandom /dev/<block-device> to_be_wiped

```

You can verify that it exists:

 `# lsblk` 
```
NAME          MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
sda             8:0    0  1.8T  0 disk
└─to_be_wiped 252:0    0  1.8T  0 crypt

```

Wipe the container with zeros. A use of `if=/dev/urandom` is not required as the encryption cipher is used for randomness.

 `# dd if=/dev/zero of=/dev/mapper/to_be_wiped status=progress`  `dd: writing to ‘/dev/mapper/to_be_wiped’: No space left on device` 
**Tip:**

*   Using *dd* with the `bs=` option, e.g. `bs=1M`, is frequently used to increase disk throughput of the operation.
*   To perform a check of the operation, zero the partition before creating the wipe container. After the wipe command `blockdev --getsize64 */dev/mapper/container*` can be used to get the exact container size as root. Now *od* can be used to spotcheck whether the wipe overwrote the zeroed sectors, e.g. `od -j *containersize - blocksize*` to view the wipe completed to the end.

Finally, close the temporary container:

```
# cryptsetup close to_be_wiped

```

When encrypting an entire system, the next step is [#Partitioning](#Partitioning). If just encrypting a partition, continue [dm-crypt/Encrypting a non-root file system#Partition](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Partition "Dm-crypt/Encrypting a non-root file system").

#### dm-crypt wipe free space after installation

Users who did not have time for the wipe procedure before [installation](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system"), can achieve a similar effect once the encrypted system is booted and the filesystems are mounted. However, consider if the concerned filesystem may have set up reserved space, e.g. for the root user, or another [disk quota](/index.php/Disk_quota "Disk quota") mechanism, that that may limit the wipe even when performed by the root user: some parts of the underlying block device might not get written to at all.

To execute the wipe, temporarily fill the remaining free space of the partition by writing to a file inside the encrypted container:

 `# dd if=/dev/zero of=/file/in/container status=progress`  `dd: writing to ‘/file/in/container’: No space left on device` 

Sync the cache to disk and then delete the file to reclaim the free space.

```
# sync
# rm /file/in/container

```

The above process has to be repeated for every partition blockdevice created and filesystem in it. For example, setting-up [LVM on LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system"), the process has to be performed for every logical volume.

#### Wipe LUKS header

The partitions formatted with dm-crypt/LUKS contain a header with the cipher and crypt-options used, which is referred to `dm-mod` when opening the blockdevice. After the header the actual random data partition starts. Hence, when re-installing on an already randomized drive, or de-commissioning one (e.g. sale of PC, switch of drives, etc.) it *may* be just enough to wipe the header of the partition, rather than overwriting the whole drive - which can be a lengthy process.

Wiping the LUKS header will delete the PBKDF2-encrypted (AES) master key, salts and so on.

**Note:** It is crucial to write to the LUKS encrypted partition (`/dev/sdX**1**` in this example) and not directly to the disks device node. Setups with encryption as a device-mapper layer on top of others, e.g. LVM on LUKS on RAID should then write to RAID respectively.

A LUKS1 header with one single default 256 bit size keyslot is 1024 KiB in size. It is advised to also overwrite the first 4 KiB written by dm-crypt, so 1028 KiB have to be wiped. That is `1052672` Byte.

For zero offset use:

```
# head -c 1052672 /dev/urandom > */dev/sdX1*; sync

```

For 512 bit key length (e.g. for aes-xts-plain with 512 bit key) the header is 2 MiB. LUKS2 header is 4 MiB if created with [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) < 2.1 or 16 MiB if created with [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) ≥ 2.1.

If in doubt, just be generous and overwrite the first 20 MiB or so:

```
# dd if=/dev/urandom of=*/dev/sdX1* bs=512 count=40960

```

Or use `shred`. For example, to overwrite the first 20 MiB for 20 times:

```
# shred -v -z -s 20MiB -n 20 */dev/sdX1*

```

**Note:** With a backup-copy of the header data can get rescued but the filesystem was likely damaged as the first encrypted sectors were overwritten. See further sections on how to make a backup of the crucial header blocks.

When wiping the header with random data everything left on the device is encrypted data. An exception to this may occur for an SSD, because of cache blocks SSDs employ. In theory it may happen that the header was cached in these some time before and that copy may consequently be still available after wiping the original header. For strong security concerns, a secure ATA erase of the SSD should be done (procedure please see the cryptsetup [FAQ 5.19](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects)).

## Partitioning

This section only applies when encrypting an entire system. After the drive(s) has/have been securely overwritten, a proper partitioning scheme will have to be accurately chosen, taking into account the requirements of dm-crypt, and the effects that the various choices will have on the management of the resulting system.

It is important to note from now that in [almost](#Boot_partition_(GRUB)) every case there has to be a separate partition for `/boot` that must remain unencrypted, because the bootloader needs to access the `/boot` directory where it will load the initramfs/encryption modules needed to load the rest of the system (see [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") for details). If this raises security concerns, see [dm-crypt/Specialties#Securing the unencrypted boot partition](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties").

Another important factor to take into account is how the swap area and system suspension will be handled, see [dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

### Physical partitions

In the simplest case, the encrypted layers can be based directly on the physical partitions; see [Partitioning](/index.php/Partitioning "Partitioning") for the methods to create them. Just like in an unencrypted system, a root partition is sufficient, besides another for `/boot` as noted above. This method allows deciding which partitions to encrypt and which to leave unencrypted, and works the same regardless of the number of disks involved. It will also be possible to add or remove partitions in the future, but resizing a partition will be limited by the size of the disk that is hosting it. Finally note that separate passphrases or keys are required to open each encrypted partition, even though this can be automated during boot using the `crypttab` file, see [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration").

### Stacked block devices

If more flexibility is needed, though, dm-crypt can coexist with other stacked block devices like [LVM](/index.php/LVM "LVM") and [RAID](/index.php/RAID "RAID"). The encrypted containers can either reside below or on top of other stacked block devices:

*   If the LVM/RAID devices are created on top of the encrypted layer, it will be possible to add, remove and resize the file systems of the same encrypted partition liberally, and only one key or passphrase will be required for all of them. Since the encrypted layer resides on a physical partition, though, it will not be possible to exploit the ability of LVM and RAID to span multiple disks.
*   If the encrypted layer is created on top of LVM/RAID devices, it will still be possible to reorganize the file systems in the future, but with added complexity, since the encryption layers will have to be adjusted accordingly. Moreover, separate passphrases or keys will be required to open each encrypted device. This, however, is the only choice for systems that need encrypted file systems to span multiple disks.

### Btrfs subvolumes

[Btrfs](/index.php/Btrfs "Btrfs")'s built-in [subvolumes feature](/index.php/Btrfs#Subvolumes "Btrfs") can be used with dm-crypt, fully replacing the need for LVM if no other file systems are required. However note that swap files were [not supported](https://btrfs.wiki.kernel.org/index.php/FAQ#Does_btrfs_support_swap_files.3F) by brtrfs before Linux 5.0, so an [encrypted swap](/index.php/Encrypted_swap "Encrypted swap") partition is necessary if [swap](/index.php/Swap "Swap") is desired on Linux <5.0 (e.g. [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)). See also [Dm-crypt/Encrypting an entire system#Btrfs subvolumes with swap](/index.php/Dm-crypt/Encrypting_an_entire_system#Btrfs_subvolumes_with_swap "Dm-crypt/Encrypting an entire system").

### Boot partition (GRUB)

See [dm-crypt/Encrypting an entire system#Encrypted boot partition (GRUB)](/index.php/Dm-crypt/Encrypting_an_entire_system#Encrypted_boot_partition_(GRUB) "Dm-crypt/Encrypting an entire system").