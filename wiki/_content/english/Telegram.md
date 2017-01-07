From [Wikipedia](https://en.wikipedia.org/wiki/Telegram_(software) "wikipedia:Telegram (software)"): **Telegram** is a cloud-based instant messaging service. Telegram clients exist for both mobile (Android, iOS, Windows Phone, Ubuntu Touch) and desktop systems (Windows, OS X, Linux). Users can send messages and exchange photos, videos, stickers and files of any type. Telegram also provides optional end-to-end-encrypted messaging.

## Contents

*   [1 Install](#Install)
    *   [1.1 Using available messaging software and adding capability of connecting to Telegram to them](#Using_available_messaging_software_and_adding_capability_of_connecting_to_Telegram_to_them)
    *   [1.2 Using GUI and desktop applications for Telegram](#Using_GUI_and_desktop_applications_for_Telegram)
    *   [1.3 Telegram applications for the command line and CLI environment](#Telegram_applications_for_the_command_line_and_CLI_environment)
    *   [1.4 Using the Web-based version of Telegram](#Using_the_Web-based_version_of_Telegram)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Telegram channels about Arch Linux](#Telegram_channels_about_Arch_Linux)

## Install

You can use one of following methods in order to use [Telegram](https://telegram.org/) in Arch:

### Using available messaging software and adding capability of connecting to Telegram to them

*   By using [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) or [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/) packages, connection to Telegram through messenger softwares based on [libpurple](https://www.archlinux.org/packages/?name=libpurple) such as [Pidgin](/index.php/Pidgin "Pidgin") is provided.
*   Messaging apps that are using [Telepathy](https://en.wikipedia.org/wiki/Telepathy "wikipedia:Telepathy") such as [empathy](https://www.archlinux.org/packages/?name=empathy) (the default messenger for [GNOME](/index.php/GNOME "GNOME")) can make use of [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze) package, which provides possibility of using [libpurple](https://www.archlinux.org/packages/?name=libpurple) and thus [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) to connect Telegram.
*   In the [KDE](/index.php/KDE "KDE") desktop environment using [telepathy-morse](https://www.archlinux.org/packages/?name=telepathy-morse) provides capability of connecting the default messenger to Telegram.

### Using GUI and desktop applications for Telegram

Available applications in order to use Telegram in graphical environment are divided into two categories:

1.  The official app from [Telegram](https://desktop.telegram.org/).
2.  Non-formal programs that are provided by others.

To install applications provided by Telegram, one can use the following packages:

*   [telegram-desktop-bin](https://aur.archlinux.org/packages/telegram-desktop-bin/) that has been compiled and is available on [Telegram](https://desktop.telegram.org/).
*   [telegram-desktop](https://aur.archlinux.org/packages/telegram-desktop/) that needs [Qt](/index.php/Qt "Qt") libraries to be compiled.

Unofficial other programs are as follows:

*   [cutegram](https://www.archlinux.org/packages/?name=cutegram) package exists in the Arch official repositories and many other Linux distributions and BSDs. This package has been created by Iranian programmers from [aseman](http://aseman.co/en/products/cutegram). The package is based on [Qt](/index.php/Qt "Qt") and has different capabilities from pure Telegram. Install [cutegram-git](https://aur.archlinux.org/packages/cutegram-git/) for latest development version install.

### Telegram applications for the command line and CLI environment

*   [telegram-cli-git](https://aur.archlinux.org/packages/telegram-cli-git/) provides command-line interface to connect and use Telegram. For more information about the program, visit the program page on [Github](https://github.com/vysheng/tg).

*   [nctelegram-git](https://aur.archlinux.org/packages/nctelegram-git/) is a command-line interface for Telegram based on [Ncurses](https://en.wikipedia.org/wiki/Ncurses "wikipedia:Ncurses") and needs [telegram-cli-git](https://aur.archlinux.org/packages/telegram-cli-git/) to run. For more information about the program, visit the program page on [Github](https://github.com/Nanoseb/ncTelegram).

### Using the Web-based version of Telegram

*   To use the web version of telegram, you can use your favorite internet browser for opening [webogram](https://telegram.org/dl/webogram) page and, after you have confirmed your account, you can use Telegram.
*   [franz-bin](https://aur.archlinux.org/packages/franz-bin/) is a closed-source web-based application that can be used for web-based interface of various instant messaging software such as [Telegram](https://en.wikipedia.org/wiki/Telegram "wikipedia:Telegram"), [WhatsApp](https://en.wikipedia.org/wiki/WhatsApp "wikipedia:WhatsApp"), [Facebook](https://en.wikipedia.org/wiki/Facebook "wikipedia:Facebook"), and more.
*   [rambox-bin](https://aur.archlinux.org/packages/rambox-bin/) is an open source alternative to Franz. It offers all features of its closed source counterpart.
*   Use [Telegram Desktop](https://addons.mozilla.org/en-US/firefox/addon/telegram-desktop/) addons for [Firefox](/index.php/Firefox "Firefox"), to connect to Telegram in your browser via web interface.
*   Use [Telegram Chrome app](https://telegram.org/dl/webogram/chromeapp) for [Chromium](/index.php/Chromium "Chromium"), to connect to Telegram in your browser via web interface.

## Tips and tricks

*   [telegram-desktop](https://aur.archlinux.org/packages/telegram-desktop/) package need to download [qtbase-src](http://download.qt.io/official_releases/qt/5.7/5.7.0/submodules/qtbase-opensource-src-5.7.0.tar.xz) file to compile. This requires approximately 40 MB to download for building package.
*   Use unofficial repository [archlinuxcn](/index.php/Unofficial_user_repositories#archlinuxcn "Unofficial user repositories") to install packages [telegram-desktop](https://aur.archlinux.org/packages/telegram-desktop/) and [telegram-desktop-bin](https://aur.archlinux.org/packages/telegram-desktop-bin/) in which case there is no need to download [qtbase-src](http://download.qt.io/official_releases/qt/5.7/5.7.0/submodules/qtbase-opensource-src-5.7.0.tar.xz) file, mentioned in the previous point for making [telegram-desktop](https://aur.archlinux.org/packages/telegram-desktop/). Some other related packages for Telegram can also be found in this repository.

### Telegram channels about Arch Linux

*   [Arch Linux News](https://telegram.me/archlinuxnews) - Latest news form Arch web site.
*   [Planet Arch](https://telegram.me/archplanet) - Latest posts from Planet Arch web site.