From [Qtile web site](http://qtile.org/):

	*Qtile 是一个全功能、可轻易修改(骇)的平铺式窗口管理程序。 Qtile 简单、轻巧、扩展性高。 撰写自订的窗口堆叠模式、插件以及指令是轻而易举的事情。程序以及设定均是以 [python](/index.php/Python_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Python (简体中文)") 写成，意味着：您可以使用语言所提供的所有能力及弹性来满足您对窗口管理的需求。*

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 启动Ｑtile](#.E5.90.AF.E5.8A.A8.EF.BC.B1tile)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 群(Groups)](#.E7.BE.A4.28Groups.29)
    *   [3.2 按键组合(Keys)](#.E6.8C.89.E9.94.AE.E7.BB.84.E5.90.88.28Keys.29)
    *   [3.3 显示器与资讯列(Screens and Bars)](#.E6.98.BE.E7.A4.BA.E5.99.A8.E4.B8.8E.E8.B5.84.E8.AE.AF.E5.88.97.28Screens_and_Bars.29)
    *   [3.4 插件(Widgets)](#.E6.8F.92.E4.BB.B6.28Widgets.29)
    *   [3.5 啟動(Startup)](#.E5.95.9F.E5.8B.95.28Startup.29)
    *   [3.6 音效(Sound)](#.E9.9F.B3.E6.95.88.28Sound.29)
*   [4 除错(Debugging)](#.E9.99.A4.E9.94.99.28Debugging.29)
*   [5 Hacking Qtile](#Hacking_Qtile)
    *   [5.1 预备](#.E9.A2.84.E5.A4.87)
    *   [5.2 关于钩(hook)](#.E5.85.B3.E4.BA.8E.E9.92.A9.28hook.29)
    *   [5.3 关于插件(widget)](#.E5.85.B3.E4.BA.8E.E6.8F.92.E4.BB.B6.28widget.29)
*   [6 相关文件](#.E7.9B.B8.E5.85.B3.E6.96.87.E4.BB.B6)

## 安装

从 [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") 安装 [qtile-git](https://aur.archlinux.org/packages/qtile-git/)。

缺省配置可以参考[Github源](https://github.com/qtile/qtile/blob/master/libqtile/resources/default_config.py)或从该源复制一份，存放于 `~/.config/qtile/config.py`：

```
$ mkdir -p ~/.config/qtile/
$ wget [https://raw.github.com/qtile/qtile/develop/libqtile/resources/default_config.py](https://raw.github.com/qtile/qtile/develop/libqtile/resources/default_config.py) -O - > ~/.config/qtile/config.py

```

若无法从Github获得缺省配置，也可以以下列方式获得一份复制：

```
$ rm ~/.config/qtile/config.py
$ cp  /usr/lib/python2.7/site-packages/libqtile/resources/default_config.py ~/.config/qtile/config.py

```

## 启动Ｑtile

将 Ｑtile 指令 `exec qtile` 加入 `~/.xinitrc` 并启动 [Xorg](/index.php/Xorg "Xorg")。 缺省启动一个新的 `xterm` 终端的按键组合是：`Alt+Enter`。

## 配置

**注意:** 这个章节只会介绍基本的配置模式，若需更详尽的配置讯息请参见 [官方文档](http://docs.qtile.org/en/latest/)。

整个 Qtile 的配置均是以[python](/index.php/Python_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Python (简体中文)")写成，存放于 `~/.config/qtile/config.py`。 若需对 [python](/index.php/Python_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Python (简体中文)") 有*快速概览*的需求，可以阅读 [这份教程](https://developers.google.com/edu/python/introduction)。 此教程将讲解关于 [python](/index.php/Python_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Python (简体中文)") 变数、函数、模组以及其他配置 qtile 所需要的预备知识。

透过以下指令测试你所编写的 config.py 文件是否有语法上的错误。

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

### 啟動(Startup)

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

### 音效(Sound)

能透过键组合来操控 `alsamixer` 来快速调整音量以及静音与否。使用者必须是 **audio gropu** 的成员。

```
keys= [
    ...
    # 音效设置，未绑定键配置！
    Key([], "XF86AudioMute", lazy.spawn("amixer -q set Master toggle")),
    Key([], "XF86AudioLowerVolume", lazy.spawn("amixer -c 0 sset Master 1- unmute")),
    Key([], "XF86AudioRaiseVolume", lazy.spawn("amixer -c 0 sset Master 1+ unmute"))
   ]

```

## 除错(Debugging)

有时候会因为插件的参数没有完整，或者设定之间有冲突情形发生、模组未 import 等，需要检查出错位置，可以以如下方式启动一个虚拟的 Xorg 并进行测试：

```
echo "exec qtile" > /tmp/.start_qtile ; xinit /tmp/.start_qtile -- :2

```

## Hacking Qtile

**注意:** 本说明为非官方文件翻译而来，请勿将用于生产的桌面环境进行不保证稳定的修改行为。

目前官方的开发状况：

*   [Qtile 官方文档](http://docs.qtile.org/en/latest/) 是 Qtile 0.5 的说明文件，而在函式库的呼叫上， 0.5 版与 0.6 版有不相容的差异；这些差异将会使 [缺省配置](https://github.com/qtile/qtile/blob/master/libqtile/resources/default_config.py) 无法于 Qtile 0.5 上运行。
    *   Ubuntu PPA 包含的是 Qtile 0.5
    *   ArchLinux 的 [qtile-git](https://aur.archlinux.org/packages/qtile-git/) 则是最新的 Qtile 0.6
*   依照邮件列表内开发者的意思， Qtile 并不打算撰写完整的说明文件，而是优先扩充 *问与答 (FAQ)* ，而若有细节需求，会请求直接阅读源码。
*   Qtile 可以很好的与其他桌面环境组件协调运作。

### 预备

*   关于 [Xephyr](http://awesome.naquadah.org/wiki/Using_Xephyr) 使用方式的基本知识，请避免在实验期间重启 Qtile。
*   关于 [python](/index.php/Python_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Python (简体中文)") 的操作能力。

### 关于钩(hook)

### 关于插件(widget)

## 相关文件

*   [Qtile 官方网站](http://qtile.org/)
*   [官方文档](http://docs.qtile.org/en/latest/)
*   [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers")
*   [xinitrc](/index.php/Xinitrc "Xinitrc")
*   [tilenol](https://github.com/tailhook/tilenol) - 受 Qtile 启发，以 Python3 写成的类似窗口管理程序(注：Qtile 是 Python2)