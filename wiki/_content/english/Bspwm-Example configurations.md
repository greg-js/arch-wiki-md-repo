The [bspwm](/index.php/Bspwm "Bspwm") configurations below will get you up to speed quickly.

## Annotated example configuration based on the default one

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

Kill the focused window:

```
super + shift + q
    bspc window -c

```

Next tiling mode:

```
super + t
    bspc desktop -l next

```

**Note:** There are two tiling modes in bspwm at the moment. The default one is the usual b-tree based tiling, the other mode is the monocle mode that puts the focused window on fullscreen.

Balance desktop areas:

```
super + b
    bspc desktop -B

```

Toggle floating/fullscreen:

```
super + {s,f}
    bspc window -t {floating,fullscreen}

```

**Note:** This shows an interesting bit of sxhkd syntax where the the first item "s" in the input array corresponds to the first entry "floating" in the command array and so on.

Move (with `Super+hjkl`) changes the window focus and preselect (with `Super+Ctrl+hjkl`) marks the given edge of the focused window for modification (this is called preselection):

```
super + {_,ctrl + }{h,j,k,l}
    bspc window -{f,p} {left,down,up,right}

```

**Note:** Shows another interesting bit of sxhkd syntax where "_" means that no other key is necessary to trigger the command.

Swap (with `Super+Shift+hjkl`) allows you to swap the focused window with another window while transplant (with `Super+Shift+hjkl`) will move the window into another preselection:

```
super + {shift,alt} + {h,j,k,l}
   bspc window -{s,w} {left,down,up,right}

```

**Note:** To play with transplantation, preselect an edge of an adjacent window, then transplant into the adjacent window.

Cycle forward/backward:

```
super + {_,shift + }c
    bspc window -f {next,prev}

```

Circulate leaves backward/forward:

```
super + {comma,period}
    bspc desktop -C {backward,forward}

```

Rotate tree clockwise/counter clockwise:

```
super + ctrl + {comma,period}
    bspc desktop -R {270,90}

```

Previous/next desktop:

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

Move window to selected desktop:

```
super + {_,shift + }{1-9,0}
    bspc {desktop -f,window -d} ^{1-9,10}

```

Mouse click focus:

```
~button1
    bspc pointer -g focus

```

Mouse move/resize side/resize corner:

```
super + button{1-3}
    bspc pointer -g {move,resize_side,resize_corner}

super + !button{1-3}
    bspc pointer -t %i %i

super + @button{1-3}
    bspc pointer -u

```