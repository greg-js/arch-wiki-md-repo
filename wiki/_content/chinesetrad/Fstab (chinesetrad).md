`/etc/fstab`這個檔案提供了檔案系統的資訊。他定義了儲存設備和磁區如何初始化和如何聯接至整個系統。

## Contents

*   [1 欄位定義](#欄位定義)
*   [2 Example](#Example)
*   [3 Defining filesystems](#Defining_filesystems)
    *   [3.1 Kernel naming](#Kernel_naming)
    *   [3.2 UUIDs](#UUIDs)
    *   [3.3 Labels](#Labels)
*   [4 Tips](#Tips)
    *   [4.1 atime options](#atime_options)
*   [5 Resources](#Resources)

## 欄位定義

`/etc/fstab`檔案內容利用用tab或是空白鍵分隔出下列欄位：

```
<file system>	<dir>	<type>	<options>	<dump>	<pass>

```

*   **<file systems>** - 儲存裝置，例：`/dev/sda1`。
*   **<dir>** - 使用mount指令將儲存裝置掛載到哪個資料夾。
*   **<type>** - 定義該儲存裝置的檔案系統類型。有許多不同的類型已被支援，例：ext2, ext3, reiserfs, xfs, jfs, smbfs, iso9660, vfat, ntfs, swap。另外也可使用auto這個項目，讓mount指令字型判斷該儲存裝置適用哪種檔案系統，可以用在移動或卸除的裝置(例：外接光碟機)。
*   **<options>** - 根據不同的檔案系類型會有不同的特殊選項可以使用，不同檔案系統類型可能會有所不同下面列出一般的選項。

*   auto - 該儲存裝置會再開機時或執行'mount -a'時自動掛載。
*   noauto - 該儲存裝置，只有在你指定掛載時才會掛載。
*   exec - 允許二進位的執行檔再該儲存裝置上運行(預設)。
*   noexec - 不允許二進位的執行檔再該儲存裝置上運行.
*   ro - 為read-only簡寫，唯讀。
*   rw - 為read-write簡寫，只可以讀寫。
*   sync - I/O should be done synchronously
*   async - I/O should be done asynchronously
*   user - Permit any user to mount the filesystem (implies noexec,nosuid,nodev unless overridden.)
*   nouser - Only allow root to mount the filesystem. (default)
*   defaults - Default mount settings (equivalent to rw,suid,dev,exec,auto,nouser,async).
*   suid - Allow the operation of suid, and sgid bits. They are mostly used to allow users on a computer system to execute binary executables with temporarily elevated privileges in order to perform a specific task.
*   nosuid - Block the operation of suid, and sgid bits.
*   noatime - Do not update inode access times on the filesystem. Can help performance (see [atime options](#atime_options)).
*   nodiratime - Do not update directory inode access times on the filesystem. Can help performance (see [atime options](#atime_options)).
*   relatime - Update inode access times relative to modify or change time. Access time is only updated if the previous access time was earlier than the current modify or change time. (Similar to noatime, but doesn't break mutt or other applications that need to know if a file has been read since the last time it was modified.) Can help performance (see [atime options](#atime_options)).

*   **<dump>** - Is used by the dump utility to decide when to make a backup. When installed (not installed by a standard installation of Arch Linux), dump checks the entry and uses the number to decide if a file system should be backed up. Possible entries are 0 and 1\. If 0, dump will ignore the file system, if 1, dump will make a backup. Most users will not have dump installed, so they should put 0 for the <dump> entry.
*   **<pass>** fsck reads the <pass> number and determines in which order the file systems should be checked. Possible entries are 0, 1, and 2\. The root file system should have the highest priority, 1, all other file systems you want to have checked should get a 2\. File systems with a <pass> value 0 will not be checked by the fsck utility.

## Example

Here is an example `/etc/fstab` using kernel naming (/dev/sdx) descriptors:

```
# <file system>        <dir>         <type>    <options>             <dump> <pass>
none                   /dev/pts      devpts    defaults                0      0
none                   /dev/shm      tmpfs     defaults                0      0

/dev/cdrom             /media/cd     iso9660   ro,user,noauto,unhide   0      0
/dev/dvd               /media/dvd    udf       ro,user,noauto,unhide   0      0
/dev/fd0               /media/fl     auto      user,noauto             0      0

/dev/sda2              /             ext4      defaults,noatime        0      1
/dev/sda6              /home         ext4      defaults,noatime        0      2
/dev/sda7              none          swap      defaults                0      0

```

## Defining filesystems

You can define the filesystems in the `/etc/fstab` configuration in three different ways: by kernel naming descriptors, by UUID, or by labels. The advantage of using UUIDs or labels is that they are not dependent on disk order. This is useful if you change your storage device order in the BIOS, you switch storage device cabling, or because some BIOS's may occasionally change the order of storage devices.

### Kernel naming

You can get kernel naming descriptors using `fdisk`:

```
# fdisk -l
...

Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *           1        2550    20482843+   b  W95 FAT32
/dev/sda2            2551        5100    20482875   83  Linux
/dev/sda3            5101        7650    20482875   83  Linux
/dev/sda4            7651      121601   915311407+   5  Extended
/dev/sda5            7651       10200    20482843+  83  Linux
/dev/sda6           10201       17849    61440561   83  Linux
/dev/sda7           17850       18104     2048256   82  Linux swap / Solaris
/dev/sda8           18105       18113       72261   83  Linux
/dev/sda9           18114      121601   831267328+   7  HPFS/NTFS

```

### UUIDs

UUIDs are generated by the make-filesystem utilities (`mkfs.*`) when you create a filesystem. `blkid` will show you the UUIDs of mounted devices and partitions:

```
# blkid
/dev/sda1: UUID="76E4F702E4F6C401" LABEL="vista" TYPE="ntfs"
/dev/sda2: LABEL="Root" UUID="24f28fc6-717e-4bcd-a5f7-32b959024e26" TYPE="ext4"
/dev/sda6: LABEL="Home" UUID="03ec5dd3-45c0-4f95-a363-61ff321a09ff" TYPE="ext4" 
/dev/sda7: LABEL="swap" UUID="4209c845-f495-4c43-8a03-5363dd433153" TYPE="swap"
/dev/sda10: UUID="0ea7a93f-537c-4868-9201-0dc090c050e4" TYPE="crypto_LUKS"
/dev/mapper/sda10: UUID="d3560bbb-b5d5-46c5-a7a8-434c885217c7" UUID_SUB="425ab275-d520-4636-8d16-55fb2b957971" TYPE="btrfs"

```

An example `/etc/fstab` using the UUID identifiers:

```
# <file system>        <dir>         <type>    <options>             <dump> <pass>
none                   /dev/pts      devpts    defaults                0      0
none                   /dev/shm      tmpfs     defaults                0      0

/dev/cdrom             /media/cd     iso9660   ro,user,noauto,unhide   0      0
/dev/dvd               /media/dvd    udf       ro,user,noauto,unhide   0      0
/dev/fd0               /media/fl     auto      user,noauto             0      0

UUID=24f28fc6-717e-4bcd-a5f7-32b959024e26 /     ext4 defaults,noatime  0      1
UUID=03ec5dd3-45c0-4f95-a363-61ff321a09ff /home ext4 defaults,noatime  0      2
UUID=4209c845-f495-4c43-8a03-5363dd433153 none  swap defaults          0      0

```

### Labels

The device or partition will need to be labeled first. You can use a common application like [gparted](https://www.archlinux.org/packages/?name=gparted) to label partitions (not all filesystem types support labels however) or you can use `e2label` to label ext2, ext3, and ext4 partitions.

To label a device or partition it can not be mounted (needs source). Boot from a LiveCD or LiveUSB then you can label by:

```
e2label /dev/sda6 Arch_Linux

```

Labels can be up to 16 characters long. They can also have spaces too, but there is no way to have your `fstab` file (or [GRUB](/index.php/GRUB "GRUB") configuration file for that matter) be able to recognize them by that label if you do.

Labels should be un-ambiguous. That is that each label needs to be unique in order to not cause any conflicts. Devices and partitions can be labeled and used as identifiers by:

```
# <file system>        <dir>         <type>    <options>             <dump> <pass>
none                   /dev/pts      devpts    defaults                0      0
none                   /dev/shm      tmpfs     defaults                0      0

/dev/cdrom             /media/cd     iso9660   ro,user,noauto,unhide   0      0
/dev/dvd               /media/dvd    udf       ro,user,noauto,unhide   0      0
/dev/fd0               /media/fl     auto      user,noauto             0      0

LABEL=Arch_Linux       /             ext4      defaults,noatime        0      1
LABEL=Arch_Swap        none          swap      defaults                0      0

```

## Tips

Some tips.

### atime options

The use of `noatime`, `nodiratime` or `relatime` can help disk performance for ext2, ext3, and ext4 filesystems. Linux by default keeps a record (writes to the disk) every times it reads from the disk. This was more purposeful when Linux was being used for servers and doesn't have much use for desktop use. This works good for almost all applications but [Mutt](/index.php/Mutt "Mutt") that needs this information. For mutt, you should only use the `relatime` option.

## Resources

*   [NTFS Write Support](/index.php/NTFS_Write_Support "NTFS Write Support")
*   [how to fstab](http://ubuntuforums.org/showthread.php?t=283131)
*   [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming")