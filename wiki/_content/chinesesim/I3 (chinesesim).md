**翻译状态：** 本文是英文页面 [i3](/index.php/I3 "I3") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-05-11，点击[这里](https://wiki.archlinux.org/index.php?title=i3&diff=0&oldid=313232)可以查看翻译后英文页面的改动。

[i3](http://i3wm.org/) 是一套动态[平铺式窗口管理器](https://en.wikipedia.org/wiki/Tiling_window_manager "wikipedia:Tiling window manager")，灵感来自针对开发者与资深用户的 [wmii](/index.php/Wmii "Wmii")。

i3的既定目标包括清晰可读的文档，多显示器支持，多窗口的树形数据结构，和多种的模式，例如 [vim](/index.php/Vim "Vim") 模式。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 显示管理器](#.E6.98.BE.E7.A4.BA.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [1.2 xinitrc](#xinitrc)
*   [2 使用](#.E4.BD.BF.E7.94.A8)
*   [3 键盘映射](#.E9.94.AE.E7.9B.98.E6.98.A0.E5.B0.84)
    *   [3.1 容器](#.E5.AE.B9.E5.99.A8)
    *   [3.2 程序启动器](#.E7.A8.8B.E5.BA.8F.E5.90.AF.E5.8A.A8.E5.99.A8)
*   [4 设置](#.E8.AE.BE.E7.BD.AE)
    *   [4.1 配置助手和可选键盘布局](#.E9.85.8D.E7.BD.AE.E5.8A.A9.E6.89.8B.E5.92.8C.E5.8F.AF.E9.80.89.E9.94.AE.E7.9B.98.E5.B8.83.E5.B1.80)
    *   [4.2 颜色主题](#.E9.A2.9C.E8.89.B2.E4.B8.BB.E9.A2.98)
    *   [4.3 i3bar](#i3bar)
    *   [4.4 i3bar可选方案](#i3bar.E5.8F.AF.E9.80.89.E6.96.B9.E6.A1.88)
    *   [4.5 i3status](#i3status)
        *   [4.5.1 i3status可选方案](#i3status.E5.8F.AF.E9.80.89.E6.96.B9.E6.A1.88)
        *   [4.5.2 i3status 包装器](#i3status_.E5.8C.85.E8.A3.85.E5.99.A8)
        *   [4.5.3 状态栏中的图标字体](#.E7.8A.B6.E6.80.81.E6.A0.8F.E4.B8.AD.E7.9A.84.E5.9B.BE.E6.A0.87.E5.AD.97.E4.BD.93)
    *   [4.6 在窗口之间快速跳转](#.E5.9C.A8.E7.AA.97.E5.8F.A3.E4.B9.8B.E9.97.B4.E5.BF.AB.E9.80.9F.E8.B7.B3.E8.BD.AC)
    *   [4.7 i3status](#i3status_2)
        *   [4.7.1 添加温度状态](#.E6.B7.BB.E5.8A.A0.E6.B8.A9.E5.BA.A6.E7.8A.B6.E6.80.81)
    *   [4.8 修改工作区的名称](#.E4.BF.AE.E6.94.B9.E5.B7.A5.E4.BD.9C.E5.8C.BA.E7.9A.84.E5.90.8D.E7.A7.B0)
    *   [4.9 让程序启动时，只出现在指定工作区](#.E8.AE.A9.E7.A8.8B.E5.BA.8F.E5.90.AF.E5.8A.A8.E6.97.B6.EF.BC.8C.E5.8F.AA.E5.87.BA.E7.8E.B0.E5.9C.A8.E6.8C.87.E5.AE.9A.E5.B7.A5.E4.BD.9C.E5.8C.BA)
    *   [4.10 标签式或层叠式的网络浏览器](#.E6.A0.87.E7.AD.BE.E5.BC.8F.E6.88.96.E5.B1.82.E5.8F.A0.E5.BC.8F.E7.9A.84.E7.BD.91.E7.BB.9C.E6.B5.8F.E8.A7.88.E5.99.A8)
    *   [4.11 虚拟终端](#.E8.99.9A.E6.8B.9F.E7.BB.88.E7.AB.AF)
    *   [4.12 便笺本](#.E4.BE.BF.E7.AC.BA.E6.9C.AC)
    *   [4.13 主题与配色方案](#.E4.B8.BB.E9.A2.98.E4.B8.8E.E9.85.8D.E8.89.B2.E6.96.B9.E6.A1.88)
    *   [4.14 关机，重启和锁屏](#.E5.85.B3.E6.9C.BA.EF.BC.8C.E9.87.8D.E5.90.AF.E5.92.8C.E9.94.81.E5.B1.8F)
    *   [4.15 屏幕保护器及电源管理](#.E5.B1.8F.E5.B9.95.E4.BF.9D.E6.8A.A4.E5.99.A8.E5.8F.8A.E7.94.B5.E6.BA.90.E7.AE.A1.E7.90.86)
    *   [4.16 网速显示](#.E7.BD.91.E9.80.9F.E6.98.BE.E7.A4.BA)
*   [5 疑难排除](#.E7.96.91.E9.9A.BE.E6.8E.92.E9.99.A4)
    *   [5.1 鼠标指针总处于忙碌状态](#.E9.BC.A0.E6.A0.87.E6.8C.87.E9.92.88.E6.80.BB.E5.A4.84.E4.BA.8E.E5.BF.99.E7.A2.8C.E7.8A.B6.E6.80.81)
*   [6 参见](#.E5.8F.82.E8.A7.81)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [i3](https://www.archlinux.org/groups/x86_64/i3/) [软件包](/index.php/Pacman#Installing_package_groups "Pacman")，其中包含了 [i3lock](https://www.archlinux.org/packages/?name=i3lock), [i3status](https://www.archlinux.org/packages/?name=i3status) 和 [i3-wm](https://www.archlinux.org/packages/?name=i3-wm) 程序包。`i3-wm` 是一套独立的桌面管理器，`i3status` 则是用于通过 [stdout](https://en.wikipedia.org/wiki/Standard_streams#Standard_output_.28stdout.29 "wikipedia:Standard streams") 向 i3bar 写入一条状态行，`i3lock` 则专于锁屏。

[Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") 中还提供了不少附加程序包。例子可参考[#补丁](#.E8.A1.A5.E4.B8.81)章节。

### 显示管理器

[i3-wm](https://www.archlinux.org/packages/?name=i3-wm) 软件包包括了作为[Xsession](/index.php/Xsession "Xsession")的`i3.desktop`,用于启动窗口管理器。 `i3-with-shmlog.desktop` 启用了日志（对于调试很有用）。[i3-gnome](https://aur.archlinux.org/packages/i3-gnome/) 软件包在 [GNOME](/index.php/GNOME "GNOME") 中集成了 `i3-wm`。

### xinitrc

编辑 [Xinitrc](/index.php/Xinitrc "Xinitrc") ，添加：

```
exec i3

```

如果您想记录 i3 所有的输日志，则添加：

```
exec i3 -V >> ~/i3log-$(date +'%F-%k-%M-%S') 2>&1

```

## 使用

可在 [official documentation](http://i3wm.org/docs) 获取更多细节 [i3 User’s Guide](http://i3wm.org/docs/userguide.html).

## 键盘映射

在 i3 里，一切命令均以「修饰键」开头，即 `$mod`. 默认上来说是 Alt 键 `alt`(Mod1),但开始键 `Super`(Mod4) 也更为广泛接受。Super 键往往带有 Windows 图标，在苹果键盘上则是 Command 键。

见 [i3 偏好](http://i3wm.org/docs/refcard.html) 和 [Using i3](http://i3wm.org/docs/userguide.html#_using_i3) 以获取默认映射表。见 [Keyboard 绑定](http://i3wm.org/docs/userguide.html#keybindings) 以获取添加新快捷键的说明。

非Qwerty键盘布局的用户可能会希望跳过 [以下](#.E9.85.8D.E7.BD.AE.E5.8A.A9.E6.89.8B.E5.92.8C.E5.8F.AF.E9.80.89.E9.94.AE.E7.9B.98.E5.B8.83.E5.B1.80)所说的“配置助手”。

### 容器

i3 以树形结构的方式管理窗口，容器是最小的单位。这种结构可以被水平或竖式分割。容器默认是平铺的，但可以设置为标签式或栈式布局，同样也可以设置为浮动式（适用于对话窗口）。浮动的窗口总是显示在顶部。

### 程序启动器

i3 使用 [dmenu](/index.php/Dmenu "Dmenu") 作为首席程序启动器，键绑定默认为 `$Mod+d`.

[i3-wm](https://www.archlinux.org/packages/?name=i3-wm) 包含了 i3-dmenu-desktop ——— 一个 "dmenu" 的[Perl](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl") 包装器，它通过现成的所有程序 .desktop 文件，生成名单。 不或者 [j4-dmenu-desktop-git](https://aur.archlinux.org/packages/j4-dmenu-desktop-git/) 软件包也是一个不错的选择。

## 设置

见 [Configuring i3](http://i3wm.org/docs/userguide.html#configuring) 以获取更多细节。此文章余下部分假设 i3 的配置文件位于 `~/.config` 目录。

### 配置助手和可选键盘布局

当 i3 首次启动时，它会启动配置助手 *i3-config-wizard*。此工具会通过重写位于 `/etc/i3/config.keycodes` 的模板配置文件来创建 `~/.config/i3/config`。他会对默认模板造成两次修改。

1.  它会询问用户以选择默认的修饰建。它会在模板文件中添加一行，类似于 `set $mod Mod1`; 然后
2.  它会用用户设置的键盘布局相应的 *bindsyn* 行替换所有 *bindcode* 行。

第二步是设计用于确保 Qwerty 键盘上的四个导航键 `j`， `k`， `l` 和 "分号" on a Qwerty keyboard会被映射在拥有相同位置的按键上，举例说，[Dvorak](/index.php/Dvorak "Dvorak") 键盘上的 `h`， `t`， `n`， `s`。这个小戏法的副作用是 最多十五个按键会被以一种破话位置记忆的方式被映射 - 所以，对于 Dvorak 用户， “重启”被绑定于 `$mod1+p` 而不是 `$mod1+r`，“竖直分割”被绑定于 `$mod1+d` 而不是 `$mod1+h`,类似的还有更多。

因此，其他键盘布局的用户若是想要直截了当的，符合教程中给出的按键绑定的键盘绑定，可能更倾向于不去使用 "config wizard" 。这可以拷贝 `/etc/i3/config` 到 `~/.config/i3/config` （或 `~/.i3/config`），然后编辑此文件。

注意，用户也可以建立一份以键码为基础的配置。例如，对于那些经常切换键盘布局，但是想要 i3 的键盘绑定保持相同的用户。

### 颜色主题

The configuration file allows for customization of window decoration colors, but the syntax makes it impractical to create or share themes. There are several projects which make this easier and include a variety of user-contributed themes.

*   **i3-style** — Modifies your config in place from a theme stored in a JSON object, designed for frequently tweaking or changing a colorscheme

	[https://github.com/acrisci/i3-style](https://github.com/acrisci/i3-style) || [nodejs-i3-style](https://aur.archlinux.org/packages/nodejs-i3-style/)

*   **j4-make-config** — Merge your config with a collection of themes or personal config parts, for example host-specific configuration, allowing quick changing of the theme and flexible, dynamic customization of the configuration

	[https://github.com/okraits/j4-make-config](https://github.com/okraits/j4-make-config) || [j4-make-config-git](https://aur.archlinux.org/packages/j4-make-config-git/)

### i3bar

除了显示工作区信息外，i3bar 也可以作为 i3status 的输入，或是替代品。下一章节会对此进行详细描述。示例：

 `~/.config/i3/config` 
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

更多细节，见[Configuring i3bar](http://i3wm.org/docs/userguide.html#_configuring_i3bar) 。

### i3bar可选方案

一些用户可能更偏好于类似于常规 [桌面环境](/index.php/Desktop_environment "Desktop environment") 提供的面板。这可以通过在 i3 启动时运行面板程序达成。

例如 [XFCE 面板](/index.php/Xfce#Panel "Xfce")，在 `~/.config/i3/config` 的任何处添加以为行：

```
exec --no-startup-id xfce4-panel --disable-wm-check

```

i3bar 可以通过注释掉 `~/.config/i3/config` 中的 `bar{ }` 段落禁用，或者定义一个按键以切换 i3bar 显示状态：

 `~/.config/i3/config` 
```
# bar toggle, hide or show 	
bindsym $mod+m bar mode toggle

```

### i3status

拷贝默认的配置文件到家目录：

```
$ cp /etc/i3status.conf ~/.config/i3status/config

```

不是所有的插件都被在默认配置文件中被定义，一些配置值对于系统也可能是无效的，所以需要相应的更新。具体见 `man i3status` 。

#### i3status可选方案

*   **[conky](/index.php/Conky "Conky")** — 高度可扩展系统监视器。配合 i3 的使用方法见 [this tutorial](http://i3wm.org/docs/user-contributed/conky-i3bar.html)

	[https://github.com/brndnmtthws/conky](https://github.com/brndnmtthws/conky) || [conky](https://www.archlinux.org/packages/?name=conky)

*   **[i3blocks](/index.php/I3blocks "I3blocks")** — 通过 shell 脚本扩展。 它可以处理点击事件，中断，和定义或更在块的基础上更新间隔。

	[https://github.com/vivien/i3blocks](https://github.com/vivien/i3blocks) || [i3blocks](https://aur.archlinux.org/packages/i3blocks/)

*   **i3pystatus** — 默认带有许多插件和选项的可扩展 Python 3 状态栏

	[https://github.com/enkore/i3pystatus](https://github.com/enkore/i3pystatus) i3pystatus || [i3pystatus-git](https://aur.archlinux.org/packages/i3pystatus-git/)

*   **i3situation** — 另一个 Python 3 状态栏生成器。

	[https://github.com/HarveyHunt/i3situation](https://github.com/HarveyHunt/i3situation) || [i3situation-git](https://aur.archlinux.org/packages/i3situation-git/)

*   **j4status** — 提供了状态栏，可以通过插件扩展，且是用 C 写成的。额外的插件由[j4status-plugins-git](https://aur.archlinux.org/packages/j4status-plugins-git/).

	[http://j4status.j4tools.org/](http://j4status.j4tools.org/) || [j4status-git](https://aur.archlinux.org/packages/j4status-git/)提供

*   **goi3bar** — Go 写的 i3status 替代品。配置文件同时还有各种插件，并发选项和丰富的插件支持。

	[https://github.com/denbeigh2000/goi3bar/](https://github.com/denbeigh2000/goi3bar/) || [goi3bar-git](https://aur.archlinux.org/packages/goi3bar-git/)

#### i3status 包装器

*   **i3cat** — A [go](/index.php/Go "Go") based wrapper which can concatenate inputs from multiple external sources. It can handle click events and forwarding user specified signals to its subprocesses.

	[http://vincent-petithory.github.io/i3cat/](http://vincent-petithory.github.io/i3cat/) || [i3cat-git](https://aur.archlinux.org/packages/i3cat-git/)

*   **py3status** — An extensible i3status wrapper written in Python.

	[https://github.com/ultrabug/py3status](https://github.com/ultrabug/py3status) || [py3status](https://aur.archlinux.org/packages/py3status/)

#### 状态栏中的图标字体

'i3bar' 有个[补丁](#.E8.A1.A5.E4.B8.81)负责实现对 XBM 图标的支持，不过我们也可以使用图标字体。

*   **ttf-font-awesome** — 可以通过 CSS定制的可缩放矩阵字体。[[1]](http://fortawesome.github.io/Font-Awesome/cheatsheet/)显示了每个图像的 Unicode 值。

	[http://fortawesome.github.io/Font-Awesome/](http://fortawesome.github.io/Font-Awesome/) || [ttf-font-awesome](https://aur.archlinux.org/packages/ttf-font-awesome/)

*   **ttf-font-icons** — 也提供了全面的图像字符，包括彼此毫无重叠的 Awesome 和 Ionicons, 也很好地避免了 Awesome 与 DejaVu Sans 的微秒重叠。

	[http://kageurufu.net/icons.pdf](http://kageurufu.net/icons.pdf) || [ttf-font-icons](https://aur.archlinux.org/packages/ttf-font-icons/).

要结合这些字体，在配置文件中一种字体属性的后缀用`,`分割字体。示例：

 `~/.config/i3/config` 
```
bar {
   ...
   font pango:DejaVu Sans Mono, **Icons** 8
   ...
 }
```

In accordance with [pango syntax](https://developer.gnome.org/pango/stable/pango-Fonts.html#pango-font-description-from-string), font size is specified only once, at the end of the comma-separated list of font families. Setting a size for each font would cause all but the last font to be ignored.

Add icons to the format strings in `~/.config/i3status/config` using the unicode numbers given in the cheatsheets linked above. The input method will vary between text editors. For instance, to insert the "heart" icon (unicode number f004):

*   in various gui text editors (e.g. [gedit](/index.php/Gedit "Gedit"), Leafpad) and terminals (e.g. GNOME Terminal, xfce4-terminal): `ctrl+shift+u`, `f004`, `Enter`
*   in [Emacs](/index.php/Emacs "Emacs"): `ctrl+x`, `8`, `Enter`, `f004`, `Enter`
*   in [Vim](/index.php/Vim "Vim") (while in insert mode): `Ctrl+v`, `uf004`
*   in [urxvt](/index.php/Urxvt "Urxvt"): while holding `Ctrl+Shift`, type `f004`

### 在窗口之间快速跳转

*   [quickswitch-for-i3](https://github.com/proxypoke/quickswitch-for-i3) – 一把可在 i3 的窗口之间快速跳转，定位的 Python 实现。
*   [i3-wm-scripts](https://github.com/yiuin/i3-wm-scripts) – 用正则表达式在窗口之间进行搜索并跳转
*   [winmenupy](https://github.com/ziberna/i3-py/tree/master/examples#winmenupy) 启动 dmenu 时就会依次列出工作空间上的一系列客户端，选定其中一个并跳转即可

### i3status

首先我们得把默认设置文件复制到 home 目录，以好工作：

```
$ cp /etc/i3status.conf ~/.i3status.conf

```

**提示：** 示范配置文件中用 `eth0` 和 `wlan0` 作为接口名，如果与您系统并不一致，请参考 [Network configuration#Device names](/index.php/Network_configuration#Device_names "Network configuration")
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
*   [rxvt](https://aur.archlinux.org/packages/rxvt/)
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

### 网速显示

可以参考此处的脚本文件[measure-net-speed.bash](https://github.com/glittershark/i3status/blob/master/contrib/measure-net-speed.bash)、[measure-net-speed-i3status.bash](https://github.com/glittershark/i3status/blob/master/contrib/measure-net-speed-i3status.bash)。

*   获得你的网络接口 (使用 `ip addr`)，如 `wlan0`
*   在 `/sys/devices` 找到网卡的名称:

 ` $ find /sys/devices -name *network_interface*` 例如 ` $ find /sys/devices -name wlan0` 
**Tip:** Use `/sys/class/net/*interface*/statistics/` to not depend on PCI location.

把修改后的脚本文件放置在适当的位置 (比如 `~/.config/i3`) 按照脚本中的建议设置你的[i3-wm](https://www.archlinux.org/packages/?name=i3-wm)和[i3status](https://www.archlinux.org/packages/?name=i3status)配置文件:

*   为脚本 `measure-net-speed-i3status.bash` 、 `measure-net-speed.bash` 添加可执行权限

*   修改 `measure-net-speed-i3status.bash` 中行`dat=$(measure-net-speed.bash)` 为 `dat=$(/path/to/measure-net-speed.bash)`

*   修改 `~/.i3/config` 中对应章节：

```
bar {
   status_command /path/to/measure-net-speed-i3status.bash
}

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