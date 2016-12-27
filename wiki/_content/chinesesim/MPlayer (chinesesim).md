**翻译状态：** 本文是英文页面 [MPlayer](/index.php/MPlayer "MPlayer") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-12-23，点击[这里](https://wiki.archlinux.org/index.php?title=MPlayer&diff=0&oldid=454536)可以查看翻译后英文页面的改动。

[MPlayer](http://www.mplayerhq.hu/) 是 GNU/Linux 下非常流行的影音播放器，支持大多数文件格式，非常通用。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 图形前端](#.E5.9B.BE.E5.BD.A2.E5.89.8D.E7.AB.AF)
*   [3 浏览器整合](#.E6.B5.8F.E8.A7.88.E5.99.A8.E6.95.B4.E5.90.88)
    *   [3.1 Firefox 和 Chromium](#Firefox_.E5.92.8C_Chromium)
    *   [3.2 Konqueror](#Konqueror)
*   [4 配置](#.E9.85.8D.E7.BD.AE)
    *   [4.1 按键绑定](#.E6.8C.89.E9.94.AE.E7.BB.91.E5.AE.9A)
*   [5 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [5.1 继续之前的播放](#.E7.BB.A7.E7.BB.AD.E4.B9.8B.E5.89.8D.E7.9A.84.E6.92.AD.E6.94.BE)
    *   [5.2 硬件加速](#.E7.A1.AC.E4.BB.B6.E5.8A.A0.E9.80.9F)
        *   [5.2.1 启用 VDPAU](#.E5.90.AF.E7.94.A8_VDPAU)
        *   [5.2.2 Enabling VA-API](#Enabling_VA-API)
    *   [5.3 Translucent video with Radeon cards and Composite enabled](#Translucent_video_with_Radeon_cards_and_Composite_enabled)
    *   [5.4 播放流媒体文件](#.E6.92.AD.E6.94.BE.E6.B5.81.E5.AA.92.E4.BD.93.E6.96.87.E4.BB.B6)
    *   [5.5 播放DVD](#.E6.92.AD.E6.94.BEDVD)
        *   [5.5.1 DVB-T Streaming](#DVB-T_Streaming)
    *   [5.6 JACK support](#JACK_support)
    *   [5.7 Advanced Subtitles](#Advanced_Subtitles)
    *   [5.8 Internet radio](#Internet_radio)
*   [6 问题处理](#.E9.97.AE.E9.A2.98.E5.A4.84.E7.90.86)
    *   [6.1 无法打开名称含空格的文件](#.E6.97.A0.E6.B3.95.E6.89.93.E5.BC.80.E5.90.8D.E7.A7.B0.E5.90.AB.E7.A9.BA.E6.A0.BC.E7.9A.84.E6.96.87.E4.BB.B6)
    *   [6.2 MPlayer has black or strange colored font for OSD and Subtitles](#MPlayer_has_black_or_strange_colored_font_for_OSD_and_Subtitles)
    *   [6.3 Smplayer无图像](#Smplayer.E6.97.A0.E5.9B.BE.E5.83.8F)
    *   [6.4 Transparent SMPlayer in Gnome with Composite enabled](#Transparent_SMPlayer_in_Gnome_with_Composite_enabled)
    *   [6.5 SMPlayer: OSD font too big / subtitle text too small](#SMPlayer:_OSD_font_too_big_.2F_subtitle_text_too_small)
    *   [6.6 Mplayer shows question marks for some characters on subtitle](#Mplayer_shows_question_marks_for_some_characters_on_subtitle)
    *   [6.7 Choppy audio CD playback](#Choppy_audio_CD_playback)

## 安装

*   **[MPlayer](/index.php/MPlayer "MPlayer")** — 官方软件包

	[https://mplayerhq.hu/](https://mplayerhq.hu/) || [mplayer](https://www.archlinux.org/packages/?name=mplayer)

其他版本：

*   **MPlayer-VAAPI** — 启用 VAAPI 的版本

	[http://gitorious.org/vaapi/mplayer](http://gitorious.org/vaapi/mplayer) || [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/)

*   **MPlayer-svn** — 开发版本

	|| [mplayer-svn](https://aur.archlinux.org/packages/mplayer-svn/)

*   **MPlayer2** — MPlayer 的一个分支

	[http://www.mplayer2.org/](http://www.mplayer2.org/) || [mplayer2](https://aur.archlinux.org/packages/mplayer2/)

**注意:** *mplayer2* 的开发已经停止，推荐使用 [mpv](/index.php/Mpv "Mpv")，mpv 更注重速度和开发质量，这会破坏兼容性，使用前请注意一下它们的 [差异](https://github.com/mpv-player/mpv/blob/master/DOCS/mplayer-changes.rst)。

## 图形前端

*   **[SMPlayer](https://en.wikipedia.org/wiki/SMPlayer "wikipedia:SMPlayer")** — MPlayer 的Qt前端，外加一些补丁。

	[http://smplayer.sourceforge.net/](http://smplayer.sourceforge.net/) || [smplayer](https://www.archlinux.org/packages/?name=smplayer)

*   **UMPlayer** — SMPlayer的个分支，额外功能包括:CSS 主题、YouTube 整合、ShoutCast 支持等。

	[http://www.umplayer.com/](http://www.umplayer.com/) || [umplayer](https://aur.archlinux.org/packages/umplayer/)

*   **GNOME-MPlayer** — MPlayer的 GTK 前端。

	[http://kdekorte.googlepages.com/gnomemplayer](http://kdekorte.googlepages.com/gnomemplayer) || [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer)

*   **KMPlayer** — Konqueror 视频播放插件，KDE 的MPlayer/Xine/ffmpeg/ffserver/VDR 前端。

	[http://kmplayer.kde.org/](http://kmplayer.kde.org/) || [kmplayer](https://www.archlinux.org/packages/?name=kmplayer)

## 浏览器整合

要让MPlayer控制浏览器的影音播放，请安装以下内容：

### Firefox 和 Chromium

[官方软件仓库](/index.php/Official_repositories "Official repositories")提供了[gecko-mediaplayer](https://www.archlinux.org/packages/?name=gecko-mediaplayer) 软件包，依赖于 [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer)，这个软件还提供了完整的图形前端。

### Konqueror

[AUR](/index.php/AUR "AUR") 中的 [kmplayer](https://www.archlinux.org/packages/?name=kmplayer) 软件包提供了Konqueror 插件，这个软件包也提供了完整的 mplayer 图形前端。

## 配置

系统全局配置文件位于`/etc/mplayer/`，用户配置文件位于`~/.mplayer/`。

`/etc/mplayer/` 下默认包含：

*   `codecs.conf` - 解码器配置文件.
*   `example.conf` - mplayer.conf 示例，要进行配置，需要安装之后将此示例文件复制为 mplayer.conf.
*   `input.conf` - 快捷键配置.

`~/.mplayer/` 下默认包含一个 *config* 文件.

参考 [MPlayer 配置示例](http://mplayerhq.hu/DOCS/man/en/mplayer.1.html#CONFIGURATION%20FILES) 和 `man mplayer`.

### 按键绑定

系统按键绑定通过 `/etc/mplayer/input.conf` 配置，个人按键绑定通过 `~/.mplayer/input.conf` 配。完整的键盘快捷键列表请阅读 `man mplayer`.

参阅：[XF86 键盘符号](http://wiki.linuxquestions.org/wiki/XF86_keyboard_symbols)

## 提示与技巧

### 继续之前的播放

To get this behavior, you can install the [mplayer-resumer](https://aur.archlinux.org/packages/mplayer-resumer/) package from the [AUR](/index.php/AUR "AUR"). The package contains a Perl wrapper script for MPlayer which will allow you to autoresume playback from the point it was last stopped.

To use it, simply call the wrapper script in place of MPlayer:

```
$ mplayer-resumer *options* *path/to/file*

```

If this script is restarted within a short amount of time after closing MPayer (default 5 seconds) then it will delete the file used to keep track of the videos resume position, effectively starting the video from the beginning.

If the video file to be played is on a read-only filesystem, or otherwise lives in a location that cannot be written to, resume will fail. This is because the current implementation uses a file parallel to the video file to store the timecode.

### 硬件加速

See [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

#### 启用 VDPAU

将下列内容加入前面提到过的配置文件（全局或用户配置文件均可）：

```
vo=vdpau,
vc=ffmpeg12vdpau,ffwmv3vdpau,ffvc1vdpau,ffh264vdpau,ffodivxvdpau,

```

**Note:**

*   The trailing commas are important! They tell MPlayer to fall back on other drivers and codecs should the specified ones not be found.
*   `-vo` option selects VDPAU video output driver, `-vc` option selects VDPAU video codecs.

**警告:** 只有最新型号的显卡支持ffodivxvdpau。如果你的不支持，可以删除。详情请查阅 [NVIDIA 页面](/index.php/NVIDIA#Pure_Video_HD "NVIDIA") 。

#### Enabling VA-API

This requires [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/) from the AUR.

 `$ mplayer -vo vaapi -va vaapi *foobar.mpeg*` 

*   **-vo** - Select vaapi video output driver
*   **-va** - Select vaapi video decoder driver

MPlayer based players:

*   [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer): To enable hardware acceleration: *Edit > Preferences > Player*, then set Video Output to `vaapi`.
*   [smplayer](https://www.archlinux.org/packages/?name=smplayer): To enable hardware acceleration: *Options > Preferences > General > Video*, then set Output driver to `vaapi`.

### Translucent video with Radeon cards and Composite enabled

To get translucent video output in X you have to enable textured video in MPlayer:

```
$ mplayer -vo xv:adaptor=1 *file*

```

Or add the following line to `~/.mplayer/config`:

```
vo=xv:adaptor=1

```

You can use `xvinfo` to check which video modes your graphic card supports.

### 播放流媒体文件

要播放流媒体（如*.asx文件)，使用以下命令：

```
$ mplayer -playlist link-to-stream.asx 

```

必须使用-playlist参数，因为这些文件是流媒体列表，而非影音文件。

### 播放DVD

To play a DVD with MPlayer:

```
$ mplayer dvd://*N*

```

where *N* is the desired title number. Start at 1 and work up if unsure. To start at a specific chapter use the '-chapter' flag. For example, adding '-chapter 5' to the command starts the dvd playing at chapter five of the title.

Mplayer checks `/dev/dvd` by default. Tell it to use `/dev/sr0` with the `dvd-device` option at the command line, or the `dvd-device` variable in `~/.mplayer/config`.

To play a DVD image file:

```
$ mplayer -dvd-device movie.iso dvd://*N*

```

To enable the DVD menu use:

```
$ mplayer dvdnav://

```

**Note:** You use arrow keys to navigate and the `Enter` key to choose.

To enable mouse support in DVD menus use:

```
$ mplayer -mouse-movements dvdnav://

```

To find the audio language, start MPlayer with the `-v` switch to output audio IDs. An audio track is selected with `-aid *audio_id*`. Set a default audio language by editing `~/.mplayer/config` and adding the line `alang=en` for English.

With MPlayer, the DVD could be set to a low volume. To increase the maximum volume to 400%, use `softvol=yes` and `softvol-max=400`. The startup volume defaults to 100% of software volume and the global mixer levels will remain untouched. Using the `9` and `0` keys, volume can be adjusted between 0 and 400 percent.

```
alang=en
softvol=yes
softvol-max=400

```

#### DVB-T Streaming

See [DVB-T](/index.php/DVB-T "DVB-T") for more info.

### JACK support

To have MPlayer audio output directed to [JACK](/index.php/JACK "JACK") as its default behavior, edit `~/.mplayer/config` and add:

```
ao=jack

```

If you do not have JACK running all the time, you can have MPlayer output to JACK on an as-needed basis by invoking MPlayer from the command line as such:

```
$ mplayer -ao jack *path/to/file*

```

### Advanced Subtitles

In order to get Advanced SubStation Alpha (ass) or SubStation Alpha (ssa) formatted subtitles to display properly you need to either edit `~/.mplayer/config` and add:

```
ass=true

```

or add -ass to the command line:

```
$ mplayer -ass *path/to/subtitledVideo.mkv*

```

One possible indication of needing to enable this flag is if you get numbers appearing with your subtitles. This is caused by the positioning information being interpreted as something to be displayed. Mplayer will also complain about subtitles being either too long or having too many lines.

Enabling `ass` also enables any embedded fonts. As per the note in the mplayer's man adding `embeddedfonts=true` is unneeded if [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) is version 2.4.2 or newer. Fontconfig will also be used to select which font to use when there are no embedded fonts. This may result in a different font being used than the OSD subtitle renderer.

### Internet radio

Here is an example of a script for an easy start/stop of playing a predefined radio station. [[1]](http://www.linuxforums.org/forum/miscellaneous/199396-mplayer-flash.html#post941062)

```
#!/bin/bash
XX="X"$1;
PLAYIT='mplayer  -loop 0 -playlist http://*.*.*.*:8000/listen.pls';

if [ "$XX" == "Xstop" ]; then
  killall mplayer;
else
  if [ 'EX' == 'EX'"$(pidof mplayer)" ]; then
    if [ "$UID" -ne 0 ]; then 
      nohup $PLAYIT &> /dev/null & disown;
    else 
      echo The "root" user is not allowed to run this script.
    fi
  else
    echo mplayer is already running by user: $(ps -eo user,comm | grep -i "mplayer"$ | sed 's/ mplayer/,/m') | sed "s/ ,$/./m";
  fi
fi

```

For more details on a running mplayer instance:

```
$ ps -eo pcpu,pid,user,comm | grep -i "mplayer"$ | sed  "s/ mplayer$//m"

```

## 问题处理

### 无法打开名称含空格的文件

打开名称含空格的文件时，如果报类似于“无法打开file:///The%20Movie”的错误（空格被替换成“%20”了），可以通过下面的方法解决：

打开`/usr/share/applications/mplayer.desktop`，修改下面的内容：

```
Exec=mplayer %U

```

为：

```
Exec=mplayer "%F"

```

如果要使用图形前端，修改为`Exec=gui_name "%F"`即可。

### MPlayer has black or strange colored font for OSD and Subtitles

There appears to be an issue with OSD and Subtitle colors when using vdpau output, which mplayer may be using by default. You can get around this issue by using xv instead of vdpau:

As a command line option:

```
mplayer -vo xv

```

Adding the following line to your `~/.mplayer/config` file:

```
vo=xv

```

See the original [forums thread](https://bbs.archlinux.org/viewtopic.php?pid=1379141) for details.

### Smplayer无图像

打开mp4和flv文件时，Smplayer可能出现无图像问题。解决方法如下： 打开`~/.mplayer/config`添加：

```
 [extension.mp4]
 demuxer=mov

```

如果还有问题，可能是由Smplayer原有设置导致的。删除设置文件即可：

```
 $ rm -rf ~/.config/smplayer/file_settings

```

### Transparent SMPlayer in Gnome with Composite enabled

Have you noticed the transparent screen of smplayer when you are using compiz and maybe cairo-dock? Well it’s ridiculous that when you open your videos using SMplayer you can just hear audio and no video! Here’s how you fix this: [copy paste into terminal]

```
   sudo bash -c "cat > /usr/bin/smplayer.helper" <<EOF
   export XLIB_SKIP_ARGB_VISUALS=1
   exec smplayer.real "$@"
   EOF
   sudo chmod 755 /usr/bin/smplayer.helper
   sudo mv /usr/bin/smplayer{,.real}
   sudo ln -sf smplayer.helper /usr/bin/smplayer

```

If you don’t use sudo then just use “su” to login as root and do the above!

### SMPlayer: OSD font too big / subtitle text too small

Since SMPlayer 0.8.2.1 (with MPlayer2 20121128-1), the ratio of the subtitle font to the OSD font is very strange. This can result in the OSD text filling the whole screen while the subtitles are very small and unreadable. This problem can be solved by adding:

```
-subfont-osd-scale 2

```

or to the extra options passed to MPlayer from SMPlayer. These options are found in *Options > Preferences > Advanced > Options for MPlayer*. This can also be achieved by adding the following line to `~/.mplayer/config`:

```
subfont-osd-scale=2

```

### Mplayer shows question marks for some characters on subtitle

If the codepage of the subtitles is utf8, try using:

```
-subcp utf8

```

You can find the codepage of the subtitles with:

```
file subtitles.srt

```

See [mplayer-shows-question-marks-for-some-characters-on-subtitle](http://www.linuxquestions.org/questions/slackware-14/mplayer-shows-question-marks-for-some-characters-on-subtitle-works-fine-on-xine-906077/).

### Choppy audio CD playback

CDDA playback may be interrupted every few seconds as the CDROM spins down the CD. To get around this you need to cache or buffer in advance using the `-cache` option:

```
mplayer cdda://:1 -cache 1024

```

The `:1` is to lower the CDROM speed for a constant spin and less noise.