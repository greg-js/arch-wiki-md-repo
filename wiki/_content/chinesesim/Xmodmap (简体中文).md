**Xmodmap** is a utility for modifying keymaps and pointer button mappings in [Xorg](/index.php/Xorg "Xorg").

## Contents

*   [1 介绍](#.E4.BB.8B.E7.BB.8D)
*   [2 Keymap表](#Keymap.E8.A1.A8)
*   [3 Custom table](#Custom_table)
    *   [3.1 Test changes](#Test_changes)
*   [4 Special keys/signals](#Special_keys.2Fsignals)
*   [5 Reverse Scrolling](#Reverse_Scrolling)
*   [6 Additional resources](#Additional_resources)

## 介绍

在每次按下键盘时， Linux 内核都会生成一个 Code。 Code 同 `keycodes表` 比较，然后决定按下的是什么。

而 [Xorg](/index.php/Xorg "Xorg") 使用自己的 Keycodes表 来参与这个过程。 每一个 Keycode 属于一个 `keysym`。 一个 keysym 就像一个 function 被 Keycode 调用执行。 Xmodmap 允许你编辑 keycode-keysym 之间的关系。

## Keymap表

以可被解释的格式打印当前 Keymap表，

 `$ xmodmap -pke`  `keycode  57 = n N` 

每条 Keymap 之后都跟随要被映射的 `keysyms`。 下面的例子表明 keycode `57` 被映射到小写 _n_, 同时大写 _N_ 映射于 `57` + `Shift`

每个 keysym列 都对应指定的键组合：

1.  `Key`
2.  `Shift+Key`
3.  `mode_switch+Key`
4.  `mode_switch+Shift+Key`
5.  `AltGr+Key`
6.  `AltGr+Shift+Key`

在 keysym组合 没有被指定时， 使用 `NoSymbol` 代替。

使用 [xev](/index.php/Extra_keyboard_keys#In_Xorg "Extra keyboard keys") 来查看每个键对应的 keymap.

**Tip:** There are predefined descriptive keycodes that make mapping additional keys easier (e.g. `XF86AudioMute`, `XF86Mail`). Those keycodes can be found in: `/usr/include/X11/XF86keysym.h`

## Custom table

You can create your own map and store it in your home directory (i.e. `~/.Xmodmap`). Print the current keymap table into a configuration file:

```
xmodmap -pke > ~/.Xmodmap

```

Make the desired changes to `~/.Xmodmap` and then test the new configuration with:

```
xmodmap ~/.Xmodmap

```

To activate your custom table when starting Xorg add the following:

 `~/.xinitrc` 

```
if [ -f $HOME/.Xmodmap ]; then
    /usr/bin/xmodmap $HOME/.Xmodmap
fi
```

Alternatively, edit the global startup script `/etc/X11/xinit/xinitrc`.

### Test changes

You can also make temporary changes for the current session. For example:

```
xmodmap -e "keycode  46 = l L l L lstroke Lstroke lstroke"
xmodmap -e "keysym a = e E"

```

## Special keys/signals

You can also also edit the keys: `Shift`, `Ctrl`, `Alt` and `Super` (there always exists a left and a right one (Alt_R=AltGr))

At first you have to delete/clear the signals that should be edited. In the beginning of your `~/.Xmodmap`:

```
!clear Shift
!clear Lock
clear Control
!clear Mod1
!clear Mod2
!clear Mod3
clear Mod4
!clear Mod5
keycode   8 =
...

```

Remember, `!` is a comment so only `Control` and `Mod4` (Standard: Super_L Super_R) get cleared.

Write the new signals at the end of `~/.Xmodmap`

```
keycode 255 =
!add Shift   = Shift_L Shift_R
!add Lock    = Caps_Lock
add Control = Super_L Super_R
!add Mod1    = Alt_L Alt_R
!add Mod2    = Mode_switch
!add Mod3    =
add Mod4    = Control_L Control_R
!add Mod5    =

```

The `Super` keys have now been exchanged with the `Ctrl` keys.

附加一个将`CapsLock`映射成`Control`, `Shift+CapsLock`映射成`CapsLock`的例子： `~/.Xmodmap`

```
clear lock
clear control
add control = Caps_Lock Control_L Control_R
keycode 66 = Control_L Caps_Lock NoSymbol NoSymbol

```

## Reverse Scrolling

The natural scrolling feature available in OS X Lion can be mimicked with xmodmap. Since the synaptics driver uses the buttons 4/5/6/7 for up/down/left/right scrolling, you simply need to swap the order of how the buttons are declared in `~/.Xmodmap`.

Open `~/.Xmodmap` and append the following line to the file:

```
pointer = 1 2 3 5 4 7 6 8 9 10 11 12

```

Note how the 4 and 5 have been reversed.

Then update xmodmap:

```
xmodmap ~/.Xmodmap

```

To return to regular scrolling simply reverse the order of the 4 and 5 or delete the line altogether. For more information check Peter Hutterer's post, [Natural scrolling in the synaptics driver](http://who-t.blogspot.com/2011/09/natural-scrolling-in-synaptics-driver.html), or the [Reverse scrolling direction ala Mac OS X Lion?](https://bbs.archlinux.org/viewtopic.php?id=126258) forum thread.

## Additional resources

*   [Current man page](http://www.x.org/archive/current/doc/man/man1/xmodmap.1.xhtml) at X.Org Foundation
*   [Multimediakeys with .Xmodmap HOWTO](http://cweiske.de/howto/xmodmap/allinone.html) by Christian Weiske
*   [Mapping unsupported keys with xmodmap](http://dev-loki.blogspot.com/2006/04/mapping-unsupported-keys-with-xmodmap.html) by Pascal Bleser
*   [How to retrieve scancodes](http://keytouch.sourceforge.net/howto_keyboard/node4.html) by Marvin Raaijmakers
*   [List of Keysyms Recognised by Xmodmap](http://wiki.linuxquestions.org/wiki/List_of_Keysyms_Recognised_by_Xmodmap) on [LinuxQuestions](http://linuxquestions.org)