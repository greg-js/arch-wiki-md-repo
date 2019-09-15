Related articles

*   [PulseAudio/Examples](/index.php/PulseAudio/Examples "PulseAudio/Examples")
*   [PulseAudio/Troubleshooting](/index.php/PulseAudio/Troubleshooting "PulseAudio/Troubleshooting")

**翻译状态：** 本文是英文页面 [PulseAudio](/index.php/PulseAudio "PulseAudio") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-01-26，点击[这里](https://wiki.archlinux.org/index.php?title=PulseAudio&diff=0&oldid=349898)可以查看翻译后英文页面的改动。

[PulseAudio](https://en.wikipedia.org/wiki/PulseAudio "wikipedia:PulseAudio") 是在[GNOME](/index.php/GNOME "GNOME") 或 [KDE](/index.php/KDE "KDE")等桌面环境中广泛使用的音频服务。它在内核音频组件（比如[ALSA](/index.php/ALSA "ALSA") 和 [OSS](/index.php/OSS "OSS")）和应用程序之间充当代理的角色。由于Arch Linux默认包含ALSA，PulseAudio经常和ALSA协同使用。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
    *   [1.1 前端](#前端)
*   [2 配置](#配置)
*   [3 启动](#启动)
    *   [3.1 在不支持的桌面环境中自动启动Pulse](#在不支持的桌面环境中自动启动Pulse)
*   [4 后端设置](#后端设置)
    *   [4.1 ALSA](#ALSA)
        *   [4.1.1 在不独占硬件设备的情况下使用ALSA/dmix](#在不独占硬件设备的情况下使用ALSA/dmix)
    *   [4.2 OSS](#OSS)
        *   [4.2.1 ossp](#ossp)
        *   [4.2.2 padsp wrapper](#padsp_wrapper)
    *   [4.3 GStreamer](#GStreamer)
    *   [4.4 OpenAL](#OpenAL)
    *   [4.5 libao](#libao)
*   [5 均衡器](#均衡器)
    *   [5.1 加载均衡器通道和dbus协议模块](#加载均衡器通道和dbus协议模块)
    *   [5.2 安装并运行图形前端](#安装并运行图形前端)
    *   [5.3 每次启动时加载均衡器和dbus模块](#每次启动时加载均衡器和dbus模块)
*   [6 应用程序](#应用程序)
    *   [6.1 QEMU](#QEMU)
    *   [6.2 AlsaMixer.app](#AlsaMixer.app)
    *   [6.3 XMMS2](#XMMS2)
    *   [6.4 KDE Plasma Workspaces 和 Qt4](#KDE_Plasma_Workspaces_和_Qt4)
    *   [6.5 Audacious](#Audacious)
    *   [6.6 Java/OpenJDK 6](#Java/OpenJDK_6)
    *   [6.7 Music Player Daemon (MPD)](#Music_Player_Daemon_(MPD))
    *   [6.8 MPlayer](#MPlayer)
    *   [6.9 guvcview](#guvcview)
*   [7 故障排查](#故障排查)
*   [8 相关阅读](#相关阅读)

## 安装

安装 [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) 。

有的 PulseAudio 模块已经从主软件包中 [分离](https://www.archlinux.org/news/pulseaudio-split/) 了。如果需要的话请分别安装：

*   [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth): 蓝牙 (Bluez) 支持
*   [pulseaudio-equalizer](https://www.archlinux.org/packages/?name=pulseaudio-equalizer): 均衡器 接收器 (qpaeq)
*   [pulseaudio-gconf](https://www.archlinux.org/packages/?name=pulseaudio-gconf): GConf 支持 (paprefs)
*   [pulseaudio-jack](https://www.archlinux.org/packages/?name=pulseaudio-jack): JACK 接收器, 源和jackdbus检测
*   [pulseaudio-lirc](https://www.archlinux.org/packages/?name=pulseaudio-lirc): 红外 (LIRC) 音量控制
*   [pulseaudio-xen](https://www.archlinux.org/packages/?name=pulseaudio-xen): Xen 半虚拟化接收器
*   [pulseaudio-zeroconf](https://www.archlinux.org/packages/?name=pulseaudio-zeroconf): Zeroconf (Avahi/DNS-SD) 支持

**Note:** 用户可能在 [ALSA](/index.php/ALSA "ALSA") 和 PulseAudio 之间产生混淆。ALSA 包括有着声卡驱动的Linux内核组件和用户空间组件两部分，`libalsa`.[[1]](http://www.alsa-project.org/main/index.php/Download) PulseAudio 只依赖于内核组件,但是也通过 [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa) 和 `libalsa` 实现了兼容。[[2]](http://www.freedesktop.org/wiki/Software/PulseAudio/FAQ/#index14h3)

### 前端

有多种前端工具可以用以控制 PulseAudio 守护进程：

*   GTK GUI：[paprefs](https://www.archlinux.org/packages/?name=paprefs) 和 [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol)
*   按键音量控制: [pulseaudio-ctl](https://aur.archlinux.org/packages/pulseaudio-ctl/)，[pavolume-git](https://aur.archlinux.org/packages/pavolume-git/)
*   控制台 (CLI)混合器：[ponymix](https://www.archlinux.org/packages/?name=ponymix)和[pamixer](https://www.archlinux.org/packages/?name=pamixer)
*   控制台 (curses) 混合器：[pulsemixer](https://www.archlinux.org/packages/?name=pulsemixer)
*   网页音量控制：[PaWebControl](https://github.com/Siot/PaWebControl)
*   系统托盘图标：[pasystray](https://www.archlinux.org/packages/?name=pasystray)，[pasystray-git](https://aur.archlinux.org/packages/pasystray-git/)
*   KF5 plasma 程序：[kmix](https://www.archlinux.org/packages/?name=kmix)和[plasma-pa](https://www.archlinux.org/packages/?name=plasma-pa)
*   如果你想通过 PulseAudio 使用蓝牙耳机或其他蓝牙音频设备的话，请参见[Bluetooth headset](/index.php/Bluetooth_headset "Bluetooth headset").

## 配置

Pulseaudio 支持通过多种模块扩展其功能。在这里可以找到PulseAudio可用的模块的详细信息： [Pulseaudio Loadable Modules](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Modules/)。增加 `load-module <module-name-from-list>` 到文件 `/etc/pulse/default.pa`就可以启用对应的模块。

## 启动

**Warning:** 如果你给每个用户拷贝了配置文件（例如`client.conf`, `daemon.conf` 或者 `default.pa`）到`~/.config/pulse/` 或者 `~/.pulse/`目录下，确定这些文件的修改与`/etc/pulse/`下的文件修改同步，否则PulseAudio可能由于配置文件错误而拒绝启动。

**Note:** 大多数X11环境会在启动X11会话时自动启动PulseAudio。

少数情况下PulseAudio在启动X11时没有自动启动，可运行下面的命令启动：

```
$ pulseaudio --start

```

运行下面的命令可以终止PulseAudio：

```
$ pulseaudio --kill

```

### 在不支持的桌面环境中自动启动Pulse

**Note:** 正如之前所说, 如果用户安装了桌面环境，PulseAudio很可能通过 `/etc/X11/xinit/xinitrc.d/pulseaudio`文件或者 `/etc/xdg/autostart/`目录下的文件自动启动

查看PulseAudio是否正在运行：

 `$ pgrep -af pulseaudio` 
```
369 /usr/bin/pulseaudio

```

如果PulseAudio未运行而且用户正在使用X11，运行下面的命令可以在启动PulseAudio的同时加载需要的X11插件：

```
$ start-pulseaudio-x11

```

如果你没有运行GNOME, KDE或者Xfce，并且你的`~/.xinitrc`文件并未引用`/etc/X11/xinit/xinitrc.d`目录下的文件内容，为了让PulseAudio自动启动，你可以这样做：

 `~/.xinitrc` 
```
/usr/bin/start-pulseaudio-x11

```

## 后端设置

### ALSA

从[official repositories](/index.php/Official_repositories "Official repositories")安装[pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa)，这个软件包包含了配置ALSA与PulseAudio共同工作必须的文件`/etc/asound.conf`。

如果你需要在x86_64系统上运行32位程序（比如Wine，Skype和Steam），也需要安装[lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse)和[lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins)

为了防止应用程序使用ALSA的OSS模拟功能而忽略PulseAudio（从而导致其他应用程序无法播放声音），确定`snd_pcm_oss`模块没有在系统启动时自动加载。如果该模块已经被加载(`lsmod | grep oss`)，运行下面命令以卸载该模块：

```
# rmmod snd_pcm_oss

```

#### 在不独占硬件设备的情况下使用ALSA/dmix

**Note:** 本段描述了备选的设置方案，一般不推荐这么做

你可能希望在大多数程序里直接使用ALSA，并且同时能正常运行依赖于PulseAudio的程序。以下步骤允许PulseAudio以dmix为后端，而不是独占ALSA硬件设备：

*   移除[pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa)软件包，该软件包提供了ALSA程序和PulseAudio之间的兼容层。移除后ALSA程序将直接使用ALSA而不是被Pulse接管。
*   编辑 `/etc/pulse/default.pa`.

	找到并取消与加载后端驱动相关的行的注释符号。按照下面的范例增加"device"参数。然后注释掉与加载自动检测模块相关的行。

```
load-module module-alsa-sink **device=dmix**
load-module module-alsa-source **device=dsnoop**
# load-module module-udev-detect
# load-module module-detect

```

*   *Optional:* 如果你使用 [kdemultimedia-kmix](https://www.archlinux.org/packages/?name=kdemultimedia-kmix) 你可能希望控制ALSA音量而不是PulseAudio音量：

```
$ echo export KMIX_PULSEAUDIO_DISABLE=1 > ~/.kde4/env/kmix_disable_pulse.sh
$ chmod +x ~/.kde4/env/kmix_disable_pulse.sh

```

*   现在，重启系统，试试同时运行ALSA应用程序和PulseAudio应用程序。两者应该能同时发声了。

	你可以使用 [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) 控制 PulseAudio 音量。

### OSS

有多种方法可以使只支持OSS的程序通过PulseAudio输出音频：

#### ossp

安装[ossp](https://www.archlinux.org/packages/?name=ossp) 并启动 `osspd.service`服务。

#### padsp wrapper

使用OSS的程序可以通过padsp（包含在PulseAudio中）启动，从而与PulseAudio兼容：

```
$ padsp OSSprogram

```

一些例子：

```
$ padsp aumix
$ padsp sox foo.wav -t ossdsp /dev/dsp

```

你可以像下面这样编写一个程序启动脚本：

 `/usr/local/bin/OSSProgram` 
```
#!/bin/sh
exec padsp /usr/bin/OSSprogram "$@"

```

确定**PATH**环境变量中`/usr/local/bin` 在 `/usr/bin`之前。

### GStreamer

安装 [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good)。如果程序使用的是旧版本的Gstreamer，安装[gstreamer0.10-good-plugins](https://aur.archlinux.org/packages/gstreamer0.10-good-plugins/)。

### OpenAL

OpenAL程序默认就应该使用PulseAudio了，但是可以明确指定其使用PulseAudio：

 `/etc/openal/alsoft.conf`  `drivers=pulse,alsa` 

### libao

编辑libao配置文件：

 `/etc/libao.conf`  `default_driver=pulse` 

一定要移除alsa驱动的`dev=default`选项，或者编辑该选项指定一个Pulse 通道名称或者编号。

**Note:** 如果你已经安装[pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa)，你也许可以保留libao默认使用alsa输出不变，因为支持alsa的程序已经默认通过PulseAudio输出了。

## 均衡器

PulseAudio内置了10段均衡器系统，按下列步骤操作以启用均衡器：

### 加载均衡器通道和dbus协议模块

```
$ pactl load-module module-equalizer-sink
$ pactl load-module module-dbus-protocol

```

### 安装并运行图形前端

安装[python-pyqt4](https://aur.archlinux.org/packages/python-pyqt4/)并执行：

```
$ qpaeq

```

**Note:** 如果运行qpaeq无效，安装[pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) ，运行媒体播放器时把 "ALSA Playback on" 改为 "FFT based equalizer on ..."。

### 每次启动时加载均衡器和dbus模块

编辑 `/etc/pulse/default.pa` 并加入下面几行：

```
### Load the integrated PulseAudio equalizer and D-Bus module
load-module module-equalizer-sink
load-module module-dbus-protocol

```

## 应用程序

### QEMU

运行下面命令以确定QEMU是否支持[pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio)：

```
$ qemu-system-x86_64 -audio-help | grep 'Name: pa'

```

QEMU可通过环境变量配置音频

```
export QEMU_AUDIO_DRV=pa
export QEMU_PA_SINK=alsa_output.pci-0000_04_01.0.analog-stereo.monitor
export QEMU_PA_SOURCE=input
```

运行下面的命令可查看更多与[pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio)有关的选项：

```
$ qemu-system-x86_64 -audio-help | grep '_PA_'

```

运行下面的命令可查看QEMU支持的音频模拟驱动

```
$ qemu-system-x86_64 -soundhw help

```

例如，在QEMU中使用`-soundhw ac97` 命令可以在虚拟机中使用`ac97`驱动。

{{Note|

*   在 `qemu-system-*XXX*`命令中， *XXX* 代表虚拟机的硬件架构。 运行 `ls /usr/bin/qemu-system-* -1`可以查看可用的硬件架构。
*   虚拟机的虚拟显卡驱动也可能造成音频质量问题。逐个尝试以便解决问题。运行 `qemu-system-x86_64 -h | grep vga`以查看可用的虚拟显卡选项。

### AlsaMixer.app

Make [AlsaMixer.app](https://aur.archlinux.org/packages/AlsaMixer.app/) dockapp for the [windowmaker](https://aur.archlinux.org/packages/windowmaker/) use pulseaudio, e.g.

```
$ AlsaMixer.app --device pulse

```

Here is a two examples where the first one is for ALSA and the other one is for pulseaudio. You can run multiple instances of it. Use the `-w` option to choose which of the control buttons to bind to the mouse wheel.

```
# AlsaMixer.app -3 Mic -1 Master -2 PCM --card 0 -w 1
# AlsaMixer.app --device pulse -1 Capture -2 Master -w 2

```

**Note:** It can use only those output sinks that set as default.

### XMMS2

将程序切换到pulseaudio输出：

```
$ nyxmms2 server config output.plugin pulse

```

以及alsa：

```
$ nyxmms2 server config output.plugin alsa

```

让xmms2使用不同的通道输出：

```
 $ nyxmms2 server config pulse.sink alsa_output.pci-0000_04_01.0.analog-stereo.monitor

```

另可查阅官方指南 [[3]](https://xmms2.org/wiki/Using_the_application).

### KDE Plasma Workspaces 和 Qt4

KDE/Qt4程序会自动使用PulseAudio。PulseAudio在KDE混音器中是默认支持的。更多信息请查阅[Archlinux Wiki KDE](http://www.pulseaudio.org/wiki/KDE)。这个页面提到一个窍门，就是把`load-module module-device-manager`这一行添加到`/etc/pulse/default.pa`文件中。 如果Phonon使用phonon-gstreamer为后端，Gstreamer应该按照[#GStreamer](#GStreamer)这一节进行设置。

### Audacious

[Audacious](/index.php/Audacious "Audacious") 默认支持PulseAudio。把 Audacious Preferences -> Audio -> Current output plugin 设置为 'PulseAudio Output Plugin'即可。

### Java/OpenJDK 6

参考[Java sound with PulseAudio](/index.php/Java#Java_sound_with_PulseAudio "Java")，用padsp为Java程序创建一个启动脚本。

### Music Player Daemon (MPD)

[配置](http://mpd.wikia.com/wiki/PulseAudio) [MPD](/index.php/MPD "MPD") 使其使用 PulseAudio。另请参阅 [MPD/Tips and Tricks#MPD and PulseAudio](/index.php/MPD/Tips_and_Tricks#MPD_and_PulseAudio "MPD/Tips and Tricks").

### MPlayer

[MPlayer](/index.php/MPlayer "MPlayer") 可通过 `-ao pulse` 选项支持PulseAudio输出。也可以设置mplayer默认使用pulseaudio输出。编辑`~/.mplayer/config`更改当前用户的设置，或者编辑`/etc/mplayer/mplayer.conf`更改整个系统的设置：

 `/etc/mplayer/mplayer.conf`  `ao=pulse` 

### guvcview

当[guvcview](https://www.archlinux.org/packages/?name=guvcview)使用网络摄像头的PulseAudio输入时，音频输入可能挂起，导致没有声音被录下来。你可以运行下面命令来检查：

```
$ pactl list sources

```

如果音频源显示为"suspended"（挂起），那么编辑`/etc/pulse/default.pa`，把下面这行

```
load-module module-suspend-on-idle

```

修改为

```
#load-module module-suspend-on-idle

```

然后不论你重启PulseAudio还是重启电脑，输入源都只会处于空闲状态而不是挂起。这样的话guvcview就可以正确地录音了。

## 故障排查

详见 [PulseAudio/Troubleshooting](/index.php/PulseAudio/Troubleshooting "PulseAudio/Troubleshooting")。

## 相关阅读

*   [http://www.alsa-project.org/main/index.php/Asoundrc](http://www.alsa-project.org/main/index.php/Asoundrc) - ALSA wiki on .asoundrc
*   [http://www.pulseaudio.org/](http://www.pulseaudio.org/) - PulseAudio official site
*   [http://www.pulseaudio.org/wiki/FAQ](http://www.pulseaudio.org/wiki/FAQ) - PulseAudio FAQ