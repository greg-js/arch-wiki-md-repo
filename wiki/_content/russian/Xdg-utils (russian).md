**Состояние перевода:** На этой странице представлен перевод статьи [xdg-utils](/index.php/Xdg-utils "Xdg-utils"). Дата последней синхронизации: 25 апреля 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Xdg-utils&diff=0&oldid=518645).

[xdg-utils](https://www.freedesktop.org/wiki/Software/xdg-utils/) ([xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils)) предоставляет официальные утилиты для управления [XDG приложениями MIME](/index.php/XDG_MIME_Applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "XDG MIME Applications (Русский)").

*   [xdg-desktop-menu(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-desktop-menu.1) - Установка элементов меню рабочего стола
*   [xdg-desktop-icon(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-desktop-icon.1) - Копирование [ярлыков приложений](/index.php/%D0%AF%D1%80%D0%BB%D1%8B%D0%BA%D0%B8_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9 "Ярлыки приложений") на рабочий стол пользователя
*   [xdg-email(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-email.1) - Открытие предпочитаемого пользователем клиента электронной почты (с возможностью указания темы и других параметров создаваемого сообщения)
*   [xdg-icon-resource(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-icon-resource.1) - Установка ресурсов значков
*   [xdg-mime(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-mime.1) - Запрос и установка типов и ассоциаций MIME
*   [xdg-open(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-open.1) - Открытие файла или URI в предпочтительном приложении пользователя
*   [xdg-screensaver(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-screensaver.1) - разрешение, запрещение или приостановка хранителя экрана
*   [xdg-settings(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-settings.1) - Установка по умолчанию веб-браузера и обработчиков URL-адресов

## xdg-mime

Для получения дополнительной информации смотрите [xdg-mime(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-mime.1).

Определение типа MIME файла:

```
$ xdg-mime query filetype photo.jpeg
image/jpeg

```

Определение приложения по умолчанию для типа MIME:

```
$ xdg-mime query default image/jpeg
gimp.desktop

```

Изменение приложения по умолчанию для типа MIME:

```
$ xdg-mime default feh.desktop image/jpeg

```

## xdg-open

xdg-open - [открыватель ресурсов](/index.php/Resource_opener "Resource opener"), который реализует [XDG MIME Applications (Русский)](/index.php/XDG_MIME_Applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "XDG MIME Applications (Русский)") и используется многими программами, для получения информации о использование смотрите [xdg-open(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-open.1).

xdg-open - не зависящий от окружения рабочего стола, в том смысле, что он пытается использовать по умолчанию родной инструмент каждого окружения.

Если окружение рабочего стола не обнаружено, обнаружение типа MIME возвращается к использованию [file](https://www.archlinux.org/packages/?name=file) который—по иронии судьбы—не реализует стандарт XDG. Если вы хотите, чтобы xdg-open использовал [XDG MIME Applications (Русский)](/index.php/XDG_MIME_Applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "XDG MIME Applications (Русский)") без окружения рабочего стола, вам необходимо [установить](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C "Установить") [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) или использовать один из [открывателей ресурсов](/index.php/Resource_opener "Resource opener"), которые поддерживают [XDG MIME Applications (Русский)](/index.php/XDG_MIME_Applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "XDG MIME Applications (Русский)").

## xdg-settings

Для получения дополнительной информации смотрите [xdg-settings(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-settings.1).

Ярлык для открытия всех веб типов MIME с помощью одного приложения:

```
$ xdg-settings set default-web-browser firefox.desktop

```

Ярлык для установки приложения по умолчанию для схемы URL:

```
$ xdg-settings set default-url-scheme-handler irc xchat.desktop

```