**Состояние перевода:** На этой странице представлен перевод статьи [Telegram](/index.php/Telegram "Telegram"). Дата последней синхронизации: 12 декабря 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Telegram&diff=0&oldid=497975).

Из [Wikipedia](https://en.wikipedia.org/wiki/Telegram_(software) "wikipedia:Telegram (software)"): **Telegram** — бесплатный кроссплатформенный мессенджер для смартфонов и других устройств, позволяющий обмениваться текстовыми сообщениями и медиафайлами различных форматов. Используются проприетарная серверная часть c закрытым кодом и несколько клиентов с открытым исходным кодом, в том числе под лицензией GNU GPL.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Плагины для других приложений](#.D0.9F.D0.BB.D0.B0.D0.B3.D0.B8.D0.BD.D1.8B_.D0.B4.D0.BB.D1.8F_.D0.B4.D1.80.D1.83.D0.B3.D0.B8.D1.85_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [1.2 GUI/графические приложения](#GUI.2F.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [1.3 CLI/приложения для терминала](#CLI.2F.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B4.D0.BB.D1.8F_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B0)
    *   [1.4 Web-приложения](#Web-.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
*   [2 Советы и хитрости](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.85.D0.B8.D1.82.D1.80.D0.BE.D1.81.D1.82.D0.B8)
    *   [2.1 Каналы в Telegram про Arch Linux](#.D0.9A.D0.B0.D0.BD.D0.B0.D0.BB.D1.8B_.D0.B2_Telegram_.D0.BF.D1.80.D0.BE_Arch_Linux)

## Установка

Вы можете использовать Telegram в Arch одним из способов ниже:

### Плагины для других приложений

*   При использовании пакетов [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) или [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/) подключиться к Telegram можно из приложений, основанных на [libpurple](https://www.archlinux.org/packages/?name=libpurple), к примеру, [Pidgin](/index.php/Pidgin_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pidgin (Русский)").
*   В приложениях на основе [Telepathy](https://en.wikipedia.org/wiki/Telepathy_(software) (к примеру, [empathy](https://www.archlinux.org/packages/?name=empathy), мессенджер по умолчанию в [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)")) можно использовать пакет [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze) с совместимостью с [libpurple](https://www.archlinux.org/packages/?name=libpurple), а затем [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) для подключения к Telegram.
*   В [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)") можно использовать [telepathy-morse](https://www.archlinux.org/packages/?name=telepathy-morse) для добавления поддержки Telegram в мессенджер по умолчанию.

### GUI/графические приложения

[Официальное приложение](https://desktop.telegram.org/):

*   [telegram-desktop-bin](https://aur.archlinux.org/packages/telegram-desktop-bin/) скомпилированное приложение от [Telegram](https://desktop.telegram.org/).
*   [telegram-desktop](https://www.archlinux.org/packages/?name=telegram-desktop) требующее библиотеки [Qt](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)") для сборки.
*   [telegram-desktop-systemqt](https://aur.archlinux.org/packages/telegram-desktop-systemqt/) экспериментальная сборка Telegram Desktop, использующая системные библиотеки Qt вместо встроенных.
*   [telegram-desktop-systemqt-notoemoji](https://aur.archlinux.org/packages/telegram-desktop-systemqt-notoemoji/) экспериментальная сборка Telegram Desktop, использующая системные библиотеки Qt вместо встроенных и emoji от [Noto Color Emoji](https://github.com/googlei18n/noto-emoji).
*   [telegram-desktop-systemqt-emojione](https://aur.archlinux.org/packages/telegram-desktop-systemqt-emojione/) экспериментальная сборка Telegram Desktop, использующая системные библиотеки Qt вместо встроенных и emoji от [EmojiOne](https://emojione.com/).

Альтернативные неофициальные клиенты:

*   [cutegram](https://aur.archlinux.org/packages/cutegram/), клиент с открытым исходным кодом от иранского разработчика [aseman](http://aseman.co/en/products/cutegram). Пакет использует [Qt](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)") и отличается от официального клиента возможностями. Для последней разрабатываемой версии установите пакет [cutegram-git](https://aur.archlinux.org/packages/cutegram-git/).

### CLI/приложения для терминала

*   [telegram-cli-git](https://aur.archlinux.org/packages/telegram-cli-git/) позволяет использовать Telegram при помощи командной строки. Для дополнительной информации о программе обратитесь к официальной странице на [Github](https://github.com/vysheng/tg).

*   [nctelegram-git](https://aur.archlinux.org/packages/nctelegram-git/) основанный на [Ncurses](https://en.wikipedia.org/wiki/Ncurses "wikipedia:Ncurses") клиент для командной строки, требует [telegram-cli-git](https://aur.archlinux.org/packages/telegram-cli-git/). Для дополнительной информации о программе обратитесь к официальной странице на [Github](https://github.com/Nanoseb/ncTelegram).

### Web-приложения

*   Официальный [Telegram Web](https://web.telegram.org).
*   [franz](https://aur.archlinux.org/packages/franz/) веб-приложение с открытым исходным кодом, предоставляющее доступ к различным мессенджерам, таким как [Telegram](https://en.wikipedia.org/wiki/Telegram "wikipedia:Telegram"), [WhatsApp](https://en.wikipedia.org/wiki/WhatsApp "wikipedia:WhatsApp"), [Facebook](https://en.wikipedia.org/wiki/Facebook "wikipedia:Facebook") и другим.
*   [rambox-bin](https://aur.archlinux.org/packages/rambox-bin/) альтернатива Franz с открытым исходным кодом, предоставляет все его возможности.
*   Аддон [Telegram Desktop](https://addons.mozilla.org/ru/firefox/addon/telegram-desktop/) для [Firefox](/index.php/Firefox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Firefox (Русский)"), позволяет общаться в Telegram из браузера.
*   Приложение [Telegram Chrome app](https://telegram.org/dl/webogram/chromeapp) для [Chromium](/index.php/Chromium_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Chromium (Русский)"), позволяет общаться в Telegram из браузера.

## Советы и хитрости

*   Пакет [telegram-desktop](https://www.archlinux.org/packages/?name=telegram-desktop) требует для сборки [qtbase-src](http://download.qt.io/official_releases/qt/5.7/5.7.0/submodules/qtbase-opensource-src-5.7.0.tar.xz), а это около 40MB дополнительных загрузок.
*   Использование неофициального репозитория [archlinuxcn](/index.php/Unofficial_user_repositories#archlinuxcn "Unofficial user repositories") для установки [telegram-desktop](https://www.archlinux.org/packages/?name=telegram-desktop) и [telegram-desktop-bin](https://aur.archlinux.org/packages/telegram-desktop-bin/) позволяет не загружать [qtbase-src](http://download.qt.io/official_releases/qt/5.7/5.7.0/submodules/qtbase-opensource-src-5.7.0.tar.xz), упомянутый выше. Некоторые другие связанные с Telegram пакеты также доступны в этом репозитории.

### Каналы в Telegram про Arch Linux

*   [Arch Linux News](https://telegram.me/archlinuxnews) - Последние новости с официального сайта Arch (на английском).
*   [Planet Arch](https://telegram.me/archplanet) - Последние публикации с сайта Planet Arch (на английском).
*   [Arch Linux RU & UA](https://telegram.me/ArchLinuxChatRU) - Неофициальный чат сообщества ArchLinux в СНГ.