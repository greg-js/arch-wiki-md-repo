Fbterm (**F**rame **b**uffer **term**inal)是内核终端的直接替代：一个没有 Xorg 也能使用的终端模拟器。

**警告:** Fbterm 的开发已经停止。

## Contents

*   [1 功能](#功能)
*   [2 安装](#安装)
*   [3 自定义](#自定义)
    *   [3.1 配置文件](#配置文件)
    *   [3.2 字体](#字体)
    *   [3.3 输入法支持](#输入法支持)
*   [4 提示与技巧](#提示与技巧)
    *   [4.1 背景图](#背景图)
    *   [4.2 白色字体](#白色字体)

## 功能

摘自 [http://code.google.com/p/fbterm/](http://code.google.com/p/fbterm/):

	FbTerm 是一个使用 frame buffer 设备或 VESA 显卡的终端模拟器，功能包括：

*   若加速滚动开启的话，速度可和linux核心的终端媲美
*   使用fontconfig选择字体，和Qt/GTK+上用的应用一样，使用freetype2来绘制字体
*   动态创建和销毁最多10个原生运行默认shell的窗口
*   记录任何窗口的回滚历史
*   自动检测目前本地化环境下的文本内码，支持双字节脚本，比如中文、日文等
*   在线热键切换配置的额外文本内码
*   当gpm服务器运行时，可使用鼠标在窗口间复制和粘贴选择的文本
*   可改屏幕显示方式，比如：屏幕翻转
*   C/S结构（客户端/服务器）的轻量级输入法框架
*   背景图片

## 安装

~~Fbterm 可以通过官方软件仓库中 [fbterm](https://www.archlinux.org/packages/?name=fbterm) 安装。~~

**注意:** 官方软件仓库已经没有 Fbterm

安装完成之后，请注意其后续说明：

```
==> 若想使用非根用户运行fbterm，需要把用户加入video组：
sudo gpasswd -a YOUR_USERNAME video
==> 若想非根用户可使用键盘快捷方式，需要：
sudo setcap 'cap_sys_tty_config+ep' /usr/bin/fbterm
或者：
sudo chmod u+s /usr/bin/fbterm

```

## 自定义

### 配置文件

Fbterm 使用 ~/.fbtermrc 来进行配置。该文件将在第一次运行 Fbterm 之后自动生成。文件内有详细的注释，可以帮助您了解如何配置 Fbterm。

### 字体

Fbterm 使用 [fontconfig](https://en.wikipedia.org/wiki/fontconfig "wikipedia:fontconfig") 管理字体，试一下每一个字体直到可以渲染字符。

要修改字体，从 `fc-list` 给出的列表中选定一个字体，用 `--font-names` 选项指定。

### 输入法支持

目前，Fbterm支持不同的[输入法](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method")，通过作为一个独立的输入法服务器的客户端。[Internationalization#Input methods](/index.php/Internationalization#Input_methods "Internationalization") 记录了 Arch 支持的几个程序。

中文用户可以安装官方软件仓库中的 [fcitx-fbterm](https://www.archlinux.org/packages/?name=fcitx-fbterm) 来输入中文。在安装好 fcitx-fbterm 之后，直接启动 `fcitx-fbterm-helper` 或修改 `~/.fbtermrc` 文件中的 `input-method` 行为

```
input-method=fcitx-fbterm

```

启动 Fbterm 即可。

## 提示与技巧

### 背景图

想要使用背景图片，Fbterm 可以设置成启动时截取 frame buffer 设备的屏幕。

下面的脚本 (使用 [fbv](https://www.archlinux.org/packages/?name=fbv) 图形查看器) 是在man页面推荐的：

```
#!/bin/bash
# fbterm-bi: a wrapper script to enable background image with fbterm
# usage: fbterm-bi /path/to/image fbterm-options
echo -ne "\e[?25l" # hide cursor
fbv -ciuker "$1" << EOF
q
EOF
shift
export FBTERM_BACKGROUND_IMAGE=1
exec fbterm "$@"

```

### 白色字体

默认配置下，fbterm 把白色的文字显示成灰色，即使使用 -f 7 开关也不行。 可以通过在 feterm 中运行 echo 一次来得到真正的白色，例如：

```
echo -en "\e]P7ffffff"

```