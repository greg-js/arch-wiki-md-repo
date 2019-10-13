Ссылки по теме

*   [Плагины для браузеров](/index.php/%D0%9F%D0%BB%D0%B0%D0%B3%D0%B8%D0%BD%D1%8B_%D0%B4%D0%BB%D1%8F_%D0%B1%D1%80%D0%B0%D1%83%D0%B7%D0%B5%D1%80%D0%BE%D0%B2 "Плагины для браузеров")
*   [Firefox/Tweaks](/index.php/Firefox/Tweaks "Firefox/Tweaks")
*   [Firefox/Profile on RAM (Русский)](/index.php/Firefox/Profile_on_RAM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Firefox/Profile on RAM (Русский)")
*   [Firefox/Privacy](/index.php/Firefox/Privacy "Firefox/Privacy")
*   [Chromium (Русский)](/index.php/Chromium_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Chromium (Русский)")
*   [Opera](/index.php/Opera "Opera")

**Состояние перевода:** На этой странице представлен перевод статьи [Firefox](/index.php/Firefox "Firefox"). Дата последней синхронизации: 20 сентября 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Firefox&diff=0&oldid=583421).

[Firefox](https://www.mozilla.org/ru/firefox/) — популярный графический веб-браузер с открытым исходным кодом, разрабатываемый [Mozilla](https://www.mozilla.org/ru/).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Дополнения](#Дополнения)
    *   [2.1 Добавление движков поиска](#Добавление_движков_поиска)
        *   [2.1.1 arch-firefox-search](#arch-firefox-search)
*   [3 Плагины](#Плагины)
*   [4 Настройка](#Настройка)
    *   [4.1 Воспроизведение медиаконтента](#Воспроизведение_медиаконтента)
        *   [4.1.1 Дополнение "Open With"](#Дополнение_"Open_With")
    *   [4.2 Проверка орфографии](#Проверка_орфографии)
    *   [4.3 Интеграция с KDE/GNOME](#Интеграция_с_KDE/GNOME)
    *   [4.4 Плавная прокрутка](#Плавная_прокрутка)
*   [5 Советы и рекомендации](#Советы_и_рекомендации)
    *   [5.1 Тёмные темы](#Тёмные_темы)
    *   [5.2 Частота смены кадров](#Частота_смены_кадров)
    *   [5.3 Ограничение использования памяти](#Ограничение_использования_памяти)
    *   [5.4 Расположение новых вкладок](#Расположение_новых_вкладок)
    *   [5.5 Скриншот страницы](#Скриншот_страницы)
    *   [5.6 Wayland](#Wayland)
    *   [5.7 Правила оконного менеджера](#Правила_оконного_менеджера)
        *   [5.7.1 Профили](#Профили)
    *   [5.8 Сенсорные жесты и точная прокрутка на тачпаде](#Сенсорные_жесты_и_точная_прокрутка_на_тачпаде)
*   [6 Решение проблем](#Решение_проблем)
    *   [6.1 Отключены все расширения Firefox (май 2019)](#Отключены_все_расширения_Firefox_(май_2019))
    *   [6.2 Запуск Firefox занимает много времени](#Запуск_Firefox_занимает_много_времени)
    *   [6.3 Исправление шрифтов](#Исправление_шрифтов)
    *   [6.4 Выбор клиента электронной почты](#Выбор_клиента_электронной_почты)
    *   [6.5 Ассоциации файлов](#Ассоциации_файлов)
    *   [6.6 Firefox самопроизвольно создаёт директорию ~/Desktop](#Firefox_самопроизвольно_создаёт_директорию_~/Desktop)
    *   [6.7 Плагины и блокирование всплывающих окон](#Плагины_и_блокирование_всплывающих_окон)
    *   [6.8 Поведение при нажатии средней кнопки мыши](#Поведение_при_нажатии_средней_кнопки_мыши)
    *   [6.9 Клавиша Backspace не выполняет функцию "Назад"](#Клавиша_Backspace_не_выполняет_функцию_"Назад")
    *   [6.10 Firefox не запоминает авторизацию на сайте](#Firefox_не_запоминает_авторизацию_на_сайте)
    *   [6.11 Не появляется запрос на сохранение открытых вкладок](#Не_появляется_запрос_на_сохранение_открытых_вкладок)
    *   [6.12 Firefox обнаруживает неправильную версию плагина](#Firefox_обнаруживает_неправильную_версию_плагина)
    *   [6.13 Контекстное меню JavaScript не отображается на некоторых сайтах](#Контекстное_меню_JavaScript_не_отображается_на_некоторых_сайтах)
    *   [6.14 Firefox не запоминает язык проверки орфографии по умолчанию](#Firefox_не_запоминает_язык_проверки_орфографии_по_умолчанию)
    *   [6.15 Не отображаются некоторые символы MathML](#Не_отображаются_некоторые_символы_MathML)
    *   [6.16 Разрыв изображения в полноэкранном режиме](#Разрыв_изображения_в_полноэкранном_режиме)
    *   [6.17 WebRTC-модуль Firefox не обнаруживает микрофон](#WebRTC-модуль_Firefox_не_обнаруживает_микрофон)
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

*   **Firefox KDE** — версия с патчем от OpenSUSE для лучшей [интеграции с KDE](#Интеграция_с_KDE/GNOME), чем это возможно сделать с помощью простых дополнений для Firefox.

	[https://build.opensuse.org/package/show/mozilla:Factory/MozillaFirefox](https://build.opensuse.org/package/show/mozilla:Factory/MozillaFirefox) || [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/)

*   Кроме указанных выше каналов распространения Mozilla, существуют также форки со своими особенностями. Смотрите [Список приложений#Основанные на Gecko](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9#Основанные_на_Gecko "Список приложений").

Кроме языка по умолчанию, английского, для Firefox также доступен ряд языковых пакетов. Обычно они называются `firefox-i18n-*languagecode*` (где `*languagecode*` может быть любым кодом языка, например, **ru**, **de**, **ja**, **fr** и так далее). Для получения списка доступных языковых пакетов смотрите [firefox-i18n](https://www.archlinux.org/packages/extra/any/firefox-i18n/) для [firefox](https://www.archlinux.org/packages/?name=firefox), [firefox-developer-edition-i18n](https://www.archlinux.org/packages/community/any/firefox-developer-edition-i18n/) для [firefox-developer-edition](https://www.archlinux.org/packages/?name=firefox-developer-edition) и [firefox-nightly-](https://aur.archlinux.org/packages/?K=firefox-nightly-) для [firefox-nightly](https://aur.archlinux.org/packages/firefox-nightly/).

## Дополнения

Firefox известен большой библиотекой дополнений, которые используются для добавления новых возможностей или изменения существующих. Управлять дополнениями, а также находить новые, можно с помощью инструмента "Дополнения" в Firefox.

Для получения информации об установке дополнений и их списков, смотрите статью [Browser extensions](/index.php/Browser_extensions "Browser extensions").

### Добавление движков поиска

Движки поиска добавляются посредством обычных дополнений. Смотрите [эту страницу](https://addons.mozilla.org/ru/firefox/search-tools/) для получения списка доступных поисковых движков.

Большой список движков поиска можно найти на сайте [Mycroft Project](https://mycroftproject.com/).

Также можно воспользоваться дополнением [add-to-searchbar](https://firefox.maltekraus.de/extensions/add-to-search-bar) для добавления движков поиска с любого сайта, просто нажав правой кнопкой мышки на соответствующее поле поиска, а затем выбрав *Add to Search Bar...* в меню.

#### arch-firefox-search

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [arch-firefox-search](https://aur.archlinux.org/packages/arch-firefox-search/), чтобы добавить специфичные для Arch движки поиска (AUR, wiki, форум и т.д.).

## Плагины

Единственный поддерживаемый Firefox плагин — [Adobe Flash Player](/index.php/Browser_plugins#Adobe_Flash_Player "Browser plugins") (NPAPI-версия). Другие плагины [больше не поддерживаются](https://support.mozilla.org/ru/kb/npapi-plugins).

Для получения списка установленных/активированных плагинов введите:

```
about:plugins

```

в адресную строку или перейдите в *Дополнения* в меню Firefox и выберите вкладку *Плагины*.

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

### Воспроизведение медиаконтента

В Firefox используется [FFmpeg](/index.php/FFmpeg "FFmpeg") для воспроизведения медиаконтента в HTML5-элементах `<audio>` и `<video>`. Перейдите на [HTML5-страницу YouTube](https://www.youtube.com/html5), [страницу видео-теста](https://www.quirksmode.org/html5/tests/video.html) или [страницу аудио-теста](https://hpr.dogphilosophy.net/test/) для проверки поддерживаемых форматов.

Воспроизведение HTML5 DRM поддерживается Google Widevine CDM, но не активировано по умолчанию. Смотрите *Настройки > Основные > Содержимое использующее технические средства защиты авторских прав (DRM)* для получения более подробной информации.

Смотрите [Firefox/Tweaks#Enable additional media codecs](/index.php/Firefox/Tweaks#Enable_additional_media_codecs "Firefox/Tweaks") для получения информации об активации и расширенной настройке Widevine (Netflix, Amazon Video и т.д.).

В Firefox используется [PulseAudio (Русский)](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PulseAudio (Русский)") при захвате и воспроизведении аудио, для чего потребуется установка пакета [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio).

Если вы не можете использовать [PulseAudio (Русский)](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PulseAudio (Русский)") по какой-либо причине, воспользуйтесь [apulse](/index.php/Advanced_Linux_Sound_Architecture#PulseAudio_compatibility "Advanced Linux Sound Architecture"). В таком случае, необходимо исключить `/dev/snd/` из песочницы Firefox, добавив данный путь в список разделяемый запятой в `about:config`:

```
security.sandbox.content.write_path_whitelist

```

**Примечание:** Важно использовать завершающий слэш в `/dev/snd/`, иначе *apulse* будет сообщать об ошибках "Permission denied".

Если у вас нет звука даже при использовании *apulse*, попробуйте добавить `16` в `security.sandbox.content.syscall_whitelist` в `about:config`.

#### Дополнение "Open With"

1.  Установите дополнение [Open With](https://addons.mozilla.org/ru/firefox/addon/open-with/).
2.  Перейдите в *Дополнения > Open With > Preferences*.
3.  Следуйте инструкциям по установке файла в систему, после чего проверьте его доступность.
4.  Нажмите *Add browser*.
5.  В диалоге укажите название для данной записи в меню и команду для запуска видеоплеера с поддержкой потокового вещания (например, [/usr/bin/mpv](/index.php/Mpv_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mpv (Русский)")).
6.  (Опционально) Добавьте необходимые аргументы плеера (например, `--force-window --ytdl` для *mpv*)
7.  Нажмите правой кнопкой мыши на ссылке с видео или перейдите на его страницу. Выберите добавленную запись из меню Open With и если сайт поддерживается, откроется плеер с данным видео.

Таким же образом можно добавить запись с *youtube-dl* для загрузки видео.

### Проверка орфографии

Установите пакет [hunspell](https://www.archlinux.org/packages/?name=hunspell). Также потребуется установить словари для необходимых языков, например, [hunspell-fr](https://www.archlinux.org/packages/?name=hunspell-fr) (для французского) или [hunspell-he](https://www.archlinux.org/packages/?name=hunspell-he) (для иврита).

Чтобы включить проверку правописания для определённого языка, нажмите правой кнопкой мыши на любом текстовом поле и отметьте галочкой пункт *Проверка орфографии*. Для выбора языка, снова нажмите ПКМ и выберите необходимый язык из подменю *Языки*.

Чтобы загрузить больше языков, выберите пункт *Добавить словари...* и установите необходимые языки из списка. Также можно воспользоваться пакетом [firefox-spell-ru](https://www.archlinux.org/packages/?name=firefox-spell-ru) для добавления русского языка.

Если выбор языка по умолчанию не сохраняется, см. раздел [Firefox#Firefox does not remember default spell check language](/index.php/Firefox#Firefox_does_not_remember_default_spell_check_language "Firefox").

### Интеграция с KDE/GNOME

*   Чтобы задать внешний вид [KDE (Русский)](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)") GTK-приложениям (включая Firefox), установите [breeze-gtk](https://www.archlinux.org/packages/?name=breeze-gtk) и [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config). После чего перейдите в *Параметры системы > Оформление приложений > Стиль программ GNOME/GTK+*. Убедитесь, что в полях 'Выберите тему GTK+ 2.x/3.x' стоит 'Breeze' и отмечены галочки 'Показывать значки на кнопках GTK+' и 'Показывать значки в меню GTK+'.
*   Чтобы полоса прокрутки перемещалась в указанное положение по нажатию левой кнопки мыши (вместо средней в KDE), перейдите в *Параметры системы > Оформление приложений > Стиль программ GNOME/GTK+* и в опции 'При нажатии левой кнопкой мыши на полосе прокрутки' выберите 'Проматывать страницу в соответствии с положением курсора'.
*   Чтобы использовать диалоги выбора файлов и печати KDE в Firefox 64 или новее, воспользуйтесь следующей инструкцией:
    1.  Установите пакеты [xdg-desktop-portal](https://www.archlinux.org/packages/?name=xdg-desktop-portal) и [xdg-desktop-portal-kde](https://www.archlinux.org/packages/?name=xdg-desktop-portal-kde).
    2.  Задайте [переменную окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `GTK_USE_PORTAL=1` или [отредактируйте файл .desktop](/index.php/Desktop_entries_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Изменение_переменных_среды "Desktop entries (Русский)"), добавив `GTK_USE_PORTAL=1` в начало команды во всех строках `Exec`.
*   Для интеграции с системой MIME-типов [KDE (Русский)](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)") и диалогом выбора файлов можно воспользоваться [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/), сборкой Firefox с патчами от OpenSUSE. В качестве альтернативы можно создать символическую ссылку на базу данных MIME `~/.config/mimeapps.list` из устаревшей базы данных `~/.local/share/applications/mimeapps.list`, используемой Firefox. См. [XDG MIME Applications (Русский)#mimeapps.list](/index.php/XDG_MIME_Applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#mimeapps.list "XDG MIME Applications (Русский)").
*   Также существуют расширения для дополнительной интеграции, например:
    *   Интеграция браузера с [Plasma (Русский)](/index.php/Plasma_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Plasma (Русский)"). Необходимо установить [plasma-browser-integration](https://www.archlinux.org/packages/?name=plasma-browser-integration) и [дополнение Plasma Integration](https://addons.mozilla.org/ru/firefox/addon/plasma-integration/).
    *   [mozilla-extension-gnome-keyring-git](https://aur.archlinux.org/packages/mozilla-extension-gnome-keyring-git/) (реализация на JavaScript) для интеграции Firefox с [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring"). Задайте параметру `extensions.gnome-keyring.keyringName` значение `login` в `about:config`, чтобы firefox-gnome-keyring использовал вашу связку ключей для входа. Обратите внимание на строчную букву 'l', несмотря на прописную 'L' в названии связки ключей в Seahorse.

### Плавная прокрутка

Для того, чтобы добиться плавной, основанной на физике прокрутки, как в других браузерах, можно изменить параметры `general.smoothScroll.msdPhysics`. Для более быстрой настройки добавьте следующие строки в файл `~/.mozilla/firefox/**ваш-профиль**/user.js` (требует перезагрузки):

```
user_pref("general.smoothScroll.lines.durationMaxMS", 125);
user_pref("general.smoothScroll.lines.durationMinMS", 125);
user_pref("general.smoothScroll.mouseWheel.durationMaxMS", 200);
user_pref("general.smoothScroll.mouseWheel.durationMinMS", 100);
user_pref("general.smoothScroll.msdPhysics.enabled", true);
user_pref("general.smoothScroll.other.durationMaxMS", 125);
user_pref("general.smoothScroll.other.durationMinMS", 125);
user_pref("general.smoothScroll.pages.durationMaxMS", 125);
user_pref("general.smoothScroll.pages.durationMinMS", 125);

```

Также, опционально, измените настройки прокрутки колёсиком мыши, чтобы добиться такого же плавного скролла:

```
user_pref("mousewheel.min_line_scroll_amount", 30);
user_pref("mousewheel.system_scroll_override_on_root_content.enabled", true);
user_pref("mousewheel.system_scroll_override_on_root_content.horizontal.factor", 175);
user_pref("mousewheel.system_scroll_override_on_root_content.vertical.factor", 175);
user_pref("toolkit.scrollbox.horizontalScrollDistance", 6);
user_pref("toolkit.scrollbox.verticalScrollDistance", 2);

```

При возникновении проблем с производительностью, попробуйте добиться желаемого результата, изменяя параметр `mousewheel.min_line_scroll_amount`.

## Советы и рекомендации

Для получения информации об общих улучшениях и улучшениях безопасности смотрите статьи [Firefox/Tweaks](/index.php/Firefox/Tweaks "Firefox/Tweaks") и [Firefox/Privacy](/index.php/Firefox/Privacy "Firefox/Privacy") соответственно.

### Тёмные темы

Рекомендуется запускать Firefox с более светлой темой (например, Adwaita), если используется тёмная тема [GTK (Русский)](/index.php/GTK_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GTK (Русский)") (например, Arc Dark). См. [GTK+ (Русский)#Темы](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Темы "GTK+ (Русский)") и [Firefox/Tweaks#Unreadable input fields with dark GTK themes](/index.php/Firefox/Tweaks#Unreadable_input_fields_with_dark_GTK_themes "Firefox/Tweaks") для получения более подробной информации.

В качестве альтернативы, начиная с Firefox 68, интерфейсу Firefox и даже другим сайтам можно задать приоритет использования тёмной темы независимо от темы Firefox и системной темы GTK. Задайте параметру `browser.in-content.dark-mode` значение `true`, а параметру `ui.systemUsesDarkTheme` значение `1` на странице `about:config` [[1]](https://bugzilla.mozilla.org/show_bug.cgi?id=1488384#c23).

### Частота смены кадров

Firefox может не определить корректное значение автоматически и вернётся к отрисовке на частоте 60 Гц, если используется монитор с высокой частотой смены кадров. Задайте параметру `layout.frame_rate` частоту смены кадров используемого монитора, например, 144 для монитора с частотой 144 Гц, чтобы изменить данное поведение вручную.

### Ограничение использования памяти

Воспользуйтесь [Firejail](/index.php/Firejail "Firejail") с параметром `rlimit-as`, чтобы предотвратить слишком большое потребление памяти веб-страницами (и возможную нехватку памяти).

Также может помочь уменьшение [Swappiness (Русский)](/index.php/Swappiness_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Swappiness (Русский)").

### Расположение новых вкладок

Используйте параметры `browser.tabs.insertAfterCurrent` и `browser.tabs.insertRelatedAfterCurrent`, чтобы настроить расположение новых вкладок (относительное или абсолютное). См. [[2]](https://support.mozilla.org/en/questions/1229062) для получения более подробной информации.

### Скриншот страницы

*Сделать скриншот* можно из меню *Действия страницы* (три горизонтальных точки) в адресной строке или из контекстного меню страницы (доступному по щелчку ПКМ). См. [[3]](https://support.mozilla.org/ru/kb/skrinshoty-firefox) для получения более подробной информации.

**Примечание:**

*   Кнопка *Сохранить* обманчиво загружает скриншот на поддомен firefox.com. Задайте параметру `extensions.screenshots.upload-disabled` значение `true`, чтобы отключить эту функцию. [[4]](https://github.com/mozilla-services/screenshots/issues/3503)
*   Если включён параметр [privacy.resistFingerprinting](/index.php/Firefox/Privacy#Anti-fingerprinting "Firefox/Privacy"), для создания скриншота вышеописанным методом потребуется дать разрешение *Extract Canvas Data*.

Также можно воспользоваться кнопкой создания скриншота всей страницы в *Инструментах разработчика*, которые доступны по нажатию `F12` или `Ctrl+Shift+i` (сперва может потребоваться включить эту кнопку в *Настройках инструментов разработчика > Доступные кнопки инструментов > Сделать скриншот всей страницы*).

### Wayland

Последние версии Firefox можно запустить в Wayland, используя переменную окружения.

Для начала убедитесь, что текущая сессия действительно запущена в Wayland:

 `$ printenv XDG_SESSION_TYPE` 
```
wayland

```

Затем запустите Firefox следующим образом:

```
$ MOZ_ENABLE_WAYLAND=1 firefox

```

После чего перейдите на страницу about:support и проверьте значение строки "Window Protocol" — если метод сработал, вы увидите `wayland`. В противном случае, будет отображаться `x11`.

Чтобы сделать данное изменение постоянным, отредактируйте ярлык Firefox (`firefox.desktop`), добавив `env MOZ_ENABLE_WAYLAND=1` ко всем строкам `Exec=`. См. [Desktop entries (Русский)#Изменение переменных среды](/index.php/Desktop_entries_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Изменение_переменных_среды "Desktop entries (Русский)") для получения более подробной информации.

Затем запустите Firefox с помощью ярлыка и снова проверьте строку "Window Protocol".

### Правила оконного менеджера

Измените значение строки WM_CLASS на желаемое с использованием аргумента `--class` для применения разных настроек к окнам Firefox.

#### Профили

Для запуска новых копий Firefox необходимо создать несколько профилей:

```
$ firefox [--new-instance] -P

```

Класс окна указывается при запуске Firefox с неиспользуемым профилем:

```
$ firefox [--new-instance] -P *profile_name* --class=*class_name*

```

### Сенсорные жесты и точная прокрутка на тачпаде

Задайте [переменную окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `MOZ_USE_XINPUT2=1` перед запуском Firefox для включения сенсорных жестов (например, прокрутки и масштабирования) и ("один в один") точной прокрутки на тачпаде (что заметно в GTK3-приложениях, например, Nautilus).

## Решение проблем

### Отключены все расширения Firefox (май 2019)

**Важно:** **Не** удаляйте или переустанавливайте дополнения, чтобы попытаться решить проблему, так как удалятся все их данные.

Все дополнения Firefox (расширения, темы, поисковые движки и языковые пакеты) были ошибочно помечены **устаревшими** и не могли быть включены между 3–5 мая 2019\. [Баг](https://bugzilla.mozilla.org/show_bug.cgi?id=1548973) был вызван просроченным промежуточным сертификатом.

Для большинства пользователей проблема была исправлена в Firefox 66.0.4 и Firefox ESR 60.6.2\. Дополнения должны автоматически включиться при установке новой версии Firefox с патчем. Некоторым же пользователям, например, использующим мастер-пароль, требуется несколько дополнительных шагов. См. [официальную страницу поддержки](https://support.mozilla.org/ru/kb/dopolneniya-otklyucheny-ili-ih-nevozmozhno-ustanov) Firefox для получения более подробной информации.

### Запуск Firefox занимает много времени

Firefox может загружаться дольше, чем другие браузеры, если отсутствует конфигурация локальной машины в файле `/etc/hosts`. См. раздел [Настройка сети#Разрешение имён хостов локальной сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8#Разрешение_имён_хостов_локальной_сети "Настройка сети") для получения информации о настройке.

### Исправление шрифтов

См. [Настройка шрифтов](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%88%D1%80%D0%B8%D1%84%D1%82%D0%BE%D0%B2 "Настройка шрифтов").

Firefox использует отдельный параметр, определяющий количество замен из fontconfig. Задайте параметру `gfx.font_rendering.fontconfig.max_generic_substitutions` значение `127` (максимальное число), чтобы разрешить использование всех правил замены.

### Выбор клиента электронной почты

Firefox по умолчанию открывает ссылки `mailto` веб-приложением, таким как Gmail или Yahoo Mail. Чтобы выбрать другой клиент, перейдите в *Настройки > Приложения* и в столбике *Действие* для `mailto` укажите абсолютный путь к исполняемому файлу клиента электронной почты (например, `/usr/bin/kmail` для KMail).

Вне браузера, ссылки `mailto` обрабатываются MIME-типом `x-scheme-handler/mailto`, который можно легко настроить с помощью [xdg-mime](/index.php/XDG_MIME_Applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "XDG MIME Applications (Русский)"). См. статью [Приложения по умолчанию](/index.php/%D0%9F%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F_%D0%BF%D0%BE_%D1%83%D0%BC%D0%BE%D0%BB%D1%87%D0%B0%D0%BD%D0%B8%D1%8E "Приложения по умолчанию") для получения более подробной информации.

### Ассоциации файлов

Смотрите [Приложения по умолчанию](/index.php/%D0%9F%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F_%D0%BF%D0%BE_%D1%83%D0%BC%D0%BE%D0%BB%D1%87%D0%B0%D0%BD%D0%B8%D1%8E "Приложения по умолчанию").

### Firefox самопроизвольно создаёт директорию ~/Desktop

Firefox использует директорию `~/Desktop` для скачиваемых и загружаемых файлов по умолчанию. Настройте параметр `XDG_DESKTOP_DIR`, как описано в статье [XDG user directories (Русский)](/index.php/XDG_user_directories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "XDG user directories (Русский)"), чтобы сменить директорию.

### Плагины и блокирование всплывающих окон

Некоторые плагины могут работать неправильно и игнорировать стандартные настройки, например Flash. Это можно исправить следующим образом:

1.  Введите `about:config` в адресной строке.
2.  Нажмите правую кнопку мыши на странице и выберите *Создать > Целое*.
3.  Задайте название: `privacy.popups.disable_from_plugins`.
4.  Задайте значение: 2.

Возможные значения:

*   `**0**`: Разрешать все всплывающие окна плагинов.
*   `**1**`: Разрешать всплывающие окна, но ограничивать их до `dom.popup_maximum`.
*   `**2**`: Блокировать всплывающие окна плагинов.
*   `**3**`: Блокировать всплывающие окна плагинов, даже на сайтах в белом списке.

### Поведение при нажатии средней кнопки мыши

Задайте параметру `middlemouse.contentLoadURL` или `middlemouse.paste` значение `true` в `about:config`, чтобы использовать среднюю кнопку мыши для вставки содержимого буфера обмена, как это принято в UNIX-подобных операционных системах. Опция `middlemouse.contentLoadURL` была включена по умолчанию до Firefox 57.

Задайте параметру `general.autoScroll` значение `true`, чтобы использовать среднюю кнопку мыши для прокрутки (стандартное поведение для браузеров в Windows).

### Клавиша Backspace не выполняет функцию "Назад"

Согласно [MozillaZine](http://kb.mozillazine.org/Browser.backspace_action), действие клавиши `Backspace` задавалось в зависимости от ОС, в которой выполнялся браузер. В качестве компромисса был создан параметр, позволяющий игнорировать нажатие `Backspace` или использовать его для перехода на следующую/предыдущую страницу или для прокрутки страницы вверх/вниз.

Задайте параметру `browser.backspace_action` значение `0` в `about:config`, чтобы использовать `Backspace` для перехода на одну страницу назад и `Shift+Backspace` на страницу вперёд в истории вкладки.

Задайте параметру `browser.backspace_action` значение `1`, чтобы использовать клавишу `Backspace` для прокрутки на одну страницу вверх и `Shift+Backspace` на страницу вниз. В случае с какими-либо другими значениями нажатия клавиши будут игнорироваться (в Arch Linux по умолчанию используется `2`, т.е. действие не назначено).

### Firefox не запоминает авторизацию на сайте

Это может быть вызвано повреждённым файлом `cookies.sqlite` в [профиле Firefox](https://support.mozilla.org/ru/kb/profili-gde-firefox-hranit-vashi-zakladki-paroli-i). Переименуйте или удалите `cookie.sqlite` предварительно закрыв Firefox, чтобы исправить проблему.

Откройте терминал и введите следующее:

```
$ rm -f ~/.mozilla/firefox/<id профиля>.default/cookies.sqlite

```

ID профиля — случайно сгенерированная строка из 8 символов.

Перезапустите Firefox и проверьте, помогло ли это решить проблему.

### Не появляется запрос на сохранение открытых вкладок

C официального сайта [поддержки Mozilla](https://support.mozilla.com/ru/questions/767751):

1.  Введите `about:config` в адресную строку.
2.  Задайте значение `true` параметру `browser.warnOnQuit`.
3.  Задайте значение `true` параметру `browser.showQuitWarning`.

### Firefox обнаруживает неправильную версию плагина

Во время закрытия, Firefox записывает временную метку (timestamp) и текущую версию плагинов в файл `pluginreg.dat`, расположенный в директории профиля (обычно `~/.mozilla/firefox/*xxxxxxxx*.default/`).

Если вы обновили плагин в то время, когда Firefox был запущен, то в файл будет записана неправильная информация. При следующем запуске Firefox покажет сообщение `Firefox has prevented the outdated plugin "XXXX" from running on ...` во время воспроизведения контента соответствующим плагином, что часто случается с официальным [плагином Adobe Flash Player](/index.php/Browser_plugins#Adobe_Flash_Player "Browser plugins").

Решение состоит в удалении файла `pluginreg.dat` из директории профиля. Firefox автоматически пересоздаст данный файл при следующем закрытии. [[5]](https://bugzilla.mozilla.org/show_bug.cgi?id=1109795#c16)

### Контекстное меню JavaScript не отображается на некоторых сайтах

Попробуйте задать параметру `dom.w3c_touch_events.enabled` значение `0` в `about:config`.

### Firefox не запоминает язык проверки орфографии по умолчанию

Язык проверки орфографии по умолчанию задаётся следующим образом:

1.  Введите `about:config` в адресной строке.
2.  Задайте параметру `spellchecker.dictionary` необходимый язык, например, `en_GB`.
3.  Заметьте, что в случае со словарями, установленными с помощью плагинов Firefox, следует указывать `en-GB`, а в случае со словарями [hunspell](https://www.archlinux.org/packages/?name=hunspell) — `en_GB`.

Firefox может не запоминать язык по умолчанию, если установлены только системные словари [hunspell](https://www.archlinux.org/packages/?name=hunspell). Это исправляется установкой хотя бы одного [словаря](https://addons.mozilla.org/firefox/language-tools/) в виде Firefox-плагина. Также после этого появится вкладка **Словари** в **Дополнениях**. Кроме того, может потребоваться изменить порядок предпочитаемых языков для отображения веб-страниц в `about:preferences#general`, чтобы язык проверки орфографии по умолчанию соответствовал языку словаря из дополнения.

Связанные вопросы на **StackExchange**: [[6]](https://stackoverflow.com/questions/26936792/change-firefox-spell-check-default-language/29446115), [[7]](https://stackoverflow.com/questions/21542515/change-default-language-on-firefox/29446353), [[8]](https://askubuntu.com/questions/184300/how-can-i-change-firefoxs-default-dictionary/576877)

Соответствующие отчёты об ошибках: [Bugzilla 776028](https://bugzilla.mozilla.org/show_bug.cgi?id=776028), [Ubuntu bug 1026869](https://bugs.launchpad.net/ubuntu/+source/firefox/+bug/1026869)

### Не отображаются некоторые символы MathML

Необходимо установить шрифты Latin Modern Math и STIX (см. страницу MDN: [[9]](https://developer.mozilla.org/en-US/docs/Mozilla/MathML_Project/Fonts#Linux)) для корректного отображения MathML.

В Arch Linux данные шрифты содержатся в пакетах [texlive-core](https://www.archlinux.org/packages/?name=texlive-core) **и** [texlive-fontsextra](https://www.archlinux.org/packages/?name=texlive-fontsextra), но недоступны fontconfig по умолчанию. См. [TeX Live#Making fonts available to Fontconfig](/index.php/TeX_Live#Making_fonts_available_to_Fontconfig "TeX Live") для получения более подробной информации. Также можно попробовать другие [математические шрифты](/index.php/Fonts#Math "Fonts").

### Разрыв изображения в полноэкранном режиме

Если наблюдается разрыв изображения ("тиринг") при просмотре видео в полноэкранном режиме с драйверами Intel или Nouveau (в сеансе Xorg), попробуйте [Firefox tweaks#Enable OpenGL Off-Main-Thread Compositing (OMTC)](/index.php/Firefox_tweaks#Enable_OpenGL_Off-Main-Thread_Compositing_(OMTC) "Firefox tweaks").

### WebRTC-модуль Firefox не обнаруживает микрофон

WebRTC-приложения, например, [тестовая страница Firefox WebRTC getUserMedia](https://mozilla.github.io/webrtc-landing/gum_test.html), сообщают, что не могут обнаружить микрофон. Проблема воспроизводится как с ALSA, так и с PulseAudio, а логи отладки Firefox показывают следующую ошибку:

 `$ NSPR_LOG_MODULES=MediaManager:5,GetUserMedia:5 firefox` 
```
...
[Unnamed thread 0x7fd7c0654340]: D/GetUserMedia  VoEHardware:GetRecordingDeviceName: Failed 1
```

Попробуйте задать параметру `media.navigator.audio.full_duplex` значение `false` на странице `about:config` и перезапустить Firefox.

Также это может помочь в случае, когда Firefox не обнаруживает виртуальный источник эхоподавления при использовании [module-echo-cancel](/index.php/PulseAudio/Troubleshooting#Enable_Echo/Noise-Cancellation "PulseAudio/Troubleshooting") в PulseAudio.

## Смотрите также

*   [Официальный веб-сайт](https://www.mozilla.org/ru/firefox/)
*   [Mozilla Foundation](https://www.mozilla.org/ru/)
*   [MozillaWiki:Firefox](https://wiki.mozilla.org/Firefox "mozillawiki:Firefox")
*   [Дополнения для Firefox](https://addons.mozilla.org/ru/firefox/)
*   [Темы для Firefox](https://addons.mozilla.org/ru/firefox/themes/)
*   [Wikipedia:ru:Mozilla Firefox](https://en.wikipedia.org/wiki/ru:Mozilla_Firefox "wikipedia:ru:Mozilla Firefox")
*   [mozillaZine](http://forums.mozillazine.org/) — Неофициальный форум