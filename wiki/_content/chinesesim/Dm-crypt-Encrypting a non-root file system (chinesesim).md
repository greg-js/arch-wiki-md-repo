The following are examples of encrypting a secondary, i.e. non-root, filesystem with dm-crypt.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Overview](#Overview)
*   [2 分区](#分区)
    *   [2.1 手动挂载和卸载](#手动挂载和卸载)
    *   [2.2 自动解锁并挂载](#自动解锁并挂载)
        *   [2.2.1 启动时解锁](#启动时解锁)
        *   [2.2.2 用户登录时解锁](#用户登录时解锁)
*   [3 Loop device](#Loop_device)
    *   [3.1 Without losetup](#Without_losetup)
    *   [3.2 Using losetup](#Using_losetup)
        *   [3.2.1 Manual mounting and unmounting](#Manual_mounting_and_unmounting)

## Overview

Encrypting a secondary filesystem usually protects only sensitive data, while leaving the operating system and program files unencrypted. This is useful for encrypting an external medium, such as a USB drive, so that it can be moved to different computers securely. One might also choose to encrypt sets of data separately according to who has access to it.

Because dm-crypt is a [block-level](/index.php/Disk_encryption#Block_device_encryption "Disk encryption") encryption layer, it only encrypts full devices, [full partitions](#Partition) and [loop devices](#Loop_device). To encrypt individual files requires a filesystem-level encryption layer, such as [eCryptfs](/index.php/ECryptfs "ECryptfs") or [EncFS](/index.php/EncFS "EncFS"). See [Disk encryption](/index.php/Disk_encryption "Disk encryption") for general information about securing private data.

## 分区

这个例子说的是对 `/home` 分区的加密，但是也可以应用到其他非根分区的、包含用户数据的分区。

**提示：** 你可能在一个分区上有某个用户专用的 `/home` 目录，或者是所有用户共用这个分区作为 `/home` 目录。

首先要保证分区是空的（上面没有建立文件系统）。如果有文件系统，删除这个分区并重新建立一个空的分区。然后对其安全擦除，参见 [Dm-crypt/Drive preparation#Secure erasure of the hard disk drive](/index.php/Dm-crypt/Drive_preparation#Secure_erasure_of_the_hard_disk_drive "Dm-crypt/Drive preparation").

接下来建立包含加密容器的分区。

建立 LUKS 头：

```
# cryptsetup *options* luksFormat *device*

```

把 `*device*` 替换成之前建立的分区。参见 [Dm-crypt/Device encryption#Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") 来知道 `*options*` 可以写什么。

为了对加密分区进行操作，用设备映射器来解锁它：

```
# cryptsetup open *device* *name*

```

解锁分区之后，它会被映射成块设备 `/dev/mapper/*name*`，现在要建立 [文件系统](/index.php/%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F "文件系统")：

```
# mkfs.*fstype* /dev/mapper/*name*

```

把文件系统挂载到 `/home`；或者如果它是某个用户专用的的话，挂载到 `/home/*username*`，参见 [#手动挂载和卸载](#手动挂载和卸载)。

**提示：** 卸载并挂载一次来确定映射没有问题。

### 手动挂载和卸载

挂载分区：

```
# cryptsetup open *device* *name*
# mount -t *fstype* /dev/mapper/*name* /mnt/home

```

卸载：

```
# umount /mnt/home
# cryptsetup close *name*

```

**提示：** [GVFS](/index.php/GVFS "GVFS") 也可以挂载加密分区。用支持 gvfs 的文件管理器（比如 [Thunar](/index.php/Thunar "Thunar")）挂载该分区的时候，密码对话框就会弹出来。对于其他桌面环境，[zulucrypt](https://aur.archlinux.org/packages/zulucrypt/) 也提供了图形界面。

### 自动解锁并挂载

有三种不同方法来进行自动化解锁分区并挂载文件系统。

#### 启动时解锁

配置 `/etc/crypttab` 文件，systemd 的自动解析会在启动过程中自动解锁。如果home分区是所有用户一起用的（或者要自动挂载其他加密块设备），这种方法是最推荐使用的。

更多细节参见 [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration") 和 [Dm-crypt/System configuration#Mounting at boot time](/index.php/Dm-crypt/System_configuration#Mounting_at_boot_time "Dm-crypt/System configuration")。

#### 用户登录时解锁

借助 *pam_exec* 调用*cryptsetup open* 来实现用户登录时解锁分区。如果整个分区都是某个用户专用的 home 目录，这个方法就比较推荐。参见 [dm-crypt/Mounting at login](/index.php/Dm-crypt/Mounting_at_login "Dm-crypt/Mounting at login")。

此外也可以用 [pam_mount](/index.php/Pam_mount "Pam mount")。

## Loop device

There are two methods for using a loop device as an encrypted container, one using `losetup` directly and one without.

### Without losetup

Using losetup directly can be avoided completely by doing the following [[1]](https://wiki.gentoo.org/wiki/Custom_Initramfs#Encrypted_keyfile):

```
$ dd if=/dev/urandom of=bigsecret.img bs=100M count=1 iflag=fullblock
$ cryptsetup luksFormat bigsecret.img

```

Make sure to not omit the `iflag=fullblock` option, otherwise *dd* might return a partial read. See [dd#Partial read](/index.php/Dd#Partial_read "Dd") for details.

Before running `cryptsetup`, look at the [encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") and [ciphers and modes of operation](/index.php/Disk_encryption#Ciphers_and_modes_of_operation "Disk encryption") first to select your additional desired settings.

The instructions for opening the device and making the [file system](/index.php/File_system "File system") are the same as [#Partition](#Partition).

Creating a file smaller than the LUKS2 header (16 MiB) will give a `Requested offset is beyond real size of device bigsecret.img` error when trying to open the device.

Manual mounting and unmounting procedure is equivalent to [#Manual mounting and unmounting](#Manual_mounting_and_unmounting).

### Using losetup

A loop device enables to map a blockdevice to a file with the standard util-linux tool `losetup`. The file can then contain a filesystem, which can be used quite like any other filesystem. A lot of users know [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") as a tool to create encrypted containers. Just about the same functionality can be achieved with a loopback filesystem encrypted with LUKS and is shown in the following example.

First, start by creating an encrypted container with [dd](/index.php/Dd "Dd"), using an appropriate [random number generator](/index.php/Random_number_generator "Random number generator"):

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