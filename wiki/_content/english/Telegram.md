[Telegram](https://en.wikipedia.org/wiki/Telegram_(service) is a cloud-based cross-platform instant messaging service with optional end-to-end encryption. Account creation requires a phone number.

The official clients are open-source but the code for recent versions is not always immediately published. The server-side code is proprietary.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Chat client plugins](#Chat_client_plugins)
    *   [1.2 Graphical clients](#Graphical_clients)
    *   [1.3 Command-line clients](#Command-line_clients)
    *   [1.4 Web-based clients](#Web-based_clients)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Telegram channels about Arch Linux](#Telegram_channels_about_Arch_Linux)
    *   [2.2 Unread messages counter for Telegram Desktop](#Unread_messages_counter_for_Telegram_Desktop)

## Installation

You can use one of following methods in order to use Telegram in Arch:

### Chat client plugins

*   By using [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) or [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/) packages, connection to Telegram through messenger softwares based on [libpurple](https://www.archlinux.org/packages/?name=libpurple) such as [Pidgin](/index.php/Pidgin "Pidgin") is provided.
*   Messaging apps that are using [Telepathy](https://en.wikipedia.org/wiki/Telepathy_(software) such as [empathy](https://www.archlinux.org/packages/?name=empathy) (the default messenger for [GNOME](/index.php/GNOME "GNOME")) can make use of [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze) package, which provides possibility of using [libpurple](https://www.archlinux.org/packages/?name=libpurple) and thus [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) to connect Telegram.
*   In the [KDE](/index.php/KDE "KDE") desktop environment using [telepathy-morse](https://www.archlinux.org/packages/?name=telepathy-morse) provides capability of connecting the default messenger to Telegram.

### Graphical clients

The [official app](https://desktop.telegram.org/):

*   [telegram-desktop](https://www.archlinux.org/packages/?name=telegram-desktop), built by Arch Linux
*   [telegram-desktop-bin](https://aur.archlinux.org/packages/telegram-desktop-bin/), built by upstream
*   [telegram-desktop-systemqt-notoemoji](https://aur.archlinux.org/packages/telegram-desktop-systemqt-notoemoji/) Experimental build of Telegram Desktop using system Qt and emojis replaced with those from [Noto Color Emoji](https://github.com/googlei18n/noto-emoji).

### Command-line clients

*   [telegram-cli-git](https://aur.archlinux.org/packages/telegram-cli-git/) provides command-line interface to connect and use Telegram. For more information about the program, visit the program page on [Github](https://github.com/vysheng/tg).

*   [nctelegram-git](https://aur.archlinux.org/packages/nctelegram-git/) is a command-line interface for Telegram based on [Ncurses](https://en.wikipedia.org/wiki/Ncurses "wikipedia:Ncurses") and needs [telegram-cli-git](https://aur.archlinux.org/packages/telegram-cli-git/) to run. For more information about the program, visit the program page on [Github](https://github.com/Nanoseb/ncTelegram).

### Web-based clients

*   The official [Telegram Web](https://web.telegram.org).
*   [franz](https://aur.archlinux.org/packages/franz/) is an open-source web-based application that can be used for web-based interface of various instant messaging software such as [Telegram](https://en.wikipedia.org/wiki/Telegram_(service) "wikipedia:Telegram (service)"), [WhatsApp](https://en.wikipedia.org/wiki/WhatsApp "wikipedia:WhatsApp"), [Facebook](https://en.wikipedia.org/wiki/Facebook "wikipedia:Facebook"), and more.
*   [rambox-bin](https://aur.archlinux.org/packages/rambox-bin/) is an open source alternative to Franz. It offers all features of its closed source counterpart.
*   Use [Telegram Desktop](https://addons.mozilla.org/en-US/firefox/addon/telegram-desktop/) addons for [Firefox](/index.php/Firefox "Firefox"), to connect to Telegram in your browser via web interface.
*   Use [Telegram Chrome app](https://telegram.org/dl/webogram/chromeapp) for [Chromium](/index.php/Chromium "Chromium"), to connect to Telegram in your browser via web interface.

## Tips and tricks

### Telegram channels about Arch Linux

*   [Arch Linux News](https://telegram.me/archlinuxnews) - Latest news form Arch web site.
*   [Planet Arch](https://telegram.me/archplanet) - Latest posts from Planet Arch web site.
*   [Arch Linux](https://telegram.me/archlinuxgroup) - Unofficial group for discussing everything about Arch Linux.

### Unread messages counter for Telegram Desktop

By default, only the icon in the system tray will show the number of unread messages. If you want to have the actual app icon to show the unread message counter as well, you can use the Unity badge integration, which can be handled by KDE and Gnome as well. To enable the Unity integration, you will have to install [libunity](https://aur.archlinux.org/packages/libunity/) and start Telegram Desktop with the `XDG_CURRENT_DESKTOP` environment variable set to `Unity`, e.g. copy the `.desktop` file to `~/.local/share/applications/` and change the `Exec` line to start Telegram Desktop with the environment variable set instead.