# dm-crypt/Swap encryption

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Back to [Dm-crypt](/index.php/Dm-crypt "Dm-crypt").

Depending on requirements, different methods may be used to encrypt the swap partition which are described in the following. A setup where the swap encryption is re-initialised on reboot (with a new encryption) provides higher data protection, because it avoids sensitive file fragments which may have been swapped out a long time ago without being overwritten. However, re-encrypting swap also forbids using a suspend-to-disk feature generally.

## Contents

*   [1 Without suspend-to-disk support](#Without_suspend-to-disk_support)
    *   [1.1 UUID and LABEL](#UUID_and_LABEL)
*   [2 With suspend-to-disk support](#With_suspend-to-disk_support)
    *   [2.1 LVM on LUKS](#LVM_on_LUKS)
    *   [2.2 mkinitcpio hook](#mkinitcpio_hook)
    *   [2.3 Using a swap file](#Using_a_swap_file)

## Without suspend-to-disk support

In systems where suspend-to-disk is not a desired feature, it is possible to encrypt the swap partition with a random key at boot-time, thus destroying the contents of the named partition during every boot. This is accomplished by using plain dm-crypt and configuring `/etc/crypttab` to call `mkswap`: see [point cryptsetup FAQ 2.3](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#2-setup) and on "swap" option described in `man (5) crypttab`.

Default `/etc/crypttab` already contains a line for swap encryption so you can basically just uncomment it and change the `<device>` parameter to the [persistent name](/index.php/Persistent_block_device_naming "Persistent block device naming") of your swap device.

 `/etc/crypttab` 

```
# <name>       <device>         <password>              <options>
# swap         /dev/sdaX        /dev/urandom            swap,cipher=aes-cbc-essiv:sha256,size=256
```

Where:

<name>

Represents the name to state in the first column of `/etc/fstab` (as "`/dev/mapper/<name>`").

<device>

Should be the persistent device name for the swap device.

<password>

`/dev/urandom` sets the dm-crypt master key to be randomized on every volume recreation.

<options>

The `swap` option runs mkswap after cryptographic's are setup.

**Warning:** Make sure to use either `by-id`, `by-path` or [LVM](/index.php/LVM "LVM") logical volumes' [persistent device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") for the `<device>` array (especially if there are multiple storage drives in the system), as it might happen that their usual kernel naming order (sda, sdb,...) changes upon boots and thus the swap would be created over a valuable file system, destroying all its content. Because of the recreation and re-encryption of the swap device on every boot with `mkswap`, labels and UUIDs cannot be used (see [naming by UUID](/index.php/Persistent_block_device_naming#by-uuid "Persistent block device naming") and [cryptsetup FAQ 2.3](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#2-setup)).

For example, `by-id` persistent device naming is first identified for the chosen device:

 `# ls -l /dev/disk/*/* | grep sdaX` 

```
lrwxrwxrwx 1 root root 10 Oct 12 16:54 /dev/disk/by-id/ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-partX -> ../../sdaX
lrwxrwxrwx 1 root root 10 Oct 12 16:54 /dev/disk/by-id/wwn-0x60015ee0000b237f-partX -> ../../sdaX

```

and then used as a persistent reference for the `/dev/sdaX` example partition (if two results are returned as above, choose either one of them):

 `/etc/crypttab` 

```
# <name>                      <device>                                   <password>     <options>
  swap  /dev/disk/by-id/ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-partX  /dev/urandom   swap,cipher=aes-cbc-essiv:sha256,size=256
```

This will map `/dev/sdaX` to `/dev/mapper/swap` as a swap partition that can be added in `/etc/fstab` like a normal swap. If you had a non-encrypted swap partition before, do not forget to disable it - or re-use its [fstab](/index.php/Fstab "Fstab") entry by changing the device to `/dev/mapper/swap`.

After a reboot to activate the encrypted swap, you will note that running `swapon -s` shows an arbitrary device mapper entry (e.g. `/dev/dm-1`) for it, while the `lsblk` command shows **crypt** in the `FSTYPE` column. Due to fresh encryption each boot, the UUID for `/dev/mapper/swap` will change every time.

If the partition chosen for swap was previously a LUKS partition, crypttab will not overwrite the partition to create a swap partition. This is a safety measure to prevent data loss from accidental mis-identification of the swap partition in crypttab. In order to use such a partition the [LUKS header must be overwritten](/index.php/Dm-crypt/Drive_preparation#Wipe_LUKS_header "Dm-crypt/Drive preparation") once.

### UUID and LABEL

It is very dangerous to use crypttab swap with `/dev/sdx4` or even `/dev/disk/by-id/ata-SERIAL-partX`. A small change in your device names or partitioning layout and `/etc/crypttab` will see your valuable data formatted on the next boot. It is more reliable to identify the correct partition by giving it a UUID or LABEL. By default that does not work because dm-crypt and `mkswap` would simply overwrite any content on that partition; however, it is possible to specify an offset. This allows you to create a very small, empty, bogus filesystem (with no other purpose than providing a UUID or LABEL), which survives the swap encryptions.

Create a filesystem with label of your choice:

```
# mkfs.ext2 -L cryptswap /dev/sdx4 1M

```

The unusual parameter after the device name limits the filesystem size to 1 MiB.

 `# blkid /dev/sdx4`  `/dev/sdx4: LABEL="cryptswap" UUID="b72c384e-bd3c-49aa-b7a7-a28ea81a2605" TYPE="ext2"` 

With this, `/dev/sdx4` now can easily be identified either by UUID or LABEL, regardless of how its device name or even partition number might change in the future. All that's left is the `/etc/crypttab` and `/etc/fstab` entries:

 `/etc/crypttab` 

```
# <name>       <device>         <password>              <options>
cryptswap      LABEL=cryptswap  /dev/urandom            swap,offset=2048,cipher=aes-xts-plain64,size=512
```

Note the offset: it's 2048 sectors of 512 bytes, thus 1 MiB. This way the filesystem LABEL/UUID remains intact, and data alignment works out as well.

 `/etc/fstab` 

```
# <filesystem>         <dir>  <type>  <options>  <dump>  <pass>
/dev/mapper/cryptswap  none   swap    defaults   0       0
```

## With suspend-to-disk support

The following three methods are alternatives for setting up an encrypted swap for resume-from-disk. If you apply any of them, be aware that critical data swapped out by the system may potentially stay in the swap over a long period (i.e. until it is overwritten). To reduce this risk consider setting up a system job which re-encrypts swap, e.g. each time the system is going into a regular shut-down, along with the method of your choice.

### LVM on LUKS

A simple way to realize encrypted swap with suspend-to-disk support is by using [LVM](/index.php/LVM "LVM") ontop the encryption layer, so one encrypted partition can contain infinite filesystems (root, swap, home, ...). Follow the instructions on [Dm-crypt/Encrypting an entire system#LVM on LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system") and then just configure the [required kernel parameters](/index.php/Suspend_and_hibernate#Required_kernel_parameters "Suspend and hibernate").

Assuming you have setup LVM on LUKS with a swap logical volume (at `/dev/MyStorage/swap` for example), all you need to do is add the **resume** [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") hook, and add the `resume=/dev/MyStorage/swap` kernel parameter to your boot loader. For [GRUB](/index.php/GRUB "GRUB"), this can be done by appending it to the `GRUB_CMDLINE_LINUX_DEFAULT` variable in `/etc/default/grub`.

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX_DEFAULT="... resume=/dev/MyStorage/swap"` 

then run `grub-mkconfig -o /boot/grub/grub.cfg` to update GRUB's configuration file. To add the mkinitcpio hook, edit the following line in `mkinitcpio.conf`

 `/etc/mkinitcpio.conf`  `HOOKS="... encrypt lvm2 **resume** ... filesystems ..."` 

then run `mkinitcpio -p linux` to update the [initramfs](/index.php/Initramfs "Initramfs") image.

### mkinitcpio hook

To be able to resume after suspending the computer to disk (hibernate), it is required to keep the swap filesystem intact. Therefore, it is required to have a pre-existent LUKS swap partition, which can be stored on the disk or input manually at startup. Because the resume takes place before `/etc/crypttab` can be used, it is required to create a hook in `/etc/mkinitcpio.conf` to open the swap LUKS device before resuming.

If you want to use a partition which is currently used by the system, you have to disable it first:

```
# swapoff /dev/<device>

```

Also make sure you remove any line in `/etc/crypttab` pointing to this device.

The following setup has the disadvantage of having to insert an additional passphrase for the swap partition manually on every boot.

**Warning:** Do not use this setup with a key file. Please read about the issue reported [here](https://wiki.archlinux.org/index.php?title=Talk:Dm-crypt&oldid=255742#Suspend_to_disk_instructions_are_insecure). Alternatively, use a gnupg-encrypted keyfile as per [https://bbs.archlinux.org/viewtopic.php?id=120181](https://bbs.archlinux.org/viewtopic.php?id=120181)

To format the encrypted container for the swap partition, create a keyslot for a user-memorizable passphrase.

Open the partition in `/dev/mapper`:

```
# cryptsetup open --type luks /dev/<device> swapDevice

```

Create a swap filesystem inside the mapped partition:

```
# mkswap /dev/mapper/swapDevice

```

Now you have to create a hook to open the swap at boot time. You can either [install](/index.php/Install "Install") and configure [mkinitcpio-openswap](https://aur.archlinux.org/packages/mkinitcpio-openswap/)<sup><small>AUR</small></sup>, or follow the following instructions. Create a hook file containing the open command:

 `/lib/initcpio/hooks/openswap` 

```
 run_hook ()
 {
     cryptsetup open --type luks /dev/<device> swapDevice
 }

```

for opening the swap device by typing your password or

 `/lib/initcpio/hooks/openswap` 

```
 run_hook ()
 {
     mkdir crypto_key_device
     mount /dev/mapper/<root-device> crypto_key_device
     cryptsetup open --type luks --key-file crypto_key_device/<path-to-the-key> /dev/<device> swapDevice
     umount crypto_key_device
 }

```

for opening the swap device by loading a keyfile from a crypted root device

**Note:** If swap is on a Solid State Disk (SSD) and Discard/TRIM is desired the option `--allow-discards` has to get added to the cryptsetup line in the openswap hook above. See [Discard/TRIM support for solid state disks (SSD)](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_disks_.28SSD.29 "Dm-crypt/Specialties") or [SSD](/index.php/SSD "SSD") for more information on discard. Additionally you have to add the mount option 'discard' to your fstab entry for the swap device.

Then create and edit the hook setup file:

 `/lib/initcpio/install/openswap` 

```
build ()
{
   add_runscript
}
help ()
{
cat<<HELPEOF
  This opens the swap encrypted partition /dev/<device> in /dev/mapper/swapDevice
HELPEOF
}

```

Add the hook `openswap` in the `HOOKS` array in `/etc/mkinitcpio.conf`, before `filesystem` but after `encrypt`. Do not forget to add the `resume` hook after `openswap`.

```
HOOKS="... encrypt openswap resume filesystems ..."

```

Regenerate the boot image:

```
# mkinitcpio -p linux

```

Add the mapped partition to `/etc/fstab` by adding the following line:

```
/dev/mapper/swapDevice swap swap defaults 0 0

```

Set up your system to resume from `/dev/mapper/swapDevice`. For example, if you use [GRUB](/index.php/GRUB "GRUB") with kernel hibernation support, add `resume=/dev/mapper/swapDevice` to the kernel line in `/boot/grub/grub.cfg`. A line with encrypted root and swap partitions can look like this:

```
kernel /vmlinuz-linux cryptdevice=/dev/sda2:rootDevice root=/dev/mapper/rootDevice resume=/dev/mapper/swapDevice ro

```

To make the parameter persistent on kernel updates, add it to `/etc/default/grub`.

At boot time, the `openswap` hook will open the swap partition so the kernel resume may use it. If you use special hooks for resuming from hibernation, make sure they are placed **after** `openswap` in the `HOOKS` array. Please note that because of initrd opening swap, there is no entry for swapDevice in `/etc/crypttab` needed in this case.

### Using a swap file

A swap file can be used to reserve swap-space within an existing partition and may also be setup inside an encrypted blockdevice's partition. When resuming from a swapfile the `resume` hook must be supplied with the passphrase to unlock the device where the swap file is located.

**Warning:** [Btrfs](/index.php/Dm-crypt/Drive_preparation#Btrfs_subvolumes "Dm-crypt/Drive preparation") does not support swap files. Failure to heed this warning may result in file system corruption. While a swap file may be used on [Btrfs](/index.php/Btrfs#Swap_file "Btrfs") when mounted through a loop device, this will result in severely degraded swap performance.

To create it, first choose a mapped partition (e.g. `/dev/mapper/rootDevice`) whose mounted filesystem (e.g. `/`) contains enough free space to create a swapfile with the desired size.

Now [create the swap file](/index.php/Swap#Swap_file_creation "Swap") (e.g. `/swapfile`) inside the mounted filesystem of your chosen mapped partition. Be sure to activate it with `swapon` and also add it to your `/etc/fstab` file afterward. Note that the swapfile's previous contents remain transparent over reboots.

Set up your system to resume from your chosen mapped partition. For example, if you use [GRUB](/index.php/GRUB "GRUB") with kernel hibernation support, add `resume=`_your chosen mapped partition_ and `resume_offset=`_see calculation command below_ to the kernel line in `/boot/grub/grub.cfg`. A line with encrypted root partition can look like this:

```
kernel /vmlinuz-linux cryptdevice=/dev/sda2:rootDevice root=/dev/mapper/rootDevice resume=/dev/mapper/rootDevice resume_offset=123456789 ro

```

The `resume_offset` of the swap-file points to the start (extent zero) of the file and can be identified like this:

```
# filefrag -v /swapfile | awk '{if($1=="0:"){print $4}}'

```

Add the `resume` hook to your `etc/mkinitcpio.conf` file and [rebuild the image](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") afterward:

```
HOOKS="... encrypt **resume** ... filesystems ..."

```

If you use a USB keyboard to enter your decryption password, then the `keyboard` module **must** appear in front of the `encrypt` hook, as shown below. Otherwise, you will not be able to boot your computer because you could not enter your decryption password to decrypt your Linux root partition! (If you still have this problem after adding `keyboard`, try `usbinput`, though this is deprecated.)

```
HOOKS="... **keyboard** encrypt ..."

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dm-crypt/Swap_encryption&oldid=410695](https://wiki.archlinux.org/index.php?title=Dm-crypt/Swap_encryption&oldid=410695)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Encryption](/index.php/Category:Encryption "Category:Encryption")
*   [File systems](/index.php/Category:File_systems "Category:File systems")