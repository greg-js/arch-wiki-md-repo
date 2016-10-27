## Contents

*   [1 Об этой статье](#.D0.9E.D0.B1_.D1.8D.D1.82.D0.BE.D0.B9_.D1.81.D1.82.D0.B0.D1.82.D1.8C.D0.B5)
*   [2 Настройка локали](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D0.B8)
*   [3 Настройка консоли](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BA.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D0.B8)
*   [4 Настройка X.org](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_X.org)
    *   [4.1 Настройки клавиатуры](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
        *   [4.1.1 Модель клавиатуры](#.D0.9C.D0.BE.D0.B4.D0.B5.D0.BB.D1.8C_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
        *   [4.1.2 Опции раскладок](#.D0.9E.D0.BF.D1.86.D0.B8.D0.B8_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA)
        *   [4.1.3 Переключение раскладок](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA)
        *   [4.1.4 Переключение раскладок средствами X.org](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA_.D1.81.D1.80.D0.B5.D0.B4.D1.81.D1.82.D0.B2.D0.B0.D0.BC.D0.B8_X.org)
    *   [4.2 Compose-последовательности](#Compose-.D0.BF.D0.BE.D1.81.D0.BB.D0.B5.D0.B4.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D0.B8)
*   [5 Настройка GTK1](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_GTK1)
*   [6 Настройка ncurses приложений](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_ncurses_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [6.1 Midnight Commander (mc)](#Midnight_Commander_.28mc.29)
    *   [6.2 nano](#nano)
    *   [6.3 ncmpc](#ncmpc)
    *   [6.4 dialog](#dialog)
*   [7 Настройка русских man-страниц](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.80.D1.83.D1.81.D1.81.D0.BA.D0.B8.D1.85_man-.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B8.D1.86)
*   [8 Сделаем openoffice русским](#.D0.A1.D0.B4.D0.B5.D0.BB.D0.B0.D0.B5.D0.BC_openoffice_.D1.80.D1.83.D1.81.D1.81.D0.BA.D0.B8.D0.BC)
*   [9 Перекодировка тегов MP3](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0_.D1.82.D0.B5.D0.B3.D0.BE.D0.B2_MP3)

## Об этой статье

Эта статья рассказывает о том, как настроить отображение и ввод русского языка в Arch Linux.

## Настройка локали

В файле /etc/locale.gen раскомментируйте следующую строку:

```
ru_RU.UTF-8   UTF-8

```

Создайте выбранную вами локаль командой:

```
/usr/sbin/locale-gen

```

Проверьте, что все заявленные локали были созданы:

```
locale -a

```

## Настройка консоли

Несколько слов о том как работает консоль.

Любой вывод программы перенаправляется консольному драйверу в ядре. Ядро работает только в кодировке unicode. Если программа не использует utf-8 для вывода текста, необходима таблица ACM (Application Character Map), которая будет выполнять соответствующее преобразование из 8-битной кодироки в unicode. Если используется пакет kbd (в arch он устанавливается по умолчанию), то эту таблицу можно найти по адресу /usr/share/kbd/consoletrans.

Далее ядро должно отобразить символ на экране. Таблица соответствия знаков шрифта кодам unicode называется SFM (Screen Font Map). Она либо находится внутри шрифта (в большинстве случаев), либо подгружается дополнительно (из /usr/share/kbd/unimaps). Сами шрифты располагаются в /usr/share/kbd/consolefonts.

Кроме этого, нужна ещё клавиатурная раскладка - таблица по переводу скан-кодов клавиатуры в нужный код символа (соответственно может быть либо старая 8-битная либо новая unicode).

Таким образом, работа по настройке консоли разбивается на пункты (рассмотрен utf вариант):

1.  Найти нормальную клавиатурную раскладку, поддерживающую unicode и ваши любимые способы переключения языков и указать её как KEYMAP="..." в файле /etc/vconsole.conf.
2.  Установить экранный шрифт, имеющий встроенную таблицу SFM и приличное начертание: FONT="..." в файле /etc/vconsole.conf.
3.  Убедиться что необходимость в ACM пропадает (CONSOLEMAP="" - остаётся пустым) в файле /etc/vconsole.conf.

Вся остальная работа по настройке kbd (типа использования утилит loadkeys и setfont) уже сделана известными людьми, написавшими стартовые файлы системы.

Пакет kbd поддерживает русские раскладки в utf8\. Дополнительные раскладки клавиатуры можно получить, установив пакет kbd-ru-keymaps командой

```
pacman -S kbd-ru-keymaps

```

или cкачав одну из раскладкок вручную:

*   [Русская UTF-8 раскладка клавиатуры с переключением по правой клавише Alt](http://mlclm.narod.ru/ru-utf.map.gz)
*   [Русская UTF-8 раскладка клавиатуры с переключением по Ctrl-Shift](http://moose.ylsoftware.com/gentoo.ru/ru-mab.map.gz)

и поместив их в каталог `/usr/share/kbd/keymaps/i386/qwerty`

Установите шрифт Terminus из репозитория [community]:

```
pacman -S terminus-font

```

Отредактируйте файл /etc/vconsole.conf:

```
LOCALE="ru_RU.UTF-8"
KEYMAP="ru" # Или ru-mab для раскладки с переключением по Ctrl-Shift
FONT="ter-v16v" # Можно поэкспериментировать с другими шрифтами ter-v* из /usr/share/kbd/consolefonts
CONSOLEMAP=""

```

Обратите внимание, что поиск шрифта происходит в `/usr/share/kbd/consolefonts`.

Можно обойтись и без terminus, установив:

```
CONSOLEFONT="cyr-sun16"

```

**Примечание:** Значение `LOCALE=` может быть как `"ru_RU.UTF-8"`, так и `"ru_RU.utf-8"` или `"ru_RU.utf8"`. Но, с целью уменьшения путаницы, все же лучше использовать вариант `LOCALE="ru_RU.UTF-8"`.

Можно обойтись без установки пакета kbd-ru-keymaps, вариант с переключением по Ctrl+Shift:

```
LOCALE="ru_RU.UTF-8"
HARDWARECLOCK="UTC"
TIMEZONE="Europe/Moscow"
KEYMAP="ru"
CONSOLEFONT="cyr-sun16"
CONSOLEMAP=""
USECOLOR="yes"

```

**Примечание:** Текущая версия [initscripts](https://www.archlinux.org/packages/?name=initscripts) не требует наличия в `rc.conf` переменной *LOCALE*. Тем не менее необходимо внести в файл `/etc/locale.conf` следующие строки:

```
LANG=ru_RU.UTF-8
LC_MESSAGES=ru_RU.UTF-8

```

Учитывая, что теперь установка консольных шрифтов и раскладки вынесена из `/etc/rc.sysinit`, в некоторых случаях, для корректного отображения шрифтов в консоли, Вам потребуется добавить хуки и регенерировать образ ядра. Для этого список хуков в файле `/etc/mkinitcpio.conf` необходимо привести примерно к следующему виду:

```
HOOKS="base consolefont keymap udev <Ваши хуки>"

```

то есть, вставить два дополнительных хука **consolefont** и **keymap**. После чего регенерировать образ ядра:

```
# mkinitcpio -p linux

```

и перезагрузить машину.

**Примечание:** Если вышеперечисленные способы не помогли изменить шрифт в tty, вероятно, изменения не сохраняются после KMS. Для обхода этой проблемы. попробуйте добавить в initrd модуль, выполняющий modesetting (nouveau/radeon/i915 и т.п.): `MODULES="nouveau"` 

## Настройка X.org

Установите шрифты [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) и [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) из репозитория [community]:

```
pacman -S ttf-dejavu ttf-liberation

```

### Настройки клавиатуры

**Примечание:** Начиная с версии Xorg 1.8, [HAL](/index.php/HAL "HAL") не используется для настройки

Создайте файл /etc/hal/fdi/policy/10-keymap.fdi такого содержания:

```
<?xml version="1.0" encoding="utf-8"?>
<deviceinfo version="0.2">
 <device>
  <match key="info.capabilities" contains="input.keypad">
    <merge key="input.xkb.rules" type="string">base</merge>
    <merge key="input.xkb.model" type="string">pc105</merge>
    <merge key="input.x11_driver" type="string">evdev</merge>
    <merge key="input.xkb.layout" type="string">us,ru</merge>
    <merge key="input.xkb.variant" type="string">,winkeys</merge>
    <merge key="input.xkb.options" type="string">grp:rctrl_toggle</merge>
  </match>
 </device>
</deviceinfo>

```

Это простой пример, подходящий для владельцев стандартных устройств ввода. Для владельцев ноутбуков, подключающих, допустим, выносную клавиатуру, правила будут сложнее.

#### Модель клавиатуры

Модель Вашей клавиатуры указана в ключе input.xkb.model. Различные значения для этого ключа можно увидеть в `/usr/share/X11/xkb/rules/evdev.lst`. В данном примере модель pc105 - стандартная клавиатура. Например, для клавиатуры Logitech Generic Keyboard строка примет вид:

```
<merge key="input.xkb.model" type="string">logitech_base</merge>

```

#### Опции раскладок

Параметры *xkb.layout* и *xkb.variant* указывают соответственно на варианты раскладки. В примере раскладки *us,ru* дополнены опцией *winkeys* которая расставляет знаки препинания и некоторые символы в соответствии с раскладкой win.

#### Переключение раскладок

Для настройки переключения между двумя раскладками, используйте опцию значение ключа input.xkb.options. В примере переключение осуществляется по правому Ctrl. Другой пример: раскладки переключаются комбинацией Ctrl-Shift, при использовании русской раскладки горит лампочка Scroll Lock, строка опций должна выглядеть следующим образом:

```
<merge key="input.xkb.options" type="string">grp:ctrl_shift_toggle,grp_led:scroll</merge>

```

Возможно будет удобно использовать <Menu> для переключения раскладок и поменять CapsLock и левый Ctrl. Тогда нужно написать так:

```
<merge key="input.xkb.options" type="string">grp:menu_toggle,grp_led:scroll,ctrl:swapcaps</merge>

```

#### Переключение раскладок средствами X.org

Описано на странице [Xorg (Русский)](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B "Xorg (Русский)")

### Compose-последовательности

С помощью клавиши «Compose» можно вводить практически все варианты символов с акцентами, а также разные специальные символы, например кавычки или тире «—», которых нет в стандартных раскладках. Для этого

*   Добавьте в xorg.conf опцию

```
Option "XkbOptions" "compose:menu"

```

*   Присвойте переменным окружения GTK_IM_MODULE и QT_IM_MODULE значение xim. Если этот шаг пропустить, все последующие настройки на GTK приложения распространяться не будут (они будут использовать свой метод ввода).
*   После этого можно создать в домашнем каталоге файл `~/.XCompose`. Первой его строчкой можно включить все стандартные комбинации клавиш:

```
include "/usr/share/X11/locale/en_US.UTF-8/Compose"

```

	а затем можно и задать любые дополнительные последовательности (по образцу как в `/usr/share/X11/locale/en_US.UTF-8/Compose`). Например,

```
<Multi_key> <period> <space> : "…" U2026 # HORIZONTAL ELLIPSIS, многоточие
<Multi_key> <apostrophe> <apostrophe> : "́" U0301 # ударение

```

После этого стало возможным набирать много интересных символов, нажимая вначале клавишу Compose, а потом набирая ту или короткую иную последовательность. Например,

	Compose + O + C даёт © (символ авторского права),

	Compose + O + R даёт ®

[Полный список последовательностей.](http://webcvs.freedesktop.org/xorg/xc/nls/Compose/en_US.UTF-8?view=co) Пример .XCompose:

 `.XCompose` 
```
# -*- coding: utf-8 -*-
#
# .XCompose
#
# $Id: .XCompose,v 1.31 2008/09/18 17:57:14 deskpot Exp $

#
# Quotation marks
#
<Multi_key> <Cyrillic_be>       : "«"   guillemotleft  # LEFT DOUBLE ANGLE QUOTATION
<Multi_key> <comma>             : "«"   guillemotleft  # LEFT DOUBLE ANGLE QUOTATION
<Multi_key> <Cyrillic_yu>       : "»"   guillemotright # RIGHT DOUBLE ANGLE QUOTATION
<Multi_key> <period>            : "»"   guillemotright # RIGHT DOUBLE ANGLE QUOTATION
<Multi_key> <Cyrillic_BE>       : "„"   U201e # DOUBLE LOW-9 QUOTATION MARK
<Multi_key> <less>              : "„"   U201e # DOUBLE LOW-9 QUOTATION MARK
<Multi_key> <Cyrillic_YU>       : "“"   U201c # LEFT DOUBLE QUOTATION MARK
<Multi_key> <greater>           : "“"   U201c # LEFT DOUBLE QUOTATION MARK
#
<Multi_key> <Cyrillic_zhe>      : "‘"   U2018 # LEFT SINGLE QUOTATION MARK
<Multi_key> <semicolon>         : "‘"   U2018 # LEFT SINGLE QUOTATION MARK
<Multi_key> <Cyrillic_e>        : "’"   U2019 # RIGHT SINGLE QUOTATION MARK
<Multi_key> <apostrophe>        : "’"   U2019 # RIGHT SINGLE QUOTATION MARK
<Multi_key> <Cyrillic_ZHE>      : "“"   U201c # LEFT DOUBLE QUOTATION MARK
<Multi_key> <colon>             : "“"   U201c # LEFT DOUBLE QUOTATION MARK
<Multi_key> <Cyrillic_E>        : "”"   U201d # RIGHT DOUBLE QUOTATION MARK
<Multi_key> <quotedbl>          : "”"   U201d # RIGHT DOUBLE QUOTATION MARK

#
# Dashes
#
<Multi_key> <minus>             : "—"   emdash       # EM DASH
<Multi_key> <underscore>        : "–"   endash       # EN DASH

#
# Currencies
#
<Multi_key> <Cyrillic_u>        : "€"   EuroSign     # EURO SIGN
<Multi_key> <e>                 : "€"   EuroSign     # EURO SIGN
<Multi_key> <Cyrillic_a>        : "£"   sterling     # POUND SIGN
<Multi_key> <f>                 : "£"   sterling     # POUND SIGN

#
# Trademarks
#
<Multi_key> <Cyrillic_es>       : "©"   copyright    # COPYRIGHT SIGN
<Multi_key> <c>                 : "©"   copyright    # COPYRIGHT SIGN
<Multi_key> <Cyrillic_ka>       : "®"   registered   # REGISTERED SIGN
<Multi_key> <r>                 : "®"   registered   # REGISTERED SIGN
<Multi_key> <Cyrillic_ie>       : "™"   U2122        # TRADE MARK SIGN
<Multi_key> <t>                 : "™"   U2122        # TRADE MARK SIGN

#
# Math
#
<Multi_key> <Cyrillic_ef>       : "≈"   approximate  # ALMOST EQUAL TO
<Multi_key> <a>                 : "≈"   approximate  # ALMOST EQUAL TO
<Multi_key> <5>                 : "‰"   U2030        # PER MILLE SIGN
<Multi_key> <equal>             : "≠"   U2260        # NOT EQUAL TO
<Multi_key> <plus>              : "±"   plusminus    # PLUS-MINUS SIGN

#
# Misc. typographics
#
<Multi_key> <Cyrillic_yeru>     : "§"   section      # SECTION SIG
<Multi_key> <s>                 : "§"   section      # SECTION SIGN
<Multi_key> <Cyrillic_shcha>    : "°"   degree       # DEGREE SIGN
<Multi_key> <o>                 : "°"   degree       # DEGREE SIGN
<Multi_key> <space>             : " "   nobreakspace # NO-BREAK SPACE
<Multi_key> <Cyrillic_ve>       : "…"   ellipsis     # HORIZONTAL ELLIPSIS
<Multi_key> <d>                 : "…"   ellipsis     # HORIZONTAL ELLIPSIS

#
# Missing keys in Russian layout
#
<Multi_key> <3>                 : "#"   numbersign   # NUMBER SIGN
<Multi_key> <4>                 : "$"   dollar       # DOLLAR SIGN
<Multi_key> <Cyrillic_ha>       : "["   bracketleft  # LEFT SQUARE BRACKET
<Multi_key> <Cyrillic_hardsign> : "]"   bracketright # RIGHT SQUARE BRACKET

#
# Bindings to ease usage with the Russian `typewriter' layout.
# NB: Unable to bind dollar symbol to be Compose+4, it's Compose+Shift+4.
#
<Multi_key> <2>                 : "—"   emdash       # EM DASH
<Multi_key> <8>                 : "–"   endash       # EN DASH
<Multi_key> <slash>             : "#"   numbersign   # NUMBER SIGN
<Multi_key> <percent>           : "‰"   U2030        # PER MILLE SIGN
<Multi_key> <bar>               : "±"   plusminus    # PLUS-MINUS SIGN

```

## Настройка GTK1

Отредактируйте файл

 `/etc/gtk/gtkrc.ru` 
```
style "gtk-default-ru" {
       fontset = "-*-arial-medium-r-normal--12-*-*-*-*-*-iso10646-1",\
       -*-fixed-medium-r-*-*-14-*-*-*-*-*-iso10646-1"
}

```

class "GtkWidget" style "gtk-default-ru"

## Настройка ncurses приложений

### Midnight Commander (mc)

Пакет [mc](https://www.archlinux.org/packages/?name=mc) с версией 4.6.1-5 из репозитория [extra]
При старом срезе - пакет из репозитория **community** mc-utf8.
Теперь mc собран с поддержкой юникодной локали и имеет приличный вид.

### nano

С версии 2.0 nano поддерживает utf-8.

### ncmpc

В репозитории extra пакет ncmpc 0.11.1 собран с ncurses без поддержки unicode, а также файл руссификации почему-то в кодировке ISO-8859-1\. Решение:

*   Скачайте из AUR архив
*   Переместите его в **/var/abs/local/** (если вы используете ABS) или в любую другую директорию
*   Разархивируйте **tar -xzf ncmpc-svn.tar.gz**
*   Перейдите в получившуюся директорию
*   Выполните **makepkg -i**

### dialog

Некоторые скрипты (например, alsaconf) используют программу dialog для вывода сообщений. Чтобы включить в ней поддержку юникода, поставьте пакет dialog-w из community или пересобирите с опцией `--with-ncursesw`

## Настройка русских man-страниц

Установите русские страницы командой

```
 pacman -S man-pages-ru

```

Также позаботьтесь о том, чтобы переменная окружения *LESSCHARSET* имела значение *UTF-8*, либо просто заккоментируйте строку **export LESSCHARSET="latin1"** в файле */etc/profile*, тогда less будет автоматически брать кодировку из локали.

## Сделаем openoffice русским

Все просто. Поддержка языков в openoffice реализуется отдельными пакетами. Смотрим список пакетов:

```
 pacman -Ss openoffice

```

Ставим поддержку русского языка

```
 pacman -S openoffice-ru

```

## Перекодировка тегов MP3

Установите пакет mutagen:

```
 pacman -S mutagen

```

В каталоге с вашей коллекцией mp3 файлов выполните команду:

```
 find -iname '*.mp3' -print0 | xargs -0 mid3iconv -eCP1251 --remove-v1

```

Команда перекодирует старые теги из кодировки CP1251 в UTF8, запишет тег версии id3v2.4 и удалит теги первой версии.

Минус способа: не все проигрыватели из ОС Windows понимают теги формата 2.4\. Поведение при этом различное: от игнорирования тега, до ругани на битый файл.

Hint: в mpd после этого нужно перечитать список проигрывания, например так:

```
 mpc update (дождитесь завершения, статус можно смотреть запуская mpc без параметров)
 mpc clear
 mpc listall | mpc add

```

Опционально:

```
 mpc rm all
 mpc save all

```