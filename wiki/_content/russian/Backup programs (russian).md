Ссылки по теме

*   [Full system backup with rsync](/index.php/Full_system_backup_with_rsync "Full system backup with rsync")
*   [Full system backup with tar](/index.php/Full_system_backup_with_tar "Full system backup with tar")
*   [Клонирование диска](/index.php/%D0%9A%D0%BB%D0%BE%D0%BD%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5_%D0%B4%D0%B8%D1%81%D0%BA%D0%B0 "Клонирование диска")
*   [Snapper](/index.php/Snapper "Snapper")

**Состояние перевода:** На этой странице представлен перевод статьи [Backup programs](/index.php/Backup_programs "Backup programs"). Дата последней синхронизации: 2 октября 2015\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Backup_programs&diff=0&oldid=402619).

## Contents

*   [1 Введение](#.D0.92.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5)
*   [2 Нарастающие бекапы (Incremental backups)](#.D0.9D.D0.B0.D1.80.D0.B0.D1.81.D1.82.D0.B0.D1.8E.D1.89.D0.B8.D0.B5_.D0.B1.D0.B5.D0.BA.D0.B0.D0.BF.D1.8B_.28Incremental_backups.29)
    *   [2.1 Резервное копирование Rsync-типа](#.D0.A0.D0.B5.D0.B7.D0.B5.D1.80.D0.B2.D0.BD.D0.BE.D0.B5_.D0.BA.D0.BE.D0.BF.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_Rsync-.D1.82.D0.B8.D0.BF.D0.B0)
        *   [2.1.1 Интерфейс командной строки (Консоль)](#.D0.98.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.BD.D0.BE.D0.B9_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B8_.28.D0.9A.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D1.8C.29)
        *   [2.1.2 С графическим интерфейсом](#.D0.A1_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.BC_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D0.BE.D0.BC)
    *   [2.2 Другие способы бэкапа](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D1.81.D0.BF.D0.BE.D1.81.D0.BE.D0.B1.D1.8B_.D0.B1.D1.8D.D0.BA.D0.B0.D0.BF.D0.B0)
        *   [2.2.1 Консоль](#.D0.9A.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D1.8C)
        *   [2.2.2 Графические](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5)
        *   [2.2.3 Консольные и графические](#.D0.9A.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.B8_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5)
*   [3 Облачные сервисы резервного копирования](#.D0.9E.D0.B1.D0.BB.D0.B0.D1.87.D0.BD.D1.8B.D0.B5_.D1.81.D0.B5.D1.80.D0.B2.D0.B8.D1.81.D1.8B_.D1.80.D0.B5.D0.B7.D0.B5.D1.80.D0.B2.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BA.D0.BE.D0.BF.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
*   [4 Cooperative storage cloud backups](#Cooperative_storage_cloud_backups)
*   [5 Non-incremental backups](#Non-incremental_backups)
*   [6 Versioning systems](#Versioning_systems)
    *   [6.1 Version control systems](#Version_control_systems)
    *   [6.2 VCS-based backups](#VCS-based_backups)
*   [7 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Введение

Эта статья содержит информацию о различных программах, предназначенных для резервного архивирования данных. Хорошая практика - использовать регулярные бекапы важной информации, особенно конфигурационных файлов (`/etc/*`) и локальной базы данных pacman'а (обычно `/var/lib/pacman/local/*`).

Несколько слов для окончаня введения: перед тем, как начать пробовать эти программы, подумайте о том, что именно вам нужно; например, решите следущие вопросы:

*   Какой носитель данных у меня есть для хранения бекапов?
    *   cd / dvd
    *   удаленный сервер (По какому доступу? Ssh? Могу ли я устанавливать какие-нибудь программы на нем (необходимые, например, для решений, основанных на rsync)?)
    *   внежний жесткий диск
*   Как часто я собираюсь делать бекап?
    *   ежедневно?
    *   еженедельно?
    *   еще реже?
*   Какие преимущества я ожидаю от выбранного способа архивирования данных?
    *   сжатие? (по каким алгоритмам?)
    *   кодирование? (gpg или что-то более простое?)
*   Самое главное: как я планирую восстанавливать бекапы когда это понадобится?

Ладно, с этим разобрались, давайте посмотрим варианты!

## Нарастающие бекапы (Incremental backups)

Основная особенность этого способа резервного копирования состоит в том, что в начале сохраняется полная копия (зеркало) данных, которые вы хотите резервировать. А далее сохраняется только то, что было изменено, так называемые различия('diffs'). Если вы хотите часто делать бекапы, это - лучший вариант. Обычно файлы резервных копий не сжимаются и не шифруются, по этому всегда можно быстро получить рабочую копию данных. Но такой подход затрудняет записи архива на CD / DVD ..

### Резервное копирование Rsync-типа

Основной характеристикой данного типа резервного копирования, является то, что он сохраняет копию каталога, чтобы сохранить резервную копию в традиционном образе "зеркала".

Обознеаченные программы Rsync-типа также делают снимок резервного копирования путем сохранения файлов, которые описывают, какое содержимое файлов и папок изменено с момента последнего резервного копирования (так называемые 'diffs'). Следовательно они по существу инкрементальные (нарастающие), но обычно они в своём арсенале не имеют сжатия или шифрования. С другой стороны, рабочая копия сразу же доступна, - нет нееобходимости в распаковке/расшифровании. Камень предкновения програм rsync-типа это то, что они не могут легко записать и восстановить с CD или DVD.

#### Интерфейс командной строки (Консоль)

*   **[rsync](/index.php/Rsync "Rsync")** — Программа передачи данных, предназначенная для синхронизации файлов на удалённом доступе.
    *   Rsync почти всегда создает зеркало исходных данных.
    *   It is possible to restore a full backup before the most recent backup if hardlinks are allowed in the backup file system. See [Back up your data with rsync](http://www.ibm.com/developerworks/aix/library/au-spunix_rsync/index.html#backup) for more information.
    *   If hard links are not allowed, it is impossible to restore a full backup before the most recent backup (but you can use --backup to keep old versions of the files).
    *   Входит в стандартный набор пакетов всех дистрибутивов Linux.
    *   Может работать через SSH (порт 22) или родной протокол rsync (порт 873).
    *   Доступна версия под Win32.

	[http://rsync.samba.org/](http://rsync.samba.org/) || [rsync](https://www.archlinux.org/packages/?name=rsync)

*   **[rdiff-backup](https://en.wikipedia.org/wiki/Rsync#Variations "wikipedia:Rsync")** — Утилита для локального/удалённого зеркального и инкрементного бекапа.
    *   Сохраняет последнюю резервную копию, как обычные файлы.
    *   Чтобы вернуться к более старым версиям, примените Diff-файлы, чтобы создать старые версии.
    *   Создаёт покрупичные инкрементальные (дельта резервное копирование) бекапы, - сохраняет только изменения в файле; не будет создавать новую копию файла при изменении.
    *   Доступна версия Win32.

	[http://www.nongnu.org/rdiff-backup/](http://www.nongnu.org/rdiff-backup/) || [rdiff-backup](https://www.archlinux.org/packages/?name=rdiff-backup)

*   **[rsnapshot](/index.php/Rsnapshot "Rsnapshot")** — Утилита удалённого снимка файловой системы.
    *   Не хранит "diffs", вместо этого он копирует целые файлы, если они изменились.
    *   Создает жесткие ссылки между серией резервируемых путей (снимков).
    *   It is differential in that the size of the backup is only the original backup size plus the size of all files that have changed since the last backup.
    *   Destination filesystem must support hard links.
    *   Доступна версия Win32.

	[http://www.rsnapshot.org/](http://www.rsnapshot.org/) || [rsnapshot](https://www.archlinux.org/packages/?name=rsnapshot)

*   **SafeKeep** — Клиент/сервер система резервного копирования, которая использует rdiff-бекап.
    *   Integrates with Linux LVM and databases to create consistent backups.
    *   Bandwidth throttling.

	[http://safekeep.sourceforge.net/](http://safekeep.sourceforge.net/) || [safekeep](https://aur.archlinux.org/packages/safekeep/)

*   **Link-Backup** — Утилита похожая на основу Rsync-скриптов, но не использует Rsync. ПРИМЕЧАНИЕ: не разрабатывается с 2008\.
    *   Creates hard links between a series of backed-up trees (snapshots).
    *   Intelligently handles renames, moves, and duplicate files without additional storage or transfer.
    *   The backup directory contains `.catalog`, a catalog of all unique file instances; backup trees hard-link to this catalog.
    *   Transfer occurs over standard I/O locally or remotely between a client and server instance of this script.
    *   It copies itself to the server; it does not need to be installed on the server.
    *   Requires SSH for remote backups.
    *   It resumes stopped backups; it can even be told to run for an arbitrary number of minutes.

	[http://www.scottlu.com/Content/Link-Backup.html](http://www.scottlu.com/Content/Link-Backup.html) || [link-backup](https://aur.archlinux.org/packages/link-backup/)

*   **[Unison](https://en.wikipedia.org/wiki/Unison_(file_synchronizer) "wikipedia:Unison (file synchronizer)")** — A program that synchronizes files between two machines over network (LAN or Inet) using a smart diff method + rsync. Allows the user to interactively choose which changes to push, pull, or merge.

	[http://www.cis.upenn.edu/~bcpierce/unison/](http://www.cis.upenn.edu/~bcpierce/unison/) || [unison](https://www.archlinux.org/packages/?name=unison)

*   **rsync-snapshot.sh** — Another rsync shellscript with smart rotation (non-linear distribution) of backups. Integrity protection, Quotas, Rules and many more features.

	[http://blog.pointsoftware.ch/index.php/howto-local-and-remote-snapshot-backup-using-rsync-with-hard-links/](http://blog.pointsoftware.ch/index.php/howto-local-and-remote-snapshot-backup-using-rsync-with-hard-links/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **osync.sh** — Osync is a robust bidirectional file synchronization tool written in bash and based on rsync. It works on local and / or remote directories via ssh tunnels. It's mainly targeted to be launched as cron task, with features turned towards automation among:
    *   Execution time control
    *   Fault tolerance with possibility to resume on error
    *   Soft deletion, on-conflict backups with automatic cleanup
    *   Alert notifications via email
    *   Before and /or after time controlled local and / or remote command execution
    *   File monitor mode

	[http://www.netpower.fr/osync](http://www.netpower.fr/osync) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **gutbackup** — The simplest [rsync](/index.php/Rsync "Rsync") wrapper for backup Linux system.

	[https://github.com/gutenye/gutbackup](https://github.com/gutenye/gutbackup) || [gutbackup](https://aur.archlinux.org/packages/gutbackup/)

*   **trinkup** — A 60-lines bash script which holds specified amount of incremental backups using [rsync](/index.php/Rsync "Rsync") and `cp -al` to minimize amount of disk operations.

	[https://gist.github.com/ei-grad/7610406/raw/trinkup](https://gist.github.com/ei-grad/7610406/raw/trinkup) || [trinkup](https://aur.archlinux.org/packages/trinkup/)

*   **keepconf** — Is a wrapper over [rsync](/index.php/Rsync "Rsync") and [git](/index.php/Git "Git"), easy and simple to use

	[https://github.com/rfrail3/keepconf](https://github.com/rfrail3/keepconf) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

#### С графическим интерфейсом

*   **[Areca Backup](https://en.wikipedia.org/wiki/ru:Areca_Backup "wikipedia:ru:Areca Backup")** — Простое и надёжное решение для использования резервного копирования Linux и Windows.
    *   Написана на Java.
    *   Прежде всего основана на архивном бекапе (zip), но может делать файл-бекапы.
    *   Поддерживается резервное копирование Дельта (сохраняет только изменения).

	[http://areca.sourceforge.net/](http://areca.sourceforge.net/) || [areca](https://aur.archlinux.org/packages/areca/)

*   **[BackupPC](/index.php/BackupPC "BackupPC")** — Высокопроизводительная, корпоративного класса система, для резервного копирования Unix, Linux, Windows, и Mac OS X настольных ПК и ноутбуков на удаленный сервер.
    *   Дедупликация: идентичные файлы на нескольких резервных копиях одних и тех же или разных компьютерах хранятся только один раз, в результате значительная экономия дискового пространства и дискового ввода / вывода.
    *   Optional compression support further reducing disk storage.
    *   Не требуется программа для клиентской части.
    *   Простой, но мощный веб-интерфейс.

	[http://backuppc.sourceforge.net/index.html](http://backuppc.sourceforge.net/index.html) || [backuppc](https://www.archlinux.org/packages/?name=backuppc)

*   **[Back In Time](/index.php/Back_In_Time "Back In Time")** — Простой инструмент резервного копирования для Linux вдохновленный проектами [FlyBack](https://en.wikipedia.org/wiki/FlyBack "wikipedia:FlyBack") и [TimeVault](https://wiki.ubuntu.com/TimeVault/).
    *   Создает жесткие ссылки между серий резервируемых деревьев (снимки).
    *   На самом деле это всего лишь оболочка для `rsync`, `diff`, `cp`.
    *   Новый снимок создается, только если что-то изменилось с момента последнего снимка.

	[http://backintime.le-web.org/](http://backintime.le-web.org/) || [backintime](https://aur.archlinux.org/packages/backintime/) или в виде пакета prebuild из [coderkun's repo](http://arch.coderkun.de/)

*   **[FlyBack](https://en.wikipedia.org/wiki/FlyBack "wikipedia:FlyBack")** — клон Apple'овской [программы Time Machine](https://en.wikipedia.org/wiki/ru:Time_Machine_(%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B0) "wikipedia:ru:Time Machine (программа)"), резервного копирования для Mac OS X.

	[http://www.flyback-project.org/](http://www.flyback-project.org/) || [flyback](https://aur.archlinux.org/packages/flyback/)

*   **Free File Sync** — Free File Sync помогает синхронизировать файлы и папки для синхронизации Windows, Linux и Mac OS X. It is designed to save your time setting up and running backup jobs while having nice visual feedback along the way.

	[http://freefilesync.sourceforge.net/](http://freefilesync.sourceforge.net/) || [freefilesync](https://aur.archlinux.org/packages/freefilesync/)

*   **Grsync** — GTK+ интерфейс rsync

	[http://www.opbyte.it/grsync/](http://www.opbyte.it/grsync/) || [grsync](https://www.archlinux.org/packages/?name=grsync)

*   **[luckyBackup](https://en.wikipedia.org/wiki/LuckyBackup "wikipedia:LuckyBackup")** — Легкая программа для резервного копирования и синхронизации файлов.
    *   Написана на Qt и C++.
    *   Включает синхронизацию, резервное копирование (с опциями включить/исключить) и возможность восстановления.
    *   Может делать резервные копии удаленных соединений, резервное копирование по графику.
    *   Режим командной строки.

	[http://luckybackup.sourceforge.net/index.html](http://luckybackup.sourceforge.net/index.html) || [luckybackup](https://aur.archlinux.org/packages/luckybackup/)

*   **syncBackup** — Интерфейс для rsync. Утилита синхронизации и резервного копирования данных. Позволяет быстро синхронизировать содержимое папок, выборочно (по маске) удалять файлы. Возможен запуск из командной строки.

Можно задействовать сохранение резервных копий изменяемых и удаляемых файлов.

	[http://www.darhon.com/syncbackup](http://www.darhon.com/syncbackup) || [syncbackup](https://aur.archlinux.org/packages/syncbackup/)

*   **TimeShift** — TimeShift это утилита системного восстановления, которая принимает дополнительные снимки системы с помощью *rsync* и жёстких ссылок. Эти снимки могут быть восстановлены на более поздний срок, чтобы отменить все изменения, внесенные в систему после создания снимка.

Снимки могут быть сделаны вручную или через равные промежутки времени с использованием запланированных заданий.

	[https://launchpad.net/timeshift](https://launchpad.net/timeshift) || [timeshift](https://aur.archlinux.org/packages/timeshift/)

### Другие способы бэкапа

Большинство других приложений резервного копирования, как правило, для создания (больших) архивных файлов и (конечно) для отслеживания содержимого архива. В создании `.tar.bz2` или `.tar.gz` архивов, есть преимущество, что вы можете извлечь резервные копии только с tar/bzip2/gzip, так что вам не нужно иметь программу для резервного копирования.

#### Консоль

*   **Arch Backup** — Тривиальный скрипт резервного копирования с простой настройкой.
    *   Настраиваемый метод сжатия.
    *   Множественные цели резервного копирования.

	[http://code.google.com/p/archlinux-stuff/](http://code.google.com/p/archlinux-stuff/) || [arch-backup](https://aur.archlinux.org/packages/arch-backup/)

*   **hdup** — Очень простой инструмент резервного копирования, с использованием командной строки.
    *   Создаёт tar.gz или tar.bz2 архивы.
    *   Поддержка шифрования gpg.
    *   Поддержка SSH.
    *   Множественные цели резервного копирования.

	[http://miek.nl/projects/hdup2/](http://miek.nl/projects/hdup2/)  || [hdup](https://aur.archlinux.org/packages/hdup/)

*   **rdup** — Платформа для создания резервных копий, снабжённая скриптами для облегченного резервного копирования и шифрования, сжатия, передачи и упаковки для других утилит в истинном Unix-пути.
    *   Создание tar.gz архивов или копий rsync-типа.
    *   Шифрование (gpg, blowfish и другие); относится также и к копированию rsync-типа.
    *   Сжатие (также доступно для копий rsync-типа).

	[http://miek.nl/projects/rdup](http://miek.nl/projects/rdup)  || [rdup](https://aur.archlinux.org/packages/rdup/)

*   **[Duplicity](/index.php/Duplicity "Duplicity")** — A simple command-line utility which allows encrypted compressed incremental backup to nearly any storage.
    *   Supports gpg encryption and signing.
    *   Supports gzip compression.
    *   Supports full or incremental backups, incremental backup stores only difference between new and old file.
    *   Supports pushing over FTP, SSH, rsync, WebDAV, WebDAVs, HSi and Amazon S3 or local filesystem.

	[http://www.nongnu.org/duplicity/](http://www.nongnu.org/duplicity/) || [duplicity](https://www.archlinux.org/packages/?name=duplicity)

*   **[DAR](https://en.wikipedia.org/wiki/DAR_(Disk_Archiver) "wikipedia:DAR (Disk Archiver)")** — A full-featured command-line backup tool, short for Disk ARchive.
    *   It uses its own format for archives (so you need to have it around when you want to restore).
    *   Supports splitting backups into more files by size.
    *   Makefile-type config files, some custom scripts are available along with it.
    *   Supports basic encryption.
    *   Automatic backup using [cron](/index.php/Cron "Cron") is possible with [sarab](https://aur.archlinux.org/packages/sarab/).

	[http://dar.linux.free.fr/](http://dar.linux.free.fr/) || [dar](https://aur.archlinux.org/packages/dar/) [kdar](https://aur.archlinux.org/packages/kdar/) (frontend)

*   **Manent** — An algorithmically strong backup and archival program. NOTE: no upstream activity since 2009.
    *   Efficient backup to anything that looks like a storage.
    *   Works well over a slow and unreliable network.
    *   Offers online access to the contents of the backup.
    *   Backed up storage is completely encrypted.
    *   Several computers can use the same storage for backup, automatically sharing data.
    *   Not reliant on timestamps of the remote system to detect changes.
    *   Cross-platform support for Unicode file names.

	[http://code.google.com/p/manent/](http://code.google.com/p/manent/) || [manent](https://aur.archlinux.org/packages/manent/)

*   **btar** — tar-compatible archiver
    *   Fast archive creation (multicore compression or ciphering)
    *   Arbitrary chain of compression/ciphers (calls any compression/ciphering programs)
    *   Indexed archive retrieval or listing
    *   Redundancy
    *   Serialization through pipes (and only one file per backup)
    *   Can be extracted or checked with gnutar
    *   Differential backups of multiple levels
    *   Optional encoding of big files with *rsync*-differences

	[http://viric.name/cgi-bin/btar](http://viric.name/cgi-bin/btar) || [btar](https://aur.archlinux.org/packages/btar/)

*   **burp** — a network backup and restore program
    *   Uses librsync in order to save network traffic and to save on the amount of space that is used by each backup.
    *   It also uses VSS (Volume Shadow Copy Service) to make snapshots when backing up Windows computers.
    *   deduplication
    *   SSL/TLS connections
    *   automation the process of generating SSL certificates
    *   data encryption
    *   security models [[1]](http://burp.grke.org/txt/security-models.txt)

	[http://burp.grke.org](http://burp.grke.org) || [burp-backup](https://aur.archlinux.org/packages/burp-backup/)

*   **obnam** — Easy, secure backup program
    *   Snapshot backups. Every generation looks like a complete snapshot.
    *   Data chunk de-duplication, across files, and backup generations. This results in incremental backups.
    *   Optionally encrypted backups, using GnuPG.
    *   FUSE mountable backup repository.

	[http://liw.fi/obnam/](http://liw.fi/obnam/) || [obnam](https://aur.archlinux.org/packages/obnam/)

*   **System Tar & Restore** — Backup and Restore your system using tar or Transfer it with rsync
    *   CLI and Dialog interfaces
    *   Easy backup and restore wizards
    *   Creates *.tar.gz*, *.tar.bz2*, *.tar.xz* or *.tar* archives
    *   Supports openssl / gpg encryption
    *   Uses rsync to transfer a running system
    *   Supports Grub2 and Syslinux

	[https://github.com/tritonas00/system-tar-and-restore](https://github.com/tritonas00/system-tar-and-restore) || [system-tar-and-restore](https://aur.archlinux.org/packages/system-tar-and-restore/)

*   **Packrat** — A simple, modular backup system using [DAR](https://en.wikipedia.org/wiki/ru:DAR_(%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%BD%D0%BE%D0%B5_%D0%BE%D0%B1%D0%B5%D1%81%D0%BF%D0%B5%D1%87%D0%B5%D0%BD%D0%B8%D0%B5) "wikipedia:ru:DAR (программное обеспечение)")
    *   Full or incremental backups stored locally, on a remote system via [SSH](/index.php/Secure_Shell_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Secure Shell (Русский)"), or on Amazon S3

	[http://www.zeroflux.org/projects](http://www.zeroflux.org/projects) || [packrat](https://aur.archlinux.org/packages/packrat/)

*   **Attic** — A deduplicating backup program for efficient and secure backups.
    *   Space efficient storage: Variable block size deduplication is used to reduce the number of bytes stored by detecting redundant data.
    *   Optional data encryption: All data can be protected using 256-bit AES encryption and data integrity and authenticity is verified using HMAC-SHA256.
    *   Off-site backups: Any data can be stored on any remote host accessible over SSH (as long as Attic is installed).
    *   Backups mountable as filesystems: Backup archives are mountable as userspace filesystems for easy backup verification and restores.

	[https://github.com/jborg/attic/](https://github.com/jborg/attic/) || [attic](https://aur.archlinux.org/packages/attic/)

*   **Snebu** — File-level deduplicating snapshot backup with SQLite3 catalog db.
    *   Functionally similar to rsync/snapshot style backups, however does not use hardlinks in the filesystem.
    *   Backed up files are stored in lzop-compatible files, in the designated "vault" directory.
    *   Metadata stored in SQLite3 db, linking backup sets to file metadata to compressed files in the vault.
    *   Supports arbitrary retention schedules (such as daily/weekly/monthly) which can be individually expired

	[http://www.snebu.com](http://www.snebu.com) || [snebu](https://aur.archlinux.org/packages/snebu/)

*   **ZBackup** — A globally-deduplicating backup tool, based on the ideas found in *rsync*.
    *   Parallel LZMA or LZO compression of the stored data
    *   Built-in AES encryption of the stored data
    *   Possibility to delete old backup data
    *   Use of a 64-bit rolling hash, keeping the amount of soft collisions to zero
    *   Repository consists of immutable files. No existing files are ever modified
    *   Possibility to exchange data between repos without recompression

	[http://zbackup.org/](http://zbackup.org/) || [zbackup](https://aur.archlinux.org/packages/zbackup/)

#### Графические

*   **Backerupper** — Простая программа для резервного копирования выбранных каталогов в локальной сети. Главная задача, резервное копирование персональных данных пользователя.
    *   Создаёт `.tar.gz` архивы.
    *   Настраиваемая частота резервного копирования, время резервного копирования и 'max' копии.

	[http://sourceforge.net/projects/backerupper/](http://sourceforge.net/projects/backerupper/) || [backerupper](https://aur.archlinux.org/packages/backerupper/)

*   **[Déjà Dup](/index.php/Duplicity "Duplicity")** — Простая [GTK+](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GTK+ (Русский)") программа резервного копирования. It hides the complexity of doing backups the 'right way' (encrypted, off-site, and regular) and uses *duplicity* as the backend.
    *   Automatic, timed backup configurable in GUI.
    *   Restore wizard.
    *   Integrated into the GNOME Files file manager.
    *   Inherits several features of duplicity.

	[https://launchpad.net/deja-dup](https://launchpad.net/deja-dup) || [deja-dup](https://www.archlinux.org/packages/?name=deja-dup)

*   **Synkron** — Инструмент синхронизации данных каталогов.
    *   Syncs multiple folders.
    *   Can exclude files from sync based on wildcards.
    *   Restores files.
    *   Cross-platform support.

	[http://synkron.sourceforge.net/](http://synkron.sourceforge.net/) || [synkron](https://aur.archlinux.org/packages/synkron/)

#### Консольные и графические

*   **[Bacula](https://en.wikipedia.org/wiki/ru:Bacula "wikipedia:ru:Bacula")** — кроссплатформенное клиент-серверное программное обеспечение, позволяющее управлять резервным копированием, восстановлением, и проверкой данных по сети для компьютеров и операционных систем различных типов.
    *   Can be run on a single machine or used to back up an entire network.
    *   Supports Linux, UNIX, Windows, and Mac OS X backup clients.
    *   Supports a variety of backup devices, including tape libraries.
    *   Can be used to backup to multiple removable storage devices.
    *   Provides or supports command line console, GUI, and web interfaces.
    *   The back-end is a catalog stored in MySQL, PostgreSQL, or SQLite.
    *   Provides extensive documentation.
    *   Appears to be the most downloaded open source backup solution

	[http://www.bacula.org](http://www.bacula.org) || [bacula-common](https://aur.archlinux.org/packages/bacula-common/)

## Облачные сервисы резервного копирования

Смотрите также [Wikipedia:Comparison of online backup services](https://en.wikipedia.org/wiki/Comparison_of_online_backup_services "wikipedia:Comparison of online backup services").

*   **[Copy](https://en.wikipedia.org/wiki/Barracuda_Networks#Products "wikipedia:Barracuda Networks")** — A fair solution to shared folders.
    *   Бесплатно 15GB.
    *   Shared folders size are split between people.
    *   Daemon to sync files between the cloud and the computer.
    *   Almost any platform supported.
    *   Предложено шифрование AES-256.

	[https://www.copy.com/home/](https://www.copy.com/home/) || [copy-agent](https://aur.archlinux.org/packages/copy-agent/)

*   **[CrashPlan](/index.php/CrashPlan "CrashPlan")** — Онлайн/не зависящее от сайта, резервное копирование.
    *   Неограниченное онлайн-пространство за очень разумную цену.
    *   Автоматические и дополнительные резервные копии нескольким адресатам.
    *   Интуитивный графический интерфейс.
    *   Предложено шифрование и де-дублирование.
    *   Программное обеспечение является бесплатным для локального применения.
    *   Restore prevents simultaneous backing up

	[http://www.crashplan.com/](http://www.crashplan.com/) || [crashplan](https://aur.archlinux.org/packages/crashplan/)

*   **[Dropbox](/index.php/Dropbox "Dropbox")** — Популярный сервис обмена файлами.
    *   Демон контролирует указанный каталог, и загружает дополнительные изменения в dropbox.com.
    *   Изменения автоматически отображаются на ваших других компьютерах.
    *   Включает в себя совместное использование файлов и общественных каталогов.
    *   Вы можете восстановить удаленные файлы.
    *   Написанные сообществом дополнения.
    *   На бесплатном аккаунте предоставлено 2 Гб.

	[http://www.dropbox.com](http://www.dropbox.com) || [dropbox](https://aur.archlinux.org/packages/dropbox/) [nautilus-dropbox](https://aur.archlinux.org/packages/nautilus-dropbox/)

*   **[Google Drive](https://en.wikipedia.org/wiki/Google_Drive "wikipedia:Google Drive")** — Хранилище файлов и сервис синхронизации, предоставляемый Google.
    *   Обеспечивает облачное хранилище, совместное использование и совместное редактирование файлов.
    *   Доступно несколько клиентов.

	[https://drive.google.com](https://drive.google.com) || [google-drive-ocamlfuse](https://aur.archlinux.org/packages/google-drive-ocamlfuse/) (бесплатный), [drive](https://aur.archlinux.org/packages/drive/) (бесплатный), [insync](https://aur.archlinux.org/packages/insync/) (non-free)

*   **[Jungle Disk](https://en.wikipedia.org/wiki/Jungle_Disk "wikipedia:Jungle Disk")** — Интерактивный инструмент резервного копирования, который хранит свои данные в Amazon S3 или Rackspace Cloud Files.
    *   Файл-расширение для GNOME.
    *   Доступны только платные варианты.

	[http://www.jungledisk.com/](http://www.jungledisk.com/) || [nautilus-jungledisk](https://aur.archlinux.org/packages/nautilus-jungledisk/)

*   **[Облако Mail.Ru](https://en.wikipedia.org/wiki/%D0%9E%D0%B1%D0%BB%D0%B0%D0%BA%D0%BE_Mail.Ru "wikipedia:Облако Mail.Ru")** — Облачное хранилище данных российской компании Mail.Ru Group.

	[https://cloud.mail.ru/](https://cloud.mail.ru/) || [mailru-cloud](https://aur.archlinux.org/packages/mailru-cloud/)

*   **[MEGA](https://en.wikipedia.org/wiki/ru:Mega "wikipedia:ru:Mega")** — Преемник сервиса обмена данными MegaUpload.
    *   На бесплатном аккаунте предоставлено 50GB, воспользуйтесь платным чтобы получить больше места.
    *   Шифрование и де-дубликация данных.
    *   Обычный доступ через веб-интерфейс, но существуют и другие инструменты.

	[https://mega.co.nz](https://mega.co.nz) || [megatools](https://aur.archlinux.org/packages/megatools/), [megasync](https://aur.archlinux.org/packages/megasync/), [megafuse](https://aur.archlinux.org/packages/megafuse/)

*   **Nutstore** — Облачный сервис, который позволяет синхронизировать и обмениваться файлами повсюду.
    *   Multiple file folders sync.
    *   Сервис для Китайских пользователей.

	[http://jianguoyun.com/](http://jianguoyun.com/) || [nutstore](https://aur.archlinux.org/packages/nutstore/)

*   **[SpiderOak](https://en.wikipedia.org/wiki/SpiderOak "wikipedia:SpiderOak")** — An online backup tool for Windows, Mac and Linux users to back up, share, sync, access and store their data.
    *   Доступны бесплатные и платные верси.
    *   Бесплатный аккаунт на 2GB.
    *   Includes file sharing and a public directory.
    *   Incremental backup and sync are both supported.

	[https://spideroak.com/](https://spideroak.com/) || [spideroak](https://aur.archlinux.org/packages/spideroak/)

*   **[Storage Made Easy](https://en.wikipedia.org/wiki/Storage_Made_Easy "wikipedia:Storage Made Easy")** — Обеспечивает единый доступ к многочисленным сервисам облачных систем хранения данных, а также к собственному хранилищу.
    *   Доступны бесплатные и платные версии.
    *   Бесплатный аккаунт имеет 5 Гб и позволяет получить доступ до трех других облачных систем хранения данных.
    *   Поддержка локальных каталогов через fuse, а так же через веб-доступ.
    *   Поддерживает множество облачных сервисов хранения, таких как Box, Dropbox, Google Drive, Onedrive, и другие.

	[http://storagemadeeasy.com/](http://storagemadeeasy.com/) || [smestorage](https://aur.archlinux.org/packages/smestorage/)

*   **[Tahoe-LAFS](https://en.wikipedia.org/wiki/Tahoe-LAFS "wikipedia:Tahoe-LAFS")** — Tahoe Least-Authority Filesystem is a free and open, secure, decentralized, fault-tolerant, peer-to-peer distributed data store and distributed file system.

	[https://tahoe-lafs.org/](https://tahoe-lafs.org/) || [tahoe-lafs](https://aur.archlinux.org/packages/tahoe-lafs/)

*   **[Tarsnap](https://en.wikipedia.org/wiki/Tarsnap "wikipedia:Tarsnap")** — Безопасный онлайн-сервис резервного копирования для BSD, Linux, OS X, Solaris и Windows (через Cygwin).
    *   Сжатые, зашифрованные резервные копии на серверах Amazon S3.
    *   Автоматизация с помощью [cron](/index.php/Cron "Cron").
    *   Инкрементный бэкап.
    *   Бэкап любых файлов и каталогов.
    *   Клиент только в командной строке.
    *   Вы платите только за использование (пропускной способности и места хранения).

	[http://www.tarsnap.com](http://www.tarsnap.com) || [tarsnap](https://www.archlinux.org/packages/?name=tarsnap)

*   **[iDrive](https://en.wikipedia.org/wiki/IDrive_Inc. "wikipedia:IDrive Inc.")** — Универсальный онлайн бекап.
    *   Несколько устройства резервного копирования.
    *   Онлайн синхронизация файлов.
    *   Резервное копирование в режиме реального времени.
    *   Резервное копирование и доступ с мобильных устройств.
    *   Дистанционное Управление.
    *   Нет графического интерфейса для Linux, на основе командной строки. Сценарий оболочки можно сделать проще используя

	[https://www.idrive.com/](https://www.idrive.com/) || [idevsutil](https://aur.archlinux.org/packages/idevsutil/), [idrive-wrapper](https://aur.archlinux.org/packages/idrive-wrapper/)

*   **CloudBacko** — Корпоративная утилита облачного резервирования для Linux, Mac и Windows.
    *   Закрытый код. Бесплатная, доступны версии Lite и Pro.
    *   Написана на Java.
    *   Зашифрованное резервное копирование на несколько облачных направлений.
    *   Поддержка нескольких облачных направлений объединеных в один пул хранения.
    *   Не требует установки в бесплатной версии.
    *   Графический интерфейс для Linux в версии Pro.
    *   В версии Pro доступно резервное копирование виртуальной машины.

	[http://www.cloudbacko.com/](http://www.cloudbacko.com/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

## Cooperative storage cloud backups

A [cooperative storage cloud](https://en.wikipedia.org/wiki/Cooperative_storage_cloud "wikipedia:Cooperative storage cloud") is a decentralized model of networked online storage where data is stored on multiple computers, hosted by the participants cooperating in the cloud.

*   **[Symform](http://www.symform.com)** — A peer-to-peer cloud backup service.
    *   Unlimited free backup in exchange for 2:1 storage space contribution with an always-connected device (at least 80% uptime).
    *   [Payment options exist](http://www.symform.com/our-solutions/pricing/).
    *   First 10GB of backup storage is free (no contribution needed).
    *   In addition to paid support, support plans in exchange for extended contribution (300GB+) exist.
    *   Automatic and incremental backups.
    *   Data is encrypted before leaving the computer, though keys are also stored on the Symform's servers.[[2]](http://virtualserverguy.com/blog/2012/12/19/symform-security-analysis)
    *   Customizable limits for bandwidth consumption.
    *   Ability to have a local copy ("Hot Copy") of the backed up data on a different disk or computer.
    *   Ability to have synchronized folders between nodes (Dropbox-like).
    *   Closed source, using mono. Windows clients available.

	[http://www.symform.com/](http://www.symform.com/) || [symform](https://aur.archlinux.org/packages/symform/)

## Non-incremental backups

Another type of backups are those used in case of a disaster. These include application that allow easy backup of entire filesystems and recovery in case of failure, usually in the form of a Live CD or USB drive. The contains complete system images from one or more specific points in time and are frequently used by to record known good configurations.

*   **Q7Z** — P7Zip GUI for Linux, which attempts to simplify data compression and backup. It can create the following archive types: 7z, BZip2, Zip, GZip, Tar.
    *   Updates existing archives quickly.
    *   Backup multiple folders to a storage location.
    *   Create or extract protected archives.
    *   Lessen effort by using archiving profiles and lists.

	[http://k7z.sourceforge.net/](http://k7z.sourceforge.net/) || [q7z](https://aur.archlinux.org/packages/q7z/)

*   **[Partclone](/index.php/Partclone "Partclone")** — A tool that can be used to back up and restore a partition while considering only used blocks.
    *   Supports ext2, ext3, hfs+, reiser3.5, reiser3.6, reiser4, ext4 and btrfs.
    *   Supports compression.

	[http://partclone.org/](http://partclone.org/) || [partclone](https://www.archlinux.org/packages/?name=partclone)

*   **[Redo Backup and Recovery](https://en.wikipedia.org/wiki/Redo_Backup_and_Recovery "wikipedia:Redo Backup and Recovery")** — A backup and disaster recovery application that runs from a bootable Linux CD image.
    *   Is capable of bare-metal backup and recovery of disk partitions.
    *   Uses [xPUD](http://www.xpud.org/) and [Partclone](/index.php/Partclone "Partclone") for the backend.

	[http://www.redobackup.org/](http://www.redobackup.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[Clonezilla](https://en.wikipedia.org/wiki/Clonezilla "wikipedia:Clonezilla")** — A disaster recovery, disk cloning, disk imaging and deployment solution.
    *   Boots from live CD, USB flash drive, or PXE server.
    *   Supports ext2, ext3, ext4, reiserfs, reiser4, xfs, jfs, btrfs FAT32, NTFS, HFS+ and others.
    *   Uses Partclone (default), Partimage (optional), ntfsclone (optional), or dd to image or clone a partition.
    *   Multicasting server to restore to many machines at once.

	[http://clonezilla.org/](http://clonezilla.org/) || [clonezilla](https://www.archlinux.org/packages/?name=clonezilla)

*   **[Partimage](https://en.wikipedia.org/wiki/Partimage "wikipedia:Partimage")** — A disk cloning utility for Linux/UNIX environments.
    *   Has a Live CD.
    *   Supports the most popular filesystems on Linux, Windows and Mac OS.
    *   Compression.
    *   Saving to multiple CDs or DVDs or across a network using Samba/NFS.

	[http://www.partimage.org/Main_Page](http://www.partimage.org/Main_Page) || [partimage](https://www.archlinux.org/packages/?name=partimage)

*   **FSArchiver** — A safe and flexible file-system backup and deployment tool
    *   Support for basic file attributes (permissions, owner, ...).
    *   Support for multiple file-systems per archive.
    *   Support for extended attributes (they are used by SELinux).
    *   Support the basic file-system attributes (label, uuid, block-size) for all linux file-systems.
    *   Support for [ntfs filesystems](http://www.fsarchiver.org/Cloning-ntfs) (ability to create flexible clones of a Windows partitions).
    *   Checksumming of everything which is written in the archive (headers, data blocks, whole files).
    *   Ability to restore an archive which is corrupt (it will just skip the current file).
    *   Multi-threaded lzo, gzip, bzip2, lzma compression.
    *   Support for splitting large archives into several files with a fixed maximum size.
    *   Encryption of the archive using a password. Based on blowfish from libcrypto from [OpenSSL](/index.php/OpenSSL "OpenSSL").
    *   Support backup of a mounted root filesystem (-A option).

	[http://www.fsarchiver.org/Main_Page](http://www.fsarchiver.org/Main_Page) || [fsarchiver](https://www.archlinux.org/packages/?name=fsarchiver)

*   **[Mondo Rescue](https://en.wikipedia.org/wiki/Mondo_Rescue "wikipedia:Mondo Rescue")** — A disaster recovery solution to create backup media that can be used to redeploy the damaged system.
    *   Image-based backups, supporting Linux/Windows.
    *   Compression rate is adjustable.
    *   Can backup live systems (without having to halt it).
    *   Can split image over many files.
    *   Supports booting to a Live CD to perform a full restore.
    *   Can backup/restore over NFS, from CDs, tape drives and and other media.
    *   Can verify backups.

	[http://www.mondorescue.org/](http://www.mondorescue.org/) || [mondo](https://aur.archlinux.org/packages/mondo/)

## Versioning systems

These are traditionally used for keeping track of software development; but if you want to have a simple way to manage your config files in one directory, it might be a good solution.

### Version control systems

See also [Wikipedia:Comparison of revision control software](https://en.wikipedia.org/wiki/Comparison_of_revision_control_software "wikipedia:Comparison of revision control software").

*   **[Git](/index.php/Git "Git")** — A distributed revision control and source code management system with an emphasis on speed.
    *   Very easy creation, merging, and deletion of branches.
    *   Nearly all operations are performed locally, giving it a huge speed advantage on centralized systems.
    *   Has a "staging area" or "index", this is an intermediate area where commits can be formatted and reviewed before completing the commit.
    *   Does not handle binary files very well.

	[http://git-scm.com/](http://git-scm.com/) || [git](https://www.archlinux.org/packages/?name=git)

*   **[Subversion](/index.php/Subversion "Subversion")** — A full-featured centralized version control system originally designed to be a better CVS.
    *   Renamed/copied/moved/removed files retain full revision history.
    *   Native support for binary files, with space-efficient binary-diff storage.
    *   Costs proportional to change size, not to data size.
    *   Allows arbitrary metadata ("properties") to be attached to any file or directory.

	[http://subversion.apache.org/](http://subversion.apache.org/) || [subversion](https://www.archlinux.org/packages/?name=subversion)

*   **[Mercurial](/index.php/Mercurial "Mercurial")** — A distributed version control system written in Python and similar in many ways to Git.
    *   Platform independent.
    *   Support for [extensions](http://mercurial.selenic.com/wiki/UsingExtensions).
    *   A set of commands consistent with Subversion.
    *   Supports tags.

	[http://mercurial.selenic.com/](http://mercurial.selenic.com/) || [mercurial](https://www.archlinux.org/packages/?name=mercurial)

*   **[Bazaar](https://en.wikipedia.org/wiki/Bazaar_(software) "wikipedia:Bazaar (software)")** — A distributed version control system that helps you track project history over time and to collaborate easily with others.
    *   Similar commands to Subversion.
    *   Supports working with or without a central server.
    *   Support for working with some other revision control systems
    *   Complete Unicode support.

	[http://bazaar.canonical.com/en/](http://bazaar.canonical.com/en/) || [bzr](https://www.archlinux.org/packages/?name=bzr)

*   **[Darcs](https://en.wikipedia.org/wiki/Darcs "wikipedia:Darcs")** — A distributed revision control system that was designed to replace traditional, centralized source control systems such as CVS and Subversion.
    *   Offline mode.
    *   Easy branching and merging.
    *   Written in Haskell.
    *   Not very fast.

	[http://darcs.net/](http://darcs.net/) || [darcs](https://www.archlinux.org/packages/?name=darcs)

### VCS-based backups

*   **Gibak** — A backup system based on [Git](/index.php/Git "Git").
    *   Supports binary diffs.
    *   Uses all of Git's features (such as `.gitignore` for filtering files).
    *   Uses Git's hook system to save information that Git does not (permissions, mtime, empty directories, etc).

	[https://github.com/pangloss/gibak](https://github.com/pangloss/gibak) || [gibak](https://aur.archlinux.org/packages/gibak/)

*   **bup** — A fledgling Git-based backup solution written in [python](/index.php/Python_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Python (Русский)") and C.
    *   Uses a rolling checksum algorithm (similar to *rsync*) to split large files into chunks.
    *   Can back up directly to a remote bup server.
    *   Has an improved index format to allow you to track many files.

	[https://github.com/bup/bup](https://github.com/bup/bup) || [bup](https://www.archlinux.org/packages/?name=bup) [bup-git](https://aur.archlinux.org/packages/bup-git/)

*   **ColdStorage** — Another backup tool using Git at its core, written in [Qt](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)").

	[http://gitorious.org/coldstorage](http://gitorious.org/coldstorage) || [coldstorage-git](https://aur.archlinux.org/packages/coldstorage-git/)

## Смотрите также

*   [Краткий обзор open source средств резервного копирования](http://habrahabr.ru/company/centosadmin/blog/220555/)
*   [Backing up Linux and other Unix(-like) systems](http://www.halfgaar.net/backing-up-unix)
*   [Mirroring an Entire Site using Rsync over SSH](http://www.askapache.com/security/mirror-using-rsync-ssh.html)
*   [Performance comparison of five remote incremental backup tools: Rsync, Rdiff-backup, Duplicity, Areca and Link-Backup](http://www.si-journal.org/index.php/JSI/article/view/205)