Эта статья прояснит некоторые термины, которые используют в сообществе Arch Linux. Не стесняйтесь вносить правки, но желательно "Править" конкретный раздел, в не всю страницу. Пожалуйста, сохраняйте алфавитный порядок при добавлении нового раздела.

## Contents

*   [1 Arch Linux](#Arch_Linux)
*   [2 ABS](#ABS)
*   [3 ARM](#ARM)
*   [4 AUR](#AUR)
*   [5 PKGBUILD](#PKGBUILD)
*   [6 TU, Trusted User](#TU.2C_Trusted_User)
*   [7 bbs](#bbs)
*   [8 community/[community]](#community.2F.5Bcommunity.5D)
*   [9 core/[core]](#core.2F.5Bcore.5D)
*   [10 custom/user repository](#custom.2Fuser_repository)
*   [11 Developer](#Developer)
*   [12 extra/[extra]](#extra.2F.5Bextra.5D)
*   [13 hwd](#hwd)
*   [14 hwdetect](#hwdetect)
*   [15 initramfs](#initramfs)
*   [16 initrd](#initrd)
*   [17 makepkg](#makepkg)
*   [18 namcap](#namcap)
*   [19 package](#package)
*   [20 Мейнтейнер пакетов](#.D0.9C.D0.B5.D0.B9.D0.BD.D1.82.D0.B5.D0.B9.D0.BD.D0.B5.D1.80_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
*   [21 pacman](#pacman)
*   [22 pacman.conf](#pacman.conf)
*   [23 repository/repo](#repository.2Frepo)
*   [24 RTFM](#RTFM)
*   [25 tarball](#tarball)
*   [26 testing/[testing]](#testing.2F.5Btesting.5D)
*   [27 udev](#udev)
*   [28 wiki](#wiki)

## Arch Linux

Следует придерживаться следующего написания имени Arch:

*   **Arch Linux**
*   **Arch** (*Linux* добавляем в уме)
*   **archlinux** (в стиле UNIX)

Archlinux, ArchLinux, archLinux, aRcHlInUx и прочие вариации - долой.

'Arch' (подразумевая "Arch Linux") произносится /ˈɑrtʃ/ (*арч*), как в словах "archer" или "arch-nemesis", но *не* как в словах "ark" или "archangel" (*арк*).

## ABS

[Arch Build System](/index.php/Arch_Build_System_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Build System (Русский)") (ABS, *Система Сборки для Arch*) нужна, чтобы:

*   Создавать новые пакеты программ
*   Редактировать существующие пакеты под свои нужды
*   Пересобирать систему, используя флаги компиляции (примерно как в Gentoo)
*   Настраивать модули ядра на работу с модифицированным вами ядром

ABS полезна при использоввании Arch Linux, но не обязательна.

## ARM

**Примечание:** Сервис Arch Rollback Machine закрылся 18 августа 2013 [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1313360#p1313360)

[Arch Rollback Machine](/index.php/Downgrading_packages_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#ARM "Downgrading packages (Русский)") это зеркало, с которого можно было загрузить старые версии пакетов для отката системы.

## AUR

[Arch User Repository (AUR)](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") — это поддерживаемый сообществом репозиторий пакетов. AUR был изначально задуман, чтобы собрать в одном месте широко распространенные среди сообщества файлы [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)") и ускорить процесс попадания наиболее популярных из репозитория AUR [community] в репозитории [core] и [extra].

AUR - это родина всех новых пакетов. Пользователи представляют в AUR самостоятельно созданные пакеты. Сообщество AUR голосует за любимые из них, и, когда набирается достаточное количество голосов, [AUR Trusted User](#TU.2C_Trusted_User) может перевести пакет в репозиторий [community], к которому можно получить доступ через [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") и [ABS](/index.php/Arch_Build_System_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Build System (Русский)").

AUR находится здесь [здесь](https://aur.archlinux.org).

## PKGBUILD

[PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)")-ы - это небольшие скрипты для сборки пакетов Arch. Смотрите [Creating Packages](/index.php/Creating_packages_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Creating packages (Русский)")

## TU, Trusted User

[Доверенный пользователь](/index.php/Trusted_Users "Trusted Users") поддерживает репозитории AUR и [community]. У него есть привилегия перемещать особо популярные пакеты из AUR в [community]. TU назначается большинством голосов при голосовании других TU.

Доверенные пользователи следуют [AUR Trusted User Guidelines](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") и соблюдают [устав Доверенных пользователей](https://aur.archlinux.org/trusted-user/TUbylaws.html)

## bbs

**B**ulletin **b**oard **s**ystem - [форум](https://bbs.archlinux.org) по поддержке пользователей.

## community/[community]

В репозитории [community] находятся пакеты, которые перенесли из AUR доверенные пользователи. Чтобы получить доступ к [community], раскомментируйте строку с репозиторием в `/etc/pacman.conf`.

## core/[core]

В [core] находятся пакеты, необходимые для минимально работоспособной системы Arch Linux.

## custom/user repository

Каждый может создать свой собственный репозиторий, который другие пользователи могут добавить в `/etc/pacman.conf` и работать с ним через [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)"). Смотрите [здесь](/index.php/Custom_local_repository "Custom local repository"), как это можно сделать.

## Developer

Полубоги, бесплатно работающие над улучшением Arch. [Разработчики](https://www.archlinux.org/developers/) уступают лишь истинным богам - Джадду Винету и Аарону Гриффину.

## extra/[extra]

Изначальный набор пакетов Arch [core] довольно беден, поскольку содержит лишь необходимый минимум, но возможность расширить его дает репозиторий [extra]. Репозиторий постоянно растет благодаря сообществу пользователей. Именно в [extra] можно найти окружение рабочего стола, менеджер окон и другие программы общего назначения.

## hwd

[hwd](https://aur.archlinux.org/packages/hwd/) - это детектор "железа" вашего компьютера и генератор файла `xorg.conf`. *hwd* может предоставить информацию об используемом процессоре, видеокарте и прочих устройствах.

## hwdetect

[hwdetect](/index.php/Hwdetect "Hwdetect") это детектор устройств компьютера. Скрипт в основном используется для вывода информации о модулях, загружаемых через `/etc/[mkinitcpio.conf](/index.php/Mkinitcpio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mkinitcpio (Русский)")]`. The script makes use of information exported by the sysfs subsystem employed by the Linux kernel.

## initramfs

Смотрите [mkinitcpio](/index.php/Mkinitcpio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mkinitcpio (Русский)").

## initrd

The special file `/dev/initrd` is a read-only block device. Device `/dev/initrd` is a RAM disk that is initialized (e.g. loaded) by the boot loader before the kernel is started. The kernel then can use the block device `/dev/initrd`'s contents for a two phased system boot-up.

In the first boot-up phase, the kernel starts up and mounts an initial root file-system from the contents of `/dev/initrd` (e.g. RAM disk initialized by the boot loader). In the second phase, additional drivers or other modules are loaded from the initial root device's contents. After loading the additional modules, a new root file system (i.e. the normal root file system) is mounted from a different device.

## makepkg

[makepkg](/index.php/Makepkg "Makepkg") will build packages for you. makepkg will read the metadata required from a [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)") file. All it needs is a build-capable Linux platform, [wget](https://www.archlinux.org/packages/?name=wget), and some build scripts. The advantage to a script-based build is that you only really do the work once. Once you have the build script for a package, you just need to run makepkg and it will do the rest: download and validate source files, check dependencies, configure the build time settings, build the package, install the package into a temporary root, make customizations, generate meta-info, and package the whole thing up for [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") to use.

## namcap

[namcap](/index.php/Namcap "Namcap") is a package analysis utility that looks for problems with Arch Linux packages or their [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)") files. It can apply rules to the file list, the files themselves, or individual PKGBUILD files.

Rules return lists of messages. Each message can be one of three types: error, warning, or information (think of them as notes or comments). Errors (designated by 'E:') are things that namcap is very sure are wrong and need to be fixed. Warnings (designated by 'W:') are things that namcap thinks should be changed but if you know what you are doing then you can leave them. Information (designated 'I:') are only shown when you use the info argument. Information messages give information that might be helpful but is not anything that needs changing.

## package

A package is an archive containing

*   all of the (compiled) files of an application
*   metadata about the application, such as application name, version, dependencies, ...
*   installation files and directives for [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)")
*   (optionally) extra files to make your life easier, such as a start/stop script

Arch's package manager pacman can install, update, and remove those packages. Using packages instead of compiling and installing programs yourself has various benefits:

*   easily updatable: pacman will update existing packages as soon as updates are available
*   dependency checks: pacman handles dependencies for you, you only need to specify the program and pacman installs it together with every other program it needs
*   clean removal: pacman has a list of every file in a package. This way, no files are left behind when you decide to remove a package.

**Примечание:** Different GNU/Linux distributions use different packages and package managers, meaning that you cannot use pacman to install a Debian package on Arch.

## Мейнтейнер пакетов

The role of the package maintainer is to update packages as new versions become available upstream and to field support questions relating to bugs in said packages. The term may be applied to any of the following:

*   A core Arch Linux developer who maintains a software package in one of the official repositories (core, extra, or testing).
*   A [Trusted User](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") of the community who maintains software packages in the unsupported/unofficial community repository.
*   A normal user who maintains a [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)") and local source files in the [AUR](/index.php/AUR "AUR").

The maintainer of a package is the person currently responsible for the package. Previous maintainers should be listed as contributors in the PKGBUILD along with others who have contributed to the package.

## pacman

The [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") package manager is one of the great highlights of Arch Linux. It combines a simple binary package format with an easy-to-use build system (see [ABS](/index.php/ABS "ABS")). Pacman makes it possible to easily manage and customize packages, whether they be from the official Arch repositories or the user's own creations. The repository system allows users to build and maintain their own custom package repositories, which encourages community growth and contribution (see [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)")).

Pacman can keep a system up to date by synchronizing package lists with the master server, making it a breeze for the security-conscious system administrator to maintain. This server/client model also allows you to download/install packages with a simple command, complete with all required dependencies (similar to Debian's apt-get).

NB: Pacman was written by Judd Vinet, the creator of Arch Linux. It is used as a package management tool by other distributions as well, such as FrugalWare, Rubix, UfficioZero (in Italian, based on Ubuntu), and, of course, [Arch based distributions](/index.php/Arch_based_distributions_(active) "Arch based distributions (active)") such as Archie and AEGIS.

## pacman.conf

Это конфигурационный файл [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)"). он расположен в `/etc`. Подробнее о формате настроек:

```
man pacman.conf

```

## repository/repo

Репозиторий содержит предварительно скомпилированные пакеты одного или, что чаще, нескольких [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)")-ов. Официальными являются следующие репозитории:

*   [core]: содержит последние версии пакетов, необходимых для полностью работоспособной [CLI](https://ru.wikipedia.org/wiki/Интерфейс_командной_строки)-системы
*   [extra]: содержит последние версии пакетов общего назначения, как было описано выше.
*   [community]: пакеты, набравшие достаточное количество голосов в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") и перенесенные оттуда.

Pacman использует эти репозитории для поиска и установки пакетов. Репозиторий может быть как локальным, находящимся на вашем компьютере, так и удаленным, то есть пакеты сначала скачиваются, а потом устанавливаются.

## [RTFM](https://en.wikipedia.org/wiki/RTFM "wikipedia:RTFM")

"Read The Fucking (or Fine) Manual" - Прочитай Чертов (или Прекрасный) Мануал. Такой ответ часто дают новичкам Linux/Arch, которые спрашивают о том, что черным по белому написано в мануале той или иной программы.

Так отвечают, когда видят, что спрашивающий и не пытался найти решение самостоятельно. Если кто-то ответил вам в таком духе, то это не попытка обидеть, а лишь разочарование в связи с отсутствием каких-либо усилий с вашей стороны.

Лучшее, что можно сделать, если вы получили такой ответ, это прочитать мануал:

```
man PROGRAM-NAME

```

где PROGRAM-NAME - это имя программы, с которой возникли сложности.

Если вы не нашли ответ на свой вопрос в мануале, то есть еще несколько способов это сделать, прежде чем задавать вопрос на форуме:

*   искать в [wiki](/index.php/Special:Search "Special:Search")
*   искать на [форуме](https://bbs.archlinux.org). Можно также заглянуть на [форум русскоязычного сообщества](http://www.archlinux.org.ru/forum/).
*   искать в [почтовой рассылке](https://www.google.com/#hl=en&q=arch+site:archlinux.org%2Fpipermail%2F)
*   искать в [интернете](https://www.google.com)

## tarball

Заархивированный [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)") и файлы с исходными кодами, необходимыми makepkg для создания устанавливаемого бинарного пакета. Архив называется "tAURball", потому что его можно скачать в репозитории [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").

## testing/[testing]

В этом репозитории находятся пакеты, ожидающие перемещения в главный репозиторий, но в данный момент тестируемые на наличие багов. По умолчанию не активен, но можно включить его в `/etc/pacman.conf`.

## udev

[udev](/index.php/Udev "Udev") provides a dynamic device directory containing only the files for actually present devices. It creates or removes device node files in the `/dev` directory, or it renames network interfaces.

Usually udev runs as udevd(8) and receives uevents directly from the kernel if a device is added/removed to/from the system.

If udev receives a device event, it matches its configured rules against the available device attributes provided in sysfs to identify the device. Rules that match may provide additional device information or specify a device node name and multiple symlink names and instruct udev to run additional programs as part of the device event handling.

## [wiki](https://en.wikipedia.org/wiki/Wiki "wikipedia:Wiki")

[Вот!](/index.php/Main_page_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Main page (Русский)") Документация Arch Linux, которую может редактировать каждый.