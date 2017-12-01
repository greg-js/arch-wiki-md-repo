Related articles

*   [File systems](/index.php/File_systems "File systems")

[F2FS](https://en.wikipedia.org/wiki/F2FS "wikipedia:F2FS") (Flash-Friendly File System) is a file system intended for NAND-based flash memory equipped with Flash Transition Layer. Unlike JFFS or UBIFS it relies on FTL to handle write distribution. It is supported from kernel 3.8 onwards.

[F2FS](https://en.wikipedia.org/wiki/F2FS "wikipedia:F2FS") (Flash-Friendly File System) 是一个为配备了 Flash Transition Layer 的 NAND 闪存开发的文件系统，与 JFFS 或 UBIFS 不同，它依靠 FTL 来处理写入分发。 Linux 从内核3.8开始支持 F2FS 。

## Contents

*   [1 创建 F2FS 分区](#.E5.88.9B.E5.BB.BA_F2FS_.E5.88.86.E5.8C.BA)
*   [2 挂载 F2FS 分区](#.E6.8C.82.E8.BD.BD_F2FS_.E5.88.86.E5.8C.BA)
*   [3 扩展 F2FS 分区](#.E6.89.A9.E5.B1.95_F2FS_.E5.88.86.E5.8C.BA)
*   [4 Checking and repair](#Checking_and_repair)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 GRUB with root on F2FS](#GRUB_with_root_on_F2FS)

## 创建 F2FS 分区

创建 F2FS 分区，首先 [install](/index.php/Install "Install") [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools).

用下面的命令创建一个分区:

```
# mkfs.f2fs -l mylabel */dev/sdxY*

```

`*/dev/sdxY*` 是想要设置成 F2FS 的分区。 详细信息参阅 [mkfs.f2fs(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.f2fs.8)。

## 挂载 F2FS 分区

使用手动或是其他机制挂载分区:

```
# mount /dev/sdxY /mnt/foo

```

## 扩展 F2FS 分区

如果文件系统未被挂载，如果扩展分区，则可以增长文件系统。 [目前不支持收缩](https://www.mail-archive.com/linux-f2fs-devel@lists.sourceforge.net/msg04247.html). 首先使用 [分区工具](/index.php/Partitioning#Partitioning_tools "Partitioning")调整分区大小。例如，可以通过删除旧分区并创建一个具有相同分区类型、相同起始扇区和新的结束位置的新分区来完成此操作。

然后扩展文件系统来填充新的分区，使用以下命令:

```
# resize.f2fs /dev/sdxY

```

`*/dev/sdxY*`是要增长的 F2FS 分区. 可用的选项参阅 [resize.f2fs(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/resize.f2fs.8)。

**注意:** 如果使用 GPT, 分区的 GUID (`/dev/disk/by-partuuid/` 内) 可能会改变, 但是文件系统的 UUID (`/dev/disk/by-uuid/` 内) 应该保持不变。

## Checking and repair

Checking and repairs to f2fs partitions are accomplished with `fsck.f2fs` provided by [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools). See [fsck.f2fs(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/fsck.f2fs.8) for available switches.

## Troubleshooting

### GRUB with root on F2FS

When using [GRUB](/index.php/GRUB "GRUB") your freshly installed system might not boot after reboot. As GRUB does not support F2FS it is not able to extract the [UUID](/index.php/UUID "UUID") of your drive so it uses classic non-persistent `/dev/*sdXx*` names instead. In this case you might have to manually edit `/boot/grub/grub.cfg` and replace `root=/dev/*sdXx*` with `root=UUID=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*`. You can use the `blkid` command to get the UUID of your device, see [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").