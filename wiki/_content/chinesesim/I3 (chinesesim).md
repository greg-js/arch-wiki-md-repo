**翻译状态：** 本文是英文页面 [i3](/index.php/I3 "I3") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-05-11，点击[这里](https://wiki.archlinux.org/index.php?title=i3&diff=0&oldid=313232)可以查看翻译后英文页面的改动。

[i3](http://i3wm.org/) 是一套动态[平铺式窗口管理器](https://en.wikipedia.org/wiki/Tiling_window_manager "wikipedia:Tiling window manager")，灵感来自针对开发者与资深用户的 [wmii](/index.php/Wmii "Wmii")。

一棵包含容器的树形数据结构组织在一起就变成了客户端（桌面）。树枝由水平或垂直分割而产生，且容器可以被布局成分页式（Tabbed），或叠放式（Stacked）。当窗口的平铺式效果不太好时，可以改为浮动式窗口，不过会被放到独立于平铺式窗口之外的分层上。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 通过 xinitrc 运行 i3](#.E9.80.9A.E8.BF.87_xinitrc_.E8.BF.90.E8.A1.8C_i3)
*   [3 使用](#.E4.BD.BF.E7.94.A8)
    *   [3.1 默认键绑定](#.E9.BB.98.E8.AE.A4.E9.94.AE.E7.BB.91.E5.AE.9A)
    *   [3.2 程序启动器](#.E7.A8.8B.E5.BA.8F.E5.90.AF.E5.8A.A8.E5.99.A8)
*   [4 设置](#.E8.AE.BE.E7.BD.AE)
    *   [4.1 状态栏](#.E7.8A.B6.E6.80.81.E6.A0.8F)
        *   [4.1.1 新方案：i3bar](#.E6.96.B0.E6.96.B9.E6.A1.88.EF.BC.9Ai3bar)
        *   [4.1.2 更多可选方案](#.E6.9B.B4.E5.A4.9A.E5.8F.AF.E9.80.89.E6.96.B9.E6.A1.88)
        *   [4.1.3 面板可选方案](#.E9.9D.A2.E6.9D.BF.E5.8F.AF.E9.80.89.E6.96.B9.E6.A1.88)
        *   [4.1.4 Iconic fonts in the status bar](#Iconic_fonts_in_the_status_bar)
    *   [4.2 在窗口之间快速跳转](#.E5.9C.A8.E7.AA.97.E5.8F.A3.E4.B9.8B.E9.97.B4.E5.BF.AB.E9.80.9F.E8.B7.B3.E8.BD.AC)
    *   [4.3 i3status](#i3status)
        *   [4.3.1 添加温度状态](#.E6.B7.BB.E5.8A.A0.E6.B8.A9.E5.BA.A6.E7.8A.B6.E6.80.81)
    *   [4.4 修改工作区的名称](#.E4.BF.AE.E6.94.B9.E5.B7.A5.E4.BD.9C.E5.8C.BA.E7.9A.84.E5.90.8D.E7.A7.B0)
    *   [4.5 让程序启动时，只出现在指定工作区](#.E8.AE.A9.E7.A8.8B.E5.BA.8F.E5.90.AF.E5.8A.A8.E6.97.B6.EF.BC.8C.E5.8F.AA.E5.87.BA.E7.8E.B0.E5.9C.A8.E6.8C.87.E5.AE.9A.E5.B7.A5.E4.BD.9C.E5.8C.BA)
    *   [4.6 标签式或层叠式的网络浏览器](#.E6.A0.87.E7.AD.BE.E5.BC.8F.E6.88.96.E5.B1.82.E5.8F.A0.E5.BC.8F.E7.9A.84.E7.BD.91.E7.BB.9C.E6.B5.8F.E8.A7.88.E5.99.A8)
    *   [4.7 虚拟终端](#.E8.99.9A.E6.8B.9F.E7.BB.88.E7.AB.AF)
    *   [4.8 便笺本](#.E4.BE.BF.E7.AC.BA.E6.9C.AC)
    *   [4.9 主题与配色方案](#.E4.B8.BB.E9.A2.98.E4.B8.8E.E9.85.8D.E8.89.B2.E6.96.B9.E6.A1.88)
    *   [4.10 关机，重启和锁屏](#.E5.85.B3.E6.9C.BA.EF.BC.8C.E9.87.8D.E5.90.AF.E5.92.8C.E9.94.81.E5.B1.8F)
    *   [4.11 屏幕保护器及电源管理](#.E5.B1.8F.E5.B9.95.E4.BF.9D.E6.8A.A4.E5.99.A8.E5.8F.8A.E7.94.B5.E6.BA.90.E7.AE.A1.E7.90.86)
*   [5 疑难排除](#.E7.96.91.E9.9A.BE.E6.8E.92.E9.99.A4)
    *   [5.1 鼠标指针总处于忙碌状态](#.E9.BC.A0.E6.A0.87.E6.8C.87.E9.92.88.E6.80.BB.E5.A4.84.E4.BA.8E.E5.BF.99.E7.A2.8C.E7.8A.B6.E6.80.81)
*   [6 参见](#.E5.8F.82.E8.A7.81)

## 安装

请通过 [官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库") 安装 [i3](https://www.archlinux.org/groups/x86_64/i3/) [软件包](/index.php/Pacman#Installing_package_groups "Pacman")，其中包含了 [i3lock](https://www.archlinux.org/packages/?name=i3lock), [i3status](https://www.archlinux.org/packages/?name=i3status) 和 [i3-wm](https://www.archlinux.org/packages/?name=i3-wm) 程序包。`i3-wm` 是一套独立的桌面管理器，`i3status` 则是用于通过 [stdout](https://en.wikipedia.org/wiki/Standard_streams#Standard_output_.28stdout.29 "wikipedia:Standard streams") 向 i3bar 写入一条状态行，`i3lock` 则专于锁屏。

[Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") 中还提供了不少附加程序包。[i3-git](https://aur.archlinux.org/packages/i3-git/) 面向开发者。

[i3-gnome](https://aur.archlinux.org/packages/i3-gnome/) 则可安装 [GNOME](/index.php/GNOME "GNOME") 以及以 [i3](https://www.archlinux.org/groups/x86_64/i3/) 作为窗口管理器的Ｘ会话。

## 通过 xinitrc 运行 i3

请编辑`~/.xinitrc`，首先添加：

```
exec i3

```

现在您可以直接在 tty 上执行 `startx` 启动 i3 了。

如果您想记录 i3 所有的输出日志，可以往 `~/.xinitrc` 中添加以下行，在排错时会很有用：

```
exec i3 -V >> ~/.i3/i3log 2>&1

```

如果您在用 Nvidia 闭源驱动 **<302.17**，您得在 `~/.xinitrc` 中添加 `--force-xinerama` 标志。[i3wm.org](http://i3wm.org/docs/multi-monitor.html) 上对此作出了详细的解释。

```
exec i3 --force-xinerama

```

如果您在键盘映射上遇到了麻烦，请用 [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev), 或是阅读 [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys").

```
$ xev | grep -A2 --line-buffered '^KeyRelease' | sed -n '/keycode /s/^.*keycode \([0-9]*\).* (.*, \(.*\)).*$/\1 \2/p'

```

## 使用

在此章节下，请在 [official documentation](http://i3wm.org/docs) 索取更多细节 [i3 User’s Guide](http://i3wm.org/docs/userguide.html).

在 i3 里，一切命令均以「修饰键」开头，即 `$mod`. 默认上来说是 Alt 键 (Mod1),但开始键 (Mod4) 也更为广泛接受。

### 默认键绑定

(谢谢 Funtoo Linux 团队作出了这么出色的维基 [http://www.funtoo.org/I3_Tiling_Window_Manager](http://www.funtoo.org/I3_Tiling_Window_Manager))

| Key | Command |
| $mod + Enter | 启动虚拟终端 |
| $mod + A | 焦点转义到父窗口上 |
| $mod + S | 堆叠布局 |
| $mod + W | 标签布局 |
| $mod + E | 默认布局 |
| $mod + SpaceBar | 焦点在平铺式／浮动式转换 |
| $mod + D | 启动 dmenu |
| $mod + H | 水平分割窗口 |
| $mod + V | 垂直分割窗口 |
| $mod + J | 焦点往左窗口移 |
| $mod + K | 焦点往下窗口移 |
| $mod + L | 焦点往上窗口移 |
| $mod + ; | 焦点往右窗口移 |
| $mod + Shift + Q | 杀死当前窗口的进程 |
| $mod + Shift + E | 退出 i3 |
| $mod + Shift + C | 当场重新加载 i3config, 无需重启 |
| $mod + Shift + R | 重启 i3 （还重新加载了 i3config, 又没有退出过程） |
| $mod + Shift + J | 窗口左移 |
| $mod + Shift + K | 窗口下移 |
| $mod + Shift + L | 窗口上移 |
| $mod + Shift + : | 窗口右移 |
| $mod + Shift + SpaceBar | 窗口在平铺式／浮动式转换 |

### 程序启动器

i3 目前用 [dmenu](/index.php/Dmenu "Dmenu") 作为首席程序启动器，键绑定默认为 `$Mod+d`.

默认上， i3-dmenu-desktop 被用来当 dmenu 的包装器。前者通过现成的所有程序 .desktop 文件，生成名单。 不过有 [j4-dmenu-desktop-git](https://aur.archlinux.org/packages/j4-dmenu-desktop-git/) 重写了此包装器，但更快得许多，将来有望取代 i3-dmenu-desktop.

## 设置

### 状态栏

在 i3 的版本 v4.0 中，原本内置的状态栏 i3-wsbar 已被抛弃，改换为 i3bar.

#### 新方案：i3bar

不像需要额外安装 dzen2 的 i3-wsbar, i3bar 除了 [i3-wm](https://www.archlinux.org/packages/?name=i3-wm) 之外就没有其他依赖。它还可以接收由 [conky](/index.php/Conky "Conky") 或 i3status 输出的信息。示例（版本为4.1）：

 `~/.i3/config` 
```
bar {
    output            LVDS1
    status_command    i3status
    position          top
    mode              hide
    workspace_buttons yes
    tray_output       none

    font -misc-fixed-medium-r-normal--13-120-75-75-C-70-iso10646-1

    colors {
        background #000000
        statusline #ffffff

        focused_workspace  #ffffff #285577
        active_workspace   #ffffff #333333
        inactive_workspace #888888 #222222
        urgent_workspace   #ffffff #900000
    }
}

```

更多细节，请在官方用户指南查询 [Configuring i3bar](http://i3wm.org/docs/userguide.html#_configuring_i3bar) 条目。

#### 更多可选方案

*   [i3blocks](https://github.com/vivien/i3blocks) - Define the status line blocks with shell commands. It handles clicks, signals and different time intervals, in respect to the [i3bar protocol](http://i3wm.org/docs/i3bar-protocol.html). (AUR: [i3blocks](https://aur.archlinux.org/packages/i3blocks/))
*   [i3pystatus](https://github.com/enkore/i3pystatus) - i3status 可代替扩展，有更多的模块以及更灵活的设置。且为多线程，可快速锁屏。(AUR: [i3pystatus-git](https://aur.archlinux.org/packages/i3pystatus-git/))
*   [i3situation](https://github.com/HarveyHunt/i3situation) - 一个完全用 Python 3 编写而成的替代方案，集成众多插件从而有丰富功能。
*   [py3status](https://github.com/ultrabug/py3status) – 用 Python 编写成的 i3status 扩展
*   [conky](/index.php/Conky "Conky") – 经常被用来配合 [dzen](/index.php/Dzen "Dzen"), 以造出高度可定制的状态栏。
*   [j4status](http://j4status.j4tools.org/) - j4status 提供了用了很多若干插件的状态栏，以返回来自您计算机的信息。j4status 从属 [j4tools](http://www.j4tools.org/), 后者是配合 i3 使用的工具。
*   [h2status](/index.php/H2status "H2status") - trivial bash wrapper to i3status that nevertheless allows to conveniently write custom json entries, handle click events and asynchronously update the status bar.

#### 面板可选方案

也许有不少用户更偏好 [Desktop Environments](/index.php/Desktop_environment "Desktop environment") 所提供的面板方案。这可以在 i3 里通过启动特定的面板程序而实现。

至于 [XFCE panel](/index.php/Xfce#Panel "Xfce"), 直接添加以下进 `~/.i3/config` 即可：

```
exec --no-startup-id xfce4-panel

```

**注意:** 面板上，有些针对 [Desktop environment](/index.php/Desktop_environment "Desktop environment") 而产生的特殊功能（比如，管理工作区的窗口部件）不会正常工作，尽管不会对 i3 本身造成任何影响。

想禁用 i3bar, 直接在 `~/.i3/config` 注释掉 `bar{ }` 即可。

#### Iconic fonts in the status bar

i3bar 有个补丁负责实现对图标的支持，不过我们也可以在状态栏上直接用图像字符。AUR 上的图像字符有如下：

*   [ttf-font-awesome](https://aur.archlinux.org/packages/ttf-font-awesome/) 上的表格列出了图形字符以及对应的 Unicode 编码 [[1]](http://fortawesome.github.io/Font-Awesome/cheatsheet/).
*   [ttf-font-icons](https://aur.archlinux.org/packages/ttf-font-icons/) 也提供了全面的图像字符，包括彼此毫无重叠的 Awesome 和 Ionicons, 甚至也很好地避免了 Awesome 与 DejaVu Sans 的微秒重叠。总之它提供了在您的状态栏上的极佳图像字符解决方案，且展示表格如下： [[2]](https://www.dropbox.com/s/9iysh2i0gadi4ic/icons.pdf).

接着您可以在 `~/.i3/config` 上这样地调用它们，即追加一种字体属性的后缀:

```
bar {
  ...
  font pango:DejaVu Sans Mono, **Icons** 8
  ...
}

```

注意，您首先要用逗号分割字体与 Icons, 并在尾部加上字体大小。不用对每个字体都一一定义大小，哪怕字体大小全一样，也别指望用多字体也能有同样效果。总之正确的语法就应该像上面那样子。

最后，您终于可以在 `~/.i3status.conf` 上输进您想要的图像字符了。方法是找出所期望图像字符对应的 Unicode 编码。比如您在 Vim 里，就可以输入 <C-v>uXXXX, XXXX 就是图像字符的 Unicode 十六进制编码了。

### 在窗口之间快速跳转

*   [quickswitch-for-i3](https://github.com/proxypoke/quickswitch-for-i3) – 一把可在 i3 的窗口之间快速跳转，定位的 Python 实现。
*   [i3-wm-scripts](https://github.com/yiuin/i3-wm-scripts) – 用正则表达式在窗口之间进行搜索并跳转
*   [winmenupy](https://github.com/ziberna/i3-py/tree/master/examples#winmenupy) 启动 dmenu 时就会依次列出工作空间上的一系列客户端，选定其中一个并跳转即可

### i3status

首先我们得把默认设置文件复制到 home 目录，以好工作：

```
$ cp /etc/i3status.conf ~/.i3status.conf

```

**小贴士:** 示范配置文件中用 `eth0` 和 `wlan0` 作为接口名，如果与您系统并不一致，请参考 [Network configuration#Device names](/index.php/Network_configuration#Device_names "Network configuration")
。

#### 添加温度状态

如果您想在往 i3status 添加您的 CPU 温度状态，在 `~/,i3status.confg` 添加以下几句：

 `~/.i3status.conf` 
```
order += "cpu_temperature 0"
cpu_temperature 0 {
        format = "T: %degrees °C"
    max_threshold = 65
        path = "/sys/devices/platform/coretemp.0/temp1_input"
}
```

如果温度报告它无法读取温度数值，那修改一句：

```
path = "/sys/class/thermal/thermal_zone0/temp"

```

### 修改工作区的名称

**注意:** 工作区即 workspace

虽说不是必须的，但很多人期望能给常用工作区起名。首先您需要确定您期望哪些工作区固定在哪些显示器。在虚拟终端执行 `xrandr` 下，它告诉您当前您有哪些现成的显示器。一般来说，会有代表笔记本的 LVDS1, 或是 VGA1, HDMI1, HDMI2 等等，即外接显示器。如果您在用 [Xinerama](/index.php/Multihead#Xinerama "Multihead"), 那显示器名称要改用 xinerama-0, xinerama-1 等等。在 `~/.i3/config` 上添加您设想的工作区名称，您就也得在「移动所在窗口到任意工作区的命令」上加以修改。

```
# Workspace names
workspace "1:Web" output LVDS1
workspace "2:Mail" output LVDS1
workspace "3:Irc" output LVDS1
workspace "4:Shell" output LVDS1

```

```
# switch to workspace
bindsym $mod+1 workspace 1:Web
bindsym $mod+2 workspace 2:Mail
bindsym $mod+3 workspace 3:Irc
bindsym $mod+4 workspace 4:Shell

```

```
# move focused container to workspace
bindsym $mod+Shift+1 move container to workspace 1:Web
bindsym $mod+Shift+2 move container to workspace 2:Mail
bindsym $mod+Shift+3 move container to workspace 3:Irc
bindsym $mod+Shift+4 move container to workspace 4:Shell

```

### 让程序启动时，只出现在指定工作区

为了效率，您可以规定某些程序在启动时，自动出现在指定的工作区里。有两种途径：您可以用 `assign` 命令，那当手动启动某程序时，它直接被导向您指定的工作区。例如：

```
# 把 URxvt 导向 workspace 2
assign [class="URxvt"] 2

```

或者，如果您有修改了工作区名称，那您就要用新工作区名，而不是原来的数字：

```
# 把 URxvt 导向 workspace 4:Shell
assign [class="URxvt"] 4:Shell

```

**注意:** 为了确定一个窗口的 class, title, instance 等等，您可以用该工具 `xprop`, 通过安装 [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) 可得。

再次，您还可以通过 `i3-msg` 在工作区之间跳转，间隔地自动执行常用程序：

```
exec --no-startup-id i3-msg 'workspace 1:Web; exec /usr/bin/firefox' 
exec --no-startup-id i3-msg 'workspace 2:Mail; exec urxvt -name Mail -e /usr/bin/mutt'
exec --no-startup-id i3-msg 'workspace 3:Irc; exec /usr/bin/urxvt -name irssi -e /usr/bin/irssi'
exec --no-startup-id i3-msg 'workspace 4:Shell; exec /usr/bin/urxvt'

```

### 标签式或层叠式的网络浏览器

有些网络浏览器并没有实现 Tab, 因为原则上对 Tabs 的管理是由窗口管理器负责，而不是浏览器。

为了让 i3 管理您的无 Tab 网络浏览器，以 [uzbl](/index.php/Uzbl "Uzbl") 为例，在 `~/.i3/config` 添加以下：

```
for_window [class="Uzbl-core"] focus child, layout stacking, focus

```

这是层叠式浏览，即所有窗口为垂直地显示。好处是任何 Tab 的标题都可见，哪怕开了很多浏览器窗口。

如果您更偏好标签式浏览，即窗口在水平方向上显示，用：

```
for_window [class="Uzbl-core"] focus child, layout tabbed, focus

```

### 虚拟终端

默认来说，当您按 `$mod+Return`, 便会启动 `i3-sensible-terminal`, 即执行虚拟终端的脚本。它会试图按以下顺序一一执行，直到成功启动某虚拟终端：

*   `$TERMINAL`
*   [urxvt](/index.php/Urxvt "Urxvt")
*   [rxvt](https://www.archlinux.org/packages/?name=rxvt)
*   [terminator](/index.php/Terminator "Terminator")
*   [Eterm](https://aur.archlinux.org/packages/Eterm/)
*   [aterm](https://aur.archlinux.org/packages/aterm/)
*   [xterm](/index.php/Xterm "Xterm")
*   [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)
*   [roxterm](https://www.archlinux.org/packages/?name=roxterm)
*   [xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal)

您可以直接通过以下句的修改，以指定特定虚拟终端

```
bindsym $mod+Return exec i3-sensible-terminal

```

### 便笺本

能有个便笺本以快速呼出并粘贴是多么派得上用场啊！i3 让您能够把窗口送往「便笺本工作区」。它基本上一直被隐藏起来，直到您通过 `scratchpad show` 命令呼出它。要把当前窗口送往便笺本工作区，用 `$mod+Shift+minus`，或是通过`$mod+minus` 呼出它。往 `~/.i3/config` 添加以下几句：

```
# 把当前窗口设为便笺本
bindsym $mod+Shift+minus move scratchpad

# 呼出第一个便笺本
bindsym $mod+minus scratchpad show

```

您可以选个喜爱的编辑器进启动程序列表，并自动送往便笺本巩固走去，好随时快速呼出。以下例子示范了如果在 `~/.i3/config` 添加以下，您则可以启动 urxvt 虚拟终端，附带着 nano 编辑器，以及自动送往便笺本：

```
# 自动启动被特定了名称的虚拟终端，
exec --no-startup-id urxvt -name scratchpad -e /usr/bin/nano
# 当激活时，送往便笺本
for_window [class="URxvt" instance="scratchpad"] move scratchpad

```

### 主题与配色方案

配置文件允许定制窗口颜色，但严重依赖具体的语法，使得用户不方便创造或分享主题。不过好在已有旨在简化这方面的现成项目，提供了众多用户分享的主题，可应用于您的配置上。T

*   [i3-style](https://github.com/acrisci/i3-style) 通过 JSON 对象来修改您的主题，该格式为折腾配色方案而诞生。 [nodejs-i3-style](https://aur.archlinux.org/packages/nodejs-i3-style/)
*   [j4-make-config](https://github.com/okraits/j4-make-config) 在您原本的配置基础上，追加某种用户所分享，或由您定制的主题，以便灵活地调整配置。 [j4-make-config-git](https://aur.archlinux.org/packages/j4-make-config-git/).

### 关机，重启和锁屏

虽说并没有现成的关机，重启或锁屏按钮，但我们可以添加热键以实现。首先我们需要创建脚本，并储存为 `i3exit`。别忘了用 `chmod +x` 命令把它设为可执行文件并放进 `$PATH`。该脚本假设您安装了 [polkit](https://www.archlinux.org/packages/?name=polkit) 包，后者允许普通用户执行 [power management](/index.php/Systemd#Power_management "Systemd") 命令。

```
#!/bin/sh
lock() {
    i3lock
}

case "$1" in
    lock)
        lock
        ;;
    logout)
        i3-msg exit
        ;;
    suspend)
        lock && systemctl suspend
        ;;
    hibernate)
        lock && systemctl hibernate
        ;;
    reboot)
        systemctl reboot
        ;;
    shutdown)
        systemctl poweroff
        ;;
    *)
        echo "Usage: $0 {lock|logout|suspend|hibernate|reboot|shutdown}"
        exit 2
esac

exit 0

```

在 `~/.i3/config` 中添加以下：

```
set $mode_system System (l) lock, (e) logout, (s) suspend, (h) hibernate, (r) reboot, (Shift+s) shutdown
mode "$mode_system" {
    bindsym l exec --no-startup-id i3exit lock, mode "default"
    bindsym e exec --no-startup-id i3exit logout, mode "default"
    bindsym s exec --no-startup-id i3exit suspend, mode "default"
    bindsym h exec --no-startup-id i3exit hibernate, mode "default"
    bindsym r exec --no-startup-id i3exit reboot, mode "default"
    bindsym Shift+s exec --no-startup-id i3exit shutdown, mode "default"  

    # back to normal: Enter or Escape
    bindsym Return mode "default"
    bindsym Escape mode "default"
}
bindsym $mod+Pause mode "$mode_system"

```

有些对 i3lock 的替代方案，特别地有「模糊效果」：

*   [i3lock-wrapper](https://github.com/ashinkarov/i3-extras) from i3-extras repo (AUR: [i3lock-wrapper](https://aur.archlinux.org/packages/i3lock-wrapper/))
*   [i3lock-blur](https://aur.archlinux.org/packages/i3lock-blur/)

### 屏幕保护器及电源管理

您可以用 [DPMS](/index.php/DPMS "DPMS") 实现黑屏，或是睡眠／关掉您的显示器。在 `~/.i3/config` 添加以下，效果是显示器闲置十分钟后就会自动睡眠。

```
exec --no-startup-id xset dpms 600

```

用 [xss-lock](https://aur.archlinux.org/packages/xss-lock/) 可以对您的 i3 session 加以定义锁屏器。xss-lock 会追踪系统事件并作出应有的反应： `suspend`, `hibernate`, `lock-session`, and `unlock-session` 比如锁屏并等待，直到用户解除锁屏或是杀死锁屏器的进程。它也能对 [X screensaver](/index.php/Display_Power_Management_Signaling#xset_screen-saver_control "Display Power Management Signaling") 作出响应，即根据来自Ｘ服务器的信号，运行或是杀死锁屏器。以下能把 xss-lock 加进开机自启动程序：

```
xss-lock -- i3lock -i *background_image* &

```

## 疑难排除

### 鼠标指针总处于忙碌状态

当启动了某些并不支持启动提醒的某脚本或程序时，鼠标指针会逗留在忙碌状态六十秒以上。

为排除此现象，凡是 `exec` 命令都均加 `--no-startup-id` 后缀，比如：

```
exec --no-startup-id ~/script
bindsym $mod+d exec --no-startup-id dmenu_run

```

## 参见

*   [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers")
*   [Official website](http://i3wm.org)
*   [Source code](http://code.stapelberg.de/git/i3)
*   [Suspend/resume service files](/index.php/Systemd#Suspend.2Fresume_service_files "Systemd")
*   [Collection of scripts and patches](https://github.com/ashinkarov/i3-extras)
*   [Deepin Wiki 上的 i3 中文条目](http://wiki.linuxdeepin.com/index.php?title=I3)
*   [好用的 titling wm——i3wm](https://forum.suse.org.cn/viewtopic.php?f=23&t=262)

**Arch Linux Forums**

*   [*The i3 thread*](https://bbs.archlinux.org/viewtopic.php?id=99064) - A general discussion about i3
*   [*i3 desktop screenshots and config sharing*](https://bbs.archlinux.org/viewtopic.php?pid=1229978)