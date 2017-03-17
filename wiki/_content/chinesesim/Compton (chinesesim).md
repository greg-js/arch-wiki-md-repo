Compton是一个独立的复合管理器，适用于不提供合成功能的窗口管理器 (例如 i3-wm) Compton 是 [xcompmgr-dana](http://oliwer.net/xcompmgr-dana/) 的一个分支, 也是 [xcompmgr](/index.php/Xcompmgr "Xcompmgr") 的一个分支，可查看 [compton github page](https://github.com/chjj/compton) 获取更多信息。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 使用](#.E4.BD.BF.E7.94.A8)
    *   [2.1 开机时自动启动 Compton](#.E5.BC.80.E6.9C.BA.E6.97.B6.E8.87.AA.E5.8A.A8.E5.90.AF.E5.8A.A8_Compton)
    *   [2.2 Command only](#Command_only)
    *   [2.3 Using a configuration file](#Using_a_configuration_file)
        *   [2.3.1 Disable shadowing of some windows](#Disable_shadowing_of_some_windows)
*   [3 Multihead](#Multihead)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 slock](#slock)
    *   [4.2 dwm & dmenu](#dwm_.26_dmenu)
    *   [4.3 Unable to change the background color with xsetroot](#Unable_to_change_the_background_color_with_xsetroot)
    *   [4.4 Corrupted screen contents with Intel graphics](#Corrupted_screen_contents_with_Intel_graphics)
    *   [4.5 Screen artifacts/screenshot issues when using AMD's Catalyst driver](#Screen_artifacts.2Fscreenshot_issues_when_using_AMD.27s_Catalyst_driver)
    *   [4.6 High CPU use with nvidia drivers](#High_CPU_use_with_nvidia_drivers)
    *   [4.7 Errors while trying to daemonize with nvidia drivers](#Errors_while_trying_to_daemonize_with_nvidia_drivers)
    *   [4.8 Lag when using xft fonts](#Lag_when_using_xft_fonts)
*   [5 See also](#See_also)

## 安装

安装包 [compton](https://www.archlinux.org/packages/?name=compton) 。 如果要使用 [git](/index.php/Git "Git") 版本，可安装 [compton-git](https://aur.archlinux.org/packages/compton-git/).

## 使用

Compton 可在任何时候在终端启用或停用，或设置为自动启动 ([Daemon](/index.php/Daemon "Daemon")) 成为后台进程。还有几个可选参数可用于调整提供的合成效果。包括:

*   `-b`: 运行于后台进程当中 ([Daemon](/index.php/Daemon "Daemon")) (例如当自动启动时 [window manager](/index.php/Window_manager "Window manager") 启动 [Openbox](/index.php/Openbox "Openbox"))
*   `-c`: 启用阴影效果
*   `-C`: 禁用面板和 Docks 的阴影效果
*   `-G`: 禁用应用程序窗口和拖放对象的阴影效果
*   `--config`: 使用指定的配置文件

还有更多选项可用，包括设置时间，要管理的显示以及菜单，窗口边框和非活动应用程序菜单的不透明度。有关详细信息，请参阅[Compton Man Page](https://github.com/chjj/compton/blob/master/man/compton.1.asciidoc) 。

**注意:** 如果正在运行不同的 [composite manager](/index.php/Composite_manager "Composite manager")，则应在启动 compton 之前禁用它。

### 开机时自动启动 Compton

如何将 Compton 自动启动作为守护进程将取决于桌面环境或窗口管理器使用。 例如，对于 Openbox，请编辑 `~/.config/openbox/autostart`，而对于 i3-wm，它将是 `~/.config/i3/config` 文件。 必要时，compton 也可以从 [xprofile](/index.php/Xprofile "Xprofile") 或 [Xinitrc](/index.php/Xinitrc "Xinitrc") 自动启动。有关更多信息，请参阅 [startup files](/index.php/Startup_files "Startup files") 一文。

### Command only

To manually enable default compositing effects during a session, use the following command:

```
$ compton

```

Alternatively, to disable all shadowing effects during a session, the `-C` and `-G` arguments must be added:

```
$ compton -CG

```

To autostart compton as a background ([Daemon](/index.php/Daemon "Daemon")) process for a session, the `-b` argument must be used:

```
compton -b

```

To disable all shadowing effects from the [Daemon](/index.php/Daemon "Daemon") process, the `-C` and `-G` arguments must again be added:

```
compton -CGb

```

Finally, this is an example where additional arguments that require values to be set have been used:

```
compton -cCGfF -o 0.38 -O 200 -I 200 -t 0 -l 0 -r 3 -D2 -m 0.88

```

### Using a configuration file

The default configuration is available in `/etc/xdg/compton.conf`. For modifications, it can be copied to `~/.config/compton.conf`, or to `~/.compton.conf`.

To use a custom configuration file with compton during a session, use the following command:

```
compton --config *path/to/compton.conf*

```

To auto-start compton as a background ([Daemon](/index.php/Daemon "Daemon")) process for a session, specify the `-b` argument:

```
compton --config *path/to/compton.conf* -b

```

#### Disable shadowing of some windows

Due to the way compton draws its shadows, certain applications will have visual glitches when you have shadows enabled. The `shadow-exclude` options could disable compton shadows.

For example, to disable Compton shadows on all GTK +3 windows, add below setting to `shadow-exclude` in `compton.conf`:

```
"_GTK_FRAME_EXTENTS@:c"

```

To disable shadows around [conky](/index.php/Conky "Conky") windows - where used - first amend the conky configuration file `~/.conkyrc` as follows:

```
own_window_class conky

```

Then amend the compton configuration file as follows:

```
shadow-exclude = "class_g = 'conky'";

```

For currently disabled windows, please see [here](https://projects.archlinux.org/svntogit/community.git/tree/trunk/compton.conf?h=packages/compton#n80).

## Multihead

If a [multihead](/index.php/Multihead "Multihead") configuration is used without xinerama - meaning that X server is started with more than one screen - then compton will start on only one screen by default. It can be started on all screens by using the `-d` argument. For example, compton can be executed for 4 monitors with the following command:

```
seq 0 3 | xargs -l1 -I@ compton -b -d :0.@

```

## Troubleshooting

The use of compositing effects may on occasion cause issues such as visual glitches when not configured correctly for use with other applications and programs.

### slock

Where inactive window transparency has been enabled (the `-i` argument when running as a command), this may provide troublesome results when also using [slock](/index.php/Slock "Slock"). One solution is to amend the transparency to `0.2`. For example, where running compton arguments as a command:

```
$ compton <any other arguments> -i 0.2

```

Otherwise, where using a configuration file:

```
inactive-dim = 0.2;

```

Alternatively, you may try to exclude slock by its window id, or by excluding all windows with no name.

**Note:** Some programs change their id for every new instance, but slock's appears to be static. Someone more knowledgeable will have to confirm that slock's id is in fact static- until then, use at your own risk.

Exclude all windows with no name from compton using the following options:

```
$ compton <other arguments> --focus-exclude "! name~=*"*

```

Find your slock's window id by running the command:

```
$ xwininfo & slock

```

Quickly click anywhere on the screen (before slock exits), then type your password to unlock. You should see the window id in the output:

```
xwininfo: Window id: 0x1800001 (has no name)

```

Take the window id and exclude it from compton with:

```
$ compton <any other arguments> --focus-exclude 'id = 0x1800001'

```

Otherwise, where using a configuration file:

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