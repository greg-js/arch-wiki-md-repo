Related articles

*   [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers")
*   [Window manager](/index.php/Window_manager "Window manager")

**翻译状态：** 本文是英文页面 [Qtile](/index.php/Qtile "Qtile") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-01-18，点击[这里](https://wiki.archlinux.org/index.php?title=Qtile&diff=0&oldid=538757)可以查看翻译后英文页面的改动。

From [Qtile web site](http://qtile.org/):

	*Qtile 是一个全功能、可轻易修改(骇)的平铺式窗口管理程序。 Qtile 简单、轻巧、扩展性高。 撰写自订的窗口堆叠模式、插件以及指令是轻而易举的事情。程序以及设定均是以 [python](/index.php/Python_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Python (简体中文)") 写成，意味着：您可以使用语言所提供的所有能力及弹性来满足您对窗口管理的需求。*

## Contents

*   [1 安装](#安装)
*   [2 启动](#启动)
*   [3 配置](#配置)
    *   [3.1 群(Groups)](#群(Groups))
    *   [3.2 按键组合(Keys)](#按键组合(Keys))
    *   [3.3 显示器与资讯列(Screens and Bars)](#显示器与资讯列(Screens_and_Bars))
    *   [3.4 插件(Widgets)](#插件(Widgets))
    *   [3.5 启动](#启动_2)
*   [4 除错](#除错)
*   [5 参阅](#参阅)

## 安装

从下列软件包中选择一个进行[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")：

*   [qtile](https://www.archlinux.org/packages/?name=qtile) 最后正式版，基于 Python 3。
*   [qtile-python2](https://aur.archlinux.org/packages/qtile-python2/) 最后正式版，基于 Python 2。
*   [qtile-python3-git](https://aur.archlinux.org/packages/qtile-python3-git/) 最后开发版，基于 Python 3。
*   [qtile-git](https://aur.archlinux.org/packages/qtile-git/) 最后开发版，基于 Python 2。

## 启动

用 [xinit](/index.php/Xinit "Xinit") 执行 `qtile`。

[默认配置](http://docs.qtile.org/en/latest/manual/config/#default-configuration)设置了 `Super+Enter` 作为打开 *xterm* 终端的快捷键，`Super+Ctrl+q` 可以退出 Qile。

## 配置

**注意:** 这个章节只会介绍基本的配置模式，若需更详尽的配置讯息请参见 [官方文档](http://docs.qtile.org/en/latest/)。

[根据配置查询表](http://docs.qtile.org/en/latest/manual/config/default.html#configuration-lookup)， 如果未进行配置，Qtile 会使用默认配置文件中的设置。要自定义配置，先将默认配置文件复制到 `~/.config/qtile/config.py`：

```
$ mkdir -p ~/.config/qtile/
$ cp /usr/share/doc/*qtile_dir*/default_config.py ~/.config/qtile/config.py

```

*   `*qtile_dir*` 是安装的软件包名。
*   最新的默认配置文件位于： [libqtile/resources/default_config.py](https://github.com/qtile/qtile/blob/develop/libqtile/resources/default_config.py).
*   更完整的测试请参考 [qtile-examples](https://github.com/qtile/qtile-examples) 仓库。

整个 Qtile 的配置均是以[python](/index.php/Python_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Python (简体中文)")写成，存放于 `~/.config/qtile/config.py`。

用以下指令测试 config.py 文件是否有语法错误:

```
$ python2 -m py_compile ~/.config/qtile/config.py

```

若编译通过，此设定文件应该便无重大问题。

### 群(Groups)

在 Qtile, 称 工作区(workspaces or views) 为 **群(Groups)**。他们可透过下列方式定义：

```
from libqtile.config import Group, Match
...
groups = [
    Group("term"),
    Group("irc"),
    Group("web", match=Match(title=["Firefox"])),    #表示标题含此关键字的程序均放置于此群中
   ]
...

```

### 按键组合(Keys)

按键组合均放置于 **key** 这个类中。 底下是一个按键范例，按下 `Alt+Shift+q` 则离开 Qtile 回到console>

```
from libqtile.config import Key
from libqtile.command import lazy
...
keys = [
    Key(
        ["mod1", "shift"], "q",
        lazy.shutdown())
   ]
...

```

透过执行 [Xmodmap](/index.php/Xmodmap "Xmodmap") 来得知系统按键与 `modX` 之间的对应关系。

### 显示器与资讯列(Screens and Bars)

为你的每一部显示器配置 **Screen** 类。而 资讯列(bar) 则配置于 **Screen** 类中。

```
from libqtile.config import Screen
from libqtile import bar, widget
...
screens = [
    Screen(                       # 一部显示器
        bottom=bar.Bar([          # 将资讯列(bar)放置于萤幕底部
            widget.GroupBox(),    # 插件，用于显示群的状态
            widget.WindowName()   # 插件，用于显示当前应用程序名称
            ], 30))
   ]
...

```

### 插件(Widgets)

可以从 [官方文档](http://docs.qtile.org/en/latest/manual/ref/widgets.html) 获得关于插件更进一步详细的说明。

若想新增插件，只需要像上面资讯列设定那样调用即可 (如 `WindowName` 插件)。 例如，要新增一个电源资讯显示的插件，我们使用 `Battery` ：

```
from libqtile.config import Screen
from libqtile import bar, widget
...
screens = [
    Screen(top=bar.Bar([
        widget.GroupBox(),    # 插件，用于显示群的状态
        widget.Battery()      # 插件，用于显示电池状态
       ], 30))
   ]
...

```

### 启动

透过捆绑 **钩(hooks)** 我们可以设定许多需要 Qtile 监视的事件。其中一个 `startup` 钩是关注 Qtile 初始化事件的钩，能够在 Qtile 初始化的时连带启动其他的应用程序(一次性指令或应用程序)。其他的 **钩(hook)** 请参件 [官方文档](http://docs.qtile.org/en/latest/manual/ref/hooks.html).

底下是一个关于钩的例子：

```
import subprocess, re

def is_running(process):
    s = subprocess.Popen(["ps", "axw"], stdout=subprocess.PIPE)
    for x in s.stdout:
        if re.search(process, x):
            return True
    return False

def execute_once(process):
    if not is_running(process):
        return subprocess.Popen(process.split())

# 在 Qtile 初始化的时启动应用程式
@hook.subscribe.startup
def startup():
    execute_once("parcellite")
    execute_once("nm-applet")
    execute_once("dropboxd")
    execute_once("feh --bg-scale ~/Pictures/wallpapers.jpg")

```

## 除错

有时候会因为插件的参数没有完整，或者设定之间有冲突情形发生、模组未 import 等，需要检查出错位置，可以以如下方式启动一个虚拟的 Xorg 并进行测试：

```
echo "exec qtile" > /tmp/.start_qtile ; xinit /tmp/.start_qtile -- :2

```

## 参阅

*   [Qtile 官方网站](http://qtile.org/)
*   [官方文档](http://docs.qtile.org/en/latest/)
*   [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers")
*   [xinitrc](/index.php/Xinitrc "Xinitrc")
*   [tilenol](https://github.com/tailhook/tilenol) - 受 Qtile 启发，以 Python3 写成的类似窗口管理程序(注：Qtile 是 Python2)