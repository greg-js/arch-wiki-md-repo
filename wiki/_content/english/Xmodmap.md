Related articles

*   [Xorg](/index.php/Xorg "Xorg")
*   [Keyboard input](/index.php/Keyboard_input "Keyboard input")
*   [Extra keyboard keys in console](/index.php/Extra_keyboard_keys_in_console "Extra keyboard keys in console")
*   [Xbindkeys](/index.php/Xbindkeys "Xbindkeys")

*xmodmap* is a utility for modifying keymaps and pointer button mappings in [Xorg](/index.php/Xorg "Xorg").

*xmodmap* is not directly related to [X keyboard extension](/index.php/X_keyboard_extension "X keyboard extension") (XKB), as it uses different (pre-XKB) ideas on how *keycodes* are processed within X. Generally, it is only recommended for the simplest tasks. See [X keyboard extension](/index.php/X_keyboard_extension "X keyboard extension") for advanced layout configuration.

**Note:** *xmodmap* settings are reset by *setxkbmap*, which not only alters the alphanumeric keys to the values given in the map, but also resets all other keys to the startup default. [[1]](http://wiki.linuxquestions.org/wiki/Configuring_keyboards)

## Contents

*   [1 Introduction](#Introduction)
*   [2 Installation](#Installation)
*   [3 Keymap table](#Keymap_table)
*   [4 Custom table](#Custom_table)
    *   [4.1 Activating the custom table](#Activating_the_custom_table)
    *   [4.2 Test changes](#Test_changes)
*   [5 Modifier keys](#Modifier_keys)
    *   [5.1 Finding the keysym column modifier keys](#Finding_the_keysym_column_modifier_keys)
    *   [5.2 Reassigning modifiers to keys on your keyboard](#Reassigning_modifiers_to_keys_on_your_keyboard)
*   [6 Reverse scrolling](#Reverse_scrolling)
*   [7 Swapping mouse buttons](#Swapping_mouse_buttons)
*   [8 Templates](#Templates)
    *   [8.1 Spanish](#Spanish)
    *   [8.2 Turn CapsLock into Control](#Turn_CapsLock_into_Control)
    *   [8.3 Turn CapsLock into Control, and LeftControl into Hyper](#Turn_CapsLock_into_Control,_and_LeftControl_into_Hyper)
    *   [8.4 Switch every number key N with Shift-N and vice-versa, for Croatian layout](#Switch_every_number_key_N_with_Shift-N_and_vice-versa,_for_Croatian_layout)
*   [9 See also](#See_also)

## Introduction

There are two types of keyboard values in [Xorg](/index.php/Xorg "Xorg"): *keycodes* and *keysyms*.

	keycode

	The *keycode* is the numeric representation received by the kernel when a key or a mouse button is pressed.

	keysym

	The *keysym* is the value assigned to the *keycode*. For example, pressing `a` generates the `keycode 38`, which is mapped to the `keysym 0×61`, which matches `a` in the [ASCII table](https://en.wikipedia.org/wiki/ASCII "wikipedia:ASCII").

	The *keysyms* are managed by [Xorg](/index.php/Xorg "Xorg") in a table of *keycodes* defining the *keycode*-*keysym* relations, which is called the [keymap table](#Keymap_table). This can be shown by running `xmodmap`.

## Installation

*xmodmap* can be [installed](/index.php/Pacman "Pacman") through the [xorg-xmodmap](https://www.archlinux.org/packages/?name=xorg-xmodmap) package.

Optionally, install [xkeycaps](https://www.archlinux.org/packages/?name=xkeycaps), which is a graphical front-end to *xmodmap*.

## Keymap table

Print the current keymap table formatted into expressions:

 `$ xmodmap -pke` 
```
[...]
keycode  57 = n N
[...]
```

Each *keycode* is followed by the *keysym* it is mapped to. The above example indicates that the *keycode* `57` is mapped to the lowercase `n`, while the uppercase `N` is mapped to *keycode* `57` plus `Shift`.

Each *keysym* column in the table corresponds to a particular combination of modifier keys:

1.  `Key`
2.  `Shift+Key`
3.  `Mode_switch+Key`
4.  `Mode_switch+Shift+Key`
5.  `ISO_Level3_Shift+Key`
6.  `ISO_Level3_Shift+Shift+Key`

Not all *keysyms* have to be set, but to assign only a latter *keysym*, use the `NoSymbol` value.

To see which *keycode* corresponds to a key, see [Keyboard input#Identifying keycodes in Xorg](/index.php/Keyboard_input#Identifying_keycodes_in_Xorg "Keyboard input") for details on the *xev* utility which will output relevant keycode/keysym information about a key when you press it.

**Tip:** There are predefined descriptive *keysyms* for multimedia keys, e.g. `XF86AudioMute` or `XF86Mail`. These *keysyms* can be found in `/usr/include/X11/XF86keysym.h`. Many multimedia programs are designed to work with these *keysyms* out-of-the-box, without the need to configure any third-party application.

Note that xmodmap is influenced by xkbd settings, so all eight keysym are available for the US(intl) xkbd layout but not for the default US (it is missing the ralt_switch symbol defined in level3). To have all 8 keysyms available you should configure the *(intl)* variant of the keyboard. Using US layout as an example, `$ setxkbmap -layout 'us(intl)'` before calling xmodmap to test your changes in the current X session. To permanently make this change, edit the xorg configuration or your .xprofile or .xinitrc file. See [Xorg/Keyboard configuration#Setting keyboard layout](/index.php/Xorg/Keyboard_configuration#Setting_keyboard_layout "Xorg/Keyboard configuration") for a full explanation.

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

With [GDM](/index.php/GDM "GDM"), [XDM](/index.php/XDM "XDM") or [LightDM](/index.php/LightDM "LightDM") there is no need to source `~/.Xmodmap`. For [startx](/index.php/Startx "Startx"), use:

 `~/.xinitrc` 
```
[[ -f ~/.Xmodmap ]] && xmodmap ~/.Xmodmap

```

Alternatively, edit the global startup script `/etc/X11/xinit/xinitrc`.

### Test changes

To make temporary changes:

```
$ xmodmap -e "keycode  46 = l L l L lstroke Lstroke lstroke"
$ xmodmap -e "keysym a = e E"

```

## Modifier keys

*xmodmap* can also be used to override [modifier keys](https://en.wikipedia.org/wiki/Modifier_key "wikipedia:Modifier key"), e.g. to swap `Control` and `Super` (the [Windows key](https://en.wikipedia.org/wiki/Windows_key "wikipedia:Windows key")).

Print the current modifier table verbosely (full sample):

 `$ xmodmap -pm` 
```
xmodmap:  up to 4 keys per modifier, (keycodes in parentheses):

shift       Shift_L (0x32),  Shift_R (0x3e)
lock        Caps_Lock (0x42)
control     Control_L (0x25),  Control_R (0x69)
mod1        Alt_L (0x40),  Meta_L (0xcd)
mod2        Num_Lock (0x94)
mod3      
mod4        Super_R (0x86),  Super_L (0xce),  Hyper_L (0xcf)
mod5        ISO_Level3_Shift (0x5c),  ISO_Level3_Shift (0x6c),  Mode_switch (0x85),  Mode_switch (0xcb)
```

### Finding the keysym column modifier keys

	ISO_Level3_Shift

	The AltGr key on non-US keyboards calls modifier ISO_Level3_Shift. (On US keyboards, the right-alt `Alt_R` has the same function as the left-alt `Alt_L`, which makes setting the layout as US international preferable. See [#Keymap table](#Keymap_table).)

	Mode_switch

	The Mode_switch modifier may be mapped by default to a key that is not on your keyboard.

**Note:** The usage of the modifier names `ISO_Level3_Shift` and `Mode_switch` is different between xmodmap and [X Keyboard Extension](/index.php/X_keyboard_extension#xmodmap "X keyboard extension"). See also [[2]](https://unix.stackexchange.com/questions/55076/what-is-the-mode-switch-modifier-for).

### Reassigning modifiers to keys on your keyboard

**Note:** xmodmap is *case-sensitive*. Using incorrect case, such as `Mode_Switch` instead of the correct `Mode_switch` will cause errors.

Before assignment, the modifier keys need to be cleared. This applies to both modifiers you intend to assign and modifiers on keys that you intend to use. For example, if you intend to assign `Caps_Lock` to your A key and `B` to your NumLock key, you need to first clear the modifiers for both `Caps_Lock` and `Num_Lock`, then assign the keysyms, and finally add back the modifiers.

 `~/.Xmodmap` 
```
[...]
clear lock
clear mod2
keycode  38 = Caps_Lock
keycode  77 = Num_Lock
add lock = Caps_Lock
add mod2 = Num_Lock
```

`!` is a comment, so only the modifiers `Control` and `Mod4` get cleared in the following example. Then the *keysyms* `Control_L`, `Control_R`, `Super_L` and `Super_R` are assigned to the opposite modifier. Assigning both left and right to the same modifier means that both keys are treated the same way.

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

The [natural scrolling](http://who-t.blogspot.com/2011/09/natural-scrolling-in-synaptics-driver.html) feature available in OS X Lion (mimicking smartphone or tablet scrolling) can be [replicated](https://bbs.archlinux.org/viewtopic.php?id=126258) with *xmodmap*. Since the synaptics driver uses the buttons 4/5/6/7 for up/down/left/right scrolling, you simply need to swap the order of how the buttons are declared in `~/.Xmodmap`:

 `~/.Xmodmap`  `pointer = 1 2 3 **5 4** 7 6 8 9 10 11 12` 

Then update *xmodmap*:

```
$ xmodmap ~/.Xmodmap

```

## Swapping mouse buttons

The left, middle and right mouse buttons correspond to buttons 1,2 and 3 respectively in the synaptics driver. To swap left and right mouse buttons, again simply reverse the order in which they are listed in your `~/.Xmodmap`:

 `~/.Xmodmap`  `pointer = **3 2 1**` 

This should suffice for a simple mouse setup. Again, update *xmodmap*:

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

### Turn CapsLock into Control

Simplest example of changing `CapsLock` into `Control`.

 `~/.Xmodmap` 
```
clear lock
clear control
keycode 66 = Control_L
add control = Control_L Control_R

```

### Turn CapsLock into Control, and LeftControl into Hyper

Laptop users may prefer having `CapsLock` as `Control`. The `Left Control` key can be used as a `Hyper` modifier (an additional modifier for emacs or openbox or i3).

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

*   [xmodmap(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xmodmap.1)
*   [Multimediakeys with .Xmodmap HOWTO](http://cweiske.de/howto/xmodmap/allinone.html) by Christian Weiske
*   [Mapping unsupported keys with xmodmap](http://dev-loki.blogspot.com/2006/04/mapping-unsupported-keys-with-xmodmap.html) by Pascal Bleser
*   [List of Keysyms Recognised by Xmodmap](http://wiki.linuxquestions.org/wiki/List_of_Keysyms_Recognised_by_Xmodmap) on [LinuxQuestions](http://linuxquestions.org)