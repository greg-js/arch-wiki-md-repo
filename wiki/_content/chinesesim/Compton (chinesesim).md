Compton 是一个独立的合成管理器，可以给不带合成功能的窗口管理器（例如 [i3](/index.php/I3_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "I3 (简体中文)")）带来淡入淡出、半透明、阴影等视觉效果。Compton 是 [xcompmgr-dana](http://oliwer.net/xcompmgr-dana/) 的分支，而后者又是 [xcompmgr](/index.php/Xcompmgr "Xcompmgr") 的分支。欲了解更多，可查看 [GitHub 上的 compton 项目](https://github.com/chjj/compton)。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 使用](#.E4.BD.BF.E7.94.A8)
    *   [2.1 开机时自动启动 Compton](#.E5.BC.80.E6.9C.BA.E6.97.B6.E8.87.AA.E5.8A.A8.E5.90.AF.E5.8A.A8_Compton)
    *   [2.2 手动运行](#.E6.89.8B.E5.8A.A8.E8.BF.90.E8.A1.8C)
    *   [2.3 配置文件](#.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
        *   [2.3.1 专为某些窗口禁用阴影效果](#.E4.B8.93.E4.B8.BA.E6.9F.90.E4.BA.9B.E7.AA.97.E5.8F.A3.E7.A6.81.E7.94.A8.E9.98.B4.E5.BD.B1.E6.95.88.E6.9E.9C)
*   [3 多显示器](#.E5.A4.9A.E6.98.BE.E7.A4.BA.E5.99.A8)
*   [4 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [4.1 标签页式窗口](#.E6.A0.87.E7.AD.BE.E9.A1.B5.E5.BC.8F.E7.AA.97.E5.8F.A3)
    *   [4.2 slock](#slock)
    *   [4.3 dwm & dmenu](#dwm_.26_dmenu)
    *   [4.4 Unable to change the background color with xsetroot](#Unable_to_change_the_background_color_with_xsetroot)
    *   [4.5 Corrupted screen contents with Intel graphics](#Corrupted_screen_contents_with_Intel_graphics)
    *   [4.6 Screen artifacts/screenshot issues when using AMD's Catalyst driver](#Screen_artifacts.2Fscreenshot_issues_when_using_AMD.27s_Catalyst_driver)
    *   [4.7 High CPU use with nvidia drivers](#High_CPU_use_with_nvidia_drivers)
    *   [4.8 Errors while trying to daemonize with nvidia drivers](#Errors_while_trying_to_daemonize_with_nvidia_drivers)
    *   [4.9 Lag when using xft fonts](#Lag_when_using_xft_fonts)
*   [5 See also](#See_also)

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

### dwm & dmenu

dwm's statusbar is not detected by any of compton's functions to automatically exclude window manager elements. Neither dwm statusbar nor dmenu have a static window id. If you want to exclude it from inactive window transparency (or other), you'll have to either patch a window class into the source code of each, or exclude by less precise attributes. I have dmenu and dwm's status on top, which allows me to write a resolution independent location exclusion.

```
$ compton <any other arguments> --focus-exclude "x = 0 && y = 0 && override_redirect = true"

```

Otherwise, where using a configuration file:

```
focus-exclude = "x = 0 && y = 0 && override_redirect = true";

```

The override redirect property seems to be false for most windows- having this in the exclusion rule prevents other windows drawn in the upper left corner from being excluded (for example, when dwm statusbar is hidden, x0 y0 will match whatever is in dwm's master stack).

### Unable to change the background color with xsetroot

Currently, compton is incompatible with `xsetroot`'s `-solid` option, a workaround is to use [hsetroot](https://aur.archlinux.org/packages/hsetroot/) to set the background color:

```
$ hsetroot -solid '#000000'

```

For a detailed explanation, please see [https://github.com/chjj/compton/issues/162](https://github.com/chjj/compton/issues/162).

### Corrupted screen contents with Intel graphics

On at least some Intel chipsets, DRI3 is known to cause [trouble](https://bugs.freedesktop.org/show_bug.cgi?id=97916) for compton when the display resolution is changed or a new monitor is connected. This can happen with either the `intel` or `modesetting` driver. A workaround is to [disable DRI3](/index.php/Intel_graphics#DRI3_issues "Intel graphics").

### Screen artifacts/screenshot issues when using AMD's Catalyst driver

Try running compton with

```
--backend xrender

```

or adding

```
backend = "xrender";

```

to your compton.conf file.

For more info, please see [https://github.com/chjj/compton/issues/208](https://github.com/chjj/compton/issues/208)

### High CPU use with nvidia drivers

When facing high CPU use with `--backend glx` or tearing with `--vsync` enabled, [install](/index.php/Install "Install") [nvidia-libgl](https://www.archlinux.org/packages/?name=nvidia-libgl) as described in [NVIDIA](/index.php/NVIDIA "NVIDIA").

### Errors while trying to daemonize with nvidia drivers

If you get error `main(): Failed to create new session.` while trying to start compton in background you should try [compton-garnetius-git](https://aur.archlinux.org/packages/compton-garnetius-git/). It also provides a few pulls from upstream that aren't merged yet.

### Lag when using xft fonts

If you experience heavy lag when using Xft fonts in applications such as [xterm](/index.php/Xterm "Xterm") or [urxvt](/index.php/Urxvt "Urxvt") try running with

```
--xrender-sync --xrender-sync-fence

```

or try using the xrender backend.

See [[1]](https://github.com/chjj/compton/issues/152) for more information.

## See also

*   [Howto: Using Compton for tear-free compositing on XFCE or LXDE](http://ubuntuforums.org/showthread.php?t=2144468&p=12644745#post12644745)