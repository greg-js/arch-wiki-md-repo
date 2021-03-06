Ссылки по теме

*   [Файловые системы](/index.php/%D0%A4%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D1%8B%D0%B5_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B "Файловые системы")

**Состояние перевода:** На этой странице представлен перевод статьи [FAT](/index.php/FAT "FAT"). Дата последней синхронизации: 14 августа 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=FAT&diff=0&oldid=485344).

Из [Википедии:Таблица размещения файлов](https://en.wikipedia.org/wiki/ru:FAT "w:ru:FAT"):

	Таблица размещения файлов (FAT) - это классическая архитектура файловой системы компьютера и семейство стандартных файловых систем, использующих ее. Файловая система FAT представляет собой устаревшую файловую систему, которая проста и надежна. Она обеспечивает хорошую производительность даже в облегченных реализациях, но не может обеспечить такую же производительность, надежность и масштабируемость, как некоторые современные файловые системы. Тем не менее, она поддерживается по соображениям совместимости почти всеми разрабатываемыми в настоящее время операционными системами для персональных компьютеров и многих мобильных устройств и встроенных систем и, таким образом, является хорошо подходящим форматом для обмена данными между компьютерами и устройствами практически любого типа и возраста с 1981 года до настоящего времени.

## Конфигурации ядра

Ниже приведен пример конфигурации *монтирования* по умолчанию в ядре:

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

Краткое описание этих параметров:

*   Настройки языка: CONFIG_FAT_DEFAULT_CODEPAGE, CONFIG_FAT_DEFAULT_IOCHARSET
*   Все имена файлов в нижнем регистре букв на разделах FAT, если они включены: CONFIG_NCPFS_SMALLDOS
*   Включает поддержку файловых систем FAT: CONFIG_FAT_FS, CONFIG_MSDOS_FS, CONFIG_VFAT_FS
*   Включает поддержку разметки жестких дисков FAT на компьютерах 86x: CONFIG_MSDOS_PARTITION

Если тип раздела, обнаруженный монтированием, является VFAT, тогда запускается скрипт `/usr/bin/mount.vfat`.

 `/usr/bin/mount.vfat` 
```
#!/bin/bash
#mount VFAT with full rw (read-write) permissions for all users
#/usr/bin/mount -i -t vfat -oumask=0000,iocharset=utf8 "$@"
#The above is the same as
mount -i -t vfat -oiocharset=utf8,fmask=0000,dmask=0000 "$@"
```

## Запись на FAT32 в качестве обычного пользователя

Чтобы записать на раздел FAT32, вы должны внести несколько изменений в файл [fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)").

 `/etc/fstab`  `/dev/sd*xY*    /mnt/some_folder  vfat   **user**,rw,umask=000              0  0` 

Флаг `user` означает, что любой пользователь (даже не root) может монтировать и размонтировать раздел `/dev/sd*X*`. Флаг `rw` дает доступ на чтение и запись; параметр `umask` удаляет выбранные права - например `umask=111` удаляет исполняемые права. Проблема в том, что эта запись также удаляет исполняемые права из каталогов, поэтому мы должны исправить ее с помощью `dmask=000`. Для получения допольнительной информации смотрите [Umask](/index.php/Umask_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Umask (Русский)").

Без этих параметров все файлы будут исполняемыми. Вы можете использовать опцию `showexec` вместо параметров umask и dmask, которые отображают все исполняемые файлы Windows (com, exe, bat) в исполняемых цветах.

Например, если ваш раздел FAT32 находится на `/dev/sda9`, и вы хотите смонтировать его на `/mnt/fat32`, вы должны использовать:

 `/etc/fstab`  `/dev/sda9    /mnt/fat32        vfat   **user**,rw,umask=111,dmask=000    0  0` 

Теперь любой пользователь может смонтировать его с помощью:

```
$ mount /mnt/fat32

```

И размонтировать его с помощью:

```
$ umount /mnt/fat32

```

## Смотрите также

*   [Монтирование файловой системы FAT](http://www.nslu2-linux.org/wiki/HowTo/MountFATFileSystems)