**Состояние перевода:** На этой странице представлен перевод статьи [bspwm](/index.php/Bspwm "Bspwm"). Дата последней синхронизации: 12 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Bspwm&diff=0&oldid=425338).

Related articles

*   [Bspwm/Примеры настроек](/index.php/Bspwm/%D0%9F%D1%80%D0%B8%D0%BC%D0%B5%D1%80%D1%8B_%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B5%D0%BA "Bspwm/Примеры настроек")
*   [Оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер")
*   [Сравнение тайловых оконных менеджеров](/index.php/%D0%A1%D1%80%D0%B0%D0%B2%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D1%82%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D1%8B%D1%85_%D0%BE%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D1%85_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80%D0%BE%D0%B2 "Сравнение тайловых оконных менеджеров")

*bspwm* тайловый оконный менеджер представляющий окна как слои двоичного дерева. Также поддерживает [EWMH](https://specifications.freedesktop.org/wm-spec/wm-spec-latest.html) и несколько мониторов. Настраивается и управляется с помощью сообщений.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
    *   [2.1 Примечание для установки нескольких мониторов](#Примечание_для_установки_нескольких_мониторов)
    *   [2.2 Правила](#Правила)
    *   [2.3 Панели](#Панели)
    *   [2.4 Блокнот](#Блокнот)
    *   [2.5 Различные настройки монитора для различных машин](#Различные_настройки_монитора_для_различных_машин)
*   [3 Решение проблем](#Решение_проблем)
    *   [3.1 Помогите! У меня пустой экран и мои горячие клавиши не работают!](#Помогите!_У_меня_пустой_экран_и_мои_горячие_клавиши_не_работают!)
    *   [3.2 Размер окна больше самого приложения!](#Размер_окна_больше_самого_приложения!)
    *   [3.3 Проблемы с приложениями Java](#Проблемы_с_приложениями_Java)
    *   [3.4 Проблемы, связанные с использованием назначения клавиш fish](#Проблемы,_связанные_с_использованием_назначения_клавиш_fish)
*   [4 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/Install "Install") [bspwm](https://www.archlinux.org/packages/?name=bspwm) и [sxhkd](https://www.archlinux.org/packages/?name=sxhkd), или разрабатываемую версию: [bspwm-git](https://aur.archlinux.org/packages/bspwm-git/) и [sxhkd-git](https://aur.archlinux.org/packages/sxhkd-git/). Sxhkd простой демон горячих клавиш X, использующий для связи `bspc` с bspwm, он также запускает выбранные вами приложения.

Для запуска bspwm при входе в систему, добавьте следующие строки в `~/.xinitrc` или `~/.xprofile` (в зависимости от того, как вы запускаете X / ваш менеджер дисплея):

```
sxhkd &
exec bspwm

```

## Настройка

Пример настроек находится в `/usr/share/doc/bspwm/examples/` и на [GitHub](https://github.com/baskerville/bspwm/blob/master/examples/).

**Важно:** Создайте ваше переменное окружение $XDG_CONFIG_HOME правильно, иначе bspwmrc не будет найден. Это можно сделать путём добавления XDG_CONFIG_HOME="$HOME/.config" и экспорта XDG_CONFIG_HOME в ваш ~/.profile.

Создайте `~/.config/bspwm/` и `~/.config/sxhkd/`, затем скопируйте `/usr/share/doc/bspwm/examples/bspwmrc` в `~/.config/bspwm/` и `/usr/share/doc/bspwm/examples/sxhkdrc` в `~/.config/sxhkd/`. Сделайте bspwmrc выполняемым `chmod +x ~/.config/bspwm/bspwmrc`.

Эти два файла, в которых вы будите устанавливать соответственно настройки wm (оконного менеджера) и горячих клавиш. В качестве примера, смотрите [bspwm/Example configurations](/index.php/Bspwm/Example_configurations "Bspwm/Example configurations").

Документацию для bspwm можно посмотреть выполнив [bspwm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bspwm.1).

Также есть документация для sxhkd, выполните [sxhkd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sxhkd.1).

#### Примечание для установки нескольких мониторов

Пример настройки bspwmrc, для десяти рабочих столов на одном мониторе:

```
bspc monitor -d I II III IV V VI VII VIII IX X

```

Вам нужно будет изменить эту строку и добавить для каждого монитора, например:

```
bspc monitor DVI-I-1 -d I II III IV
bspc monitor DVI-I-2 -d V VI VII
bspc monitor DP-1 -d VIII IX X

```

Вы можете использовать запросы `xrandr -q` или `bspc query -M` чтобы узнать имя монитора.

В примере выше, было сохранено общее количество рабочих столов, - десять. Это связано с тем, что к каждому рабочему столу можно обратиться с помощью 'super + {1-9,0}' в sxhkdrc.

### Правила

Есть два способа установить правила для окна (rules) (по состоянию на [cd97a32](https://github.com/baskerville/bspwm/commit/cd97a3290aa8d36346deb706fa307f5f8faa2f34)).

Во-первых, с помощью встроенной команды правила, как показано в примере bspwmrc:

```
bspc rule -a Gimp desktop=^8 follow=on state=floating
bspc rule -a Chromium desktop=^2
bspc rule -a mplayer2 state=floating
bspc rule -a Kupfer.py focus=on
bspc rule -a Screenkey manage=off

```

Второй вариант заключается в использовании внешней команды правил. Этот вариант более сложный, но может позволить вам разрабатывать более сложные правила для окна. Смотрите команды правил [в этих примерах](https://github.com/baskerville/bspwm/tree/master/examples/external_rules).

Если какое-то окно, не ведёт себя в соответствии с вашими правилами, проверьте имя класса программы. Это можно сделать запустив `xprop | grep WM_CLASS` чтобы убедиться, что вы используете правильную строку.

### Панели

Пример панели для [lemonbar](https://aur.archlinux.org/packages/lemonbar/) есть в каталоге examples на странице GitHub. Вы также можете получить некоторые идеи из страници Wiki [lemonbar](/index.php/Lemonbar "Lemonbar"). Панель будет запускаться командой `panel &` в вашем bspwmrc. Проверьте дополнительные зависимости пакета bspwm которые могут потребоваться.

Для отображения информации о системе на строке состояния, вы можете использовать различные системные вызовы. Этот пример покажет вам как изменить `panel` , чтобы получить статус громкости на панели:

```
panel_volume()
{
        volStatus=$(amixer get Master | tail -n 1 | cut -d '[' -f 4 | sed 's/].*//g')
        volLevel=$(amixer get Master | tail -n 1 | cut -d '[' -f 2 | sed 's/%.*//g')
        # is alsa muted or not muted?
        if [ "$volStatus" == "on" ]
        then
                echo "%{Fyellowgreen} $volLevel %{F-}"
        else
                # If it is muted, make the font red
                echo "%{Findianred} $volLevel %{F-}"
        fi
}
```

Далее, мы должны убедиться, что она вызывается и отправляет в `$PANEL_FIFO`:

```
while true; do
echo "S" "$(panel_volume) $(panel_clock) > "$PANEL_FIFO"
        sleep 1s
done &

```

### Блокнот

Вы можете эмулировать блокнот (как в i3) путем добавления ярлыка для этой команды:

```
xdotool search --onlyvisible --classname scratchpad windowunmap \
|| xdotool search --classname scratchpad windowmap \
|| st -c scratchpad -g 1000x400+460 &

```

и добавив это правило:

```
bspc rule -a scratchpad sticky=on state=floating

```

Смотрите также [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1338582#p1338582) и [[2]](http://yuri-rage.github.io/geekery/2015/01/26/bleeding-edge-bspwm/).

Для блокнота, который может использовать любой тип окна без предопределенных правил, смотрите: [[3]](https://www.reddit.com/r/bspwm/comments/3xnwdf/i3_like_scratch_for_any_window_possible/cy6i585)

Для более сложных скриптов блокнота, которые поддерживают множество терминалов "из коробки", имеют флаги, делают при необходимости запуск сессии tmuxinator / tmux, превращают любое окно в блокнот на лету, автоматически меняют размер блокнота соответствующему монитору, смотрите [tdrop-git](https://aur.archlinux.org/packages/tdrop-git/).

### Различные настройки монитора для различных машин

Так как `bspwmrc` это сценарий оболочки, он позволяет делать такие вещи:

```
#! /bin/sh

 if [[ $(hostname) == 'myhost' ]]; then
     bspc monitor eDP1 -d I II III IV V VI VII VIII IX X
 elif [[ $(hostname) == 'otherhost' ]]; then
     bspc monitor VGA-0 -d I II III IV V
     bspc monitor VGA-1 -d VI VII VIII IX X
 elif [[ $(hostname) == 'yetanotherhost' ]]; then
     bspc monitor DVI-I-3 -d VI VII VIII IX X
     bspc monitor DVI-I-2 -d I II III IV V
 fi

```

## Решение проблем

### Помогите! У меня пустой экран и мои горячие клавиши не работают!

Есть несколько способов уладить это. Во-первых, пустой экран это хорошо. Это означает, что bspwm работает.

Для начала убедитесь что в вашем xinitrc есть эти строки

```
sxhkd &
exec bspwm

```

Амперсанд имеет важное значение. Далее, попробуйте вызвать терминал в вашем xinitrc, чтобы увидеть, получите ли вы его правильное положение. Он должен появиться несколько "по центру" на экране. Для этого используйте этот .xinitrc:

```
sxhkd &
urxvt &
exec bspwm

```

Если ничего не отображается, это означает, что вы, вероятно, забыли установить urxvt. Если он оказался вверху, но не по центру экрана, или занимает большую часть экрана, это означает, что BSPWM не начал работу должным образом. Убедитесь что вы выполнили `chmod +x ~/.config/bspwm/bspwmrc` .

Далее, введите в этом запустившемся терминале `pidof sxhkd`. Команда покажет число. Если этого не произойдет, это означает, что sxhd не работает. Выполните `sxhkd -c ~/.config/sxhkd/sxhkdrc` . Кроме того, можно попробовать изменить клавишу Super на другую, например Alt в вашем sxhkdrc и посмотреть, поможет ли это. Другой распространенной проблемой является копирование текста из файла примеров, вместо физического копирования файла. Копирование / вставка кода обычно приводит к проблемам отступов, к которые sxhkd может быть чувствительным.

### Размер окна больше самого приложения!

Это может произойти, если вы используете приложения GTK3, обычно это происходит с диалоговыми окнами. Для решения проблемы необходимо создать или добавить ниже в файле темы GTK3 (~/.config/gtk-3.0/gtk.css).

```
.window-frame, .window-frame:backdrop {
  box-shadow: 0 0 0 black;
  border-style: none;
  margin: 0;
  border-radius: 0;
}

.titlebar {
  border-radius: 0;
}

```

(источник: [Bspwm forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1404973#p1404973))

### Проблемы с приложениями Java

Если у вас есть проблемы, например окно приложения Java неменяет размер, или меню закрыввется после щелчка, смотрите [Java#Gray window, applications not resizing with WM, menus immediately closing](/index.php/Java#Gray_window,_applications_not_resizing_with_WM,_menus_immediately_closing "Java").

### Проблемы, связанные с использованием назначения клавиш fish

Если выиспользуете [fish](/index.php/Fish_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fish (Русский)"), вы обнаружите, что не можете переключаться между рабочими столами. Это происходит потому что bspc's использует символ ^ несовместимый с fish. Вы можете это исправить, сказав sxhkd использовать bash для выполнения команд:

```
$ set -U SXHKD_SHELL /usr/bin/bash

```

В качестве альтернативы, символ ^ может быть символом обратной косой черты в файле sxhkdrc.

## Смотрите также

*   Mailing List: bspwm *at* librelist.com.
*   `#bspwm` - IRC channel at irc.freenode.net
*   [https://bbs.archlinux.org/viewtopic.php?id=149444](https://bbs.archlinux.org/viewtopic.php?id=149444) - Arch BBS thread
*   [https://github.com/baskerville/bspwm](https://github.com/baskerville/bspwm) - GitHub project
*   [https://github.com/windelicato/dotfiles/wiki/bspwm-for-dummies](https://github.com/windelicato/dotfiles/wiki/bspwm-for-dummies) - earsplit's "bspwm for dummies"