**翻译状态：** 本文是英文页面 [EFI_System_Partition](/index.php/EFI_System_Partition "EFI System Partition") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-07-31，点击[这里](https://wiki.archlinux.org/index.php?title=EFI_System_Partition&diff=0&oldid=441553)可以查看翻译后英文页面的改动。

[EFI 系统分区](https://en.wikipedia.org/wiki/EFI_System_partition "wikipedia:EFI System partition")(也称为 ESP 或者 EFISYS)是一个 FAT32 格式的物理分区 (在硬盘主分区表上，而不是 LVM 或软件 RAID 等等) ，从这里 [UEFI](/index.php/UEFI "UEFI") 固件启动 UEFI 引导器和应用程序。

它与操作系统无关而是作为 EFI 固件要启动的引导器和应用程序的存储空间，是 UEFI 启动所必须。

推荐使用 GPT 和 UEFI 搭配因为有的 UEFI 固件不支持 UEFI-MBR 启动。

**Warning:** 如果在 UEFI/GPT 系统上配置 [双启动](/index.php/Dual_boot_with_Windows "Dual boot with Windows")，请不要重新格式化 UEFI 分区，因为已有的分区上包含 Windows 启动需要的 *.efi* 文件。不需要重新创建分区，只需要 [#挂载分区](#挂载分区).

## Contents

*   [1 创建分区](#创建分区)
    *   [1.1 GPT 磁盘分区](#GPT_磁盘分区)
    *   [1.2 MBR 磁盘分区](#MBR_磁盘分区)
*   [2 挂载分区](#挂载分区)
    *   [2.1 RAID 上的 ESP](#RAID_上的_ESP)
*   [3 技巧](#技巧)
    *   [3.1 Using bind mount](#Using_bind_mount)
*   [4 参阅](#参阅)

## 创建分区

推荐 ESP 大小为 512 MiB， 不过大一点小一点都没问题。

Microsoft 文献注解了 ESP 大小: 对高级格式化 (Advanced Format) 4K 本地驱动器 (每扇区4KB) 来说，由于 FAT32 文件格式的限制，最小为 260 MB。 FAT32 的最小分区大小可由扇区大小 (4KB) x 65527 = 算出 256 MB。高级格式化 512e 驱动器不受此限制影响，因为其虚拟扇区是 512B. 512 bytes x 65527 = 32 MB, 这比 100 MB 最小限制还要小。[[1]](http://technet.microsoft.com/en-us/library/hh824839.aspx#DiskPartitionRules)

### GPT 磁盘分区

*   **fdisk**/**gdisk**: 创建类型为 EFI System (`EFI System` (在 *fdisk* 中) 或 `ef00` (在 *gdisk* 中)的分区。然后运行 `mkfs.fat -F32 /dev/<THAT_PARTITION>` 格式化为 FAT32 格式。

(或)

*   [GNU Parted](/index.php/GNU_Parted "GNU Parted"): 创建一个 FAT32 分区然后在 Parted 中为那个分区设置/激活 `boot` 参数 (不是 `legacy_boot` 参数).

**注意:** 如果你收到消息 `WARNING: Not enough clusters for a 32 bit FAT!`, 运行 `mkfs.fat -s2 -F32 ...` 或 `-s1` 以减小簇大小，否则 UEFI 无法读取分区。

### MBR 磁盘分区

**fdisk**: 使用 fdisk 创建类型为 *EFI System* 的分区，然后运行 `mkfs.fat -F32 /dev/<THAT_PARTITION>` 格式化为 FAT32.

## 挂载分区

为防止 [EFISTUB](/index.php/EFISTUB "EFISTUB"), 内核以及 initramfs 文件应储存在 EFI 系统分区。精简起见，当以 EFISTUB 启动时你可以把 ESP 当做 `/boot` 分区而不是单独分一个 `/boot` 分区。 }}

### RAID 上的 ESP

将 ESP 包含进 RAID1 组是可行的，但是会有数据污染的危险，创建 ESP 时请三思。 细节见 [https://bbs.archlinux.org/viewtopic.php?pid=1398710#p1398710](https://bbs.archlinux.org/viewtopic.php?pid=1398710#p1398710) 和 [https://bbs.archlinux.org/viewtopic.php?pid=1390741#p1390741](https://bbs.archlinux.org/viewtopic.php?pid=1390741#p1390741).

## 技巧

### Using bind mount

除了直接将 ESP 挂载到 `/boot`，还可以将 ESP 中的某个目录 bind mount 挂载到 `/boot`(参考 `mount(8)`). 用这种方式，pacman 可以直接更新目录，而 ESP 分区上的文件可以按照需要进行放置，这个方式比文件复制要简单的多。

**Note:** 这种做法需要兼容FAT32的内核和引导。通常来说Arch都没问题， 但是其他发行版可能会有 (namely those that require symlinks in `/boot`). 讨论帖 [在这里](https://bbs.archlinux.org/viewtopic.php?pid=1331867#p1331867).

参考 [EFISTUB#Alternative ESP Mount Points](/index.php/EFISTUB#Alternative_ESP_Mount_Points "EFISTUB"), 将所有文件复制到 ESP 下的某个目录，将 ESP 挂载到 `/boot` 之外的地方 (例如 `/esp`)。然后 bind mount 目录：

```
# mount --bind /esp/EFI/arch/ /boot

```

这样 `/boot` 下就有了你需要的文件，编辑 [Fstab](/index.php/Fstab "Fstab")：

 `/etc/fstab` 
```
/esp/EFI/arch /boot none defaults,bind 0 0

```

**Warning:** 必须使用 `root=*system_root*` [内核参数](/index.php/Kernel_parameters#Parameter_list "Kernel parameters") 才能通过此方法启动。

## 参阅

*   [The EFI System Partition and the Default Boot Behavior](http://blog.uncooperative.org/blog/2014/02/06/the-efi-system-partition/)