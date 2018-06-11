相关文章

*   [Steam/Wine](/index.php/Steam/Wine "Steam/Wine")
*   [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting")

引自 [维基百科](/index.php?title=Zh-cn:Wikipedia:Steam&action=edit&redlink=1 "Zh-cn:Wikipedia:Steam (page does not exist)"):

	*Steam是美国维尔福于2003年9月12日推出的电子软件分发、数字版权管理及社交系统，它用于数字软件及游戏的发布销售与后续更新，支持Windows、Mac OS和Linux等操作系统，目前是全球最大的数字游戏平台。*

[Steam](http://store.steampowered.com/about/) is best known as the platform needed to play Source Engine games (e.g. Half-Life 2, Counter-Strike). Today it offers many games from many other developers.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 疑难问题](#.E7.96.91.E9.9A.BE.E9.97.AE.E9.A2.98)
    *   [2.1 鼠标主题不一致](#.E9.BC.A0.E6.A0.87.E4.B8.BB.E9.A2.98.E4.B8.8D.E4.B8.80.E8.87.B4)
    *   [2.2 点击关闭按钮时将 Steam 最小化](#.E7.82.B9.E5.87.BB.E5.85.B3.E9.97.AD.E6.8C.89.E9.92.AE.E6.97.B6.E5.B0.86_Steam_.E6.9C.80.E5.B0.8F.E5.8C.96)
    *   [2.3 64位系统上 Flash 无法使用](#64.E4.BD.8D.E7.B3.BB.E7.BB.9F.E4.B8.8A_Flash_.E6.97.A0.E6.B3.95.E4.BD.BF.E7.94.A8)
    *   [2.4 Text is corrupt or missing](#Text_is_corrupt_or_missing)
    *   [2.5 SetLocale('en_US.UTF-8') fails at game startup](#SetLocale.28.27en_US.UTF-8.27.29_fails_at_game_startup)
    *   [2.6 The game crashes immediately after start](#The_game_crashes_immediately_after_start)
    *   [2.7 OpenGL not using direct rendering](#OpenGL_not_using_direct_rendering)
    *   [2.8 libGL error when running certain games](#libGL_error_when_running_certain_games)
    *   [2.9 OpenGL GLX context is not using direct rendering, which may cause performance problems.](#OpenGL_GLX_context_is_not_using_direct_rendering.2C_which_may_cause_performance_problems.)
    *   [2.10 No audio in certain games](#No_audio_in_certain_games)
    *   [2.11 You are missing the following 32-bit libraries, and Steam may not run: libGL.so.1](#You_are_missing_the_following_32-bit_libraries.2C_and_Steam_may_not_run:_libGL.so.1)
    *   [2.12 Games do not launch on older intel hardware](#Games_do_not_launch_on_older_intel_hardware)
    *   [2.13 X crashes when Steam starts (Radeon open source driver)](#X_crashes_when_Steam_starts_.28Radeon_open_source_driver.29)
*   [3 Launching games with custom commands, such as Bumblebee/Primus](#Launching_games_with_custom_commands.2C_such_as_Bumblebee.2FPrimus)
    *   [3.1 Killing standalone compositors when launching games](#Killing_standalone_compositors_when_launching_games)
*   [4 Using native runtime](#Using_native_runtime)
*   [5 Steam 皮肤](#Steam_.E7.9A.AE.E8.82.A4)
    *   [5.1 Steam 皮肤管理器](#Steam_.E7.9A.AE.E8.82.A4.E7.AE.A1.E7.90.86.E5.99.A8)
*   [6 See also](#See_also)

## 安装

**注意:**

*   Arch Linux并不在[官方支持](https://support.steampowered.com/kb_article.php?ref=1504-QHXN-8366) 中。
*   由于Steam客户端是个32位程序，用户需要在pacman中开启 [Multilib](/index.php/Multilib "Multilib") 软件源。 **如果你的系统是纯64位的话**。 有可能还需要安装一些multilib-devel软件包来提供重要的multilib库。此外，还需要安装显卡的32位版本才能运行Steam。

现在，可直接从 [官方仓库](/index.php/%E5%AE%98%E6%96%B9%E4%BB%93%E5%BA%93 "官方仓库") 中安装 [steam](https://www.archlinux.org/packages/?name=steam) 。如果你使用64位系统，请先启用 [multilib](/index.php/Multilib "Multilib") 仓库。

Steam 目前在 Arch Linux 上并不被官方支持，因此需要用户做一些调整以使程序顺利运行：

*   Steam中大量使用 Arial 字体。你可以通过安装 [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) 或 [ttf-microsoft-arial](https://aur.archlinux.org/packages/ttf-microsoft-arial/) 或 [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) 或 [Steam提供的字体](#Text_is_corrupt_or_missing) 来让它看起来漂亮点儿。亚洲语言建议使用[wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei)。

*   如果你使用64位系统，你还需要安装 [32位版本的显卡驱动](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.AE.89.E8.A3.85 "Xorg (简体中文)") (位于表格中“Multilib 软件包 ”这一列) 以运行32位游戏。

*   如果你使用64位系统，你还需要安装 [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins) 为32位游戏提供声音支持。

*   有些游戏可能需要附加依赖。如果游戏不能正常启动 （一般没有任何错误提示），请确保安装了 [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting") 中列出的依赖。

## 疑难问题

**Note:** 除了记录到这里， 所有还未被记录的bug、错误或修改方案都应该报告到 Valve 的 [GitHub page](https://github.com/ValveSoftware/steam-for-linux).

### 鼠标主题不一致

Steam启动时会覆盖掉 [鼠标主题](/index.php/Cursor_themes_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Cursor themes (简体中文)")。这个问题出现在没有设置鼠标主题的Gnome 和其他 WMs/DMs。 对于Gnome，可以通过设置鼠标主题来修正。

为了解决问题，首先获得root权限，然后按照下面提示创建文件 `/usr/share/icons/default/index.theme` (如果没有目录 `/usr/share/icons/default` 请自行创建):

 `/usr/share/icons/default/index.theme` 
```
[Icon Theme]
Inherits=Adwaita

```

注意: 请用你自己的鼠标主题替代 "Adwaita"。 或者，你可以从 [AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 中安装 [gnome-cursors-fix](https://aur.archlinux.org/packages/gnome-cursors-fix/)。

或者还可以创建指向鼠标主题的软链接 `~/.icons/default` , 比如：

```
   mkdir -p ~/.icons
   ln -sT /usr/share/icons/Neutral_Plus ~/.icons/default

```

If the cursor gets stuck pointing in the wrong direction after exiting Steam, a workaround is to run `xsetroot -cursor_name left_ptr` (From [the awesomewm wiki](http://awesome.naquadah.org/wiki/FAQ#How_to_change_the_cursor_theme.3F)).

### 点击关闭按钮时将 Steam 最小化

	Valve GitHub [issue 1025](https://github.com/ValveSoftware/steam-for-linux/issues/1025)

如果想在点击**x**时关闭 Steam 窗口（并将它从任务栏移除），同时让 Steam 最小化到托盘，你需要设置环境变量`STEAM_FRAME_FORCE_CLOSE` 为`1`。可以通过以下命令行启动 Steam：

```
$ STEAM_FRAME_FORCE_CLOSE=1 steam

```

如果你通过 .desktop 文件来启动 Steam，你需要将`Exec`替换为以下内容：

```
 Exec=sh -c 'STEAM_FRAME_FORCE_CLOSE=1 steam' %U

```

### 64位系统上 Flash 无法使用

	Steam Support [article](https://support.steampowered.com/kb_article.php?ref=1493-GHZB-7612)

首先确认已经安装了[lib32-flashplugin](https://www.archlinux.org/packages/?name=lib32-flashplugin)。如果安装后还无法使用，创建一个本地 Steam Flash 插件目录：

```
$ mkdir ~/.steam/bin32/plugins/

```

并且将全局的 lib32 flash 插件目录软链接到上面创建的路径：

```
$ ln -s /usr/lib32/mozilla/plugins/libflashplayer.so ~/.steam/bin32/plugins/

```

### Text is corrupt or missing

The Steam Support [instructions](https://support.steampowered.com/kb_article.php?ref=1974-YFKL-4947) for Windows seem to work on Linux also: Simply download [SteamFonts.zip](https://support.steampowered.com/downloads/1974-YFKL-4947/SteamFonts.zip) and [install](/index.php/Fonts#Manual_installation "Fonts") them (copying to `/usr/share/fonts/` or `~/.fonts/` works at least).

### SetLocale('en_US.UTF-8') fails at game startup

Uncomment `en_US.UTF-8 UTF-8` in `/etc/locale.gen` and then run `locale-gen` as root.

### The game crashes immediately after start

If your game crashes immediately, try disabling: *"Enable the Steam Overlay while in-game"* in game *Properties*.

### OpenGL not using direct rendering

	Steam Support [article](https://support.steampowered.com/kb_article.php?ref=9938-EYZB-7457)

You have probably not installed your 32-bit graphics driver correctly. See [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg") for which packages to install.

You can check/test if it is installed correctly by installing [lib32-mesa-demos](https://www.archlinux.org/packages/?name=lib32-mesa-demos) and running the following command:

```
$ glxinfo32 | grep OpenGL.

```

### libGL error when running certain games

If you receive an error like the following `Failed to load libGL: undefined symbol: xcb_send_fd`, it could be due to an outdated steam runtime library. Deleting `~/.local/share/Steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/libxcb.so.1` will force Steam to load the library version installed by pacman.

### OpenGL GLX context is not using direct rendering, which may cause performance problems.

Steam ships its own versions of some libraries, and they sometimes are too old to work with archlinux system libraries. Removing the library supplied by Steam means Steam has to use the newer arch-specific version. [Forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1416098#p1416098).

```
rm ~/.local/share/Steam/ubuntu12_32/steam-runtime/i386/usr/lib/i386-linux-gnu/libstdc++.so.6
rm ~/.local/share/Steam/ubuntu12_32/steam-runtime/i386/lib/i386-linux-gnu/libgcc_s.so.1
```

### No audio in certain games

If there is no audio in certain games, and the suggestions provided in [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting") do not fix the problem, [#Using native runtime](#Using_native_runtime) may provide a successful workaround.

### You are missing the following 32-bit libraries, and Steam may not run: libGL.so.1

You may encounter this error when you launch Steam at first time. Make sure you have installed lib32-version of all your video driver. For example, if you have installed [catalyst-utils-pxp](https://www.archlinux.org/packages/?name=catalyst-utils-pxp), [xf86-video-dri](https://www.archlinux.org/packages/?name=xf86-video-dri), [intel-dri](https://www.archlinux.org/packages/?name=intel-dri), [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl) for AMD and Intel double card, then you should install [lib32-catalyst-utils-pxp](https://www.archlinux.org/packages/?name=lib32-catalyst-utils-pxp), [lib32-intel-dri](https://www.archlinux.org/packages/?name=lib32-intel-dri), [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl).

### Games do not launch on older intel hardware

On older Intel hardware, if the game immediately crashes when run, it may be because your hardware doesn't directly support the latest OpenGL. It appears as a gameoverlayrenderer.so error in /var/dumps/mobile_stdout.txt, but looking in /tmp/gameoverlayrenderer.log it shows a GLXBadFBConfig error.

This can be fixed, however, by forcing the game to use a later version of OpenGL than it wants. Right click on the game, select Properties. Then, click "Set Launch Options" in the "General" tab and paste the following:

```
MESA_GL_VERSION_OVERRIDE=3.1 MESA_GLSL_VERSION_OVERRIDE=140 %command%

```

This will force the game to use the latest version of OpenGL.

### X crashes when Steam starts (Radeon open source driver)

There is [a bug](https://bugs.freedesktop.org/show_bug.cgi?id=79325) in glamor-egl 0.6.0 (used by the open source Radeon driver) which causes X to crash when trying to start Steam. Installing the unofficial [glamor-egl-git](https://aur.archlinux.org/packages/glamor-egl-git/) from AUR is a workaround until a new glamour version is released.

## Launching games with custom commands, such as Bumblebee/Primus

Steam has fortunately added support for launching games using your own custom command. To do so, navigate to the Library page, right click on the selected game, click Properties, and Set Launch Options. Steam replaces the tag `%command%` with the command it actually wishes to run. For example, to launch Team Fortress 2 with primusrun and at resolution 1920x1080, you would enter:

```
primusrun %command% -w 1920 -h 1080

```

If you are running the [Linux-ck](/index.php/Linux-ck "Linux-ck") kernel, you may have some success in reducing overall latencies and improving performance by launching the game in SCHED_ISO (low latency, avoid choking CPU) via [schedtool](https://www.archlinux.org/packages/?name=schedtool)

```
# schedtool -I -e %command% *other arguments*

```

### Killing standalone compositors when launching games

Further to this, utilising the `%command%` switch, you can kill standalone compositors (such as Xcompmgr or [Compton](/index.php/Compton "Compton")) - which can cause lag and tearing in some games on some systems - and relaunch them after the game ends by adding the following to your game's launch options.

```
 killall compton && %command%; nohup compton &

```

Replace `compton` in the above command with whatever your compositor is. You can also add -options to `%command%` or `compton`, of course.

Steam will latch on to any processes launched after `%command%` and your Steam status will show as in game. So in this example, we run the compositor through `nohup` so it is not attached to Steam (it will keep running if you close Steam) and follow it with an ampersand so that the line of commands ends, clearing your Steam status.

## Using native runtime

Steam, by default, ships with a copy of every library it uses, packaged within itself, so that games can launch without issue. This can be a resource hog, and the slightly out-of-date libraries they package may be missing important features (Notably, the OpenAL version they ship lacks HRTF and surround71 support). To use your own system libraries, you can run Steam with:

```
$ STEAM_RUNTIME=0 steam

```

However, if you're missing any libraries Steam makes use of, this will fail to launch properly. An easy way to find the missing libraries is to run the following commands:

```
$ cd ~/.local/share/Steam/ubuntu12_32
$ LD_LIBRARY_PATH=".:${LD_LIBRARY_PATH}" ldd $(file *|sed '/ELF/!d;s/:.*//g')|grep 'not found'|sort|uniq

```

**Note:** The libraries will have to be 32-bit, which means you may have to download some from the AUR if on x86_64, such as NetworkManager.

Once you've done this, run steam again with `STEAM_RUNTIME=0 steam` and verify it's not loading anything outside of the handful of steam support libraries:

```
$ cat /proc/$(pidof steam)/maps|sed '/\.local/!d;s/.*  //g'|sort|uniq

```

## Steam 皮肤

通过拷贝和修改皮肤目录下的文件， Steam 界面可以被完全的定制化。

### Steam 皮肤管理器

AUR上的[steam-skin-manager](https://aur.archlinux.org/packages/steam-skin-manager/) 让 Steam 皮肤的使用过程被大大简化。这个软件包还带有一个 hacked 过的 Steam 启动器，窗口管理器可以在这个 Steam 窗口上绘制边框。

因此就有两种风格的 Steam 皮肤，一类有窗口按钮一类没有。皮肤管理器会提示你要使用哪种，还会根据你的 GTK+ 主题自动使用对应的皮肤，当然你也可以自己选择。

皮肤管理器自动两种皮肤，对应 Ubuntu 默认主题的 Ambiance 和 Radiance.

## See also

*   [https://wiki.gentoo.org/wiki/Steam](https://wiki.gentoo.org/wiki/Steam)