Ссылки по теме

*   [System backup](/index.php/System_backup "System backup")
*   [Клонирование диска](/index.php/%D0%9A%D0%BB%D0%BE%D0%BD%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5_%D0%B4%D0%B8%D1%81%D0%BA%D0%B0 "Клонирование диска")
*   [List of applications#File sharing](/index.php/List_of_applications#File_sharing "List of applications")
*   [Обслуживание системы#Резервное копирование](/index.php/%D0%9E%D0%B1%D1%81%D0%BB%D1%83%D0%B6%D0%B8%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B#Резервное_копирование "Обслуживание системы")
*   [Dotfiles](/index.php/Dotfiles "Dotfiles")
*   [File recovery](/index.php/File_recovery "File recovery")

**Состояние перевода:** На этой странице представлен перевод статьи [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs"). Дата последней синхронизации: 1 марта 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Synchronization_and_backup_programs&diff=0&oldid=566243).

Эта статья содержит список и сравнение программ для синхронизации данных между двумя и более местоположениями, а также программ с расширенными возможностями, например, инкрементным резервным копированием. Данные темы достаточно схожи между собой и, соответственно, описываются в одной статье.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Введение в резервное копирование](#Введение_в_резервное_копирование)
*   [2 Синхронизация данных](#Синхронизация_данных)
    *   [2.1 Легенда](#Легенда)
    *   [2.2 Таблица](#Таблица)
*   [3 Инкрементное резервное копирование](#Инкрементное_резервное_копирование)
    *   [3.1 Одно устройство](#Одно_устройство)
        *   [3.1.1 Инкременты на основе фрагментов (chunks)](#Инкременты_на_основе_фрагментов_(chunks))
        *   [3.1.2 Инкременты на основе файлов](#Инкременты_на_основе_файлов)
    *   [3.2 Сетевая структура](#Сетевая_структура)
*   [4 Системы управления версиями](#Системы_управления_версиями)
*   [5 Смотрите также](#Смотрите_также)

## Введение в резервное копирование

Создание резервных копий является необходимой мерой, поскольку ошибки, совершаемые людьми и машинами, могут приводить к повреждению данных; физические носители также разрушаются со временем и однажды перестают работать. Чтобы выбрать лучшую программу для своих нужд, нужно учесть следующие моменты:

*   тип носителя данных, используемый для бэкапов: CD, DVD, удалённый сервер, внешний жёсткий диск и т.д.;
*   планируемая частота создания бэкапов: ежедневно, еженедельно, ежемесячно и т.д.;
*   возможности, ожидаемые от инструмента: сжатие, шифрование, обработка переименований и т.д.;
*   планируемый метод восстановления из бэкапов при необходимости.

## Синхронизация данных

Эти приложения просто «зеркалируют» содержимое каталогов по нескольким местам. Тем не менее большинство из них позволяют сохранять и возвращать старые версии изменённых или удалённых файлов.

См. также:

*   [List of applications/Utilities#File synchronization](/index.php/List_of_applications/Utilities#File_synchronization "List of applications/Utilities")
*   [List of applications/Internet#Cloud synchronization clients](/index.php/List_of_applications/Internet#Cloud_synchronization_clients "List of applications/Internet")
*   [Wikipedia:Comparison of file synchronization software](https://en.wikipedia.org/wiki/Comparison_of_file_synchronization_software "wikipedia:Comparison of file synchronization software")

### Легенда

	Название

	Название приложения, со ссылкой на ArchWiki или официальный сайт.

	Пакет

	Ссылка на пакет.

	Реализация

	Язык программирования, библиотеки или утилиты, на базе которых создано приложение.

	Delta transfer

	Передача только изменённых частей файла.

	Зашифрованная передача

	Передача данных зашифрованном виде по умолчанию при использовании сети.

	Метаданные ФС

	Сохранение прав доступа и атрибутов файловой системы.

	Возобновляемая

	Возможность возобновления синхронизации в случае её прерывания.

	Переименования

	Перемещённые/переименованные файлы определяются и не хранятся или не передаются дважды. Обычно это означает подсчёт хеш-сумм файлов или их частей. Приложения без поддержки этого можно комбинировать с [hsync](https://aur.archlinux.org/packages/hsync/), который синхронизирует *только* переименования.

	Контроль версий

	Сохранение старых версий файла (*reverse incremental backup*).

	Передача изменений

	В каких направлениях могут передаваться изменения.

*   *односторонняя* синхронизация между двумя местами;
*   *двухсторонняя* синхронизация между двумя местами;
*   *многосторонняя* — полная синхронизация между более чем двумя местами.

	Решение конфликтов

	Обработка конфликтов файлов, автоматически или интерактивно, то есть приложение не отклоняет конфликтующие файлы молча. Неприменимо для приложений с односторонней синхронизацией.

	Мониторинг ФС

	Обработка приложением событий файловой системы для запуска синхронизации.

	CLI

	Наличие у приложения интерфейса командной строки.

	Другие интерфейсы

	Наличие указанных пользовательских интерфейсов, например GUI, TUI или web.

	Лицензия

	Лицензия серверного и клиентского приложения.

	Другие платформы

	Поддержка других операционных систем помимо Linux.

	Поддержка

	Поддерживается ли сейчас проект разработчиками.

	Особенности

	Заметки об особых функциях, которые выделяют приложение среди других.

### Таблица

| Название | Пакет | Реализация | Delta transfer | Зашифрованная передача | Метаданные ФС | Возобновляемая | Переименования | Контроль версий | Передача изменений | Решение конфликтов | Мониторинг ФС | CLI | Другие интерфейсы | Лицензия | Другие платформы | Поддержка | Особенности |
| [FreeFileSync](https://www.freefilesync.org/) | [freefilesync](https://aur.archlinux.org/packages/freefilesync/) | C++ | ? | SFTP [[1]](http://www.freefilesync.org/faq.php#features) | ? | ? | Да [[2]](http://www.freefilesync.org/faq.php#features) | Да [[3]](http://www.freefilesync.org/manual.php?topic=versioning) | **одно**сторонняя / **много**сторонняя | Да | ? | Нет | Да | GPL | Windows, macOS | Да |
| [git-annex](https://git-annex.branchable.com/) | [git-annex](https://www.archlinux.org/packages/?name=git-annex) | Haskell, git | rsync [[4]](http://git-annex.branchable.com/transferring_data/) | rsync [[5]](http://git-annex.branchable.com/transferring_data/) | ? | ? | ? | Да | **много**сторонняя; with git remotes [[6]](http://git-annex.branchable.com/sync/) | переименование конфликтующих файлов [[7]](http://git-annex.branchable.com/automatic_conflict_resolution/) | ? | Да | [git-annex assistant](http://git-annex.branchable.com/assistant/) | GPLv3 | macOS, Android (beta), Windows (beta) | Да | Manage files with git |
| [osync.sh](http://www.netpower.fr/osync) | [osync](https://aur.archlinux.org/packages/osync/) | Bash, based on rsync | rsync | rsync | ? | Да | Нет | Да | **двух**сторонняя | сохраняет несколько версий файла [[8]](http://www.netpower.fr/sites/default/files/soft/html-doc/osync_v1.2.html#toc-Subsubsection-1.3.1) | опционально [[9]](https://github.com/deajan/osync#daemon-mode) | Да | Нет | BSD | Да |
| [rclone](https://rclone.org/) | [rclone](https://www.archlinux.org/packages/?name=rclone) | Go | Нет [[10]](https://rclone.org/faq/#why-doesn-t-rclone-support-partial-transfers-binary-diffs-like-rsync) | ? | ? | ? | ? | ? | **одно**сторонняя [[11]](https://rclone.org/faq/#can-rclone-do-bi-directional-sync) | ? | ? | Да | [RcloneBrowser](https://github.com/mmozeiko/RcloneBrowser) | MIT | *BSD, Plan9, Solaris, Windows, macOS | Да | Оптимизировано для работы с облачными хранилищами, поведение варьируется в зависимости от возможностей удалённого хранилища. |
| [rdiff-backup](http://www.nongnu.org/rdiff-backup/) | [rdiff-backup](https://www.archlinux.org/packages/?name=rdiff-backup) | Python 2, librsync | rsync | rsync | Да | ? | Нет | Да | **одно**сторонняя | Нет | Да | Нет | GPL | Win32 | ? |
| [Resilio Sync](/index.php/Resilio_Sync "Resilio Sync") | [rslsync](https://aur.archlinux.org/packages/rslsync/) | C++ | Да | Да | ? | Да | ? | Да | **много**сторонняя | ? | ? | Нет | Web | Proprietary freemium | FreeBSD, Windows, macOS, Android, iOS, Windows Phone, Amazon Kindle Fire | Да | P2P sync |
| [rsync](/index.php/Rsync "Rsync") | [rsync](https://www.archlinux.org/packages/?name=rsync) | C | Да | SSH или свой протокол | Да | Да | Нет | 

*   `--link-dest` с жёсткими ссылками [[12]](http://www.ibm.com/developerworks/aix/library/au-spunix_rsync/index.html#backup)
*   `--backup`

 | **одно**сторонняя | Нет | Да | [Rsync#Front-ends](/index.php/Rsync#Front-ends "Rsync") | GPLv3 | Win32 | Да | Стандартный инструмент, доступный во всех дистрибутивах Linux. |
| [SparkleShare](https://sparkleshare.org/) | [sparkleshare](https://www.archlinux.org/packages/?name=sparkleshare) | C#, git | Да | AES-256 [[13]](https://github.com/hbons/SparkleShare/wiki/Client-Side-Encryption) | ? | ? | Да | Да | ? | ? | ? | Нет | Да | GPLv3 | Windows, macOS | Да | Может синхронизировать с любым Git-сервером через SSH. |
| [Syncany](https://www.syncany.org/) | [syncany](https://aur.archlinux.org/packages/syncany/) | Java | ? | ? | ? | ? | ? | ? | ? | ? | ? | Да | Да | GPLv3 | Нет [[14]](https://github.com/syncany/syncany/graphs/contributors) |
| [Syncthing](/index.php/Syncthing "Syncthing") | [syncthing](https://www.archlinux.org/packages/?name=syncthing) | Go | Да [[15]](http://docs.syncthing.net/users/faq.html#is-synchronization-fast) | Да [[16]](http://docs.syncthing.net/users/security.html) | частично [[17]](http://docs.syncthing.net/users/faq.html#what-things-are-synced) | Да | ? | Да [[18]](http://docs.syncthing.net/users/versioning.html), старые версии перемещаются в архивный каталог | **много**сторонняя | переименовывает один файл [[19]](https://docs.syncthing.net/users/faq.html#what-if-there-is-a-conflict) | Да | Да | Web, GTK | MPL v2 | BSD, Windows, macOS, Android, Kindle Paperwhite | Да | P2P sync |
| [Synkron](http://synkron.sourceforge.net/) | [synkron](https://aur.archlinux.org/packages/synkron/) | C++ | ? | ? | ? | ? | ? | ? | **много**сторонняя | ? | ? | Нет | Qt | GPLv2 | Windows, macOS | [No](https://sourceforge.net/projects/synkron/) |
| [taskd](/index.php/Taskd "Taskd") | [taskd](https://aur.archlinux.org/packages/taskd/) | C++, Python | Да | Да | ? | Да | ? | ? | **много**сторонняя | ? | Нет | Да | Нет | MIT | Android | Да |
| [Unison](/index.php/Unison "Unison") | [unison](https://www.archlinux.org/packages/?name=unison) | OCaml | Да | Да | частично [[20]](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html#perms) | опционально [[21]](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html#speeding) | Нет | Да [[22]](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html#backups) | **двух**сторонняя | interactive | Нет | Да | GTK2 | GPL | FreeBSD, Windows, macOS, Android | Да [[23]](http://www.cis.upenn.edu/~bcpierce/unison/status.html) |

## Инкрементное резервное копирование

Приложения, которые могут создавать [инкрементные резервные копии](https://en.wikipedia.org/wiki/Incremental_backup "wikipedia:Incremental backup"), запоминают и учитывают, какие данные были скопированы во время последнего запуска (так называемые «различия») и устраняют необходимость хранить дубликаты неизменённых данных. Восстановление данных к определённому моменту времени потребует размещения последней полной резервной копии и всех инкрементных резервных копий с того момента, когда предполагается, что они будут восстановлены. Этот вид бэкапов полезен для тех, кто делает их очень часто.

См. также:

*   [Список приложений/Безопасность#Резервное копирование](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9/%D0%91%D0%B5%D0%B7%D0%BE%D0%BF%D0%B0%D1%81%D0%BD%D0%BE%D1%81%D1%82%D1%8C#Резервное_копирование "Список приложений/Безопасность")
*   [Wikipedia:List of backup software](https://en.wikipedia.org/wiki/List_of_backup_software "wikipedia:List of backup software")
*   [Wikipedia:Comparison of backup software](https://en.wikipedia.org/wiki/Comparison_of_backup_software "wikipedia:Comparison of backup software")
*   [Wikipedia:Comparison of online backup services](https://en.wikipedia.org/wiki/Comparison_of_online_backup_services "wikipedia:Comparison of online backup services")

**Легенда:**

*   **Название**: название приложения, со ссылкой на ArchWiki или официальный сайт.
*   **Пакет**: ссылка на пакет.
*   **Реализация**: язык программирования, библиотеки или утилиты, на базе которых создано приложение.
*   **Сжатое хранилище**: использование сжатия для хранилища бэкапов.
*   **Зашифрованное хранилище**: использование шифрования для хранилища бэкапов.
*   **Delta transfer**: передача только изменённых частей файла.
*   **Зашифрованная передача**: передача данных зашифрованном виде по умолчанию при использовании сети.
*   **Метаданные ФС**: сохранение прав доступа и атрибутов файловой системы.
*   **Лёгкий доступ**: бэкап хранится как есть на файловой системе или может быть примонтирован для удобной работы с ним.
*   **Возобновляемая**: возможность возобновления синхронизации в случае её прерывания.
*   **Переименования**: перемещённые/переименованные файлы определяются и не хранятся или не передаются дважды. Обычно это означает подсчёт хеш-сумм файлов или их частей.
*   **CLI**: наличие у приложения интерфейса командной строки, что означает возможность использования в скриптах.
*   **Другие интерфейсы**: наличие указанных пользовательских интерфейсов, например GUI, TUI или web.
*   **Лицензия**: лицензия серверного и клиентского приложения.
*   **Другие платформы**: поддержка других операционных систем помимо Linux.
*   **Поддержка**: поддерживается ли сейчас проект разработчиками.
*   **Особенности**: заметки об особых функциях, которые выделяют приложение среди других.

### Одно устройство

Эти приложения ориентированы на бэкап данных того устройства, на котором они установлены, хотя место для хранения бэкапов может быть расположено на внешнем хранилище или другой системе.

#### Инкременты на основе фрагментов (chunks)

При изменении файла приложении сохраняют только изменившиеся *части* в следующем снимке. В отличие от [инкрементов на основе файлов](#Инкременты_на_основе_файлов), они более экономно расходуют место, особенно когда есть большие файлы с малыми изменениями; с другой стороны, такие бэкапы могут быть прочитаны только тем приложением, которое их создало, так как исходные файлы должны быть реконструированы по сохранённым в бэкапе различиям между версиями.

| Название | Пакет | Реализация | Сжатое хранилище | Зашифрованное хранилище | Delta transfer | Зашифрованная передача | Метаданные ФС | Лёгкий доступ | Возобновляемая | Переименования | CLI | Другие интерфейсы | Лицензия | Другие платформы | Поддержка | Особенности |
| [Areca Backup](http://areca.sourceforge.net/) | [areca](https://aur.archlinux.org/packages/areca/) | Java | Zip, Zip64 | AES128, AES256 | Да | Да | Да | Нет | Pausing only | Нет | Да | Да | GPLv2 | Windows | Да |
| [BorgBackup](http://borgbackup.readthedocs.org/en/stable/) | [borg](https://www.archlinux.org/packages/?name=borg) | Python, C (Cython) | lz4, zlib, lzma, zstd | AES256 | Да | SSH | Да [[24]](http://borgbackup.readthedocs.org/en/stable/faq.html#which-file-types-attributes-etc-are-preserved) | Да [[25]](http://borgbackup.readthedocs.org/en/stable/usage.html#borg-mount) | Да [[26]](http://borgbackup.readthedocs.org/en/stable/faq.html#if-a-backup-stops-mid-way-does-the-already-backed-up-data-stay-there) | Да | Да | third party | BSD | *BSD, macOS, Windows (Cygwin / WSL)[[27]](https://borgbackup.readthedocs.io/en/stable/#main-features) | Да | Deduplication based on variable length chunks; support both local and SSH-based remote backup destination. |
| [btar](http://viric.name/cgi-bin/btar) | [btar](https://aur.archlinux.org/packages/btar/) | C | Да | Да | Да | Да | ? | Нет | ? | ? | Да | Нет | GPLv3 | Да | Redundancy, indexed extraction, multicore compression, input and output serialisation, tolerance to partial archive errors. |
| [bup](https://bup.github.io/) | [bup](https://www.archlinux.org/packages/?name=bup) [bup-git](https://aur.archlinux.org/packages/bup-git/) | C, Python, git | Да | Нет | Да | Да | Immature | Да [[28]](https://bup.github.io/man/bup-fuse.html) | pick up where you left off [[29]](https://github.com/bup/bup/blob/master/README.md#reasons-bup-is-awesome) | Да | Да | [bups](https://aur.archlinux.org/packages/bups/) | GPLv2 | NetBSD, Windows, macOS | Да | Same storage format as git. |
| [Duplicati](http://www.duplicati.com/) | [duplicati-latest](https://aur.archlinux.org/packages/duplicati-latest/) | C# | Да | Да | Да | Да | Да | Нет | Pausing only | Нет | Да | Да | LGPL | Windows | Да |
| [Duplicity](/index.php/Duplicity "Duplicity") | [duplicity](https://www.archlinux.org/packages/?name=duplicity) | librsync | gzip | gpg | Да | Да | ? | Нет | Да | Нет | Да | [Yes](/index.php/Duplicity#Front-ends "Duplicity") | GPL | Да |
| [Kup Backup System](http://kde-apps.org/content/show.php/Kup+Backup+System?content=147465) | [kup](https://www.archlinux.org/packages/?name=kup) | rsync, bup front-end | Да | Да | Да | Да | Immature | Да | Нет | Да | bup | Qt | GPLv2 | Да |
| [obnam](https://obnam.org/) | [obnam](https://aur.archlinux.org/packages/obnam/) | Python | Да | GnuPG | Да | Да | ? | Да | checkpoints every 100MB | ? | Да | Нет | GPLv3 | [No](https://blog.liw.fi/posts/2017/08/13/retiring_obnam/) |
| [restic](https://restic.net/) | [restic](https://www.archlinux.org/packages/?name=restic) [restic-git](https://aur.archlinux.org/packages/restic-git/) | Go | Нет [[30]](https://github.com/restic/restic/issues/21) | AES-256 [[31]](https://github.com/restic/restic/blob/master/doc/Design.md) | Да | Да | Да [[32]](https://restic.readthedocs.io/en/latest/manual_rest.html#metadata-handling) | Да [[33]](https://restic.readthedocs.io/en/stable/050_restore.html#restore-using-mount) | Да [[34]](https://github.com/restic/restic/pull/310) | Да | Да | Нет [[35]](https://github.com/restic/restic/issues/60) | BSD | OpenBSD, Windows, macOS | Да | Supports storage on various cloud services natively and through [rclone](https://www.archlinux.org/packages/?name=rclone). |
| [ZBackup](http://zbackup.org/) | [zbackup](https://aur.archlinux.org/packages/zbackup/) | C++ | LZMA, LZO | AES | Да | Да | ? | планируется [[36]](https://github.com/zbackup/zbackup#improvements) | Нет | Kinda through tar | Да | Нет | GPLv2 | Да | Repository consists of immutable files. |

#### Инкременты на основе файлов

Когда файл изменяется, эти приложения сохраняют новую его версию полностью в следующем снимке. В отличие от [инкрементов на основе фрагментов](#Инкременты_на_основе_фрагментов_(chunks)), они менее экономно расходую место, особенно когда есть большие файлы с малыми изменениями; с другой стороны, зачастую такие бэкапы могут быть открыты без использования создавшего их приложения.

**Легенда:**

*   **Жёсткие ссылки**: хранение неизменённых файлов в виде жёстких ссылок на предыдущие версии.

| Название | Пакет | Реализация | Сжатое хранилище | Зашифрованное хранилище | Delta transfer | Зашифрованная передача | Метаданные ФС | Лёгкий доступ | Возобновляемая | Переименования | Жёсткие ссылки | CLI | Другие интерфейсы | Лицензия | Другие платформы | Поддержка | Особенности |
| [Back In Time](/index.php/Back_In_Time "Back In Time") | [backintime](https://aur.archlinux.org/packages/backintime/) | Python, rsync, diff | Нет | Нет | rsync | rsync | rsync | Да | Нет | Нет | Да [[37]](http://backintime.le-web.org/documentation/) | Да | Qt | GPLv2 | Да |
| [DAR](http://dar.linux.free.fr/) (Disk ARchive) | [dar](https://aur.archlinux.org/packages/dar/) | C++ | special archive format | Да | Да | Да | ? | ? | ? | ? | Нет [[38]](http://dar.linux.free.fr/doc/Features.html) | Да | [dargui](https://aur.archlinux.org/packages/dargui/) | GPL | FreeBSD, NetBSD, Windows, macOS | Да |
| [Link-Backup](http://www.scottlu.com/Content/Link-Backup.html) | [link-backup](https://aur.archlinux.org/packages/link-backup/) | Python 2 | Нет | Нет | ? | SSH | ? | ? | Да | Да | Нет [[39]](http://www.scottlu.com/Content/Link-Backup.html) | Да | Нет | MIT | Нет | It copies itself to the server. |
| [rdup](https://github.com/miekg/rdup) | [rdup](https://aur.archlinux.org/packages/rdup/) | C | tar.gz | gpg, blowfish и другие | ? | ? | ? | Да | ? | Нет | Да | Да | Нет | GPLv3 | Нет | Set of command-line tools. |
| [rsnapshot](/index.php/Rsnapshot "Rsnapshot") | [rsnapshot](https://www.archlinux.org/packages/?name=rsnapshot) | rsync | Нет | Нет | Да | Да | ? | ? | ? | ? | Да [[40]](http://rsnapshot.org/rsnapshot/docs/docbook/rest.html) | Да | Нет | GPLv2 | Win32 | Нет [[41]](https://github.com/rsnapshot/rsnapshot/issues/191) |
| [sbackup](https://launchpad.net/sbackup) | [sbackup](https://aur.archlinux.org/packages/sbackup/) | Python | gzip, bzip2 | Нет | ? | SSH | ? | Нет | Нет | Нет | Нет | Нет | GTK | GPLv3 | Нет |
| [TimeShift](https://github.com/teejee2008/timeshift) | [timeshift](https://aur.archlinux.org/packages/timeshift/) | rsync | Нет | Нет | rsync | rsync | ? | ? | ? | ? | Да | Нет | GTK | GPLv3 | Designed for full-system backups to dedicated devices. | Да |

### Сетевая структура

Эти приложения были разработаны для централизованного архивирования данных с нескольких машин, соединённых по сети, с использованием клиент-серверной модели. В целом они более сложны в развёртывании в сравнении с [одним устройством](#Одно_устройство).

**Легенда:**

*   **Направление**: Pull: сервер пишет в клиент. Push: клиент начинает сессию архивирования.
*   **Тиип инкремента**: стратегия уменьшения дублирования данных для экономии места (помимо сжатия).
    *   **файлы**: при изменении файла в новом снимке сохраняется новая версия целиком.
        *   **жёсткие ссылки**: хранение неизменённых файлов в виде жёстких ссылок на предыдущие версии.
    *   **чанки**: при изменении файла в снимке хранятся только изменённые части.

| Название | Пакет | Реализация | Направление | Сжатое хранилище | Зашифрованное хранилище | Delta transfer | Зашифрованная передача | Метаданные ФС | Лёгкий доступ | Возобновляемая | Переименования | Тиип инкремента | CLI | Другие интерфейсы | Лицензия | Другие платформы | Поддержка | Особенности |
| [BackupPC](/index.php/BackupPC "BackupPC") | [backuppc](https://www.archlinux.org/packages/?name=backuppc) | Perl | Pull | Да | Нет | Да | Да | Да | Нет | Да | ? | файлы, жёсткие ссылки [[42]](http://backuppc.sourceforge.net/faq/BackupPC.html#Backup-basics) | Нет | Web | GPLv2 | Any (no client needed) | Да | Identical files across backups of the same or different clients are stored only once. |
| [Bacula](http://www.bacula.org) | [bacula*](https://aur.archlinux.org/packages/?K=bacula) in [AUR](/index.php/AUR "AUR") | C++ | Pull | Да | Да | ? | Да | ? | ? | Да | ? | файлы [[43]](http://burp.grke.org/why.html) | Да | GUI, Web | AGPLv3 | Windows, macOS | Да |
| [burp](http://burp.grke.org) | [burp-backup](https://aur.archlinux.org/packages/burp-backup/) | librsync | Push | Да | Да | Да | Да | Да | ? | Да | ? | чанки [[44]](http://burp.grke.org/why.html) | Да | [burp-ui](https://git.ziirish.me/ziirish/burp-ui) | AGPLv3 | Windows, macOS | Да |
| [SafeKeep](http://safekeep.sourceforge.net/) | [safekeep](https://aur.archlinux.org/packages/safekeep/) | rdiff-backup | Pull | Нет | Нет | ? | Да | ? | ? | ? | ? | чанки [[45]](http://safekeep.sourceforge.net/safekeep.html) | Да | Да | GPL | Нет | Integrates with [LVM](/index.php/LVM "LVM") and databases to create consistent backups. Bandwidth throttling. |
| [Snebu](http://www.snebu.com) | [snebu](https://aur.archlinux.org/packages/snebu/) | C | Push или Pull | Да | Нет | ? | Да | ? | ? | ? | ? | файлы [[46]](http://www.snebu.com/#_concepts) | Да | Нет | GPLv3 | ? | Supports arbitrary retention schedules. |
| [Synbak](http://www.initzero.it/portal/soluzioni/software-open-source/synbak-universal-backup-system_2623.html) | [synbak](https://www.archlinux.org/packages/?name=synbak) | Multitool wrapper | ? | Да | Нет | Да | Да | Да | ? | ? | ? | ? | Нет | Web | GPLv3 | Да | Unifies several backup methods. |
| [UrBackup](https://www.urbackup.org) | [urbackup*](https://aur.archlinux.org/packages/?K=urbackup) in [AUR](/index.php/AUR "AUR") | C++ | Pull | Нет | Нет | Да | Internet transfers only | Да | Да | Да | Да | файлы, жёсткие и символьные ссылки[[47]](http://blog.urbackup.org/156/symbolically-linking-directories-during-incremental-file-backups)/chunk-based CoW-Snapshots[[48]](http://blog.urbackup.org/83/file-backup-storage-with-btrfs-snapshots) | Да (client) | GUI, Web | AGPLv3+ | Windows, macOS | Да | Identical files across backups of the same or different clients are stored only once. Integrates with LVM, dattobd and btrfs for file system snapshots. |

## Системы управления версиями

Хотя [системы управления версиями](https://en.wikipedia.org/wiki/version_control_system "wikipedia:version control system") чаще всего используются для исходного кода, они могут хранить любые файлы.

Смотрите [List of applications/Utilities#Version control systems](/index.php/List_of_applications/Utilities#Version_control_systems "List of applications/Utilities") и [dotfiles](/index.php/Dotfiles "Dotfiles").

## Смотрите также

*   [Краткий обзор open source средств резервного копирования](https://habr.com/ru/company/southbridge/blog/220555/)
*   [Backing up Linux and other Unix(-like) systems](http://www.halfgaar.net/backing-up-unix)
*   [Exhaustive list of backup solutions for Linux](https://github.com/restic/others)
*   [Performance comparison of five remote incremental backup tools: Rsync, Rdiff-backup, Duplicity, Areca and Link-Backup](http://www.si-journal.org/index.php/JSI/article/view/205)
*   [Mirroring an Entire Site using Rsync over SSH](http://www.askapache.com/security/mirror-using-rsync-ssh.html)
*   [Performance comparison of five remote incremental backup tools: Rsync, Rdiff-backup, Duplicity, Areca and Link-Backup](http://www.si-journal.org/index.php/JSI/article/view/205)
*   [rsync-snapshot.sh](http://blog.pointsoftware.ch/index.php/howto-local-and-remote-snapshot-backup-using-rsync-with-hard-links/) — Local and remote snapshot backup using rsync with hard links