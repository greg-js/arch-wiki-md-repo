#### Dansk dvorak

Du kan skifte til dansk dvorak layout i terminalen med 'setxkbmap'

```
setxkbmap dk dvorak

```

#### Permanent layout

I /etc/X11/xorg.conf skal det se sådan ud

```
Option "XkbLayout" "dk"
Option "XkbVariant" "dvorak"

```