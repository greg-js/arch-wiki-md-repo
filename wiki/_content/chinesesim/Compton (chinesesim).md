**翻译状态：** 本文是英文页面 [Compton](/index.php/Compton "Compton") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-10-04，点击[这里](https://wiki.archlinux.org/index.php?title=Compton&diff=0&oldid=487244)可以查看翻译后英文页面的改动。

Compton 是一个独立的合成管理器，可以给不带合成功能的窗口管理器（例如 [i3](/index.php/I3_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "I3 (简体中文)")）带来淡入淡出、半透明、阴影等视觉效果。Compton 是 [xcompmgr-dana](http://oliwer.net/xcompmgr-dana/) 的分支，而后者又是 [xcompmgr](/index.php/Xcompmgr "Xcompmgr") 的分支。欲了解更多，可查看 [GitHub 上的 compton 项目](https://github.com/chjj/compton)。

## Contents

*   [1 安装](#安装)
*   [2 使用](#使用)
    *   [2.1 开机时自动启动 Compton](#开机时自动启动_Compton)
    *   [2.2 手动运行](#手动运行)
    *   [2.3 配置文件](#配置文件)
        *   [2.3.1 专为某些窗口禁用阴影效果](#专为某些窗口禁用阴影效果)
*   [3 多显示器](#多显示器)
*   [4 故障排除](#故障排除)
    *   [4.1 标签页式窗口](#标签页式窗口)
    *   [4.2 slock](#slock)
    *   [4.3 dwm 与 dmenu](#dwm_与_dmenu)
    *   [4.4 用 xsetroot 无法设置桌面背景颜色](#用_xsetroot_无法设置桌面背景颜色)
    *   [4.5 Intel 显卡渲染出错](#Intel_显卡渲染出错)
    *   [4.6 使用 AMD Catalyst 驱动时出现的花屏 / 截屏问题](#使用_AMD_Catalyst_驱动时出现的花屏_/_截屏问题)
    *   [4.7 使用 NVidia 驱动时出现高 CPU 占用](#使用_NVidia_驱动时出现高_CPU_占用)
    *   [4.8 使用 NVidia 驱动时，进程后台化会报错](#使用_NVidia_驱动时，进程后台化会报错)
    *   [4.9 使用 Xft 字体会导致卡顿](#使用_Xft_字体会导致卡顿)
    *   [4.10 屏幕闪烁](#屏幕闪烁)
*   [5 延伸阅读](#延伸阅读)

## 安装

安装包 [compton](https://www.archlinux.org/packages/?name=compton) 。 如果要使用 [git](/index.php/Git "Git") 版本，可安装 [compton-git](https://aur.archlinux.org/packages/compton-git/)。

若想用 GUI 修改 compton 的配置，可安装 [compton-conf](https://aur.archlinux.org/packages/compton-conf/) 或 [compton-conf-git](https://aur.archlinux.org/packages/compton-conf-git/)。

## 使用

登录 X 会话后，用户可以随时手动启动 / 终止 compton。也可以将其设置为自动启动（例如从 [自动启动](/index.php/Xprofile_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xprofile (简体中文)")）。下面的选项可以帮你细化配置:

*   `-b`: 以后台进程（[Daemon](/index.php/Daemon "Daemon")）的形式运行
*   `-c`: 启用阴影效果
*   `-C`: 禁用面板和 Docks 的阴影效果
*   `-G`: 禁用应用程序窗口和拖放对象的阴影效果
*   `--config`: 使用指定的配置文件

除此之外 compton 还支持很多选项。包括动画时间，指定待管理的 X 显示，指定窗口的菜单、边框、失焦窗口菜单的不透明度等。详细信息请参阅 [Compton Man Page](https://github.com/chjj/compton/blob/master/man/compton.1.asciidoc)。

**注意:** 在启动 compton 之前，如果正在运行别的 [合成管理器](/index.php/Composite_manager "Composite manager")，需要先停用它。

### 开机时自动启动 Compton

不同的桌面环境 / 窗口管理器有着不同的方式来自动启动 compton。例如，Openbox 的自动启动项目在配置文件 `~/.config/openbox/autostart` 里管理。而 i3-wm 的用户需要去修改 `~/.config/i3/config` 文件。必要时，compton 也可以从 [xprofile](/index.php/Xprofile "Xprofile") 或 [Xinitrc](/index.php/Xinitrc "Xinitrc") 自动启动。有关更多信息，请参阅 [startup files](/index.php/Startup_files "Startup files") 一文。

### 手动运行

于终端运行:

```
compton

```

可以手动启动 compton 进程。

若要禁用所有的阴影特效，需要加上 `-C` 和 `-G` 这两个参数:

```
compton -CG

```

若要在登录 X 会话的过程中，以后台进程（[Daemon](/index.php/Daemon "Daemon")）的形式自动运行 compton，必须加上 `-b` 参数：

```
compton -b

```

将前面的参数一起用，效果也就一起有了:

```
compton -CGb

```

最后这个例子演示了如何使用需要指定数值的参数:

```
compton -cCGfF -o 0.38 -O 200 -I 200 -t 0 -l 0 -r 3 -D2 -m 0.88

```

### 配置文件

默认的配置文件放在 `/etc/xdg/compton.conf`。若要修改配置，需要先把默认配置拷贝一份到 `~/.config/compton.conf`。再运行 compton 时就会从这里读取配置。

若要在运行时手动指定配置文件，可以用 `--config` 参数：

```
compton --config *path/to/compton.conf*

```

#### 专为某些窗口禁用阴影效果

Compton 绘制阴影的方法可能会使某些软件的窗口的外观出现异常。用 `shadow-exclude` 配置选项即可为这些软件禁用阴影。

例如：若要让 compton 不给 GTK +3 窗口绘制阴影，可以在 `compton.conf` 文件的 `shadow-exclude` 部分里加入:

```
"_GTK_FRAME_EXTENTS@:c"

```

若要让 [conky](/index.php/Conky "Conky") 窗口不绘制 compton 阴影，首先修改 conky 的配置文件 `~/.conkyrc`:

```
own_window_class conky

```

然后如下修改 compton.conf:

```
shadow-exclude = "class_g = 'conky'";

```

在[这里](https://projects.archlinux.org/svntogit/community.git/tree/trunk/compton.conf?h=packages/compton#n80)可以看到完整的默认禁用阴影的窗口名单。

## 多显示器

如果你在用 [多个显示器](/index.php/Multihead "Multihead") 但没有使用 xinerama，那么 X server 会自动以多个 screen 的模式运行，然而 compton 默认只会接管一个 screen 的合成。解决办法是启动多个 compton 进程，并以 `-d` 参数来逐个指定要负责的 screen。下面这个范例命令是给四个 screen 用的：

```
seq 0 3 | xargs -l1 -I@ compton -b -d :0.@

```

## 故障排除

如若配置不当，合成特效可能会使某些软件产生外观异常。

### 标签页式窗口

某些自带标签页功能的软件，当它们的窗口被设置成半透明时，可能会因为顶层标签窗口是半透明的而露出底层标签窗口的内容。而且由于每个标签窗口都要绘制阴影，整体看上去就会出现浓重的多重阴影。

这类多重阴影的问题可以通过向配置文件中的 `shadow-exclude` 添加规则来解决：

```
"_NET_WM_STATE@:32a *= '_NET_WM_STATE_HIDDEN'"

```

加入下面的配置可以避免看到底层的标签窗口内容：

```
opacity-rule = [
  "95:class_g = 'URxvt' && !_NET_WM_STATE@:32a",
  "0:_NET_WM_STATE@:32a *= '_NET_WM_STATE_HIDDEN'"
];

```

这里 URxvt 指代的是你在用的终端模拟器的 X 窗口 class 属性。如果你要为别的终端指定渲染规则，可以自行相应改动。

### slock

如果通过 compton 的 `-i` 选项启用了失焦窗口的透明度，再配合使用 [slock](/index.php/Slock "Slock")，就可能出现你不想看到的结果。把透明度改成 `0.2` 可以解决这一问题。如果用命令行参数来指定的话：

```
$ compton <any other arguments> -i 0.2

```

也可以在配置文件里写这一行：

```
inactive-dim = 0.2;

```

还有一个办法是，让 compton 认为 slock 的窗口一直是获得了焦点的。可以通过其窗口 id 来识别 slock 窗口，也可以用“没有名字的窗口”来判断。

**注意:** 某些软件每次启动后窗口 id 都会不一样，但 slock 的窗口 id 似乎是固定不变的。这里我们需要有懂得相关知识的人来提供确认，否则只能是各位用户后果自负。

下面的命令可以让 compton 忽略所有 name 属性为空的窗口的焦点获取状态：

```
$ compton <原有的参数> --focus-exclude "! name~=*"*

```

用这个命令找到 slock 的窗口 id：

```
$ xwininfo & slock

```

在 slock 退出之前，尽快在屏幕上任意位置单击鼠标，然后输入你的用户密码来解锁。这样你就能看到输出的窗口 ID：

```
xwininfo: Window id: 0x1800001 (has no name)

```

把这个窗口 ID 拿给 compton，让它忽略这个窗口的焦点获取状态：

```
$ compton <原有的参数> --focus-exclude 'id = 0x1800001'

```

或者把这一行写进配置文件：

```
focus-exclude = "id = 0x1800001";

```

### dwm 与 dmenu

虽然有时我们希望 compton 不要为 dwm 状态栏渲染窗口失焦特效，但 dwm 状态栏没法轻易地被 compton 的规则匹配到。而且 dwm 状态栏和 dmenu 都没有静态的 window id。要实现这一效果，你只能尝试给这两个项目打补丁，给这些窗口加上 class 属性用于规则匹配。或者采用宽泛的规则去匹配。

下面这个方法适用于 dmenu 和 dwm 状态栏总是出现在屏幕顶端（从左上角顶点起绘制）的情况：

```
$ compton <别的参数> --focus-exclude "x = 0 && y = 0 && override_redirect = true"

```

如果要写进配置文件的话，要这么写：

```
focus-exclude = "x = 0 && y = 0 && override_redirect = true";

```

`override_redirect` 这个属性在绝大多数窗口上的值似乎都是 `false`。在匹配规则里写 `override_redirect = true` 可以避免这条规则误伤到位置一样的应用程序窗口。

### 用 xsetroot 无法设置桌面背景颜色

目前 compton 与 `xsetroot` 的 `-solid` 功能还无法兼容。不过你可以试试用 [hsetroot](https://www.archlinux.org/packages/?name=hsetroot) 这个替代方案：

```
$ hsetroot -solid '#000000'

```

在 [https://github.com/chjj/compton/issues/162](https://github.com/chjj/compton/issues/162) 可以了解到这一问题背后的具体细节。

### Intel 显卡渲染出错

已知某些 Intel 芯片在启用 DRI3 后，如果调节分辨率或者接入新显示器，compton 的渲染就会产生[问题](https://bugs.freedesktop.org/show_bug.cgi?id=97916)。`intel` 与 `modesetting` 两种驱动都受到这一问题的影响。[禁用 DRI3](/index.php/Intel_graphics#DRI3_issues "Intel graphics") 可以绕过这一问题。

### 使用 AMD Catalyst 驱动时出现的花屏 / 截屏问题

尝试在 compton 启动时加上参数

```
--backend xrender

```

或者把下面这一行写入 compton.conf 配置文件

```
backend = "xrender";

```

在 [https://github.com/chjj/compton/issues/208](https://github.com/chjj/compton/issues/208) 可以了解到更多细节。

### 使用 NVidia 驱动时出现高 CPU 占用

如果在使用参数 `--backend glx` 时发现 CPU 占用很高，或者使用 `--vsync` 时出现画面撕裂，应按照 [NVIDIA](/index.php/NVIDIA "NVIDIA") 的指示安装上 [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils)。

### 使用 NVidia 驱动时，进程后台化会报错

如果以后台进程启动 compton 时出现错误信息：`main(): Failed to create new session.`，可以装这个版本试试：[compton-garnetius-git](https://aur.archlinux.org/packages/compton-garnetius-git/)。这个版本还包含了若干个上游未能合入的补丁。

### 使用 Xft 字体会导致卡顿

如果使用了 Xft 字体会导致 [xterm](/index.php/Xterm "Xterm") 和 [urxvt](/index.php/Urxvt "Urxvt") 之类的软件严重卡顿，尝试给 compton 加上如下参数：

```
--xrender-sync --xrender-sync-fence

```

或者改用 xrender 渲染方式。

在 [https://github.com/chjj/compton/issues/152](https://github.com/chjj/compton/issues/152) 可以了解到更多细节。

### 屏幕闪烁

在无任何 panel 的桌面环境中将窗口最大化，可能会出现这一问题。解决办法是在配置文件中加入：

```
 unredir-if-possible = false;

```

在 [https://github.com/chjj/compton/issues/402](https://github.com/chjj/compton/issues/402) 可以了解到更多细节。

## 延伸阅读

*   [Howto: Using Compton for tear-free compositing on XFCE or LXDE](http://ubuntuforums.org/showthread.php?t=2144468&p=12644745#post12644745)