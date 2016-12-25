**翻译状态：** 本文是英文页面 [MPlayer](/index.php/MPlayer "MPlayer") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-12-23，点击[这里](https://wiki.archlinux.org/index.php?title=MPlayer&diff=0&oldid=454536)可以查看翻译后英文页面的改动。

[MPlayer](http://www.mplayerhq.hu/) 是 GNU/Linux 下非常流行的影音播放器，支持大多数文件格式，非常通用。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 图形前端](#.E5.9B.BE.E5.BD.A2.E5.89.8D.E7.AB.AF)
*   [3 浏览器整合](#.E6.B5.8F.E8.A7.88.E5.99.A8.E6.95.B4.E5.90.88)
    *   [3.1 Firefox 和 Chromium](#Firefox_.E5.92.8C_Chromium)
    *   [3.2 Konqueror](#Konqueror)
*   [4 配置](#.E9.85.8D.E7.BD.AE)
*   [5 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [5.1 启用 VDPAU （适用于新款nVidia显卡）](#.E5.90.AF.E7.94.A8_VDPAU_.EF.BC.88.E9.80.82.E7.94.A8.E4.BA.8E.E6.96.B0.E6.AC.BEnVidia.E6.98.BE.E5.8D.A1.EF.BC.89)
        *   [5.1.1 1\. 使用配置文件](#1._.E4.BD.BF.E7.94.A8.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
        *   [5.1.2 2\. 使用包装脚本](#2._.E4.BD.BF.E7.94.A8.E5.8C.85.E8.A3.85.E8.84.9A.E6.9C.AC)
    *   [5.2 Translucent Video with radeon and Composite enabled](#Translucent_Video_with_radeon_and_Composite_enabled)
    *   [5.3 Smplayer无图像](#Smplayer.E6.97.A0.E5.9B.BE.E5.83.8F)
    *   [5.4 Transparent SMPlayer in Gnome with Composite enabled](#Transparent_SMPlayer_in_Gnome_with_Composite_enabled)
    *   [5.5 播放流媒体文件](#.E6.92.AD.E6.94.BE.E6.B5.81.E5.AA.92.E4.BD.93.E6.96.87.E4.BB.B6)
    *   [5.6 启用dvdnav支持](#.E5.90.AF.E7.94.A8dvdnav.E6.94.AF.E6.8C.81)
    *   [5.7 使用jackd处理音频](#.E4.BD.BF.E7.94.A8jackd.E5.A4.84.E7.90.86.E9.9F.B3.E9.A2.91)
    *   [5.8 无法打开名称含空格的文件](#.E6.97.A0.E6.B3.95.E6.89.93.E5.BC.80.E5.90.8D.E7.A7.B0.E5.90.AB.E7.A9.BA.E6.A0.BC.E7.9A.84.E6.96.87.E4.BB.B6)
    *   [5.9 播放DVD](#.E6.92.AD.E6.94.BEDVD)

## 安装

*   [mplayer-vaapi](https://aur.archlinux.org/packages/mplayer-vaapi/): 启用 VAAPI 的版本
*   [mplayer2](https://aur.archlinux.org/packages/mplayer2/)：MPlayer 的一个分支。区别请参考 [MPlayer2 vs MPlayer](http://www.mplayer2.org/differences/).

[AUR](/index.php/AUR "AUR") 中的开发版本：

*   [mplayer-svn](https://aur.archlinux.org/packages/mplayer-svn/)
*   [mplayer2-git](https://aur.archlinux.org/packages/mplayer2-git/)

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

## 提示与技巧

### 启用 VDPAU （适用于新款nVidia显卡）

[此表](https://en.wikipedia.org/wiki/PureVideo#Table_of_PureVideo_.28HD.29_GPUs "wikipedia:PureVideo")列举了支持VDPAU的显卡。启用VDPAU前，首先需要安装*nvidia*驱动。启用VDPAU方法有二：

#### 1\. 使用配置文件

将下列内容加入前面提到过的配置文件（全局或用户配置文件均可）：

```
vo=vdpau,
vc=ffmpeg12vdpau,ffwmv3vdpau,ffvc1vdpau,ffh264vdpau,ffodivxvdpau,

```

**注意:** 务必添加最后的逗号！

**警告:** 只有最新型号的显卡支持ffodivxvdpau。如果你的不支持，可以删除。

#### 2\. 使用包装脚本

[AUR](/index.php/AUR "AUR")中的[mplayer-vdpau-auto](https://aur.archlinux.org/packages/mplayer-vdpau-auto/)提供了探测VDPAU支持并自动启用的脚本。

### Translucent Video with radeon and Composite enabled

To get translucent video output in X you have to enable textured video in mplayer:

```
$ mplayer -vo xv:adaptor=1 <File>

```

Or add the following line to `~/.mplayer/config`:

```
vo=xv:adaptor=1

```

You can use xvinfo to check which video modes your graphic card supports.

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

### 播放流媒体文件

要播放流媒体（如*.asx文件)，使用以下命令：

```
$ mplayer -playlist link-to-stream.asx 

```

必须使用-playlist参数，因为这些文件是流媒体列表，而非影音文件。

### 启用dvdnav支持

要启用dvdnav以使用DVD菜单，使用下列命令格式：

```
$ mplayer -nocache dvdnav://

```

### 使用jackd处理音频

打开`~/.mplayer/config`，添加：

```
ao=jack

```

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

### 播放DVD

```
mplayer -dvd-device <设备路径>（仅用于 DVD）
# 只播放第 3 标题：
mplayer -dvd-device /dev/dvd dvd://3 
# 只播放第 4 标题：
mplayer -dvd-device /dev/sr0 dvd://4

```