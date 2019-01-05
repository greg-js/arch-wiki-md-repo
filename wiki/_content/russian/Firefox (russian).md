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
*   [3 Настройка](#Настройка)
*   [4 Плагины](#Плагины)
*   [5 Советы и полезности](#Советы_и_полезности)
*   [6 Решение проблем](#Решение_проблем)
    *   [6.1 Выбор клиента электронной почты](#Выбор_клиента_электронной_почты)
    *   [6.2 Ассоциации файлов](#Ассоциации_файлов)
    *   [6.3 Firefox каждый раз самопроизвольно создаёт директорию ~/Desktop](#Firefox_каждый_раз_самопроизвольно_создаёт_директорию_~/Desktop)
    *   [6.4 Плагины и блокирование всплывающих окон (pop-up)](#Плагины_и_блокирование_всплывающих_окон_(pop-up))
    *   [6.5 Ошибки по нажатию средней кнопки мыши](#Ошибки_по_нажатию_средней_кнопки_мыши)
    *   [6.6 Клавиша *Backspace* не выполняет функцию 'Назад'](#Клавиша_Backspace_не_выполняет_функцию_'Назад')
    *   [6.7 Firefox не запоминает авторизацию на сайте](#Firefox_не_запоминает_авторизацию_на_сайте)
    *   [6.8 "Do you want Firefox to save your tabs for the next time it starts?" dialog does not appear](#"Do_you_want_Firefox_to_save_your_tabs_for_the_next_time_it_starts?"_dialog_does_not_appear)
*   [7 Смотрите также](#Смотрите_также)

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

*   Кроме указанных выше каналов распространения Mozilla, существуют также форки со своими особенностями. Смотрите [Список приложений#Основанные на Gecko](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#Основанные_на_Gecko "Список приложений").

Кроме языка по умолчанию, английского, для Firefox также доступен ряд языковых пакетов. Обычно они называются `firefox-i18n-*languagecode*` (где `*languagecode*` может быть любым кодом языка, например, **ru**, **de**, **ja**, **fr** и так далее). Для получения списка доступных языковых пакетов смотрите [firefox-i18n](https://www.archlinux.org/packages/extra/any/firefox-i18n/) для [firefox](https://www.archlinux.org/packages/?name=firefox) и [firefox-developer-edition-i18n](https://www.archlinux.org/packages/community/any/firefox-developer-edition-i18n/) для [firefox-developer-edition](https://www.archlinux.org/packages/?name=firefox-developer-edition).

## Дополнения

Firefox известен большой библиотекой дополнений, которые используются для добавления новых возможностей или изменения существующих. Управлять дополнениями, а также находить новые, можно с помощью инструмента "Дополнения" в Firefox.

Для получения информации об установке дополнений и их списков, смотрите статью [Browser extensions](/index.php/Browser_extensions "Browser extensions").

### Добавление движков поиска

Движки поиска добавляются посредством обычных дополнений. Смотрите [эту страницу](https://addons.mozilla.org/ru/firefox/search-tools/) для получения списка доступных поисковых движков.

Большой список движков поиска можно найти на сайте [Mycroft Project](https://mycroftproject.com/).

Также можно воспользоваться дополнением [add-to-searchbar](https://firefox.maltekraus.de/extensions/add-to-search-bar) для добавления движков поиска с любого сайта, просто нажав правой кнопкой мышки на соответствующее поле поиска, а затем выбрав *Add to Search Bar...* в меню.

#### arch-firefox-search

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [arch-firefox-search](https://www.archlinux.org/packages/?name=arch-firefox-search), чтобы добавить специфичные для Arch движки поиска (AUR, wiki, форум и т.д.).

## Настройка

В Firefox довольно много параметров конфигурации браузера. Чтобы просмотреть их, введите в адресную строку:

```
about:config

```

Изменения вступают в силу для текущего профиля пользователя и могут синхронизироваться между устройствами с помощью [Firefox Sync](https://www.mozilla.org/ru/firefox/sync/). Обратите внимание, что таким образом синхронизируется только часть всех параметров `about:config`, а именно параметры, начинающиеся с `services.sync.prefs`. Дополнительные параметры и параметры третьих лиц (например, дополнений) можно вручную добавить в синхронизацию, создав новый параметр типа boolean с названием, начинающимся с `services.sync.prefs.sync` ([документация](https://developer.mozilla.org/en-US/docs/Archive/Mozilla/Firefox_Sync/Syncing_custom_preferences)). Например, для синхронизации белого списка дополнения [NoScript](https://addons.mozilla.org/firefox/addon/noscript/), добавьте следующий параметр:

```
services.sync.prefs.sync.capability.policy.maonoscript.sites

```

Параметр `noscript.sync.enabled` должен иметь значение `true` для синхронизации остальных настроек NoScript через Firefox Sync.

Также Firefox позволяет хранить конфигурацию профиля в файле `user.js`: [user.js](http://kb.mozillazine.org/User.js_file) в директории профиля, обычно `~/.mozilla/firefox/*xxxxxxxx*.default/`. Пример файла, который ориентирован на увеличение безопасности и приватности пользователя, доступен в [данном репозитории](https://github.com/pyllyukko/user.js),

Недостаток такого подхода в том, что параметры не применяются сразу для всей системы. Более того, его нельзя использовать для предварительной конфигурации, так как директория профиля создаётся только после первого запуска браузера. С другой стороны, можно запустить *firefox* (в это время создастся директория профиля), закрыть его и [скопировать](https://support.mozilla.org/ru/kb/rezervirovanie-vashih-dannyh#w_caaaaulahkilii-laaeika-ii-aiiiahlai-jalii) содержимое уже созданного профиля в новую директорию.

Иногда необходимо заблокировать некоторые параметры, например, при установке модифицированной версии Firefox на большое количество устройств. Чтобы создать конфигурацию для всей системы, следуйте инструкции из статьи [Locking preferences](http://kb.mozillazine.org/Locking_preferences):

1\. Создайте `/usr/lib/firefox/defaults/pref/local-settings.js`:

```
pref("general.config.obscure_value", 0);
pref("general.config.filename", "mozilla.cfg");

```

2\. Создайте `/usr/lib/firefox/mozilla.cfg` (где будет хранится сама конфигурация):

```
//
//...ваши настройки...
// например, раскомментируйте параметр ниже для отключения Pocket
// lockPref("browser.pocket.enabled", false);

```

Обратите внимание, что первая строка должна содержать именно `//`. Синтаксис данного файла похож на синтаксис `user.js`.

## Плагины

**Примечание:** В Firefox [прекращена поддержка](https://support.mozilla.org/ru/kb/npapi-plugins) плагинов [NPAPI](https://en.wikipedia.org/wiki/ru:NPAPI "wikipedia:ru:NPAPI"), кроме Flash.

Смотрите основную статью: [Browser plugins](/index.php/Browser_plugins "Browser plugins")

Для получения списка установленных/активированных плагинов, введите:

```
about:plugins

```

в адресную строку или перейдите в *Дополнения* в меню Firefox и выберите вкладку *Плагины*.

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