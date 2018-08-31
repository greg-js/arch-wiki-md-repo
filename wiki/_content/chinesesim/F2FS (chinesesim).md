Related articles

*   [File systems](/index.php/File_systems "File systems")

**翻译状态：** 本文是英文页面 [F2FS](/index.php/F2FS "F2FS") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-12-01，点击[这里](https://wiki.archlinux.org/index.php?title=F2FS&diff=0&oldid=499311)可以查看翻译后英文页面的改动。

[F2FS](https://en.wikipedia.org/wiki/F2FS "wikipedia:F2FS") (Flash-Friendly File System) 是一个为配备了 Flash Transition Layer 的 NAND 闪存开发的文件系统，与 JFFS 或 UBIFS 不同，它依靠 FTL 来处理写入分发。 Linux 从内核3.8开始支持 F2FS 。

## Contents

*   [1 创建 F2FS 文件系统](#.E5.88.9B.E5.BB.BA_F2FS_.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
*   [2 挂载 F2FS 文件系统](#.E6.8C.82.E8.BD.BD_F2FS_.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
*   [3 扩展 F2FS 文件系统](#.E6.89.A9.E5.B1.95_F2FS_.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
*   [4 检查和修复](#.E6.A3.80.E6.9F.A5.E5.92.8C.E4.BF.AE.E5.A4.8D)
*   [5 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [5.1 在 F2FS 上使用 GRUB](#.E5.9C.A8_F2FS_.E4.B8.8A.E4.BD.BF.E7.94.A8_GRUB)

## 创建 F2FS 文件系统

要创建 F2FS 文件系统，首先 [安装](/index.php/Install "Install") 软件包 [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools).

用下面的命令创建一个文件系统:

```
# mkfs.f2fs -l mylabel */dev/sdxY*

```

`*/dev/sdxY*` 是想要设置成 F2FS 的分区。详细信息请参阅 [mkfs.f2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.f2fs.8)。

## 挂载 F2FS 文件系统

使用手动或是其他机制挂载文件系统:

```
# mount /dev/sdxY /mnt/foo

```

## 扩展 F2FS 文件系统

如果文件系统未被挂载，如果扩展分区，则可以增长文件系统。 [目前不支持压缩](https://www.mail-archive.com/linux-f2fs-devel@lists.sourceforge.net/msg04247.html)。 首先使用[分区工具](/index.php/Partitioning#Partitioning_tools "Partitioning")调整分区大小。例如，可以通过删除旧分区并创建一个具有相同分区类型、相同起始扇区和新的结束位置的新分区来完成此操作。

然后扩展文件系统来填充新的分区，使用以下命令:

```
# resize.f2fs /dev/sdxY

```

`*/dev/sdxY*`是要增长的 F2FS 分区。可用的选项参阅 [resize.f2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resize.f2fs.8)。

**注意:** 如果使用 GPT，分区的 GUID (`/dev/disk/by-partuuid/` 内) 可能会改变，但是文件系统的 UUID (`/dev/disk/by-uuid/` 内) 应该保持不变。

## 检查和修复

软件包 [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) 中的 `fsck.f2fs` 命令可以检查和修复 f2fs 文件系统。可用的选项请参阅 [fsck.f2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fsck.f2fs.8)。

## 疑难解答

### 在 F2FS 上使用 GRUB

使用 [GRUB](/index.php/GRUB "GRUB") 时，新安装的系统在重启后可能无法启动。 由于 GRUB 不支持 F2FS ，所以无法识别驱动器的 [UUID](/index.php/UUID "UUID") ，因此它使用经典的非持久性 `/dev/*sdXx*` 命名方式代替。 在这种情况下，您可能必须手动编辑 `/boot/grub/grub.cfg` 文件，并使用 `root=UUID=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*` 替换 `root=/dev/*sdXx*`。可以使用 `blkid` 命令获取设备的UUID，请参见 [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming")。