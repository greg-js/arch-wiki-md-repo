相关文章

*   [Composite](/index.php/Composite "Composite")
*   [Compiz](/index.php/Compiz_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Compiz (简体中文)")
*   [Window manager](/index.php/Window_manager "Window manager")

**翻译状态：** 本文是英文页面 [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-06-22，点击[这里](https://wiki.archlinux.org/index.php?title=Xcompmgr&diff=0&oldid=376307)可以查看翻译后英文页面的改动。

**Xcompmgr**是一个简单的混合窗口管理器，可以实现阴影、原生窗口透明（配合`transset`工具）等特效。Xcompmgr设计初衷只是实现混合窗口管理器的概念，所以比起同类混合窗口管理器如 [Compiz Fusion](/index.php/Compiz_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Compiz (简体中文)")，Xcompmgr轻量许多。

Xcompmgr不替代任何窗口管理器，所以对于[Openbox](/index.php/Openbox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Openbox (简体中文)")和[Fluxbox](/index.php/Fluxbox "Fluxbox")这类缺乏特效的[窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")来讲，配合Xcompmgr能得到更华丽的视觉效果。

## Contents

*   [1 安装](#安装)
    *   [1.1 分支版本](#分支版本)
*   [2 配置](#配置)
    *   [2.1 窗口透明度](#窗口透明度)
*   [3 小提示](#小提示)
    *   [3.1 方便开关xcompmgr的脚本](#方便开关xcompmgr的脚本)
    *   [3.2 仅用一个快捷键就切换 xcompmgr](#仅用一个快捷键就切换_xcompmgr)
*   [4 疑难解答](#疑难解答)
    *   [4.1 Mozilla Firefox 打开 Flash 时崩溃](#Mozilla_Firefox_打开_Flash_时崩溃)
    *   [4.2 登陆后变成浅灰色背景 （如Openbox）](#登陆后变成浅灰色背景_（如Openbox）)
    *   [4.3 在 awesome 窗口管理器中出现 BadPicture request](#在_awesome_窗口管理器中出现_BadPicture_request)
    *   [4.4 Chromium & Xcompmgr & Awesome & Conky](#Chromium_&_Xcompmgr_&_Awesome_&_Conky)

## 安装

在安装 Xcompmgr 前，请先确认您已经正确安装并配置了 [Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")。如果你使用了自定义配置，请打开X服务器中的 [Composite](/index.php/Composite "Composite") 拓展。

您可以直接从[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")中安装[xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr)以及透明度设置工具[transset-df](https://www.archlinux.org/packages/?name=transset-df)。

### 分支版本

您还可以选用 Xcompmgr 的分支版本，它们修正了一些错误：

*   **xcompmgr-dana** — One of the first forks of Xcompmgr.

	[http://oliwer.net/xcompmgr-dana/](http://oliwer.net/xcompmgr-dana/) || [xcompmgr-dana](https://aur.archlinux.org/packages/xcompmgr-dana/)

*   **[Compton](/index.php/Compton "Compton")** — A fork of Xcompmgr that contains most of the previous fixes as well as many others.

	[https://github.com/chjj/compton](https://github.com/chjj/compton) || [compton-git](https://aur.archlinux.org/packages/compton-git/)

## 配置

运行 `xcompmgr`：

```
$ xcompmgr -c

```

如果要在每次 Xorg 启动时运行，添加以下内容到[xprofile](/index.php/Xprofile "Xprofile")：

```
xcompmgr -c &

```

用户可以通过命令行参数调整阴影、消隐等效果，以下是一个常用的配置：

```
xcompmgr -c -C -t-5 -l-5 -r4.2 -o.55 &

```

查看命令行帮助：

```
$ xcompmgr --help

```

### 窗口透明度

`transset-df` 工具用来设置单个窗口的透明度，透明特效可能会降低系统性能。

先启动要设置透明度的程序，然后运行：

```
transset-df n

```

.. 此处 `n` 是0到1之间的数字，0表示完全透明（不可见），1表示不透明。例如：`transset .25` 代表75%的透明度。

运行后，鼠标会变成十字形。点击要设置的窗口，即可应用透明度设置。

## 小提示

### 方便开关xcompmgr的脚本

把这个脚本放在合适的应用程序目录，可以方便地启动、关闭xcompmgr。

```
#!/bin/bash
#
# Start a composition manager.
# (xcompmgr in this case)

comphelp() {
  echo "Composition Manager:"
  echo "   (re)start: COMP"
  echo "   stop:      COMP -s"
  echo "   query:     COMP -q"
  echo "              returns 0 if composition manager is running, else 1"
  exit
}

checkcomp() {
  pgrep xcompmgr &>/dev/null
}

stopcomp() {
  checkcomp && killall xcompmgr
}

startcomp() {
  stopcomp
# Example settings only. Replace with your own.
  xcompmgr -CcfF -I-.015 -O-.03 -D6 -t-1 -l-3 -r4.2 -o.5 &
  exit
}

case "$1" in
    "") startcomp ;;
  "-q") checkcomp ;;
  "-s") stopcomp; exit ;;
     *) comphelp ;;
esac

```

### 仅用一个快捷键就切换 xcompmgr

利用上面脚本的状态部分，将下面脚本设置为某个快捷键的脚本：

```
#!/bin/bash

if pgrep xcompmgr &>/dev/null; then
       echo "Turning xcompmgr ON"
       xcompmgr -c -C -t-5 -l-5 -r4.2 -o.55 &
else
       echo "Turning xcompmgr OFF"
       pkill xcompmgr &
fi

exit 0

```

## 疑难解答

### Mozilla Firefox 打开 Flash 时崩溃

新建可执行文件`/etc/profile.d/flash.sh`，文件内容如下：

```
export XLIB_SKIP_ARGB_VISUALS=1

```

这将关闭混合特效。

### 登陆后变成浅灰色背景 （如Openbox）

安装[hsetroot](https://www.archlinux.org/packages/?name=hsetroot)，在运行xcompmgr之前，执行`hsetroot -solid "#000000"`（将000000替换成你想要的颜色代码）。

### 在 awesome 窗口管理器中出现 BadPicture request

如果你在 [awesome](/index.php/Awesome "Awesome") 得到以下错误信息：

```
 error 163: BadPicture request 149 minor 8 serial 34943
 error 163: BadPicture request 149 minor 8 serial 34988
 error 163: BadPicture request 149 minor 8 serial 35033

```

只需要安装软件包 [feh](/index.php/Feh "Feh") 然后重启 [awesome](/index.php/Awesome "Awesome")。

### Chromium & Xcompmgr & Awesome & Conky

I got some problems at startup after changing the displayresolution and autostarting Chromium in AwesomeWM (laptop with external monitor). In Combination with Conky there is always some part of the screen "stuck", the problem came from my resolution change at start via `.xinitrc` and Awesome setting the background afterwards via feh. I solved this by putting

```
hsetroot -solid "#000066"

```

in my .xinitrc just before xcompmgr.