Back to [Dm-crypt](/index.php/Dm-crypt "Dm-crypt").

Depending on requirements, different methods may be used to encrypt the [swap](/index.php/Swap "Swap") partition which are described in the following. A setup where the swap encryption is re-initialised on reboot (with a new encryption) provides higher data protection, because it avoids sensitive file fragments which may have been swapped out a long time ago without being overwritten. However, re-encrypting swap also forbids using a suspend-to-disk feature generally.

## Contents

*   [1 Without suspend-to-disk support](#Without_suspend-to-disk_support)
    *   [1.1 UUID and LABEL](#UUID_and_LABEL)
*   [2 With suspend-to-disk support](#With_suspend-to-disk_support)
    *   [2.1 LVM on LUKS](#LVM_on_LUKS)
    *   [2.2 mkinitcpio hook](#mkinitcpio_hook)
    *   [2.3 Using a swap file](#Using_a_swap_file)
*   [3 Known Issues](#Known_Issues)

## Without suspend-to-disk support

In systems where suspend-to-disk (*i.e..,* hibernation) is not a desired feature, `/etc/crypttab` can be set up to decrypt the swap partition with a random password with plain dm-crypt at boot-time. The random password is discarded on shutdown, leaving behind only encrypted, inaccessible data in the swap device.

To enable this feature, simply uncomment the line beginning with `swap` in `/etc/crypttab`. Change the `<device>` parameter to the name of your swap device. For example, it will look something like this:

 `/etc/crypttab` 
```
# <name>  <device>     <password>     <options>
swap      /dev/sd*X#*    /dev/urandom   swap,cipher=aes-cbc-essiv:sha256,size=256
```

This will map `/dev/sd*X#*` to `/dev/mapper/swap` as a swap partition that can be added in `/etc/fstab` like a normal swap. If you had a non-encrypted swap partition before, do not forget to disable it - or re-use its [fstab](/index.php/Fstab "Fstab") entry by changing the device to `/dev/mapper/swap`. The default options should be sufficient for most usage. For other options see and an explanation of each column, see `man 5 crypttab` as well as [point cryptsetup FAQ 2.3](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#2-setup).

**Warning:** All contents of the named device will be permanently **deleted**. It is dangerous to use the kernel's simple naming for a swap device, since their naming order (*e.g.* `/dev/sda`, `/dev/sdb`) changes upon each boot. Options are:

*   Use `by-id` and `by-path` paths. However, these are both are susceptible to hardware changes. See [Persistent block device naming#by-id and by-path](/index.php/Persistent_block_device_naming#by-id_and_by-path "Persistent block device naming").
*   Use an [LVM](/index.php/LVM "LVM") logical volume's name.
*   Use the method described in [#UUID and LABEL](#UUID_and_LABEL). Labels and [UUIDS](/index.php/Persistent_block_device_naming#by-uuid "Persistent block device naming") **cannot** be used directly because of the recreation and re-encryption of the swap device on every boot with `mkswap` [[1]](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#2-setup).

To use a `by-id` persistent device naming instead of kernel simple naming, first identify the swap device:

 `# ls -l /dev/disk/*/* | grep sdaX` 
```
lrwxrwxrwx 1 root root 10 Oct 12 16:54 /dev/disk/by-id/ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-partX -> ../../sdaX
lrwxrwxrwx 1 root root 10 Oct 12 16:54 /dev/disk/by-id/wwn-0x60015ee0000b237f-partX -> ../../sdaX

```

Then use as a persistent reference for the `/dev/sd*X#*` example partition (if two results are returned as above, choose either one of them):

 `/etc/crypttab` 
```
# <name>  <device>                                                         <password>     <options>
swap      /dev/disk/by-id/ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-partX  /dev/urandom   swap,cipher=aes-cbc-essiv:sha256,size=256
```

After a reboot to activate the encrypted swap, you will note that running `swapon -s` shows an arbitrary device mapper entry (e.g. `/dev/dm-1`) for it, while the `lsblk` command shows **crypt** in the `FSTYPE` column. Due to fresh encryption each boot, the UUID for `/dev/mapper/swap` will change every time.

**Note:** If the partition chosen for swap was previously a LUKS partition, crypttab will not overwrite the partition to create a swap partition. This is a safety measure to prevent data loss from accidental mis-identification of the swap partition in crypttab. In order to use such a partition the [LUKS header must be overwritten](/index.php/Dm-crypt/Drive_preparation#Wipe_LUKS_header "Dm-crypt/Drive preparation") once.

**Note:** If you use the `sd-encrypt` hook and `luks.*` kernel parameters for the rootfs while also using /etc/crypttab for the swap then systemd will complain about "Not creating device 'swap' because it was not specified on the kernel command line.". To fix this issue just use `rd.luks.*` parameters instead.

### UUID and LABEL

**Note:** This does not work when using the systemd and sd-encrypt init hooks

It's dangerous to use crypttab swap with simple kernel device names like `/dev/sdX#` or even `/dev/disk/by-id/ata-SERIAL-partX`. A small change in your device names or partitioning layout and `/etc/crypttab` will see your valuable data formatted on the next boot. Same if you use PARTUUID and then decide to use that partition for something else without removing the crypttab entry first.

It is more reliable to identify the correct partition by giving it a genuine UUID or LABEL. By default that does not work because dm-crypt and `mkswap` would simply overwrite any content on that partition which would remove the UUID and LABEL too; however, it is possible to specify a swap offset. This allows you to create a very small, empty, bogus filesystem with no other purpose than providing a persistent UUID or LABEL for the swap encryption.

Create a filesystem with label of your choice:

```
# mkfs.ext2 -L *cryptswap* /dev/sd*X#* 1M

```

The unusual parameter after the device name limits the filesystem size to 1 MiB, leaving room for encrypted swap behind it.

 `# blkid /dev/sdX#`  `/dev/sdX#: LABEL="cryptswap" UUID="b72c384e-bd3c-49aa-b7a7-a28ea81a2605" TYPE="ext2"` 

With this, `/dev/sdX#` now can easily be identified either by UUID or LABEL, regardless of how its device name or even partition number might change in the future. All that's left is the `/etc/crypttab` and `/etc/fstab` entries:

 `/etc/crypttab` 
```
# <name> <device>         <password>    <options>
swap     LABEL=*cryptswap*  /dev/urandom  swap,offset=2048,cipher=aes-xts-plain64,size=256
```

Note the offset: it's 2048 sectors of 512 bytes, thus 1 MiB. This way the encrypted swap will not affect the filesystem LABEL/UUID, and data alignment works out as well.

 `/etc/fstab` 
```
# <filesystem>    <dir>  <type>  <options>  <dump>  <pass>
/dev/mapper/swap  none   swap    defaults   0       0
```

Using this setup, the cryptswap will only try to use the partition with the corresponding LABEL, regardless of what its device name may be. Should you decide to use the partition for something else, by formatting it the cryptswap LABEL would also be gone, so cryptswap won't overwrite it on your next boot.

## With suspend-to-disk support

To be able to resume after suspending the computer to disk (hibernate), it is required to keep the swap space intact. Therefore, it is required to have a pre-existent LUKS swap partition, which can be stored on the disk or input manually at startup.

The following three methods are alternatives for setting up an encrypted swap for resume-from-disk. If you apply any of them, be aware that critical data swapped out by the system may potentially stay in the swap over a long period (i.e. until it is overwritten). To reduce this risk consider setting up a system job which re-encrypts swap, e.g. each time the system is going into a regular shut-down, along with the method of your choice.

### LVM on LUKS

A simple way to realize encrypted swap with suspend-to-disk support is by using a swap [LVM](/index.php/LVM "LVM") device on the same encryption layer as the root volume, so that both are opened by the `encrypt` hook at boot. Follow the instructions on [Dm-crypt/Encrypting an entire system#LVM on LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system") and then just configure the [required kernel parameters](/index.php/Suspend_and_hibernate#Required_kernel_parameters "Suspend and hibernate").

Assuming you have setup LVM on LUKS with a swap logical volume (at `/dev/MyStorage/swap` for example), all you need to do is add the **resume** [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") hook, and add the `resume=/dev/MyStorage/swap` kernel parameter to your boot loader. For [GRUB](/index.php/GRUB "GRUB"), this can be done by appending it to the `GRUB_CMDLINE_LINUX_DEFAULT` variable in `/etc/default/grub`.

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX_DEFAULT="... resume=/dev/MyStorage/swap"` 

then run `grub-mkconfig -o /boot/grub/grub.cfg` to update GRUB's configuration file. To add the mkinitcpio hook, edit the following line in `mkinitcpio.conf`

 `/etc/mkinitcpio.conf`  `HOOKS="... encrypt lvm2 **resume** ... filesystems ..."` 

then run `mkinitcpio -p linux` to update the [initramfs](/index.php/Initramfs "Initramfs") image.

### mkinitcpio hook

**Note:** This section is only applicable when using the `encrypt` hook, which can only unlock a single device ([FS#23182](https://bugs.archlinux.org/task/23182)). With `sd-encrypt` multiple devices may be unlocked (see [Dm-crypt/System configuration#Using sd-encrypt hook](/index.php/Dm-crypt/System_configuration#Using_sd-encrypt_hook "Dm-crypt/System configuration")), but swap autodetection is not available yet.[[2]](https://github.com/systemd/systemd/issues/4878)

If the swap device is on a different device from that of the root file system, it will not be opened by the `encrypt` hook, i.e. the resume will take place before `/etc/crypttab` can be used, therefore it is required to create a hook in `/etc/mkinitcpio.conf` to open the swap LUKS device before resuming.

If you want to use a partition which is currently used by the system, you have to disable it first:

```
# swapoff /dev/<device>

```

Also make sure you remove any line in `/etc/crypttab` pointing to this device.

If you are reusing an existing swap partition, and if the partition is on a GPT partition table, you will need to remove the partition, and then recreate it with no File System type. See [Partitioning](/index.php/Partitioning "Partitioning"). This will prevent systemd-gpt-auto-generator from discovering and enabling the partition at boot.

The following setup has the disadvantage of having to insert an additional passphrase for the swap partition manually on every boot.

**Warning:** Do not use this setup with a key file if `/boot` is unencrypted. Please read about the issue reported [here](https://wiki.archlinux.org/index.php?title=Talk:Dm-crypt&oldid=255742#Suspend_to_disk_instructions_are_insecure). Alternatively, use a gnupg-encrypted keyfile as per [https://bbs.archlinux.org/viewtopic.php?id=120181](https://bbs.archlinux.org/viewtopic.php?id=120181)

To format the encrypted container for the swap partition, create a keyslot for a user-memorizable passphrase.

Open the partition in `/dev/mapper`:

```
# cryptsetup open --type luks /dev/<device> swapDevice

```

Create a swap filesystem inside the mapped partition:

```
# mkswap /dev/mapper/swapDevice

```

Now you have to create a hook to open the swap at boot time. You can either [install](/index.php/Install "Install") and configure [mkinitcpio-openswap](https://aur.archlinux.org/packages/mkinitcpio-openswap/), or follow the following instructions. Create a hook file containing the open command:

 `/etc/initcpio/hooks/openswap` 
```
 run_hook ()
 {
     cryptsetup open --type luks /dev/<device> swapDevice
 }

```

for opening the swap device by typing your password or

 `/etc/initcpio/hooks/openswap` 
```
 run_hook ()
 {
     ## Optional: To avoid race conditions
     x=0;
     while [ ! -b /dev/mapper/<root-device> ] && [ $x -le 10 ]; do
        x=$((x+1))
        sleep .2
     done
     ## End of optional

     mkdir crypto_key_device
     mount /dev/mapper/<root-device> crypto_key_device
     cryptsetup open --type luks --key-file crypto_key_device/<path-to-the-key> /dev/<device> swapDevice
     umount crypto_key_device
 }

```

for opening the swap device by loading a keyfile from a crypted root device.

On some computers race conditions may occur when mkinitcpio tries to mount the device before the decryption process and device enumeration is completed. The commented *Optional* block will delay the boot process up to 2 seconds until the root device is ready to mount.

**Note:** If swap is on a Solid State Disk (SSD) and Discard/TRIM is desired the option `--allow-discards` has to get added to the cryptsetup line in the openswap hook above. See [Discard/TRIM support for solid state disks (SSD)](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_disks_.28SSD.29 "Dm-crypt/Specialties") or [SSD](/index.php/SSD "SSD") for more information on discard. Additionally you have to add the mount option 'discard' to your fstab entry for the swap device.

Then create and edit the hook setup file:

 `/etc/initcpio/install/openswap` 
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

Set up your system to resume from your chosen mapped partition. For example, if you use [GRUB](/index.php/GRUB "GRUB") with kernel hibernation support, add `resume=`*your chosen mapped partition* and `resume_offset=`*see calculation command below* to the kernel line in `/boot/grub/grub.cfg`. A line with encrypted root partition can look like this:

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

## Known Issues

*   "Stopped (with error) /dev/dm-1" in logs. See [[3]](https://github.com/systemd/systemd/issues/1620).