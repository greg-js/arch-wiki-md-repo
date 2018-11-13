**翻译状态：** 本文是英文页面 [Telegram](/index.php/Telegram "Telegram") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-05-06，点击[这里](https://wiki.archlinux.org/index.php?title=Telegram&diff=0&oldid=474872)可以查看翻译后英文页面的改动。

部分内容来自[维基百科](https://zh.wikipedia.org/wiki/Telegram): Telegram Messenger是一个跨平台的实时通信软件，它的客户端是自由及开放源代码软件，但是它的服务器是专有软件。用户可以相互交换加密与自析构的消息，以及照片、视频、文件，支持所有的文件类型。官方网站有正式发布Android、iOS、Mac OS X与正在Beta的Windows Phone的版本；其他版本皆为非正式的版本，而且是由独立研发人员利用官方的应用程序接口来开发的。

## Contents

*   [1 安装](#安装)
    *   [1.1 作为其它聊天软件的插件](#作为其它聊天软件的插件)
    *   [1.2 图形界面应用程序](#图形界面应用程序)
    *   [1.3 终端应用](#终端应用)
    *   [1.4 网页应用](#网页应用)
*   [2 提示和技巧](#提示和技巧)
    *   [2.1 关于 Arch Linux 的 Telegram 频道](#关于_Arch_Linux_的_Telegram_频道)

## 安装

在 Arch Linux 上，你可以这样使用 Telegram:

### 作为其它聊天软件的插件

*   [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) 或 [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/) 为基于 [libpurple](https://www.archlinux.org/packages/?name=libpurple) 的聊天软件 （例如 [Pidgin](/index.php/Pidgin "Pidgin") ） 提供了支持。
*   基于 [Telepathy](https://en.wikipedia.org/wiki/Telepathy_(software) （例如 GNOME 的 [empathy](https://www.archlinux.org/packages/?name=empathy)）的软件可以使用 [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze)，它提供了对 [libpurple](https://www.archlinux.org/packages/?name=libpurple) 的支持。
*   [KDE](/index.php/KDE "KDE") 用户可以使用 [telepathy-morse](https://www.archlinux.org/packages/?name=telepathy-morse) 将默认聊天程序设置为 Telegram。

### 图形界面应用程序

[官方桌面版客户端](https://desktop.telegram.org/):

*   [telegram-desktop-bin](https://aur.archlinux.org/packages/telegram-desktop-bin/) ：来自上游的预编译版本。
*   [telegram-desktop](https://www.archlinux.org/packages/?name=telegram-desktop) ：需要同时编译 Qt。
*   [telegram-desktop-systemqt](https://aur.archlinux.org/packages/telegram-desktop-systemqt/) ：使用系统 Qt 的实验性版本。
*   [telegram-desktop-systemqt-notoemoji](https://aur.archlinux.org/packages/telegram-desktop-systemqt-notoemoji/) 使用系统 Qt 并替换 Emoji 为 [Noto Color Emoji](https://github.com/googlei18n/noto-emoji) 的实验性版本。
*   [telegram-desktop-systemqt-emojione](https://aur.archlinux.org/packages/telegram-desktop-systemqt-emojione/) 使用系统 Qt 并替换 Emoji 为 [Emoji One](https://emojione.com) 的实验性版本。

其它非官方客户端:

*   [cutegram](https://aur.archlinux.org/packages/cutegram/), 由 [aseman](http://aseman.co/en/products/cutegram) 开发，基于 [Qt](/index.php/Qt "Qt") 但是与官方客户端设计不同。安装 [cutegram-git](https://aur.archlinux.org/packages/cutegram-git/) 获得最新的开发版本。

### 终端应用

*   [telegram-cli-git](https://aur.archlinux.org/packages/telegram-cli-git/) 提供在终端连接和使用 Telegram 的界面 [这个项目的详细信息可以在 Github 上找到](https://github.com/vysheng/tg).

*   [nctelegram-git](https://aur.archlinux.org/packages/nctelegram-git/) 是基于 [Ncurses](https://en.wikipedia.org/wiki/Ncurses "wikipedia:Ncurses") 的客户端，它也需要 [telegram-cli-git](https://aur.archlinux.org/packages/telegram-cli-git/) [这个项目的详细信息可以在 Github 上找到](https://github.com/Nanoseb/ncTelegram).

### 网页应用

*   [官方网页应用 Telegram Web](https://web.telegram.org).
*   [Firefox 的官方网页应用扩展](https://addons.mozilla.org/en-US/firefox/addon/telegram-desktop/) .
*   [Telegram Web 的 Chrome app](https://telegram.org/dl/webogram/chromeapp) .

## 提示和技巧

*   [telegram-desktop](https://www.archlinux.org/packages/?name=telegram-desktop) 需要下载 [qtbase-src](http://download.qt.io/official_releases/qt/5.7/5.7.0/submodules/qtbase-opensource-src-5.7.0.tar.xz) 来进行编译。
*   非官方用户仓库 [archlinuxcn](/index.php/Unofficial_user_repositories#archlinuxcn "Unofficial user repositories") 提供几个预编译的 AUR 上 Telegram 客户端的软件包，例如 [telegram-desktop](https://www.archlinux.org/packages/?name=telegram-desktop) ，[telegram-desktop-systemqt](https://aur.archlinux.org/packages/telegram-desktop-systemqt/)，[telegram-desktop-systemqt-notoemoji](https://aur.archlinux.org/packages/telegram-desktop-systemqt-notoemoji/)。

### 关于 Arch Linux 的 Telegram 频道

*   [Arch Linux News](https://telegram.me/archlinuxnews) - 来自 Arch Linux 官方网站的最新消息.
*   [Planet Arch](https://telegram.me/archplanet) - 来自 Planet Arch 的最新消息.