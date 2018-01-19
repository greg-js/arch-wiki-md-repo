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
*   Пакет: [aurget](https://aur.archlinux.org/packages/aurget/)

### aurora

Aurora это очень простой фронтэнд для Aur. Он позволяет пользовательзователю устанавливать AUR-пакеты, скачивать AUR-пакеты(для продвинутой установки) и также помогает улучшать будующее AUR. Благодаря дизайну aurora не заменит pacman.

*   Сайт: [http://bitbucket.org/bbenne10/aurora](http://bitbucket.org/bbenne10/aurora)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=41732](https://aur.archlinux.org/packages.php?ID=41732) (not available)

### aurpac

Быстрый AUR и pacman фронтэнд

*   Сайт: [http://3ed.jogger.pl/2009/02/15/aurpac/](http://3ed.jogger.pl/2009/02/15/aurpac/) (not available)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=23919](https://aur.archlinux.org/packages.php?ID=23919) (not available)

### aurploader

Aurploader prompts the user for an AUR username and password and will then upload PKGBUILD tarballs to the AUR. Before uploading each Пакет, the user is prompted to select a category. When the uploads have completed, the user is asked if the cookie file should be kept so that the script can be run again without needing the AUR username and password to be re-entered.

*   Сайт: [http://xyne.archlinux.ca/info/aurploader](http://xyne.archlinux.ca/info/aurploader) (not available)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=23393](https://aur.archlinux.org/packages.php?ID=23393) (not available)

### aursh

**Примечание:** По состоянию на 30.09.2010 активная разработка прекращена.

AurShell это приложение-консоль. С предустановленными плагинами возможно собрать или установить пакеты из:AUR, ABS,pacman

*   Сайт: [http://github.com/husio/aursh/](http://github.com/husio/aursh/) (not available)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=33423](https://aur.archlinux.org/packages.php?ID=33423) (not available)

### autoaur

autoaur - это скрипт автоматической массовой загрузки, обновления и установки AUR-пакетов.

*   Сайт: [autoaur](/index.php?title=Autoaur&action=edit&redlink=1 "Autoaur (page does not exist)")
*   Пакет: [https://aur.archlinux.org/packages.php?ID=6390](https://aur.archlinux.org/packages.php?ID=6390) (not available)

### burp

burp это быстрый и простой AUR загрузчик написанный на С. Поддерживает технологию Cookie

*   Сайт: [http://github.com/falconindy/burp](http://github.com/falconindy/burp) (not available)
*   Пакет: [https://aur.archlinux.org/packages.php?ID=37216](https://aur.archlinux.org/packages.php?ID=37216) (not available)

### cower

Cower - быстрый и простой AUR-поисковик и загрузчик. Он также позволяет проверять обновления и подтягивать зависимости.

*   Сайт: [http://github.com/falconindy/cower](http://github.com/falconindy/cower)
*   Форум: [https://bbs.archlinux.org/viewtopic.php?id=97137](https://bbs.archlinux.org/viewtopic.php?id=97137)
*   Пакет: [cower](https://aur.archlinux.org/packages/cower/)

### haskell-archlinux

haskell-archlinux это програмная библиотека позволяющая использовать AUR и метаданные пакета используя язык Haskell

*   Сайт: [https://hackage.haskell.org/package/archlinux](https://hackage.haskell.org/package/archlinux)
*   Пакет: [haskell-archlinux](https://aur.archlinux.org/packages/haskell-archlinux/)

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
*   Пакет: [pacaur](https://aur.archlinux.org/packages/pacaur/)

### packer

Packer is a wrapper for pacman and the AUR. It was designed to be a simple and very fast replacement for the basic functionality of Yaourt. It has commands to install, update, search, and show information for any Пакет in the main repositories and in the AUR. Use pacman for other commands, such as removing a Пакет.

*   Сайт: [http://github.com/bruenig/packer](http://github.com/bruenig/packer) (not available)
*   Форум: [https://bbs.archlinux.org/viewtopic.php?id=88115](https://bbs.archlinux.org/viewtopic.php?id=88115)
*   Пакет: [packer](https://aur.archlinux.org/packages/packer/)
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

Расшифровка значений колонок:

*   *Безопасный*: не [исполняет](/index.php/Help:Reading_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Source "Help:Reading (Русский)") PKGBUILD по умолчанию вообще, или предварительно уведомляет об этом пользователя и предлагает ему возможность предварительно просмотреть файл. Некоторые помощники, как известно, выполняют PKGBUILD перед показом пользователю, **разрешая выполнение вредоносного кода**. *Опционально* означает, что существует флаг командной строки или опция конфигурации для предотвращения автоматического выполнения файла перед просмотром.
*   *Чистая сборка*: не экспортирует новые переменные, которые могут помешать успешному процессу сборки.
*   *Надёжный парсер*: способность обрабатывать сложные пакеты (например [aws-cli-git](https://aur.archlinux.org/packages/aws-cli-git/)), используя предоставленные метаданные (RPC/.SRCINFO) вместо [парсинга](https://en.wikipedia.org/wiki/Parsing#Parser "w:Parsing") PKGBUILD.
*   *Надёжный разрешатель*: способность корректно разрешать и собирать сложные цепочки зависимостей, такие, как [plasma-git-meta](https://aur.archlinux.org/packages/plasma-git-meta/).
*   *Разделённые пакеты*: способность правильно собирать и устанавливать разделённые пакеты (такие, как [python-nikola](https://aur.archlinux.org/packages/python-nikola/)) независимо.
*   *Git clone*: использует команду git clone вместо загрузки тарболлов (устарело с AUR 4)
*   *Синтаксис*: P — значит [Pacman](/index.php/Pacman "Pacman")-подобный, S — собственный.

| Название | Язык | Безопасный | Чистая сборка | Надёжный парсер | Надёжный разрешатель | Разделённые пакеты | Git clone | Автодополнение в оболочках | Синтаксис | Специфика |
| apacman | Bash | Нет [[2]](https://github.com/oshazard/apacman/issues/8) | Нет [[3]](https://github.com/oshazard/apacman/search?utf8=%E2%9C%93&q=export) | Нет | Нет | Нет | Нет | - | P | Форк *packer* |
| aura | Haskell | Да | Да | Нет [[4]](https://github.com/aurapm/aura/issues/14) | Нет | Нет [[5]](https://github.com/aurapm/aura/issues/353) | Нет | bash/zsh | P | Откаты, [ABS](/index.php/ABS "ABS"), поддержка [powerpill](/index.php/Powerpill "Powerpill"), многоязычный, требует [Haskell](/index.php/Haskell "Haskell") |
| aurel | Emacs Lisp | Да | N/A | Да | N/A | N/A | Нет | N/A | S | интеграция с Emacs, нет автосборок |
| aurget | Bash | Опционально | Да | Нет | Нет | Нет [[6]](https://github.com/pbrisbin/aurget/issues/40) | Нет | bash/zsh | P | сортировка по голосам |
| aurutils | Bash/C | Да | Да | Да | Да | Да | Да | zsh | S | [vifm](/index.php/Vifm "Vifm"), [PCRE](https://en.wikipedia.org/wiki/PCRE "w:PCRE"), [Локальный репозиторий](/index.php/Local_repository "Local repository"), [подписи пакетов](/index.php/Package_signing "Package signing"), поддержка [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") |
| bauerbill | Python3 | Да | Да | Да | Да | Да | Да | bash/zsh | P/S | Управление доверием, поддержка ABS,расширяет Powerpill |
| burgaur | Python3/C | Опционально с [mc](/index.php/Mc "Mc") | Да | Нет | Нет | Нет | Нет | - | P | Обертка для *cower* |
| cower | C | Да | N/A | Да | N/A | N/A | Нет | bash/zsh | S | Нет автосборки, поддержка регулярок, сортировка по голосам/популярности |
| owlman | Bash/C | Да | Да | Да | Нет | Частично | Нет | - | S | Обертка для *cower* |
| pacaur | Bash/C | Да | Да | Да | Да | Да | Да | bash/zsh | P/S | Минимизирует взаимодействие с пользователем, многоязычный, сортировка по голосам/популярности |
| packer | Bash | Нет | Да | Нет | Нет | Нет | Нет | - | P | - |
| pbget | Python3 | Да | N/A | Да | N/A | N/A | Да | - | S | Нет автосборки |
| PKGBUILDer | Python3 | Опционально | Да | Да | Да | Частично [[7]](https://github.com/Kwpolska/pkgbuilder/issues/39) | Да | - | P | Автосборка по умолчанию, используйте `-F` для отключения. Многоязычный |
| prm | Bash | Да [[8]](https://git.fleshless.org/prm/commit/?id=e7252333b07975ea40f526269ce995e375e627bf) | N/A | Да | N/A | N/A | Да | - | S | Нет автосборки, поддержка ABS |
| repoctl | Go | Да | N/A | Да [[9]](https://github.com/goulash/pacman/blob/master/aur/aur.go) | N/A | N/A | Нет | zsh | S | Нет автосборки, поддержка локальных репозиториев |
| spinach | Bash | Нет [[10]](https://github.com/floft/spinach/blob/master/spinach#L287) | Да | Нет | Нет | Нет | Нет | - | S | - |
| trizen | Perl | Да | Да | Да [[11]](https://github.com/trizen/trizen/commit/7ab7ee5f9f1f5d971b731d092fc8e1dd963add4b) | Нет | Да [[12]](https://github.com/trizen/trizen/commit/3c94434c66ede793758f2bf7de84d68e3174e2ac) | Нет | - | P | комментарии из AUR |
| wrapaur | Bash | Да | Да | Нет | Нет | Нет | Да | - | S | обновление зеркал, вывод новостей и комментариев AUR |
| yaah | Bash | Да | N/A | Да | N/A | N/A | Опционально | bash | S | Нет автосборки |
| yaourt | Bash/C | Нет (*yaourt -Si*) [[13]](https://github.com/archlinuxfr/yaourt/blob/f373121d23d87031a24135fee593115832d803ec/src/lib/aur.sh#L47) [[14]](https://github.com/archlinuxfr/yaourt/blob/d9790e29cd7194535c793f51d185b7130a396916/src/lib/pkgbuild.sh.in#L415-L438) | Нет [[15]](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html) | Нет | Нет [[16]](https://github.com/archlinuxfr/yaourt/issues/186) | Нет [[17]](https://github.com/archlinuxfr/yaourt/issues/85) | Опционально | bash/zsh/fish | P | Резервное копирование, поддержка ABS, комментарии AUR, многоязычный |
| yay | Go | Да | Да | Да | Нет | Частично | Нет | bash/zsh/fish | P | сортировка по голосам |

**Note:** [Pacman](/index.php/Pacman "Pacman") 4.2\. ввёл специфичные для архитектур поля. [[18]](http://allanmcrae.com/2014/12/pacman-4-2-released/) Однако, на момент 06.04.2016, [AurJson](/index.php/AurJson "AurJson") обьединяет все записи в одно поле: [FS#48796](https://bugs.archlinux.org/task/48796). Помощники, использующие RPC, могут использовать для получения зависимостей нижеследующие обходные пути:

*   [bauerbill](https://aur.archlinux.org/packages/bauerbill/) [[19]](https://bbs.archlinux.org/viewtopic.php?pid=1617235#p1617235), [pkgbuilder](https://aur.archlinux.org/packages/pkgbuilder/) [[20]](https://github.com/Kwpolska/pkgbuilder/blob/65d9d74ef05f8996b81afb1cd005e3c337afa8b2/pkgbuilder/build.py#L198): Получение конкретных полей из [.SRCINFO](/index.php/.SRCINFO ".SRCINFO")
*   [aurutils](https://aur.archlinux.org/packages/aurutils/) [[21]](https://github.com/AladW/aurutils/issues/80), [pacaur](https://aur.archlinux.org/packages/pacaur/) [[22]](https://github.com/rmarquis/pacaur/issues/465), [trizen](https://aur.archlinux.org/packages/trizen/) [[23]](https://github.com/trizen/trizen/commit/6a8ff9dc8cc83af783b8475dfbe89988dbc8a553): Убрать префикс `lib32-` на системах `i686`