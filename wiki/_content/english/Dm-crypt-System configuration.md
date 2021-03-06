**Tip:**

*   If in need to remotely unlock root or other early-boot filesystems (headless machine, distant servers...), follow the specific instructions from [dm-crypt/Specialties#Remote unlocking of the root (or other) partition](/index.php/Dm-crypt/Specialties#Remote_unlocking_of_the_root_(or_other)_partition "Dm-crypt/Specialties").
*   You may want to install and use [GNU Screen](/index.php/GNU_Screen "GNU Screen") after chrooting to make the copying and pasting of UUIDs easier.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 mkinitcpio](#mkinitcpio)
    *   [1.1 Examples](#Examples)
*   [2 Boot loader](#Boot_loader)
    *   [2.1 Kernel parameters](#Kernel_parameters)
        *   [2.1.1 root](#root)
        *   [2.1.2 resume](#resume)
    *   [2.2 Using encrypt hook](#Using_encrypt_hook)
        *   [2.2.1 cryptdevice](#cryptdevice)
        *   [2.2.2 cryptkey](#cryptkey)
        *   [2.2.3 crypto](#crypto)
    *   [2.3 Using sd-encrypt hook](#Using_sd-encrypt_hook)
        *   [2.3.1 rd.luks.uuid](#rd.luks.uuid)
        *   [2.3.2 rd.luks.name](#rd.luks.name)
        *   [2.3.3 rd.luks.options](#rd.luks.options)
        *   [2.3.4 rd.luks.key](#rd.luks.key)
        *   [2.3.5 Timeout](#Timeout)
*   [3 crypttab](#crypttab)
    *   [3.1 Mounting at boot time](#Mounting_at_boot_time)
        *   [3.1.1 Unlocking with a keyfile](#Unlocking_with_a_keyfile)
        *   [3.1.2 Mounting a stacked blockdevice](#Mounting_a_stacked_blockdevice)
    *   [3.2 Mounting on demand](#Mounting_on_demand)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 System stuck on boot/password prompt does not show](#System_stuck_on_boot/password_prompt_does_not_show)

## mkinitcpio

Depending on the particular scenarios, a subset of the following [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") hooks will have to be enabled:

| busybox | systemd | Use case |
| `encrypt` | `sd-encrypt` | Always needed when encrypting the root partition, or a partition that needs to be mounted *before* root. It is not needed in all the other cases, as system initialization scripts like `/etc/crypttab` take care of unlocking other encrypted partitions. This hook must be placed *after* the `udev` or `systemd` hook. |
| `keyboard` | Needed to make keyboards work in early userspace. |
| `keymap` | `sd-vconsole` | Provides support for non-US keymaps for typing encryption passwords; it must come *before* the `encrypt` hook. Set your keymap in `/etc/vconsole.conf`, see [Keyboard configuration in console#Persistent configuration](/index.php/Keyboard_configuration_in_console#Persistent_configuration "Keyboard configuration in console"). |
| `consolefont` | Loads an alternative console font in early userspace. Set your font in `/etc/vconsole.conf`, see [Linux console#Persistent configuration](/index.php/Linux_console#Persistent_configuration "Linux console"). |

[Other hooks](/index.php/Mkinitcpio#Common_hooks "Mkinitcpio") needed should be clear from other manual steps followed during the installation of the system.

Remember to [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") after saving the changes.

### Examples

A typical `/etc/mkinitcpio.conf` configuration using `encrypt` hook:

 `/etc/mkinitcpio.conf` 
```
...
HOOKS=(base udev autodetect keyboard keymap consolefont modconf block encrypt lvm2 filesystems fsck)
...
```

A configuration with systemd-based initramfs using `sd-encrypt` hook:

 `/etc/mkinitcpio.conf` 
```
...
HOOKS=(base systemd autodetect keyboard sd-vconsole modconf block sd-encrypt sd-lvm2 filesystems fsck)
...
```

## Boot loader

In order to enable booting an encrypted root partition, a subset of the following kernel parameters need to be set. See [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for instructions specific to your [boot loader](/index.php/Boot_loader "Boot loader").

For example, if using [GRUB](/index.php/GRUB "GRUB"), the relevant parameters are added to `/etc/default/grub` before [generating the main configuration file](/index.php/GRUB#Generate_the_main_configuration_file "GRUB"). See also [GRUB#Warning when installing in chroot](/index.php/GRUB#Warning_when_installing_in_chroot "GRUB") as another point to be aware of when installing the GRUB loader.

The kernel parameters you need to specify depend on whether or not you are using the `encrypt` hook or the `sd-encrypt` hook.

### Kernel parameters

[Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") like `root` and `resume` are specified the same way for both `encrypt` and `sd-encrypt` hooks.

#### root

The `root=` parameter specifies the `*device*` of the actual (decrypted) root file system:

```
root=*device*

```

*   If the file system is formatted directly on the decrypted device file this will be `/dev/mapper/*dmname*`.
*   If a LVM gets activated first and contains an [encrypted logical rootvolume](/index.php/Dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM "Dm-crypt/Encrypting an entire system"), the above form applies as well.
*   If the root file system is contained in a logical volume of a fully [encrypted LVM](/index.php/Encrypted_LVM "Encrypted LVM"), the device mapper for it will be in the general form of `root=/dev/*volumegroup*/*logicalvolume*`.

**Tip:** When using [GRUB](/index.php/GRUB "GRUB") and generating `grub.cfg` with *grub-mkconfig*, this parameter does not need to be specified manually. *grub-mkconfig* will determine the correct UUID of the decrypted root filesystem and add it to `grub.cfg` automatically.

#### resume

```
resume=*device*

```

*   `*device*` is the device file of the decrypted (swap) filesystem used for [suspend to disk](/index.php/Power_management/Suspend_and_hibernate#Hibernation "Power management/Suspend and hibernate"). If swap is on a separate partition, it will be in the form of `/dev/mapper/swap`. See also [dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

### Using encrypt hook

**Note:** Compared to the [sd-encrypt](/index.php/Sd-encrypt "Sd-encrypt") hook, the `encrypt` hook has some limitations. It does not support:

*   Unlocking [multiple encrypted disks](/index.php/Dm-crypt/Specialties#The_encrypt_hook_and_multiple_disks "Dm-crypt/Specialties") ([FS#23182](https://bugs.archlinux.org/task/23182)). Only **one** device can be unlocked in the initramfs.
*   Using a [detached LUKS header](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_detached_LUKS_header "Dm-crypt/Specialties") ([FS#42851](https://bugs.archlinux.org/task/42851)).

#### cryptdevice

This parameter will make the system prompt for the passphrase to unlock the device containing the encrypted root on a cold boot. It is parsed by the `encrypt` hook to identify which device contains the encrypted system:

```
cryptdevice=*device*:*dmname*

```

*   `*device*` is the path to the device backing the encrypted device. Usage of [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") is advisable.
*   `*dmname*` is the **d**evice-**m**apper name given to the device after decryption, which will be available as `/dev/mapper/*dmname*`.
*   If a LVM contains the [encrypted root](/index.php/Dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM "Dm-crypt/Encrypting an entire system"), the LVM gets activated first and the volume group containing the logical volume of the encrypted root serves as *device*. It is then followed by the respective volume group to be mapped to root. The parameter follows the form of `cryptdevice=*/dev/vgname/lvname*:*dmname*`.

**Tip:** One may want to [enable Discard/TRIM support](/index.php/Dm-crypt/Specialties#Discard/TRIM_support_for_solid_state_drives_(SSD) "Dm-crypt/Specialties") for solid state drives (SSD).

#### cryptkey

This parameter specifies the location of a keyfile and is required by the `*encrypt*` hook for reading such a keyfile to unlock the `*cryptdevice*` (unless a key is in the default location, see below). It can have three parameter sets, depending on whether the keyfile exists as a file in a particular device, a bitstream starting on a specific location, or a file in the initramfs.

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

where the offset and size are in bytes. Example: `cryptkey=/dev/sdZ:0:512` reads a 512 byte keyfile starting at the beginning of the device.

**Tip:** If the device path you want to access contains the character `:`, you have to escape it with a backslash `\`. In that case the cryptkey parameter would be as follow: `cryptkey=/dev/disk/by-id/usb-123456-0\:0:0:512` for a usb key with the id `usb-123456-0:0`.

For a file [included](/index.php/Mkinitcpio#BINARIES_and_FILES "Mkinitcpio") in the initramfs the format is[[1]](https://git.archlinux.org/svntogit/packages.git/tree/trunk/hooks-encrypt?h=packages/cryptsetup#n14):

```
cryptkey=rootfs:*path*

```

Example: `cryptkey=rootfs:/secretkey`

Also note that if `cryptkey` is not specified, it defaults to `/crypto_keyfile.bin` (in the initramfs).[[2]](https://git.archlinux.org/svntogit/packages.git/tree/trunk/hooks-encrypt?h=packages/cryptsetup#n8)

See also [dm-crypt/Device encryption#Keyfiles](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption").

#### crypto

This parameter is specific to pass *dm-crypt* plain mode options to the *encrypt* hook.

It takes the form

```
crypto=<hash>:<cipher>:<keysize>:<offset>:<skip>

```

The arguments relate directly to the *cryptsetup* options. See [dm-crypt/Device encryption#Encryption options for plain mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_plain_mode "Dm-crypt/Device encryption").

For a disk encrypted with just *plain* default options, the `crypto` arguments must be specified, but each entry can be left blank:

```
crypto=::::

```

A specific example of arguments is

```
crypto=sha512:twofish-xts-plain64:512:0:

```

### Using sd-encrypt hook

In all of the following a `rd.luks` can be replaced with a `luks`. The `rd.luks` parameters are only honored by the initrd, while the `luks` parameters are honored by both the main system and initrd. Unless you want to control devices which get unlocked after boot from kernel command line, use `rd.luks`. See [systemd-cryptsetup-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-cryptsetup-generator.8) for more options and more details.

**Tip:**

*   If the file `/etc/crypttab.initramfs` exists, [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") will add it to the initramfs as `/etc/crypttab`, you can specify devices that need to be unlocked at boot there. Syntax is documented in [#crypttab](#crypttab) and [crypttab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/crypttab.5).
*   `/etc/crypttab.initramfs` is not limited to using only UUID like `rd.luks`. You can use any of the [persistent block device naming methods](/index.php/Persistent_block_device_naming#Persistent_naming_methods "Persistent block device naming").

**Note:**

*   If you get dropped to an emergency shell at boot with systemd release 239.300-2 or later, see [FS#60907](https://bugs.archlinux.org/task/60907).
*   All of the `rd.luks` parameters can be specified multiple times to unlock multiple LUKS encrypted volumes.
*   The `rd.luks` parameters only support unlocking detectable LUKS devices. To unlock a plain dm-crypt device or a LUKS device with a detached header, you must specify it in `/etc/crypttab.initramfs`. See [#crypttab](#crypttab) for the syntax.

**Warning:** If you are using `/etc/crypttab` or `/etc/crypttab.initramfs` together with `luks.*` or `rd.luks.*` parameters, only those devices specified on the kernel command line will be activated and you will see `Not creating device 'devicename' because it was not specified on the kernel command line.`. To activate all devices in `/etc/crypttab` do not specify any `luks.*` parameters and use `rd.luks.*`. To activate all devices in `/etc/crypttab.initramfs` do not specify any `luks.*` or `rd.luks.*` parameters.

#### rd.luks.uuid

**Tip:** `rd.luks.uuid` can be omitted when using `rd.luks.name`.

```
rd.luks.uuid=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*

```

Specify the [UUID](/index.php/UUID "UUID") of the device to be decrypted on boot with this flag. If the UUID is in `/etc/crypttab.initramfs`, the options listed there will be used. For `luks.uuid` options from `/etc/crypttab.initramfs` or `/etc/crypttab` will be used.

By default the mapped device will be located at `/dev/mapper/luks-*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*` where *XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX* is the UUID of the LUKS partition.

#### rd.luks.name

**Tip:** When using this parameter you can omit `rd.luks.uuid`.

```
rd.luks.name=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*=*name*

```

Specify the name of the mapped device after the LUKS partition is open, where *XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX* is the UUID of the LUKS partition. This is equivalent to the second parameter of `encrypt`'s `cryptdevice`.

For example, specifying `rd.luks.name=12345678-9ABC-DEF0-1234-56789ABCDEF0=cryptroot` causes the unlocked LUKS device with UUID `12345678-9ABC-DEF0-1234-56789ABCDEF0` to be located at `/dev/mapper/cryptroot`.

#### rd.luks.options

```
rd.luks.options=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*=*options*

```

or

```
rd.luks.options=*options*

```

Set options for the device specified by it UUID or, if not specified, for all UUIDs not specified elsewhere (e.g., crypttab).

This is roughly equivalent to the third parameter of `encrypt`'s `cryptdevice`.

Follows a similar format to options in crypttab - options are separated by commas, options with values are specified using `*option*=*value*`.

For example:

```
rd.luks.options=timeout=10s,swap,cipher=aes-cbc-essiv:sha256,size=256

```

#### rd.luks.key

Specify the location of a password file used to decrypt the device specified by its UUID. There is no default location like there is with the `encrypt` hook parameter `cryptkey`.

If the keyfile is [included](/index.php/Mkinitcpio#BINARIES_and_FILES "Mkinitcpio") in the initramfs:

```
rd.luks.key=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*=*/path/to/keyfile*

```

or

```
rd.luks.key=*/path/to/keyfile*

```

If the keyfile is on another device:

```
rd.luks.key=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*=*/path/to/keyfile*:UUID=*ZZZZZZZZ-ZZZZ-ZZZZ-ZZZZ-ZZZZZZZZZZZZ*

```

Replace `UUID=*ZZZZZZZZ-ZZZZ-ZZZZ-ZZZZ-ZZZZZZZZZZZZ*` with the identifier of the device on which the keyfile is located. If the type of file system is different than your root file system, you must [include the kernel module for it in the initramfs](/index.php/Mkinitcpio#MODULES "Mkinitcpio").

**Warning:** `rd.luks.key` with a keyfile on another device by default does not fallback to asking for a password if the device is not available. To fallback to a password prompt, specify the `keyfile-timeout=` option in `rd.luks.options`. E.g. for a 10 second timeout: `rd.luks.options=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*=keyfile-timeout=10s` 

#### Timeout

There are two options that affect the timeout for entering the password during boot:

*   `rd.luks.options=timeout=*mytimeout*` specifies the timeout for querying for a password
*   `rootflags=x-systemd.device-timeout=*mytimeout*` specifies how long systemd should wait for the rootfs device to show up before giving up (defaults to 90 seconds)

If you want to disable the timeout altogether, then set both timeouts to zero:

```
rd.luks.options=timeout=0 rootflags=x-systemd.device-timeout=0

```

## crypttab

The `/etc/crypttab` (encrypted device table) file is similar to the [fstab](/index.php/Fstab "Fstab") file and contains a list of encrypted devices to be unlocked during system boot up. This file can be used for automatically mounting encrypted swap devices or secondary file systems.

`crypttab` is read *before* `fstab`, so that dm-crypt containers can be unlocked before the file system inside is mounted. Note that `crypttab` is read *after* the system has booted up, therefore it is not a replacement for unlocking encrypted partitions by using [mkinitcpio](#mkinitcpio) hooks and [boot loader options](#Boot_loader) as in the case of [encrypting the root partition](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system"). `crypttab` processing at boot time is made by the `systemd-cryptsetup-generator` automatically.

See [crypttab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/crypttab.5) for details, read below for some examples, and the [#Mounting at boot time](#Mounting_at_boot_time) section for instructions on how to use UUIDs to mount an encrypted device.

**Note:** When using [systemd-boot](/index.php/Systemd-boot "Systemd-boot") and the `sd-encrypt` hook, if a non-root partition's passphrase is the same as root's, there is no need to put that non-root partition in crypttab due to passphrase caching. See [this forum thread](https://bbs.archlinux.org/viewtopic.php?id=219859) for more information.

**Warning:**

*   If the *nofail* option is specified, the password entry screen may disappear while typing the password. *nofail* should therefore only be used together with keyfiles.
*   There are issues with [systemd](/index.php/Systemd "Systemd") when processing `crypttab` entries for *dm-crypt* [plain mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_plain_mode "Dm-crypt/Device encryption") (`--type plain`) devices:
    *   For `--type plain` devices with a keyfile, it is necessary to add the `hash=plain` option to crypttab due to a [systemd incompatibility](https://bugs.freedesktop.org/show_bug.cgi?id=52630). **Do not** use `systemd-cryptsetup` manually for device creation to work around it.
    *   It may be further required to add the `plain` option explicitly to force `systemd-cryptsetup` to recognize a `--type plain`) device at boot. See [systemd issue 442](https://github.com/systemd/systemd/issues/442).

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

 `/etc/crypttab`  `externaldrive         UUID=2f9a8428-ac69-478a-88a2-4aa458565431        none    luks,timeout=180` 

The first parameter is your preferred device mapper's name for the encrypted drive. The option `none` will trigger a prompt during boot to type the passphrase for unlocking the partition. The `timeout` option defines a timeout in seconds for entering the decryption password during boot.

**Note:** Keep in mind that the `timeout` option in `crypttab` only determines the amount of time allowed for *entering the password* of the encrypted device. In addition, [systemd](/index.php/Systemd "Systemd") also has a default timeout which determines the amount of time allowed for *the device to be available* (defaulting to 90 seconds), which is independent of the password timer. In consequence, even when the `timeout` option in `crypttab` is set to a value larger than 90 seconds (or it is at its default value of 0, meaning unlimited time), *systemd* will still only wait a maximum of 90 seconds for the device to be unlocked. In order to change the time *systemd* will wait for a device to be available, the option `x-systemd.device-timeout` (see [systemd.mount(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.mount.5)) can be set in [fstab](/index.php/Fstab "Fstab") for said device. It is probably desired, then, that the amount of time of the `timeout` option in `crypttab` is equal to the amount of time of the `x-systemd.device-timeout` option in `fstab` for each device mounted at boot time.

#### Unlocking with a keyfile

If the [keyfile](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") for a secondary file system is itself stored inside an encrypted root, it is safe while the system is powered off and can be sourced to automatically unlock the mount during with boot via [crypttab](/index.php/Crypttab "Crypttab"). For example, unlock a crypt specified by [UUID](/index.php/UUID "UUID"):

 `/etc/crypttab` 
```
home-crypt    UUID=<UUID identifier>    /etc/mykeyfile

```

**Tip:** If you prefer to use a `--plain` mode blockdevice, the encryption options necessary to unlock it are specified in `/etc/crypttab`. Take care to apply the systemd workaround mentioned in [crypttab](/index.php/Crypttab "Crypttab") in this case.

Then use the device mapper's name (defined in `/etc/crypttab`) to make an entry in `/etc/fstab`:

 `/etc/fstab` 
```
/dev/mapper/home-crypt        /home   ext4        defaults        0       2

```

Since `/dev/mapper/externaldrive` already is the result of a unique partition mapping, there is no need to specify an UUID for it. In any case, the mapper with the filesystem will have a different UUID than the partition it is encrypted in.

#### Mounting a stacked blockdevice

The systemd generators also automatically process stacked block devices at boot.

For example, you can create a [RAID](/index.php/RAID "RAID") setup, use cryptsetup on it and create an [LVM](/index.php/LVM "LVM") logical volume with respective filesystem inside the encrypted block device. A resulting:

 `$ lsblk -f` 
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

Given you specify the correct corresponding crypttab (e.g. UUID for the `crypto_LUKS` device) and fstab (`/dev/vgraid/lvraid`) entries, there is no need to add additional mkinitcpio hooks/configuration, because `/etc/crypttab` processing applies to non-root mounts only. One exception is when the `mdadm_udev` hook is used *already* (e.g. for the root device). In this case `/etc/madadm.conf` and the initramfs need updating to achieve the correct root raid is picked first.

### Mounting on demand

You can [start](/index.php/Start "Start") `systemd-cryptsetup@externaldrive.service` instead of using

```
# cryptsetup luksOpen UUID=... externaldrive

```

when you have an entry as follows in your `/etc/crypttab`:

 `/etc/crypttab`  `externaldrive UUID=... none noauto` 

That way you do not need to remember the exact crypttab options. It will prompt you for the passphrase if needed.

The corresponding unit file is generated automatically by [systemd-cryptsetup-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-cryptsetup-generator.8). You can list all generated unit files using:

```
$ systemctl list-unit-files | grep systemd-cryptsetup

```

## Troubleshooting

### System stuck on boot/password prompt does not show

If you are using [Plymouth](/index.php/Plymouth "Plymouth"), make sure to use the correct modules (see: [Plymouth#The plymouth hook](/index.php/Plymouth#The_plymouth_hook "Plymouth")) or disable it. Otherwise Plymouth will swallow the password prompt, making a system boot impossible.