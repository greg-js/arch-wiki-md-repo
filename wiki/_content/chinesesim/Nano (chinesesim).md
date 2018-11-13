**翻译状态：** 本文是英文页面 [Nano](/index.php/Nano "Nano") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-8-28，点击[这里](https://wiki.archlinux.org/index.php?title=Nano&diff=0&oldid={{{3}}})可以查看翻译后英文页面的改动。

[GNU nano](https://www.nano-editor.org/) （或 nano）是一个基于控制台的文本编辑器，旨在提供一个简单的界面和直观的命令选项。 *nano* 支持的功能包括语法高亮、DOS/Mac 文件格式转换、拼写检查和[UTF-8](https://en.wikipedia.org/wiki/UTF-8 "wikipedia:UTF-8")编码。 用空缓冲区打开的*nano*通常占用少于4MB的驻留内存。

## Contents

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 语法高亮](#语法高亮)
        *   [2.1.1 PKGBUILD](#PKGBUILD)
    *   [2.2 挂起](#挂起)
    *   [2.3 文本换行](#文本换行)
*   [3 使用](#使用)
    *   [3.1 特殊按键](#特殊按键)
*   [4 提示和技巧](#提示和技巧)
    *   [4.1 用nano替换vi](#用nano替换vi)
*   [5 问题解决](#问题解决)
    *   [5.1 快捷键绑定冲突](#快捷键绑定冲突)
*   [6 参考](#参考)

## 安装

*Nano* 对应的软件包是 [nano](https://www.archlinux.org/packages/?name=nano) 已经属于 [base](https://www.archlinux.org/groups/x86_64/base/) 组，所以通常已经安装在系统中。

## 配置

Nano的外观、感觉和功能通常由命令行参数或者配置文件`~/.config/nano/nanorc`控制。

程序安装时会同时安装一个示例配置文件，位于`/etc/nanorc`。 要自定义配置，首先复制一份配置文件到`~/.config/nano/nanorc`：

```
$ cp /etc/nanorc ~/.config/nano/nanorc

```

通过设置`~/.config/nano/nanorc`文件中的参数控制nano的设置。

**提示：** [nanorc(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nanorc.5)列出nano的全部可用配置选项。

**注意:** 命令行参数会优先覆盖配置文件`~/.config/nano/nanorc`中的参数。

### 语法高亮

Nano包含预定义的[语法高亮](https://en.wikipedia.org/wiki/Syntax_highlighting "wikipedia:Syntax highlighting")规则，位于文件`/usr/share/nano/*.nanorc`。 添加以下配置到`~/.config/nano/nanorc`或者`/etc/nanorc`使语法高亮生效：

```
include "/usr/share/nano/*.nanorc"

```

可以在AUR（[nano-syntax-highlighting-git](https://aur.archlinux.org/packages/nano-syntax-highlighting-git/)）找到默认语法高亮规则的增强扩展。 参考[[1]](https://paste.xinu.at/wc17YG/)，用于[Forth](https://en.wikipedia.org/wiki/Forth_(programming_language) "w:Forth (programming language)")突出显示。

#### PKGBUILD

*   将 [https://paste.xinu.at/4ss/](https://paste.xinu.at/4ss/) （类似 [svntogit-server](https://projects.archlinux.org/svntogit/packages.git/tree)）保存到 `/etc/nano/pkgbuild.nanorc`，引用它：

```
include "/etc/nano/pkgbuild.nanorc"

```

*   还可以选择安装 [nano-syntax-highlighting-git](https://aur.archlinux.org/packages/nano-syntax-highlighting-git/)

### 挂起

Nano与大部分交互程序不同，默认情况下关闭挂起功能。 取消`/etc/nanorc`中`set suspend`行的注释以启用挂起功能。 允许用按键`Ctrl+z`使nano挂起到后台。

### 文本换行

*Nano*与大部分文本编辑器不同，默认文本自动换行。 要关闭自动换行，在`~/.config/nano/nanorc`添加以下参数：

```
set nowrap

```

## 使用

快捷键提示可以在*nano*中看到。 Nano中可以用`Ctrl+g`打开在线帮助，[nano Command Manual](https://www.nano-editor.org/dist/latest/nano.html)可以查看详细说明和帮助。

### 特殊按键

Nano在屏幕底部两行显示功能快捷键。

表示方式如下：

*   `^`表示按住键盘上的`Ctrl`
*   `M-`表示按住键盘上的*`Meta`*（通常是`Alt`）或`Esc`

**提示：** [Feature Toggles](https://www.nano-editor.org/dist/latest/nano.html#Feature-Toggles)列出nano全部可用快捷键。

## 提示和技巧

### 用nano替换vi

要用nano替换vi作为控制台默认文本编辑器，例如用于[visudo](/index.php/Sudo#Using_visudo "Sudo")，设置`VISUAL`和`EDITOR` [环境变量](/index.php/Environment_variable#Defining_variables "Environment variable")，示例：

```
export VISUAL=nano
export EDITOR=nano

```

## 问题解决

### 快捷键绑定冲突

部分窗口管理器会与nona的快捷键冲突，例如`Alt+Enter`。 删除或重新绑定快捷键例如`Super`（用[mutter](https://www.archlinux.org/packages/?name=mutter)、[muffin](https://www.archlinux.org/packages/?name=muffin)和[marco](https://www.archlinux.org/packages/?name=marco)修改[dconf](https://www.archlinux.org/packages/?name=dconf)），然后重新启动窗口管理器。

## 参考

*   [nano (text editor)](https://en.wikipedia.org/wiki/Nano_(text_editor) - Wikipedia入口
*   [GNU nano Homepage](https://www.nano-editor.org/) - 官方网页
*   [GNU nano Bugs](https://savannah.gnu.org/bugs/?group=nano) 报告bug
*   [Nano语法高亮文件扩展](https://github.com/scopatz/nanorc)