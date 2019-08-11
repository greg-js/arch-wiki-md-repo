Эта статья рассказывает о настройке отображения и ввода русского языка в Arch Linux.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Настройка локали](#Настройка_локали)
*   [2 Настройка консоли](#Настройка_консоли)
*   [3 Настройка X.org](#Настройка_X.org)
    *   [3.1 Настройки клавиатуры](#Настройки_клавиатуры)
        *   [3.1.1 Переключение раскладок средствами X.org](#Переключение_раскладок_средствами_X.org)
    *   [3.2 Compose-последовательности](#Compose-последовательности)
*   [4 Настройка русских man-страниц](#Настройка_русских_man-страниц)
*   [5 Русификация LibreOffice](#Русификация_LibreOffice)
*   [6 Перекодировка тегов MP3](#Перекодировка_тегов_MP3)

## Настройка локали

Раскомментируйте следующую строку в файле `/etc/locale.gen`:

```
ru_RU.UTF-8   UTF-8

```

Создайте выбранную локаль данной командой:

```
/usr/sbin/locale-gen

```

Проверьте, что все заявленные локали были созданы:

```
locale -a

```

## Настройка консоли

Несколько слов о работе консоли.

Любой вывод программы перенаправляется консольному драйверу в ядре. Ядро работает только в кодировке Unicode. Если программа не использует UTF-8 для вывода текста, необходима таблица ACM (Application Character Map), которая будет выполнять соответствующее преобразование из 8-битной кодировки в Unicode. Эту таблицу можно найти в директории `/usr/share/kbd/consoletrans`, если используется пакет [kbd](https://www.archlinux.org/packages/?name=kbd) (в Arch установлен по умолчанию).

Далее ядро должно отобразить символ на экране. Таблица соответствия знаков шрифта кодам Unicode называется SFM (Screen Font Map). Она либо находится внутри шрифта (в большинстве случаев), либо подгружается дополнительно (из `/usr/share/kbd/unimaps`). Сами шрифты располагаются в `/usr/share/kbd/consolefonts`.

Кроме этого, также необходима клавиатурная раскладка — таблица по переводу скан-кодов клавиатуры в нужный код символа (соответственно, может быть либо старая 8-битная, либо новая Unicode).

Таким образом, настройка консоли разбивается на следующие пункты (рассмотрен вариант с UTF):

1.  Поиск клавиатурной раскладки, поддерживающей Unicode и необходимые способы переключения языков, а также указание её как `KEYMAP="..."` в файле `/etc/vconsole.conf`.
2.  Установка шрифта, имеющего встроенную таблицу SFM и необходимое начертание: `FONT="..."` в файле `/etc/vconsole.conf`.
3.  Проверка, что необходимость в ACM пропадает (`CONSOLEMAP=""` остаётся пустым) в файле `/etc/vconsole.conf`.

Вся остальная работа по настройке kbd (например, использование утилит `loadkeys` и `setfont`) уже сделана людьми, написавшими стартовые файлы системы.

Пакет [kbd](https://www.archlinux.org/packages/?name=kbd) поддерживает русские раскладки в UTF-8\. Дополнительные раскладки клавиатуры можно получить, [установив](/index.php/Help:Reading_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_пакетов "Help:Reading (Русский)") пакет [kbd-ru-keymaps](https://aur.archlinux.org/packages/kbd-ru-keymaps/).

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [terminus-font](https://www.archlinux.org/packages/?name=terminus-font) для получения шрифта Terminus.

Отредактируйте файл `/etc/vconsole.conf`:

```
LOCALE="ru_RU.UTF-8"
KEYMAP="ru" # Или ru-mab для раскладки с переключением по Ctrl+Shift или ruwin_alt_sh-UTF-8 для переключение по Alt+Shift
FONT="ter-v16n" # Можно поэкспериментировать с другими шрифтами ter-v* из /usr/share/kbd/consolefonts
CONSOLEMAP=""
```

Если возникают проблемы со шрифтом ter-v16n, воспользуйтесь конфигурацией файла `/etc/vconsole.conf`, приведённой ниже:

```
LOCALE=ru_RU.UTF-8
KEYMAP=ru
FONT=ter-u16b
CONSOLEMAP=
TIMEZONE=Europe/Moscow
HARDWARECLOCK=UTC
USECOLOR=yes
```

Обратите внимание, что поиск шрифта происходит в `/usr/share/kbd/consolefonts`.

Можно обойтись без Terminus, установив:

```
CONSOLEFONT="cyr-sun16"

```

**Примечание:** Значение `LOCALE=` может быть как `"ru_RU.UTF-8"`, так и `"ru_RU.utf-8"` или `"ru_RU.utf8"`. Но, с целью уменьшения путаницы, все же лучше использовать вариант `LOCALE="ru_RU.UTF-8"`.

Можно обойтись без установки пакета [kbd-ru-keymaps](https://aur.archlinux.org/packages/kbd-ru-keymaps/), вариант с переключением по `Ctrl+Shift`:

```
LOCALE="ru_RU.UTF-8"
HARDWARECLOCK="UTC"
TIMEZONE="Europe/Moscow"
KEYMAP="ru"
CONSOLEFONT="cyr-sun16"
CONSOLEMAP=""
USECOLOR="yes"

```

**Примечание:** Внесите в файл `/etc/locale.conf` следующую строку: `LANG=ru_RU.UTF-8` 

Также в некоторых случаях, для корректного отображения шрифтов в консоли, потребуется добавить хуки и пересоздать образ ядра. Для этого список хуков в файле `/etc/mkinitcpio.conf` необходимо привести примерно к следующему виду:

```
HOOKS="base consolefont keymap udev <ваши хуки>"

```

то есть вставить два дополнительных хука **consolefont** и **keymap**.

После чего пересоздать образ ядра:

```
# mkinitcpio -p linux

```

и перезагрузить систему.

**Примечание:** Если вышеперечисленные способы не помогли изменить шрифт в tty, вероятно, изменения не сохраняются после KMS. Попробуйте добавить в initrd модуль, выполняющий modesetting (nouveau/radeon/i915 и т.п.): `MODULES="nouveau"` 

## Настройка X.org

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакеты [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) и [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) для получения шрифтов DejaVu и Liberation соответственно.

### Настройки клавиатуры

Клавиатура настраивается при помощи [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"), а точнее, [localectl](/index.php/Locale_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_локали "Locale (Русский)"). При настройке Xorg утилита считывает и изменяет файл `00-keyboard.conf`:

```
$ cat /etc/X11/xorg.conf.d/00-keyboard.conf 
# Read and parsed by systemd-localed. It's probably wise not to edit this file
# manually too freely.
Section "InputClass"
        Identifier "system-keyboard"
        MatchIsKeyboard "on"
	Option "XkbLayout" "us,ru"
	Option "XkbModel" "pc105"
	Option "XkbVariant" "os_winkeys"
	Option "XKbOptions" "grp:menu_toggle,grp_led:scroll,ctrl:swapcaps,compose:ralt"
EndSection

```

Это значит, что `localectl` нужен root, а Xorg придется перезапускать.

Посмотреть возможные значения:

```
 $ localectl list-x11-keymap-models
 $ localectl list-x11-keymap-layouts
 $ localectl list-x11-keymap-variants ru
 $ localectl list-x11-keymap-options

```

#### Переключение раскладок средствами X.org

См. статью [Конфигурация клавиатуры в Xorg](/index.php/%D0%9A%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D1%8F_%D0%BA%D0%BB%D0%B0%D0%B2%D0%B8%D0%B0%D1%82%D1%83%D1%80%D1%8B_%D0%B2_Xorg "Конфигурация клавиатуры в Xorg").

### Compose-последовательности

См. раздел [Конфигурация клавиатуры в Xorg#Настройка клавиши Compose](/index.php/%D0%9A%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D1%8F_%D0%BA%D0%BB%D0%B0%D0%B2%D0%B8%D0%B0%D1%82%D1%83%D1%80%D1%8B_%D0%B2_Xorg#Настройка_клавиши_Compose "Конфигурация клавиатуры в Xorg").

## Настройка русских man-страниц

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [man-pages-ru](https://aur.archlinux.org/packages/man-pages-ru/) с русскими страницами.

`man` показывает страницы ориентируясь на локаль. Для принудительного показа русских страниц используйте следующую команду:

```
 $ man -L ru <manpage>

```

## Русификация LibreOffice

Поддержка языков в LibreOffice реализуется отдельными пакетами.

См. список пакетов:

```
 $ pacman -Ss libreoffice | grep \\-ru
 extra/libreoffice-fresh-ru 5.3.0-1
 extra/libreoffice-still-ru 5.2.5-1

```

После чего установите LibreOffice необходимой версии с русской локализацией.

## Перекодировка тегов MP3

Установите пакет [python-mutagen](https://www.archlinux.org/packages/?name=python-mutagen) и выполните следующую команду в каталоге с коллекцией MP3-файлов:

```
 find -iname '*.mp3' -print0 | xargs -0 mid3iconv -eCP1251 --remove-v1

```

Команда перекодирует старые теги из кодировки CP1251 в UTF8, запишет тег версии id3v2.4 и удалит теги первой версии.

**Примечание:** Не все проигрыватели из ОС Windows понимают теги формата 2.4\. Поведение при этом различное: от игнорирования тега, до ошибки о повреждённом файле.

**Примечание:** В [mpd](/index.php/Music_Player_Daemon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Music Player Daemon (Русский)") после этого необходимо перечитать список проигрывания, например:
```
mpc update (дождитесь завершения, статус можно смотреть запуская mpc без параметров)
mpc clear
mpc listall 
```

Опционально:

```
mpc rm all
mpc save all

```