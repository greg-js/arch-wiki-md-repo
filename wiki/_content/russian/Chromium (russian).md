[Chromium](https://ru.wikipedia.org/wiki/Chromium) — графический веб-браузер с открытым исходным кодом, основанный на движке [Blink](https://en.wikipedia.org/wiki/ru:Blink_(%D0%B4%D0%B2%D0%B8%D0%B6%D0%BE%D0%BA) и разрабатываемый корпорацией Google совместно с сообществом и некоторыми другими корпорациями.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 32-битные системы без поддержки SSE2](#32-.D0.B1.D0.B8.D1.82.D0.BD.D1.8B.D0.B5_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B_.D0.B1.D0.B5.D0.B7_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B8_SSE2)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Chromium как браузер по умолчанию](#Chromium_.D0.BA.D0.B0.D0.BA_.D0.B1.D1.80.D0.B0.D1.83.D0.B7.D0.B5.D1.80_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [2.2 Ассоциации файлов](#.D0.90.D1.81.D1.81.D0.BE.D1.86.D0.B8.D0.B0.D1.86.D0.B8.D0.B8_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2)
    *   [2.3 Плагин Flash Player'a](#.D0.9F.D0.BB.D0.B0.D0.B3.D0.B8.D0.BD_Flash_Player.27a)
    *   [2.4 Плагин для просмотра файлов PDF](#.D0.9F.D0.BB.D0.B0.D0.B3.D0.B8.D0.BD_.D0.B4.D0.BB.D1.8F_.D0.BF.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80.D0.B0_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_PDF)
        *   [2.4.1 libpdf](#libpdf)
        *   [2.4.2 PDF.js](#PDF.js)
    *   [2.5 Сертификаты](#.D0.A1.D0.B5.D1.80.D1.82.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82.D1.8B)
*   [3 Разные полезности](#.D0.A0.D0.B0.D0.B7.D0.BD.D1.8B.D0.B5_.D0.BF.D0.BE.D0.BB.D0.B5.D0.B7.D0.BD.D0.BE.D1.81.D1.82.D0.B8)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 Частые зависания в KDE](#.D0.A7.D0.B0.D1.81.D1.82.D1.8B.D0.B5_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D1.8F_.D0.B2_KDE)
    *   [4.2 Звук, напоминающий треск](#.D0.97.D0.B2.D1.83.D0.BA.2C_.D0.BD.D0.B0.D0.BF.D0.BE.D0.BC.D0.B8.D0.BD.D0.B0.D1.8E.D1.89.D0.B8.D0.B9_.D1.82.D1.80.D0.B5.D1.81.D0.BA)
    *   [4.3 Рендеринг шрифтов в плагине PDF](#.D0.A0.D0.B5.D0.BD.D0.B4.D0.B5.D1.80.D0.B8.D0.BD.D0.B3_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.BE.D0.B2_.D0.B2_.D0.BF.D0.BB.D0.B0.D0.B3.D0.B8.D0.BD.D0.B5_PDF)
    *   [4.4 Принудительное 3D-ускорение в Flash Player и браузере](#.D0.9F.D1.80.D0.B8.D0.BD.D1.83.D0.B4.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D0.B5_3D-.D1.83.D1.81.D0.BA.D0.BE.D1.80.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2_Flash_Player_.D0.B8_.D0.B1.D1.80.D0.B0.D1.83.D0.B7.D0.B5.D1.80.D0.B5)
    *   [4.5 Ссылки "mailto" открываются в новых вкладках](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8_.22mailto.22_.D0.BE.D1.82.D0.BA.D1.80.D1.8B.D0.B2.D0.B0.D1.8E.D1.82.D1.81.D1.8F_.D0.B2_.D0.BD.D0.BE.D0.B2.D1.8B.D1.85_.D0.B2.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B0.D1.85)
    *   [4.6 Настройка прокси](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BF.D1.80.D0.BE.D0.BA.D1.81.D0.B8)
    *   [4.7 speech-dispatcher выдает дампы памяти](#speech-dispatcher_.D0.B2.D1.8B.D0.B4.D0.B0.D0.B5.D1.82_.D0.B4.D0.B0.D0.BC.D0.BF.D1.8B_.D0.BF.D0.B0.D0.BC.D1.8F.D1.82.D0.B8)
    *   [4.8 WebGL](#WebGL)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Проект с открытым исходным кодом, **Chromium**, можно [установить](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") с пакетом [chromium](https://www.archlinux.org/packages/?name=chromium). Помимо этого в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") можно найти:

*   [chromium-dev](https://aur.archlinux.org/packages/chromium-dev/) — версия для разработчиков (уже собранный двоичный пакет: [chromium-browser-bin](https://aur.archlinux.org/packages/chromium-browser-bin/))
*   [google-chrome](https://aur.archlinux.org/packages/google-chrome/) — модифицированный вариант, **Google Chrome**, включающий в себя Flash Player
*   [google-chrome-beta](https://aur.archlinux.org/packages/google-chrome-beta/) — бета-версия Google Chrome
*   [google-chrome-dev](https://aur.archlinux.org/packages/google-chrome-dev/) — версия Google Chrome для разработчиков

**Совет:** Чтобы получить дополнительную информацию о различиях между стабильными/бета/девелоперскими версиями, между Chromium и Chrome, а также разъяснения о порядке присвоения номеров для новых версий, смотрите эти [две](https://code.google.com/p/chromium/wiki/ChromiumBrowserVsGoogleChrome) [статьи](http://news.softpedia.com/news/Google-Chrome-vs-Chromium-Understanding-Stable-Beta-Dev-Releases-and-Version-No-140060.shtml)

### 32-битные системы без поддержки SSE2

Начиная с версии 35 из *chromium* [была удалена поддержка старого оборудования, не имеющего набор инструкций SSE2](https://code.google.com/p/chromium/issues/detail?id=348761#c15). Люди, которые используют такое оборудование, но по-прежнему желают пользоваться *chromium*, могут собрать пакет [chromium-no-sse2](https://aur.archlinux.org/packages/chromium-no-sse2/) или скачать уже скомпилированный пакет из [Repo-ck](/index.php/Repo-ck#Other_packages "Repo-ck"). При этом помните, что внедрение поддержки SSE2 устранило несколько ошибок, и, если вы используете патченную версию, не следует отправлять отчеты об ошибках в upstream.

## Настройка

### Chromium как браузер по умолчанию

Это настраивается в [xdg-open](/index.php/Xdg-open "Xdg-open"): смотрите раздел [xdg-open#Установка браузера по умолчанию](/index.php/Xdg-open#Set_the_default_browser "Xdg-open"). Больше информации на эту тему можно найти в статье [Приложения по умолчанию](/index.php/Default_applications "Default applications").

### Ассоциации файлов

Это настраивается в [xdg-open](/index.php/Xdg-open "Xdg-open"): смотрите раздел [xdg-open#Настройка](/index.php/Xdg-open#Configuration "Xdg-open"). Больше информации на эту тему можно найти в статье [Приложения по умолчанию](/index.php/Default_applications "Default applications").

### Плагин Flash Player'a

**Примечание:** В связи с тем, что Chromium больше не поддерживает Netscape plugin API (NPAPI), [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) из официальных репозиториев больше не работает

**pepper-flash** - это плагин, использующий новый Pepper API. Он разрабатывается в Adobe и входит в состав Google Chrome.

Установить pepper-flash для Chromium можно с пакетом [pepper-flash](https://aur.archlinux.org/packages/pepper-flash/) из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"). Если вы хотите использовать версию для разработчиков, установите [chromium-pepper-flash-dev](https://aur.archlinux.org/packages/chromium-pepper-flash-dev/).

Разрешите использование Flash тут `chrome://settings/content`.

### Плагин для просмотра файлов PDF

Существует несколько способов включения поддержки PDF в Chromium, которые описаны ниже.

#### libpdf

**libpdf** — собственная разработка Google для просмотра PDF файлов, которая включена в Chromium (начиная с версии 37) и в Google Chrome.

При обновлении с версии 36 до версии 37 необходимо [удалить](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") пакеты [chromium-libpdf](https://aur.archlinux.org/packages/chromium-libpdf/) и [chromium-libpdf-dev](https://aur.archlinux.org/packages/chromium-libpdf-dev/). Если плагин выключен, включите его на странице `chrome://plugins`.

#### PDF.js

Смотрите основную статью: [Плагины для браузеров#PDF.js](/index.php/Browser_plugins#PDF.js "Browser plugins").

### Сертификаты

Для работы с сертификатами Chromium использует [NSS](/index.php/Network_Security_Services_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Network Security Services (Русский)"). Управлять сертификатами можно, зайдя в `Настройки` → `Показать дополнительные настройки...` → `Управление сертификатами...`.

## Разные полезности

Смотрите основную статью: [Хитрости Chromium](/index.php/Chromium_tweaks "Chromium tweaks").

## Решение проблем

### Частые зависания в KDE

[Удалите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") пакет [libcanberra-pulse](https://www.archlinux.org/packages/?name=libcanberra-pulse). Смотрите ветку форума [BBS#1228558](https://bbs.archlinux.org/viewtopic.php?pid=1228558).

### Звук, напоминающий треск

Некоторые пользователи жалуются на треск вместо нормального звука при использовании Chromium и аудиовыхода HDMI. Для решения этой проблемы запускайте Chromium с изменённым размером буфера аудио:

```
$ chromium --audio-buffer-size=2048

```

### Рендеринг шрифтов в плагине PDF

Для корректного рендеринга шрифтов в PDF необходимо установить пакет [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation), иначе замещающий шрифт может вызывать наслоение букв друг на друга. Один из пользователей Arch создал [отчёт об ошибке на баг-трекере chromium](https://code.google.com/p/chromium/issues/detail?id=369991).

### Принудительное 3D-ускорение в Flash Player и браузере

**Важно:** Данное действие может стать причиной нестабильной работы браузера, включая аварийное завершение программы. Смотрите отчёты об ошибках на странице `chrome://gpu`

Для принудительного 3D графического ускорения необходимо включить опцию *Override software rendering list* на странице `chrome://flags`, предварительно корректно выставив значения переменных окружения и установив необходимые пакеты, как описано в статье [VDPAU](/index.php/VDPAU_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "VDPAU (Русский)").

Проверить, работает ли ускорение, можно на странице `chrome://gpu`.

### Ссылки "mailto" открываются в новых вкладках

Если вы не используете окружение рабочего стола, все ссылки "mailto" могут открываться в отдельном окне браузера, а не в вашем клиенте электронной почты по умолчанию. В этом случае необходимо отредактировать файл `/usr/bin/xdg-email`, настройки из которого считывает Chromium:

```
# sed 's/open_generic "${mailto}"/open_gnome "${mailto}"/' -i /usr/bin/xdg-email

```

Это необходимо делать после каждого обновления пакета [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils). Если вы не хотите заботиться об этом, установите пакет [xdg-utils-xdg-email-gnome](https://aur.archlinux.org/packages/xdg-utils-xdg-email-gnome/) или [xdg-utils-mimeo](https://aur.archlinux.org/packages/xdg-utils-mimeo/).

### Настройка прокси

По состоянию на июнь 2012 г. не редки ситуации, когда настройки прокси не работают правильно, особенно если для их настройки использовался интерфейс KDE. Работающее решение - воспользоваться для настройки прокси опциями командной строки Chromium, такими как `--proxy-auto-detect`, `--proxy-pac-url` и `--proxy-server`.

### speech-dispatcher выдает дампы памяти

**Примечание:** По этому поводу создан баг-репорт [FS#38456](https://bugs.archlinux.org/task/38456)

Chromium устанавливает пакет [speech-dispatcher](https://www.archlinux.org/packages/?name=speech-dispatcher) в качестве зависимости. Это независимый слой для интерфейса синтезирования речи, по умолчанию он использует бэкенд [festival](https://www.archlinux.org/packages/?name=festival). Если вы часто получаете дампы памяти, скорее всего, у вас не установлен festival. Чтобы решить эту проблему, либо установите festival, либо измените бэкенд, который использует speech-dispatcher.

### WebGL

Иногда Chromium выключает WebGL из-за определённых конфигураций видеокарты. Это может быть исправлено деактивировав пункт *Disable WebGL* на странице `chrome://flags` либо запуском браузера с опцией командной строки `--enable-webgl`.

Есть также вероятность, что ваша видеокарта занесена в чёрный список Chromium. Что бы обойти ограничение, на странице `chrome://flags` активируйте пункт *Override software rendering list* либо запускайте браузер с опцией командной строки `--ignore-gpu-blacklist`.

Если вы запускаете Chromium через [Bumblebee](/index.php/Bumblebee_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bumblebee (Русский)"), WebGL может работать нестабильно из-за того, что видеокарта работает в песочнице. В этом случае, необходимо выключить песочницу для видеокарты запустив Chromium с опцией командной строки `--disable-gpu-sandbox`:

 `optirun chromium --disable-gpu-sandbox` 

## Смотрите также

*   [Официальный сайт Chromium](http://www.chromium.org/Home)
*   [Примечания к релизам Google Chrome](http://googlechromereleases.blogspot.com)
*   [Chrome web store](https://chrome.google.com/webstore/category/home)
*   [Различия между Chromium и Google Chrome](https://en.wikipedia.org/wiki/ru:Chromium#.D0.9E.D1.82.D0.BB.D0.B8.D1.87.D0.B8.D1.8F_.D0.BE.D1.82_Google_Chrome "wikipedia:ru:Chromium")
*   [Список опций командной строки для Chromium](http://peter.sh/experiments/chromium-command-line-switches/)