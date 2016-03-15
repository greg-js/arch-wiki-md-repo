这篇文章讲述如果在你的电脑上安装和配置**O**pen **S**ound **S**ystem (OSS)。

[Open Sound System](https://en.wikipedia.org/wiki/Open_Sound_System "wikipedia:Open Sound System") 是一个类Unix和POSIX兼容系统上一个可选的声音架构。OSSv3是Linux下原始的声音系统并集成在内核里，但是OSSv4在2002年OSS成为商业软件时它地位被ALSA所取代。OSSv4在2007年又成为了开源软件 ，[4Front Technologies](http://www.opensound.com/) 以GPL协议发布了它的源码。

## Contents

*   [1 与ALSA驱动对比](#.E4.B8.8EALSA.E9.A9.B1.E5.8A.A8.E5.AF.B9.E6.AF.94)
    *   [1.1 OSS的优点（对用户来说）](#OSS.E7.9A.84.E4.BC.98.E7.82.B9.EF.BC.88.E5.AF.B9.E7.94.A8.E6.88.B7.E6.9D.A5.E8.AF.B4.EF.BC.89)
    *   [1.2 OSS的优点（对开发者来说）](#OSS.E7.9A.84.E4.BC.98.E7.82.B9.EF.BC.88.E5.AF.B9.E5.BC.80.E5.8F.91.E8.80.85.E6.9D.A5.E8.AF.B4.EF.BC.89)
    *   [1.3 ALSA的优点](#ALSA.E7.9A.84.E4.BC.98.E7.82.B9)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 测试](#.E6.B5.8B.E8.AF.95)
*   [4 声音控制](#.E5.A3.B0.E9.9F.B3.E6.8E.A7.E5.88.B6)
    *   [4.1 颜色定义](#.E9.A2.9C.E8.89.B2.E5.AE.9A.E4.B9.89)
    *   [4.2 保存和恢复混音器设置](#.E4.BF.9D.E5.AD.98.E5.92.8C.E6.81.A2.E5.A4.8D.E6.B7.B7.E9.9F.B3.E5.99.A8.E8.AE.BE.E7.BD.AE)
    *   [4.3 其他的混音器程序](#.E5.85.B6.E4.BB.96.E7.9A.84.E6.B7.B7.E9.9F.B3.E5.99.A8.E7.A8.8B.E5.BA.8F)
*   [5 配置程序来使用OSS](#.E9.85.8D.E7.BD.AE.E7.A8.8B.E5.BA.8F.E6.9D.A5.E4.BD.BF.E7.94.A8OSS)
    *   [5.1 Skype](#Skype)
    *   [5.2 Wine](#Wine)
    *   [5.3 Gajim](#Gajim)
    *   [5.4 MOC](#MOC)
    *   [5.5 使用Gstreamer的程序](#.E4.BD.BF.E7.94.A8Gstreamer.E7.9A.84.E7.A8.8B.E5.BA.8F)
    *   [5.6 firefox（火狐）>=3.5](#firefox.EF.BC.88.E7.81.AB.E7.8B.90.EF.BC.89.3E.3D3.5)
    *   [5.7 Mplayer](#Mplayer)
    *   [5.8 Music Player Daemon（MPD）](#Music_Player_Daemon.EF.BC.88MPD.EF.BC.89)
    *   [5.9 其他程序](#.E5.85.B6.E4.BB.96.E7.A8.8B.E5.BA.8F)
*   [6 问题以及解决](#.E9.97.AE.E9.A2.98.E4.BB.A5.E5.8F.8A.E8.A7.A3.E5.86.B3)
    *   [6.1 HDAudio硬件的问题解决](#HDAudio.E7.A1.AC.E4.BB.B6.E7.9A.84.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
        *   [6.1.1 问题如何产生](#.E9.97.AE.E9.A2.98.E5.A6.82.E4.BD.95.E4.BA.A7.E7.94.9F)
        *   [6.1.2 如何解决](#.E5.A6.82.E4.BD.95.E8.A7.A3.E5.86.B3)
    *   [6.2 解决其他问题](#.E8.A7.A3.E5.86.B3.E5.85.B6.E4.BB.96.E9.97.AE.E9.A2.98)
*   [7 提示和小技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E5.B0.8F.E6.8A.80.E5.B7.A7)
    *   [7.1 OSS与多媒体键](#OSS.E4.B8.8E.E5.A4.9A.E5.AA.92.E4.BD.93.E9.94.AE)
    *   [7.2 ossvol的问题解决](#ossvol.E7.9A.84.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
    *   [7.3 改变采样率](#.E6.94.B9.E5.8F.98.E9.87.87.E6.A0.B7.E7.8E.87)
    *   [7.4 Changing the Default Sound Output](#Changing_the_Default_Sound_Output)
    *   [7.5 Creative Sound Blaster X-Fi Surround 5.1 SB1090 USB](#Creative_Sound_Blaster_X-Fi_Surround_5.1_SB1090_USB)
    *   [7.6 简单的系统托盘小工具](#.E7.AE.80.E5.8D.95.E7.9A.84.E7.B3.BB.E7.BB.9F.E6.89.98.E7.9B.98.E5.B0.8F.E5.B7.A5.E5.85.B7)
    *   [7.7 开机自启动ossxmix托盘](#.E5.BC.80.E6.9C.BA.E8.87.AA.E5.90.AF.E5.8A.A8ossxmix.E6.89.98.E7.9B.98)
    *   [7.8 录制一个程序的声音](#.E5.BD.95.E5.88.B6.E4.B8.80.E4.B8.AA.E7.A8.8B.E5.BA.8F.E7.9A.84.E5.A3.B0.E9.9F.B3)
    *   [7.9 Suspend and Hibernation](#Suspend_and_Hibernation)
    *   [7.10 ALSA 模拟器](#ALSA_.E6.A8.A1.E6.8B.9F.E5.99.A8)
        *   [7.10.1 介绍](#.E4.BB.8B.E7.BB.8D)
    *   [7.11 对特定驱动的设置](#.E5.AF.B9.E7.89.B9.E5.AE.9A.E9.A9.B1.E5.8A.A8.E7.9A.84.E8.AE.BE.E7.BD.AE)
    *   [7.12 System-wide (software) equalizer effects](#System-wide_.28software.29_equalizer_effects)

# 与ALSA驱动对比

OSS与ALSA相比的一些优缺点。

## OSS的优点（对用户来说）

*   在内核空间（kernel space）里面包含了一个透明软件混音器(vmix)。这样多个程序就可以同时使用声音设备而且没有任何问题。
*   这个混音器可以让你单独调节各个程序的音量。
*   对某些老声卡有着更好的支持比如创新（Creative）的X-Fi。
*   声音程序的初始反应时间一般更好。
*   对使用OSS的应用程序接口（API）的程序有更好的支持，很多程序都支持OSS的API，而不需要ALSA的模拟。

## OSS的优点（对开发者来说）

*   清晰的API[文档](http://manuals.opensound.com/developer)，更易于使用。
*   支持用户空间的声音驱动。
*   可移植性强，OSS也可以在BSDs和Solaris下运行。
*   本身可以跨平台，可以更[方便](http://revolf.free.fr/Alchimie-7/Alchimie7_OSS_Haiku.en.pdf)移植到新的操作系统。

## ALSA的优点

*   ALSA对USB音频设备支持更好，而OSS的输出还在试验中，输入还未实现。
*   ALSA支持蓝牙声音设备。
*   ALSA支持AC'97和HDAudio dial-up soft-modems (比如Si3055)。
*   ALSA对MIDI支持得更好，但用OSS你只能通过软件合成器（如timidity和fluidsynth）来使用MIDI。
*   ALSA对待机支持更好，而用OSS，你需要在待机前使用<tt>soundoff</tt>来停止OSS驱动，在恢复后使用<tt>soundon</tt>来启动OSS。
*   OSS的jack检测目前在**某些**HDAudio-powered主板上不能正常工作。也就是说在某些型号的主板上，你可能需要在插入耳机的时候手动关闭外置扬声器。而ALSA没这个问题。

# 安装

从 [AUR](/index.php/AUR "AUR") 安装 [oss](https://aur.archlinux.org/packages/oss/).

这会安装OSS并运行其启动脚本，它会暂时使ALSA模块失效，并安装OSS内核模块。因为ALSA在引导过程中默认开启，你需要关闭它以免引导时它与OSS发生冲突。可以编辑{Filename|rc.conf}} 文件并添加：

```
MODULES=(!soundcore ...

```

然后将OSS加入守护进程中：

```
DAEMONS=(crond hal @oss...

```

如果用户不在audio组里，把他加进去：

```
# gpasswd -a username audio

```

*   运行下面的命令启动oss:

```
# /etc/rc.d/oss start

```

如果OSS无法检测到你的声卡，运行：

```
# ossdetect -v

```

然后运行 `soundoff && soundon` 来重新激活它。

# 测试

要注意默认的音量很高，不要戴耳机，并且调低扬声器的音量（如果可以），然后再进行测试：

**测试OSS：**

```
$ osstest

```

你应该能在测试过程中听到音乐，如果没有，尝试在接下来的步骤里调节音量。

如果你要让多个程序同时发声，可以用OSS的软件混音器——vmix。

**检查vmix是否开启了：**

```
$ ossmix -a | grep -i vmix

```

你应该能看到类似'vmix0-enable ON|OFF (currently ON)'.的一行。如果你没看到任何含'vmix'的行，很可能vmix没有依附到你的声音设备上，运行下面命令：

```
$ vmixctl attach device

```

其中*device*是你的声音设备，比如/dev/oss/oss_envy240/pcm0。

为了避免将来手动运行这个命令，可以把它加到/usr/lib/oss/soundon.user里，像[[1]](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Changing_the_default_sound_output)中建议的。

如果你看到了"Device or resource busy"（设备或资源繁忙）的错误，需要把"vmix_no_autoattach=1"加到/usr/lib/oss/conf/osscore.conf中，然后重启。

**查看哪个设置被检测到了：**

```
$ ossinfo

```

你应该能够看到你的设备列在Device objects 或 Audio Devices下。如果你要用的设备不在其中，需要编辑 /usr/lib/oss/etc/installed_drivers 。设备的驱动应该在更上边。而后可能需要运行soundoff, soundon。如果还不工作，注释掉所有不必要的驱动。

# 声音控制

为了控制不同设备，你要设置混音器。命令行工具是 `ossmix`，它很像BSD声音混音器(mixerctl)。还有一个更友好的基于图形界面的混音器 `ossxmix` ，运行时依赖[gtk2](https://www.archlinux.org/packages/?name=gtk2)。

<tt>ossxmix</tt>的基本界面和控制功能如下：

```
 / High Definition Audio ALC262 \    --------------------------------> 1
/________________________________\________________________________
|                                                                 \
| [x] vmix0-enable [vmix0-rate: 48.000kHz]      vmix0-channels    |--> 2
|                                               [ Stereo [v] ]    |
|                                                                 |
|  __codec1______________________________________________________ |
| |  _jack______________________________________________________ ||--> 3
| | |  _int-speaker_________________   _green_________________  |||
| | | |                             | |                       | |||
| | | |  _mode_____ | |             | |  _mode_____   | |     | |||
| | | | [ mix [v] ] o o [x] [ ]mute | | [ mix  [v] ]  o o [x] | |||
| | | |             | |             | |               | |     | |||
| | | |_____________________________| |_______________________| |||
| | |___________________________________________________________|||
| |______________________________________________________________||
| ___vmix0______________________________________________________  |
| |  __mocp___  O O   _firefox_  O O  __pcm7___  O O            | |--> 4
| | |         | O O  |         | x x |         | O O            | |
| | | | |     | x O  | | |     | x x | | |     | O O            | |
| | | o o [x] | x x  | o o [x] | x x | o o [x] | O O            | |
| | | | |     | x x  | | |     | x x | | |     | O O            | |
| | |_________| x x  |_________| x x |_________| O O            | |
| |_____________________________________________________________| |
|_________________________________________________________________|

```

1.  一个声卡一个标签页。
2.  Vmix (虚拟混音器) 的特别配置，包括采样率和混音器优先级。
3.  这是你声卡的插孔（输入和输出）的配置。声卡提供的每一个混音器控制都在这里显示。
4.  应用程序vmix混音器和音量控制。如果程序不在播放声音它会用pcm08, pcm09...标记，当播放时会显示程序名称。

## 颜色定义

对于high definition (HD) audio，`ossxmix`会用预定义的颜色显示jack的设置：

| Color | Type | Connector |
| green | front channels (stereo output) | 3.5mm TRS |
| black | rear channels (stereo output) | 3.5mm TRS |
| grey | side channels (stereo output) | 3.5mm TRS |
| gold | center and subwoofer (dual output) | 3.5mm TRS |
| blue | line level (stereo input) | 3.5mm TRS |
| pink | microphone (mono input) | 3.5mm TS |

## 保存和恢复混音器设置

混音器设置在关机时会保存，如果你现在就要保存，可以运行：

```
# savemixer

```

`savemixer` 可以用来把音量记录在文件中（用 `-f` 选项）然后用 `-L` 选项恢复。

## 其他的混音器程序

其他支持OSS的混音器程序有：

*   GNOME - Gnome volume control
*   KDE - Kmix - OSS的支持正在开发中。

# 配置程序来使用OSS

## Skype

<tt>skype</tt>包只支持ALSA ，获得支持OSS的Skype，安装 <tt>skype-oss</tt> 包：

```
# pacman -S skype-oss

```

如果你用的是x86_64，可以用[bin32-skype-oss](https://aur.archlinux.org/packages/bin32-skype-oss/)。

## Wine

*   运行 <tt>winecfg</tt>。

```
$ winecfg

```

*   到<tt>Audio（音频）</tt> 选项卡。

*   选择<tt>OSS Driver（OSS驱动）</tt>。

## Gajim

Gajim缺省用 `aplay -q`放声音。可以在Advanced Settings（高级设置）里搜索`soundplayer`变量。oss提供的ossplay程序是一个好的替换：`ossplay -qq`

## MOC

让MOC支持OSS4,你必须把配置文件`"$HOME"/.moc`中的 OSSMixerDevice 改成`/dev/ossmix`。 然后MOC就可以正常工作。或者你可以编译AUR中的moc-svn包（它支持新的vmix）。 在界面下更改OSSMixerChannel可以在mocp中按'w'。

## 使用Gstreamer的程序

移除pulseaudio和gstreamer*-pulse的程序和库。

要将gstreamer的输出设置成OSS而不是缺省的ALSA，运行：

```
gstreamer-properties

```

把**Default Output**（缺省输出）选成 custom（自定义），并把文本框中内容改成：

```
oss4sink

```

对于输入：

```
oss4src

```

**Note:** oss4src不一定比osssrc听起来更好，所以只有在发现确实这样时再改。

**Note:** 对于一些程序 (像 Rhythmbox, Totem) ，gstreamer-properties没作用，因为它们依赖 "musicaudiosink" 而不是 "audiosink"（gstreamer-properties修改的）。用gstreamer-properties设置完Workaround后用gconf-editor把"/system/gstreamer/0.10/default/audiosink"值拷贝到"musicaudiosink"（在一个位置)中

如果你用gstreamer作为phonon的后端，要设置环境变量，对于当前用户：

```
export PHONON_GST_AUDIOSINK=oss4sink

```

把它加到 `~/.bashrc` 来登陆自动加载。

## firefox（火狐）>=3.5

Firefox 3.5 新引进的<video>和<audio>标签支持直接播放ogg媒体。然而它不能同时支持ALSA和OSS，所以你需要安装[community]中的xulrunner-oss包。

```
1\. 关闭 firefox。
2\. 安装[community]中的xulrunner-oss包。
3\. 启动firefox。

```

## Mplayer

如果你用GUI外壳（如smplayer）。你会发现在音频设置中有oss输出选项。如果用它本身，可以播放时指定`mplayer -ao oss /some/file/to/play.mkv`，如果嫌麻烦可以在`"$HOME"/.mplayer/config`中加入 "ao=oss"。

## Music Player Daemon（MPD）

MPD的配置文件是 /etc/mpd.conf 和 ~/.mpdconf，检查这两个文件，找到这样的东西：

```
 audio_output {
       type           "alsa"
       name           "Some Device Name"
 }

```

如果你发现一个像上边的未注释的ALSA配置，注释或删掉，并加入下边的内容：

```
 audio_output {
       type           "oss"
       name           "My OSS Device"
 }

```

**Note:** 我必须把这个配置写到 ~/.mpdconf 才能正常工作，按理预改/etc/mpd.conf也行。（应该是~/.mpdconf把优先级高或者把/etc/mpd.conf配置覆盖了）

对于大多数用户可以不需要进一步的配置了。然而如果你的MPD重启后不成正常工作，或者你更具体地配置，OSS音频输出可以像这样更详细地配置： 首先运行：

```
 ossinfo | grep /dev/dsp

```

找到类似这样`/dev/dsp -> /dev/oss/<SOME_CARD_IDENTIFIER>/pcm0`的行。注意你的 <SOME_CARD_IDENTIFIER> ，然后加入下边粗体的部分到你的MPD配置文件：

```
 audio_output {
       type            "oss"
       name            "My OSS Device"
       **device          "/dev/oss/<SOME_CARD_IDENTIFIER>/pcm0"**
       **mixer_device    "/dev/oss/<SOME_CARD_IDENTIFIER>/mix0"**
 }

```

## 其他程序

*   如果你不能让其他程序发出声音，试试看[为程序设置OSSv4](http://www.4front-tech.com/wiki/index.php/Configuring_Applications_for_OSSv4)这里
*   用{Codeline|pacman -Ss -- -oss}} 和 [AUR中](https://aur.archlinux.org/packages.php?K=-oss%7C) 搜索特定的包。

# 问题以及解决

## HDAudio硬件的问题解决

### 问题如何产生

如果你有一个HDAudio声音设备，有可能你必须调整一些设置你的声卡才能正常工作。

HDAudio devices are very powerful in the sense that they can contain a lot of small circuits (called *widgets*) that can be adjusted by software at any time.（参考翻译：任何时间软件都可以调整强大的HDAudio上包含的很多小器件）。这些控制对混音器是外露的，例如，可以被用来把耳机声音输出功能改到声音输入功能。

但是，这可能导致问题，主要因为HDAudio标准比理想中应该有的标准来说太灵活了，也因为计算机开发商经常支持关注怎么让*官方驱动*正常工作。

所以你才会在使用HDAudio设备的时候，发现控制是混乱的，必须自己尝试手动调整每一个控制条直到可以工作，因为默认根本不会正常工作。你需要在前台调整ossxmix混音器设定的时候，后台有个程序录制/播放声音(比如 <tt>ossrecord - | ossplay -</tt> 来录制或者 <tt>osstest -lV</tt>来播放)。

### 如何解决

打开<tt>ossxmix</tt>，尝试改变每个控制条到中间位置，这包含在声卡特殊设定，就如上面"[混音器](/index.php/OSS#The_mixer "OSS")"说到的一样。

*   把每个音量控制条往上调整Raise every volume control slider.
*   在每个选择框里面，尝试改变选项，一定要尝试每个可能的选项
*   如果你听到有噪音，一个一个尝试把某些控制往下调整或者静音，直到你找到噪音的来源。

请注意，你**不必**调整顶部区域和底部区域的有关虚拟<tt>vmix</tt>混音器控制的部分控制条。

## 解决其他问题

*   类似ALSA的，你需要降低main音量和PCM音量来一定程序上减少噪音(这根据你芯片情况而定。我使用vol=65,pcm=65，芯片为via8237)

*   看[这里](http://4front-tech.com/forum/viewtopic.php?t=2358)了解如何设定默认声卡，因为默认的选择不是最优的。

*   如果一个程序播放声音遇到困难, 4front的wiki里面可能有[解决办法](http://www.4front-tech.com/wiki/index.php/Configuring_Applications_for_OSSv4).

*   如果你有其他问题，尝试在这个地方搜索或者发帖: [http://www.4front-tech.com/forum/](http://www.4front-tech.com/forum/)

# 提示和小技巧

## OSS与多媒体键

一个简单的静音/恢复和增减音量的方法是使用[AUR](/index.php/AUR "AUR")中的 [`ossvol` 脚本](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#ossvol)。 如果你的多媒体键默认不工作，查看 [使用多媒体键控制OSS](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Using_multimedia_keys_with_OSS)。

安装好了这样在开关声音：

```
$ ossvol -t

```

输入`ossvol -h`查看其他命令：

如果你不如果怎么把命令绑定到多媒体键上，看[Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")。

## `ossvol`的问题解决

如果你看到这样的错误：

```
Bad mixer control name(987) 'vol'

```

你需要编辑`/usr/bin/ossvol`改`CHANNEL`变量的值，它在脚本的开始处。例如我的是`CHANNEL="vmix0-outvol"`。

*   **注意** 如果你用xbindkeys来绑定快捷键，把

```
"ossmix vmix0-outvol -- +1"

```

raise volume

```
"ossmix vmix0-outvol -- -1"

```

lower volume

加到.xbindkeysrc中的traise/lower volume section是调整音量的好方法。

## 改变采样率

改变采样率不是那么简单的事，它只能通过root用户改变并且改变时vmix不能被任何程序使用。在接下来的操作之前，检查一下你的receiver/amplifier（接收器/放大器）并且使用高质量的扬声器而不是普通的电脑扬声器。因为如果你用的是普通的电脑扬声器，下边的任何改动都不会让你感觉到任何变化。

缺省的采样率是48000hz。 There are several conditions in which you may want to change this. This all depends on your usage patterns. You want the sample rate you are using to match the media you use the most. If your computer has to change the sampling rate of the media to suit the hardware it is likely, though not guaranteed that you will have a loss in audio quality. This is most noticable in downsampling (ie. 96000hz → 48000hz). There is an article about this issue in ["Stereophile"](http://www.stereophile.com/news/121707lucky/) which was [discussed](http://lists.apple.com/archives/coreaudio-api/2008/Jan/msg00272.html) on Apple's "CoreAudio API" mailing list if you wish to learn more about this issue.

Some example sample rates:

*   44100hz - Sample rate of standard [Red Book](https://en.wikipedia.org/wiki/Red_Book_(audio_CD_standard) audio cds.
*   88000hz - Sample rate of [SACD](https://en.wikipedia.org/wiki/Super_Audio_CD "wikipedia:Super Audio CD") high definition audio discs/downloads. It is rare that your motherboard will support this sample rate.
*   96000hz - Sample rate of most high definition audio downloads. If your motherboard is an [AC'97](https://en.wikipedia.org/wiki/AC%2797 "wikipedia:AC'97") motherboard, this is likely to be your highest bitrate.
*   192000hz - Sample rate of BluRay, and some (very few) high definition downloads. Support for external audio reciever equipment is limited to high end audio. Not all motherboards support this. An example of a motherboard chipset that would support this includes [Intel HDA audio](https://en.wikipedia.org/wiki/Intel_High_Definition_Audio "wikipedia:Intel High Definition Audio").

To check what your sample rate is currently set to:

1.  Run `"ossmix | grep rate"`.

You are likely to see `"vmix0-rate <decimal value> (currently 48000) (Read-only)"`.

If you do not see a "vmix0-rate" (or "vmix1-rate", etc.) being outputted, than it probably means that vmix is disabled. In that case, OSS will use the rate requested by the program which uses the device, so this section doesn't apply. Exception: envy24(ht) cards have a setting envy24.rate which has a similiar function (see "oss_envy24" manpage). You can follow these steps, but at step 2, change with ossmix the value of "envy24.rate" as well.

Steps to affect the change:

1.  First, make sure your card is able to use the new rate. Run "ossinfo -v2" and see if the wanted rate is in the "Native sample rates" output.
2.  As root, run `"/usr/lib/oss/scripts/killprocs.sh"`. Be aware, this will close any program that currently has an open sound channel (examples being media players, Firefox as of 3.5 if you have xulrunner-oss installed, and the gnome volume control).
3.  After all programs occupying vmix are terminated, run as root: `"vmixctl rate /dev/dsp 96000"` replacing the rate with your desired sample rate.
4.  Run `"ossmix | grep rate"` and check for `"vmix0-rate <decimal value> (currently 96000) (Read-only)"` to see if you were successful.
5.  **Make changes permanent** use the soundon.user file to set the rate for every soundon

```
write `"vmixctl rate /dev/dsp 96000" in the file /usr/lib/oss/soundon.user` and make it executable.

```

## Changing the Default Sound Output

When running osstest, the first test passes for the first channel, but not for the stereo or right channel, it sounds distorted/hisses. If this is what your sound is like, then it's set to the wrong output.

```
      *** Scanning sound adapter #-1 ***
      /dev/oss/oss_hdaudio0/pcm0 (audio engine 0): HD Audio play front
      - Performing audio playback test... 
      <left> OK <right> OK <stereo> OK <measured srate 47991.00 Hz (-0.02%)> 

```

The left sounded good, the right and stereo were the distorted ones.

Let the test continue until you get a working output:

```
      /dev/oss/oss_hdaudio0/spdout0 (audio engine 5): HD Audio play spdif-out 
      - Performing audio playback test... 
      <left> OK <right> OK <stereo> OK <measured srate 47991.00 Hz (-0.02%)> 

```

If this passed the test on all left, right and stereo, proceed to next step.

So from here: [Changing_the_default_sound_output](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Changing_the_default_sound_output) you get the command to change the default output; change according to what works for you

```
      sudo ln -sf /dev/oss/oss_hdaudio0/spdout0 /dev/dsp_multich

```

With 5.1 surround, chose dsp_multichannel; with 2 channel, dsp should work.

## Creative Sound Blaster X-Fi Surround 5.1 SB1090 USB

This information is completely from [4front-tech.com](http://www.4front-tech.com/forum/viewtopic.php?f=3&t=3423) ; courtesy of kristian and Maxa. Thanks!!

It's surprising to learn that the external card does not work just because of a missing true return value in the function write_control_value(...) in ossusb_audio.c.

To fix this, a recompile of oss is nessasary, for now.

1\. Grab the latest oss from the Arch Repo

```
[https://repos.archlinux.org/wsvn/community/oss/repos/community-x86_64/](https://repos.archlinux.org/wsvn/community/oss/repos/community-x86_64/)

```

2\. Extract it

3\. cd to the folder, I renamed the folder to oss

4\. run makepkg --nobuild

5\. cd to src/kernel/drv/oss_usb/ ; **edit the ossusb_audio.c** ; **add a Return 1** ; should look like so and **SAVE**

```
  static int
 write_control_value (ossusb_devc * devc, udi_endpoint_handle_t * endpoint,
            int ctl, int l, unsigned int v)
 {
   return 1;

```

6\. cd to src/kernel/setup and edit srcconf_linux.inc, search for -Werror and remove it, otherwise OSS will not compile.

7\. do a makepkg --noextract

Now you must install the package with pacman -U ; remove oss first if already installed (pacman -Rd oss)

## 简单的系统托盘小工具

想要一个GNOME那样的控制音量小工具？W [在这里](https://bbs.archlinux.org/viewtopic.php?id=77440)我得到一个可用的 [工具](http://pastebin.furver.se/0xflchkfz/)。

下载 [这个脚本](http://pastebin.furver.se/0xflchkfz/0xflchkfz.txt) 重命名（例如 ossvolctl），运行：

```
$ chmod +x ossvolctl
# cp ossvolctl /usr/bin/ossvolctl

```

or

```
# install -Dm755 ossvolctl /usr/bin/ossvolctl

```

## 开机自启动ossxmix托盘

**KDE 4**

在`~/.local/share/applications/`创建一个启动器`ossxmix.desktop`：

```
[Desktop Entry]
Name=Open Sound System Mixer
GenericName=Audio Mixer
Exec=ossxmix -b
Icon=audio-card
Categories=Application;GTK;AudioVideo;Player;
Terminal=false
Type=Application
Encoding=UTF-8
```

让它随桌面环境启动：

System Settings（系统设置） > Advanced tab（高级） > Autostart（自启动），然后点击add program（添加程序）并选择 'Multimedia' （多媒体）。

**Gnome**

*   以root用户创建/usr/local/bin/ossxmix_bg：

```
#!/bin/sh
exec /usr/bin/ossxmix -b

```

到 System（系统）> Preferences（属性） > Start Up Applications（启动程序）

*   点击Add（添加），在Name（名称）中输入 OSSMIX ，field（内容）中输入`/usr/local/bin/ossxmix_bg`然后点击Add（添加）按钮。

*   重新登陆生效。

## 录制一个程序的声音

*   [Recording sound output of a program](http://www.opensound.com/wiki/index.php/Tips_And_Tricks#Recording_sound_output_of_a_program).

## Suspend and Hibernation

OSS does not automatically support suspend meaning that OSS must be manually stopped prior to suspending or hibernating.

OSS provides <tt>soundon</tt> and <tt>soundoff</tt> to enable and disable OSS, although any processes that use sound must be terminated first.

The following script is a rather basic method of automatically unloading OSS prior to suspending and reloading afterwards.

```
#!/bin/sh
. "${PM_FUNCTIONS}"

suspend_osssound()
{
 /usr/lib/oss/scripts/killprocs.sh
 /usr/sbin/soundoff
}

resume_osssound()
{
 /usr/sbin/soundon
}

case "$1" in
 hibernate|suspend)
 suspend_osssound
	;;
 thaw|resume)
	resume_osssound
	;;
 *) exit $NA
	;;
esac

```

Save the contents of the script (as root) into `/etc/pm/sleep.d/50ossound` and make it executable. `chmod a+x /etc/pm/sleep.d/50ossound`

**Note:** This script is rather basic and will terminate any application directly accessing OSS, save your work prior to suspending/hibernating.

OSS does not support suspending but we don't care or better [s2ram](/index.php/Suspend_to_RAM "Suspend to RAM") works fine without stopping OSS. Just create a nice suspend script to /sbin/suspend and make it executable.

```
 #!/bin/sh

 ## Checking if you are a root or not
 if ! [ -w / ]; then
   echo >&2 "This script must be run as root"
   exit 1
 fi

 s2ram -f

 sleep 2

 /etc/rc.d/oss restart 2>/tmp/oss.txt ||
 echo "OSS restart failed, check /tmp/oss.txt for advice"

```

That's all your apps are fine and suspend works. \o/

**Note:** If you are using Opera you must kill operapluginwrapper before suspend. To do this add **pid=$(pidof operapluginwrapper) && kill $pid** before s2ram -f.

## ALSA 模拟器

你可以让<tt>alsa-lib</tt>用OSS作为声音输出系统，这是一种ALSA模拟器。

但是注意，这个方法可能在你声音输出的时候造成额外的延迟，而且模拟器也不完善，无法保证能让所有程序发声。例如如果软件通过ALSA检测设备，这个软件就不能正常工作。

所以，因为大多数应用直接支持OSSS，这个方法只是最后的解决方案。

将来会有更完善的ALSA模拟器，像<tt>libsalsa</tt>和<tt>cuckoo</tt>.

### 介绍

*   安装<tt>alsa-plugins</tt>包。

```
# pacman -S alsa-plugins

```

*   编辑 `/etc/asound.conf`：

```
pcm.oss {
   type oss
    device /dev/dsp
}

pcm.!default {
    type oss
    device /dev/dsp
}

ctl.oss {
    type oss
    device /dev/mixer
}

ctl.!default {
    type oss
    device /dev/mixer
}

```

**Note:** 如果你不再使用OSS，别忘了把`/etc/asound.conf`改回去。

## 对特定驱动的设置

If something isn't working, there is a possibility, that there are specific settings for specific driver (this way I have enabled jack-sense on my laptop)

*   Find out which driver is used

```
# lspci -vnn|grep -i -A 15 audio

```

```
00:1e.2 Multimedia audio controller [0401]: Intel Corporation 82801FB/FBM/FR/FW/FRW (ICH6 Family) AC'97 Audio Controller [8086:266e] (rev 03)
	Subsystem: Hewlett-Packard Company NX6110/NC6120 [103c:099c]
	Flags: bus master, medium devsel, latency 0, IRQ 21
	I/O ports at 2100 [size=256]
	I/O ports at 2200 [size=64]
	Memory at d0581000 (32-bit, non-prefetchable) [size=512]
	Memory at d0582000 (32-bit, non-prefetchable) [size=256]
	Capabilities: <access denied>
	Kernel driver in use: *oss_ich*
	Kernel modules: snd-intel8x0
```

*   Locate configuration file for device in:

```
# cd /usr/lib/oss/conf/

```

*   Try changing defaults. There are only few settings, and they are self explanatory

Setting:

```
ich_jacksense = 1 

```

in oss_ich.conf turned on jack-sense on my laptop (now plugged headphones are recognized, and speaker muted).

*   Restart oss for changes take effects.

```
# sudo /etc/rc.d/oss restart

```

*   oss_hdaudio.conf has hdaudio_jacksens too. Maybe it will work for you. Unfortunately not for everyone.

## System-wide (software) equalizer effects

NOTES: This requires the use of the old softoss module (the predecessor of vmix) which may not be as good as vmix, wine and gstreamer do not play nice with softoss, and the module will not work with sample rates higher than 48khz.

We must do a few things to gain access to these effects.

*   If you're running the oss-linux-free daemon right now, stop it by running (as root):

```
/etc/rc.d/oss-linux-free stop

```

*   *   On builds 1015 and older, in /usr/lib/oss/etc/installed_drivers remove

```
vmix

```

*   *   On 1016 and newer, you should instead pass "vmix_disabled=1" parameter to osscore (via /usr/lib/oss/conf/osscore.conf) to disable vmix.
*   in /usr/lib/oss/etc/installed_drivers add

```
softoss

```

*   in /etc/rc.d/oss-linux-free comment out lines 15 through 20 so that it looks kinda like this

```
#!/bin/bash
. /etc/rc.conf
. /etc/rc.d/functions
case "$1" in
 start)
   stat_busy "Starting OSS/Open source driver"
   # start
   /usr/sbin/soundon
   if [ $? -gt 0 ]; then
     stat_fail
   else
     grep '^softoss' /proc/modules >/dev/null 2>/dev/null
#      if [ $? -eq 0 ]; then
#        stat_busy "Replacing old \"softoss\" module with \"vmix\""
#        rmmod softoss
#        modprobe vmix
#        sed -i 's/^softoss.*$/vmix/' /usr/lib/oss/etc/installed_drivers
#      fi
     add_daemon oss4
     stat_done
   fi
   ;;
 stop)
   stat_busy "Saving OSS mixer"
   /usr/sbin/savemixer
   if [ $? -gt 0 ]; then
     stat_fail
   else
     stat_done
   fi
   grep '^"cuckoo"' /proc/modules >/dev/null 2>/dev/null
   if [ $? -eq 0 ]; then
     stat_busy "Removing \"cuckoo\" module"
     rmmod \"cuckoo\"
   fi
   stat_busy "Stopping OSS/Open source driver"
   /usr/sbin/soundoff
   if [ $? -gt 0 ]; then
     stat_fail
   else
     rm_daemon oss4
     stat_done
   fi
   ;;
 restart)
   $0 stop
   sleep 1
   $0 start
   ;;
 *)
   echo "usage: $0 {start|stop|restart}"
esac

```

This keeps the oss-linux-free daemon from replacing softoss with vmix. (Very useful if you wish to switch between softoss and vmix.)

*   start the daemon again (as root of course)

```
/etc/rc.d/oss-linux-free start

```

*   If no errors are reported, then you may now see/use the effects with either ossmix or ossxmix with

```
ossmix -d1

```

or

```
ossxmix

```

*   you must turn off bipass to actually use the effects

```
ossmix -d1 effects.eq.bypass OFF

```

or just uncheck bypass in ossxmix

*   enjoy