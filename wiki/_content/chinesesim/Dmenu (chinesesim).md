## Contents

*   [1 介绍](#介绍)
*   [2 安装](#安装)
*   [3 设置](#设置)
*   [4 延伸](#延伸)
*   [5 其他资源](#其他资源)

## 介绍

dmenu是一个X下的快速、轻量级的软件启动器，为他绑定一个快捷键，输入你想启动的软件的名字，Enter！

## 安装

安装dmenu是很简单的：

```
# pacman -S dmenu

```

运行

```
$ dmenu_run

```

## 设置

现在你可以将此命令关联到一个快捷键，很多窗口管理器和桌面环境都有设置工具可以做到，用[xbindkeys](/index.php/Xbindkeys "Xbindkeys")也可以做到，想得到更详细的信息参见[Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")条目。

## 延伸

```
$ pacman -Ql dmenu | grep bin
dmenu /usr/bin/dmenu
dmenu /usr/bin/dmenu_path
dmenu /usr/bin/dmenu_run

```

可见/usr/bin/下有三个文件，其中**dmenu_path**和**dmenu_run**是两个shell脚本，真正的执行/显示部分都由**dmenu**完成，其中**dmenu_path**用于列出$PATH里的可执行文件，每个文件名一行，然后通过“|”传递给**dmenu**，具体语法可从**dmenu_run**里找到。 你也可以在终端里执行：

```
$ echo | dmenu

```

然后输入任意字串，这个字串就会被显示在终端里，这其实才是dmenu的核心功能。

由此配合其他工具可以完成其他任务，比如运行：

```
$ notify-send "`exec $(echo | dmenu)`"

```

你可以试着在运行后输入date，之后系统就会借助notify-send弹出日期提示。

## 其他资源

*   [dmenu](http://tools.suckless.org/dmenu) - dmenu官方网站
*   [Yeganesh](http://dmwit.com/yeganesh) - dmenu的一个前段处理器，可以按照使用频率进行排序
*   [LinuxTOY](http://linuxtoy.org/archives/dmenu.html) - dmenu运行后的效果图