# xmodmap (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Ссылки по теме

*   [Xorg (Русский)](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)")
*   [Extra keyboard keys (Русский)](/index.php/Extra_keyboard_keys_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Extra keyboard keys (Русский)")
*   [Extra Keyboard Keys in Xorg (Русский)](/index.php/Extra_Keyboard_Keys_in_Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Extra Keyboard Keys in Xorg (Русский)")
*   [Extra keyboard keys in console](/index.php/Extra_keyboard_keys_in_console "Extra keyboard keys in console")
*   [Xbindkeys (Русский)](/index.php/Xbindkeys_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xbindkeys (Русский)")

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

_xmodmap_ - это утилита для изменения раскладки клавиш клавиатуры и мыши в [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)").

_xmodmap_ не относится к [X KeyBoard extension](/index.php/X_KeyBoard_extension "X KeyBoard extension") (XKB), так как использует другие (pre-XKB) идеи на то, как _коды клавиш_ обрабатываются в X. В целом, он рекомендуется только для простых задач. Смотрите [X KeyBoard extension](/index.php/X_KeyBoard_extension "X KeyBoard extension") для продвинутой настройки раскладки.

## Contents

*   [1 Введение](#.D0.92.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Таблица назначений клавиш](#.D0.A2.D0.B0.D0.B1.D0.BB.D0.B8.D1.86.D0.B0_.D0.BD.D0.B0.D0.B7.D0.BD.D0.B0.D1.87.D0.B5.D0.BD.D0.B8.D0.B9_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88)
*   [4 Изменение таблицы](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.82.D0.B0.D0.B1.D0.BB.D0.B8.D1.86.D1.8B)
    *   [4.1 Активация изменённой таблицы при загрузке](#.D0.90.D0.BA.D1.82.D0.B8.D0.B2.D0.B0.D1.86.D0.B8.D1.8F_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D1.91.D0.BD.D0.BD.D0.BE.D0.B9_.D1.82.D0.B0.D0.B1.D0.BB.D0.B8.D1.86.D1.8B_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5)
    *   [4.2 Попробовать изменения](#.D0.9F.D0.BE.D0.BF.D1.80.D0.BE.D0.B1.D0.BE.D0.B2.D0.B0.D1.82.D1.8C_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F)
*   [5 Клавиши-модификаторы](#.D0.9A.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8-.D0.BC.D0.BE.D0.B4.D0.B8.D1.84.D0.B8.D0.BA.D0.B0.D1.82.D0.BE.D1.80.D1.8B)
*   [6 Прокрутка в другую сторону](#.D0.9F.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B0_.D0.B2_.D0.B4.D1.80.D1.83.D0.B3.D1.83.D1.8E_.D1.81.D1.82.D0.BE.D1.80.D0.BE.D0.BD.D1.83)
*   [7 Примеры](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B)
    *   [7.1 Испанский](#.D0.98.D1.81.D0.BF.D0.B0.D0.BD.D1.81.D0.BA.D0.B8.D0.B9)
    *   [7.2 Вместо CapsLock Control, а вместо LeftControl Hyper](#.D0.92.D0.BC.D0.B5.D1.81.D1.82.D0.BE_CapsLock_Control.2C_.D0.B0_.D0.B2.D0.BC.D0.B5.D1.81.D1.82.D0.BE_LeftControl_Hyper)
*   [8 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Введение

В [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)") есть два типа значений клавиатуры: _коды клавиш (keycodes)_ и _символы клавиш (keysyms)_.

keycode

_Код клавиши_ (keycode) - это числовое значение, получаемое ядром при нажатии клавиши клавиатуры или мыши.

keysym

_Символ клавиши_ (keysym) - это значение, назначенное _коду клавиши_. Например, нажатие клавиши `A` генерирует `keycode 73`, которому назначен `keysym 0×61`, которому в свою очередь назначен символ `A` в таблице [ASCII](https://en.wikipedia.org/wiki/ru:ASCII "wikipedia:ru:ASCII").

_Символами клавиш_ (keysyms) управляет [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)") с помощью таблицы _кодов клавиш_ (keycodes), определяющей пару _keycode_-_keysym_, которая называется [таблицей назначений клавиш](#.D0.A2.D0.B0.D0.B1.D0.BB.D0.B8.D1.86.D0.B0_.D0.BD.D0.B0.D0.B7.D0.BD.D0.B0.D1.87.D0.B5.D0.BD.D0.B8.D0.B9_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88). Её можно увидеть, выполнив команду `xmodmap`.

## Установка

_xmodmap_ можно [установить](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") с помощью пакета [xorg-xmodmap](https://www.archlinux.org/packages/?name=xorg-xmodmap) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Если хотите, можете установить [xkeycaps](https://www.archlinux.org/packages/?name=xkeycaps) - это графический фронт-энд для _xmodmap_.

## Таблица назначений клавиш

Чтобы отобразить текущую таблицу назначений клавиш, форматированную в выражения:

 `$ xmodmap -pke` 

```
[...]
keycode  57 = n N
[...]
```

Каждому столбцу _символов клавиш_ в таблице соответствует определённая комбинация клавиш-модификаторов:

1.  `Key`
2.  `Shift+Key`
3.  `mode_switch+Key`
4.  `mode_switch+Shift+Key`
5.  `AltGr+Key`
6.  `AltGr+Shift+Key`

После каждого _кода клавиши_ идут _символы клавиши_, которые ему назначены. На примере выше видно, что _коду клавиши_ `57` назначен символ нижнего регистра `n`, а символу верхнего регистра `N` назначен _код клавиши_ `57` плюс `Shift`.

Не обязательно назначать все _символы клавиши_; чтобы не назначать их в конкретных столбцах, можете использовать значение `NoSymbol`.

Чтобы узнать какой _код клавиши_ отвечает за нужную вам клавишу, прочтите статью о [дополнительных клавишах](/index.php/Extra_keyboard_keys_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A0.D0.B5.D0.B6.D0.B8.D0.BC_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D0.BA.D0.B8 "Extra keyboard keys (Русский)"), в которой объясняется как использовать утилиту _xev_.

**Совет:** Существуют предопределённые описательные _символы клавиш_ для мультимедиа кнопок, например `XF86AudioMute` или `XF86Mail`. Узнать от таких _символах клавиш_ вы можете из файла `/usr/include/X11/XF86keysym.h`. Многие мультимедиа программы изначально разработаны так, чтобы работать с такими _символами клавиш_ из коробки, без необходимости каких-либо настроек.

## Изменение таблицы

Сохраним текущую таблицу назначений клавиш в файл (i.e. `~/.Xmodmap`):

```
$ xmodmap -pke > ~/.Xmodmap

```

Можете убрать строки для клавиш, которые вы не собираетесь менять. Прописав/узменив нужные значения клавишам , применим изменения:

```
$ xmodmap ~/.Xmodmap

```

### Активация изменённой таблицы при загрузке

Если вы используете [GDM](/index.php/GDM "GDM"), [XDM](/index.php/XDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "XDM (Русский)") или [KDM](/index.php/KDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDM (Русский)"), вам нет необходимости указывать `~/.Xmodmap`. А если вы пользуетесь [startx](/index.php/Startx "Startx"), внесите следующее содержимое в файл `~/.xinitrc`:

 `~/.xinitrc` 

```
if [ -s ~/.Xmodmap ]; then
    xmodmap ~/.Xmodmap
fi
```

Другим вариантом является редактирование глобального скрипта автозапуска `/etc/X11/xinit/xinitrc`.

### Попробовать изменения

Чтобы сделать временные изменения:

```
$ xmodmap -e "keycode  46 = l L l L lstroke Lstroke lstroke"
$ xmodmap -e "keysym a = e E"

```

## Клавиши-модификаторы

_xmodmap_ также умеет переопределять [клавиши-модификаторы](https://en.wikipedia.org/wiki/Modifier_key "wikipedia:Modifier key"), например, можно "поменять местами" клавиши `Control` и `Super`.

Перед тек как назначать клавишу-модификатор, её надо очистить. `!` является комментированием, так что в следующем примере будут очищены только клавиши `Control` и `Mod4`. Затем _символы клавиш_ `Control_L`, `Control_R`, `Super_L` и `Super_R` переназначены на противоположные. Переназначение как левой, так и правой клавиш на один и тот же модификатор означает, что обе клавиши будут функционировать одинаково.

 `~/.Xmodmap` 

```
[...]
!clear Shift
!clear Lock
clear Control
!clear Mod1
!clear Mod2
!clear Mod3
clear Mod4
!clear Mod5
!add Shift   = Shift_L Shift_R
!add Lock    = Caps_Lock
add Control = Super_L Super_R
!add Mod1    = Alt_L Alt_R
!add Mod2    = Mode_switch
!add Mod3    =
add Mod4    = Control_L Control_R
!add Mod5    =
```

**Обратите внимание:** Пример подразумевает, что символы клавиш `Control_L` и `Control_R` были назначены на модификаторе `Control`, а символы клавиш `Super_L` и `Super_R` на модификатор `Mod4`. Если у вас возникает ошибка `X Error of failed request: BadValue (integer parameter out of range for operation)`, вы должны адаптировать таблицу соответствующе. Команда `xmodmap` покажет список модификаторов и клавиш, назначенных на них.

## Прокрутка в другую сторону

Иногда такую прокрутку называют _естественной_. Она похожа на поведение прокрутки на смартфонах. Добиться такого поведения можно с помощью xmodmap. Так как драйвер synaptics использует кнопки 4/5/6/7 для прокрутки вверх/вниз/влево/вправо, вы просто можете поменять порядок объявления кнопок в файле `~/.Xmodmap`:

 `~/.Xmodmap`  `pointer = 1 2 3 **5 4** 7 6 8 9 10 11 12` 

Теперь примените изменения:

```
$ xmodmap ~/.Xmodmap

```

## Примеры

### Испанский

 `~/.Xmodmap` 

```
keycode  24 = a A aacute Aacute ae AE ae
keycode  26 = e E eacute Eacute EuroSign cent EuroSign
keycode  30 = u U uacute Uacute downarrow uparrow downarrow
keycode  31 = i I iacute Iacute rightarrow idotless rightarrow
keycode  32 = o O oacute Oacute oslash Oslash oslash
keycode  57 = n N ntilde Ntilde n N n
keycode  58 = comma question comma questiondown dead_acute dead_doubleacute dead_acute
keycode  61 = exclam section exclamdown section dead_belowdot dead_abovedot dead_belowdot
!Maps the Mode key to the Alt key
keycode 64 = Mode_switch

```

### Вместо CapsLock Control, а вместо LeftControl Hyper

Некоторые пользователи ноутбуков предпочитают, чтобы `CapsLock` работал как `Control`. А клавиша `Left Hyper` может быть использоваться в качестве клавиши-модификатора.

 `~/.Xmodmap` 

```
clear      lock 
clear   control
clear      mod1
clear      mod2
clear      mod3
clear      mod4
clear      mod5
keycode      37 = Hyper_L
keycode      66 = Control_L
add     control = Control_L Control_R
add        mod1 = Alt_L Alt_R Meta_L
add        mod2 = Num_Lock
add        mod3 = Hyper_L
add        mod4 = Super_L Super_R
add        mod5 = Mode_switch ISO_Level3_Shift

```

## Смотрите также

*   [Current man page](http://www.x.org/archive/current/doc/man/man1/xmodmap.1.xhtml) at X.Org Foundation
*   [Multimediakeys with .Xmodmap HOWTO](http://cweiske.de/howto/xmodmap/allinone.html) by Christian Weiske
*   [Mapping unsupported keys with xmodmap](http://dev-loki.blogspot.com/2006/04/mapping-unsupported-keys-with-xmodmap.html) by Pascal Bleser
*   [List of Keysyms Recognised by Xmodmap](http://wiki.linuxquestions.org/wiki/List_of_Keysyms_Recognised_by_Xmodmap) on [LinuxQuestions](http://linuxquestions.org)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Xmodmap_(Русский)&oldid=416986](https://wiki.archlinux.org/index.php?title=Xmodmap_(Русский)&oldid=416986)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Keyboards (Русский)](/index.php/Category:Keyboards_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Keyboards (Русский)")
*   [X server (Русский)](/index.php/Category:X_server_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:X server (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")