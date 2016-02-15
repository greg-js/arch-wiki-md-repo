**Состояние перевода:** На этой странице представлен перевод статьи [X resources](/index.php/X_resources "X resources"). Дата последней синхронизации: 5 октября 2015\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=X_resources&diff=0&oldid=403404).

**Xresources** - это настраиваемый на уровне пользователя _dotfile_ ("точкафайл", [dotfiles](/index.php/Dotfiles "Dotfiles")), как правило, находящийся по пути `~/.Xresources`. Он может быть использован для установки [ресурсов X](https://en.wikipedia.org/wiki/X_resources "wikipedia:X resources"), параметров настроек для клиентских приложений X.

Они может сделать много операций, в том числе:

*   определить цвета терминала
*   настроить предпочтения терминала
*   задать DPI монитора, сглаживание (antialiasing), хинтование (hinting) и другие настройки шрифтов X
*   изменить тему Xcursor
*   установить тему xscreensaver
*   изменять предпочтения низкоуровневых приложений X (xclock ([xorg-xclock](https://www.archlinux.org/packages/?name=xorg-xclock)), [xpdf](https://aur.archlinux.org/packages/xpdf/), [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode), и т.д.)

**Обратите внимание:** Устарело использование `~/.Xdefaults`, так что эта статья будет относиться только к ресурсам, загруженных с xrdb xrdb

## Contents

*   [1 Начинаем](#.D0.9D.D0.B0.D1.87.D0.B8.D0.BD.D0.B0.D0.B5.D0.BC)
    *   [1.1 Разбор .Xresources](#.D0.A0.D0.B0.D0.B7.D0.B1.D0.BE.D1.80_.Xresources)
    *   [1.2 Добавление к xinitrc](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA_xinitrc)
    *   [1.3 Настройки по умолчанию](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [1.4 Синтаксис Xresources](#.D0.A1.D0.B8.D0.BD.D1.82.D0.B0.D0.BA.D1.81.D0.B8.D1.81_Xresources)
        *   [1.4.1 Основной синтаксис](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D0.BE.D0.B9_.D1.81.D0.B8.D0.BD.D1.82.D0.B0.D0.BA.D1.81.D0.B8.D1.81)
        *   [1.4.2 Джокер соответствия (Wildcard matching)](#.D0.94.D0.B6.D0.BE.D0.BA.D0.B5.D1.80_.D1.81.D0.BE.D0.BE.D1.82.D0.B2.D0.B5.D1.82.D1.81.D1.82.D0.B2.D0.B8.D1.8F_.28Wildcard_matching.29)
        *   [1.4.3 Комментарии](#.D0.9A.D0.BE.D0.BC.D0.BC.D0.B5.D0.BD.D1.82.D0.B0.D1.80.D0.B8.D0.B8)
        *   [1.4.4 Включение файлов](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2)
*   [2 Примеры использования](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [2.1 Цвета терминала](#.D0.A6.D0.B2.D0.B5.D1.82.D0.B0_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B0)
    *   [2.2 Ресурсы Xcursor](#.D0.A0.D0.B5.D1.81.D1.83.D1.80.D1.81.D1.8B_Xcursor)
    *   [2.3 Ресурсы Xft](#.D0.A0.D0.B5.D1.81.D1.83.D1.80.D1.81.D1.8B_Xft)
    *   [2.4 Ресурсы Xterm](#.D0.A0.D0.B5.D1.81.D1.83.D1.80.D1.81.D1.8B_Xterm)
    *   [2.5 Ресурсы rxvt-unicode (urxvt)](#.D0.A0.D0.B5.D1.81.D1.83.D1.80.D1.81.D1.8B_rxvt-unicode_.28urxvt.29)
    *   [2.6 Предпочтения Aterm](#.D0.9F.D1.80.D0.B5.D0.B4.D0.BF.D0.BE.D1.87.D1.82.D0.B5.D0.BD.D0.B8.D1.8F_Aterm)
    *   [2.7 Ресурсы Xpdf](#.D0.A0.D0.B5.D1.81.D1.83.D1.80.D1.81.D1.8B_Xpdf)
    *   [2.8 Ресурсы Lal clock](#.D0.A0.D0.B5.D1.81.D1.83.D1.80.D1.81.D1.8B_Lal_clock)
    *   [2.9 Предпочтения Xclock](#.D0.9F.D1.80.D0.B5.D0.B4.D0.BF.D0.BE.D1.87.D1.82.D0.B5.D0.BD.D0.B8.D1.8F_Xclock)
    *   [2.10 Ресурсы X11-ssh-askpass](#.D0.A0.D0.B5.D1.81.D1.83.D1.80.D1.81.D1.8B_X11-ssh-askpass)
    *   [2.11 Ресурсы XScreenSaver](#.D0.A0.D0.B5.D1.81.D1.83.D1.80.D1.81.D1.8B_XScreenSaver)
    *   [2.12 Ресурсы Xcalc](#.D0.A0.D0.B5.D1.81.D1.83.D1.80.D1.81.D1.8B_Xcalc)
*   [3 Команды цветовой схемы](#.D0.9A.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D1.8B_.D1.86.D0.B2.D0.B5.D1.82.D0.BE.D0.B2.D0.BE.D0.B9_.D1.81.D1.85.D0.B5.D0.BC.D1.8B)
    *   [3.1 Показать все 256 цветов](#.D0.9F.D0.BE.D0.BA.D0.B0.D0.B7.D0.B0.D1.82.D1.8C_.D0.B2.D1.81.D0.B5_256_.D1.86.D0.B2.D0.B5.D1.82.D0.BE.D0.B2)
    *   [3.2 Показать выход кодов tput](#.D0.9F.D0.BE.D0.BA.D0.B0.D0.B7.D0.B0.D1.82.D1.8C_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4_.D0.BA.D0.BE.D0.B4.D0.BE.D0.B2_tput)
    *   [3.3 Перечисление цветов, поддерживаемые терминалами](#.D0.9F.D0.B5.D1.80.D0.B5.D1.87.D0.B8.D1.81.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.86.D0.B2.D0.B5.D1.82.D0.BE.D0.B2.2C_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B0.D0.BC.D0.B8)
    *   [3.4 Перечислить возможности терминала](#.D0.9F.D0.B5.D1.80.D0.B5.D1.87.D0.B8.D1.81.D0.BB.D0.B8.D1.82.D1.8C_.D0.B2.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D0.BE.D1.81.D1.82.D0.B8_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B0)
*   [4 Цветные схемы скриптов](#.D0.A6.D0.B2.D0.B5.D1.82.D0.BD.D1.8B.D0.B5_.D1.81.D1.85.D0.B5.D0.BC.D1.8B_.D1.81.D0.BA.D1.80.D0.B8.D0.BF.D1.82.D0.BE.D0.B2)
    *   [4.1 Скрипт #1](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D1.82_.231)
    *   [4.2 Скрипт #2](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D1.82_.232)
    *   [4.3 Скрипт #3](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D1.82_.233)
    *   [4.4 Скрипт #4](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D1.82_.234)
    *   [4.5 Скрипт #5](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D1.82_.235)
    *   [4.6 Скрипт #6](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D1.82_.236)
    *   [4.7 Скрипт #7](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D1.82_.237)
*   [5 Представленные примеры](#.D0.9F.D1.80.D0.B5.D0.B4.D1.81.D1.82.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B)
*   [6 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [6.1 Ошибки чтения (парсинга) файла ~/.Xresources](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B8_.D1.87.D1.82.D0.B5.D0.BD.D0.B8.D1.8F_.28.D0.BF.D0.B0.D1.80.D1.81.D0.B8.D0.BD.D0.B3.D0.B0.29_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.7E.2F.Xresources)
*   [7 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Начинаем

Убедитесь, что пакет [xorg-xrdb](https://www.archlinux.org/packages/?name=xorg-xrdb) установлен на вашей системе.

### Разбор .Xresources

Файл `~/.Xresources` не существует по умолчанию. Это обычный текстовый файл, вы можете создавать и редактировать его с помощью любого текстового редактора. После создания, он будет "разобран" на программы `xrdb` (базы данных ресурсов Xorg) автоматически, при условии что вы либо:

*   используете [Экранный менеджер (менеджер входа)](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)") чтобы войти в X. Большинство Экранных Менеджеров будут автоматически загружать файл `~/.Xresources` на входе в систему.
*   если вы используете `startx`, вы должны отредактировать `~/.[xinitrc](/index.php/Xinitrc "Xinitrc")`. Для подробностей, смотрите ниже.

Ресурсы будут сохранены в X-сервере, так что файл не должен читаться каждый раз, когда приложение запускается.

Чтобы перечитать ваш файл .Xresources, и удалить старые ресурсы:

```
xrdb ~/.Xresources

```

Чтобы перечитать ваш файл .Xresources, и сохранить старые ресурсы:

```
xrdb -merge ~/.Xresources

```

**Совет:** `~/.Xresources` это просто условное название; xrdb может загрузить любой файл. Если вы используете вручную xrdb, вы можете поместить этот файл в любом месте, где захотите (например, `~/.config/Xresources`).

**Обратите внимание:** Ресурсы загруженные с xrdb также доступны в _удалённых_ клиентах X11 (таких как перенаправление на SSH).

**Важно:**

*   Если вы в фоне выполняете xrdb в цепи команд `~/.xinitrc`, программы запущенные в той же цепи, не могут использовать его, так что рекомендуется _никогда_ не запускать в фоне команды xrdb в `~/.xinitrc`.
*   Старый и устаревший файл `~/.Xdefaults` читается каждый раз при запуске программ X11 таких как `xterm`, но **только** если `xrdb` "никогда" не был использован в текущем сеансе X. [[1]](https://groups.google.com/forum/#!msg/comp.windows.x/hQBEdql8l-Q/hF3DETcIHGwJ)

### Добавление к xinitrc

Если вы не используете [Среду рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)"), добавьте следующую строку в [xinitrc](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)"):

```
[[ -f ~/.Xresources ]] && xrdb -merge -I$HOME ~/.Xresources

```

### Настройки по умолчанию

Для просмотра настроек по умолчанию для установленных приложений X11, смотрите `/usr/share/X11/app-defaults/`.

Подробная информация о конкретных программных ресурсах, как правило, предоставляется на страницах руководства программ (man). Хорошим примером является руководство xterm, так как оно содержит список ресурсов Х и их значения по умолчанию.

Чтобы увидеть текущие загружены ресурсы:

```
xrdb -query -all

```

### Синтаксис Xresources

#### Основной синтаксис

Синтаксис файла Xresources заключается в следующем:

```
**name.Class.resource: value** (**имя.Класс.ресурс: значение**)

```

а вот реальный пример:

```
xscreensaver.Dialog.headingFont: -*-fixed-bold-r-*-*-*-100-*-*-*-*-iso8859-1

```

	name (имя)

	Название приложения, такое как Xterm, Xpdf и т.д.

	class (класс)

	Классификация используется для объединения ресурсов вместе. Имена классов, как правило, в верхнем регистре.

	resource (ресурс)

	Название ресурса, значение которого должно быть изменено. Ресурсы как правило в нижнем регистре, а для объединения в верхнем.

	value (значение)

	Фактическое значение ресурса. Это может быть 1 из 3-х типов:

*   Integer (целые числа)
*   Boolean (true/false, yes/no, on/off (т.е. верно/неверно, да/нет, вкл/выкл)
*   String (строка символов) (например слово (`white`), цвет (`#ffffff`), или путь (`/usr/bin/firefox`))

	delimiters (разделители)

	Точка (`**.**`) используется для обозначения каждого шага вниз по иерархии  —  в приведенном выше примере мы начали с **name**, затем спустились до **Class**, и наконец до самого **resource**. Двоеточие (`**:**`) используется, чтобы отделить описание ресурса от фактического значения.

#### Джокер соответствия (Wildcard matching)

Звездочка (`*****`) может использоваться в качестве шаблона, что облегчает использование одного правила , которое может быть применено ко многим различным приложениям или элементам.

Воспользуемся предыдущим примером, если вы хотите применить тот же шрифт для всех программ (не только для XScreenSaver) которые содержат имя класса `Dialog`, и которое содержит имя ресурса `headingFont`, можно записать так:

```
*****Dialog.headingFont:     -*-fixed-bold-r-*-*-*-100-*-*-*-*-iso8859-1

```

Если вы хотите применить это правило для всех программ, которые содержат ресурс `headingFont`, независимо от его класса, вы должны написать:

```
*****headingFont:    -*-fixed-bold-r-*-*-*-100-*-*-*-*-iso8859-1

```

#### Комментарии

Чтобы добавить комментарий в файле Xresources, просто воспользуйтесь префиксом с воскрицательным знаком (`!`), например:

```
! Следующее правило будет игнорироваться, поскольку оно было закомментировано
!Xft.antialias:        true

```

#### Включение файлов

Чтобы использовать различные файлы для каждого приложения, используйте `#include` в главном файле. Например:

 `~/.Xresources` 

```
#include ".Xresources.d/xterm"
#include ".Xresources.d/rxvt-unicode"
#include ".Xresources.d/fonts"
#include ".Xresources.d/xscreensaver"

```

Если файлы не удалось загрузить, укажите каталог для _xrdb_ с параметром `-I`. Например:

 `~/.xinitrc` 

```
xrdb -I_$HOME_ ~/.Xresources

```

## Примеры использования

Следующие образцы должны помочь понять какие настройки приложения могут быть изменены с помощью файла Xresources. Для получения подробной информации, обратитесь к справочной странице (man) приложения.

### Цвета терминала

Большинство терминалов, в том числе [xterm](/index.php/Xterm_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xterm (Русский)") и [urxvt](/index.php/Urxvt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Urxvt (Русский)"), поддерживают по крайней мере 16 базовых цветов. Ниже приведён пример 16-цветовой гаммы. Цвета 0-7 представляют собой 'нормальные' цвета, а цвета 8-15 их 'яркие' дубликаты, используемые, например, для выделения. Хорошим началом для создания вашего Xresources, будет установка цветов терминала по умолчанию:

```
! Цвета терминала ------------------------------------------------------------

! Схема tangoesque 
*background: #111111
*foreground: #babdb6
! Black (not tango) + DarkGrey (Чёрный (не танго)+ТёмноСерый)
*color0:  #000000
*color8:  #555753
! DarkRed + Red (ТёмноКрасный+Красный)
*color1:  #ff6565
*color9:  #ff8d8d
! DarkGreen + Green (ТёмноЗелёный+Зелёный)
*color2:  #93d44f
*color10: #c8e7a8
! DarkYellow + Yellow (ТёмноЖёлтый+Жёлтый)
*color3:  #eab93d
*color11: #ffc123
! DarkBlue + Blue (ТёмноСиний+Синий)
*color4:  #204a87
*color12: #3465a4
! DarkMagenta + Magenta (ТёмноПурпурный+Пурпурный)
*color5:  #ce5c00
*color13: #f57900
!DarkCyan + Cyan (both not tango) (ТёмноГолубой+Голубой (оба не танго))
*color6:  #89b6e2
*color14: #46a4ff
! LightGrey + White (СветлоСерый+Белый)
*color7:  #cccccc
*color15: #ffffff

```

Смотрите [man page (Русский)#Цветные страницы в xterm или rxvt-unicode](/index.php/Man_page_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A6.D0.B2.D0.B5.D1.82.D0.BD.D1.8B.D0.B5_.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B8.D1.86.D1.8B_.D0.B2_xterm_.D0.B8.D0.BB.D0.B8_rxvt-unicode "Man page (Русский)") о том как xterm и rxvt автоматически "раскрашивает" **полужирный** и <u>подчеркнутый</u> текст.

Дополнительные примеры цветовых схем, смотрите в разделе [#Представленные примеры](#.D0.9F.D1.80.D0.B5.D0.B4.D1.81.D1.82.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B) (нижней части этой статьи).

### Ресурсы Xcursor

Установите тему и размер вашего курсора мыши:

```
! Xcursor --------------------------------------------------------------------

Xcursor.theme: Vanilla-DMZ-AA
Xcursor.size:  22

```

Доступные темы хранятся в `/usr/share/icons` и местные (только для конкретного пользователя) темы могут быть установлены из `~/.icons`.

### Ресурсы Xft

Вы можете определить основные ресурсы шрифта без файла `fonts.conf` или среды рабочего стола.

**Обратите внимание:** Тем не менее, использование среды рабочего стола и/или `fonts.conf` может изменить эти настройки.

Вашим лучшим выбором будет использование одного из них, но не обеих сразу.

```
! Xft settings ---------------------------------------------------------------

Xft.dpi:        96
Xft.antialias:  true
Xft.rgba:       rgb
Xft.hinting:    true
Xft.hintstyle:  hintslight

```

### Ресурсы Xterm

Следующие ресурсы откроют [xterm](/index.php/Xterm_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xterm (Русский)") с размером окна 80x25 символов, полосой прокрутки и возможностью прокрутки последних 512 линий. Указанное семейство шрифтов по имени [Terminus](/index.php/Fonts#Bitmap "Fonts") является популярным и "чистым" шрифтом для терминала.

```
! xterm ----------------------------------------------------------------------

xterm*VT100.geometry:     80x25
xterm*faceName:           Terminus:style=Regular:size=10
!xterm*font:              -*-dina-medium-r-*-*-16-*-*-*-*-*-*-*
xterm*dynamicColors:      true
xterm*utf8:               2
xterm*eightBitInput:      true
xterm*saveLines:          512
xterm*scrollKey:          true
xterm*scrollTtyOutput:    false
xterm*scrollBar:          true
xterm*rightScrollBar:     true
xterm*jumpScroll:         true
xterm*multiScroll:        true
xterm*toolBar:            false

```

### Ресурсы rxvt-unicode (urxvt)

[rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) предоставляет большой список доступных опций, которые можно настраивать при помощи файла `~/.Xresources`. Для получения дополнительной информации обратитесь к странице справочного руководства (man) _urxvt_ или разделу [rxvt-unicode (Русский)#Создание ~/.Xresources](/index.php/Rxvt-unicode_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.7E.2F.Xresources "Rxvt-unicode (Русский)").

### Предпочтения Aterm

Примеры настройки для Aterm (очень похожие на urxvt):

```
!aterm settings-------------------------------------------------------------     

aterm*background:               black
aterm*foreground:               white
aterm*transparent:              true
aterm*shading:                  30
aterm*cursorColor:              gray
aterm*saveLines:                2000
!aterm*tinting:                 gray
aterm*scrollBar:                false
!aterm*scrollBar_right:          true
aterm*transpscrollbar:          true
aterm*borderwidth:              0
aterm*font:                     -*-terminus-*-*-*-*-*-*-*-*-*-*-*-*
aterm*geometry:                 80x25
!aterm*fading:                  70  

```

### Ресурсы Xpdf

Ниже приведены некоторые основные ресурсы для [xpdf](https://aur.archlinux.org/packages/xpdf/), легковесного приложения для просмотра PDF:

```
! xpdf -----------------------------------------------------------------------

xpdf*enableFreetype:    yes
xpdf*antialias:         yes
xpdf*foreground:        black
xpdf*background:        white
xpdf*urlCommand:        /usr/bin/firefox %s

```

Больше информации чем указано выше, лежит в `~/.xpdfrc`. Для подробной информации смотрите страницу man xpdf. Обратите внимание, что `viKeys` устарела.

### Ресурсы Lal clock

```
! lal clock ------------------------------------------------------------------

lal*font:       Arial
lal*fontsize:   12
lal*bold:       true
lal*color:      #ffffff
lal*width:      150
lal*format:     %a %b %d %l:%M%P

```

### Предпочтения Xclock

Некоторые основные настройки Xclock. Смотрите справочную страницу Xclock для всех ресурсов X.

```
! xclock ---------------------------------------------------------------------

xclock*update:            1
xclock*analog:            false
xclock*Foreground:        white
xclock*background:        black

```

### Ресурсы X11-ssh-askpass

```
! x11-ssh-askpass ------------------------------------------------------------

x11-ssh-askpass*font:                   -*-dina-medium-r-*-*-12-*-*-*-*-*-*-*
x11-ssh-askpass*background:             #000000
x11-ssh-askpass*foreground:             #ffffff
x11-ssh-askpass.Button*background:      #000000
x11-ssh-askpass.Indicator*foreground:   #ff9900
x11-ssh-askpass.Indicator*background:   #090909
x11-ssh-askpass*topShadowColor:         #000000
x11-ssh-askpass*bottomShadowColor:      #000000
x11-ssh-askpass.*borderWidth:           1

```

### Ресурсы XScreenSaver

Ниже приведен пример темы [XScreenSaver](/index.php/XScreenSaver "XScreenSaver"). Для большей информации, посетите страницу man XScreenSaver.

**Обратите внимание:** В старых версиях XScreenSaver, если файл `~/.xscreensaver` существует, то он переопределяет любые настройки в базе данных X ресурсов. Тем не менее, в последних версиях вы можете использовать оба одновременно.

```
! xscreensaver ---------------------------------------------------------------

!Настройки шрифта
xscreensaver.Dialog.headingFont:        -*-dina-bold-r-*-*-12-*-*-*-*-*-*-*
xscreensaver.Dialog.bodyFont:           -*-dina-medium-r-*-*-12-*-*-*-*-*-*-*
xscreensaver.Dialog.labelFont:          -*-dina-medium-r-*-*-12-*-*-*-*-*-*-*
xscreensaver.Dialog.unameFont:          -*-dina-medium-r-*-*-12-*-*-*-*-*-*-*
xscreensaver.Dialog.buttonFont:         -*-dina-bold-r-*-*-12-*-*-*-*-*-*-*
xscreensaver.Dialog.dateFont:           -*-dina-medium-r-*-*-12-*-*-*-*-*-*-*
xscreensaver.passwd.passwdFont:         -*-dina-bold-r-*-*-12-*-*-*-*-*-*-*
!Общее диалоговое окно (влияет на текст: hostname, username, и password )
xscreensaver.Dialog.foreground:         #ffffff
xscreensaver.Dialog.background:         #111111
xscreensaver.Dialog.topShadowColor:     #111111
xscreensaver.Dialog.bottomShadowColor:  #111111
xscreensaver.Dialog.Button.foreground:  #666666
xscreensaver.Dialog.Button.background:  #ffffff
!username/password окно ввода и цвет текста date
xscreensaver.Dialog.text.foreground:    #666666
xscreensaver.Dialog.text.background:    #ffffff
xscreensaver.Dialog.internalBorderWidth:24
xscreensaver.Dialog.borderWidth:        20
xscreensaver.Dialog.shadowThickness:    2
!Бар таймаута (background фактически определяется Dialog.text.background)
xscreensaver.passwd.thermometer.foreground:  #ff0000
xscreensaver.passwd.thermometer.background:  #000000
xscreensaver.passwd.thermometer.width:       8
!Формат штампа даты -- смотрите руководство для уточнения деталей strftime(3)
xscreensaver.dateFormat:    %I:%M%P %a %b %d, %Y

```

### Ресурсы Xcalc

Ниже приведены некоторые ресурсы Xcalc, раскрашивающие и настраивающие кнопки.

```
!xcalc-----------------------------------------------------------------------

xcalc*geometry:                        200x275
xcalc.ti.bevel.background:             #111111
xcalc.ti.bevel.screen.background:      #000000
xcalc.ti.bevel.screen.DEG.background:  #000000
xcalc.ti.bevel.screen.DEG.foreground:  LightSeaGreen
xcalc.ti.bevel.screen.GRAD.background: #000000
xcalc.ti.bevel.screen.GRAD.foreground: LightSeaGreen
xcalc.ti.bevel.screen.RAD.background:  #000000
xcalc.ti.bevel.screen.RAD.foreground:  LightSeaGreen
xcalc.ti.bevel.screen.INV.background:  #000000
xcalc.ti.bevel.screen.INV.foreground:  Red
xcalc.ti.bevel.screen.LCD.background:  #000000
xcalc.ti.bevel.screen.LCD.foreground:  LightSeaGreen
xcalc.ti.bevel.screen.LCD.shadowWidth: 0
xcalc.ti.bevel.screen.M.background:    #000000
xcalc.ti.bevel.screen.M.foreground:    LightSeaGreen
xcalc.ti.bevel.screen.P.background:    #000000
xcalc.ti.bevel.screen.P.foreground:    Yellow
xcalc.ti.Command.foreground:  White
xcalc.ti.Command.background:  #777777
xcalc.ti.button5.background:  Orange3
xcalc.ti.button19.background: #611161
xcalc.ti.button18.background: #611161
xcalc.ti.button20.background: #611111
!Расскомментируйте для изменения метки division button
!xcalc.ti.button20.label:      /
xcalc.ti.button25.background: #722222
xcalc.ti.button30.background: #833333
xcalc.ti.button35.background: #944444
xcalc.ti.button40.background: #a55555
xcalc.ti.button22.background: #222262
xcalc.ti.button23.background: #222262
xcalc.ti.button24.background: #222272
xcalc.ti.button27.background: #333373
xcalc.ti.button28.background: #333373
xcalc.ti.button29.background: #333373
xcalc.ti.button32.background: #444484
xcalc.ti.button33.background: #444484
xcalc.ti.button34.background: #444484
xcalc.ti.button37.background: #555595
xcalc.ti.button38.background: #555595
xcalc.ti.button39.background: #555595
XCalc*Cursor:                 hand2
XCalc*ShapeStyle:             rectangle

```

## Команды цветовой схемы

Вот некоторые команды Баш, которые вы можете быстро выполнить прямо в оболочке.

### Показать все 256 цветов

Очень быстро вывести все 256 цветов на экран.

```
(x=`tput op` y=`printf %76s`;for i in {0..256};do o=00$i;echo -e ${o:${#o}-3:3} `tput setaf $i;tput setab $i`${y// /=}$x;done)

```

### Показать выход кодов tput

Замените `tput op` на тот tput который вы хотите проследить. По умолчанию `op` это цвет переднего плана (например текста) и заднего плана (фон).

```
$ ( strace -s5000 -e write tput op 2>&2 2>&1 ) | tee -a /dev/stderr | grep -o '"[^"]*"'

```

```
033[\033[1;34m"\33[39;49m"\033[00m

```

### Перечисление цветов, поддерживаемые терминалами

Следующая команда позволит вам узнать все ваши терминалы с поддержкой terminfo, и число цветов поддерживаемых каждым терминалом. Возможные значения: 8, 15, 16, 52, 64, 88 и 256.

```
$ for T in `find /usr/share/terminfo -type f -printf '%f '`;do echo "$T `tput -T $T colors`";done|sort -nk2

```

```
Eterm-88color 88
rxvt-88color 88
xterm+88color 88
xterm-88color 88
Eterm-256color 256
gnome-256color 256
konsole-256color 256
putty-256color 256
rxvt-256color 256
screen-256color 256
screen-256color-bce 256
screen-256color-bce-s 256
screen-256color-s 256
xterm+256color 256
xterm-256color 256

```

### Перечислить возможности терминала

Эта команда полезна, чтобы увидеть функции, которые поддерживаются вашим терминалом.

```
$ infocmp -1 | sed -nu 's/^[ \000\t]*//;s/[ \000\t]*$//;/[^ \t\000]\{1,\}/!d;/acsc/d;s/=.*,//p'|column -c80

```

```
bel	cuu	ich	kb2	kf15	kf3	kf44	kf59	mc0	rmso	smul
blink	cuu1	il	kbs	kf16	kf30	kf45	kf6	mc4	rmul	tbc
bold	cvvis	il1	kcbt	kf17	kf31	kf46	kf60	mc5	rs1	u6
cbt	dch	ind	kcub1	kf18	kf32	kf47	kf61	meml	rs2	u7
civis	dch1	indn	kcud1	kf19	kf33	kf48	kf62	memu	sc	u8
clear	dl	initc	kcuf1	kf2	kf34	kf49	kf63	op	setab	u9
cnorm	dl1	invis	kcuu1	kf20	kf35	kf5	kf7	rc	setaf	vpa

```

## Цветные схемы скриптов

Любой из следующих скриптов будет отображать график вашей текущей цветовой гаммы терминала. Это удобно для тестирования и еще много чего.

### Скрипт #1

```
#!/usr/bin/bash
#
#   This file echoes a bunch of color codes to the 
#   terminal to demonstrate what's available.  Each 
#   line is the color code of one foreground color,
#   out of 17 (default + 16 escapes), followed by a 
#   test use of that color on all nine background 
#   colors (default + 8 escapes).
#

T='gYw'   # The test text

echo -e "\n                 40m     41m     42m     43m\
     44m     45m     46m     47m";

for FGs in '    m' '   1m' '  30m' '1;30m' '  31m' '1;31m' '  32m' \
           '1;32m' '  33m' '1;33m' '  34m' '1;34m' '  35m' '1;35m' \
           '  36m' '1;36m' '  37m' '1;37m';
  do FG=${FGs// /}
  echo -en " $FGs \033[$FG  $T  "
  for BG in 40m 41m 42m 43m 44m 45m 46m 47m;
    do echo -en "$EINS \033[$FG\033[$BG  $T  \033[0m";
  done
  echo;
done
echo
```

### Скрипт #2

```
#!/usr/bin/bash
# Original: [http://frexx.de/xterm-256-notes/](http://frexx.de/xterm-256-notes/) 
#           [http://frexx.de/xterm-256-notes/data/colortable16.sh](http://frexx.de/xterm-256-notes/data/colortable16.sh) 
# Modified by Aaron Griffin
# and further by Kazuo Teramoto
FGNAMES=(' black ' '  red  ' ' green ' ' yellow' '  blue ' 'magenta' '  cyan ' ' white ')
BGNAMES=('DFT' 'BLK' 'RED' 'GRN' 'YEL' 'BLU' 'MAG' 'CYN' 'WHT')

echo "     ┌──────────────────────────────────────────────────────────────────────────┐"
for b in {0..8}; do
  ((b>0)) && bg=$((b+39))

  echo -en "\033[0m ${BGNAMES[b]} │ "

  for f in {0..7}; do
    echo -en "\033[${bg}m\033[$((f+30))m ${FGNAMES[f]} "
  done

  echo -en "\033[0m │"
  echo -en "\033[0m\n\033[0m     │ "

  for f in {0..7}; do
    echo -en "\033[${bg}m\033[1;$((f+30))m ${FGNAMES[f]} "
  done

  echo -en "\033[0m │"
  echo -e "\033[0m"

  ((b<8)) &&
  echo "     ├──────────────────────────────────────────────────────────────────────────┤"
done
echo "     └──────────────────────────────────────────────────────────────────────────┘"
```

### Скрипт #3

```
#!/usr/bin/bash
# Original: [http://frexx.de/xterm-256-notes/](http://frexx.de/xterm-256-notes/) 
#           [http://frexx.de/xterm-256-notes/data/colortable16.sh](http://frexx.de/xterm-256-notes/data/colortable16.sh) 
# Modified by Aaron Griffin
# and further by Kazuo Teramoto

FGNAMES=(' black ' '  red  ' ' green ' ' yellow' '  blue ' 'magenta' '  cyan ' ' white ')
BGNAMES=('DFT' 'BLK' 'RED' 'GRN' 'YEL' 'BLU' 'MAG' 'CYN' 'WHT')
echo "     ----------------------------------------------------------------------------"
for b in $(seq 0 8); do
    if [ "$b" -gt 0 ]; then
      bg=$(($b+39))
    fi

    echo -en "\033[0m ${BGNAMES[$b]} : "
    for f in $(seq 0 7); do
      echo -en "\033[${bg}m\033[$(($f+30))m ${FGNAMES[$f]} "
    done
    echo -en "\033[0m :"

    echo -en "\033[0m\n\033[0m     : "
    for f in $(seq 0 7); do
      echo -en "\033[${bg}m\033[1;$(($f+30))m ${FGNAMES[$f]} "
    done
    echo -en "\033[0m :"
        echo -e "\033[0m"

  if [ "$b" -lt 8 ]; then
    echo "     ----------------------------------------------------------------------------"
  fi
done
echo "     ----------------------------------------------------------------------------"
```

### Скрипт #4

```
#!/usr/bin/env lua

function cl(e)
	return string.format('\27[%sm', e)
end

function print_fg(bg, pre)
	for fg = 30,37 do
		fg = pre..fg
		io.write(cl(bg), cl(fg), string.format(' %6s ', fg), cl(0))
	end
end

for bg = 40,47 do
	io.write(cl(0), ' ', bg, ' ')
	print_fg(bg, ' ')
	io.write('\n    ')
	print_fg(bg, '1;')
	io.write('\n\n')
end

-- Andres P
```

### Скрипт #5

```
#!/usr/bin/bash
#
# ANSI color scheme script featuring Space Invaders
#
# Original: [http://crunchbang.org/forums/viewtopic.php?pid=126921%23p126921#p126921](http://crunchbang.org/forums/viewtopic.php?pid=126921%23p126921#p126921)
# Modified by lolilolicon
#

f=3 b=4
for j in f b; do
  for i in {0..7}; do
    printf -v $j$i %b "\e[${!j}${i}m"
  done
done
bld=$'\e[1m'
rst=$'\e[0m'

cat << EOF

 $f1  ▀▄   ▄▀     $f2 ▄▄▄████▄▄▄    $f3  ▄██▄     $f4  ▀▄   ▄▀     $f5 ▄▄▄████▄▄▄    $f6  ▄██▄  $rst
 $f1 ▄█▀███▀█▄    $f2███▀▀██▀▀███   $f3▄█▀██▀█▄   $f4 ▄█▀███▀█▄    $f5███▀▀██▀▀███   $f6▄█▀██▀█▄$rst
 $f1█▀███████▀█   $f2▀▀███▀▀███▀▀   $f3▀█▀██▀█▀   $f4█▀███████▀█   $f5▀▀███▀▀███▀▀   $f6▀█▀██▀█▀$rst
 $f1▀ ▀▄▄ ▄▄▀ ▀   $f2 ▀█▄ ▀▀ ▄█▀    $f3▀▄    ▄▀   $f4▀ ▀▄▄ ▄▄▀ ▀   $f5 ▀█▄ ▀▀ ▄█▀    $f6▀▄    ▄▀$rst

 $bld$f1▄ ▀▄   ▄▀ ▄   $f2 ▄▄▄████▄▄▄    $f3  ▄██▄     $f4▄ ▀▄   ▄▀ ▄   $f5 ▄▄▄████▄▄▄    $f6  ▄██▄  $rst
 $bld$f1█▄█▀███▀█▄█   $f2███▀▀██▀▀███   $f3▄█▀██▀█▄   $f4█▄█▀███▀█▄█   $f5███▀▀██▀▀███   $f6▄█▀██▀█▄$rst
 $bld$f1▀█████████▀   $f2▀▀▀██▀▀██▀▀▀   $f3▀▀█▀▀█▀▀   $f4▀█████████▀   $f5▀▀▀██▀▀██▀▀▀   $f6▀▀█▀▀█▀▀$rst
 $bld$f1 ▄▀     ▀▄    $f2▄▄▀▀ ▀▀ ▀▀▄▄   $f3▄▀▄▀▀▄▀▄   $f4 ▄▀     ▀▄    $f5▄▄▀▀ ▀▀ ▀▀▄▄   $f6▄▀▄▀▀▄▀▄$rst

                                     $f7▌$rst

                                   $f7▌$rst

                              $f7    ▄█▄    $rst
                              $f7▄█████████▄$rst
                              $f7▀▀▀▀▀▀▀▀▀▀▀$rst

EOF
```

### Скрипт #6

```
#!/usr/bin/env ruby
# coding: utf-8

# ANSI color scheme script 
# Author: Ivaylo Kuzev < Ivo >
# Original: [http://crunchbang.org/forums/viewtopic.php?pid=134749%23p134749#p134749](http://crunchbang.org/forums/viewtopic.php?pid=134749%23p134749#p134749)
# Modified using Ruby.

CL = "\e[0m"
BO = "\e[1m"

R = "\e[31m" 
G = "\e[32m"
Y = "\e[33m"
B = "\e[34m"
P = "\e[35m"
C = "\e[36m"

print <<EOF 

#{BO}#{R}  ██████  #{CL} #{BO}#{G}██████  #{CL}#{BO}#{Y}   ██████#{CL} #{BO}#{B}██████ #{CL}  #{BO}#{P}  ██████#{CL} #{BO}#{C}  ███████#{CL}
#{BO}#{R}  ████████#{CL} #{BO}#{G}██    ██ #{CL}#{BO}#{Y}██ #{CL}      #{BO}#{B}██    ██#{CL} #{BO}#{P}██████ #{CL} #{BO}#{C} █████████#{CL}
#{R}  ██  ████#{CL} #{G}██  ████#{CL}#{Y} ████    #{CL} #{B}████  ██#{CL} #{P}████ #{CL}    #{C}█████ #{CL}
#{R}  ██    ██#{CL} #{G}██████ #{CL}#{Y}  ████████#{CL} #{B}██████ #{CL}  #{P}████████#{CL} #{C}██ #{CL}

EOF
```

### Скрипт #7

```
#!/bin/sh
# Original Posted at [http://crunchbang.org/forums/viewtopic.php?pid=126921%23p126921#p126921](http://crunchbang.org/forums/viewtopic.php?pid=126921%23p126921#p126921)
# [ESC] character in original post removed here.

# ANSI Color -- use these variables to easily have different color
#    and format output. Make sure to output the reset sequence after
#    colors (f = foreground, b = background), and use the 'off'
#    feature for anything you turn on.

initializeANSI()
{
 esc="$(echo -en '\e')"

  blackf="${esc}[30m";   redf="${esc}[31m";    greenf="${esc}[32m"
  yellowf="${esc}[33m"   bluef="${esc}[34m";   purplef="${esc}[35m"
  cyanf="${esc}[36m";    whitef="${esc}[37m"

  blackb="${esc}[40m";   redb="${esc}[41m";    greenb="${esc}[42m"
  yellowb="${esc}[43m"   blueb="${esc}[44m";   purpleb="${esc}[45m"
  cyanb="${esc}[46m";    whiteb="${esc}[47m"

  boldon="${esc}[1m";    boldoff="${esc}[22m"
  italicson="${esc}[3m"; italicsoff="${esc}[23m"
  ulon="${esc}[4m";      uloff="${esc}[24m"
  invon="${esc}[7m";     invoff="${esc}[27m"

  reset="${esc}[0m"
}

# note in this first use that switching colors doesn't require a reset
# first - the new color overrides the old one.

#clear

initializeANSI

cat << EOF

 ${yellowf}  ▄███████▄${reset}   ${redf}  ▄██████▄${reset}    ${greenf}  ▄██████▄${reset}    ${bluef}  ▄██████▄${reset}    ${purplef}  ▄██████▄${reset}    ${cyanf}  ▄██████▄${reset}
 ${yellowf}▄█████████▀▀${reset}  ${redf}▄${whitef}█▀█${redf}██${whitef}█▀█${redf}██▄${reset}  ${greenf}▄${whitef}█▀█${greenf}██${whitef}█▀█${greenf}██▄${reset}  ${bluef}▄${whitef}█▀█${bluef}██${whitef}█▀█${bluef}██▄${reset}  ${purplef}▄${whitef}█▀█${purplef}██${whitef}█▀█${purplef}██▄${reset}  ${cyanf}▄${whitef}█▀█${cyanf}██${whitef}█▀█${cyanf}██▄${reset}
 ${yellowf}███████▀${reset}      ${redf}█${whitef}▄▄█${redf}██${whitef}▄▄█${redf}███${reset}  ${greenf}█${whitef}▄▄█${greenf}██${whitef}▄▄█${greenf}███${reset}  ${bluef}█${whitef}▄▄█${bluef}██${whitef}▄▄█${bluef}███${reset}  ${purplef}█${whitef}▄▄█${purplef}██${whitef}▄▄█${purplef}███${reset}  ${cyanf}█${whitef}▄▄█${cyanf}██${whitef}▄▄█${cyanf}███${reset}
 ${yellowf}███████▄${reset}      ${redf}████████████${reset}  ${greenf}████████████${reset}  ${bluef}████████████${reset}  ${purplef}████████████${reset}  ${cyanf}████████████${reset}
 ${yellowf}▀█████████▄▄${reset}  ${redf}██▀██▀▀██▀██${reset}  ${greenf}██▀██▀▀██▀██${reset}  ${bluef}██▀██▀▀██▀██${reset}  ${purplef}██▀██▀▀██▀██${reset}  ${cyanf}██▀██▀▀██▀██${reset}
 ${yellowf}  ▀███████▀${reset}   ${redf}▀   ▀  ▀   ▀${reset}  ${greenf}▀   ▀  ▀   ▀${reset}  ${bluef}▀   ▀  ▀   ▀${reset}  ${purplef}▀   ▀  ▀   ▀${reset}  ${cyanf}▀   ▀  ▀   ▀${reset}

 ${boldon}${yellowf}  ▄███████▄   ${redf}  ▄██████▄    ${greenf}  ▄██████▄    ${bluef}  ▄██████▄    ${purplef}  ▄██████▄    ${cyanf}  ▄██████▄${reset}
 ${boldon}${yellowf}▄█████████▀▀  ${redf}▄${whitef}█▀█${redf}██${whitef}█▀█${redf}██▄  ${greenf}▄${whitef}█▀█${greenf}██${whitef}█▀█${greenf}██▄  ${bluef}▄${whitef}█▀█${bluef}██${whitef}█▀█${bluef}██▄  ${purplef}▄${whitef}█▀█${purplef}██${whitef}█▀█${purplef}██▄  ${cyanf}▄${whitef}█▀█${cyanf}██${whitef}█▀█${cyanf}██▄${reset}
 ${boldon}${yellowf}███████▀      ${redf}█${whitef}▄▄█${redf}██${whitef}▄▄█${redf}███  ${greenf}█${whitef}▄▄█${greenf}██${whitef}▄▄█${greenf}███  ${bluef}█${whitef}▄▄█${bluef}██${whitef}▄▄█${bluef}███  ${purplef}█${whitef}▄▄█${purplef}██${whitef}▄▄█${purplef}███  ${cyanf}█${whitef}▄▄█${cyanf}██${whitef}▄▄█${cyanf}███${reset}
 ${boldon}${yellowf}███████▄      ${redf}████████████  ${greenf}████████████  ${bluef}████████████  ${purplef}████████████  ${cyanf}████████████${reset}
 ${boldon}${yellowf}▀█████████▄▄  ${redf}██▀██▀▀██▀██  ${greenf}██▀██▀▀██▀██  ${bluef}██▀██▀▀██▀██  ${purplef}██▀██▀▀██▀██  ${cyanf}██▀██▀▀██▀██${reset}
 ${boldon}${yellowf}  ▀███████▀   ${redf}▀   ▀  ▀   ▀  ${greenf}▀   ▀  ▀   ▀  ${bluef}▀   ▀  ▀   ▀  ${purplef}▀   ▀  ▀   ▀  ${cyanf}▀   ▀  ▀   ▀${reset}

EOF
```

## Представленные примеры

Проверьте эти ссылки на реальном примере файлов ресурсов X, внесенных членами сообщества.

**Обратите внимание:** `~/.Xdefaults` имеет такой же синтаксис как в `~/.Xresources`, и вам рекомендуется использовать `~/.Xresources` потому что `~/.Xdefaults` устарел в апстриме.

*   [http://dotfiles.org/~buttons/.Xdefaults](http://dotfiles.org/~buttons/.Xdefaults)
*   [https://github.com/jelly/Dotfiles/blob/master/.Xdefaults](https://github.com/jelly/Dotfiles/blob/master/.Xdefaults)
*   [https://paste.debian.net/14515/](https://paste.debian.net/14515/) .Xresources

## Решение проблем

### Ошибки чтения (парсинга) файла ~/.Xresources

[Экранные менеджеры](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)"), такие как [GDM](/index.php/GDM "GDM") и [LightDM](/index.php/LightDM "LightDM"), могут запускать _xrdb_ с опцией `--nocpp`. Смотрите раздел [LightDM#Xresources not being parsed correctly](/index.php/LightDM#Xresources_not_being_parsed_correctly "LightDM").

## Смотрите также

*   [Конфиг:Xresources (Рус.)](http://linuxoid.in/%D0%9A%D0%BE%D0%BD%D1%84%D0%B8%D0%B3:Xresources)
*   [Using the Xdefaults File](https://engineering.purdue.edu/ECN/Support/KB/Docs/UsingTheXdefaultsFil) - Статья с углублением о том, как X интерпретирует файл Xdefaults
*   [Rxvt-unicode Configuration Tutorial](http://wiki.afterstep.org/index.php?title=Rxvt-Unicode_Configuration_Tutorial) - много информации для пользователей urxvt
*   [Example Colors and their names](http://mkaz.com/solog/system/xterm-colors.html) - перечень примеров цветов и названий цветов для xterm и других приложений X.
*   [Color Themes](https://web.archive.org/web/20090130061234/http://phraktured.net/terminal-colors/) - Обширный список цветовых тем для терминала, составленный Phraktured.
*   [Xcolors.net](http://xcolors.net/) Список цветовых тем для терминала, составленных пользователями.
*   [Цвета Х составленные dkeg](http://beta.andrewrcraig.us/index.php?page=xcolors)