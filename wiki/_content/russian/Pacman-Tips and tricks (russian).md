**Состояние перевода:** На этой странице представлен перевод статьи [pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks"). Дата последней синхронизации: 19 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Pacman/Tips_and_tricks&diff=0&oldid=426435).

Смотрите главную статью [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)").

Для общих методов улучшения гибкости предоставляемых советов или самого Pacman смотрите [Базовые утилиты](/index.php/%D0%91%D0%B0%D0%B7%D0%BE%D0%B2%D1%8B%D0%B5_%D1%83%D1%82%D0%B8%D0%BB%D0%B8%D1%82%D1%8B "Базовые утилиты") и [Bash](/index.php/Bash_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bash (Русский)").

## Contents

*   [1 Красота и комфорт](#.D0.9A.D1.80.D0.B0.D1.81.D0.BE.D1.82.D0.B0_.D0.B8_.D0.BA.D0.BE.D0.BC.D1.84.D0.BE.D1.80.D1.82)
    *   [1.1 Операции и синтаксис Bash](#.D0.9E.D0.BF.D0.B5.D1.80.D0.B0.D1.86.D0.B8.D0.B8_.D0.B8_.D1.81.D0.B8.D0.BD.D1.82.D0.B0.D0.BA.D1.81.D0.B8.D1.81_Bash)
    *   [1.2 Графические оболочки](#.D0.93.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8)
    *   [1.3 Утилиты](#.D0.A3.D1.82.D0.B8.D0.BB.D0.B8.D1.82.D1.8B)
*   [2 Обслуживание](#.D0.9E.D0.B1.D1.81.D0.BB.D1.83.D0.B6.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [2.1 Список пакетов](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
        *   [2.1.1 С размером](#.D0.A1_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80.D0.BE.D0.BC)
        *   [2.1.2 Последние установленные пакеты](#.D0.9F.D0.BE.D1.81.D0.BB.D0.B5.D0.B4.D0.BD.D0.B8.D0.B5_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B)
        *   [2.1.3 Все пакеты, которые не зависят от других](#.D0.92.D1.81.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B.2C_.D0.BA.D0.BE.D1.82.D0.BE.D1.80.D1.8B.D0.B5_.D0.BD.D0.B5_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D1.8F.D1.82_.D0.BE.D1.82_.D0.B4.D1.80.D1.83.D0.B3.D0.B8.D1.85)
        *   [2.1.4 Поиск установленных пакетов, не принадлежащих определенной группе или репозиторию](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2.2C_.D0.BD.D0.B5_.D0.BF.D1.80.D0.B8.D0.BD.D0.B0.D0.B4.D0.BB.D0.B5.D0.B6.D0.B0.D1.89.D0.B8.D1.85_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D0.BE.D0.B9_.D0.B3.D1.80.D1.83.D0.BF.D0.BF.D0.B5_.D0.B8.D0.BB.D0.B8_.D1.80.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.B8.D1.8E)
    *   [2.2 Просмотр файлов, принадлежащих пакету с определенным размером](#.D0.9F.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.2C_.D0.BF.D1.80.D0.B8.D0.BD.D0.B0.D0.B4.D0.BB.D0.B5.D0.B6.D0.B0.D1.89.D0.B8.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.83_.D1.81_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D0.BC_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80.D0.BE.D0.BC)
    *   [2.3 Поиск файлов, не принадлежащих ни одному пакету](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.2C_.D0.BD.D0.B5_.D0.BF.D1.80.D0.B8.D0.BD.D0.B0.D0.B4.D0.BB.D0.B5.D0.B6.D0.B0.D1.89.D0.B8.D1.85_.D0.BD.D0.B8_.D0.BE.D0.B4.D0.BD.D0.BE.D0.BC.D1.83_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.83)
    *   [2.4 Удаление неиспользуемых пакетов](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D0.BC.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
        *   [2.4.1 Сироты](#.D0.A1.D0.B8.D1.80.D0.BE.D1.82.D1.8B)
        *   [2.4.2 Явно установленные](#.D0.AF.D0.B2.D0.BD.D0.BE_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5)
    *   [2.5 Удаление всех пакетов, кроме группы base](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2.D1.81.D0.B5.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2.2C_.D0.BA.D1.80.D0.BE.D0.BC.D0.B5_.D0.B3.D1.80.D1.83.D0.BF.D0.BF.D1.8B_base)
    *   [2.6 Получения списка зависимостей нескольких пакетов](#.D0.9F.D0.BE.D0.BB.D1.83.D1.87.D0.B5.D0.BD.D0.B8.D1.8F_.D1.81.D0.BF.D0.B8.D1.81.D0.BA.D0.B0_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B8.D0.BC.D0.BE.D1.81.D1.82.D0.B5.D0.B9_.D0.BD.D0.B5.D1.81.D0.BA.D0.BE.D0.BB.D1.8C.D0.BA.D0.B8.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
    *   [2.7 Построение списка изменённых файлов из резервного копирования](#.D0.9F.D0.BE.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.BF.D0.B8.D1.81.D0.BA.D0.B0_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D1.91.D0.BD.D0.BD.D1.8B.D1.85_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_.D0.B8.D0.B7_.D1.80.D0.B5.D0.B7.D0.B5.D1.80.D0.B2.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BA.D0.BE.D0.BF.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [2.8 Создание резервной копии базы данных Pacman](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.80.D0.B5.D0.B7.D0.B5.D1.80.D0.B2.D0.BD.D0.BE.D0.B9_.D0.BA.D0.BE.D0.BF.D0.B8.D0.B8_.D0.B1.D0.B0.D0.B7.D1.8B_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_Pacman)
    *   [2.9 Лёгкий способ проверки списка изменений](#.D0.9B.D1.91.D0.B3.D0.BA.D0.B8.D0.B9_.D1.81.D0.BF.D0.BE.D1.81.D0.BE.D0.B1_.D0.BF.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B8_.D1.81.D0.BF.D0.B8.D1.81.D0.BA.D0.B0_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B9)
*   [3 Installation and recovery](#Installation_and_recovery)
    *   [3.1 Installing packages from a CD/DVD or USB stick](#Installing_packages_from_a_CD.2FDVD_or_USB_stick)
    *   [3.2 Custom local repository](#Custom_local_repository)
    *   [3.3 Network shared pacman cache](#Network_shared_pacman_cache)
        *   [3.3.1 Read-only cache](#Read-only_cache)
        *   [3.3.2 Read-write cache](#Read-write_cache)
        *   [3.3.3 Dynamic reverse proxy cache using nginx](#Dynamic_reverse_proxy_cache_using_nginx)
        *   [3.3.4 Synchronize pacman package cache using BitTorrent Sync](#Synchronize_pacman_package_cache_using_BitTorrent_Sync)
        *   [3.3.5 Preventing unwanted cache purges](#Preventing_unwanted_cache_purges)
    *   [3.4 Recreate a package from the file system](#Recreate_a_package_from_the_file_system)
    *   [3.5 Резервное копирование и извлечение списка установленных пакетов](#.D0.A0.D0.B5.D0.B7.D0.B5.D1.80.D0.B2.D0.BD.D0.BE.D0.B5_.D0.BA.D0.BE.D0.BF.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B8_.D0.B8.D0.B7.D0.B2.D0.BB.D0.B5.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.BF.D0.B8.D1.81.D0.BA.D0.B0_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
    *   [3.6 Listing all changed files from packages](#Listing_all_changed_files_from_packages)
    *   [3.7 Переустановка всех пакетов](#.D0.9F.D0.B5.D1.80.D0.B5.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B2.D1.81.D0.B5.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
    *   [3.8 Restore pacman's local database](#Restore_pacman.27s_local_database)
        *   [3.8.1 Generating the package recovery list](#Generating_the_package_recovery_list)
        *   [3.8.2 Performing the recovery](#Performing_the_recovery)
    *   [3.9 Recovering a USB key from existing install](#Recovering_a_USB_key_from_existing_install)
    *   [3.10 Extracting contents of a .pkg file](#Extracting_contents_of_a_.pkg_file)
    *   [3.11 Viewing a single file inside a .pkg file](#Viewing_a_single_file_inside_a_.pkg_file)
    *   [3.12 Find applications that use libraries from older packages](#Find_applications_that_use_libraries_from_older_packages)
*   [4 Performance](#Performance)
    *   [4.1 Database access speeds](#Database_access_speeds)
    *   [4.2 Увеличение скорости загрузки](#.D0.A3.D0.B2.D0.B5.D0.BB.D0.B8.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.BA.D0.BE.D1.80.D0.BE.D1.81.D1.82.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8)
        *   [4.2.1 Powerpill](#Powerpill)
        *   [4.2.2 wget](#wget)
        *   [4.2.3 aria2](#aria2)
        *   [4.2.4 Другие приложения](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)

## Красота и комфорт

### Операции и синтаксис Bash

В дополнение к стандартному набору функций pacman, есть способ их расширить при помощи команд/синтаксиса [Bash](/index.php/Bash_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bash (Русский)").

Чтобы установить несколько пакетов, разделяющих аналогичные модели в своих названиях -- не всю группу, ни все совпадающие пакеты; например.[plasma](https://www.archlinux.org/groups/x86_64/plasma/):

```
# pacman -S plasma-{desktop,mediacenter,nm}

```

Конечно, это не ограничено и может быть расширено до множества необходимых уровней:

```
# pacman -S plasma-{workspace{,-wallpapers},pa}

```

Иногда, `-s` встроенный в ERE может вызвать множество нежелательных результатов, поэтому он должен быть ограничен, чтобы соответствовать только именю пакета; не описанию, ни любой другой области:

```
# pacman -Ss '^vim-'

```

pacman содержит операнд `-q` чтобы скрыть столбец версии, поэтому можно запросить и переустановить пакеты "compiz" как часть их имени:

```
# pacman -S $(pacman -Qq | grep compiz)

```

### Графические оболочки

*   **Discover** — Утилита управления пакетами для KDE, используя PackageKit.

	[https://projects.kde.org/projects/kde/workspace/discover](https://projects.kde.org/projects/kde/workspace/discover) || [discover](https://www.archlinux.org/packages/?name=discover)

*   **GNOME packagekit** — Утилита для управления пакетами, на основе GTK

	[http://www.freedesktop.org/software/PackageKit/](http://www.freedesktop.org/software/PackageKit/) || [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit)

*   **GNOME Software** — Gnome Software App. (Curated selection for GNOME)

	[https://wiki.gnome.org/Apps/Software](https://wiki.gnome.org/Apps/Software) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

*   **pcurses** — Управление пакетами при помощи текстового интерфейса (curses)

	[https://github.com/schuay/pcurses](https://github.com/schuay/pcurses) || [pcurses](https://www.archlinux.org/packages/?name=pcurses)

*   **tkPacman** — Графический интерфейс для pacman. Зависит от Tcl/Tk и X11, но не как не от GTK+, и QT. Взаимодействует только с базой данных пакетов через интерфейс командной строки 'pacman'. Таким образом, установка и удаление пакетов с tkPacman или с pacman

приведёт к одинаковым результатам.

	[http://sourceforge.net/projects/tkpacman](http://sourceforge.net/projects/tkpacman) || [tkpacman](https://aur.archlinux.org/packages/tkpacman/)

### Утилиты

*   **Lostfiles** — Сценарий для обнаружения осиротевших файлов.

	[https://github.com/graysky2/lostfiles](https://github.com/graysky2/lostfiles) || [lostfiles](https://aur.archlinux.org/packages/lostfiles/)

*   **[Pacmatic](/index.php/Pacmatic "Pacmatic")** — Оболочка для Pacman, проверяющая новости Arch перед обновлением, во избежании частичных обновлений, и предупреждающая об изменении файлов настроек.

	[http://kmkeen.com/pacmatic](http://kmkeen.com/pacmatic) || [pacmatic](https://www.archlinux.org/packages/?name=pacmatic)

*   **[pkgfile](/index.php/Pkgfile "Pkgfile")** — Утилита, которая находит какому пакету принадлежит файл.

	[http://github.com/falconindy/pkgfile](http://github.com/falconindy/pkgfile) || [pkgfile](https://www.archlinux.org/packages/?name=pkgfile)

*   **[pkgtools](/index.php/Pkgtools "Pkgtools")** — Коллекция скриптов для пакетов Arch Linux.

	[https://github.com/Daenyth/pkgtools](https://github.com/Daenyth/pkgtools) || [pkgtools](https://aur.archlinux.org/packages/pkgtools/)

*   **srcpac** — Простая утилита, которая позволяет автоматизировать пересоздание пакетов из исходного кода.

	[https://projects.archlinux.org/srcpac.git](https://projects.archlinux.org/srcpac.git) || [srcpac](https://www.archlinux.org/packages/?name=srcpac)

*   **[snap-pac](/index.php/Snapper#snap-pac_pacman_hooks "Snapper")** — Заставить pacman автоматически использовать snapper для создания снимков до/после, как в openSUSE'овском YaST.

	[https://github.com/wesbarnett/snap-pac](https://github.com/wesbarnett/snap-pac) || [snap-pac](https://aur.archlinux.org/packages/snap-pac/)

## Обслуживание

Смотрите также [Обслуживание системы](/index.php/%D0%9E%D0%B1%D1%81%D0%BB%D1%83%D0%B6%D0%B8%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B "Обслуживание системы").

### Список пакетов

Вы можете получить список установленных пакетов с их версией, что полезно при составлении отчетов об ошибках или обсуждении установленных пакетов.

*   Список всех явно установленных пакетов: `pacman -Qe` .
*   Список всех внешних пакетов (обычно загруженных и установленных вручную): `pacman -Qm` .
*   Список всех родных пакетов (установленных из синхронизированной(ых) баз(ы)): `pacman -Qn` .
*   Список пакетов по регулярному выражению (regex): `pacman -Qs *regex*`.
*   Список пакетов по регулярному выражению с пользовательским форматом вывода: `expac -s "%-30n %v" *regex*` (требуется [expac](https://www.archlinux.org/packages/?name=expac)).

#### С размером

Чтобы получить список установленных пакетов, отсортированный по размеру, который может быть полезен, когда необходимо освободить пространство на жестком диске:

*   Установите [expac](https://www.archlinux.org/packages/?name=expac) и выполните `expac -H M '%m\t%n' | sort -h`.
*   Запустите [pacgraph](https://www.archlinux.org/packages/?name=pacgraph) с опцией `-c`.
*   Запустите [apacman](https://aur.archlinux.org/packages/apacman/) с опцией `-L`.

Чтобы перечислить размер нескольких загружаемых пакетов (оставьте `*packages*` пустым, чтобы перечислить все пакеты):

```
$ expac -S -H M '%k\t%n' *packages*

```

Чтобы получить список явно установленных пакетов не из [base](https://www.archlinux.org/groups/x86_64/base/) и не из [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) с размерами и описанием:

```
$ expac -H M "%011m\t%-20n\t%10d" $( comm -23 <(pacman -Qqen|sort) <(pacman -Qqg base base-devel|sort) ) | sort -n

```

#### Последние установленные пакеты

Установите [expac](https://www.archlinux.org/packages/?name=expac) и выполните `expac --timefmt='%Y-%m-%d %T' '%l\t%n' | sort | tail -20` или `expac --timefmt=%s '%l\t%n' | sort -n | tail -20`

#### Все пакеты, которые не зависят от других

Если вы хотите создать список всех установленных пакетов, которые больше не от кого не зависят, вы можете использовать следующий скрипт. Это очень полезно, если вы установили много пакетов, которые не можете вспомнить, и пытаетесь освободить место на жестком диске. Вы можете просмотреть вывод, чтобы найти пакеты которые вам больше не нужны.

**Примечание:** Этот скрипт покажет все пакеты, которые ни от чего не зависят, в том числе от тех, которые явно установлены. Чтобы получить список пакетов, не установленных в качестве зависимостей, но больше не требующихся какому-либо установленному пакету, смотрите [#Сироты](#.D0.A1.D0.B8.D1.80.D0.BE.D1.82.D1.8B).

```
ignoregrp="base base-devel"
ignorepkg=""

comm -23 <(pacman -Qqt | sort) <(echo $ignorepkg | tr ' ' '
' | cat <(pacman -Sqg $ignoregrp) - | sort -u)

```

Для получения списка с описаниями для пакетов:

```
expac -HM "%-20n\t%10d" $( comm -23 <(pacman -Qqt|sort) <(pacman -Qqg base base-devel|sort) )

```

#### Поиск установленных пакетов, не принадлежащих определенной группе или репозиторию

Следующая команда выведет список всех установленных пакетов, которые не принадлежат [base](https://www.archlinux.org/groups/x86_64/base/) или [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), и как таковые, вероятно, были установлены пользователем вручную:

```
$ comm -23 <(pacman -Qeq | sort) <(pacman -Qgq base base-devel | sort)

```

Список всех установленных пакетов, установленных не из указанного репозитория (`*repo_name*` в примере):

```
$ comm -23 <(pacman -Qtq | sort) <(pacman -Slq *repo_name* | sort)

```

Список всех установленных пакетов, которые находятся в `*repo_name*` репозитории:

```
$ comm -12 <(pacman -Qtq | sort) <(pacman -Slq *repo_name* | sort)

```

### Просмотр файлов, принадлежащих пакету с определенным размером

Это может пригодиться, если вы обнаружили что конкретный пакет использует огромное количество места, и вы хотите выяснить, какие файлы занимают больше всего.

```
$ pacman -Qlq *package* | grep -v '/$' | xargs du -h | sort -h

```

### Поиск файлов, не принадлежащих ни одному пакету

Если в вашей системе присутствуют "беспризорные" файлы, не принадлежащие ни одному пакету (например, в случае установки программного обеспечения в обход пакетного менеджера), вам может потребоваться найти такие файлы для очистки системы. В таком случае необходимо выполнить следующую последовательность действий:

1.  Создайте отсортированный список файлов, чью принадлежность конкретному пакету вы хотите проверить: `$ find /etc /opt /usr | sort > all_files.txt` 
2.  Создайте отсортированный список файлов, отслеживаемых пакетным менеджером (с удалением замыкающих слэшей из названий директорий): `$ pacman -Qlq | sed 's|/$||' | sort > owned_files.txt` 
3.  Найдите строки в первом списке, отсутствующие во втором: `$ comm -23 all_files.txt owned_files.txt` 

На практике применение этого приёмы осложняется тем, что многие важные файлы не принадлежат какому-либо пакету (к примеру, файлы, сгенерированные в процессе выполнения каких-либо приложений, пользовательские конфигурационные файлы, и т. д.) и будут включены в список "беспризорных", поэтому не стоит слепо полагаться исключительно на автоматику и пренебрегать ручной очисткой системы.

Скрипт [lostfiles](https://aur.archlinux.org/packages/lostfiles/) совершает схожие действия, но дополнительно сверяется с встроенным обширным перечнем файлов, необходимых системе, но не принадлежащих ни одному пакету.

### Удаление неиспользуемых пакетов

#### Сироты

Для *рекурсивного* удаления пакетов-сирот, от которых не зависят другие пакеты, и их конфигурационных файлов:

```
# pacman -Rns $(pacman -Qtdq)

```

Если сироты не найдены, Pacman завершает работу с ошибкой `error: no targets specified`. Это работает так же, как если бы никакие аргумены не были переданы в `pacman -Rns`.

**Примечание:** С версии Pacman 4.2.0 в список выводятся только настоящие сироты. Для добавления в список также пакетов, от которых опционально зависят другие пакеты, передайте флаг `-t`/`--unrequired` дважды:
```
$ pacman -Qdttq

```
Используйте эту команду с осторожностью, поскольку в результате её выполнения могут быть удалены пакеты, не являющиеся на самом деле сиротами.

#### Явно установленные

Поскольку более легковесную систему проще поддерживать, зачастую бывает полезно просмотреть список установленных пакетов и *вручную* удалить неиспользуемые. Для вывода списка явно установленных пакетов, доступных через официальные репозитории:

```
$ pacman -Qen

```

Для вывода списка явно установленных пакетов, не доступных через официальные репозитории:

```
$ pacman -Qem

```

### Удаление всех пакетов, кроме группы base

Если существует необходимость удалить все пакеты, кроме принадлежащих к группе *base*, это можно сделать командой в одну строку:

```
# pacman -R $(comm -23 <(pacman -Qq|sort) <((for i in $(pacman -Qqg base); do pactree -ul $i; done)|sort -u|cut -d ' ' -f 1))

```

Этак команда была изначально разработана в [this discussion](https://bbs.archlinux.org/viewtopic.php?id=130176) и позднее доработана для этой статьи.

Замечания:

1.  `comm` требует отсортированного ввода, иначе вы получите что-то вроде `comm: file 1 is not in sorted order`.
2.  `pactree` выводит название пакета исходя из того, что его предоставляет. Например:

 `$ pactree -lu logrotate` 
```
logrotate
popt
glibc
linux-api-headers
tzdata
dcron cron
bash
readline
ncurses
gzip
```

Строка `dcron cron` выглядит проблемной, так что необходимо включить `cut -d ' ' -f 1` для сохранения обычного названия пакета.

### Получения списка зависимостей нескольких пакетов

Во многих случаях вы можете использовать `pacman -Qi` для того, чтобы сократить время выполнения поискового запроса. Но вы не можете использовать эту команду в случае, если требуется выявить зависимости нескольких пакетов. Ненайденные пакеты легко отбрасываются (hence the `2>/dev/null`).

```
$ pacman -Si $@ 2>/dev/null | awk -F ": " -v filter="^Depends" \ '$0 ~ filter {gsub(/[>=<][^ ]*/,"",$2) ; gsub(/ +/,"
",$2) ; print $2}' | sort -u

```

Зависимости сортируются в алфавитном порядке, дубликаты удаляются из списка.

Также вы можете использовать `expac`: `expac -l '
' %E -S $@ | sort -u`.

### Построение списка изменённых файлов из резервного копирования

Если вы хотите сделать резервное копирование ваших системных конфигурационных файлов, вы можете копировать все файлы из `/etc/`, но, скорее всего, вас интересуют только те файлы, в которых были сделаны изменения. Список модифицированных [заархивированных файлов](/index.php/Pacnew_and_Pacsave_files#Package_backup_files "Pacnew and Pacsave files") может быть построен следующей командой:

```
# pacman -Qii | awk '/^MODIFIED/ {print $2}'

```

Запуск этой команды с root-привилегиями даёт гарантию того, что файлы, доступные для просмотра только от root-а (такие, как `/etc/sudoers`), будут включены в список.

**Совет:** Для построения списка всех изменённых файлов из базы данных Pacman (не только из резервного копирования) смотрите [#Listing all changed files from packages](#Listing_all_changed_files_from_packages).

### Создание резервной копии базы данных Pacman

Следующая команда может быть использована для резервного копирования локальной базы данных Pacman:

```
$ tar -cjf pacman_database.tar.bz2 /var/lib/pacman/local

```

Храните заархивированную базу данных на одном или нескольких внешних хранилищах, таких, как USB-накопитель, внешний жёсткий диск или диск CD-R.

База данных может быть восстановлена путём перемещения `pacman_database.tar.bz2` в `/` и последующего выполнения команды:

```
# tar -xjvf pacman_database.tar.bz2

```

**Примечание:** Если файл с базой данных Pacman повреждён и нет других доступных резервных копий, есть надежда исправить ситуацию путём пересоздания базы данных. Подробнее смотрите тут: [Pacman tips#Restore pacman's local database](/index.php/Pacman_tips#Restore_pacman.27s_local_database "Pacman tips").

**Совет:** Пакет [pakbak-git](https://aur.archlinux.org/packages/pakbak-git/) предоставляет скрипт и сервис [systemd](/index.php/Systemd "Systemd") для автоматизации этой задачи. Конфигурация доступна в `/etc/pakbak.conf`.

### Лёгкий способ проверки списка изменений

Когда мейнтейнеры обновляют пакеты, правки часто комментируются в удобной форме. Пользователи могут легко просмотреть их из командной строки с помощью [paclog](https://aur.archlinux.org/packages/paclog/). Эта утилита выводит список последних комментариев мейнтейнеров к правкам для пакетов из официальных репозиториев или AUR, используя `paclog package`.

## Installation and recovery

Alternative ways of getting and restoring packages.

### Installing packages from a CD/DVD or USB stick

To download packages, or groups of packages:

```
# cd ~/Packages
# pacman -Syw base base-devel grub-bios xorg gimp --cachedir .
# repo-add ./custom.db.tar.gz ./*

```

Then you can burn the "Packages" folder to a CD/DVD or transfer it to a USB stick, external HDD, etc.

To install:

**1.** Mount the media:

```
# mkdir /mnt/repo
# mount /dev/sr0 /mnt/repo    #For a CD/DVD.
# mount /dev/sdxY /mnt/repo   #For a USB stick.

```

**2.** Edit `pacman.conf` and add this repository *before* the other ones (e.g. extra, core, etc.). This is important. Do not just uncomment the one on the bottom. This way it ensures that the files from the CD/DVD/USB take precedence over those in the standard repositories:

 `/etc/pacman.conf` 
```
[custom]
SigLevel = PackageRequired
Server = file:///mnt/repo/Packages
```

**3.** Finally, synchronize the pacman database to be able to use the new repository:

```
# pacman -Syu

```

### Custom local repository

Use the *repo-add* script included with Pacman to generate a database for a personal repository. Use `repo-add --help` for more details on its usage. Simply store all of the built packages to be included in the repository in one directory, and execute the following command (where *repo* is the name of the custom repository):

```
$ repo-add /path/to/repo.db.tar.gz /path/to/*.pkg.tar.xz

```

**Примечание:** A package database is a tar file, optionally compressed. Valid extensions are “.db” or “.files” followed by an archive extension of “.tar”, “.tar.gz”, “.tar.bz2”, “.tar.xz”, or “.tar.Z”. The file does not need to exist, but all parent directories must exist. Furthermore when using `repo-add` keep in mind that the database and the packages do not need to be in the same directory. But when using pacman with that database, they should be together.

To add a new package to the database, or to replace the old version of an existing package in the database, run:

```
$ repo-add /path/to/repo.db.tar.gz /path/to/packagetoadd-1.0-1-i686.pkg.tar.xz

```

*repo-remove* is used in the exact same manner as *repo-add*, except that the packages listed on the command line are removed from the repository database.

Once the local repository database has been created, add the repository to `pacman.conf` for each system that is to use the repository. An example of a custom repository is in `pacman.conf`. The repository's name is the database filename with the file extension omitted. In the case of the example above the repository's name would simply be *repo*. Reference the repository's location using a `file://` url, or via FTP using [ftp://localhost/path/to/directory](ftp://localhost/path/to/directory).

If willing, add the custom repository to the [list of unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories"), so that the community can benefit from it.

### Network shared pacman cache

If you happen to run several Arch boxes on your LAN, you can share packages so that you can greatly decrease your download times. Keep in mind you should not share between different architectures (i.e. i686 and x86_64) or you'll run into problems.

#### Read-only cache

If you are looking for a quick and dirty solution, you can simply run a standalone webserver which other computers can use as a first mirror: `darkhttpd /var/cache/pacman/pkg`. Just add this server at the top of your mirror list. Be aware that you might get a lot of 404 errors, due to cache misses, depending on what you do, but pacman will try the next (real) mirrors when that happens.

#### Read-write cache

**Совет:** See [pacserve](/index.php/Pacserve "Pacserve") for an alternative (and probably simpler) solution than what follows.

In order to share packages between multiple computers, simply share `/var/cache/pacman/` using any network-based mount protocol. This section shows how to use shfs or sshfs to share a package cache plus the related library-directories between multiple computers on the same local network. Keep in mind that a network shared cache can be slow depending on the file-system choice, among other factors.

First, install any network-supporting filesystem; for example [sshfs](/index.php/Sshfs "Sshfs"), [shfs](/index.php/Shfs "Shfs"), ftpfs, [smbfs](/index.php/Smbfs "Smbfs") or [nfs](/index.php/Nfs "Nfs").

**Совет:** To use sshfs or shfs, consider reading [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys").

Then, to share the actual packages, mount `/var/cache/pacman/pkg` from the server to `/var/cache/pacman/pkg` on every client machine.

#### Dynamic reverse proxy cache using nginx

[nginx](/index.php/Nginx "Nginx") can be used to proxy requests to official upstream mirrors and cache the results to local disk. All subsequent requests for that file will be served directly from the local cache, minimizing the amount of internet traffic needed to update a large number of servers with minimal effort.

**Важно:** This method has a limitation. You must use mirrors that use the same relative path to package files and you must configure your cache to use that same path. In this example, we are using mirrors that use the relative path `/archlinux/$repo/os/$arch` and our cache's `Server` setting in `mirrorlist` is configured similarly.

In this example, we will run the cache server on `http://cache.domain.local:8080/` and storing the packages in `/srv/http/pacman-cache/`.

Create the directory for the cache and adjust the permissions so nginx can write files to it:

```
 # mkdir /srv/http/pacman-cache
 # chown http:http /srv/http/pacman-cache

```

Next, configure nginx as our dynamic cache (read the comments for an explanation of the commands):

 `/etc/nginx/nginx.conf` 
```
http
{
    ...

    # nginx may need to resolve domain names at run time
    resolver 8.8.8.8 8.8.4.4;

    # Pacman Cache
    server
    {
        listen      8080;
        server_name cache.domain.local;
        root        /srv/http/pacman-cache;
        autoindex   on;

        # Requests for package db and signature files should redirect upstream without caching
        location ~ \.(db|sig)$ {
            proxy_pass http://mirrors$request_uri;
        }

        # Requests for actual packages should be served directly from cache if available.
        #   If not available, retrieve and save the package from an upstream mirror.
        location ~ \.tar\.xz$ {
            try_files $uri @pkg_mirror;
        }

        # Retrieve package from upstream mirrors and cache for future requests
        location @pkg_mirror {
            proxy_store    on;
            proxy_redirect off;
            proxy_store_access  user:rw group:rw all:r;
            proxy_next_upstream error timeout http_404;
            proxy_pass          http://mirrors$request_uri;
        }
    }

    # Upstream Arch Linux Mirrors
    # - Configure as many backend mirrors as you want in the blocks below
    # - Servers are used in a round-robin fashion by nginx
    # - Add "backup" if you want to only use the mirror upon failure of the other mirrors
    # - Separate "server" configurations are required for each upstream mirror so we can set the "Host" header appropriately
    upstream mirrors {
        server localhost:8001;
        server localhost:8002 backup;
        server localhost:8003 backup;
    }

    # Arch Mirror 1 Proxy Configuration
    server
    {
        listen      8001;
        server_name localhost;

        location / {
            proxy_pass       http://mirror.rit.edu$request_uri;
            proxy_set_header Host mirror.rit.edu;
        }
    }

    # Arch Mirror 2 Proxy Configuration
    server
    {
        listen      8002;
        server_name localhost;

        location / {
            proxy_pass       http://mirrors.acm.wpi.edu$request_uri;
            proxy_set_header Host mirrors.acm.wpi.edu;
        }
    }

    # Arch Mirror 3 Proxy Configuration
    server
    {
        listen      8003;
        server_name localhost;

        location / {
            proxy_pass       http://lug.mtu.edu$request_uri;
            proxy_set_header Host lug.mtu.edu;
        }
    }
}

```

Finally, update your other Arch Linux servers to use this new cache by adding the following line to the `mirrorlist` file:

 `/etc/pacman.d/mirrorlist` 
```
Server = http://cache.domain.local:8080/archlinux/$repo/os/$arch
...

```

**Примечание:** You will need to create a method to clear old packages, as this directory will continue to grow over time. `paccache` (which is included with `pacman`) can be used to automate this using retention criteria of your choosing. For example, `find /srv/http/pacman-cache/ -type d -exec paccache -v -r -k 2 -c {} \;` will keep the last 2 versions of packages in your cache directory.

#### Synchronize pacman package cache using BitTorrent Sync

[BitTorrent Sync](/index.php/BitTorrent_Sync "BitTorrent Sync") is a new way of synchronizing folder via network (it works in LAN and over the internet). It is peer-to-peer so you do not need to set up a server: follow the link for more information. How to share a pacman cache using BitTorrent Sync:

*   First install the [btsync](https://aur.archlinux.org/packages/btsync/) package from the AUR on the machines you want to sync
*   Follow the installation instructions of the AUR package or on the [BitTorrent Sync](/index.php/BitTorrent_Sync "BitTorrent Sync") wiki page
    *   set up BitTorrent Sync to work for the root account. This process requires read/write to the pacman package cache.
    *   make sure to set a good password on btsync's web UI
    *   start the systemd daemon for btsync.
    *   in the btsync Web GUI add a new synchronized folder on the first machine and generate a new Secret. Point the folder to `/var/cache/pacman/pkg`
    *   Add the folder on all the other machines using the same Secret to share the cached packages between all systems. Or, to set the first system as a master and the others as slaves, use the Read Only Secret. Be sure to point it to `/var/cache/pacman/pkg`

Now the machines should connect and start synchronizing their cache. Pacman works as expected even during synchronization. The process of syncing is entirely automatic.

#### Preventing unwanted cache purges

By default, `pacman -Sc` removes package tarballs from the cache that correspond to packages that are not installed on the machine the command was issued on. Because pacman cannot predict what packages are installed on all machines that share the cache, it will end up deleting files that should not be.

To clean up the cache so that only *outdated* tarballs are deleted, add this entry in the `[options]` section of `/etc/pacman.conf`:

```
CleanMethod = KeepCurrent

```

### Recreate a package from the file system

To recreate a package from the file system, use *bacman* (included with pacman). Files from the system are taken as they are, hence any modifications will be present in the assembled package. Distributing the recreated package is therefore discouraged; see [ABS](/index.php/ABS "ABS") and [Arch Rollback Machine](/index.php/Arch_Rollback_Machine "Arch Rollback Machine") for alternatives.

**Совет:** *bacman* honours the `PACKAGER`, `PKGDEST` and `PKGEXT` options from `makepkg.conf`. Custom options for the compression tools can be configured by exporting the relevant environment variable, for example `XZ_OPT="-T 0"` will enable parallel compression for *xz*.

An alternative tool would be [fakepkg](https://aur.archlinux.org/packages/fakepkg/). It supports parallelization and can handle multiple input packages in one command, which *bacman* both does not support.

### Резервное копирование и извлечение списка установленных пакетов

**Совет:** You may want to use [plist-gist](https://aur.archlinux.org/packages/plist-gist/) or [bacpac](https://bbs.archlinux.org/viewtopic.php?id=200067) to automatise the below tasks.

It is good practice to keep periodic backups of all pacman-installed packages. In the event of a system crash which is unrecoverable by other means, pacman can then easily reinstall the very same packages onto a new installation.

*   First, backup the current list of non-local packages: `$ pacman -Qqen > pkglist.txt`

*   Store the `pkglist.txt` on a USB key or other convenient medium or gist.github.com or Evernote, Dropbox, etc.

*   Copy the `pkglist.txt` file to the new installation, and navigate to the directory containing it.

*   Issue the following command to install from the backup list: `# pacman -S $(< pkglist.txt)`

In the case you have a list which was not generated like mentioned above, there may be foreign packages in it (i.e. packages not belonging to any repos you have configured, or packages from the AUR).

In such a case, you may still want to install all available packages from that list:

```
# pacman -S --needed $(comm -12 <(pacman -Slq|sort) <(sort badpkdlist) )

```

Explanation:

*   `pacman -Slq` lists all available softwares, but the list is sorted by repository first, hence the `sort` command.
*   Sorted files are required in order to make the `comm` command work.
*   The `-12` parameter display lines common to both entries.
*   The `--needed` switch is used to skip already installed packages.

Finally, you may want to remove all the packages on your system that are not mentioned in the list.

**Важно:** Use this command wisely, and always check the result prompted by pacman.

```
# pacman -Rsu $(comm -23 <(pacman -Qq|sort) <(sort pkglist))

```

### Listing all changed files from packages

If you are suspecting file corruption (e.g. by software / hardware failure), but don't know for sure whether / which files really got corrupted, you might want to compare with the hash sums in the packages. This can be done with the following script.

The script depends on the accuracy of pacman's database in `/var/lib/pacman/local/` and the used programs such as *bash*, *grep* and so on. For recovery of the database see [#Restore pacman's local database](#Restore_pacman.27s_local_database). The `mtree` files can also be [extracted as `.MTREE` from the respective package files](#Viewing_a_single_file_inside_a_.pkg_file).

**Примечание:**

*   This should **not** be used as is when suspecting malicious changes! In this case security precautions such as using a live medium and an independent source for the hash sums are advised.
*   This could take a long time, depending on the hardware and installed packages.

```
#!/bin/bash -e

# Select the hash algorithm. Currently available (see mtree files and mtree(5)):
# md5, sha256
algo="md5"

for package in /var/lib/pacman/local/*; do
    [ "$package" = "/var/lib/pacman/local/ALPM_DB_VERSION" ] && continue

    # get files and hash sums
    zgrep " ${algo}digest=" "$package/mtree" | grep -Ev '^\./\.[A-Z]+' | \
        sed 's/^\([^ ]*\).*'"${algo}"'digest=\([a-f0-9]*\).*/\1 \2/' | \
        while read -r file hash
    do
        # expand "
nn" (in mtree) / "\0nnn" (for echo) escapes of ASCII
        # characters (octal representation)
        for ascii in $(grep -Eo '\\[0-9]{1,3}' <<< "$file"); do
            file="$(sed "s/\\$ascii/$(echo -e "\0${ascii:1}")/" <<< "$file")"
        done

        # check file hash
        if [ "$("${algo}sum" /"$file" | awk '{ print $1; }')" != "$hash" ]; then
            echo "$(basename "$package")" /"$file"
        fi
    done
done

```

### Переустановка всех пакетов

Чтобы переустановить все родные пакеты, используйте:

```
# pacman -Qenq | pacman -S -

```

Внешние пакеты (AUR) должны быть установлены отдельно; вы можете перечислить их с помощью `pacman -Qemq`.

Pacman, по умолчанию, сохраняет аргументы установки.

### Restore pacman's local database

Signs that pacman needs a local database restoration:

*   `pacman -Q` gives absolutely no output, and `pacman -Syu` erroneously reports that the system is up to date.
*   When trying to install a package using `pacman -S package`, and it outputs a list of already satisfied dependencies.
*   When `testdb` (part of [pacman](https://www.archlinux.org/packages/?name=pacman)) reports database inconsistency.

Most likely, pacman's database of installed software, `/var/lib/pacman/local`, has been corrupted or deleted. While this is a serious problem, it can be restored by following the instructions below.

Firstly, make sure pacman's log file is present:

```
$ ls /var/log/pacman.log

```

If it does not exist, it is *not* possible to continue with this method. You may be able to use [Xyne's package detection script](https://bbs.archlinux.org/viewtopic.php?pid=670876) to recreate the database. If not, then the likely solution is to re-install the entire system.

#### Generating the package recovery list

**Важно:** If for some reason your [pacman](/index.php/Pacman "Pacman") cache or [makepkg](/index.php/Makepkg "Makepkg") package destination contain packages for other architectures, remove them before continuation.

Create the log filter script and make it executable:

 `pacrecover` 
```
#!/bin/bash -e

. /etc/makepkg.conf

PKGCACHE=$((grep -m 1 '^CacheDir' /etc/pacman.conf || echo 'CacheDir = /var/cache/pacman/pkg') | sed 's/CacheDir = //')

pkgdirs=("$@" "$PKGDEST" "$PKGCACHE")

while read -r -a parampart; do
  pkgname="${parampart[0]}-${parampart[1]}-*.pkg.tar.xz"
  for pkgdir in ${pkgdirs[@]}; do
    pkgpath="$pkgdir"/$pkgname
    [ -f $pkgpath ] && { echo $pkgpath; break; };
  done || echo ${parampart[0]} 1>&2
done

```

Run the script (optionally passing additional directories with packages as parameters):

```
$ paclog-pkglist /var/log/pacman.log | ./pacrecover >files.list 2>pkglist.orig

```

This way two files will be created: `files.list` with package files, still present on machine and `pkglist.orig`, packages from which should be downloaded. Later operation may result in mismatch between files of older versions of package, still present on machine, and files, found in new version. Such mismatches will have to be fixed manually.

Here is a way to automatically restrict second list to packages available in a repository:

```
$ { cat pkglist.orig; pacman -Slq; } | sort | uniq -d > pkglist

```

Check if some important *base* package are missing, and add them to the list:

```
$ comm -23 <(pacman -Sgq base) pkglist.orig >> pkglist

```

Proceed once the contents of both lists are satisfactory, since they will be used to restore pacman's installed package database; `/var/lib/pacman/local/`.

#### Performing the recovery

Define bash alias for recovery purposes:

```
# recovery-pacman() {
    pacman "$@"       \
    --log /dev/null   \
    --noscriptlet     \
    --dbonly          \
    --force           \
    --nodeps          \
    --needed          \
    #
}

```

`--log /dev/null` allows to avoid needless pollution of pacman log, `--needed` will save some time by skipping packages, already present in database, `--nodeps` will allow installation of cached packages, even if packages being installed depend on newer versions. Rest of options will allow **pacman** to operate without reading/writing filesystem.

Populate the sync database:

```
# pacman -Sy

```

Start database generation by installing locally available package files from `files.list`:

```
# recovery-pacman -U $(< files.list)

```

Install the rest from `pkglist`:

```
# recovery-pacman -S $(< pkglist)

```

Update the local database so that packages that are not required by any other package are marked as explicitly installed and the other as dependences. You will need be extra careful in the future when removing packages, but with the original database lost is the best we can do.

```
# pacman -D --asdeps $(pacman -Qq)
# pacman -D --asexplicit $(pacman -Qtq)

```

Optionally check all installed packages for corruption:

```
# pacman -Qk

```

Optionally [#Identify files not owned by any package](#Identify_files_not_owned_by_any_package).

Update all packages:

```
# pacman -Su

```

### Recovering a USB key from existing install

If you have Arch installed on a USB key and manage to mess it up (e.g. removing it while it is still being written to), then it is possible to re-install all the packages and hopefully get it back up and working again (assuming USB key is mounted in /newarch)

```
# pacman -S $(pacman -Qq --dbpath /newarch/var/lib/pacman) --root /newarch --dbpath /newarch/var/lib/pacman

```

### Extracting contents of a .pkg file

The `.pkg` files ending in `.xz` are simply tar'ed archives that can be decompressed with:

```
$ tar xvf package.tar.xz

```

If you want to extract a couple of files out of a `.pkg` file, this would be a way to do it.

### Viewing a single file inside a .pkg file

For example, if you want to see the contents of `/etc/systemd/logind.conf` supplied within the [systemd](https://www.archlinux.org/packages/?name=systemd) package:

```
$ tar -xOf /var/cache/pacman/pkg/systemd-204-3-x86_64.pkg.tar.xz etc/systemd/logind.conf

```

Or you can use [vim](https://www.archlinux.org/packages/?name=vim), then browse the archive:

```
$ vim /var/cache/pacman/pkg/systemd-204-3-x86_64.pkg.tar.xz

```

### Find applications that use libraries from older packages

Even if you installed a package the existing long-running programs (like daemons and servers) still keep using code from old package libraries. And it is a bad idea to let these programs running if the old library contains a security bug.

Here is a way how to find all the programs that use old packages code:

```
# lsof +c 0 | grep -w DEL | awk '1 { print $1 ": " $NF }' | sort -u

```

It will print running program name and old library that was removed or replaced with newer content.

## Performance

### Database access speeds

Pacman stores all package information in a collection of small files, one for each package. Improving database access speeds reduces the time taken in database-related tasks, e.g. searching packages and resolving package dependencies. The safest and easiest method is to run as root:

```
# pacman-optimize

```

This will attempt to put all the small files together in one (physical) location on the hard disk so that the hard disk head does not have to move so much when accessing all the data. This method is safe, but is not foolproof: it depends on your filesystem, disk usage and empty space fragmentation. Another, more aggressive, option would be to first remove uninstalled packages from cache and to remove unused repositories before database optimization:

```
# pacman -Sc && pacman-optimize

```

### Увеличение скорости загрузки

**Примечание:** Если у вас низкая скорость загрузки, убедитесь, что не используете зеркало ftp.archlinux.org ([новость с марта 2007 г.](https://www.archlinux.org/news/302/)), вместо него используйте другие зеркала из списка [зеркал](/index.php/Mirrors_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mirrors (Русский)").

When downloading packages pacman uses the mirrors in the order they are in `/etc/pacman.d/mirrorlist`. The mirror which is at the top of the list by default however may not be the fastest for you. To select a faster mirror, see [Mirrors](/index.php/Mirrors "Mirrors").

Скорость Pacman'а при загрузке пакетов также можно улучшить, если использовать другое приложение для загрузки вместо встроенного в Pacman менеджера закачек.

В любом случае, прежде чем делать какие-либо изменения, убедитесь, что используете самый свежий Pacman.

```
# pacman -Syu

```

#### Powerpill

Powerpill is a full wrapper for Pacman that uses parallel and segmented downloads to speed up the download process. Normally Pacman will download one package at a time, waiting for it to complete before beginning the next download. Powerpill takes a different approach: it tries to download as many packages as possible at once.

The [Powerpill wiki page](/index.php/Powerpill "Powerpill") provides basic configuration and usage examples along with package and upstream links.

#### wget

Если Вам нужны более мощные настройки прокси, в отличии от тех, которые предоставляет встроенный менеджер закачек [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)")'а.

Для использования `wget`, во первых [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [wget](https://www.archlinux.org/packages/?name=wget) а затем отредактируйте `/etc/pacman.conf` приведя в секции `[options]` строку к следующему виду:

```
XferCommand = /usr/bin/wget -c -q --show-progress --passive-ftp -O %o %u

```

Вместо того чтобы размещать параметры `wget` в файле `/etc/pacman.conf`, Вы можете изменять непосредственно конфигурационный файл `wget`(общесистемный файл `/etc/wgetrc`, или пользовательские файлы `$HOME/.wgetrc`.

#### aria2

[aria2](/index.php/Aria2_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Aria2 (Русский)") - легковесная утилита загрузки с возможностью докачки и сегментированной HTTP/HTTPS и FTP загрузки. [aria2](http://aria2.sourceforge.net/) - одновременно поддерживает несколько HTTP/HTTPS и FTP подключений к зеркалам Arch, это означает, что может увеличиться скорости загрузки файлов и поиска пакетов.

**Примечание:** Using aria2c in Pacman's XferCommand will **not** result in parallel downloads of multiple packages. Pacman invokes the XferCommand with a single package at a time and waits for it to complete before invoking the next. To download multiple packages in parallel, see the [powerpill](#Using_Powerpill) section above.

Install [aria2](https://www.archlinux.org/packages/?name=aria2), then edit `/etc/pacman.conf` by adding the following line to the `[options]` section:

```
XferCommand = /usr/bin/aria2c --allow-overwrite=true --continue=true --file-allocation=none --log-level=error --max-tries=2 --max-connection-per-server=2 --max-file-not-found=5 --min-split-size=5M --no-conf --remote-time=true --summary-interval=60 --timeout=5 --dir=/ --out %o %u

```

**Совет:** [This alternative configuration for using pacman with aria2](https://bbs.archlinux.org/viewtopic.php?pid=1491879#p1491879) tries to simplify configuration and adds more configuration options.

See [OPTIONS](http://aria2.sourceforge.net/manual/en/html/aria2c.html#options) in `man aria2c` for used aria2c options.

	`-d, --dir`

	Директорию для загруженных файлов брать из настроек [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)").

	`-o, --output`

	Имя полученного файла из загруженного.

	`%o`

	Переменная предоставляющая локальные файлы согласно настройкам pacman.

	`%u`

	Переменная предоставляюща загруженные URL согласно настройкам pacman.

#### Другие приложения

Есть и другие приложения для загрузок, которые можно использовать с Pacman. Вот они и связанные с ними параметры XferCommand:

*   `snarf`: `XferCommand = /usr/bin/snarf -N %u`
*   `lftp`: `XferCommand = /usr/bin/lftp -c pget %u`
*   `axel`: `XferCommand = /usr/bin/axel -n 2 -v -a -o %o %u`