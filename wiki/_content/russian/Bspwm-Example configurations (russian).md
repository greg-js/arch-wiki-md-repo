**Состояние перевода:** На этой странице представлен перевод статьи [bspwm/Example configurations](/index.php/Bspwm/Example_configurations "Bspwm/Example configurations"). Дата последней синхронизации: 27 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Bspwm/Example_configurations&diff=0&oldid=428031).

Получите настройки [bspwm](/index.php/Bspwm_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bspwm (Русский)") быстро, из списка ниже.

## Аннотированный пример настроек, на основе одного значения по умолчанию

### bspwmrc

```
#! /bin/sh

bspc config border_width        2
bspc config window_gap         12

bspc config split_ratio         0.52
bspc config borderless_monocle  false
bspc config gapless_monocle     false
bspc config focus_by_distance   true

bspc config auto_cancel         true
bspc config presel_border_color "#ff5555"

```

### sxhkdrc

Убить окно в фокусе:

```
super + shift + q
    bspc window -c

```

Следующий тайловый режим:

```
super + t
    bspc desktop -l next

```

**Примечание:** На данный момент в bspwm есть два тайловых режима. По умолчанию, один обычный b-древовидный тайлинг, другой режим монокля, который ставит сфокусированное окно на весь экран.

Баланс области рабочего стола:

```
super + b
    bspc desktop -B

```

Переключится на плавающий/полноэкранный режим:

```
super + {s,f}
    bspc window -t {floating,fullscreen}

```

**Примечание:** Это показывает интересный бит синтаксиса sxhkd, где первый элемент "s" во входном массиве соответствует первому элементу "плавающего" в командной массива и так далее.

Перемещение (с помощью `Super+hjkl`) изменяет фокус окна и предварительно выбирать (с `Super+Ctrl+hjkl`) отмечает данный край сфокусированного окна для модификации (это называется предварительный выбор):

```
    bspc window -{f,p} {left,down,up,right}

```

**Примечание:** Показывает еще один интересный бит синтаксиса sxhkd где "_" означает, что никакой другой ключ не требуется, чтобы вызвать команду.

Swap (с помощью`Super+Shift+hjkl`) позволяет поменять сфокусированное окно с другим окном во время трансплантации (с помощью `Super+Shift+hjkl`) переместит окно в другой предварительный отбор:

```
super + {shift,alt} + {h,j,k,l}
   bspc window -{s,w} {left,down,up,right}

```

**Примечание:** Для того, чтобы поиграть с трансплантацией, предварительно выберите край соседнего окна, а затем трансплантируйте в соседнее окно.

Цикл вперед/назад:

```
super + {_,shift + }c
    bspc window -f {next,prev}

```

Circulate leaves назад/вперёд:

```
super + {comma,period}
    bspc desktop -C {backward,forward}

```

Повернуть дерево по часовой/против часовой стрелки:

```
super + ctrl + {comma,period}
    bspc desktop -R {270,90}

```

Предыдущий/Следующий рабочий стол:

```
super + bracket{left,right}
    bspc desktop -f {prev,next}

```

Отменить предварительный выбор окна/рабочего стола:

```
super + ctrl + {_,shift + }space
    bspc {window -p cancel,desktop -c}

```

Количество предварительного выбора:

```
super + ctrl + {1-9}
    bspc window -r 0.{1-9}

```

Переместить окно на выбранный рабочий стол:

```
super + {_,shift + }{1-9,0}
    bspc {desktop -f,window -d} ^{1-9,10}

```

Фокус по щелчку мыши:

```
~button1
    bspc pointer -g focus

```

Мышкой: переместить/изменить размер стороны/сторон (за уголок):

```
super + button{1-3}
    bspc pointer -g {move,resize_side,resize_corner}

super + !button{1-3}
    bspc pointer -t %i %i

super + @button{1-3}
    bspc pointer -u

```