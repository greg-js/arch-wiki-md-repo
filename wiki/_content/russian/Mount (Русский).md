_mount_ это команда для подключения и доступа к файловым системам, дисковых отделав и сетевых ресурсов. Она может подключать файловые системы поддерживающиеся ядром Линукса но может также быть дополнена новыми дополнениями для ядра программами такими как [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) для подключения [NTFS](/index.php/NTFS-3G_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NTFS-3G (Русский)") файловых систем с поддержкой для чтения и записи.

## Contents

*   [1 Поддерживающиеся ФС](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D1.8E.D1.89.D0.B8.D0.B5.D1.81.D1.8F_.D0.A4.D0.A1)
*   [2 Изменения настроек использованных по умолчанию](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [2.1 VFAT, FAT, DOS](#VFAT.2C_FAT.2C_DOS)
    *   [2.2 NTFS](#NTFS)
    *   [2.3 ISO образ, CD, DVD](#ISO_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.2C_CD.2C_DVD)
    *   [2.4 Reiser ФС](#Reiser_.D0.A4.D0.A1)
    *   [2.5 Squash ФС](#Squash_.D0.A4.D0.A1)
*   [3 См. также](#.D0.A1.D0.BC._.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Поддерживающиеся ФС

Показать поддерживающиеся ядром:

```
$ zgrep _FS= /proc/config.gz

```

или более чистый:

```
$ zgrep _FS= /proc/config.gz | sed "s/^CONFIG_//m" | sed "s/.$//m" | sed "s/_FS=//m" | sort

```

Показать все поддерживающиеся ФС также видны в `man mount`.

Показать все поддерживающиеся ФС твоим ядром:

```
$ zgrep -e 'FS_' -e _FS -e 'CONFIG_ISO' -e  '_NLS=' -e CONFIG_NLS_ISO /proc/config.gz

```

## Изменения настроек использованных по умолчанию

Здесь несколько примеров о том как можно расширить возможности mount и изменить стандартные настройки. Для изменения настроек [ядра](/index.php/Kernel_Compilation_without_ABS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel Compilation without ABS (Русский)") вам надо скомпилировать ядро самостоятельно. Если скрипт не создан то настройки по умолчанию будут использоваться.

*   [Скомпилировать ядро самостоятельно](/index.php/Kernel_Compilation_without_ABS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel Compilation without ABS (Русский)")
*   Использование скриптов
*   [Редактированием fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)")
*   [Созданием правил udev/udisks](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)") - управляющий устройствами в Linux ядре

Такие как _mount.X_ скрипты где _X_ это название ФС, могут быть использованы для обхода стандартных настроя для _mount_ в ядре для почти каждой поддерживающейся ФС. Используй _-i_ параметр для игнорирования mount.X скриптов, `mount -i /dev/sdXY /mnt/sdXY`.

### VFAT, FAT, DOS

Здесь пример настроек для _mount_ в ядре:

 `$ zgrep -e FAT -e DOS /proc/config.gz | sort -r ` 

```
# DOS/FAT/NT Filesystems
CONFIG_FAT_FS=m
CONFIG_MSDOS_PARTITION=y
CONFIG_FAT_FS=m
CONFIG_MSDOS_FS=m
CONFIG_VFAT_FS=m
CONFIG_FAT_DEFAULT_CODEPAGE=437
CONFIG_FAT_DEFAULT_IOCHARSET="iso8859-1"
CONFIG_NCPFS_SMALLDOS=y
```

**Обратите внимание:** Права доступа по умолчанию _rwxr-xr-x_, `umask=755` тоже как `fmask=0022,dmask=0022`

Если тип ФС установлен как VFAT то будет запущен `/usr/bin/mount.vfat` скрипт.

 `$ cat /usr/bin/mount.vfat` 

```
#!/bin/bash
#mount VFAT with full rw (read-write) permissions for all users
#/usr/bin/mount -i -t vfat -oumask=0000,iocharset=utf8 "$@"
#The above is the same as
mount -i -t vfat -oiocharset=utf8,fmask=0000,dmask=0000 "$@"
```

Смотри также: [more details about mounting of the FAT file systems](http://www.nslu2-linux.org/wiki/HowTo/MountFATFileSystems).

### NTFS

В конфигурации по умолчанию:

 `$ zgrep ^CONFIG_NTFS  /proc/config.gz` 

```
CONFIG_NTFS_FS=m
CONFIG_NTFS_RW=y
```

Опция настройки ядра `CONFIG_NTFS_RW=y` обеспечивает поддержку чтения и записи для [NTFS](https://en.wikipedia.org/wiki/ru:NTFS "wikipedia:ru:NTFS") файловой системы. Это также означает, что ядро ​​предопределено использовать [ntfs-3g](/index.php/NTFS-3G_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NTFS-3G (Русский)") в режиме чтения и записи. Сборка в поддержку файловых систем NTFS ядром является _только для чтения_, даже если активируется опция для чтения и записи.

**Обратите внимание:**

*   Когда [ntfs-3g](/index.php/NTFS-3G_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NTFS-3G (Русский)") будет установлен он может создать символическую ссылку /usr/bin/mount.ntfs в /usr/bin/ntfs-3g.
*   [ntfs-3g](/index.php/NTFS-3G_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NTFS-3G (Русский)") инструмент крепление поддерживает многие из тех же Параметры командной строки в качестве стандарта Linux монтирования полезность, но специализируется на монтаже из [NTFS](https://en.wikipedia.org/wiki/ru:NTFS "wikipedia:ru:NTFS") отформатированных разделов.
*   По умолчанию на монтаж [ntfs-3g](/index.php/NTFS-3G_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NTFS-3G (Русский)") драйвер обеспечивает полный доступ на чтение и запись разрешения для всех пользователей. В некоторых ситуациях доступ с полными правами разрешений может привести к повреждению, см. устранение неисправностей [NTFS](https://en.wikipedia.org/wiki/ru:NTFS "wikipedia:ru:NTFS").

По умолчанию параметры монтирования могут быть изменены при запуске mount.ntfs путем переименования /usr/bin/mount.ntfs символическую ссылку, если существует и создании скрипта на его месте с предпочтительными настройками или использовать -I параметр ( mount -i -t ntfs ), чтобы игнорировать все файлы mount.X и использовать изначально поддерживается функциональность ядром. Этот пример будет монтировать NTFS как только для чтения:

 `$ cat /usr/bin/mount.ntfs` 

```
#!/bin/bash
#mount -i -oro "$@"
#mount with a read-only rights
ntfs-3g -oro  "$@" & disown
```

Смотри также man 8 ntfs-3g для получения дополнительной информации о драйвере NTFS-3G.

### ISO образ, CD, DVD

Когда iso9660 образ обнаружен с mount, то будет запусчен /usr/bin/mount.iso9660 скрипт.

 `$ cat /usr/bin/mount.iso9660` 

```
#!/bin/bash
mount -i -t iso9660 "$@"
#mount -oloop,ro,relatime,utf8 -i -t iso9660 "$@"
# fuseiso "$@"
```

*   Работает с utf8 но показывает ошибки при использовании iso8859 для iocharset.
*   Параметр utf8 такой же как и iocharset=utf8, можешь использовать лубой из них.
*   Вы также можете использовать fuseiso и закомментируйте mount строку и раскомментируйте fuseiso "$@". Или используй любую другую программу для монтирования.

**Обратите внимание:** Вам всё ещо требуются root права (su/sudo) для использования mount команды даже если fuseiso используется в скрипте.

Настройки ISO в ядре по умолчанию:

 `$ zgrep -e CONFIG_ISO -e  CONFIG_NLS_ISO /proc/config.gz` 

```
CONFIG_ISO9660_FS=m
CONFIG_NLS_ISO8859_8=m
CONFIG_NLS_ISO8859_1=m
CONFIG_NLS_ISO8859_2=m
CONFIG_NLS_ISO8859_3=m
CONFIG_NLS_ISO8859_4=m
CONFIG_NLS_ISO8859_5=m
CONFIG_NLS_ISO8859_6=m
CONFIG_NLS_ISO8859_7=m
CONFIG_NLS_ISO8859_9=m
CONFIG_NLS_ISO8859_13=m
CONFIG_NLS_ISO8859_14=m
CONFIG_NLS_ISO8859_15=m
```

### Reiser ФС

В конфигурации по умолчанию:

 `$ zgrep -ie reiserfs /proc/config.gz` 

```
CONFIG_REISERFS_FS=m
# CONFIG_REISERFS_CHECK is not set
CONFIG_REISERFS_PROC_INFO=y
CONFIG_REISERFS_FS_XATTR=y
CONFIG_REISERFS_FS_POSIX_ACL=y
CONFIG_REISERFS_FS_SECURITY=y
```

ReiserFS имеет проблему при подключении с использованием `mount.reiserfs` скриптов. _Mount_ игнорирует `-oro` опцию только для чтения и использует `-orw` вместо её, для записи и чтения, но при использовании с коммандной строки проблема `-oro` не возникает. _Я пробывал только с ReiserFS в соданом пустом документе._

### Squash ФС

В конфигурации по умолчанию:

 `$ zgrep  SQUASHFS /proc/config.gz` 

```
CONFIG_SQUASHFS=m
# CONFIG_SQUASHFS_FILE_CACHE is not set
CONFIG_SQUASHFS_FILE_DIRECT=y
# CONFIG_SQUASHFS_DECOMP_SINGLE is not set
# CONFIG_SQUASHFS_DECOMP_MULTI is not set
CONFIG_SQUASHFS_DECOMP_MULTI_PERCPU=y
CONFIG_SQUASHFS_XATTR=y
CONFIG_SQUASHFS_ZLIB=y
CONFIG_SQUASHFS_LZO=y
CONFIG_SQUASHFS_XZ=y
# CONFIG_SQUASHFS_4K_DEVBLK_SIZE is not set
# CONFIG_SQUASHFS_EMBEDDED is not set
CONFIG_SQUASHFS_FRAGMENT_CACHE_SIZE=3
```

Для создания файловой системы Squash необходимо установить пакет [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools) SquashFS может быть смонтирован только в режиме для чтения. Он поддерживает такие популярные методы сжатия, как gzip, lzma, lzo, lz4, xz (по умолчанию gzip)

```
mksquashfs source /адрес/назначения.img   -comp lzo  -Xalgorithm  lzo1x_999 -Xcompression-level 9

```

**Обратите внимание:** Параметры должны быть указаны после адреса назначения.

После того, как сжатый файл создастся, вы можете смонтировать его.

В Arch Linux нет справочного руководства по утилите _mksquashfs_, но вы можете использовать `mksquashfs -h`, чтобы ознакомится со всеми возможными параметрами.

* * *

Вы можете добавить дополнительные действия, когда внешнее устройство хранения (USB диск или файл образа (ISO, img, dd)) монтируется с помощью скриптов.

## См. также

*   Документация файловых систем, поддерживаемых ядром: [kernel.org](https://www.kernel.org/doc/Documentation/filesystems/) (англ.)
*   Руководство по комманде _mount_: [linux.die.net](http://linux.die.net/man/8/mount) (англ.)
*   [Mount на Википедии](https://en.wikipedia.org/wiki/ru:Mount "wikipedia:ru:Mount")
*   Краткая инструкция по созданию и использованию образов диска: [darkdust.net](http://darkdust.net/writings/diskimagesminihowto) (англ.)