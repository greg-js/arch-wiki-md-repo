**Состояние перевода:** На этой странице представлен перевод статьи [bspwm/Example configurations](/index.php/Bspwm/Example_configurations "Bspwm/Example configurations"). Дата последней синхронизации: 27 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Bspwm/Example_configurations&diff=0&oldid=428031).

The [bspwm](/index.php/Bspwm_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bspwm (Русский)") configurations below will get you up to speed quickly.

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

**Примечание:** There are two tiling modes in bspwm at the moment. The default one is the usual b-tree based tiling, the other mode is the monocle mode that puts the focused window on fullscreen.

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

**Примечание:** This shows an interesting bit of sxhkd syntax where the the first item "s" in the input array corresponds to the first entry "floating" in the command array and so on.

Move (with `Super+hjkl`) changes the window focus and preselect (with `Super+Ctrl+hjkl`) marks the given edge of the focused window for modification (this is called preselection):

```
super + {_,ctrl + }{h,j,k,l}
    bspc window -{f,p} {left,down,up,right}

```

**Примечание:** Shows another interesting bit of sxhkd syntax where "_" means that no other key is necessary to trigger the command.

Swap (with `Super+Shift+hjkl`) allows you to swap the focused window with another window while transplant (with `Super+Shift+hjkl`) will move the window into another preselection:

```
super + {shift,alt} + {h,j,k,l}
   bspc window -{s,w} {left,down,up,right}

```

**Примечание:** To play with transplantation, preselect an edge of an adjacent window, then transplant into the adjacent window.

Цикл вперед/назад:

```
super + {_,shift + }c
    bspc window -f {next,prev}

```

Circulate leaves backward/forward:

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

Cancel window/desktop preselection:

```
super + ctrl + {_,shift + }space
    bspc {window -p cancel,desktop -c}

```

Preselection amount:

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

Мышь переместить/изменить размер стороны/изменить размер сторон (за уголок):

```
super + button{1-3}
    bspc pointer -g {move,resize_side,resize_corner}

super + !button{1-3}
    bspc pointer -t %i %i

super + @button{1-3}
    bspc pointer -u

```