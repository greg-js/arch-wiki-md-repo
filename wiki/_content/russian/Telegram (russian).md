**Состояние перевода:** На этой странице представлен перевод статьи [Telegram](/index.php/Telegram "Telegram"). Дата последней синхронизации: 5 января 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Telegram&diff=0&oldid=561769).

[Telegram](https://en.wikipedia.org/wiki/ru:Telegram "wikipedia:ru:Telegram") — облачный кроссплатформенный мессенджер с опциональным end-to-end шифрованием. Для создания аккаунта требуется номер телефона.

Хотя официальные приложения и имеют открытый исходный код, они обновляются не сразу же после выхода новых версий приложений. Серверная часть Telegram является проприетарной.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
    *   [1.1 Плагины для других приложений](#Плагины_для_других_приложений)
    *   [1.2 Графические приложения](#Графические_приложения)
    *   [1.3 Приложения для терминала](#Приложения_для_терминала)
    *   [1.4 Web-приложения](#Web-приложения)
*   [2 Советы и рекомендации](#Советы_и_рекомендации)
    *   [2.1 Ресурсы в Telegram про Arch Linux](#Ресурсы_в_Telegram_про_Arch_Linux)
    *   [2.2 Счётчик непрочитанных сообщений для Telegram Desktop](#Счётчик_непрочитанных_сообщений_для_Telegram_Desktop)

## Установка

Вы можете использовать Telegram в Arch Linux одним из способов ниже:

### Плагины для других приложений

*   При использовании пакетов [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) или [telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/) подключиться к Telegram можно из приложений, основанных на [libpurple](https://www.archlinux.org/packages/?name=libpurple), к примеру, [Pidgin](/index.php/Pidgin_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pidgin (Русский)").
*   В приложениях на основе [Telepathy](https://en.wikipedia.org/wiki/ru:Telepathy "wikipedia:ru:Telepathy") (к примеру, [empathy](https://www.archlinux.org/packages/?name=empathy), мессенджер по умолчанию в [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)")) можно использовать пакет [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze) с совместимостью с [libpurple](https://www.archlinux.org/packages/?name=libpurple), а затем [telegram-purple](https://aur.archlinux.org/packages/telegram-purple/) для подключения к Telegram.
*   В [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)") можно использовать [telepathy-morse](https://www.archlinux.org/packages/?name=telepathy-morse) для добавления поддержки Telegram в мессенджер по умолчанию.

### Графические приложения

[Официальное приложение](https://desktop.telegram.org/):

*   [telegram-desktop](https://www.archlinux.org/packages/?name=telegram-desktop) — официальное приложение (сборка от команды Arch Linux).
*   [telegram-desktop-bin](https://aur.archlinux.org/packages/telegram-desktop-bin/) — официальное приложение (сборка от команды Telegram).
*   [telegram-desktop-systemqt-notoemoji](https://aur.archlinux.org/packages/telegram-desktop-systemqt-notoemoji/) — экспериментальная сборка Telegram Desktop, использующая системные библиотеки Qt вместо встроенных и emoji от [Noto Color Emoji](https://github.com/googlei18n/noto-emoji).

### Приложения для терминала

*   [telegram-cli-git](https://aur.archlinux.org/packages/telegram-cli-git/) — позволяет использовать Telegram при помощи командной строки. Для получения дополнительной информации о программе обратитесь к официальной странице на [Github](https://github.com/vysheng/tg).

*   [nctelegram-git](https://aur.archlinux.org/packages/nctelegram-git/) — основанный на [Ncurses](https://en.wikipedia.org/wiki/ru:ncurses "wikipedia:ru:ncurses") клиент для командной строки, требует [telegram-cli-git](https://aur.archlinux.org/packages/telegram-cli-git/). Для получения дополнительной информации о программе обратитесь к официальной странице на [Github](https://github.com/Nanoseb/ncTelegram).

### Web-приложения

*   Официальный [Telegram Web](https://web.telegram.org).
*   [franz](https://aur.archlinux.org/packages/franz/) — веб-приложение с открытым исходным кодом, предоставляющее доступ к различным мессенджерам, таким как [Telegram](https://en.wikipedia.org/wiki/ru:Telegram "wikipedia:ru:Telegram"), [WhatsApp](https://en.wikipedia.org/wiki/ru:WhatsApp "wikipedia:ru:WhatsApp"), [Facebook](https://en.wikipedia.org/wiki/ru:Facebook "wikipedia:ru:Facebook") и другим.
*   [rambox-bin](https://aur.archlinux.org/packages/rambox-bin/) — альтернатива Franz с открытым исходным кодом, предоставляет все его возможности.
*   Дополнение [Telegram Desktop](https://addons.mozilla.org/ru/firefox/addon/telegram-desktop/) для [Firefox](/index.php/Firefox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Firefox (Русский)") — позволяет общаться в Telegram из браузера.
*   Приложение [Telegram Chrome app](https://telegram.org/dl/webogram/chromeapp) для [Chromium](/index.php/Chromium_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Chromium (Русский)") — позволяет общаться в Telegram из браузера.

## Советы и рекомендации

### Ресурсы в Telegram про Arch Linux

*   [archlinux_ru](https://t.me/archlinux_ru) — неофициальная группа русскоговорящего сообщества Arch Linux.
*   [Arch Linux RU](https://t.me/ArchLinuxChatRU) — неофициальная группа сообщества Arch Linux в СНГ.
*   [Arch Linux](https://t.me/archlinuxgroup) — неофициальная группа для обсуждения всего о Arch Linux (на английском).
*   [ArchWikiBot](https://t.me/archewikibot) — встроенный бот для поиска в ArchWiki.
*   [Planet Arch Linux & News](https://t.me/planetarch) — канал с последними публикациями Planet Arch и новостями с сайта Arch Linux.
*   [Arch Linux: Recent package updates](https://t.me/archlinux_updates) — канал с последними обновлениями пакетов в репозиториях Arch Linux.
*   [Arch Linux News](https://t.me/archlinuxnews) — канал с последними новостями с официального сайта Arch Linux (*не обновляется*).
*   [Planet Arch](https://t.me/archplanet) — канал с последними публикациями с сайта Planet Arch *(не обновляется)*.

### Счётчик непрочитанных сообщений для Telegram Desktop

По умолчанию, количество непрочитанных сообщений будет отображаться только на иконке Telegram Desktop в системном трее. Если же вы хотите также включить счётчик непосредственно на иконке самого приложения, можно задействовать интеграцию значков Unity, которая поддерживается как в GNOME, так и в KDE Plasma. Для этого нужно установить [libunity](https://aur.archlinux.org/packages/libunity/) и запустить Telegram Desktop с переменной окружения `XDG_CURRENT_DESKTOP` со значением `Unity`. Например, скопируйте файл `.desktop` в `~/.local/share/applications/` и измените строку `Exec` для запуска Telegram Desktop с вышеуказанной переменной окружения.