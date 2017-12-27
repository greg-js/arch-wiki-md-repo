From [Wikipedia](https://en.wikipedia.org/wiki/Telegram_(software) "wikipedia:Telegram (software)"): **Telegram** is a cloud-based instant messaging service. Telegram clients exist for both mobile (Android, iOS, Windows Phone, Ubuntu Touch) and desktop systems (Windows, OS X, Linux). Users can send messages and exchange photos, videos, stickers and files of any type. Telegram also provides optional end-to-end-encrypted messaging.

The official clients are open-source but the code for recent versions is not always immediately published. The server-side code is closed-source and proprietary.

## Contents

*   [1 Install](#Install)
    *   [1.1 Plugin for other chat software](#Plugin_for_other_chat_software)
    *   [1.2 GUI/graphical application](#GUI.2Fgraphical_application)
    *   [1.3 CLI/command line application](#CLI.2Fcommand_line_application)
    *   [1.4 Web application](#Web_application)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Telegram channels about Arch Linux](#Telegram_channels_about_Arch_Linux)

## Install

You can use one of following methods in order to use Telegram in Arch:

### Plugin for other chat software

*   By using [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) or [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/) packages, connection to Telegram through messenger softwares based on [libpurple](https://www.archlinux.org/packages/?name=libpurple) such as [Pidgin](/index.php/Pidgin "Pidgin") is provided.
*   Messaging apps that are using [Telepathy](https://en.wikipedia.org/wiki/Telepathy_(software) such as [empathy](https://www.archlinux.org/packages/?name=empathy) (the default messenger for [GNOME](/index.php/GNOME "GNOME")) can make use of [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze) package, which provides possibility of using [libpurple](https://www.archlinux.org/packages/?name=libpurple) and thus [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) to connect Telegram.
*   In the [KDE](/index.php/KDE "KDE") desktop environment using [telepathy-morse](https://www.archlinux.org/packages/?name=telepathy-morse) provides capability of connecting the default messenger to Telegram.

### GUI/graphical application

The [official app](https://desktop.telegram.org/):

*   [telegram-desktop-bin](https://aur.archlinux.org/packages/telegram-desktop-bin/) pre-compiled binary from [Telegram](https://desktop.telegram.org/).
*   [telegram-desktop](https://www.archlinux.org/packages/?name=telegram-desktop) that needs [Qt](/index.php/Qt "Qt") libraries to be compiled.
*   [telegram-desktop-systemqt](https://aur.archlinux.org/packages/telegram-desktop-systemqt/) Experimental build of Telegram Desktop using system Qt instead of Telegram custom Qt libraries.
*   [telegram-desktop-systemqt-notoemoji](https://aur.archlinux.org/packages/telegram-desktop-systemqt-notoemoji/) Experimental build of Telegram Desktop using system Qt and emojis replaced with those from [Noto Color Emoji](https://github.com/googlei18n/noto-emoji).

Alternative unofficial clients:

*   [cutegram](https://aur.archlinux.org/packages/cutegram/), open-source client by Iranian developer [aseman](http://aseman.co/en/products/cutegram). The package is based on [Qt](/index.php/Qt "Qt") and has different capabilities from pure Telegram. Install [cutegram-git](https://aur.archlinux.org/packages/cutegram-git/) for latest development version.

### CLI/command line application

*   [telegram-cli-git](https://aur.archlinux.org/packages/telegram-cli-git/) provides command-line interface to connect and use Telegram. For more information about the program, visit the program page on [Github](https://github.com/vysheng/tg).

*   [nctelegram-git](https://aur.archlinux.org/packages/nctelegram-git/) is a command-line interface for Telegram based on [Ncurses](https://en.wikipedia.org/wiki/Ncurses "wikipedia:Ncurses") and needs [telegram-cli-git](https://aur.archlinux.org/packages/telegram-cli-git/) to run. For more information about the program, visit the program page on [Github](https://github.com/Nanoseb/ncTelegram).

### Web application

*   The official [Telegram Web](https://web.telegram.org).
*   [franz](https://aur.archlinux.org/packages/franz/) is an open-source web-based application that can be used for web-based interface of various instant messaging software such as [Telegram](https://en.wikipedia.org/wiki/Telegram "wikipedia:Telegram"), [WhatsApp](https://en.wikipedia.org/wiki/WhatsApp "wikipedia:WhatsApp"), [Facebook](https://en.wikipedia.org/wiki/Facebook "wikipedia:Facebook"), and more.
*   [rambox-bin](https://aur.archlinux.org/packages/rambox-bin/) is an open source alternative to Franz. It offers all features of its closed source counterpart.
*   Use [Telegram Desktop](https://addons.mozilla.org/en-US/firefox/addon/telegram-desktop/) addons for [Firefox](/index.php/Firefox "Firefox"), to connect to Telegram in your browser via web interface.
*   Use [Telegram Chrome app](https://telegram.org/dl/webogram/chromeapp) for [Chromium](/index.php/Chromium "Chromium"), to connect to Telegram in your browser via web interface.

## Tips and tricks

*   [telegram-desktop](https://www.archlinux.org/packages/?name=telegram-desktop) package need to download [qtbase-src](http://download.qt.io/official_releases/qt/5.7/5.7.0/submodules/qtbase-opensource-src-5.7.0.tar.xz) file to compile. This requires approximately 40 MB to download for building package.
*   Use unofficial repository [archlinuxcn](/index.php/Unofficial_user_repositories#archlinuxcn "Unofficial user repositories") to install packages [telegram-desktop](https://www.archlinux.org/packages/?name=telegram-desktop) and [telegram-desktop-bin](https://aur.archlinux.org/packages/telegram-desktop-bin/) in which case there is no need to download [qtbase-src](http://download.qt.io/official_releases/qt/5.7/5.7.0/submodules/qtbase-opensource-src-5.7.0.tar.xz) file, mentioned in the previous point for making [telegram-desktop](https://www.archlinux.org/packages/?name=telegram-desktop). Some other related packages for Telegram can also be found in this repository.

### Telegram channels about Arch Linux

*   [Arch Linux News](https://telegram.me/archlinuxnews) - Latest news form Arch web site.
*   [Planet Arch](https://telegram.me/archplanet) - Latest posts from Planet Arch web site.