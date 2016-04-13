**翻译状态：** 本文是英文页面 [Mpv](/index.php/Mpv "Mpv") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-04-13，点击[这里](https://wiki.archlinux.org/index.php?title=Mpv&diff=0&oldid=429916)可以查看翻译后英文页面的改动。

[mpv](http://mpv.io/) 是一个基于 [MPlayer](/index.php/MPlayer "MPlayer") 和 MPlayer2 的多媒体播放器。 它支持多种视频文件格式、音频和视频编解码器和字幕类型。 在[这里](https://github.com/mpv-player/mpv/blob/master/DOCS/mplayer-changes.rst)可以找到mpv播放器与上述播放器之间的区别的综合列表（可能不是完全统计）。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 前端](#.E5.89.8D.E7.AB.AF)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 一个示例 input.conf 文件](#.E4.B8.80.E4.B8.AA.E7.A4.BA.E4.BE.8B_input.conf_.E6.96.87.E4.BB.B6)
*   [3 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [3.1 硬件编码](#.E7.A1.AC.E4.BB.B6.E7.BC.96.E7.A0.81)
    *   [3.2 高品质视频输出](#.E9.AB.98.E5.93.81.E8.B4.A8.E8.A7.86.E9.A2.91.E8.BE.93.E5.87.BA)
    *   [3.3 自动恢复上次停止的地方](#.E8.87.AA.E5.8A.A8.E6.81.A2.E5.A4.8D.E4.B8.8A.E6.AC.A1.E5.81.9C.E6.AD.A2.E7.9A.84.E5.9C.B0.E6.96.B9)
    *   [3.4 音量太小](#.E9.9F.B3.E9.87.8F.E5.A4.AA.E5.B0.8F)
    *   [3.5 快速循环多重纵横比](#.E5.BF.AB.E9.80.9F.E5.BE.AA.E7.8E.AF.E5.A4.9A.E9.87.8D.E7.BA.B5.E6.A8.AA.E6.AF.94)
    *   [3.6 从根窗口绘制](#.E4.BB.8E.E6.A0.B9.E7.AA.97.E5.8F.A3.E7.BB.98.E5.88.B6)
    *   [3.7 总是显示图形界面](#.E6.80.BB.E6.98.AF.E6.98.BE.E7.A4.BA.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2)
    *   [3.8 作为浏览器插件使用](#.E4.BD.9C.E4.B8.BA.E6.B5.8F.E8.A7.88.E5.99.A8.E6.8F.92.E4.BB.B6.E4.BD.BF.E7.94.A8)
    *   [3.9 使用Lua脚本让mpv作为音乐播放器](#.E4.BD.BF.E7.94.A8Lua.E8.84.9A.E6.9C.AC.E8.AE.A9mpv.E4.BD.9C.E4.B8.BA.E9.9F.B3.E4.B9.90.E6.92.AD.E6.94.BE.E5.99.A8)
    *   [3.10 Twitch.tv streaming over mpv](#Twitch.tv_streaming_over_mpv)
    *   [3.11 使用youtube-dl 并选择格式](#.E4.BD.BF.E7.94.A8youtube-dl_.E5.B9.B6.E9.80.89.E6.8B.A9.E6.A0.BC.E5.BC.8F)
    *   [3.12 youtube-dl audio with search](#youtube-dl_audio_with_search)
    *   [3.13 使用mpv与合成器](#.E4.BD.BF.E7.94.A8mpv.E4.B8.8E.E5.90.88.E6.88.90.E5.99.A8)
*   [4 Vapoursynth](#Vapoursynth)
    *   [4.1 Debanding (flash3kyuu)](#Debanding_.28flash3kyuu.29)

## 安装

[Install](/index.php/Install "Install") [mpv](https://www.archlinux.org/packages/?name=mpv) 可以从 [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") [official repositories](/index.php/Official_repositories "Official repositories") 或 [mpv-git](https://aur.archlinux.org/packages/mpv-git/) 安装mpv。

### 前端

*mpv* 提供了一个叫做OSC的优雅的用户界面（在移动鼠标时出现），为了降低普通用户的使用难度，还有其他的图形界面：

*   **Baka MPlayer** — 免费、开源、跨平台， 基于*libmpv*的多媒体播放器。(Qt 5)

	[https://github.com/u8sand/Baka-MPlayer/](https://github.com/u8sand/Baka-MPlayer/) || [baka-mplayer](https://www.archlinux.org/packages/?name=baka-mplayer), [baka-mplayer-git](https://aur.archlinux.org/packages/baka-mplayer-git/)

*   **bomi** — 强大易用的多媒体播放器 (Qt 5)。

	[https://bomi-player.github.io/](https://bomi-player.github.io/) || [bomi](https://aur.archlinux.org/packages/bomi/)。 [bomi-git](https://aur.archlinux.org/packages/bomi-git/)

*   **GNOME MPV** — 一个简单的 *mpv* 前端 (GTK+ 3).

	[https://github.com/gnome-mpv/gnome-mpv/](https://github.com/gnome-mpv/gnome-mpv/) || [gnome-mpv-git](https://aur.archlinux.org/packages/gnome-mpv-git/)。 [gnome-mpv](https://aur.archlinux.org/packages/gnome-mpv/)

*   **[SMPlayer](https://en.wikipedia.org/wiki/SMPlayer "wikipedia:SMPlayer")** — Qt 写的拥有额外特性的多媒体播放器 (CSS 主题, YouTube 整合等等) (Qt 5).

	[http://smplayer.sourceforge.net/](http://smplayer.sourceforge.net/) || [smplayer](https://www.archlinux.org/packages/?name=smplayer)

*   **xt7-player-mpv** — Qt/Gambas 写的 mpv 图形界面，提供了一套丰富的配置选项，包括过滤器和驱动，ladspa 插件支持以及资源库/播放列表管理, 还有YouTube, 在线电台, podcasts, DVB-T 和更多。

	[https://github.com/kokoko3k/xt7-player-mpv](https://github.com/kokoko3k/xt7-player-mpv) || [xt7-player-mpv-git](https://aur.archlinux.org/packages/xt7-player-mpv-git/)

**Note:** CMPlayer/*bomi* 安装包已在内部集成 *mpv*。

## 配置

*mpv'*s configuration is read from the files `mpv.conf` (settings), `input.conf` (key bindings), and `lua-settings/osc.conf` (on screen display). For a full list of options, see the man page or the github docs [options.rst](https://github.com/mpv-player/mpv/blob/master/DOCS/man/options.rst), [input.rst](https://github.com/mpv-player/mpv/blob/master/DOCS/man/input.rst), and [osc.rst](https://github.com/mpv-player/mpv/blob/master/DOCS/man/osc.rst).

If the [environment variable](/index.php/Environment_variable "Environment variable") `XDG_CONFIG_HOME` is not set, user configuration files will be read from the `~/.config/mpv` directory. System-wide configuration files are read from the `/etc/mpv` directory.

### 一个示例 `input.conf` 文件

Copying the following into `~/.config/mpv/input.conf` will add a number of useful keybindings to mpv such as rotating video 90 degrees, zooming and panning.

```
Alt+RIGHT add video-rotate 90
Alt+LEFT add video-rotate -90
Alt+- add video-zoom -0.25
Alt+= add video-zoom 0.25
Alt+j add video-pan-x -0.05
Alt+l add video-pan-x 0.05
Alt+i add video-pan-y 0.05
Alt+k add video-pan-y -0.05

```

## 提示和技巧

### 硬件编码

Unlike *mplayer* and *mplayer2*, *mpv* has both [VA-API](/index.php/VA-API "VA-API") and [VDPAU](/index.php/VDPAU "VDPAU") support built-in. To enable it, run *mpv* with the `--hwdec='method'` option. You can find list of all available methods looking for `--hwdec=<api>` in [man page](/index.php/Man_page "Man page") `mpv (1)`. To make this persistent, add the line `hwdec=*method*` to your configuration file. When hardware decoding is used, the video output should be set to `opengl`, `opengl-hq` or `vdpau` (if using `hwdec=vdpau`). Using `vo=vaapi` is not recommended for use anymore [[1]](https://github.com/mpv-player/mpv/blob/master/DOCS/man/vo.rst). If hardware decoding cannot be used, *mpv* will automatically fall back to software decoding. See [options.rst](https://github.com/mpv-player/mpv/blob/master/DOCS/man/options.rst) and [vo.rst](https://github.com/mpv-player/mpv/blob/master/DOCS/man/vo.rst) for more information.

### 高品质视频输出

The `opengl-hq` video output is an OpenGL output preconfigured with various options by the mpv developers. To make use of it, specify it in your configuration file.

 `~/.config/mpv/mpv.conf`  `vo=opengl-hq` 

This comes with a GLSL debanding filter by default, which may lead to bad performance for some users, and can reduce the visual quality of grainy content. You can disable it easily though.

 `~/.config/mpv/mpv.conf`  `vo=opengl-hq:deband=no` 

### 自动恢复上次停止的地方

The default key to quit *mpv*, saving the video's current position and state, is `Shift+q`. This key can be changed by adding the `quit_watch_later` string in the key bindings configuration file.

To always automatically save the current playback position on quit, start *mpv* with a flag `--save-position-on-quit`. To make option permanent, add line `save-position-on-quit` to configuration file.

### 音量太小

Set `softvol-max=*value*` in your configuration file to a reasonable amount, such as `softvol-max=600`. Additionally (or alternatively), you can utilize [dynamic range compression](https://en.wikipedia.org/wiki/Dynamic_range_compression "wikipedia:Dynamic range compression") with `af=drc`.

### 快速循环多重纵横比

You can cycle between aspect ratios using `Shift+a` from version 0.8.0 onwards.

### 从根窗口绘制

Run *mpv* with `--wid=0`. This tells *mpv* to draw onto a window with a window ID of 0.

### 总是显示图形界面

It may be useful to always show the GUI window, even for audio files, especially when *mpv* is not started from terminal. This can be done by using `--force-window` option.

### 作为浏览器插件使用

With the help of [mozplugger](https://aur.archlinux.org/packages/mozplugger/), *mpv* can be used in a supported browser to play video. See [Browser plugins#MozPlugger](/index.php/Browser_plugins#MozPlugger "Browser plugins") for configuration details. This coupled with a user script such as [ViewTube](http://isebaro.com/viewtube/?ln=en), allows you to use *mpv* in place of a site's integrated video player.

[Browser plugins#Video players workarounds](/index.php/Browser_plugins#Video_players_workarounds "Browser plugins") page shows other easy ways to watch videos.

### 使用Lua脚本让mpv作为音乐播放器

The development of mpv's Lua scripts are documented in [DOCS/man/lua.rst](https://github.com/mpv-player/mpv/blob/master/DOCS/man/lua.rst) and examples are shown in [TOOLS/lua](https://github.com/mpv-player/mpv/tree/master/TOOLS/lua) of the [mpv repository](https://github.com/mpv-player/mpv). [This blog post](http://bamos.github.io/2014/07/05/mpv-lua-scripting/) introduces the [music.lua](https://github.com/bamos/dotfiles/blob/master/.mpv/scripts/music.lua) script, which shows how Lua scripts can be used to improve mpv as a music player.

### Twitch.tv streaming over mpv

If [youtube-dl](https://www.archlinux.org/packages/?name=youtube-dl) is installed, mpv can directly open a Twitch livestream.

Alternatively, [livestreamer](https://www.archlinux.org/packages/?name=livestreamer) can be used to stream Twitch. See [Livestreamer#Twitch](/index.php/Livestreamer#Twitch "Livestreamer").

Another alternative based on Livestreamer is this Lua script: [https://gist.github.com/ChrisK2/8701184fe3ea7701c9cc](https://gist.github.com/ChrisK2/8701184fe3ea7701c9cc)

### 使用youtube-dl 并选择格式

The default `--ytdl-format` is `bestvideo+bestaudio/best`. For youtube videos that have 4K resolutions available, this may mean that your device will struggle to decode 4K VP9 encoded video in software even if the attached monitor is much lower resolution.

Setting the right youtube-dl format selectors can fix this easily though. In the following configuration example, only videos with a vertical resolution of 1080 pixels or less will be considered.

```
ytdl-format=bestvideo[height<=?1080]+bestaudio/best

```

If you wish to avoid a certain codec altogether because you cannot hardware-decode it, you can add this to the format selector. For example, we can additionally choose to ignore VP9 as follows:

```
ytdl-format=bestvideo[height<=?1080][vcodec!=vp9]+bestaudio/best

```

### youtube-dl audio with search

To find and play audio straight from your terminal with `mm ' *SEARCH* '` put the following function in your `.bashrc`:

```
mm () { youtube-dl ytsearch:"$@" -q -f bestaudio --ignore-config --console-title --print-traffic --max-downloads 1 --no-call-home --no-playlist -o - | mpv --no-terminal --no-video --cache=256 -; }

```

### 使用mpv与合成器

If you're using a compositor (e.g. in KDE Plasma 5) and find that composition is disabled (e.g. in Plasma this would make you unable to present windows or see window thumbnails in the default app switcher) when mpv is playing a video, try `x11-bypass-compositor=no`

## Vapoursynth

Vapoursynth is an alternative to AviSynth that can be used on Linux and allows for Video manipulation via python scripts. Vapoursynths python scripts can be used as video filters for *mpv*.

To use vapoursynth filters you have to install the `vapoursynth` package and compile *mpv* with the `--enable-vapoursynth` build flag.

### Debanding (flash3kyuu)

To use the f3k_db debanding filter install [vapoursynth-plugin-flash3kyuu_deband-git](https://aur.archlinux.org/packages/vapoursynth-plugin-flash3kyuu_deband-git/) and write a python script that uses the *vapoursynth* extension.

The following sample script can be used to enable debanding in *mpv*.

```
import vapoursynth as vs
core = vs.get_core()

clip = video_in
clip = core.std.Trim(clip, first=0, length=500000)
clip = core.f3kdb.Deband(clip, grainy=0, grainc=0, output_depth=16)
clip.set_output()

```

Finally specify the python script in the config file or use a command line argument when executing mpv.

```
mpv --vf=vapoursynth=f3k_db.py <video_file>

```