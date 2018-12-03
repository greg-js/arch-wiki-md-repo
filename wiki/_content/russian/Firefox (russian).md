Ссылки по теме

*   [Плагины для браузеров](/index.php/%D0%9F%D0%BB%D0%B0%D0%B3%D0%B8%D0%BD%D1%8B_%D0%B4%D0%BB%D1%8F_%D0%B1%D1%80%D0%B0%D1%83%D0%B7%D0%B5%D1%80%D0%BE%D0%B2 "Плагины для браузеров")
*   [Firefox/Tweaks](/index.php/Firefox/Tweaks "Firefox/Tweaks")
*   [Firefox/Profile on RAM (Русский)](/index.php/Firefox/Profile_on_RAM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Firefox/Profile on RAM (Русский)")
*   [Firefox/Privacy](/index.php/Firefox/Privacy "Firefox/Privacy")
*   [Chromium (Русский)](/index.php/Chromium_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Chromium (Русский)")
*   [Opera](/index.php/Opera "Opera")

[Firefox](https://www.mozilla.org/ru/firefox/) — популярный графический веб-браузер с открытым исходным кодом, разрабатываемый [Mozilla](https://www.mozilla.org/ru/).

## Contents

*   [1 Установка](#Установка)
*   [2 Дополнения](#Дополнения)
    *   [2.1 Добавление движков поиска](#Добавление_движков_поиска)
        *   [2.1.1 arch-firefox-search](#arch-firefox-search)
*   [3 Плагины](#Плагины)
    *   [3.1 Словари проверки орфографии](#Словари_проверки_орфографии)
    *   [3.2 Инструменты поиска](#Инструменты_поиска)
        *   [3.2.1 Удобный поиск по AUR/Wiki/Форуму Arch Linux с помощью arch-firefox-search](#Удобный_поиск_по_AUR/Wiki/Форуму_Arch_Linux_с_помощью_arch-firefox-search)
*   [4 Советы и полезности](#Советы_и_полезности)
*   [5 Решение проблем](#Решение_проблем)
    *   [5.1 Выбор клиента электронной почты](#Выбор_клиента_электронной_почты)
    *   [5.2 Ассоциации файлов](#Ассоциации_файлов)
    *   [5.3 Firefox каждый раз самопроизвольно создаёт директорию ~/Desktop](#Firefox_каждый_раз_самопроизвольно_создаёт_директорию_~/Desktop)
    *   [5.4 Плагины и блокирование всплывающих окон (pop-up)](#Плагины_и_блокирование_всплывающих_окон_(pop-up))
    *   [5.5 Ошибки по нажатию средней кнопки мыши](#Ошибки_по_нажатию_средней_кнопки_мыши)
    *   [5.6 Клавиша *Backspace* не выполняет функцию 'Назад'](#Клавиша_Backspace_не_выполняет_функцию_'Назад')
    *   [5.7 Firefox не запоминает авторизацию на сайте](#Firefox_не_запоминает_авторизацию_на_сайте)
    *   [5.8 "Do you want Firefox to save your tabs for the next time it starts?" dialog does not appear](#"Do_you_want_Firefox_to_save_your_tabs_for_the_next_time_it_starts?"_dialog_does_not_appear)
*   [6 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [firefox](https://www.archlinux.org/packages/?name=firefox).

Альтернативы:

*   **Firefox Developer Edition** — для разработчиков

	[https://www.mozilla.org/ru/firefox/developer/](https://www.mozilla.org/ru/firefox/developer/) || [firefox-developer-edition](https://www.archlinux.org/packages/?name=firefox-developer-edition)

*   **Firefox Extended Support Release** — версия с длительным сроком поддержки

	[https://www.mozilla.org/firefox/organizations/](https://www.mozilla.org/firefox/organizations/) || [firefox-esr](https://aur.archlinux.org/packages/firefox-esr/) или [firefox-esr-bin](https://aur.archlinux.org/packages/firefox-esr-bin/)

*   **Firefox Beta** — бета-версия

	[https://www.mozilla.org/ru/firefox/channel/desktop/#beta](https://www.mozilla.org/ru/firefox/channel/desktop/#beta) || [firefox-beta](https://aur.archlinux.org/packages/firefox-beta/) или [firefox-beta-bin](https://aur.archlinux.org/packages/firefox-beta-bin/)

*   **Firefox Nightly** — ночные сборки для тестирования [экспериментальных возможностей](https://developer.mozilla.org/Firefox/Experimental_features)

	[https://www.mozilla.org/ru/firefox/channel/desktop/#nightly](https://www.mozilla.org/ru/firefox/channel/desktop/#nightly) || [firefox-nightly](https://aur.archlinux.org/packages/firefox-nightly/)

*   **Firefox KDE** — версия с патчем от OpenSUSE для лучшей [интеграции с KDE](/index.php/Firefox#KDE/GNOME_integration "Firefox"), чем это возможно сделать с помощью простых дополнений для Firefox.

	[https://build.opensuse.org/package/show/mozilla:Factory/MozillaFirefox](https://build.opensuse.org/package/show/mozilla:Factory/MozillaFirefox) || [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/)

*   Кроме различных каналов распространения Mozilla, существуют также форки, в которых присутствуют свои особенности. Смотрите [Список приложений#Основанные на Gecko](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#Основанные_на_Gecko "Список приложений").

Кроме языка по умолчанию, английского, для Firefox также доступен ряд языковых пакетов. Обычно они называются `firefox-i18n-*languagecode*` (где `*languagecode*` может быть любым кодом языка, например, **ru**, **de**, **ja**, **fr** и так далее). Для получения списка доступных языковых пакетов смотрите [firefox-i18n](https://www.archlinux.org/packages/extra/any/firefox-i18n/) для [firefox](https://www.archlinux.org/packages/?name=firefox) и [firefox-developer-edition-i18n](https://www.archlinux.org/packages/community/any/firefox-developer-edition-i18n/) для [firefox-developer-edition](https://www.archlinux.org/packages/?name=firefox-developer-edition).

## Дополнения

Firefox имеет большую библиотеку дополнений, значительно способные расширить функционал. Дополнения можно найти с помощью инструмента "Дополнения" в Firefox.

См. также список [дополнений, отсортированный по популярности](https://addons.mozilla.org/ru-RU/firefox/extensions/?sort=список). См. также [список дополнений Firefox](https://en.wikipedia.org/wiki/List_of_Firefox_extensions "wikipedia:List of Firefox extensions") на Wikipedia.

### Добавление движков поиска

Движки поиска могут быть добавлены посредством дополнений. Смотрите [эту страницу](https://addons.mozilla.org/firefox/search-tools/).

Большой список движков поиска может быть найдет на сайте [Mycroft Project](http://mycroftproject.com/).

Вы можете использовать дополнение [add-to-searchbar](https://firefox.maltekraus.de/extensions/add-to-search-bar), чтобы добавлять движки поиска с любого сайта, просто нажав правой кнопкой мышки на соответствующее поле, а затем выбрав нужный пункт в меню.

#### arch-firefox-search

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [arch-firefox-search](https://www.archlinux.org/packages/?name=arch-firefox-search), чтобы добавить специфичные для Arch движки поиска (AUR, wiki, форум и т.д.).

## Плагины

См. основную статью: [Browser plugins](/index.php/Browser_plugins "Browser plugins").

Список установленных плагинов можно узнать на странице `about:plugins`, перейдя на страницу *Дополнения* через меню *Инструменты* и выбрав вкладку *Плагины*.

### Словари проверки орфографии

Вы можете кликнуть правой кнопкой мыши по полю ввода текста и добавить словарь с нужным языком. После чего перезапустите Firefox, снова нажмите правой кнопкой мыши по полю ввода текста и активируйте проверку орфографии.

Другой вариант: установка необходимого пакета из официального репозитория:

 `pacman -Ss hunspell` 

### Инструменты поиска

Для этого достаточно зайти на сайт [https://addons.mozilla.org/ru/firefox/search-tools/](https://addons.mozilla.org/ru/firefox/search-tools/) и установить нужную вам поисковую службу.

Для добавления поисковой службы вручную, см. файл: `~/.mozilla/firefox/xxx.default/searchplugins/` где xxx — идентификатор вашего профиля в браузере).

#### Удобный поиск по AUR/Wiki/Форуму Arch Linux с помощью arch-firefox-search

Для автоматического добавления поисковых служб связанных с Arch Linux (AUR, Wiki, форум и не только), установите пакет [arch-firefox-search](https://www.archlinux.org/packages/?name=arch-firefox-search), доступный в официальном репозитории.

 `# pacman -S arch-firefox-search` 

## Советы и полезности

См. основную статью: [Firefox tweaks](/index.php/Firefox_tweaks "Firefox tweaks")

## Решение проблем

### Выбор клиента электронной почты

Firefox по умолчанию открывает `mailto` ссылки веб-приложением, таким как Gmail или Yahoo Mail. Чтобы выбрать свой клиент электронной почты для открытия ссылок `mailto`, перейдите в *Настройки > Приложения* и измените значение в столбике *Действие* для `mailto`. Значение должно быть абсолютным путём к исполняемому файлу вашего e-mail клиента (напр. `/usr/bin/kmail` для Kmail).

### Ассоциации файлов

Смотрите [Приложения по умолчанию](/index.php/%D0%9F%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F_%D0%BF%D0%BE_%D1%83%D0%BC%D0%BE%D0%BB%D1%87%D0%B0%D0%BD%D0%B8%D1%8E "Приложения по умолчанию").

### Firefox каждый раз самопроизвольно создаёт директорию ~/Desktop

Firefox использует директорию `~/Desktop` для скачиваемых и загружаемых файлов по умолчанию. Чтобы сменить директорию, создайте файл `~/.config/user-dirs.dirs` со следующим содержимым:

 `~/.config/user-dirs.dirs` 
```
XDG_DESKTOP_DIR="/home/user/"
XDG_DOWNLOAD_DIR="/home/user/dir"
XDG_TEMPLATES_DIR="/home/user/dir"
XDG_PUBLICSHARE_DIR="/home/user/dir"
XDG_DOCUMENTS_DIR="/home/user/dir"
XDG_MUSIC_DIR="/home/user/dir"
XDG_PICTURES_DIR="/home/user/dir"
XDG_VIDEOS_DIR="/home/user/dir"

```

Где */home/user/dir* — существующий путь к директории.

### Плагины и блокирование всплывающих окон (pop-up)

Некоторые плагины могут работать неправильно и игнорировать стандартные настройки, например Flash. Это можно исправив следующими действиями:

1.  Перейдите на страницу `about:config`.
2.  Нажмите правую кнопку мыши на страницу и выберите `Создать` и затем `Целое`.
3.  Задайте название: `privacy.popups.disable_from_plugins`.
4.  Задайте значение: 2.

Возможные значения:

*   **0**: Допустить все всплывающие окна плагинов.
*   **1**: Допустить всплывающие окна плагинов, но ограничить их до dom.popup_maximum.
*   **2**: Блокировать всплывающие окна плагинов.
*   **3**: Блокировать всплывающие окна плагинов, даже на сайтах в белом списке.

### Ошибки по нажатию средней кнопки мыши

Достаточно распространено сообщение об ошибке при использовании средней кнопки мыши в Firefox:

```
The URL is not valid and cannot be loaded.

```

Другой симптом это непредсказуемое поведение браузера, например самопроизвольное открытие случайных сайтов.

Причина связана с использованием средней кнопки мыши в UNIX-подобных операционных системах. Она используется для вставки текста из буфера обмена. Даллее, вероятно, присутствует конфликт одной из возможностей Firefox, которая, по умолчанию, загружает URL в добавленном в буфер обмена тексте по отпусканию средней кнопки мыши. Это поведение можно выключить перейдя на страницу `about:config` и измененив значения опции `middlemouse.contentLoadURL` на **false**.

Как альтернатива, можно переключиться на традиционное для пользователей Windows поведение, когда по нажатию на среднюю кнопку мыши активируется прокрутка страницы. Для этого измените значение опции `general.autoScroll` на **true**.

### Клавиша *Backspace* не выполняет функцию 'Назад'

Согласно [этой статье](http://ubuntu.wordpress.com/2006/12/21/fix-firefox-backspace-to-take-you-to-the-previous-page/), данная возможность была удалена с целью исправления ошибки. Чтобы вернуть это, перейдите на `about:config` и измените значение опции `browser.backspace_action` на **0** (ноль).

### Firefox не запоминает авторизацию на сайте

Это может быть вызвано испорченным файлом `cookies.sqlite` в [директории профиля Firefox](https://support.mozilla.org/ru/kb/profili-gde-firefox-hranit-vashi-zakladki-paroli-i?redirectlocale=en-US&redirectslug=Profiles#w_ouj-kli-luiai-kai-laaeiku). Для исправления, просто переименуйте или удалите `cookie.sqlite`, предварительно закрыв Firefox.

Откройте терминал и введите следующее:

```
$ cd ~/.mozilla/firefox/xxxxxxxx.default/
$ rm -f cookies.sqlite

```

**Примечание:** *xxxxxxxx* — случайно сгенерированная строка из 8 символов.

### "Do you want Firefox to save your tabs for the next time it starts?" dialog does not appear

From the [Mozilla support](https://support.mozilla.com/en-US/questions/767751) site:

1.  Type `about:config` in the address bar.
2.  Set `browser.warnOnQuit` to `true`.
3.  Set `browser.showQuitWarning` to `true`.

## Смотрите также

*   [Официальный веб-сайт](https://www.mozilla.org/ru/firefox/)
*   [Mozilla Foundation](https://www.mozilla.org/ru/)
*   [MozillaWiki:Firefox](https://wiki.mozilla.org/Firefox "mozillawiki:Firefox")
*   [Дополнения для Firefox](https://addons.mozilla.org/ru/firefox/)
*   [Темы для Firefox](https://addons.mozilla.org/ru/firefox/themes/)
*   [Wikipedia:ru:Mozilla Firefox](https://en.wikipedia.org/wiki/ru:Mozilla_Firefox "wikipedia:ru:Mozilla Firefox")
*   [mozillaZine](http://forums.mozillazine.org/) — Неофициальный форум