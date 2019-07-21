相关文章

*   [mpv](/index.php/Mpv "Mpv")

**翻译状态：** 本文是英文页面 [MPlayer](/index.php/MPlayer "MPlayer") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-11-24，点击[这里](https://wiki.archlinux.org/index.php?title=MPlayer&diff=0&oldid=550300)可以查看翻译后英文页面的改动。

[MPlayer](http://www.mplayerhq.hu/) 是 GNU/Linux 下非常流行的影音播放器，支持绝大多数视频/音频文件格式，非常通用。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 图形前端](#图形前端)
*   [3 配置](#配置)
    *   [3.1 按键绑定](#按键绑定)
*   [4 提示与技巧](#提示与技巧)
    *   [4.1 继续之前的播放](#继续之前的播放)
    *   [4.2 硬件加速](#硬件加速)
        *   [4.2.1 启用 VDPAU](#启用_VDPAU)
        *   [4.2.2 启用 VA-API](#启用_VA-API)
    *   [4.3 Radeon 显卡启用半透明视频混合显示](#Radeon_显卡启用半透明视频混合显示)
    *   [4.4 播放流媒体文件](#播放流媒体文件)
    *   [4.5 播放DVD](#播放DVD)
        *   [4.5.1 DVB-T Streaming](#DVB-T_Streaming)
    *   [4.6 JACK support](#JACK_support)
    *   [4.7 Advanced Subtitles](#Advanced_Subtitles)
    *   [4.8 Internet radio](#Internet_radio)
*   [5 问题处理](#问题处理)
    *   [5.1 无法打开名称含空格的文件](#无法打开名称含空格的文件)
    *   [5.2 MPlayer has black or strange colored font for OSD and Subtitles](#MPlayer_has_black_or_strange_colored_font_for_OSD_and_Subtitles)
    *   [5.3 Smplayer无图像](#Smplayer无图像)
    *   [5.4 Transparent SMPlayer in Gnome with Composite enabled](#Transparent_SMPlayer_in_Gnome_with_Composite_enabled)
    *   [5.5 SMPlayer: OSD font too big / subtitle text too small](#SMPlayer:_OSD_font_too_big_/_subtitle_text_too_small)
    *   [5.6 Mplayer shows question marks for some characters on subtitle](#Mplayer_shows_question_marks_for_some_characters_on_subtitle)
    *   [5.7 Choppy audio CD playback](#Choppy_audio_CD_playback)
*   [6 参阅](#参阅)

## 安装

[安装](/index.php/Install "Install") 软件包 [mplayer](https://www.archlinux.org/packages/?name=mplayer) 或它的开发版本 [mplayer-svn](https://aur.archlinux.org/packages/mplayer-svn/) 。

定制版：

*   **MPlayer-VAAPI** — 支持 VAAPI 的版本

	[http://gitorious.org/vaapi/mplayer](http://gitorious.org/vaapi/mplayer) || [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/)

*   **MPlayer2** — MPlayer 的分支

	[https://github.com/nezumisama/mplayer2](https://github.com/nezumisama/mplayer2) || [mplayer2](https://aur.archlinux.org/packages/mplayer2/)

**注意:** *mplayer2* 的开发已经停止，推荐使用 [mpv](/index.php/Mpv "Mpv")，mpv 更注重速度和开发质量，尽管它对老旧设备兼容性差。使用前请注意一下它们的 [差异](https://github.com/mpv-player/mpv/blob/master/DOCS/mplayer-changes.rst)。

## 图形前端

参考 [List of applications/Multimedia#MPlayer-based](/index.php/List_of_applications/Multimedia#MPlayer-based "List of applications/Multimedia").

## 配置

系统全局配置文件位于`/etc/mplayer/`，用户配置文件位于`~/.mplayer/`。

`/etc/mplayer/` 下默认包含：

*   `codecs.conf` - 解码器配置文件。
*   `example.conf` - mplayer.conf 不会在安装时自动创建，这是其示例文件。
*   `input.conf` - 快捷键配置文件。

`~/.mplayer/` 下默认包含一个 *config* 文件。

参考 [MPlayer 配置示例](http://mplayerhq.hu/DOCS/man/en/mplayer.1.html#CONFIGURATION%20FILES) 和 [mplayer(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mplayer.1)。

### 按键绑定

系统按键绑定通过 `/etc/mplayer/input.conf` 配置，个人按键绑定通过 `~/.mplayer/input.conf` 配。完整的键盘快捷键列表请阅读 [mplayer(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mplayer.1)。

参阅：[XF86 键盘符号](http://wiki.linuxquestions.org/wiki/XF86_keyboard_symbols)

## 提示与技巧

### 继续之前的播放

为了获得这个功能, 你可以到 [AUR](/index.php/AUR "AUR") 下载[mplayer-resumer](https://aur.archlinux.org/packages/mplayer-resumer/) 软件包。这个软件包包含一个Perl脚本，使你可以从上一次的播放记录继续播放。

To use it, simply call the wrapper script in place of MPlayer:

```
$ mplayer-resumer *options* *path/to/file*

```

If this script is restarted within a short amount of time after closing MPayer (default 5 seconds) then it will delete the file used to keep track of the videos resume position, effectively starting the video from the beginning.

If the video file to be played is on a read-only filesystem, or otherwise lives in a location that cannot be written to, resume will fail. This is because the current implementation uses a file parallel to the video file to store the timecode.

### 硬件加速

参考 [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

#### 启用 VDPAU

将下列内容加入前面提到过的配置文件（全局或用户配置文件均可）：

```
vo=vdpau,
vc=ffmpeg12vdpau,ffwmv3vdpau,ffvc1vdpau,ffh264vdpau,ffodivxvdpau,

```

**Note:**

*   The trailing commas are important! They tell MPlayer to fall back on other drivers and codecs should the specified ones not be found.
*   `-vo` option selects VDPAU video output driver, `-vc` option selects VDPAU video codecs.

**警告:** 只有最新型号的显卡支持ffodivxvdpau。如果你的不支持，可以删除。详情请查阅 [NVIDIA#VDPAU](/index.php/NVIDIA#VDPAU "NVIDIA")。

#### 启用 VA-API

This requires [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/) from the AUR.

 `$ mplayer -vo vaapi -va vaapi *foobar.mpeg*` 

*   **-vo** - Select vaapi video output driver
*   **-va** - Select vaapi video decoder driver

MPlayer based players:

*   [gnome-mplayer](https://www.archlinux.org/packages/?name=gnome-mplayer): To enable hardware acceleration: *Edit > Preferences > Player*, then set Video Output to `vaapi`.
*   [smplayer](https://www.archlinux.org/packages/?name=smplayer): To enable hardware acceleration: *Options > Preferences > General > Video*, then set Output driver to `vaapi`.

### Radeon 显卡启用半透明视频混合显示

为了在 X 中获得半透明视频效果，你需要在MPlayer中启用视频纹理:

```
$ mplayer -vo xv:adaptor=1 *file*

```

或者在 `~/.mplayer/config` 中添加一行:

```
vo=xv:adaptor=1

```

你可以使用 `xvinfo` 命令检查你的显卡支持那种视频模式。

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
Exec=mplayer %U

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

## 参阅

*   [MPlayer FAQ](https://wiki.multimedia.cx/index.php?title=MPlayer_FAQ)
*   [MPlayer tips](https://help.ubuntu.com/community/MPlayerTips)
*   [How to configure MPlayer](http://how-to.wikia.com/wiki/How_to_configure_MPlayer)
*   [playerctl](https://github.com/acrisci/playerctl): A command-line utility and library for controlling media players