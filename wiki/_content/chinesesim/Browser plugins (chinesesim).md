根据插件 API 的不同，浏览器的插件可以分为两种：

*   Netscape plugin API (NPAPI): 可以在 [Firefox](/index.php/Firefox "Firefox") 和一些浏览器中使用(**不能** 在 Chromium 和 Opera 中使用).
*   Pepper plugin API (PPAPI): 仅能在 [Chromium](/index.php/Chromium "Chromium")，Chrome 和 [Opera](/index.php/Opera "Opera") 中使用.

除非明确说明，本页中的插件都只支持 NPAPI。

## Contents

*   [1 Flash Player](#Flash_Player)
    *   [1.1 Adobe Flash Player](#Adobe_Flash_Player)
        *   [1.1.1 Installation](#Installation)
    *   [1.2 Gnash](#Gnash)
*   [2 PDF浏览器](#PDF.E6.B5.8F.E8.A7.88.E5.99.A8)
    *   [2.1 Evince](#Evince)
    *   [2.2 Adobe Reader](#Adobe_Reader)
        *   [2.2.1 32位（i686）](#32.E4.BD.8D.EF.BC.88i686.EF.BC.89)
        *   [2.2.2 64位（x86_64）](#64.E4.BD.8D.EF.BC.88x86_64.EF.BC.89)
*   [3 Citrix](#Citrix)
*   [4 Java](#Java)
    *   [4.1 IcedTea](#IcedTea)
    *   [4.2 Weird symlink](#Weird_symlink)
*   [5 视频播放插件](#.E8.A7.86.E9.A2.91.E6.92.AD.E6.94.BE.E6.8F.92.E4.BB.B6)
    *   [5.1 Gecko Media Player](#Gecko_Media_Player)
    *   [5.2 Totem Plugin](#Totem_Plugin)
*   [6 其他](#.E5.85.B6.E4.BB.96)
    *   [6.1 Mozplugger](#Mozplugger)
*   [7 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [7.1 Flash独占了声音设备](#Flash.E7.8B.AC.E5.8D.A0.E4.BA.86.E5.A3.B0.E9.9F.B3.E8.AE.BE.E5.A4.87)
    *   [7.2 Flash无声音](#Flash.E6.97.A0.E5.A3.B0.E9.9F.B3)
    *   [7.3 Flash性能](#Flash.E6.80.A7.E8.83.BD)
    *   [7.4 插件安装后无法使用](#.E6.8F.92.E4.BB.B6.E5.AE.89.E8.A3.85.E5.90.8E.E6.97.A0.E6.B3.95.E4.BD.BF.E7.94.A8)
    *   [7.5 Gecko Media Player 无法播放 Apple Trailers](#Gecko_Media_Player_.E6.97.A0.E6.B3.95.E6.92.AD.E6.94.BE_Apple_Trailers)
    *   [7.6 Flash中webcam分辨率低](#Flash.E4.B8.ADwebcam.E5.88.86.E8.BE.A8.E7.8E.87.E4.BD.8E)
    *   [7.7 Black bars in fullscreen video playback on multiheaded desktops](#Black_bars_in_fullscreen_video_playback_on_multiheaded_desktops)

## Flash Player

### Adobe Flash Player

#### Installation

不同的浏览器需要安装不同的插件。

*   NPAPI 插件可以通过软件包 [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) 进行 [安装](/index.php/%E5%AE%89%E8%A3%85 "安装")，[Adobe 已经停止开发此插件](https://blogs.adobe.com/flashplayer/2012/02/adobe-and-google-partnering-for-flash-player-on-linux.html)，版本固定到 11.2 但是会提供 5 年安全支持，直到 2017 年 3 月.[[1]](https://blogs.adobe.com/flashplayer/2012/02/adobe-and-google-partnering-for-flash-player-on-linux.html)[[2]](http://helpx.adobe.com/flash-player/release-note/release-notes-developer-flash-player.html)).

*   PPAPI 版本和 Google Chrome 一起发布. 详情参考 [Chromium#Flash Player plugin](/index.php/Chromium#Flash_Player_plugin "Chromium").

**Note:**

*   某些时候文本显示不太正常，可能需要从[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")安装[ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)
*   [freshplayerplugin-git](https://aur.archlinux.org/packages/freshplayerplugin-git/) 软件包提供了 NPAPI 浏览器比如 Firefox 使用 [chromium-pepper-flash](https://aur.archlinux.org/packages/chromium-pepper-flash/) 的测试版本。可以通过将 `/usr/share/freshplayerplugin/freshwrapper.conf.example` 复制到 `/usr/share/freshplayerplugin/freshwrapper.conf` 配置硬件加速。

### Gnash

参考 [Wikipedia:Gnash](https://en.wikipedia.org/wiki/Gnash "wikipedia:Gnash"). [GNU Gnash](http://www.gnu.org/software/gnash/) 是 Adobe Flash Player 的自由软件替代。可以作为单独的播放器，也可以嵌入浏览器。支持 SWF v7 和 80% 的 ActionScript 2.0。

可以通过软件包[gnash](https://aur.archlinux.org/packages/gnash/), [gnash-kde4](https://aur.archlinux.org/packages/gnash-kde4/), [gnash-git](https://aur.archlinux.org/packages/gnash-git/).

**Note:** 如果发现 Gnash 无法工作，可能需要先 [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [gstreamer0.10-ffmpeg](https://www.archlinux.org/packages/?name=gstreamer0.10-ffmpeg).

## PDF浏览器

### Evince

Firefox中现已可以直接打开PDF

### Adobe Reader

由于许可证问题，官方软件仓库不能提供 Adobe Reader。但在[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")中可以找到这些包。

[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")中亦提供了多语言支持包[localizations](https://aur.archlinux.org/packages.php?O=0&K=acroread-&do_Search=Go)。

#### 32位（i686）

32位安装包：[acroread](https://aur.archlinux.org/packages/acroread/)。

该包也提供Firefox插件。硬件渲染功能在Linux平台貌似不可用。

第三方软件仓库提供了预编译版本。打开`/etc/pacman.conf`，添加如下内容：

```
[archlinuxfr]
Server = [http://repo.archlinux.fr/i686](http://repo.archlinux.fr/i686)

```

然后更新软件信息，并安装Adobe Reader：

```
# pacman -Syu acroread

```

#### 64位（x86_64）

Adobe Reader是闭源软件。除非官方提供支持，否则我们无法使用原生64位版本。

作为代替，可以安装[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")中的[acroread](https://aur.archlinux.org/packages/acroread/)，并使用32位软件库。该包的可选依赖也最好一并安装。注意该包的Firefox插件无法在64位浏览器直接使用。要使用插件，安装[nspluginwrapper](https://www.archlinux.org/packages/?name=nspluginwrapper)，然后以普通用户身份执行：

```
$ nspluginwrapper -v -a -i

```

## Citrix

参见：[Citrix](/index.php/Citrix "Citrix")

## Java

### IcedTea

```
# pacman -S icedtea-web-java7

```

### Weird symlink

开源和闭源[Java](/index.php/Java "Java")软件包都提供了浏览器插件支持。官方仓库提供了开源版本：

```
# pacman -S jre7-openjdk

```

[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")中有闭源版本：[jre](https://aur.archlinux.org/packages/jre/)。

两个版本不能同时使用。开源版本目前已经相当完美，无需刻意使用闭源版本。闭源版本有个小问题，由于从Firefox3.6开始，浏览器不再从`/usr/lib/mozilla/plugins`查找插件，而jre插件默认安装在这里，需要调整一下：

```
# ln -s /opt/java/jre/lib/i386/libnpjp2.so ~/mozilla/plugins/libnpjp2.so

```

## 视频播放插件

### Gecko Media Player

mplayer用户可以使用该插件：

```
# pacman -S gecko-mediaplayer

```

### Totem Plugin

gstreamer用户可以使用该插件：

```
# pacman -S totem-plugin

```

## 其他

### Mozplugger

从[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")安装[mozplugger](https://aur.archlinux.org/packages/mozplugger/)。

## 疑难解答

### Flash独占了声音设备

如果发现播放Flash时其他程序无法正常播放声音，那么可能是由于没有加载`snd_pcm_oss`模块：

```
$ lsmod | grep snd_pcm_oss

```

重新加载：

```
# rmmod snd_pcm_oss

```

并重启浏览器即可。

### Flash无声音

Flash Player只通过默认的ALSA设备输出音频（编号0）。如果使用多个声音设备（比如，除了声卡外，使用了显卡的HDMI输出），可能你要使用的声音设备编号不是0，从而导致Flash无声音。

例如：

```
$ aplay -l
**** List of PLAYBACK Hardware Devices ****
card 0: Generic [HD-Audio Generic], device 3: HDMI 0 [HDMI 0]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: DX [Xonar DX], device 0: Multichannel [Multichannel]
  Subdevices: 0/1
  Subdevice #0: subdevice #0
card 1: DX [Xonar DX], device 1: Digital [Digital]
  Subdevices: 1/1
  Subdevice #0: subdevice #0

```

上面的示例中，HDMI设备编号为0，而声卡编号为1。要将该声卡作为ALSA默认输入，创建`~/.asoundrc`，内容如下：

```
pcm.!default {
type hw
card 1
}

ctl.!default {
type hw
card 1
}

```

### Flash性能

Adobe的Flash插件有严重的性能问题，尤其是在CPU使用自动降频功能时。参见：[cpufrequtils#Changing the ondemand governor's threshold](/index.php/Cpufrequtils#Changing_the_ondemand_governor.27s_threshold "Cpufrequtils")。

### 插件安装后无法使用

这通常是因为第一次安装插件后，用户未重登录，插件路径还未设置。测试如下变量：

```
echo $MOZ_PLUGIN_PATH

```

若未设置，请尝试重新登录。

### Gecko Media Player 无法播放 Apple Trailers

设置浏览器的用户代理（user agent）为：

```
QuickTime/7.6.2 (qtver=7.6.2;os=Windows NT 5.1Service Pack 3)

```

### Flash中webcam分辨率低

尝试使用如下命令启动浏览器：

```
LD_PRELOAD=/usr/lib/libv4l/v4l1compat.so chromium

```

### Black bars in fullscreen video playback on multiheaded desktops

Follow the instructions on this page: [link](http://al.robotfuzz.com/content/workaround-fullscreen-flash-linux-multiheaded-desktops)