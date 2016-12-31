В данной статье приводится список вспомогательных интструментов для поиска и/или сборки пакетов из [Пользовательского репозитория Arch](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").

**Важно:** Ни один из перечисленных в статье инструментов не поддерживается разработчиками Arch. См. [[1]](https://bbs.archlinux.org/viewtopic.php?pid=828254#p828254).

Список графических фронтендов для pacman, некоторые из которых могут работать с AUR можно найти в [соответствующей статье](/index.php/Pacman_GUI_Frontends_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman GUI Frontends (Русский)").

## Contents

*   [1 Список вспомогательных инструментов](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.B2.D1.81.D0.BF.D0.BE.D0.BC.D0.BE.D0.B3.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D0.B8.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D0.BE.D0.B2)
    *   [1.1 aurget](#aurget)
    *   [1.2 aurora](#aurora)
    *   [1.3 aurpac](#aurpac)
    *   [1.4 aurploader](#aurploader)
    *   [1.5 aursh](#aursh)
    *   [1.6 autoaur](#autoaur)
    *   [1.7 burp](#burp)
    *   [1.8 cower](#cower)
    *   [1.9 haskell-archlinux](#haskell-archlinux)
    *   [1.10 makeaur](#makeaur)
    *   [1.11 Meat ( Alpha / Under development )](#Meat_.28_Alpha_.2F_Under_development_.29)
    *   [1.12 pacaur](#pacaur)
    *   [1.13 packer](#packer)
    *   [1.14 pacmoon](#pacmoon)
    *   [1.15 paktahn](#paktahn)
    *   [1.16 pbfetch](#pbfetch)
    *   [1.17 pbget](#pbget)
    *   [1.18 pkgman](#pkgman)
    *   [1.19 powaur](#powaur)
    *   [1.20 spinach](#spinach)
    *   [1.21 srcman](#srcman)
    *   [1.22 yaourt](#yaourt)
*   [2 Сравнительная таблица](#.D0.A1.D1.80.D0.B0.D0.B2.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D1.82.D0.B0.D0.B1.D0.BB.D0.B8.D1.86.D0.B0)

## Список вспомогательных инструментов

### aurget

Цель aurget - предоставление простого, подобного pacman интерфейса к AUR, сделать AUR удобным, в независимости от того, желает ли пользователь найти, скачать, собрать, установить или обновить пакеты AUR.

*   Сайт: [http://pbrisbin.com/posts/aurget/](http://pbrisbin.com/posts/aurget/)
*   Пакет: [https://aur.archlinux.org/packages/aurget/](https://aur.archlinux.org/packages/aurget/)

### aurora

Aurora is a very simple frontend for the AUR. It allows the user to install AUR packages, download the AUR packages (for manual installation) and also offers an AUR upgrade feature. By design, aurora does not wrap pacman.

*   Сайт: [http://bitbucket.org/bbenne10/aurora](http://bitbucket.org/bbenne10/aurora)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=41732](https://aur.archlinux.org/packages.php?ID=41732) (not available)

### aurpac

Light'n'fast AUR and pacman frontend.

*   Сайт: [http://3ed.jogger.pl/2009/02/15/aurpac/](http://3ed.jogger.pl/2009/02/15/aurpac/) (not available)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=23919](https://aur.archlinux.org/packages.php?ID=23919) (not available)

### aurploader

Aurploader prompts the user for an AUR username and password and will then upload PKGBUILD tarballs to the AUR. Before uploading each Пакет, the user is prompted to select a category. When the uploads have completed, the user is asked if the cookie file should be kept so that the script can be run again without needing the AUR username and password to be re-entered.

*   Сайт: [http://xyne.archlinux.ca/info/aurploader](http://xyne.archlinux.ca/info/aurploader) (not available)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=23393](https://aur.archlinux.org/packages.php?ID=23393) (not available)

### aursh

**Примечание:** По состоянию на 30.09.2010 активная разработка прекращена.

AurShell is a shell-like application. With plugins included, it's possible to build and install packages from AUR, ABS, and even wrap pacman.

*   Сайт: [http://github.com/husio/aursh/](http://github.com/husio/aursh/) (not available)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=33423](https://aur.archlinux.org/packages.php?ID=33423) (not available)

### autoaur

autoaur is a script for automatic mass downloading, updating, building, and installing groups of AUR packages.

*   Сайт: [autoaur](/index.php?title=Autoaur&action=edit&redlink=1 "Autoaur (page does not exist)")
*   Пакет: [https://aur.archlinux.org/packages.php?ID=6390](https://aur.archlinux.org/packages.php?ID=6390) (not available)

### burp

burp is a fast and simple AUR uploader written in C. Supports persistent cookies for seamless logins.

*   Сайт: [http://github.com/falconindy/burp](http://github.com/falconindy/burp) (not available)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=37216](https://aur.archlinux.org/packages.php?ID=37216) (not available)

### cower

Cower is a fast and simple AUR search and download agent, which will also check for updates and download dependencies.

*   Сайт: [http://github.com/falconindy/cower](http://github.com/falconindy/cower)
*   Форум: [https://bbs.archlinux.org/viewtopic.php?id=97137](https://bbs.archlinux.org/viewtopic.php?id=97137)
*   Пакет: [https://aur.archlinux.org/packages/cower/](https://aur.archlinux.org/packages/cower/)

### haskell-archlinux

haskell-archlinux is a library to programmatically access the AUR and Пакет metadata from the Haskell programming language.

*   Сайт: [https://hackage.haskell.org/package/archlinux](https://hackage.haskell.org/package/archlinux)
*   Пакет: [https://aur.archlinux.org/packages/haskell-archlinux/](https://aur.archlinux.org/packages/haskell-archlinux/)

### makeaur

Makeaur is a wrapper for pacman and makepkg that allows users to easily install packages from the Arch User Repository.

*   Сайт: [http://github.com/ghost1227/makeaur/](http://github.com/ghost1227/makeaur/)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=23678](https://aur.archlinux.org/packages.php?ID=23678) (not available)

### Meat ( Alpha / Under development )

Meat is a front-end for cower ( see above ) and it is fully written in bash.

*   Сайт: [http://github.com/e36freak/meat](http://github.com/e36freak/meat)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=50075](https://aur.archlinux.org/packages.php?ID=50075) (not available)

### pacaur

Pacaur is a fast workflow AUR wrapper, using [cower](/index.php/AUR_helpers#cower "AUR helpers") as backend. It aims on speed and simplicity, with an uncluttered interface. It is inspired by [pbfetch](/index.php/AUR_helpers#pbfetch "AUR helpers").

*   Сайт: [https://github.com/Spyhawk/pacaur](https://github.com/Spyhawk/pacaur)
*   Форум: [https://bbs.archlinux.org/viewtopic.php?pid=937423](https://bbs.archlinux.org/viewtopic.php?pid=937423)
*   Пакет: [https://aur.archlinux.org/packages/pacaur/](https://aur.archlinux.org/packages/pacaur/)

### packer

Packer is a wrapper for pacman and the AUR. It was designed to be a simple and very fast replacement for the basic functionality of Yaourt. It has commands to install, update, search, and show information for any Пакет in the main repositories and in the AUR. Use pacman for other commands, such as removing a Пакет.

*   Сайт: [http://github.com/bruenig/packer](http://github.com/bruenig/packer) (not available)
*   Форум: [https://bbs.archlinux.org/viewtopic.php?id=88115](https://bbs.archlinux.org/viewtopic.php?id=88115)
*   Пакет: [https://aur.archlinux.org/packages/packer/](https://aur.archlinux.org/packages/packer/)
*   Wiki: [https://github.com/bruenig/packer/wiki](https://github.com/bruenig/packer/wiki)

### pacmoon

pacmoon is a script for compiling arch linux packages from the AUR and repositories. It can automatically install make dependencies as binaries when necessary and update the entire system or just packages listed. It keeps track of which files have been compiled so that in the event of compiled packages getting replaced with a binary (like during an upgrade process) then pacmoon can recompile only the necessary packages.

*   Сайт: [http://chilon.net/pacmoon](http://chilon.net/pacmoon)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=41911](https://aur.archlinux.org/packages.php?ID=41911)

### paktahn

Paktahn is a yaourt replacement. It is under active development and already includes improvements such as a local cache for fast searches and interactive installation.

*   Сайт: [http://github.com/skypher/paktahn](http://github.com/skypher/paktahn)
*   Форум: [https://bbs.archlinux.org/viewtopic.php?id=77674&p=1](https://bbs.archlinux.org/viewtopic.php?id=77674&p=1)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=30242](https://aur.archlinux.org/packages.php?ID=30242)

### pbfetch

Pbfetch is a script which can be used as a pacman-independent AUR helper or a pacman wrapper with additional AUR functionality. Pbfetch aims to be a simple and fast versus the well established yaourt. Pbfetch can be used as a shortcut to simply download PKGBUILDs from AUR or automatically build with dependency resolution among other things. The user can select which AUR packages to upgrade using a simple menu as well as update all AUR packages.

*   Сайт/Source: [https://github.com/dalingrin/pbfetch](https://github.com/dalingrin/pbfetch)
*   Форум: [https://bbs.archlinux.org/viewtopic.php?id=87789](https://bbs.archlinux.org/viewtopic.php?id=87789)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=33256](https://aur.archlinux.org/packages.php?ID=33256)

### pbget

Pbget is a simple command-line tool for retrieving PKGBUILDs and local source files for Arch Linux. It is able to retrieve files from the official SVN and CVS web interface, the AUR and the ABS rsync server.

*   Сайт: [http://xyne.archlinux.ca/info/pbget](http://xyne.archlinux.ca/info/pbget)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=23848](https://aur.archlinux.org/packages.php?ID=23848)

### pkgman

pkgman is a script which helps to manage a local repository. It retrieves the PKGBUILD and related files for given name from ABS or AUR and lets you edit them, automatically generates checksums, backs up the source tarball, builds and adds the Пакет to your local repository. Then you can install it as usual with pacman. It also has AUR support for submitting tarballs and leaving comments.

*   Сайт: [http://sourceforge.net/apps/mediawiki/pkgman/index.php](http://sourceforge.net/apps/mediawiki/pkgman/index.php)
*   Форум: [https://bbs.archlinux.org/viewtopic.php?id=49023](https://bbs.archlinux.org/viewtopic.php?id=49023)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=17100](https://aur.archlinux.org/packages.php?ID=17100)

### powaur

powaur is a minimalistic AUR helper with a pacman-like interface.

*   Сайт: [https://github.com/yanhan/powaur](https://github.com/yanhan/powaur)
*   Форум: [https://bbs.archlinux.org/viewtopic.php?pid=938688](https://bbs.archlinux.org/viewtopic.php?pid=938688)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=49296](https://aur.archlinux.org/packages.php?ID=49296)

### spinach

Spinach is a tiny Bash AUR helper with few dependencies.

*   Сайт: [http://floft.net/wiki/Scripts/Spinach](http://floft.net/wiki/Scripts/Spinach)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=46993](https://aur.archlinux.org/packages.php?ID=46993)

### srcman

srcman is a pacman/makepkg wrapper written in Bash, which transparently handles pacman operations on 'source packages'. This means, for example, that packages can be specified for installation either explicitly (pacman's -U operation) or can be installed from a (source) repository (-S operation). The address of an AUR pacman database can be found in the corresponding Форум thread, by the way. The primary goal of this project is to provide a complete pacman wrapper and therefore, srcman supports all current pacman operations for binary *and* source packages.

*   Сайт: [https://bbs.archlinux.org/viewtopic.php?id=65501](https://bbs.archlinux.org/viewtopic.php?id=65501)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=23945](https://aur.archlinux.org/packages.php?ID=23945)

### yaourt

[Yaourt](/index.php/Yaourt "Yaourt") (Yet Another User Repository Tool) это разрабатываемая сообществом обертка для pacman, которая добавляет бесшовный доступ к AUR, поддерживает автоматическую компиляцию и установку пакетов по вашему выбору из тысяч PKGBUILS в дополнение к доступным в Arch Linux многим тысячам бинарных пакетов в официальных репозиториях. Yaourt использует синтаксис pacman, что позволит вам не осваивать принципиально новый способ обслуживания системы, но также добавляет новые возможности. Yaourt расширяет мощь и простоту pacman путем добавления многих полезных функций, поддерживает приятный глазу цветной вывод результатов, интерактивный поиск и многое другое.

*   Сайт: [http://archlinux.fr/yaourt-en](http://archlinux.fr/yaourt-en)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=5863](https://aur.archlinux.org/packages.php?ID=5863)

## Сравнительная таблица

| Программа | Язык | Поддержка зависимостей | Поддержка репозиториев Core/extra/community | Активно разрабатывается | Использование |
| [Aurget](#aurget) | Bash | Да | Нет | Да | see `aurget --help` |
| [AurShell](#aursh) | Python | Нет | Нет | Нет | aursh (запускает Aurshell, где используется определенный набор команд) |
| [Aurora](#aurora) | Python3 | Базовая (при помощи makepkg) | Нет | Да | см. aurora --help |
| [Clyde](#clyde) | Lua | Да | Да | Нет | Идентично pacman'у (например, clyde -S <имя_пакета>) |
| [Cower](#cower) | C | Да | Нет | Да | см. `cower -h` |
| [Makeaur](#makeaur) | Bash | Нет | Нет | Создан форк | makeaur <имя_пакета> |
| [Pacaur](#pacaur) | Bash, backend in C (cower) | Да | Да | Да | Идентично pacman'у, со специфичными для AUR аргументами. См. также `pacaur -h`. |
| [Packer](#packer) | Bash | Да | Да | Да | Идентично pacman'у (например, packer -S <имя_пакета>) |
| [pacmoon](#pacmoon) | Zsh | Да | Да | Да | Идентично emerge из portage pacmoon -av <имя_пакета> |
| [Paktahn](#paktahn) | Lisp | Да | Да | Да | Идентично pacman'у (например, pak -S <имя_пакета>) |
| [pbfetch](#pbfetch) | Bash | Да | Да | Да | Идентично pacman'у, со специфичными для AUR аргументами (доп. аргументы для редактирования PKGBUILD и т.п.) |
| [powaur](#powaur) | C | Нет | Ограниченная | Да | Идентично pacman'у (например, powaur -S <имя_пакета>) |
| [tupac](#tupac) | PHP | Да | Да | Updated under request | Идентично pacman'у (например, tupac -S <имя_пакета>) |
| [Yaourt](#yaourt) | Bash, бэкенд на C | Да | Да | Да | Идентично pacman'у (например, yaourt -S <имя_пакета>) |