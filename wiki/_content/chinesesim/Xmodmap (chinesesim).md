相关文章

*   [Xorg](/index.php/Xorg "Xorg")
*   [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")
*   [Extra keyboard keys in Xorg](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg")
*   [Extra keyboard keys in console](/index.php/Extra_keyboard_keys_in_console "Extra keyboard keys in console")

**Xmodmap** is a utility for modifying keymaps and pointer button mappings in [Xorg](/index.php/Xorg "Xorg").

## Contents

*   [1 介绍](#介绍)
*   [2 Keymap表](#Keymap表)
*   [3 自定义映射表](#自定义映射表)
    *   [3.1 测试你的修改](#测试你的修改)
*   [4 特殊的按键](#特殊的按键)
*   [5 MAC OS X的自然滚动](#MAC_OS_X的自然滚动)
*   [6 Additional resources](#Additional_resources)

## 介绍

在每次按下键盘时， Linux 内核都会生成一个 Code。 Code 同 `keycodes表` 比较，然后决定按下的是什么。

而 [Xorg](/index.php/Xorg "Xorg") 使用自己的 Keycodes表 来参与这个过程。 每一个 Keycode 属于一个 `keysym`。 一个 keysym 就像一个 function 被 Keycode 调用执行。 Xmodmap 允许你编辑 keycode-keysym 之间的关系。

## Keymap表

以可被解释的格式打印当前 Keymap表，

 `$ xmodmap -pke`  `keycode  57 = n N` 

每条 Keymap 之后都跟随要被映射的 `keysyms`。 下面的例子表明 keycode `57` 被映射到小写 *n*, 同时大写 *N* 映射于 `57` + `Shift`

每个 keysym列 都对应指定的键组合：

1.  `Key`
2.  `Shift+Key`
3.  `mode_switch+Key`
4.  `mode_switch+Shift+Key`
5.  `AltGr+Key`
6.  `AltGr+Shift+Key`

在 keysym组合 没有被指定时， 使用 `NoSymbol` 代替。

使用 [xev](/index.php/Extra_keyboard_keys#In_Xorg "Extra keyboard keys") 来查看每个键对应的 keymap.

**Tip:** 有一些预定义的keycodes被映射成附加的快捷键 (e.g. `XF86AudioMute`, `XF86Mail`). 那些keycodes能在这个文件找到: `/usr/include/X11/XF86keysym.h`

## 自定义映射表

你可以创建自己的映射表并且把它储存在你的`home`目录下(i.e. `~/.Xmodmap`). 输出当前键盘映射表到一个配置文件中：

```
xmodmap -pke > ~/.Xmodmap

```

在 `~/.Xmodmap` 文件中做好想要的修改 然后测试新的配置文件：

```
xmodmap ~/.Xmodmap

```

要在启动Xorg时激活你自己的映射表，请添加下面的文件和内容：

 `~/.xinitrc` 
```
if [ -f $HOME/.Xmodmap ]; then
    /usr/bin/xmodmap $HOME/.Xmodmap
fi
```

或者你也可以编辑全局启动脚本 `/etc/X11/xinit/xinitrc`.

### 测试你的修改

你也可以在当前会话做临时的修改。 一个例子：

```
xmodmap -e "keycode  46 = l L l L lstroke Lstroke lstroke"
xmodmap -e "keysym a = e E"

```

## 特殊的按键

你也可以编辑这些特殊的按键： `Shift`, `Ctrl`, `Alt` and `Super` (这里存在左右之分 (Alt_R=AltGr))

首先你必须delete/clear你想要编辑的按键在`~/.Xmodmap`这个文件的开头:

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

记住, `!` 是一个注释符号 所以只有 `Control` 和 `Mod4` (Standard: Super_L Super_R) 被clear了.

把你的修改写到 `~/.Xmodmap` 文件末尾

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

现在 `Super` 键 和 `Ctrl` 键被交换了.

附加一个将`CapsLock`映射成`Control`, `Shift+CapsLock`映射成`CapsLock`的例子： `~/.Xmodmap`

```
clear lock
clear control
add control = Caps_Lock Control_L Control_R
keycode 66 = Control_L Caps_Lock NoSymbol NoSymbol

```

## MAC OS X的自然滚动

你能用xmodmap去模仿OS X上的自然滚动（反向滚动） 因为synaptics驱动使用按键 4/5/6/7 作为 up/down/left/right 滚动, 你只需要交换按钮的命令，它的描述在这个文件 `~/.Xmodmap` 里.

打开 `~/.Xmodmap` 文件，然后把下面这行添加到文件里面：

```
pointer = 1 2 3 5 4 7 6 8 9 10 11 12

```

现在4和5互换了 然后更新xmodmap的设置:

```
xmodmap ~/.Xmodmap

```

恢复只需要交换4和5或者完全删除那行. 获取更多的信息请查看Peter Hutterer的帖子, [Natural scrolling in the synaptics driver](http://who-t.blogspot.com/2011/09/natural-scrolling-in-synaptics-driver.html), 或者 [Reverse scrolling direction ala Mac OS X Lion?](https://bbs.archlinux.org/viewtopic.php?id=126258) 论坛帖子

## Additional resources

*   [Current man page](http://www.x.org/archive/current/doc/man/man1/xmodmap.1.xhtml) at X.Org Foundation
*   [Multimediakeys with .Xmodmap HOWTO](http://cweiske.de/howto/xmodmap/allinone.html) by Christian Weiske
*   [Mapping unsupported keys with xmodmap](http://dev-loki.blogspot.com/2006/04/mapping-unsupported-keys-with-xmodmap.html) by Pascal Bleser
*   [How to retrieve scancodes](http://keytouch.sourceforge.net/howto_keyboard/node4.html) by Marvin Raaijmakers
*   [List of Keysyms Recognised by Xmodmap](http://wiki.linuxquestions.org/wiki/List_of_Keysyms_Recognised_by_Xmodmap) on [LinuxQuestions](http://linuxquestions.org)