Ссылки по теме

*   [Плагины для браузеров](/index.php/%D0%9F%D0%BB%D0%B0%D0%B3%D0%B8%D0%BD%D1%8B_%D0%B4%D0%BB%D1%8F_%D0%B1%D1%80%D0%B0%D1%83%D0%B7%D0%B5%D1%80%D0%BE%D0%B2 "Плагины для браузеров")
*   [Firefox/Tweaks](/index.php/Firefox/Tweaks "Firefox/Tweaks")
*   [Firefox/Profile on RAM (Русский)](/index.php/Firefox/Profile_on_RAM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Firefox/Profile on RAM (Русский)")
*   [Firefox/Privacy](/index.php/Firefox/Privacy "Firefox/Privacy")
*   [Chromium (Русский)](/index.php/Chromium_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Chromium (Русский)")
*   [Opera](/index.php/Opera "Opera")

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
    *   [5.2 Скриншот страницы](#Скриншот_страницы)
    *   [5.3 Правила оконного менеджера](#Правила_оконного_менеджера)
    *   [5.4 Сенсорные жесты и точная прокрутка на тачпаде](#Сенсорные_жесты_и_точная_прокрутка_на_тачпаде)
*   [6 Решение проблем](#Решение_проблем)
    *   [6.1 Запуск Firefox занимает много времени](#Запуск_Firefox_занимает_много_времени)
    *   [6.2 Выбор клиента электронной почты](#Выбор_клиента_электронной_почты)
    *   [6.3 Ассоциации файлов](#Ассоциации_файлов)
    *   [6.4 Firefox каждый раз самопроизвольно создаёт директорию ~/Desktop](#Firefox_каждый_раз_самопроизвольно_создаёт_директорию_~/Desktop)
    *   [6.5 Плагины и блокирование всплывающих окон (pop-up)](#Плагины_и_блокирование_всплывающих_окон_(pop-up))
    *   [6.6 Ошибки по нажатию средней кнопки мыши](#Ошибки_по_нажатию_средней_кнопки_мыши)
    *   [6.7 Клавиша *Backspace* не выполняет функцию 'Назад'](#Клавиша_Backspace_не_выполняет_функцию_'Назад')
    *   [6.8 Firefox не запоминает авторизацию на сайте](#Firefox_не_запоминает_авторизацию_на_сайте)
    *   [6.9 Не появляется запрос на сохранение открытых вкладок](#Не_появляется_запрос_на_сохранение_открытых_вкладок)
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

## Плагины

**Примечание:** В Firefox [прекращена поддержка](https://support.mozilla.org/ru/kb/npapi-plugins) [NPAPI](https://en.wikipedia.org/wiki/ru:NPAPI "wikipedia:ru:NPAPI")-плагинов, кроме Flash.

Смотрите основную статью: [Browser plugins (Русский)](/index.php/Browser_plugins_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Browser plugins (Русский)")

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
    1.  Установите [xdg-desktop-portal](https://www.archlinux.org/packages/?name=xdg-desktop-portal) и [xdg-desktop-portal-kde](https://www.archlinux.org/packages/?name=xdg-desktop-portal-kde),
    2.  Скопируйте [ярлык](/index.php/Desktop_entries_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop entries (Русский)") Firefox `/usr/share/applications/firefox.desktop` в `~/.local/share/applications/firefox.desktop`,
    3.  Отредактируйте `~/.local/share/applications/firefox.desktop`, добавив `GTK_USE_PORTAL=1` перед самой командой во всех строках `Exec`. Например: `Exec=GTK_USE_PORTAL=1 /usr/lib/firefox/firefox %u`.
*   Для интеграции с системой MIME-типов [KDE (Русский)](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)") и диалогом выбора файлов можно воспользоваться [firefox-kde-opensuse](https://aur.archlinux.org/packages/firefox-kde-opensuse/), сборкой Firefox с патчами от OpenSUSE.
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

Если используется тёмная тема [GTK (Русский)](/index.php/GTK_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GTK (Русский)") (например, Arc Dark), рекомендуется запускать Firefox с более светлой темой (например, Adwaita). См. [GTK+ (Русский)#Темы](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Темы "GTK+ (Русский)") и [Firefox/Tweaks#Unreadable input fields with dark GTK+ themes](/index.php/Firefox/Tweaks#Unreadable_input_fields_with_dark_GTK+_themes "Firefox/Tweaks") для получения более подробной информации.

### Скриншот страницы

*Сделать скриншот* можно из меню *Действия страницы* (три горизонтальных точки) в адресной строке или из контекстного меню страницы (доступному по щелчку ПКМ). См. [[1]](https://support.mozilla.org/ru/kb/skrinshoty-firefox) для получения более подробной информации.

**Примечание:**

*   Кнопка *Сохранить* обманчиво загружает скриншот на поддомен firefox.com. Задайте параметру `extensions.screenshots.upload-disabled` значение `true`, чтобы отключить эту функцию. [[2]](https://github.com/mozilla-services/screenshots/issues/3503)
*   Если включён параметр [privacy.resistFingerprinting](/index.php/Firefox/Privacy#Anti-fingerprinting "Firefox/Privacy"), для создания скриншота вышеописанным методом потребуется дать разрешение *Extract Canvas Data*.

Также можно воспользоваться кнопкой создания скриншота всей страницы в *Инструментах разработчика*, которые доступны по нажатию `F12` или `Ctrl+Shift+i` (сперва может потребоваться включить эту кнопку в *Настройках инструментов разработчика > Доступные кнопки инструментов > Сделать скриншот всей страницы*).

### Правила оконного менеджера

Измените значение строки WM_CLASS на желаемое с использованием аргумента `--class` для применения разных настроек к окнам Firefox. [[3]](https://developer.mozilla.org/ru/docs/Mozilla/Command_Line_Options#%D0%9E%D0%BF%D1%86%D0%B8%D0%B8_X11)

Для запуска новых копий Firefox необходимо создать несколько профилей:

```
$ firefox --ProfileManager

```

Класс окна указывается при запуске Firefox с неиспользуемым профилем:

```
$ firefox -P *название_профиля* --class=*название_класса*

```

### Сенсорные жесты и точная прокрутка на тачпаде

Задайте [переменную окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `MOZ_USE_XINPUT2=1` перед запуском Firefox для включения сенсорных жестов (например, прокрутки и масштабирования) и ("один в один") точной прокрутки на тачпаде (что заметно в GTK3-приложениях, например, Nautilus).

## Решение проблем

### Запуск Firefox занимает много времени

Firefox может загружаться дольше, чем другие браузеры, если отсутствует конфигурация локальной машины в файле `/etc/hosts`. См. раздел [Network configuration (Русский)#Установка имени узла](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_имени_узла "Network configuration (Русский)") для получения информации о настройке.

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

### Не появляется запрос на сохранение открытых вкладок

C официального сайта [поддержки Mozilla](https://support.mozilla.com/ru/questions/767751):

1.  Введите `about:config` в адресную строку.
2.  Задайте значение `true` параметру `browser.warnOnQuit`.
3.  Задайте значение `true` параметру `browser.showQuitWarning`.

## Смотрите также

*   [Официальный веб-сайт](https://www.mozilla.org/ru/firefox/)
*   [Mozilla Foundation](https://www.mozilla.org/ru/)
*   [MozillaWiki:Firefox](https://wiki.mozilla.org/Firefox "mozillawiki:Firefox")
*   [Дополнения для Firefox](https://addons.mozilla.org/ru/firefox/)
*   [Темы для Firefox](https://addons.mozilla.org/ru/firefox/themes/)
*   [Wikipedia:ru:Mozilla Firefox](https://en.wikipedia.org/wiki/ru:Mozilla_Firefox "wikipedia:ru:Mozilla Firefox")
*   [mozillaZine](http://forums.mozillazine.org/) — Неофициальный форум