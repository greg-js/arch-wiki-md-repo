Ссылки по теме

*   [Файловые системы](/index.php/%D0%A4%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D1%8B%D0%B5_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B "Файловые системы")

**Состояние перевода:** На этой странице представлен перевод статьи [XFS](/index.php/XFS "XFS"). Дата последней синхронизации: 24 июля 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=XFS&diff=0&oldid=482825).

XFS - это высокопроизводительная файловая система с журналированием, созданная Silicon Graphics, Inc. XFS особенно хорошо справляется с параллельным вводом-выводом благодаря своей структуре на основе группы размещения. Это обеспечивает исключительную масштабируемость потоков ввода-вывода, пропускной способности файловой системы, размера файлов и файловой системы при работе с несколькими устройствами хранения.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Повреждение данных](#Повреждение_данных)
    *   [2.1 Восстановление файловой системы XFS](#Восстановление_файловой_системы_XFS)
    *   [2.2 Онлайн проверка метаданных (scrub)](#Онлайн_проверка_метаданных_(scrub))
*   [3 Интеграция](#Интеграция)
*   [4 Производительность](#Производительность)
    *   [4.1 Размер и ширина полосы](#Размер_и_ширина_полосы)
    *   [4.2 Отключение барьера](#Отключение_барьера)
    *   [4.3 Время доступа](#Время_доступа)
    *   [4.4 Дефрагментация](#Дефрагментация)
        *   [4.4.1 Проверить уровень фрагментации](#Проверить_уровень_фрагментации)
        *   [4.4.2 Выполнение дефрагментации](#Выполнение_дефрагментации)
    *   [4.5 Свободный btree инод](#Свободный_btree_инод)
*   [5 Решение пробелм](#Решение_пробелм)
    *   [5.1 Квота корневой файловой системы](#Квота_корневой_файловой_системы)
*   [6 Смотрите также](#Смотрите_также)

## Установка

Инструменты для управления разделами XFS находятся в пакете [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) из [official repositories](/index.php/Official_repositories "Official repositories"), который включен в базовую установку по умолчанию.

## Повреждение данных

Если по какой-либо причине вы испытываете повреждение данных, вам нужно будет восстановить файловую систему вручную.

### Восстановление файловой системы XFS

Сначала размонтируйте файловую систему XFS.

```
# umount /dev/sda3

```

После размонтирования запустите инструмент [xfs_repair(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfs_repair.8).

```
# xfs_repair -v /dev/sda3

```

### Онлайн проверка метаданных (scrub)

**Warning:** Эта программа является ЭКСПЕРИМЕНТАЛЬНОЙ, что означает, что ее поведение и интерфейс могут измениться в любое время, см. [xfs_scrub(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfs_scrub.8).

`xfs_scrub` asks the kernel to scrub all metadata objects in the [filesystem](/index.php/Filesystem "Filesystem"). Metadata records are scanned for obviously bad values and then cross-referenced against other metadata. The goal is to establish a reasonable confidence about the consistency of the overall filesystem by examining the consistency of individual metadata records against the other metadata in the filesystem. Damaged metadata can be rebuilt from other metadata if there exists redundant data structures which are intact.

[Enable](/index.php/Enable "Enable") `xfs_scrub_all.timer` периодическая проверка онлайн-метаданных для всей файловой системы. One may want to [edit](/index.php/Edit "Edit") `xfs_scrub_all.timer`, since it runs every Sunday at 3:10am.

## Интеграция

xfsprogs 3.2.0 has introduced a new on-disk format (v5) that includes a metadata checksum scheme called [Self-Describing Metadata](https://www.kernel.org/doc/Documentation/filesystems/xfs-self-describing-metadata.txt). Основанный на CRC32, он обеспечивает, например, дополнительную защиту от повреждения метаданных во время непредвиденных потерь мощности. Контрольная сумма включена по умолчанию при использовании xfsprogs 3.2.3 или новее. Если вам нужно монтировать xfs для чтения и записи для более старого ядра, его можно легко отключить с помощью переключателя `-m crc=0` при вызове [mkfs.xfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.xfs.8).

```
# mkfs.xfs -m crc=0 /dev/*target_partition*

```

The XFS v5 on-disk format is considered stable for production workloads starting Linux Kernel 3.15.

**Примечание:** В отличие от [Btrfs](/index.php/Btrfs "Btrfs") и [ZFS](/index.php/ZFS "ZFS"), контрольная сумма CRC32 применяется только к метаданным, а не к фактическим данным.

## Производительность

Для оптимальной скорости просто создайте файловую систему XFS:

```
# mkfs.xfs /dev/*target_partition*

```

Yep, so simple - since all of the ["boost knobs" are already "on" by default](http://xfs.org/index.php/XFS_FAQ#Q:_I_want_to_tune_my_XFS_filesystems_for_.3Csomething.3E).

**Warning:** Отключение барьеров, отключение atime и другие улучшения производительности значительно повышают вероятность повреждения и сбоя данных.

В соответствии с [XFS wiki](http://xfs.org/index.php/XFS_FAQ#Q:_I_want_to_tune_my_XFS_filesystems_for_.3Csomething.3E), рассмотрите возможность изменения CFQ по умолчанию [I/O scheduler](/index.php/Improving_performance#Tuning_I/O_scheduler "Improving performance") (for example to [Deadline](https://en.wikipedia.org/wiki/Deadline_scheduler "wikipedia:Deadline scheduler"), [Noop](https://en.wikipedia.org/wiki/NOOP_scheduler "wikipedia:NOOP scheduler") или [BFQ](/index.php/Linux-ck#How_to_enable_the_BFQ_I.2FO_Scheduler "Linux-ck")) чтобы пользоваться всеми преимуществами XFS, особенно для [SSDs](/index.php/SSD "SSD").

### Размер и ширина полосы

Если эта файловая система будет работать на чередующемся RAID-массиве, вы можете значительно повысить скорость, указав размер чередования в команде [mkfs.xfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.xfs.8).

See [How to calculate the correct sunit,swidth values for optimal performance](http://xfs.org/index.php/XFS_FAQ#Q:_How_to_calculate_the_correct_sunit.2Cswidth_values_for_optimal_performance)

### Отключение барьера

Вы можете повысить производительность, отключив использование барьера для файловой системы, добавив параметр монтирования *nobarrier* в файл `/etc/fstab`.

### Время доступа

В некоторых файловых системах вы можете повысить производительность, добавив параметр монтирования `noatime` в файл `/etc/fstab`. Для файловых систем XFS стандартным поведением atime является `relatime`, которое почти не имеет накладных расходов по сравнению с noatime, но при этом сохраняет нормальные значения atime. Все файловые системы Linux теперь используют это как значение по умолчанию (начиная с версии 2.6.30), но XFS использует релятивное поведение с 2006 года, поэтому никому не нужно когда-либо использовать noatime для XFS по соображениям производительности.

Кроме того, `noatime` подразумевает `nodiratime`, поэтому нет необходимости указывать **nodiratime**, когда также указывается **noatime**.

### Дефрагментация

Хотя основанная на экстентах природа XFS и используемая им стратегия отложенного размещения значительно повышает устойчивость файловой системы к проблемам фрагментации, XFS предоставляет утилиту дефрагментации файловой системы (xfs_fsr, сокращение от реорганизатора файловой системы XFS), которая может дефрагментировать файлы на смонтированной и активной файловой системе XFS. Может быть полезно периодически просматривать фрагментацию XFS.

[xfs_fsr(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfs_fsr.8) улучшает организацию смонтированной файловой системы. Алгоритм реорганизации работает с одним файлом за раз, сжимая или иным образом улучшая компоновку экстентов файла (смежные блоки данных файла).

#### Проверить уровень фрагментации

Чтобы увидеть, насколько фрагментирована ваша файловая система:

```
# xfs_db -c frag -r /dev/sda3

```

#### Выполнение дефрагментации

Чтобы начать дефрагментацию, используйте команду [xfs_fsr(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfs_fsr.8):

```
# xfs_fsr /dev/sda3

```

### Свободный btree инод

Начиная с Linux 3.16, XFS добавила btree, который отслеживает свободные иноды. Это эквивалентно существующему btree для распределения инодов, за исключением того, что свободный btree inode отслеживает фрагменты inode, по крайней мере, с одним свободным inode. Цель состоит в том, чтобы улучшить поиск свободных кластеров inode для распределения inode. Это повышает производительность на устаревших файловых системах, то есть на месяцы или годы, когда вы добавили и удалили миллионы файлов в / из файловой системы. Использование этой функции не влияет на общий уровень надежности файловой системы или возможности восстановления.

This feature relies on the new v5 on-disk format that has been considered stable for production workloads starting Linux Kernel 3.15\. It does not change existing on-disk structures, but adds a new one that must remain consistent with the inode allocation btree; for this reason older kernels will only be able to mount read-only filesystems with the free inode btree feature.

Функция включена по умолчанию при использовании xfsprogs 3.2.3 или новее. Если вам требуется доступная для записи файловая система для более старого ядра, ее можно отключить с помощью переключателя `finobt=0` при форматировании раздела XFS. Вам нужно `crc=0` вместе.

```
# mkfs.xfs -m crc=0,finobt=0 /dev/*target_partition*

```

or shortly (`finobt` depends `crc`)

```
# mkfs.xfs -m crc=0 /dev/*target_partition*

```

## Решение пробелм

### Квота корневой файловой системы

Параметры монтирования XFS (`uquota`, `gquota`, `prjquota` и т.д.) Не выполняются во время повторного монтирования файловой системы. Чтобы включить квоту для корневой файловой системы, параметр монтирования должен быть передан initramfs как [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `rootflags=`. Впоследствии его не следует указывать среди параметров монтирования в `/etc/fstab` для корневой (`/`) файловой системы.

**Примечание:** Существуют некоторые различия в квоте XFS по сравнению со стандартным Linux [Disk quota](/index.php/Disk_quota "Disk quota"), эту статью [http://inai.de/linux/adm_quota](http://inai.de/linux/adm_quota) стоит прочитать.

## Смотрите также

*   [XFS FAQ](http://xfs.org/index.php/XFS_FAQ)
*   [Improving Metadata Performance By Reducing Journal Overhead](http://xfs.org/index.php/Improving_Metadata_Performance_By_Reducing_Journal_Overhead)
*   [XFS Wikipedia Entry](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS")