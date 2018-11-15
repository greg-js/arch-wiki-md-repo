Ссылки по теме

*   [Core utilities#lsblk](/index.php/Core_utilities#lsblk "Core utilities")

*   [Разрешения и атрибуты файлов](/index.php/%D0%A0%D0%B0%D0%B7%D1%80%D0%B5%D1%88%D0%B5%D0%BD%D0%B8%D1%8F_%D0%B8_%D0%B0%D1%82%D1%80%D0%B8%D0%B1%D1%83%D1%82%D1%8B_%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2 "Разрешения и атрибуты файлов")
*   [Fsck (Русский)](/index.php/Fsck_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fsck (Русский)")
*   [fstab (Русский)](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)")
*   [Список приложений/Утилиты#Монтирование](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9/%D0%A3%D1%82%D0%B8%D0%BB%D0%B8%D1%82%D1%8B#Монтирование "Список приложений/Утилиты")
*   [Оптический привод](/index.php/%D0%9E%D0%BF%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B9_%D0%BF%D1%80%D0%B8%D0%B2%D0%BE%D0%B4 "Оптический привод")
*   [Разметка дисков](/index.php/%D0%A0%D0%B0%D0%B7%D0%BC%D0%B5%D1%82%D0%BA%D0%B0_%D0%B4%D0%B8%D1%81%D0%BA%D0%BE%D0%B2 "Разметка дисков")
*   [NFS (Русский)](/index.php/NFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NFS (Русский)")
*   [NTFS-3G (Русский)](/index.php/NTFS-3G_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NTFS-3G (Русский)")
*   [FAT (Русский)](/index.php/FAT_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "FAT (Русский)")
*   [QEMU (Русский)#Монтирование раздела внутри образа диска raw](/index.php/QEMU_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Монтирование_раздела_внутри_образа_диска_raw "QEMU (Русский)")

*   [Samba (Русский)](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Samba (Русский)")
*   [tmpfs (Русский)](/index.php/Tmpfs_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Tmpfs (Русский)")
*   [udev (Русский)](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)")
*   [Udisks (Русский)](/index.php/Udisks_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udisks (Русский)")
*   [Umask (Русский)](/index.php/Umask_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Umask (Русский)")
*   [USB-накопители](/index.php/USB-%D0%BD%D0%B0%D0%BA%D0%BE%D0%BF%D0%B8%D1%82%D0%B5%D0%BB%D0%B8 "USB-накопители")

**Состояние перевода:** На этой странице представлен перевод статьи [File systems](/index.php/File_systems "File systems"). Дата последней синхронизации: 10 августа 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=File_systems&diff=0&oldid=484782).

Из [Википедии](https://en.wikipedia.org/wiki/ru:%D0%A4%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D0%B0%D1%8F_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0 "w:ru:Файловая система"):

	Файловая система (англ. file system) — порядок, определяющий способ организации, хранения и именования данных на носителях информации в компьютерах, а также в другом электронном оборудовании: цифровых фотоаппаратах, мобильных телефонах и т.п. Файловая система определяет формат содержимого и способ физического хранения информации, которую принято группировать в виде файлов. Конкретная файловая система определяет размер имен файлов и (каталогов), максимальный возможный размер файла и раздела, набор атрибутов файла. Некоторые файловые системы предоставляют сервисные возможности, например, разграничение доступа или шифрование файлов.

Отдельные разделы дисков можно настроить с использованием одной из множества доступных файловых систем. У каждой есть свои преимущества, недостатки и уникальные особенности. Ниже приведен краткий обзор поддерживаемых файловых систем; также и ссылки на страницы Википедии, которые предоставляют гораздо больше информации.

## Contents

*   [1 Типы файловых систем](#Типы_файловых_систем)
    *   [1.1 Журналирование](#Журналирование)
    *   [1.2 Файловые системы на основе FUSE](#Файловые_системы_на_основе_FUSE)
    *   [1.3 Штабелируемые файловые системы](#Штабелируемые_файловые_системы)
    *   [1.4 Файловые системы только для чтения](#Файловые_системы_только_для_чтения)
    *   [1.5 Кластерные файловые системы](#Кластерные_файловые_системы)
*   [2 Определение существующих файловых систем](#Определение_существующих_файловых_систем)
*   [3 Создание файловой системы](#Создание_файловой_системы)
*   [4 Монтирование файловой системы](#Монтирование_файловой_системы)
    *   [4.1 Список смонтированных файловых систем](#Список_смонтированных_файловых_систем)
    *   [4.2 Размонтирование файловой системы](#Размонтирование_файловой_системы)
*   [5 Смотрите также](#Смотрите_также)

## Типы файловых систем

Смотрите [filesystems(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/filesystems.5) для общего обзора и [Википедию:Сравнение файловых систем](https://en.wikipedia.org/wiki/ru:%D0%A1%D1%80%D0%B0%D0%B2%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D1%8B%D1%85_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC "w:ru:Сравнение файловых систем") для подробного сравнения функций. Файловые системы, поддерживаемые ядром, перечислены в `/proc/filesystems`.

| Файловая система | Команда создания | Утилиты пользовательского пространства | [Archiso](/index.php/Archiso_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Archiso (Русский)") [[1]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.both) | Документация ядра [[2]](https://www.kernel.org/doc/Documentation/filesystems/) | Заметки |
| [Btrfs](/index.php/Btrfs_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Btrfs (Русский)") | [mkfs.btrfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.btrfs.8) | [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) | Да | [btrfs.txt](https://www.kernel.org/doc/Documentation/filesystems/btrfs.txt) | [Статус стабильности](https://btrfs.wiki.kernel.org/index.php/Status) |
| [VFAT](/index.php/FAT_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "FAT (Русский)") | [mkfs.vfat(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.vfat.8) | [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) | Да | [vfat.txt](https://www.kernel.org/doc/Documentation/filesystems/vfat.txt) |
| [exFAT](https://en.wikipedia.org/wiki/ru:exFAT "w:ru:exFAT") | mkfs.exfat(8) | [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils) | Опционально | N/A (на основе FUSE) |
| [F2FS](/index.php/F2FS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "F2FS (Русский)") | [mkfs.f2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.f2fs.8) | [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) | Да | [f2fs.txt](https://www.kernel.org/doc/Documentation/filesystems/f2fs.txt) | Флэш-устройства |
| [ext3](/index.php/Ext3_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Ext3 (Русский)") | [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8) | [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | Да ([base](https://www.archlinux.org/groups/x86_64/base/)) | [ext3.txt](https://www.kernel.org/doc/Documentation/filesystems/ext3.txt) |
| [ext4](/index.php/Ext4_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Ext4 (Русский)") | [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8) | [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | Да ([base](https://www.archlinux.org/groups/x86_64/base/)) | [ext4.txt](https://www.kernel.org/doc/Documentation/filesystems/ext4.txt) |
| [HFS](https://en.wikipedia.org/wiki/ru:HFS "w:ru:HFS") | [mkfs.hfsplus(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.hfsplus.8) | [hfsprogs](https://aur.archlinux.org/packages/hfsprogs/) | Опционально | [hfs.txt](https://www.kernel.org/doc/Documentation/filesystems/hfs.txt) | Файловая система [MacOS](https://en.wikipedia.org/wiki/ru:macOS "w:ru:macOS") |
| [JFS](/index.php/JFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "JFS (Русский)") | [mkfs.jfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.jfs.8) | [jfsutils](https://www.archlinux.org/packages/?name=jfsutils) | Да ([base](https://www.archlinux.org/groups/x86_64/base/)) | [jfs.txt](https://www.kernel.org/doc/Documentation/filesystems/jfs.txt) |
| [NILFS2](https://en.wikipedia.org/wiki/ru:NILFS "w:ru:NILFS") | [mkfs.nilfs2(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.nilfs2.8) | [nilfs-utils](https://www.archlinux.org/packages/?name=nilfs-utils) | Да | [nilfs2.txt](https://www.kernel.org/doc/Documentation/filesystems/nilfs2.txt) |
| [NTFS](/index.php/NTFS-3G_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NTFS-3G (Русский)") | [mkfs.ntfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.ntfs.8) | [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) | Да | N/A (на основе FUSE) | Файловая система [Windows](https://en.wikipedia.org/wiki/ru:Windows "w:ru:Windows") |
| [Reiser4](/index.php/Reiser4_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Reiser4 (Русский)") | mkfs.reiser4(8) | [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/) | Нет |
| [ReiserFS](https://en.wikipedia.org/wiki/ru:ReiserFS "w:ru:ReiserFS") | [mkfs.reiserfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.reiserfs.8) | [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs) | Да ([base](https://www.archlinux.org/groups/x86_64/base/)) |
| [XFS](/index.php/XFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "XFS (Русский)") | [mkfs.xfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.xfs.8) | [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) | Да ([base](https://www.archlinux.org/groups/x86_64/base/)) | 

[xfs.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs.txt)
[xfs-delayed-logging-design.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs-delayed-logging-design.txt)
[xfs-self-describing-metadata.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs-self-describing-metadata.txt)

 |
| [ZFS](/index.php/ZFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ZFS (Русский)") | [zfs-linux](https://aur.archlinux.org/packages/zfs-linux/) | Нет | N/A (порт [OpenZFS](https://en.wikipedia.org/wiki/OpenZFS "w:OpenZFS")) |

**Примечание:** У ядра есть свой собственный драйвер NTFS (смотрите [ntfs.txt](https://www.kernel.org/doc/Documentation/filesystems/ntfs.txt)), но он имеет ограниченную поддержку на запись файлов.

### Журналирование

Все вышеупомянутые файловые системы, за исключением ext2, FAT16/32, Btrfs и ZFS, используют [ведение журнала](https://en.wikipedia.org/wiki/ru:%D0%96%D1%83%D1%80%D0%BD%D0%B0%D0%BB%D0%B8%D1%80%D1%83%D0%B5%D0%BC%D0%B0%D1%8F_%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D0%B0%D1%8F_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0 "w:ru:Журналируемая файловая система"). Журналирование обеспечивает отказоустойчивость путем регистрации изменений до того, как они будут привязаны к файловой системе. В случае сбоя системы или сбоя питания такие файловые системы быстрее возвращаются в сеть и реже становятся поврежденными. Ведение журнала происходит в выделенной области файловой системы.

Не все методы ведения журнала одинаковы. Ext3 и ext4 предлагают журналирование в режиме данных, в котором регистрируются как данные, так и метаданные, а также возможность вести журнал только изменений метаданных. Журналирование в режиме данных имеет ограничение скорости и не включено по умолчанию. В том же ключе [Reiser4](/index.php/Reiser4_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Reiser4 (Русский)") предлагает так называемые ["модели транзакций"](https://reiser4.wiki.kernel.org/index.php/Reiser4_transaction_models), которые включают в себя чистое ведение журнала (эквивалентное журнальному ведению журнала данных ext4), чистый подход копирования при записи (эквивалент по умолчанию btrfs) и комбинированный подход, который эвристически чередуется между двумя бывшими.

**Примечание:** Reiser4 не обеспечивает эквивалент поведения журналирования по умолчанию ext4 (только для метаданных).

Другие файловые системы обеспечивают упорядоченное ведение журнала, которое регистрирует только метаданные. Хотя все журналирование вернет файловую систему в допустимое состояние после сбоя, журналирование в режиме данных обеспечивает максимальную защиту от повреждений и потери данных. Однако есть компромисс в производительности системы, поскольку журналирование в режиме данных выполняет две операции записи: сначала в журнал, а затем на диск. При выборе типа файловой системы следует учитывать компромисс между скоростью системы и безопасностью данных.

Файловые системы, основанные на механизме копирования при записи, такие как Btrfs и ZFS, не должны использовать традиционный журнал для защиты метаданных, потому что они никогда не обновляются на месте. Хотя Btrfs все еще имеет журнальное дерево, подобное журналу, оно используется только для ускорения работы fdatasync/fsync.

### Файловые системы на основе FUSE

[Файловая система в пользовательском пространстве](https://en.wikipedia.org/wiki/ru:FUSE_(%D0%BC%D0%BE%D0%B4%D1%83%D0%BB%D1%8C_%D1%8F%D0%B4%D1%80%D0%B0) "w:ru:FUSE (модуль ядра)") (FUSE) - это механизм для Unix-подобных операционных систем, который позволяет не-привилегированным пользователям создавать свои собственные файловые системы без редактирования кода ядра. Это достигается путем запуска кода файловой системы в *пространстве пользователя*, в то время как модуль ядра FUSE предоставляет только "мост" для реальных интерфейсов ядра.

Некоторые файловые системы на основе FUSE:

*   **adbfs-git** — монтирует устройства Android, подключенные через USB.

	[http://collectskin.com/adbfs/](http://collectskin.com/adbfs/) || [adbfs-git](https://aur.archlinux.org/packages/adbfs-git/)

*   **[EncFS](/index.php/EncFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "EncFS (Русский)")** — это пользовательская наращиваемая криптографическая файловая система.

	[https://vgough.github.io/encfs/](https://vgough.github.io/encfs/) || [encfs](https://www.archlinux.org/packages/?name=encfs)

*   **fuseiso** — монтирует ISO в качестве обычного пользователя.

	[http://sourceforge.net/projects/fuseiso/](http://sourceforge.net/projects/fuseiso/) || [fuseiso](https://www.archlinux.org/packages/?name=fuseiso)

*   **[gitfs](/index.php/Gitfs_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Gitfs (Русский)")** — файловая система FUSE, которая полностью интегрируется с git.

	[https://www.presslabs.com/gitfs/](https://www.presslabs.com/gitfs/) || [gitfs](https://aur.archlinux.org/packages/gitfs/)

*   **xbfuse-git** — монтирует Xbox (360) ISO.

	[http://multimedia.cx/xbfuse/](http://multimedia.cx/xbfuse/) || [xbfuse-git](https://aur.archlinux.org/packages/xbfuse-git/)

*   **xmlfs** — представляет файл XML в качестве структуры каталогов для легкого доступа.

	[https://github.com/halhen/xmlfs](https://github.com/halhen/xmlfs) || [xmlfs](https://aur.archlinux.org/packages/xmlfs/)

*   **vdfuse** — монтирует образы дисков VirtualBox (VDI/VMDK/VHD).

	[https://github.com/muflone/virtualbox-includes](https://github.com/muflone/virtualbox-includes) || [vdfuse](https://aur.archlinux.org/packages/vdfuse/)

Для получения допольнительной информации смотрите [Википедия:Файловая система в пространстве пользователей#Примеры использования](https://en.wikipedia.org/wiki/Filesystem_in_Userspace#Example_uses "wikipedia:Filesystem in Userspace").

### Штабелируемые файловые системы

*   **aufs** — усовершенствованная многоуровневая файловая система унификации, объединенная файловая система на основе FUSE, полностью переписанная Unionfs, отклоненная от основной линии Linux, и вместо этого OverlayFS был объединен в ядро Linux.

	[http://aufs.sourceforge.net](http://aufs.sourceforge.net) || [aufs](https://aur.archlinux.org/packages/aufs/)

*   **[eCryptfs](/index.php/ECryptfs_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ECryptfs (Русский)")** — корпоративная криптографическая файловая система представляет собой пакет программного обеспечения для шифрования диска Linux. Он реализует шифрование на уровне файловой системы, совместимый с POSIX, с целью предложить функциональность, аналогичную функции GnuPG на уровне операционной системы.

	[http://ecryptfs.org](http://ecryptfs.org) || [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils)

*   **mergerfs** — объединенная файловая система на основе FUSE.

	[https://github.com/trapexit/mergerfs](https://github.com/trapexit/mergerfs) || [mergerfs](https://aur.archlinux.org/packages/mergerfs/)

*   **mhddfs** — файловая система Multi-HDD FUSE, объединенная на основе FUSE.

	[http://mhddfs.uvw.ru](http://mhddfs.uvw.ru) || [mhddfs](https://aur.archlinux.org/packages/mhddfs/)

*   **[overlayfs](/index.php/Overlay_filesystem_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Overlay filesystem (Русский)")** — это служба файловой системы для Linux, которая реализует объединение для монтирования других файловых систем.

	[https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt](https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt) || [linux](https://www.archlinux.org/packages/?name=linux)

*   **Unionfs** — это служба файловой системы для Linux, FreeBSD и NetBSD, которая реализует объединение монтирования для других файловых систем.

	[http://unionfs.filesystems.org/](http://unionfs.filesystems.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **unionfs-fuse** — реализация пользовательского пространства Unionfs.

	[https://github.com/rpodgorny/unionfs-fuse](https://github.com/rpodgorny/unionfs-fuse) || [unionfs-fuse](https://www.archlinux.org/packages/?name=unionfs-fuse)

### Файловые системы только для чтения

*   **[SquashFS](https://en.wikipedia.org/wiki/ru:Squashfs "w:ru:Squashfs")** — сжимающая файловая система для GNU/Linux, предоставляющая доступ к данным в режиме "только для чтения". Squashfs сжимает файлы, индексные дескрипторы и каталоги, а также поддерживает блоки размером до 1024 Кбайт для лучшего сжатия.

	[http://squashfs.sourceforge.net/](http://squashfs.sourceforge.net/) || [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools)

### Кластерные файловые системы

*   **[Ceph](/index.php/Ceph_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Ceph (Русский)")** — унифицированная распределенная система хранения, предназначенная для отличной производительности, надежности и масштабируемости.

	[https://ceph.com/](https://ceph.com/) || [ceph](https://www.archlinux.org/packages/?name=ceph)

*   **[Glusterfs](/index.php/Glusterfs_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Glusterfs (Русский)")** — кластерная файловая система способна масштабироваться до нескольких пета-байт.

	[https://www.gluster.org/](https://www.gluster.org/) || [glusterfs](https://www.archlinux.org/packages/?name=glusterfs)

*   **[IPFS](/index.php/IPFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "IPFS (Русский)")** — одноранговый протокол гипермедиа, чтобы сделать Интернет более быстрым, безопасным и открытым. IPFS нацелена на замену HTTP и создание лучшей сети для всех нас. Использует блоки для хранения частей файла, каждый сетевой узел хранит только интересующий контент, обеспечивает дедупликацию, распространение, масштабируемую систему, ограниченную только пользователями. (В настоящее время в aplha)

	[https://ipfs.io/](https://ipfs.io/) || [go-ipfs](https://www.archlinux.org/packages/?name=go-ipfs)

*   **[MooseFS](https://en.wikipedia.org/wiki/ru:Moose_File_System "w:ru:Moose File System")** — это отказоустойчивая, высокодоступная и высокопроизводительная сетевая распределенная файловая система.

	[https://www.gluster.org/](https://www.gluster.org/) || [moosefs](https://www.archlinux.org/packages/?name=moosefs)

*   **[OpenAFS](/index.php/OpenAFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "OpenAFS (Русский)")** — реализация с открытым исходным кодом распределенной файловой системы AFS

	[http://www.openafs.org](http://www.openafs.org) || [openafs](https://aur.archlinux.org/packages/openafs/)

*   **[OrangeFS](https://en.wikipedia.org/wiki/OrangeFS "wikipedia:OrangeFS")** — это масштабируемая сетевая файловая система, предназначенная для прозрачного доступа к дисковой памяти на нескольких серверах параллельно. Имеет оптимизированную поддержку MPI-IO для параллельных и распределенных приложений. Упрощает использование параллельного хранения не только для клиентов Linux, но и для Windows, Hadoop и WebDAV. POSIX-совместимая. Часть ядра Linux, начиная с версии 4.6.

	[http://www.orangefs.org/](http://www.orangefs.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **Sheepdog** — распределенная система хранения объектов для объемных и контейнерных сервисов и разумно управляет дисками и узлами.

	[https://sheepdog.github.io/sheepdog/](https://sheepdog.github.io/sheepdog/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[Tahoe-LAFS](https://en.wikipedia.org/wiki/Tahoe-LAFS "wikipedia:Tahoe-LAFS")** — файловая система Thahoe Least-Authority - это бесплатное и открытое, безопасное, децентрализованное, отказоустойчивое, одноранговое распределенное хранилище данных и распределенная файловая система.

	[https://tahoe-lafs.org/](https://tahoe-lafs.org/) || [tahoe-lafs](https://aur.archlinux.org/packages/tahoe-lafs/)

## Определение существующих файловых систем

Чтобы определить существующие файловые системы, вы можете использовать [lsblk](/index.php/Lsblk_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Lsblk (Русский)"):

 `$ lsblk -f` 
```
NAME   FSTYPE LABEL     UUID                                 MOUNTPOINT
sdb                                                          
└─sdb1 vfat   Transcend 4A3C-A9E9
```

Существующая файловая система, если она есть, будет показана в столбце `FSTYPE`. Если она с[монтирова](/index.php/%D0%9C%D0%BE%D0%BD%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0 "Монтирова")на, тогда появится в столбце `MOUNTPOINT`.

## Создание файловой системы

Файловые системы обычно создаются на [раздел](/index.php/%D0%A0%D0%B0%D0%B7%D0%B4%D0%B5%D0%BB "Раздел")е, внутри логических контейнеров, таких как [LVM](/index.php/LVM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "LVM (Русский)"), [RAID](/index.php/RAID_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "RAID (Русский)") и [dm-crypt](/index.php/Dm-crypt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dm-crypt (Русский)"), или в обычном файле (смотрите [w:Loop device](https://en.wikipedia.org/wiki/Loop_device "w:Loop device")). В этом разделе описывается случай раздела.

**Примечание:** Файловые системы могут быть записаны непосредственно на диск, называемый [superfloppy](https://msdn.microsoft.com/en-us/library/windows/hardware/dn640535(v=vs.85).aspx#gpt_faq_superfloppy) или *безраздельным диском*. С этим методом связаны определенные ограничения, особенно при [загрузке](/index.php/Arch_boot_process "Arch boot process") с такого диска. Для примеров смотрите [Btrfs#Безраздельный диск Btrfs](/index.php/Btrfs_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Безраздельный_диск_Btrfs "Btrfs (Русский)").

**Важно:**

*   После создания новой файловой системы данные, ранее сохраненные на этом разделе, вряд ли можно будет восстановить. **Создайте резервную копию любых данных, которые вы хотите сохранить**.
*   Цель данного раздела может ограничить выбор файловой системы. Например, [системный раздел EFI](/index.php/%D0%A1%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%BD%D1%8B%D0%B9_%D1%80%D0%B0%D0%B7%D0%B4%D0%B5%D0%BB_EFI "Системный раздел EFI") должен содержать файловую систему FAT32 (`mkfs.vfat`), а файловая система, содержащая каталог `/boot`, должна поддерживаться с помощью [загрузчик](/index.php/%D0%97%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D1%87%D0%B8%D0%BA "Загрузчик")а.

Прежде чем продолжить, [определите устройство](/index.php/Lsblk_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Lsblk (Русский)"), в котором будет создана файловая система, и независимо от того, монтируется ли она. Например:

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1                      C4DA-2C4D                            
├─sda2 ext4                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 /mnt
└─sda3                      56adc99b-a61e-46af-aab7-a6d07e504652 

```

Перед продолжением **необходимо** [размонтировать](#Размонтирование_файловой_системы) файловые системы. В приведенном выше примере существующая файловая система находится на `/dev/sda2` и монтируется в `/mnt`. Он будет размонтирован командой:

```
# umount /dev/sda2

```

Чтобы найти только смонтированные файловые системы, смотрите [#Список смонтированных файловых систем](#Список_смонтированных_файловых_систем).

Чтобы создать новую файловую систему, используйте [mkfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.8). Смотрите [#Типы файловых систем](#Типы_файловых_систем) для точного типа, а также утилиты пользовательского пространства, которые вы, возможно, захотите установить для конкретной файловой системы.

Например, чтобы создать новую файловую систему типа [ext4](/index.php/Ext4_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Ext4 (Русский)") (обычно для разделов данных Linux) на `/dev/sda1`, запустите:

```
# mkfs.ext4 /dev/sda1

```

**Совет:**

*   Используйте флаг `-L` *mkfs.ext4*, чтобы указать [метку файловой системы](/index.php/Persistent_block_device_naming_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#метка "Persistent block device naming (Русский)"). *e2label* можно использовать для изменения метки в существующей файловой системе.
*   Файловые системы могут быть *изменены* после создания с определенными ограничениями. Например, размер файловой системы [XFS](/index.php/XFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "XFS (Русский)") может быть увеличен, но он не может быть уменьшен. Для получения допольнительной информации смотрите [Возможности изменения размера](https://en.wikipedia.org/wiki/ru:%D0%A1%D1%80%D0%B0%D0%B2%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D1%8B%D1%85_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC#.D0.92.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE.D1.81.D1.82.D0.B8_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80.D0.B0 "w:ru:Сравнение файловых систем") и соответствующую документацию файловой системы.

Новая файловая система теперь может быть смонтирована в выбранный каталог.

## Монтирование файловой системы

Чтобы вручную смонтировать файловую систему, расположенную на устройстве (например, раздел) к каталогу, используйте [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8). В этом примере монтируется `/dev/sda1` в `/mnt`.

```
# mount /dev/sda1 /mnt

```

Это прикрепляет файловую систему раздела `/dev/sda1` в каталог `/mnt`, делая содержимое файловой системы видимым. Любые данные, существовавшие в `/mnt` перед этим действием, становятся невидимыми до тех пор, пока устройство не будет размонтировано.

[fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)") содержит информацию о том, как устройства должны автоматически монтироваться, если они присутствуют. Для получения дополнительной информации о том, как изменить это поведение, смотрите статью [fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)").

Если устройство указано в `/etc/fstab`, и в командной строке указывается только устройство или точки монтирования, эта информация будет использоваться при монтирование. Например, если `/etc/fstab` содержит строку, указывающую, что `/dev/sda1` должен быть смонтирован в `/mnt`, тогда он автоматически будет монтировать это устройство к этому месту:

```
# mount /dev/sda1

```

Или

```
# mount /mnt

```

*mount* содержит несколько параметров, многие из которых зависят от указанной файловой системы. Параметры могут быть изменены:

*   использование флагов в командной строке с *mount*
*   редактирование [fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)")
*   создание правил [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)")
*   [самостоятельно компилировать ядро](/index.php/Arch_Build_System "Arch Build System")
*   или используя скрипты монтирования файловой системы (расположенные по адресу `/usr/bin/mount.*`).

Более подробную информацию смотрите в связанных статьях и статье интересующей файловой системы.

### Список смонтированных файловых систем

Чтобы просмотреть все смонтированные файловые системы, используйте [findmnt(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/findmnt.8):

```
$ findmnt

```

*findmnt* принимает множество аргументов, которые могут фильтровать вывод и отображать дополнительную информацию. Например, в качестве аргумента может принимать устройство или точку монтирования для отображения только информации о том, что указывается:

```
$ findmnt /dev/sda1

```

*findmnt* собирает информацию из `/etc/fstab`, `/etc/mtab` и `/proc/self/mounts`.

### Размонтирование файловой системы

Чтобы размонтировать файловую систему, используйте [umount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/umount.8). Можно указать либо устройство, содержащее файловую систему (например, `/dev/sda1`), либо точку монтирования (например, `/mnt`):

```
# umount /dev/sda1

```

Или

```
# umount /mnt

```

## Смотрите также

*   [filesystems(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/filesystems.5)
*   [Документация файловых систем, поддерживаемых linux](https://www.kernel.org/doc/Documentation/filesystems/)
*   [Википедия:Файловая система](https://en.wikipedia.org/wiki/ru:%D0%A4%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D0%B0%D1%8F_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0 "w:ru:Файловая система")
*   [Википедия:mount](https://en.wikipedia.org/wiki/ru:mount "w:ru:mount")