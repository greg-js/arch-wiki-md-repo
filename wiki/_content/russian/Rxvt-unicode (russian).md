Related articles

*   [Rxvt-unicode/Советы и хитрости](/index.php/Rxvt-unicode/%D0%A1%D0%BE%D0%B2%D0%B5%D1%82%D1%8B_%D0%B8_%D1%85%D0%B8%D1%82%D1%80%D0%BE%D1%81%D1%82%D0%B8 "Rxvt-unicode/Советы и хитрости")

**Состояние перевода:** На этой странице представлен перевод статьи [Rxvt-unicode](/index.php/Rxvt-unicode "Rxvt-unicode"). Дата последней синхронизации: 29 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Rxvt-unicode&diff=0&oldid=428493).

[rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode.html) это очень настраиваемый [эмулятор терминала](https://en.wikipedia.org/wiki/ru:%D0%AD%D0%BC%D1%83%D0%BB%D1%8F%D1%82%D0%BE%D1%80_%D1%82%D0%B5%D1%80%D0%BC%D0%B8%D0%BD%D0%B0%D0%BB%D0%B0 для того, чтобы свести к минимуму использование системных ресурсов. Некоторые из наиболее выдающихся особенностей rxvt-Unicode включают международную языковую поддержку через [Юникод](https://en.wikipedia.org/wiki/ru:%D0%AE%D0%BD%D0%B8%D0%BA%D0%BE%D0%B4 "wikipedia:ru:Юникод"), способность отображать различные типы шрифтов и поддержку расширений [Perl](https://en.wikipedia.org/wiki/ru:Perl "wikipedia:ru:Perl"). Разработан Марк Леманном и сообществом разработчиков.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Создание ~/.Xresources](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.7E.2F.Xresources)
    *   [2.2 Полоса прокрутки](#.D0.9F.D0.BE.D0.BB.D0.BE.D1.81.D0.B0_.D0.BF.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B8)
    *   [2.3 Позиция полосы прокрутки](#.D0.9F.D0.BE.D0.B7.D0.B8.D1.86.D0.B8.D1.8F_.D0.BF.D0.BE.D0.BB.D0.BE.D1.81.D1.8B_.D0.BF.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B8)
    *   [2.4 Прокрутка буфера в дополнительном экране](#.D0.9F.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B0_.D0.B1.D1.83.D1.84.D0.B5.D1.80.D0.B0_.D0.B2_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D0.BC_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B5)
    *   [2.5 Методы декларации шрифта](#.D0.9C.D0.B5.D1.82.D0.BE.D0.B4.D1.8B_.D0.B4.D0.B5.D0.BA.D0.BB.D0.B0.D1.80.D0.B0.D1.86.D0.B8.D0.B8_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.B0)
    *   [2.6 Расстояние шрифта](#.D0.A0.D0.B0.D1.81.D1.81.D1.82.D0.BE.D1.8F.D0.BD.D0.B8.D0.B5_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.B0)
    *   [2.7 Цвета](#.D0.A6.D0.B2.D0.B5.D1.82.D0.B0)
*   [3 Вырезать и вставить](#.D0.92.D1.8B.D1.80.D0.B5.D0.B7.D0.B0.D1.82.D1.8C_.D0.B8_.D0.B2.D1.81.D1.82.D0.B0.D0.B2.D0.B8.D1.82.D1.8C)
*   [4 Perl расширения](#Perl_.D1.80.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [4.1 Кликабельные ссылки (URL-адреса)](#.D0.9A.D0.BB.D0.B8.D0.BA.D0.B0.D0.B1.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.81.D1.81.D1.8B.D0.BB.D0.BA.D0.B8_.28URL-.D0.B0.D0.B4.D1.80.D0.B5.D1.81.D0.B0.29)
    *   [4.2 Yankable URL'ы (без мыши)](#Yankable_URL.27.D1.8B_.28.D0.B1.D0.B5.D0.B7_.D0.BC.D1.8B.D1.88.D0.B8.29)
    *   [4.3 Простые вкладки](#.D0.9F.D1.80.D0.BE.D1.81.D1.82.D1.8B.D0.B5_.D0.B2.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B8)
    *   [4.4 Полноэкранный](#.D0.9F.D0.BE.D0.BB.D0.BD.D0.BE.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.BD.D1.8B.D0.B9)
    *   [4.5 Поддержка колеса прокрутки](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_.D0.BA.D0.BE.D0.BB.D0.B5.D1.81.D0.B0_.D0.BF.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B8)
    *   [4.6 Изменение размера шрифта на лету](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80.D0.B0_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.B0_.D0.BD.D0.B0_.D0.BB.D0.B5.D1.82.D1.83)
    *   [4.7 Отключение расширений Perl](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D0.B9_Perl)
    *   [4.8 Цвета как в Xterm](#.D0.A6.D0.B2.D0.B5.D1.82.D0.B0_.D0.BA.D0.B0.D0.BA_.D0.B2_Xterm)
*   [5 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [5.1 Настройки ~/.Xresources не применяются](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.7E.2F.Xresources_.D0.BD.D0.B5_.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D0.BD.D1.8F.D1.8E.D1.82.D1.81.D1.8F)
    *   [5.2 Прозрачность не работает после обновления, начиная с версии 9.09](#.D0.9F.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D0.BE.D1.81.D1.82.D1.8C_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F.2C_.D0.BD.D0.B0.D1.87.D0.B8.D0.BD.D0.B0.D1.8F_.D1.81_.D0.B2.D0.B5.D1.80.D1.81.D0.B8.D0.B8_9.09)
    *   [5.3 Удаленные хосты](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D1.85.D0.BE.D1.81.D1.82.D1.8B)
    *   [5.4 Использование rxvt-Unicode в качестве терминала gmrun (Gnome Completion-Run)](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_rxvt-Unicode_.D0.B2_.D0.BA.D0.B0.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.B5_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B0_gmrun_.28Gnome_Completion-Run.29)
    *   [5.5 Моя цифровая клавиатура действует странно и производит странный вывод (например, в VIM)](#.D0.9C.D0.BE.D1.8F_.D1.86.D0.B8.D1.84.D1.80.D0.BE.D0.B2.D0.B0.D1.8F_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D0.B0_.D0.B4.D0.B5.D0.B9.D1.81.D1.82.D0.B2.D1.83.D0.B5.D1.82_.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.BD.D0.BE_.D0.B8_.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D0.B8.D1.82_.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.BD.D1.8B.D0.B9_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4_.28.D0.BD.D0.B0.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D1.80.2C_.D0.B2_VIM.29)
    *   [5.6 pseudo-tty](#pseudo-tty)
    *   [5.7 Горячие клавиши не работают](#.D0.93.D0.BE.D1.80.D1.8F.D1.87.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.82)
    *   [5.8 Низкая производительность при рисовании глифов](#.D0.9D.D0.B8.D0.B7.D0.BA.D0.B0.D1.8F_.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D1.8C_.D0.BF.D1.80.D0.B8_.D1.80.D0.B8.D1.81.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8_.D0.B3.D0.BB.D0.B8.D1.84.D0.BE.D0.B2)
*   [6 Внешние ресурсы](#.D0.92.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.B5_.D1.80.D0.B5.D1.81.D1.83.D1.80.D1.81.D1.8B)

## Установка

[Установите](/index.php/Install "Install") пакет [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode).

## Настройка

Смотрите доступные настройки и значения [urxvt(1)](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.1.pod) и [urxvt(7)](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.7.pod).

### Создание ~/.Xresources

Rxvt-unicode управляется с помощью аргументов командной строки или [ресурсами Х](/index.php/%D0%A0%D0%B5%D1%81%D1%83%D1%80%D1%81%D1%8B_%D0%A5 "Ресурсы Х"). Аргументы командной строки переопределяют, и имеют приоритет над параметрами ресурсов. Смотрите статью [Ресурсы Х](/index.php/%D0%A0%D0%B5%D1%81%D1%83%D1%80%D1%81%D1%8B_%D0%A5 "Ресурсы Х") `urxvt --help` Отобразит все доступные ресурсы *rxvt*. Страница пользовательского руководства man page содержит полное объяснение каждого ресурса.

### Полоса прокрутки

Внешний вид полосы прокрутки может быть выбраны через эту запись в `~/.Xresources`:

```
! стиль полосы прокрутки - rxvt (по умолчанию), plain (самый компактный), next, или xterm
URxvt.scrollstyle: rxvt

```

Полоса прокрутки может быть полностью отключена:

```
URxvt.scrollBar: false

```

### Позиция полосы прокрутки

По умолчанию, когда появляется вывод оболочки, вид прокрутки автоматически переходит к нижней части буфера для отображения нового вывода. Если вы хотите, увидеть предыдущий выход (например, сообщения компилятора), установите следующие параметры в `~/.Xresources`:

```
! Не прокручивать при выводе
URxvt*scrollTtyOutput: false

! прокручивать по отношению к буферу (прокрутка мышью или Shift+Page Up)
URxvt*scrollWithBuffer: true

! прокрутка по нажатию клавиши
URxvt*scrollTtyKeypress: true

```

### Прокрутка буфера в дополнительном экране

Когда вы прокручиваете постранично во *вторичном экране* (например `less` без опции`**-X**`), будет хорошей идеей отключить прокрутку буфера, чтобы иметь возможность прокручивать *именно* постранично *вторичный экран*, а не буфер терминала: это неизменено по умолчанию в терминалах на основе vte. Чтобы отключить буфер прокрутки *второго* экрана в *urxvt*:

```
URxvt.secondaryScreen: 1
URxvt.secondaryScroll: 0

```

Эта настройка работает как и ожидалось, за исключением прокрутки колесом мыши. Когда вы листаете постранично "вторичный экран" колесом мыши - и там было что-то в буфере прокрутки - вместо страницы *вторичного экрана* колесом мыши будет прокручиватся буфер прокрутки. Чтобы решить эту проблему, необходимо ввести новый параметр в rxvt-unicode[[1]](https://bbs.archlinux.org/viewtopic.php?id=132150). Патченный rxvt-unicode доступен в пакете [rxvt-unicode-better-wheel-scrolling](https://aur.archlinux.org/packages/rxvt-unicode-better-wheel-scrolling/). После его установки добавьте следующие строки в файл настроек:

```
URxvt.secondaryWheel: 1

```

**Примечание:** Пожалуйста, не используйте эту опцию с расширением Perl [vtwheel](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_.D0.BA.D0.BE.D0.BB.D0.B5.D1.81.D0.B0_.D0.BF.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B8): это приведёт к беспорядку

### Методы декларации шрифта

```
URxvt.font: 9x15

```

Тоже самое что и:

```
URxvt.font: -misc-fixed-medium-r-normal--15-140-75-75-c-90-iso8859-1

```

И, для того же шрифта bold (толстый):

```
URxvt.font: 9x15bold

```

Тоже самое что и:

```
URxvt.font: -misc-fixed-bold-r-normal--15-140-75-75-c-90-iso8859-1

```

Полный список коротких имен для основных шрифтов Х может быть найден в `/usr/share/fonts/misc/fonts.alias` (также есть файлы fonts.alias в некоторых других подкаталогах `/usr/share/fonts/`, но они упакованы отдельно от реальных шрифтов, и могут перечислять шрифты которые на самом деле не установлены). Стоит отметить, что эти короткие псевдонимы выбираются для версии ISO-8859-1 а не версии ISO-10646-1 (Юникод), и скорее версии 75 DPI чем 100 DPI, так что лучше избегать их, и вместо них выбирать шрифты по полному имени.

**Примечание:** Пункт выше только для растровых шрифтов. Другие шрифты могут быть использованы через Xft, используя следующий формат:

```
URxvt.font: xft:monaco:size=10

```

Или

```
URxvt.font: xft:monaco:bold:size=10

```

**Примечание:**

*   Если есть дефис (-) в имени шрифта Xft, он должен быть экранирован двойным (\). Как в этом примере:

```
URxvt*font: xft:Inconsolata\\-\\dz for Powerline:size=12

```

Это отличается от использования варианта опции urxvt -fn которая возвращает результат fc-list, где (\) указан только один раз.

*   Вы увидите новый шрифт только при перезапуске сервера Х.

Хороший способ для тестирования шрифтов прямо в терминале до совершения изменений в файле настроек, является вывод escape-кодов в терминале, например:

```
$ printf '\e]710;%s\007' "xft:Terminus:pixelsize=12"

```

### Расстояние шрифта

По умолчанию, расстояние между символами слишком широкое. Это контролируется параметром:

 `~/.Xresources` 
```
URxvt.letterSpace: -1

```

Здесь `-1` уменьшается расстояние от одного пикселя, при необходимости можно регулировать.

### Цвета

По умолчанию, rxvt-unicode собран с поддержкой цвета. В дополнении к стандартным цветам переднего плана и цвету фона, rxvt может отображать до 256 цветов (плюс high-intensity bold/blinking/underlined (высокоинтенсивный жирный/мигающий/подчёркнутый) и любое сочетание из них).

Образец `~/.Xresources` для urxvt терминала с цветами по умолчанию, белые шрифты на чёрном фоне написаны как и следует:

 `~/.Xresources` 
```
! Background color
URxvt*background: black

! Цвет шрифта
URxvt*foreground: white

! Другие цвета
URxvt*color0: black
URxvt*color1: red3
URxvt*color2: green3
URxvt*color3: yellow3
URxvt*color4: blue2
URxvt*color5: magenta3
URxvt*color6: cyan3
URxvt*color7: gray90
URxvt*color8: grey50
URxvt*color9: red
URxvt*color10: green
URxvt*color11: yellow
URxvt*color12: blue
URxvt*color13: magenta
URxvt*color14: cyan
URxvt*color15: white
```

Также можно указать значения цветов foreground (передний план/шрифт), background (фон), cursorColor (цвет курсора), cursorColor2 (цвет курсора2), colorBD, colorUL как число 0-15, - удобное сокращение ссылки на цвет color0-color15\. Смотрите [#Создание ~/.Xresources](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.7E.2F.Xresources) для создания комментированного файла `~/.Xresources` для `urxvt`.

## Вырезать и вставить

**Примечание:** При использовании терминального мультиплексора, urxvt (или любой эмулятор терминала) интеграция `CLIPBOARD` не будет эффективной, поскольку будет невозможно выбрать весь нужный текст в прямом режиме или вообще, в некоторых случаях (например, когда активный мультиплексированный терминал меняется на другой, а затем происходит возврат к первоначальному, и один выбирает текст сверх того, что можно видеть, что вызывает текст из другого терминала, который будет отображаться). Очевидно, что это связано с тем, что эмулятор терминала не способен различать мультиплексированные терминалы. Таким образом, было бы излишне эффективно для тех, кто всегда использует терминальный мультиплексор, способный прокручивать буфер прокрутки и интеграцию с `CLIPBOARD` (например [tmux](/index.php/Tmux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Tmux (Русский)") c [индивидуальными горячими клавишами](/index.php/Tmux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9A.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F "Tmux (Русский)")) для интеграции `CLIPBOARD` с urxvt.

Для пользователей, незнакомых с методами передачи данных [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)"), обмен информацией из rxvt-unicode может стать обузой. Достаточно сказать, что rxvt-unicode использует путь буфера который обычно загружается в текущем `PRIMARY` выборе по умолчанию. [[2]](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.1.pod#THE_SELECTION_SELECTING_AND_PASTING_) Пользователи призывают пересмотреть [Wikipedia:X Window selection](https://en.wikipedia.org/wiki/X_Window_selection "wikipedia:X Window selection") для получения дополнительной информации.

## Perl расширения

Вы можете включить расширения perl в URxvt, следующей строкой:

```
URxvt.perl-ext-common: имя_расширения_1,имя_расширения_2,...

```

Обратите внимание, что между именами расширения **не** должно быть пробелов.

### Кликабельные ссылки (URL-адреса)

Вы можете сделать URL-адреса в терминале кликабельными, используя расширение matcher. Например, для открытия ссылок в веб-браузере по умолчанию левой кнопкой мыши, добавьте следуюшее в`.Xresources`:

```
URxvt.perl-ext-common: default,matcher
URxvt.url-launcher: /usr/bin/xdg-open
URxvt.matcher.button: 1

```

С rxvt-unicode 9.14, также можно использовать matcher для открытия списка последних (в настоящее время ограничено до 10) URL-адресов с помощью клавиатуры:

```
URxvt.keysym.C-Delete: perl:matcher:last
URxvt.keysym.M-Delete: perl:matcher:list

```

Соответствующие ссылки могут быть окрашены с помощью [#Цвета](#.D0.A6.D0.B2.D0.B5.D1.82.D0.B0) переднего плана (foreground) или фона (background), например, в синий:

```
URxvt.matcher.rend.0: Uline Bold fg5

```

В качестве альтернативы, используйте `colorUL` для цвета #RRGGBB. Это, окрасит весь подчеркнутый текст, только для ссылок matches:

```
URxvt.colorUL: #4682B4

```

### Yankable URL'ы (без мыши)

Кроме того, вы можете выбрать и открыть URL, в веб-браузере, не используя мышь. Установите пакет [urxvt-perls](https://www.archlinux.org/packages/?name=urxvt-perls) из [официальных репозиторий](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") и настройте как надо `.Xresources`. Пример показан ниже:

```
URxvt.perl-ext: default,url-select
URxvt.keysym.M-u: perl:url-select:select_next
URxvt.url-select.launcher: /usr/bin/xdg-open
URxvt.url-select.underline: true

```

**Примечание:** Это расширение заменяет расширение Clickable URLs упомянутых выше, так `matcher` могут быть удалены из списка `URxvt.perl-ext`.

**Основные команды:**

| Клавиша | Описание |
| Alt+u | Вход в режим выбора. Будет выбран последний URL на вашем экране. Вы можете повторить `Alt+u` для выбора следующего upward URL. |
| k | Select next upward URL |
| j | Select next downward URL |
| Return | Открыть выбранный URL в браузере и выйти из режима выбора |
| o | Открыть выбранный URL в браузере без выхода из режима выбора |
| y | Скопировать (yank) выбранные URL выйти из режима выбора |
| Esc | Отменить режим выбора URL |

### Простые вкладки

Чтобы добавить вкладки в urxvt, добавьте следующую строку в ваш `~/.Xresources`:

```
URxvt.perl-ext-common: ...,tabbed,...

```

Для управления вкладками, используйте:

| Клавиши | Описание |
| Shift+Down | Новая вкладка |
| Shift+Left | Перейти к левой вкладке |
| Shift+Right | Перейти к правой вкладке |
| Ctrl+Left | Переместить вкладку влево |
| Ctrl+Right | Переместить вкладку вправо |
| Ctrl+d | Закрыть вкладку |

Вы можете изменить цвета вкладок, следующими значениями:

```
URxvt.tabbed.tabbar-fg: 2
URxvt.tabbed.tabbar-bg: 0
URxvt.tabbed.tab-fg: 3
URxvt.tabbed.tab-bg: 0

```

### Полноэкранный

Вы можете установить [AUR](/index.php/AUR "AUR") пакет [urxvt-fullscreen](https://aur.archlinux.org/packages/urxvt-fullscreen/), а затем назначить клавишу (или сочетание клавиш), чтобы привести urxvt в полноэкранный режим.

 `~/.Xresources` 
```
...
URxvt.perl-ext-common: ..., fullscreen, ...
URxvt.keysym.F11: perl:fullscreen:switch
...

```

### Поддержка колеса прокрутки

Установите [urxvt-vtwheel](https://aur.archlinux.org/packages/urxvt-vtwheel/) из [AUR](/index.php/AUR "AUR") и добавьте его в ваше расширение Perl внутри `~/.Xresources`:

```
 URxvt.perl-ext-common:  ...,vtwheel,...

```

### Изменение размера шрифта на лету

Установите [urxvt-resize-font-git](https://aur.archlinux.org/packages/urxvt-resize-font-git/) из [AUR](/index.php/AUR "AUR"), и добавьте его в ваше расширение Perl внутри `~/.Xresources`

```
 URxvt.perl-ext-common:  ...,resize-font,...

```

и добавьте некоторые горячие клавиши, например, как эти:

```
 URxvt.resize-font.smaller: C-Down
 URxvt.resize-font.bigger: C-Up

```

Для назначения работы Ctrl+Shift, по умолчанию необходимо отключить назначение (binding)(обсуждение см [здесь](http://wilmer.gaa.st/blog/archives/36-rxvt-unicode-and-ISO-14755-mode.html)):

```
 URxvt.iso14755: false
 URxvt.iso14755_52: false

```

### Отключение расширений Perl

Если вы не используете функции расширения Perl, вы можете улучшить безопасность и скорость, отключив расширения Perl полностью.

```
URxvt.perl-ext:
URxvt.perl-ext-common:

```

**Примечание:** Если вы используете несколько возможностей расширения Perl, вы можете перечислить их в последовательности, разделяя запятыми: `URxvt.perl-ext-common:default,matcher,tabbed.`

### Цвета как в Xterm

По умолчанию `urxvt` использует те же цвета `xterm` кроме одного. Добавьте следующую строку в конце вашего `~/.Xresources` для цветов как в xterm:

 `~/.Xresources` 
```
...
URxvt*color12: rgb:5c/5c/ff
```

а затем объедините его содержимое с текущей настройкой X resources:

```
xrdb -merge ~/.Xresources

```

и перезапустите `urxvt`.

## Решение проблем

### Настройки ~/.Xresources не применяются

В некоторых случаях, когда *urxvt* не признаёт `~/.Xresources`, вы можете добавить строку `xrdb -merge ~/.Xresources` в ваш файл `~/.xinitrc`. Для получения дополнительной информации смотрите статью [Ресурсы Х](/index.php/%D0%A0%D0%B5%D1%81%D1%83%D1%80%D1%81%D1%8B_%D0%A5 "Ресурсы Х").

### Прозрачность не работает после обновления, начиная с версии 9.09

Разработчики rxvt-Unicode удалили код совместимости для многих нестандартных установщиков обоев с этим обновлением. Использование несовместимых установщиков обоев, ломает поддержку прозрачности. Рекомендуемые установщики обоев:

*   [feh](/index.php/Feh "Feh")
*   hsetroot
*   esetroot

Для того, чтобы работала истинная прозрачность, убедитесь что закомментированы URxvt.tintColor и URxvt.inheritPixmap.

### Удаленные хосты

Если вы заходите на удаленный хост, вы можете столкнуться с проблемами при запуске программ в текстовм режиме под rxvt-Unicode. Это может быть исправлено путем установки [rxvt-unicode-terminfo](https://www.archlinux.org/packages/?name=rxvt-unicode-terminfo) на удаленном хосте или с помощью копирования, `/usr/share/terminfo/r/rxvt-unicode` с локального компьютера на ваш хост в `~/.terminfo/r/rxvt-unicode`; тоже самое для rxvt-unicode-256color.

Некоторые удаленные системы не изменяют название автоматически, если вы не укажете TERM=xterm. Чтобы решить этот вопрос, добавьте на удалённой машине в .bashrc строку:

```
PROMPT_COMMAND='echo -ne "\033]0;${USER}@${HOSTNAME}:${PWD}\007"'

```

### Использование rxvt-Unicode в качестве терминала gmrun (Gnome Completion-Run)

В отличие от некоторых других терминалов, urxvt ожидает аргументы `-e` определённые отдельно, а не сгруппированные вместе с кавычками. Это вызывает проблемы с [gmrun](/index.php/Gmrun "Gmrun"), который предполагает противоположное поведение. Это можно обойти, указав "eval" перед значением терминала в `.gmrunrc`:

```
Terminal = eval urxvt
TermExec = ${Terminal} -e

```

(gmrun использует `/bin/sh` чтобы выполнять команды, так что "eval" здесь понимается.) "eval" имеет побочный эффект "разрыва" аргументов `-e` таким же образом, что `$@` делает в [Bash](/index.php/Bash "Bash"), что делает команды понятными для urxvt.

### Моя цифровая клавиатура действует странно и производит странный вывод (например, в VIM)

Кажется есть проблема у некоторых пользователей Debian GNU/Linux, хотя никаких конкретных подробностей не сообщалось до сих пор. Вполне возможно, что это вызвано установкой неправильного TERM, хотя подробностей как это может произойти неизвестно, как TERM=rxvt должен предложить совместимую раскладку. Смотрите ответ на предыдущий вопрос, и, пожалуйста, сообщите если это помогло.

Тем не менее, с помощью программы *xmodmap* ([xorg-xmodmap](https://www.archlinux.org/packages/?name=xorg-xmodmap)), вы можете переназначить клавиши цифровой клавиатуры обратно.

1\. Проверьте, что ваш keycode цифровой клавиатры (numpad) генерируется с поомщью программы `xev`.

*   Запустите программу `xev`
*   Нажмите цифру на вашей цифровой клавиатуре, смотрите *... keycode xxx ...* в выводе `xev`. Например, клавиша 1 на моей клавиатуре также известна как калавиша "End", что имеет '**keycode 87'**.

2\. Создайте или измените ваш файл xmodmap, обычно `~/.Xmodmap`, с содержимым, представляющим свой код клавиш.

Пример Xmodmap файла с номером keycode:

```
keycode 63 = KP_Multiply
keycode 79 = Home KP_7
keycode 80 = Up KP_8
keycode 81 = Prior KP_9
keycode 82 = KP_Subtract
keycode 83 = Left KP_4
keycode 84 = KP_5
keycode 85 = Right KP_6
keycode 86 = KP_Add
keycode 87 = End KP_1
keycode 88 = Down KP_2
keycode 89 = Next KP_3
keycode 90 = Insert KP_0
keycode 91 = Delete KP_Decimal
keycode 112 = Prior
keycode 117 = Next
```

3\. Загрузите ваш файл xmodmap при запуске X сессии.

Например добавьте в файл `~/.xinitrc`:

```
...
xmodmap ~/.Xmodmap
...

```

### pseudo-tty

Следующая ошибка, скорее всего, вызвана `/dev/pts`, будучи смонтированным с неправильными опциями.

```
urxvt: cannot initialize pseudo-tty, aborting.

```

Удалите `/dev/pts` из `/etc/fstab` и исправьте текущие опции монтирования на:

```
sudo mount -o remount,gid=5,mode=620 /dev/pts

```

Смотрите также [[3]](https://mailman.archlinux.org/pipermail/arch-dev-public/2013-August/025332.html), [FS#36548](https://bugs.archlinux.org/task/36548), и [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1318127).

### Горячие клавиши не работают

Смотрите [Get Alt key to work in terminal](http://vim.wikia.com/wiki/Get_Alt_key_to_work_in_terminal?useskin=monobook).

### Низкая производительность при рисовании глифов

Некоторые программы, такие как alsamixer и xprop не хорошо выполняются с некоторыми графическими драйверами, и как следствие перерисовывают очень медленно. Опция "skipBuiltinGlyphs" в `~/.Xresources` или параметр командной строки `-sbg` может это исправить. Одним из возможных решений является добавление следующей строки в `~/.Xresources`:

```
URxvt*skipBuiltinGlyphs:    true

```

## Внешние ресурсы

*   [rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode.html) - Официальный сайт
*   [Source Code](http://cvs.schmorp.de/rxvt-unicode/) - Browseable CVS
*   [rxvt-unicode FAQ](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.7.pod) - Оффициальные ЧАВО
*   [rxvt-unicode Reference](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.1.pod) - Официальная страница руководства
*   [urxvtperl](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/src/urxvt.pm) - Официальная справка расширений Perl