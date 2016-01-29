# xmodmap

Related articles

*   [Xorg](/index.php/Xorg "Xorg")
*   [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")
*   [Extra keyboard keys in Xorg](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg")
*   [Extra keyboard keys in console](/index.php/Extra_keyboard_keys_in_console "Extra keyboard keys in console")
*   [Xbindkeys](/index.php/Xbindkeys "Xbindkeys")

**Note:** _xmodmap_ settings are reset by _setxkbmap_, which not only alters the alphanumeric keys to the values given in the map, but also resets all other keys to the startup default. [[1]](http://wiki.linuxquestions.org/wiki/Configuring_keyboards)

_xmodmap_ is a utility for modifying keymaps and pointer button mappings in [Xorg](/index.php/Xorg "Xorg").

_xmodmap_ is not directly related to [X KeyBoard extension](/index.php/X_KeyBoard_extension "X KeyBoard extension") (XKB), as it uses different (pre-XKB) ideas on how _keycodes_ are processed within X. Generally, it is only recommended for the simplest tasks. See [X KeyBoard extension](/index.php/X_KeyBoard_extension "X KeyBoard extension") for advanced layout configuration.

## Contents

*   [1 Introduction](#Introduction)
*   [2 Installation](#Installation)
*   [3 Keymap table](#Keymap_table)
*   [4 Custom table](#Custom_table)
    *   [4.1 Activating the custom table](#Activating_the_custom_table)
    *   [4.2 Test changes](#Test_changes)
*   [5 Modifier keys](#Modifier_keys)
*   [6 Reverse scrolling](#Reverse_scrolling)
*   [7 Templates](#Templates)
    *   [7.1 Spanish](#Spanish)
    *   [7.2 Turn CapsLock into Control, and LeftControl into Hyper](#Turn_CapsLock_into_Control.2C_and_LeftControl_into_Hyper)
    *   [7.3 Switch every number key N with Shift-N and vice-versa, for Croatian layout](#Switch_every_number_key_N_with_Shift-N_and_vice-versa.2C_for_Croatian_layout)
*   [8 See also](#See_also)

## Introduction

There are two types of keyboard values in [Xorg](/index.php/Xorg "Xorg"): _keycodes_ and _keysyms_.

NaN

## Installation

_xmodmap_ can be [installed](/index.php/Pacman "Pacman") through the [xorg-xmodmap](https://www.archlinux.org/packages/?name=xorg-xmodmap) package from the [official repositories](/index.php/Official_repositories "Official repositories").

Optionally, install [xkeycaps](https://www.archlinux.org/packages/?name=xkeycaps), which is a graphical front-end to _xmodmap_.

## Keymap table

Print the current keymap table formatted into expressions:

 `$ xmodmap -pke` 

```
[...]
keycode  57 = n N
[...]
```

Each _keycode_ is followed by the _keysym_ it is mapped to. The above example indicates that the _keycode_ `57` is mapped to the lowercase `n`, while the uppercase `N` is mapped to _keycode_ `57` plus `Shift`.

Each _keysym_ column in the table corresponds to a particular combination of modifier keys:

1.  `Key`
2.  `Shift+Key`
3.  `mode_switch+Key`
4.  `mode_switch+Shift+Key`
5.  `AltGr+Key`
6.  `AltGr+Shift+Key`

Not all _keysyms_ have to be set, but to assign only a latter _keysym_, use the `NoSymbol` value.

To see which _keycode_ corresponds to a key, see [Extra keyboard keys#In Xorg](/index.php/Extra_keyboard_keys#In_Xorg "Extra keyboard keys") for details on the _xev_ utility.

**Tip:** There are predefined descriptive _keysyms_ for multimedia keys, e.g. `XF86AudioMute` or `XF86Mail`. These _keysyms_ can be found in `/usr/include/X11/XF86keysym.h`. Many multimedia programs are designed to work with these _keysyms_ out-of-the-box, without the need to configure any third-party application.

Note that xmodmap is influenced by xkbd settings, so all eight keysym are available for the us(intl) xkbd layout but not for the default us (it is missing the ralt_switch symbol defined in level3). To have all 8 keysyms available you should configure the _(intl)_ variant of the keyboard from xorg.conf or add, using us layout as an example, `setxkbmap -layout 'us(intl)'` before calling xmodmap.

## Custom table

To create a key map (i.e. `~/.Xmodmap`):

```
$ xmodmap -pke > ~/.Xmodmap

```

To test the changes:

```
$ xmodmap ~/.Xmodmap

```

### Activating the custom table

With [GDM](/index.php/GDM "GDM"), [XDM](/index.php/XDM "XDM"), [KDM](/index.php/KDM "KDM") or [LightDM](/index.php/LightDM "LightDM") there is no need to source `~/.Xmodmap`. For [startx](/index.php/Startx "Startx"), use:

 `~/.xinitrc` 

```
if [ -s ~/.Xmodmap ]; then
    xmodmap ~/.Xmodmap
fi
```

Alternatively, edit the global startup script `/etc/X11/xinit/xinitrc`.

### Test changes

To make temporary changes:

```
$ xmodmap -e "keycode  46 = l L l L lstroke Lstroke lstroke"
$ xmodmap -e "keysym a = e E"

```

## Modifier keys

_xmodmap_ can also be used to override [modifier keys](https://en.wikipedia.org/wiki/Modifier_key "wikipedia:Modifier key"), e.g. to swap `Control` and `Super` (the [Windows keys](https://en.wikipedia.org/wiki/Windows_key "wikipedia:Windows key")).

Before assignment the modifier keys need to be empty. `!` is a comment, so only the modifiers `Control` and `Mod4` get cleared in the following example. Then the _keysyms_ `Control_L`, `Control_R`, `Super_L` and `Super_R` are assigned to the opposite modifier. Assigning both left and right to the same modifier means that both keys are treated the same way.

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

**Note:** The example assumes that the `Control_L` and `Control_R` keysyms were assigned to the `Control` modifier, and `Super_L` and `Super_R` keysyms to the `Mod4` modifier. If you get the following error message `X Error of failed request: BadValue (integer parameter out of range for operation)`, you will need to adapt accordingly. Running `xmodmap` produces a list of modifiers and keys that are assigned to them.

The following example modifies `CapsLock` to `Control`, and `Shift+CapsLock` to `CapsLock`:

 `~/.Xmodmap` 

```
clear lock
clear control
add control = Caps_Lock Control_L Control_R
keycode 66 = Control_L Caps_Lock NoSymbol NoSymbol
```

## Reverse scrolling

The [natural scrolling](http://who-t.blogspot.com/2011/09/natural-scrolling-in-synaptics-driver.html) feature available in OS X Lion (mimicking smartphone or tablet scrolling) can be [replicated](https://bbs.archlinux.org/viewtopic.php?id=126258) with _xmodmap_. Since the synaptics driver uses the buttons 4/5/6/7 for up/down/left/right scrolling, you simply need to swap the order of how the buttons are declared in `~/.Xmodmap`:

 `~/.Xmodmap`  `pointer = 1 2 3 **5 4** 7 6 8 9 10 11 12` 

Then update _xmodmap_:

```
$ xmodmap ~/.Xmodmap

```

## Templates

### Spanish

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

### Turn CapsLock into Control, and LeftControl into Hyper

Laptop users may prefer having `CapsLock` as `Control`. The `Left Hyper` key can be used as a modifier.

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

### Switch every number key N with Shift-N and vice-versa, for Croatian layout

Should work fine for layouts similar to Croatian as well.

 `~/.Xmodmap` 

```
keycode 10 = exclam 1 1 exclam asciitilde dead_tilde asciitilde
keycode 11 = quotedbl 2 2 quotedbl dead_caron caron dead_caron
keycode 12 = numbersign 3 3 numbersign asciicircum dead_circumflex asciicircum
keycode 13 = dollar 4 4 dollar dead_breve breve dead_breve
keycode 14 = percent 5 5 percent degree dead_abovering degree
keycode 15 = ampersand 6 6 ampersand dead_ogonek ogonek dead_ogonek
keycode 16 = slash 7 7 slash grave dead_grave grave
keycode 17 = parenleft 8 8 parenleft dead_abovedot abovedot dead_abovedot
keycode 18 = parenright 9 9 parenright dead_acute apostrophe dead_acute
keycode 19 = equal 0 0 equal dead_doubleacute doubleacute dead_doubleacute

```

## See also

*   [Current man page](http://www.x.org/archive/current/doc/man/man1/xmodmap.1.xhtml) at X.Org Foundation
*   [Multimediakeys with .Xmodmap HOWTO](http://cweiske.de/howto/xmodmap/allinone.html) by Christian Weiske
*   [Mapping unsupported keys with xmodmap](http://dev-loki.blogspot.com/2006/04/mapping-unsupported-keys-with-xmodmap.html) by Pascal Bleser
*   [List of Keysyms Recognised by Xmodmap](http://wiki.linuxquestions.org/wiki/List_of_Keysyms_Recognised_by_Xmodmap) on [LinuxQuestions](http://linuxquestions.org)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Xmodmap&oldid=398830](https://wiki.archlinux.org/index.php?title=Xmodmap&oldid=398830)"