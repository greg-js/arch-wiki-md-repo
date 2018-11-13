相关文章

*   [Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")
*   [Xmodmap](/index.php/Xmodmap "Xmodmap")
*   [Extra keyboard keys in Xorg](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg")
*   [Extra keyboard keys in console](/index.php/Extra_keyboard_keys_in_console "Extra keyboard keys in console")

许多键盘都有一些"特殊按键"(也叫热键)，用于执行某个应用程序或者输入那些不被包含在标准键盘映射表中的特殊字符。由于没有相应的规格标准，内核无法知道如何处处理它们，这也是为什么我们需要(手工的)将这些按键映射到特定的动作。我们有两种方法来实现：

*   通用的做法，使用 [Xorg](/index.php/Xorg "Xorg") 提供的工具 (以及桌面环境的工具)
*   更快的方式，使用第三方程序，在图形界面中完成所有配置，如 Gnome 控制中心或者[keytouch](/index.php/Keytouch "Keytouch")。

开始之前，你需要学习一些(新)词汇...

**扫描码(scancode)**是一个键的最小识别 ID。如果一个键没有扫描码值，我们无法做任何事，因为内核看不到它。

**键位码(keycode)**是一个键的第二级识别 ID，对应到一个函数。

**符号(symbol)**是一个键的第三级识别 ID，Xorg 通过该 ID 引用按键。

## Contents

*   [1 第一步： 映射扫描码](#第一步：_映射扫描码)
    *   [1.1 使用 xev](#使用_xev)
    *   [1.2 使用 showkey](#使用_showkey)
    *   [1.3 2.6 内核](#2.6_内核)
    *   [1.4 检查扫描码](#检查扫描码)
*   [2 第二步: 映射按键码](#第二步:_映射按键码)
    *   [2.1 终端中](#终端中)
    *   [2.2 Xorg 中](#Xorg_中)
*   [3 笔记本](#笔记本)
    *   [3.1 Asus M series](#Asus_M_series)

## 第一步： 映射扫描码

你的大部分按键应该已经有键位码了，或者至少有扫描码。没有扫描码的键无法被内核识别。

### 使用 xev

使用图形界面程序 "xev" (不需要切换到终端环境)。安装 xev 程序：

 `# pacman -S xorg-xev` 

使用下面一行命令你可以启动 xev 然后直接 grep 到重要的部分：

```
$ xev | grep -A2 --line-buffered '^KeyRelease' | sed -n '/keycode /s/^.*keycode \([0-9]*\).* (.*, \(.*\)).*$/\1 \2/p'

```

在下面的例子中，我按下 "a", "r", "c" 和 "h" 键，以及两个我的 Dell 键盘上的媒体键。这样我得到以下输出：

```
38 a
27 r
54 c
43 h
153 NoSymbol
144 NoSymbol

```

这个输出的意思是 "a", "r", "c" 和 "h" 键的键位码分别是 38, 27, 54 和 43 并且被正确的映射。而键位码 153 和 144 的媒体键没有对应的功能，使用 "NoSymbol" 指示。如果你按下一个按键之后终端里没有显示，那就意味这内核无法看到这个按键或者没有映射。

### 使用 showkey

通常来说，使用`showkey`程序可以知道你的按键是否拥有一个keycode。使用showkey程序后，你可以按下一个按键来查看屏幕上的输出，如果什么都不做，程序将在10秒后退出，这也是退出showkey程序的唯一方法。你需要在一个真正的控制台下执行showkey程序，就是说你得切出图形界面，用ctrl+alt+F1组合键就能回到命令行的界面了。

```
 $ showkey

```

尝试按下你的按键。如果有keycode输出则说明这个键是被映射了的。如果没有，啊，真是一个悲剧。这说明内核认不出这个键或者是这个按键还没被映射。

### 2.6 内核

根据 keymap man page:

**注意:** 在 2.6 内核中，raw 模式，或者叫扫描码模式，一点也不 raw 。扫描码首先翻译成键位码，当需要键位码时再翻译回来...不同的转换被涉及，并且无法确保最终结果与键盘硬件发送的信号对应。

有可能 keymaps 从 showkey 获取的以及 [setkeycodes](/index.php/Setkeycodes "Setkeycodes") 是设置的键位码与 X 中的 xev 获取的值不同。记住当把 keymaps 翻译成 keysyms 时，使用 xmodmap (参见 [Extra keyboard keys in Xorg](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg")).

如果找到了键盘码，请跳到后面的第二步，否则：

### 检查扫描码

如果按键没有键盘码，可以通过 dmesg 命令从内核日志中查找扫描码：

```
$ dmesg|tail -5

```

按下按键后可以看到：

```
atkbd.c: Unknown key pressed (translated set 2, code 0xf1 on isa0060/serio0).
atkbd.c: Use 'setkeycodes e071 <keycode>' to make it known.

```

这样就找到了按键的扫描码，可以映射到键盘码，参见 [Map scancodes to keycodes](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes")。

如果没有新日志信息，说明内核不识别这个按键，无法使用它。

## 第二步: 映射按键码

### 终端中

终端中可以用热键打印某个字符或字符串，如果字符串设置为命令加回车，将自动执行命令！

详情参见： [Extra keyboard keys in console](/index.php/Extra_keyboard_keys_in_console "Extra keyboard keys in console")。

### Xorg 中

图形环境中有多种方式将热键映射到命令，参见：[Extra keyboard keys in Xorg](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg")。

## 笔记本

### Asus M series

可能在其它系列中也可以使用，使用下面方法可以使用多媒体按键，禁用光传感器：编辑 `/etc/rc.local`,添加：

```
$ echo 0 > /sys/devices/platform/asus-laptop/ls_switch

```