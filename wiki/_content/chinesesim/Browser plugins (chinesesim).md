根据插件 API 的不同，浏览器的插件可以分为两种：

*   Netscape plugin API (NPAPI): 可以在 [Firefox](/index.php/Firefox "Firefox") 和一些浏览器中使用(**不能** 在 Chromium 和 Opera 中使用).
*   Pepper plugin API (PPAPI): 仅能在 [Chromium](/index.php/Chromium "Chromium")，Chrome 和 [Opera](/index.php/Opera "Opera") 中使用.

除非明确说明，本页中的插件都只支持 NPAPI。

## Contents

*   [1 Flash Player](#Flash_Player)
    *   [1.1 Adobe Flash Player](#Adobe_Flash_Player)
        *   [1.1.1 Installation](#Installation)
        *   [1.1.2 更新](#.E6.9B.B4.E6.96.B0)
        *   [1.1.3 配置](#.E9.85.8D.E7.BD.AE)
        *   [1.1.4 Disable the "Press ESC to exit full screen mode" message](#Disable_the_.22Press_ESC_to_exit_full_screen_mode.22_message)
        *   [1.1.5 Multiple monitor full-screen fix](#Multiple_monitor_full-screen_fix)
        *   [1.1.6 Playing DRM-protected content](#Playing_DRM-protected_content)
    *   [1.2 Shumway](#Shumway)
    *   [1.3 Gnash](#Gnash)
    *   [1.4 Lightspark](#Lightspark)
*   [2 PDF浏览器](#PDF.E6.B5.8F.E8.A7.88.E5.99.A8)
    *   [2.1 PDF.js](#PDF.js)
    *   [2.2 External PDF viewers](#External_PDF_viewers)
*   [3 中国的在线支付](#.E4.B8.AD.E5.9B.BD.E7.9A.84.E5.9C.A8.E7.BA.BF.E6.94.AF.E4.BB.98)
*   [4 Citrix](#Citrix)
*   [5 Java](#Java)
*   [6 Pipelight](#Pipelight)
*   [7 视频播放插件](#.E8.A7.86.E9.A2.91.E6.92.AD.E6.94.BE.E6.8F.92.E4.BB.B6)
    *   [7.1 其它插件](#.E5.85.B6.E5.AE.83.E6.8F.92.E4.BB.B6)
*   [8 其他](#.E5.85.B6.E4.BB.96)
    *   [8.1 Hangouts](#Hangouts)
    *   [8.2 MozPlugger](#MozPlugger)
    *   [8.3 kpartsplugin](#kpartsplugin)
*   [9 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [9.1 Flash无声音](#Flash.E6.97.A0.E5.A3.B0.E9.9F.B3)
    *   [9.2 Flash独占了声音设备](#Flash.E7.8B.AC.E5.8D.A0.E4.BA.86.E5.A3.B0.E9.9F.B3.E8.AE.BE.E5.A4.87)
    *   [9.3 Flash性能](#Flash.E6.80.A7.E8.83.BD)
    *   [9.4 Flash中webcam分辨率低](#Flash.E4.B8.ADwebcam.E5.88.86.E8.BE.A8.E7.8E.87.E4.BD.8E)
    *   [9.5 Black bars in fullscreen video playback on multiheaded desktops](#Black_bars_in_fullscreen_video_playback_on_multiheaded_desktops)
    *   [9.6 Flash Player: plugin version still shown older version after upgrade](#Flash_Player:_plugin_version_still_shown_older_version_after_upgrade)
    *   [9.7 插件安装后无法使用](#.E6.8F.92.E4.BB.B6.E5.AE.89.E8.A3.85.E5.90.8E.E6.97.A0.E6.B3.95.E4.BD.BF.E7.94.A8)
    *   [9.8 Gecko Media Player 无法播放 Apple Trailers](#Gecko_Media_Player_.E6.97.A0.E6.B3.95.E6.92.AD.E6.94.BE_Apple_Trailers)

## Flash Player

### Adobe Flash Player

#### Installation

不同的浏览器需要安装不同的插件。

*   NPAPI 插件可以通过软件包 [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) 进行 [安装](/index.php/%E5%AE%89%E8%A3%85 "安装")，[Adobe 曾表示要停止开发此插件](https://blogs.adobe.com/flashplayer/2012/02/adobe-and-google-partnering-for-flash-player-on-linux.html)，但是在2016年9月，Adobe 宣布将继续为其提供支持。

*   PPAPI 版本和 Google Chrome 一起发布. 详情参考 [Chromium#Flash Player plugin](/index.php/Chromium#Flash_Player_plugin "Chromium").

**Note:**

*   某些时候文本显示不太正常，可能需要从[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")安装[ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)
*   [freshplayerplugin-git](https://aur.archlinux.org/packages/freshplayerplugin-git/) 软件包提供了 NPAPI 浏览器比如 Firefox 使用 [pepper-flash](https://www.archlinux.org/packages/?name=pepper-flash) 的测试版本。可以通过将 `/usr/share/freshplayerplugin/freshwrapper.conf.example` 复制到 `/usr/share/freshplayerplugin/freshwrapper.conf` 配置硬件加速。

#### 更新

如果使用 [Firefox](/index.php/Firefox "Firefox")，请查阅 [此处的说明](/index.php/Firefox#Firefox_detects_the_wrong_version_of_my_plugin "Firefox").

#### 配置

To change the preferences (privacy settings, resource usage, etc.) of Flash Player, right click on any embedded Flash content (for instance [adobe's flash home](https://helpx.adobe.com/flash-player.html)) and choose *Settings* from the menu.

You can also use the Flash settings file `/etc/adobe/mms.cfg`. Gentoo has an extensively commented [example mms.cfg](http://sources.gentoo.org/cgi-bin/viewvc.cgi/gentoo-x86/www-plugins/adobe-flash/files/mms.cfg).

To enable video decoding with [hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration"), add/uncomment the following line:

```
EnableLinuxHWVideoDecode = 1

```

It might also be required to add/uncomment the following line:

```
OverrideGPUValidation = 1

```

#### Disable the "Press ESC to exit full screen mode" message

There is no solution other than patching the Flash plugin. Please note only the NPAPI plugin is supported. Install [flash-fullscreen-patcher](https://aur.archlinux.org/packages/flash-fullscreen-patcher/) which provides wine as a required dependency since the patch has been initially made for Windows.

After the package has been installed, backup `libflashplayer.so`:

```
# cp /usr/lib/mozilla/plugins/libflashplayer.so /usr/lib/mozilla/plugins/libflashplayer.so.backup 

```

Then, patch `libflashplayer.so`:

```
# flash-fullscreen-patcher.sh -f /usr/lib/mozilla/plugins/libflashplayer.so

```

If you use Firefox and want to remove the message *Press ESC to exit full screen mode in HTML5 videos* too, go to about:config and set `full-screen-api.warning.timeout` to `0`.

Alternatively, install Firefox extension [Disable HTML5 Fullscreen Alert](https://addons.mozilla.org/firefox/addon/disable-html5-fullscreen-alert/), which will suppress full screen warnings for HTML5 content.

#### Multiple monitor full-screen fix

When using a multiple monitor setup, or swapping between virtual desktops, it is possible to lose focus on a fullscreen flash window. In such a case, the adobe flash-plugin will automatically exit full-screen mode. This may not be to your liking.

Unfortunately, this behavior is hard coded into the binary. In order to change this behavior it is necessary to alter the binary.

Fixing this issue only works for the NPAPI plugin and this issue can be fixed via 2 ways.

*   Using the [flashplugin-focusfix](https://aur.archlinux.org/packages/flashplugin-focusfix/).

*   [Patching manually](http://www.webupd8.org/2012/10/ubuntu-multi-monitor-tweaks-full-screen.html):

	After the package has been installed, backup `libflashplayer.so`:

	 `# cp /usr/lib/mozilla/plugins/libflashplayer.so /usr/lib/mozilla/plugins/libflashplayer.so.backup` 

	Then, you will need to alter that file using a hex editor like [ghex](https://www.archlinux.org/packages/?name=ghex). You must open it with root privileges obviously.

	 `# ghex /usr/lib/mozilla/plugins/libflashplayer.so` 

	Using the hex editor find the string `_NET_ACTIVE_WINDOW`. In ghex the readable string is on the right hand side of the window, and the hex is on the left, you are trying to locate the readable string. It should be easy to find using a search function.

	Upon finding `_NET_ACTIVE_WINDOW` rewrite the line, but **do not** change the length of the line, for example `_NET_ACTIVE_WINDOW` becomes `_XET_ACTIVE_WINDOW`.

	Save the binary, and restart any processes using the plugin (as this will crash any instance of the plugin in use.)

#### Playing DRM-protected content

See [Flash DRM content](/index.php/Flash_DRM_content "Flash DRM content").

### Shumway

[Shumway](http://mozilla.github.io/shumway/) 尝试直接使用 HTML5 技术而不是本地代码处理和显示 SWF 文件。可以通过 [Mozilla's github.io 网页](http://mozilla.github.io/shumway/)直接安装. 根据 [Shumway wiki](https://github.com/mozilla/shumway/wiki), "如果实验成功，这个功能有机会整合进 Firef。"

Firefox Nightly/Aurora 编译版本包含了 Shumway.

### Gnash

参考 [Wikipedia:Gnash](https://en.wikipedia.org/wiki/Gnash "wikipedia:Gnash"). [GNU Gnash](http://www.gnu.org/software/gnash/) 是 Adobe Flash Player 的自由软件替代。可以作为单独的播放器，也可以嵌入浏览器。支持 SWF v7 和 80% 的 ActionScript 2.0。

可以通过软件包[gnash](https://aur.archlinux.org/packages/gnash/), [gnash-kde4](https://aur.archlinux.org/packages/gnash-kde4/), [gnash-git](https://aur.archlinux.org/packages/gnash-git/).

**Note:** 如果发现 Gnash 无法工作，可能需要先 [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [gstreamer0.10-ffmpeg](https://aur.archlinux.org/packages/gstreamer0.10-ffmpeg/).

### Lightspark

[Lightspark](http://lightspark.github.com/) is another attempt to provide a free alternative to Adobe Flash aimed at supporting newer Flash formats. Lightspark has the ability to fall back on Gnash for old content, which enables users to install both and enjoy wider coverage. Although it is still very much in development, it supports some [popular sites](https://github.com/lightspark/lightspark/wiki/Site-Support).

Lightspark can be [installed](/index.php/Install "Install") with the [lightspark-git](https://aur.archlinux.org/packages/lightspark-git/) package.

## PDF浏览器

### PDF.js

[PDF.js](https://github.com/mozilla/pdf.js) is a PDF renderer created by Mozilla and built using HTML5 technologies.

It is included in [Firefox](/index.php/Firefox "Firefox").

For [Chromium](/index.php/Chromium "Chromium") and Google Chrome it is available as extension in the [Chrome Web Store](https://chrome.google.com/webstore/detail/pdf-viewer/oemmndcbldboiebfnladdacbdfmadadm).

### External PDF viewers

To use an external PDF viewer you need [#MozPlugger](#MozPlugger) or [#kpartsplugin](#kpartsplugin).

If you want to use MozPlugger with Evince, for example, you have to find the lines containing `pdf` in the `/etc/mozpluggerrc` file and modify the corresponding line after `GV()` as below:

```
repeat noisy swallow(evince) fill: evince "$file"

```

(replace `evince` with something else if it is not your viewer of choice).

If this is not enough, you may need to change 2 values in `about:config`:

*   Change `pdfjs.disabled`'s value to *true*;
*   Change `plugin.disable_full_page_plugin_for_types`'s value to an empty value.

Restart and it should work like a charm!

## 中国的在线支付

中国的第三方在线支付网站通常采用所谓的“安全插件”来输入密码。这些 NPAPI 插件在 Firefox 52+ 中已不再支持，可以尝试使用 [palemoon](https://aur.archlinux.org/packages/palemoon/)

*   银联在线支付：[upeditor](https://aur.archlinux.org/packages/upeditor/)
*   支付宝：[aliedit](https://aur.archlinux.org/packages/aliedit/)

## Citrix

参见：[Citrix](/index.php/Citrix "Citrix")

## Java

**Note:** Both Java plugins are NPAPI-only and thus do not work in Chromium and Opera.

To enable [Java](/index.php/Java "Java") support in your browser, you have two options: the open-source [OpenJDK](https://en.wikipedia.org/wiki/OpenJDK "wikipedia:OpenJDK") (recommended) or Oracle's proprietary version. For details about why OpenJDK is recommended see [this](https://mailman.archlinux.org/pipermail/arch-general/2011-August/021671.html).

To use OpenJDK, you have to install the [IcedTea](http://icedtea.classpath.org/wiki/Main_Page) browser plugin, [icedtea-web](https://www.archlinux.org/packages/?name=icedtea-web).

If you want to use Oracle's JRE, install the [jre](https://aur.archlinux.org/packages/jre/) package.

See [Java#OpenJDK](/index.php/Java#OpenJDK "Java") for additional details and references.

**Note:** If you experience any problems with the Java plugin (e.g. it is not recognized by the browser), you can try this [solution](#Plugins_are_installed_but_not_working).

## Pipelight

See [Pipelight](/index.php/Pipelight "Pipelight").

## 视频播放插件

很多浏览器支持通过 [GStreamer](/index.php/GStreamer "GStreamer") 框架播放 HTML5 `<audio>` 和 `<video>`。安装时注意查看浏览器的可选依赖关系(或 [webkitgtk](https://aur.archlinux.org/packages/webkitgtk/)/[webkitgtk2](https://aur.archlinux.org/packages/webkitgtk2/) 依赖关系)确认支持的 GStreamer 版本，可能是当前 `gst-*` 版本或老的 `gstreamer0.10-*` 版本。详情参考 [GStreamer#Installation](/index.php/GStreamer#Installation "GStreamer").

### 其它插件

*   **Gecko 媒体播放器** — Mozilla 处理网页多媒体的插件，使用 MPlayer.

	[https://sites.google.com/site/kdekorte2/gecko-mediaplayer](https://sites.google.com/site/kdekorte2/gecko-mediaplayer) || [gecko-mediaplayer](https://www.archlinux.org/packages/?name=gecko-mediaplayer)

*   **GNOME Videos 插件** — 基于 [GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos") 媒体播放器的插件，使用 [GStreamer](/index.php/GStreamer "GStreamer").

	[https://wiki.gnome.org/Apps/Videos](https://wiki.gnome.org/Apps/Videos) || [totem](https://www.archlinux.org/packages/?name=totem)

*   **Rosa Media Player Plugin** — 基于 MPlayer 的 Qt 浏览器插件.

	[https://abf.rosalinux.ru/uxteam/ROSA_Media_Player](https://abf.rosalinux.ru/uxteam/ROSA_Media_Player) || [rosa-media-player-plugin](https://aur.archlinux.org/packages/rosa-media-player-plugin/)

*   **VLC Plugin** — NPAPI 接口，VLC 插件.

	[https://code.videolan.org/videolan/npapi-vlc](https://code.videolan.org/videolan/npapi-vlc) || [npapi-vlc](https://www.archlinux.org/packages/?name=npapi-vlc)

## 其他

### Hangouts

Hangouts plugin can be installed with the [google-talkplugin](https://aur.archlinux.org/packages/google-talkplugin/) package. Installing this plugin is not necessary for fresh version of chromium browser. Hangouts is a messenger by Google, that allows you to make video call between 15 people simultaneously. While using "new" version, you can share your screen with others like in Skype, but if you switch to "old" version, it will be possible to do the following things together: watching YouTube, making diagrams, editing documents, playing games and other things.

### MozPlugger

MozPlugger can be installed with the [mozplugger](https://aur.archlinux.org/packages/mozplugger/) package.

[MozPlugger](http://mozplugger.mozdev.org/) is a Mozilla plugin which can show many types of multimedia inside your browser. To accomplish this, it uses external programs such as MPlayer, xine, Evince, OpenOffice, TiMidity, etc. To modify or add applications to be used by MozPlugger just modify the `/etc/mozpluggerrc` file.

For example, MozPlugger uses OpenOffice by default to open `doc` files. To change it to use LibreOffice instead, look for the OpenOffice section:

 `/etc/mozpluggerrc` 
```
...
### OpenOffice
define([OO],[swallow(VCLSalFrame) fill: ooffice2.0 -nologo -norestore -view $1 "$file"
    swallow(VCLSalFrame) fill: ooffice -nologo -norestore -view $1 "$file"
    swallow(VCLSalFrame) fill: soffice -nologo $1 "$file"])
...

```

and add LibreOffice at the beginning of the list:

 `/etc/mozpluggerrc` 
```
...
### LibreOffice/OpenOffice
define([OO],[swallow(VCLSalFrame) fill: libreoffice --nologo --norestore --view $1 "$file"
    swallow(VCLSalFrame) fill: ooffice2.0 -nologo -norestore -view $1 "$file"
    swallow(VCLSalFrame) fill: ooffice -nologo -norestore -view $1 "$file"
    swallow(VCLSalFrame) fill: soffice -nologo $1 "$file"])
...

```

**Note:** Be sure to also choose LibreOffice as your preferred application to open `doc` files.

As another simple example, if you want to open `cpp` files with your favorite text editor (we will use Kate) to get syntax highlighting, just add a new section to your `mozpluggerrc` file:

 `/etc/mozpluggerrc` 
```
text/x-c++:cpp:C++ Source File
text/x-c++:hpp:C++ Header File
    repeat noisy swallow(kate) fill: kate -b "$file"

```

To change the default of MPlayer so that [mpv](/index.php/Mpv "Mpv") is used instead, change the appropriate lines such that:

 `/etc/mozpluggerrc` 
```
...
### MPlayer

#define(MP_CMD,[mplayer -really-quiet -nojoystick -nofs -zoom -vo xv,x11 -ao esd,alsa,oss,arts,null -osdlevel 0 $1 </dev/null])
define(MP_CMD,[mpv -really-quiet $1 </dev/null])

#define(MP_EMBED,[embed noisy ignore_errors: MP_CMD(-xy $width -wid $window $1)])
define(MP_EMBED,[embed noisy ignore_errors: MP_CMD(--autofit=$width -wid $window $1)])

#define(MP_NOEMBED,[noembed noisy ignore_errors maxaspect swallow(MPlayer): MP_CMD($1)])
define(MP_NOEMBED,[noembed noisy ignore_errors maxaspect swallow(mpv): MP_CMD($1)])

...

#define(MP_AUDIO,[mplayer -quiet -nojoystick $1 </dev/null])
define(MP_AUDIO,[mpv -really-quiet $1 </dev/null])

#define(MP_AUDIO_STREAM,[controls stream noisy ignore_errors: mplayer -quiet -nojoystick $1 "$file" </dev/null])
define(MP_AUDIO_STREAM,[controls stream noisy ignore_errors: mpv -really-quiet $1 "$file" </dev/null])
...
```

For a more complete list of MozPlugger options see [this page](http://www.linuxmanpages.com/man7/mozplugger.7.php).

### kpartsplugin

[The KParts plugin](http://www.unix-ag.uni-kl.de/~fischer/kpartsplugin/) is a plugin that uses KDE's KPart technology to embed different file viewers in the browser, such as Okular (for PDF), Ark (for different archives), Calligra Words (for ODF), etc. It cannot use applications that are not based on the KPart technology.

The KParts plugin can be installed with the package [kpartsplugin](https://www.archlinux.org/packages/?name=kpartsplugin).

## 疑难解答

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

### Flash性能

Adobe的Flash插件有严重的性能问题，尤其是在CPU使用自动降频功能时。参见：[cpufrequtils#Changing the ondemand governor's threshold](/index.php/Cpufrequtils#Changing_the_ondemand_governor.27s_threshold "Cpufrequtils")。

### Flash中webcam分辨率低

尝试使用如下命令启动浏览器：

```
$ LD_PRELOAD=/usr/lib/libv4l/v4l1compat.so [broswer]

```

### Black bars in fullscreen video playback on multiheaded desktops

The Flash plugin has a known bug where the full screen mode does not really work when you have a multi-monitor setup. Apparently, it incorrectly determines the full screen resolution, so the full screen Flash Player fills the correct monitor but gets scaled as if the monitor had the resolution of the total display area.

To fix this, you can use the "hack" described [here](http://al.robotfuzz.com/content/workaround-fullscreen-flash-linux-multiheaded-desktops). Simply download the source from the link given on the page, and follow the instructions in the README.

**Tip:** The hack is available and can be installed with the [fullscreenhack](https://aur.archlinux.org/packages/fullscreenhack/) package.

**Note:** While the author mentions using NVDIA's TwinView, the hack should work for any multi-monitor setup.

### Flash Player: plugin version still shown older version after upgrade

Solution for Firefox: delete file "pluginreg.dat" in user's profile directory.

*   Close firefox
*   Go to /home/<username>/.mozilla/firefox/<profile_folder>/
*   Delete file "pluginreg.dat"

Firefox will automatically rebuild this file once it is started again. Make sure to substitute <username> and <profile_folder> with the appropriate information.

### 插件安装后无法使用

这通常是因为第一次安装插件后，用户未重登录，插件路径还未设置。测试如下变量：

```
echo $MOZ_PLUGIN_PATH

```

若未设置，请尝试重新登录, 或:

```
$ source /etc/profile.d/mozilla-common.sh && firefox

```

### Gecko Media Player 无法播放 Apple Trailers

设置浏览器的用户代理（user agent）为：

```
QuickTime/7.6.2 (qtver=7.6.2;os=Windows NT 5.1Service Pack 3)

```