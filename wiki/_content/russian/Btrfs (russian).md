**Состояние перевода:** На этой странице представлен перевод статьи [Btrfs](/index.php/Btrfs "Btrfs"). Дата последней синхронизации: 30 октября 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Btrfs&diff=0&oldid=455472).

Из [Wikipedia:Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs"):

	Btrfs (файловая система основанная на структурах B-деревьев, произносится как "butter F S", "better F S", "b-tree F S", или просто как аббревиатура) эта файловая система работает по принципу «копирование при записи» (COW), первоначально разработанная Oracle Corporation для использования в Linux. Разработка Btrfs началась в 2007, а в августе 2014 файловая система была помечена как стабильная.

Из [Btrfs Wiki](https://btrfs.wiki.kernel.org/index.php/Main_Page):

	Btrfs это новая файловая система для Linux с принципом копирования при записи (CoW), направленная на реализацию дополнительных функций с особым упором на отказоустойчивость, восстановление и простоту администрирования. Совместная разработка Oracle, Red Hat, Fujitsu, Intel, SUSE, STRATO и многих других, Btrfs распространяется под лицензией GPL, что позволяет внести свой вклад любому желающему.

**Важно:** Btrfs содержит некоторые возможности, считающиеся экспериментальными. За подробностями, пройдите по ссылкам Btrfs Wiki's [Статус](https://btrfs.wiki.kernel.org/index.php/Status), [Btrfs стабильна?](https://btrfs.wiki.kernel.org/index.php/FAQ#Is_btrfs_stable.3F) и [Начинаем](https://btrfs.wiki.kernel.org/index.php/Getting_started). Смотрите раздел [#Известные проблемы](#.D0.98.D0.B7.D0.B2.D0.B5.D1.81.D1.82.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B).

## Contents

*   [1 Подготовка](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Создание раздела диска Btrfs](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.B0_.D0.B4.D0.B8.D1.81.D0.BA.D0.B0_Btrfs)
*   [3 Создание файловой системы](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.BE.D0.B9_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
    *   [3.1 Создание новой файловой системы](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BD.D0.BE.D0.B2.D0.BE.D0.B9_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.BE.D0.B9_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
        *   [3.1.1 Файловая система на одном устройстве](#.D0.A4.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.B0.D1.8F_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0_.D0.BD.D0.B0_.D0.BE.D0.B4.D0.BD.D0.BE.D0.BC_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B5)
        *   [3.1.2 Файловая система на нескольких устройствах](#.D0.A4.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.B0.D1.8F_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0_.D0.BD.D0.B0_.D0.BD.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.B8.D1.85_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0.D1.85)
    *   [3.2 Конвертация Ext3/4 в Btrfs](#.D0.9A.D0.BE.D0.BD.D0.B2.D0.B5.D1.80.D1.82.D0.B0.D1.86.D0.B8.D1.8F_Ext3.2F4_.D0.B2_Btrfs)
*   [4 Настройка файловой системы](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.BE.D0.B9_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
    *   [4.1 Копирование при записи (CoW)](#.D0.9A.D0.BE.D0.BF.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D0.B8_.28CoW.29)
        *   [4.1.1 Отключение CoW](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_CoW)
        *   [4.1.2 Принудительное CoW](#.D0.9F.D1.80.D0.B8.D0.BD.D1.83.D0.B4.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D0.B5_CoW)
    *   [4.2 Сжатие](#.D0.A1.D0.B6.D0.B0.D1.82.D0.B8.D0.B5)
    *   [4.3 Подтома](#.D0.9F.D0.BE.D0.B4.D1.82.D0.BE.D0.BC.D0.B0)
        *   [4.3.1 Создание подтома](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.B4.D1.82.D0.BE.D0.BC.D0.B0)
        *   [4.3.2 Просмотр подтомов](#.D0.9F.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80_.D0.BF.D0.BE.D0.B4.D1.82.D0.BE.D0.BC.D0.BE.D0.B2)
        *   [4.3.3 Удаление подтома](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.B4.D1.82.D0.BE.D0.BC.D0.B0)
        *   [4.3.4 Монтирование подтомов](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.B4.D1.82.D0.BE.D0.BC.D0.BE.D0.B2)
            *   [4.3.4.1 Опции монтирования](#.D0.9E.D0.BF.D1.86.D0.B8.D0.B8_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
        *   [4.3.5 Changing the default sub-volume](#Changing_the_default_sub-volume)
    *   [4.4 Commit Interval](#Commit_Interval)
    *   [4.5 SSD TRIM](#SSD_TRIM)
*   [5 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [5.1 Показать использованное/свободное место](#.D0.9F.D0.BE.D0.BA.D0.B0.D0.B7.D0.B0.D1.82.D1.8C_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.BD.D0.BE.D0.B5.2F.D1.81.D0.B2.D0.BE.D0.B1.D0.BE.D0.B4.D0.BD.D0.BE.D0.B5_.D0.BC.D0.B5.D1.81.D1.82.D0.BE)
    *   [5.2 Дефрагментация](#.D0.94.D0.B5.D1.84.D1.80.D0.B0.D0.B3.D0.BC.D0.B5.D0.BD.D1.82.D0.B0.D1.86.D0.B8.D1.8F)
    *   [5.3 RAID](#RAID)
        *   [5.3.1 Scrub](#Scrub)
            *   [5.3.1.1 Start manually](#Start_manually)
            *   [5.3.1.2 Запуск службы или таймера](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D1.81.D0.BB.D1.83.D0.B6.D0.B1.D1.8B_.D0.B8.D0.BB.D0.B8_.D1.82.D0.B0.D0.B9.D0.BC.D0.B5.D1.80.D0.B0)
        *   [5.3.2 Balance](#Balance)
    *   [5.4 Снимки](#.D0.A1.D0.BD.D0.B8.D0.BC.D0.BA.D0.B8)
    *   [5.5 Отправить / получить](#.D0.9E.D1.82.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D1.82.D1.8C_.2F_.D0.BF.D0.BE.D0.BB.D1.83.D1.87.D0.B8.D1.82.D1.8C)
*   [6 Известные проблемы](#.D0.98.D0.B7.D0.B2.D0.B5.D1.81.D1.82.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B)
    *   [6.1 Шифрование](#.D0.A8.D0.B8.D1.84.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [6.2 Файл подкачки (Swap)](#.D0.A4.D0.B0.D0.B9.D0.BB_.D0.BF.D0.BE.D0.B4.D0.BA.D0.B0.D1.87.D0.BA.D0.B8_.28Swap.29)
    *   [6.3 Ядро Linux-rt](#.D0.AF.D0.B4.D1.80.D0.BE_Linux-rt)
*   [7 Tips and tricks](#Tips_and_tricks)
    *   [7.1 Corruption recovery](#Corruption_recovery)
    *   [7.2 Загрузка в снимки с помощью GRUB](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.B2_.D1.81.D0.BD.D0.B8.D0.BC.D0.BA.D0.B8_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_GRUB)
    *   [7.3 Использование подтомов Btrfs с systemd-nspawn](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.B4.D1.82.D0.BE.D0.BC.D0.BE.D0.B2_Btrfs_.D1.81_systemd-nspawn)
*   [8 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [8.1 GRUB](#GRUB)
        *   [8.1.1 Смещение разделов](#.D0.A1.D0.BC.D0.B5.D1.89.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.BE.D0.B2)
        *   [8.1.2 Отсутствует root](#.D0.9E.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D0.B5.D1.82_root)
    *   [8.2 Ошибка BTRFS: open_ctree failed](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_BTRFS:_open_ctree_failed)
    *   [8.3 Проверка btrfs](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_btrfs)
*   [9 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Подготовка

The official kernels [linux](https://www.archlinux.org/packages/?name=linux) and [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) include support for Btrfs. If you want to boot from a Btrfs file system, check if your [boot loader](/index.php/Boot_loader "Boot loader") supports Btrfs.

User space utilities are available by [installing](/index.php/Installing "Installing") the [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) package.

## Создание раздела диска Btrfs

Btrfs can occupy an entire data storage device, replacing the [MBR](/index.php/MBR "MBR") or [GPT](/index.php/GPT "GPT") partitioning schemes, using [subvolumes](#Subvolumes) to simulate partitions. However, using a partitionless setup is not required to simply [create a Btrfs filesystem](#Creating_a_new_file_system) on an existing [partition](/index.php/Partition "Partition") that was created using another method. There are some limitations to partitionless single disk setups:

*   Cannot use different [file systems](/index.php/File_systems "File systems") for different [mount points](/index.php/Fstab "Fstab").
*   Cannot use [swap area](/index.php/Swap "Swap") as Btrfs does not support [swap files](/index.php/Swap#Swap_file "Swap") and there is no place to create [swap partition](/index.php/Swap#Swap_partition "Swap"). This also limits the use of hibernation/resume, which needs a swap area to store the hibernation image.
*   Cannot use [UEFI](/index.php/UEFI "UEFI") to boot.

To overwrite the existing partition table with Btrfs, run the following command:

```
# mkfs.btrfs /dev/sd*X*

```

For example, use `/dev/sda` rather than `/dev/sda1`. The latter would format an existing partition instead of replacing the entire partitioning scheme.

Install the [boot loader](/index.php/Boot_loader "Boot loader") like you would for a data storage device with a [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record"). See [Syslinux#Manual install](/index.php/Syslinux#Manual_install "Syslinux") or [GRUB#Install to partition or partitionless disk](/index.php/GRUB#Install_to_partition_or_partitionless_disk "GRUB").

**Важно:** GRUB strongly discourages installation to a partitionless disk.

## Создание файловой системы

A Btrfs file system can either be newly created or have one converted.

### Создание новой файловой системы

#### Файловая система на одном устройстве

To format a partition do:

```
# mkfs.btrfs -L *mylabel* /dev/*partition*

```

The Btrfs default blocksize is 16KB. To use a larger blocksize for data/metadata, specify a value for the `nodesize` via the `-n` switch as shown in this example using 16KB blocks:

```
# mkfs.btrfs -L *mylabel* -n 16k /dev/*partition*

```

#### Файловая система на нескольких устройствах

**Важно:**

*   As of August 2016, the RAID 5, RAID 6 mode of Btrfs is considered *fatally flawed*, and shouldn't be used for "anything but testing with throw-away data." [[1]](https://www.mail-archive.com/linux-btrfs@vger.kernel.org/msg55161.html)
*   Some [boot loaders](/index.php/Boot_loader "Boot loader") such as [Syslinux](/index.php/Syslinux "Syslinux") do not support multi-device file systems.

Multiple devices can be entered to create a RAID. Supported RAID levels include RAID 0, RAID 1, RAID 10, RAID 5 and RAID 6\. The RAID levels can be configured separately for data and metadata using the `-d` and `-m` options respectively. By default the data is striped (`raid0`) and the metadata is mirrored (`raid1`). See [Using Btrfs with Multiple Devices](https://btrfs.wiki.kernel.org/index.php/Using_Btrfs_with_Multiple_Devices) for more information about how to create a Btrfs RAID volume as well as the manpage for `mkfs.btrfs`.

```
# mkfs.btrfs -d raid0 -m raid1 /dev/*part1* /dev/*part2* ...

```

You **must** include either the `udev` hook or the `btrfs` hook in `/etc/mkinitcpio.conf` in order to use multiple btrfs devices in a pool. See the [Mkinitcpio#Common hooks](/index.php/Mkinitcpio#Common_hooks "Mkinitcpio") article for more information.

**Примечание:** If the disks in your multi-disk array have different sizes, this may not use the full capacity of all drives. In order to utilize the full capacity of all disks, use `-d single` instead of `-d raid0 -m raid1` (metadata mirrored, data not mirrored and not striped)

**Примечание:** Mounting such a filesystem may result in all but one of the according *.device*-jobs getting stuck and systemd never finishing startup due to a [bug](https://github.com/systemd/systemd/issues/1921) in handling this type of filesystem.

See [#RAID](#RAID) for advice on maintenance specific to multi-device Btrfs file systems.

### Конвертация Ext3/4 в Btrfs

**Важно:** As of mid-to-late 2015, there are many reports on the btrfs mailing list about incomplete/corrupt/broken conversions. The situation is improving as patches are being submitted, but proceed very carefully. Make sure you have *working* backups of any data you cannot afford to lose. See [Conversion from Ext3](https://btrfs.wiki.kernel.org/index.php/Conversion_from_Ext3) on the btrfs wiki.

Boot from an install CD, then convert by doing:

```
# btrfs-convert /dev/*partition*

```

Mount the partion and test the conversion by checking the files. Be sure to change the `/etc/fstab` to reflect the change (**type** to `btrfs` and **fs_passno** [the last field] to `0` as Btrfs does not do a file system check on boot). Also note that the UUID of the partition will have changed, so update fstab accordingly when using UUIDs. `chroot` into the system and rebuild the GRUB menu list (see [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux") and [GRUB](/index.php/GRUB "GRUB") articles). If converting a root filesystem, while still chrooted run `mkinitcpio -p linux` to regenerate the initramfs or the system will not successfully boot. If you get stuck in grub with 'unknown filesystem' try reinstalling grub with `grub-install /dev/*partition*` and regenerate the config as well `grub-mkconfig -o /boot/grub/grub.cfg`.

After confirming that there are no problems, complete the conversion by deleting the backup `ext2_saved` sub-volume. Note that you cannot revert back to ext3/4 without it.

```
# btrfs subvolume delete /ext2_saved

```

Finally [balance](#Balance) the file system to reclaim the space.

## Настройка файловой системы

### Копирование при записи (CoW)

By default, Btrfs uses [Wikipedia:copy-on-write](https://en.wikipedia.org/wiki/copy-on-write "wikipedia:copy-on-write") for all files all the time. See [the Btrfs Sysadmin Guide section](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Copy_on_Write_.28CoW.29) for implementation details, as well as advantages and disadvantages.

#### Отключение CoW

To disable copy-on-write for newly created files in a mounted subvolume, use the `nodatacow` mount option. This will only affect newly created files. Copy-on-write will still happen for existing files.

To disable copy-on-write for single files/directories do:

```
$ chattr +C */dir/file*

```

This will disable copy-on-write for those operation in which there is only one reference to the file. If there is more than one reference (e.g. through `cp --reflink=always` or because of a filesystem snapshot), copy-on-write still occurs.

**Примечание:** From chattr man page: "For btrfs, the 'C' flag should be set on new or empty files. If it is set on a file which already has data blocks, it is undefined when the blocks assigned to the file will be fully stable. If the 'C' flag is set on a directory, it will have no effect on the directory, but new files created in that directory will have the No_COW attribute."

**Совет:** In accordance with the note above, you can use the following trick to disable copy-on-write on existing files in a directory:
```
$ mv */path/to/dir* */path/to/dir*_old
$ mkdir */path/to/dir*
$ chattr +C */path/to/dir*
$ cp -a */path/to/dir*_old/* */path/to/dir*
$ rm -rf */path/to/dir*_old

```

Make sure that the data are not used during this process. Also note that `mv` or `cp --reflink` as described below will not work.

#### Принудительное CoW

To force copy-on-write when copying files use:

```
$ cp --reflink *source* *dest* 

```

This would only be required if CoW was disabled for the file to be copied (as implemented above). See the man page on `cp` for more details on the `--reflink` flag.

### Сжатие

Btrfs supports transparent compression, meaning every file on the partition is automatically compressed. This not only reduces the size of files, but also [improves performance](http://www.phoronix.com/scan.php?page=article&item=btrfs_compress_2635&num=1), in particular if using the [lzo algorithm](http://www.phoronix.com/scan.php?page=article&item=btrfs_lzo_2638&num=1), in some specific use cases (e.g. single thread with heavy file IO), while obviously harming performance on other cases (e.g. multithreaded and/or cpu intensive tasks with large file IO).

Compression is enabled using the `compress=zlib` or `compress=lzo` mount options. Only files created or modified after the mount option is added will be compressed. However, it can be applied quite easily to existing files (e.g. after a conversion from ext3/4) using the `btrfs filesystem defragment -c*alg*` command, where `*alg*` is either `zlib` or `lzo`. In order to re-compress the whole file system with [lzo](https://www.archlinux.org/packages/?name=lzo), run the following command:

```
# btrfs filesystem defragment -r -v -clzo /

```

**Совет:** Compression can also be enabled per-file without using the `compress` mount option; simply apply `chattr +c` to the file. When applied to directories, it will cause new files to be automatically compressed as they come.

When installing Arch to an empty Btrfs partition, use the `compress` option when [mounting](/index.php/Mount "Mount") the file system: `mount -o compress=lzo /dev/sd*xY* /mnt/`. During configuration, add `compress=lzo` to the mount options of the root file system in [fstab](/index.php/Fstab "Fstab").

### Подтома

"A btrfs подтома (subvolume) is not a block device (and cannot be treated as one) instead, a btrfs subvolume can be thought of as a POSIX file namespace. This namespace can be accessed via the top-level subvolume of the filesystem, or it can be mounted in its own right." [[2]](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Subvolumes)

Each Btrfs file system has a top-level subvolume with ID 5\. It can be mounted as `/` (by default), or another subvolume can be [mounted](#Mounting_subvolumes) instead.

See the following links for more details:

*   [Btrfs Wiki SysadminGuide#Subvolumes](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Subvolumes)
*   [Btrfs Wiki Getting started#Basic Filesystem Commands](https://btrfs.wiki.kernel.org/index.php/Getting_started#Basic_Filesystem_Commands)
*   [Btrfs Wiki Trees](https://btrfs.wiki.kernel.org/index.php/Trees)

#### Создание подтома

To create a subvolume:

```
# btrfs subvolume create */path/to/subvolume*

```

#### Просмотр подтомов

To see a list of current subvolumes under `*path*`:

```
# btrfs subvolume list -p *path*

```

#### Удаление подтома

To delete a subvolume:

```
# btrfs subvolume delete */path/to/subvolume*

```

Attempting to remove the directory `*/path/to/subvolume*` without using the above command will not delete the subvolume.

#### Монтирование подтомов

Subvolumes can be mounted like file system partitions using the `subvol=*/path/to/subvolume*` or `subvolid=*objectid*` mount flags. For example, you could have a subvolume named `subvol_root` and mount it as `/`. One can mimic traditional file system partitions by creating various subvolumes under the top level of the file system and then mounting them at the appropriate mount points. Thus one can easily restore a file system (or part of it) to a previous state easily using [#Snapshots](#Snapshots).

**Совет:** Changing subvolume layouts is made simpler by not using the toplevel subvolume (ID=5) as `/` (which is done by default). Instead, consider creating a subvolume to house your actual data and mounting it as `/`.

See [Snapper#Suggested filesystem layout](/index.php/Snapper#Suggested_filesystem_layout "Snapper"), [Btrfs SysadminGuide#Managing Snapshots](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Managing_Snapshots), and [Btrfs SysadminGuide#Layout](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Layout) for example file system layouts using subvolumes.

##### Опции монтирования

When mounting subvolumes with `subvol=` several mount options are available. For example, mount options that affect [#Compression](#Compression) or [#Copy-On-Write (CoW)](#Copy-On-Write_.28CoW.29) can be used.

See [Btrfs Wiki Mount options](https://btrfs.wiki.kernel.org/index.php/Mount_options) and [Btrfs Wiki Gotchas](https://btrfs.wiki.kernel.org/index.php/Gotchas) for more information. In addition to configurations that can be made during or after file system creation, the various mount options for Btrfs can drastically change its performance characteristics. As this is a file system that is still in active development, changes and regressions should be expected. See links in the [#See also](#See_also) section for some benchmarks.

**Важно:** Specific mount options can disable safety features and increase the risk of complete file system corruption.

#### Changing the default sub-volume

The default sub-volume is mounted if no `subvol=` mount option is provided. To change the default subvolume, do:

```
# btrfs subvolume set-default *subvolume-id* /

```

where *subvolume-id* can be found by [listing](#Listing_subvolumes).

**Примечание:** After changing the default subvolume on a system with [GRUB](/index.php/GRUB "GRUB"), you should run `grub-install` again to notify the bootloader of the changes. See [this forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1615373).

**Важно:** Changing the default subvolume with `btrfs subvolume set-default` will make the top level of the filesystem inaccessible when the default subvolume is mounted . Reference: [Btrfs Wiki Sysadmin Guide](https://btrfs.wiki.kernel.org/index.php/SysadminGuide).

### Commit Interval

The resolution at which data are written to the filesystem is dictated by Btrfs itself and by system-wide settings. Btrfs defaults to a 30 seconds checkpoint interval in which new data are committed to the filesystem. This can be changed by appending the `commit` mount option in `/etc/fstab` for the btrfs partition.

```
LABEL=arch64 / btrfs defaults,noatime,ssd,compress=lzo,commit=120 0 0

```

System-wide settings also affect commit intervals. They include the files under `/proc/sys/vm/*` and are out-of-scope of this wiki article. The kernel documentation for them resides in `Documentation/sysctl/vm.txt`.

### SSD TRIM

A Btrfs filesystem will automatically free unused blocks from an SSD drive supporting the TRIM command.

More information about enabling and using TRIM can be found in [Solid State Drives#TRIM](/index.php/Solid_State_Drives#TRIM "Solid State Drives").

## Использование

### Показать использованное/свободное место

General linux userspace tools such as `/usr/bin/df` will inaccurately report free space on a Btrfs partition since it does not take into account space allocated for and used by the metadata. It is recommended to use `/usr/bin/btrfs` to query a Btrfs partition. Below is an illustration of this effect, first querying using `df -h`, and then using `btrfs filesystem df`:

 `$ df -h /` 
```
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda3       119G  3.0G  116G   3% /

```
 `$ btrfs filesystem df /` 
```
Data: total=3.01GB, used=2.73GB
System: total=4.00MB, used=16.00KB
Metadata: total=1.01GB, used=181.83MB
```

Notice that `df -h` reports 3.0GB used but `btrfs filesystem df` reports 2.73GB for the data. This is due to the way Btrfs allocates space into the pool. The true disk usage is the sum of all three 'used' values which is inferior to 3.0GB as reported by `df -h`.

**Примечание:** If you see an entry of type `unknown` in the output of `btrfs filesystem df` at kernel >= 3.15, this is a display bug. As of [this patch](http://thread.gmane.org/gmane.comp.file-systems.btrfs/34419), the entry means GlobalReserve, which is kind of a buffer for changes not yet flushed. This entry is displayed as `unknown, single` in RAID setups and is not possible to re-balance.

Another useful command to show a less verbose readout of used space is `btrfs filesystem show`:

```
# btrfs filesystem show /dev/sda3

```

The newest command to get information on free/used space of a is `btrfs filesystem usage`:

```
# btrfs filesystem usage

```

**Примечание:** The `btrfs filesystem usage` command does not currently work correctly with `RAID5/RAID6` RAID levels.

### Дефрагментация

Btrfs supports online defragmentation. To defragment the metadata of the root folder:

```
# btrfs filesystem defragment /

```

This *will not* defragment the entire file system. For more information read [this page](https://btrfs.wiki.kernel.org/index.php/Problem_FAQ#Defragmenting_a_directory_doesn.27t_work) on the Btrfs wiki.

To defragment the entire file system verbosely:

```
# btrfs filesystem defragment -r -v /

```

### RAID

Btrfs offers native "RAID" for [#Multi-device file systems](#Multi-device_file_system). Notable features which set btrfs RAID apart from [mdadm](/index.php/Mdadm "Mdadm") are self-healing redundant arrays and online balancing. See [the Btrfs wiki page](https://btrfs.wiki.kernel.org/index.php/Using_Btrfs_with_Multiple_Devices) for more information. The Btrfs sysadmin page also [has a section](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#RAID_and_data_replication) with some more technical background.

**Важно:** Parity RAID (RAID 5/6) code has multiple serious data-loss bugs in it. See the Btrfs Wiki's [RAID5/6 page](https://btrfs.wiki.kernel.org/index.php/RAID56) and a bug report on [linux-btrfs mailing list](https://www.mail-archive.com/linux-btrfs@vger.kernel.org/msg55161.html) for more detailed information.

#### Scrub

The [Btrfs Wiki Glossary](https://btrfs.wiki.kernel.org/index.php/Glossary) says that Btrfs scrub is "[a]n online filesystem checking tool. Reads all the data and metadata on the filesystem, and uses checksums and the duplicate copies from RAID storage to identify and repair any corrupt data."

**Важно:** A running scrub process will prevent the system from suspending, see [this thread](http://comments.gmane.org/gmane.comp.file-systems.btrfs/33106) for details.

##### Start manually

To start a scrub for the subvolume mounted at root do:

```
# btrfs scrub start /

```

To check the status of the scrub do:

```
# btrfs scrub status /

```

##### Запуск службы или таймера

The [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) package brings the `btrfs-scrub@.timer` unit for monthly scrubbing the specified mountpoint. [Enable](/index.php/Enable "Enable") the timer with an escaped path, e.g. `btrfs-scrub@-.timer` for `/` and `btrfs-scrub@home.timer` for `/home`. You can use the *systemd-escape* tool to escape a given string, see `systemd-escape(1)` for examples.

You can also run the scrub by [starting](/index.php/Starting "Starting") `btrfs-scrub@.service` (with the same encoded path). The advantage of this over `# btrfs scrub` is that the results of the scrub will be logged in the [systemd journal](/index.php/Systemd_journal "Systemd journal").

#### Balance

"A balance passes all data in the filesystem through the allocator again. It is primarily intended to rebalance the data in the filesystem across the devices when a device is added or removed. A balance will regenerate missing copies for the redundant RAID levels, if a device has failed." [[4]](https://btrfs.wiki.kernel.org/index.php/Glossary) See [Upstream FAQ page](https://btrfs.wiki.kernel.org/index.php/FAQ#What_does_.22balance.22_do.3F).

```
# btrfs balance start /
# btrfs balance status /

```

### Снимки

"A snapshot is simply a subvolume that shares its data (and metadata) with some other subvolume, using btrfs's COW capabilities." See [Btrfs Wiki SysadminGuide#Snapshots](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Snapshots) for details.

To create a snapshot:

```
# btrfs subvolume snapshot *source* [*dest*/]*name*

```

To create a readonly snapshot add the `-r` flag. To create writable version of a readonly snapshot, simply create a snapshot of it.

**Примечание:** Snapshots are not recursive. Every sub-volume inside sub-volume will be an empty directory inside the snapshot.

### Отправить / получить

A subvolume can be sent to stdout or a file using the `send` command. This is usually most useful when piped to a Btrfs `receive` command. For example, to send a snapshot named `/root_backup` (perhaps of a snapshot you made of `/` earlier) to `/backup` you would do the following:

```
 # btrfs send /root_backup | btrfs receive /backup

```

The snapshot that is sent *must* be readonly. The above command is useful for copying a subvolume to an external device (*e.g.*, a USB disk mounted at `/backup` above).

You can also send only the difference between two snapshots. For example, if you have already sent a copy of `root_backup` above and have made a new readonly snapshot on your system named `root_backup_new`, then to send only the incremental difference to `/backup` do:

```
 # btrfs send -p /root_backup /root_backup_new | btrfs receive /backup

```

Now a new subvolume named `root_backup_new` will be present in `/backup`.

See [Btrfs Wiki's Incremental Backup page](https://btrfs.wiki.kernel.org/index.php/Incremental_Backup) on how to use this for an incremental backup and for tools that automate the process.

## Известные проблемы

Несколько ограничений должны быть известны перед использованием.

### Шифрование

Btrfs has no built-in encryption support, but this may come in future. Users can encrypt the partition before running `mkfs.btrfs`. See [dm-crypt/Encrypting an entire system#Btrfs subvolumes with swap](/index.php/Dm-crypt/Encrypting_an_entire_system#Btrfs_subvolumes_with_swap "Dm-crypt/Encrypting an entire system").

Existing Btrfs file systems can use something like [EncFS](/index.php/EncFS "EncFS") or [TrueCrypt](/index.php/TrueCrypt "TrueCrypt"), though perhaps without some of Btrfs' features.

### Файл подкачки (Swap)

Btrfs does not yet support [swap files](/index.php/Swap#Swap_file "Swap"). This is due to swap files requiring a function that Btrfs does not have for possibility of file system corruption [[5]](https://btrfs.wiki.kernel.org/index.php/FAQ#Does_btrfs_support_swap_files.3F). Patches for swapfile support are already available [[6]](https://lkml.org/lkml/2014/12/9/718) and may be included in an upcoming kernel release. As an alternative a swap file can be mounted on a loop device with poorer performance but will not be able to hibernate. Install the package [systemd-swap](https://www.archlinux.org/packages/?name=systemd-swap) to automate this.

### Ядро Linux-rt

As of version 3.14.12_rt9, the [linux-rt](/index.php/Kernel#-rt "Kernel") kernel does not boot with the Btrfs file system. This is due to the slow development of the *rt* patchset.

## Tips and tricks

### Corruption recovery

*btrfs-check* cannot be used on a mounted file system. To be able to use *btrfs-check* without booting from a live USB, add it to the initial ramdisk:

 `/etc/mkinitcpio.conf`  `BINARIES="/usr/bin/btrfs"` 

Regenerate the initial ramdisk using [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio").

Then if there is a problem booting, the utility is available for repair.

**Примечание:** If the fsck process has to invalidate the space cache (and/or other caches?) then it is normal for a subsequent boot to hang up for a while (it may give console messages about btrfs-transaction being hung). The system should recover from this after a while.

See the [Btrfs Wiki page](https://btrfs.wiki.kernel.org/index.php/Btrfsck) for more information.

### Загрузка в снимки с помощью GRUB

You can manually create a [GRUB#GNU/Linux menu entry](/index.php/GRUB#GNU.2FLinux_menu_entry "GRUB") with the `rootflags=subvol=` argument. The `subvol=` mount options in `/etc/fstab` of the snapshot to boot into also have to be specified correctly.

Alternatively, you can automatically populate your GRUB menu with btrfs snapshots when regenerating the GRUB configuration file by using [grub-btrfs](https://aur.archlinux.org/packages/grub-btrfs/) or [grub-btrfs-git](https://aur.archlinux.org/packages/grub-btrfs-git/).

### Использование подтомов Btrfs с systemd-nspawn

See the [Systemd-nspawn#Use Btrfs subvolume as container root](/index.php/Systemd-nspawn#Use_Btrfs_subvolume_as_container_root "Systemd-nspawn") and [Systemd-nspawn#Use temporary Btrfs snapshot of container](/index.php/Systemd-nspawn#Use_temporary_Btrfs_snapshot_of_container "Systemd-nspawn") articles.

## Решение проблем

See the [Btrfs Problem FAQ](https://btrfs.wiki.kernel.org/index.php/Problem_FAQ) for general troubleshooting.

### GRUB

#### Смещение разделов

**Примечание:** The offset problem may happen when you try to embed `core.img` into a partitioned disk. It means that [it is OK](https://wiki.archlinux.org/index.php?title=Talk:Btrfs&diff=319474&oldid=292530) to embed grub's `core.img` into a Btrfs pool on a partitionless disk (e.g. `/dev/sd*X*`) directly.

[GRUB](/index.php/GRUB "GRUB") can boot Btrfs partitions however the module may be larger than other [file systems](/index.php/File_systems "File systems"). And the `core.img` file made by `grub-install` may not fit in the first 63 sectors (31.5KiB) of the drive between the MBR and the first partition. Up-to-date partitioning tools such as `fdisk` and `gdisk` avoid this issue by offsetting the first partition by roughly 1MiB or 2MiB.

#### Отсутствует root

Users experiencing the following: `error no such device: root` when booting from a RAID style setup then edit /usr/share/grub/grub-mkconfig_lib and remove both quotes from the line `echo " search --no-floppy --fs-uuid --set=root ${hints} ${fs_uuid}"`. Regenerate the config for grub and the system should boot without an error.

### Ошибка BTRFS: open_ctree failed

As of November 2014 there seems to be a bug in [systemd](/index.php/Systemd "Systemd") or [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") causing the following error on systems with multi-device Btrfs filesystem using the `btrfs` hook in `mkinitcpio.conf`:

```
BTRFS: open_ctree failed
mount: wrong fs type, bad option, bad superblock on /dev/sdb2, missing codepage or helper program, or other error

In some cases useful info is found in syslog - try dmesg|tail or so.

You are now being dropped into an emergency shell.

```

A workaround is to remove `btrfs` from the `HOOKS` array in `/etc/mkinitcpio.conf` and instead add `btrfs` to the `MODULES` array. Then regenerate the initramfs with `mkinitcpio -p linux` (adjust the preset if needed) and reboot.

See the [original forums thread](https://bbs.archlinux.org/viewtopic.php?id=189845) and [FS#42884](https://bugs.archlinux.org/task/42884) for further information and discussion.

You will get the same error if you try to mount a raid array without one of the devices. In that case you must add the `degraded` mount option to `/etc/fstab`. If your root resides on the array, you must also add `rootflags=degraded` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

**Примечание:** As of August 2016, a potential workaround for this bug is to mount the array by a single drive only in `/etc/fstab`, and allow btrfs to discover and append the other drives automatically. Group-based identifiers such as UUID and LABEL appear to contribute to the failure. For example, a two-device RAID1 array consisting of 'disk1' and disk2' will have a UUID allocated to it, but instead of using the UUID, use only `/dev/mapper/disk1` in `/etc/fstab`.

For a more detailed explanation, see the following [blog post.](https://blog.samcater.com/fix-for-btrfs-open_ctree-failed-when-running-root-fs-on-raid-1-or-raid10-arch-linux/)

### Проверка btrfs

**Важно:** Since Btrfs is under heavy development, especially the `btrfs check` command, it is highly recommended to create a **backup** and consult the following Btfrs documentation before executing `btrfs check` with the `--repair` switch.

The *[btrfs check](https://btrfs.wiki.kernel.org/index.php/Manpage/btrfs-check)* command can be used to check or repair an unmounted Btrfs filesystem. However, this repair tool is still immature and not able to repair certain filesystem errors even those that do not render the filesystem unmountable.

See [Btrfsck](https://btrfs.wiki.kernel.org/index.php/Btrfsck) for more information.

## Смотрите также

*   **Официальный сайт**
    *   [Btrfs Wiki](https://btrfs.wiki.kernel.org/)
*   **Performance related**
    *   [Btrfs on raw disks?](http://superuser.com/questions/432188/should-i-put-my-multi-device-btrfs-filesystem-on-disk-partitions-or-raw-devices)
    *   [Varying leafsize and nodesize in Btrfs](http://comments.gmane.org/gmane.comp.file-systems.btrfs/19440)
    *   [Btrfs support for efficient SSD operation (data blocks alignment)](http://comments.gmane.org/gmane.comp.file-systems.btrfs/15646)
    *   [Is Btrfs optimized for SSDs?](https://btrfs.wiki.kernel.org/index.php/FAQ#Is_Btrfs_optimized_for_SSD.3F)
    *   **Phoronix mount option benchmarking**
        *   [Linux 3.14](http://www.phoronix.com/scan.php?page=article&item=linux_314_btrfs)
        *   [Linux 3.11](http://www.phoronix.com/scan.php?page=article&item=linux_btrfs_311&num=1)
        *   [Linux 3.9](http://www.phoronix.com/scan.php?page=news_item&px=MTM0OTU)
        *   [Linux 3.7](http://www.phoronix.com/scan.php?page=article&item=btrfs_linux37_mounts&num=1)
        *   [Linux 3.2](http://www.phoronix.com/scan.php?page=article&item=linux_btrfs_options&num=1)
    *   [Lzo vs. zLib](http://blog.erdemagaoglu.com/post/4605524309/lzo-vs-snappy-vs-lzf-vs-zlib-a-comparison-of)
*   **Miscellaneous**
    *   [Funtoo Wiki Btrfs Fun](http://www.funtoo.org/wiki/BTRFS_Fun)
    *   [Avi Miller presenting Btrfs](http://www.phoronix.com/scan.php?page=news_item&px=MTA0ODU) at SCALE 10x, January 2012.
    *   [Summary of Chris Mason's talk](http://www.phoronix.com/scan.php?page=news_item&px=MTA4Mzc) from LFCS 2012
    *   [Btrfs: stop providing a bmap operation to avoid swapfile corruptions](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=commit;h=35054394c4b3cecd52577c2662c84da1f3e73525) 2009-01-21
    *   [Doing Fast Incremental Backups With Btrfs Send and Receive](http://marc.merlins.org/perso/btrfs/post_2014-03-22_Btrfs-Tips_-Doing-Fast-Incremental-Backups-With-Btrfs-Send-and-Receive.html)