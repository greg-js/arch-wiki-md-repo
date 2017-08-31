相关文章

*   [Sound system](/index.php/Sound_system "Sound system")
*   [Disable PC speaker beep (简体中文)](/index.php/Disable_PC_speaker_beep_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Disable PC speaker beep (简体中文)")

**翻译状态：** 本文是英文页面 [Advanced_Linux_Sound_Architecture](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-08-28，点击[这里](https://wiki.archlinux.org/index.php?title=Advanced_Linux_Sound_Architecture&diff=0&oldid=484694)可以查看翻译后英文页面的改动。

[高级 Linux 声音体系](https://en.wikipedia.org/wiki/zh:ALSA "wikipedia:zh:ALSA")（Advanced Linux Sound Architecture，**ALSA**）是Linux中提供声音设备驱动的内核组件，用来代替原来的开放声音系统（Open Sound System，OSSv3）。除了声音设备驱动，**ALSA**还包含一个用户空间的函数库，开发者可以通过这些高级 API 使用驱动，不必直接与内核驱动进行交互。

**注意:** 关于另一种声音体系，请阅读[开放声音系统（OSS）](/index.php/Open_Sound_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Open Sound System (简体中文)")的页面。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 用户权限](#.E7.94.A8.E6.88.B7.E6.9D.83.E9.99.90)
    *   [1.2 ALSA 工具](#ALSA_.E5.B7.A5.E5.85.B7)
    *   [1.3 OSS 兼容性](#OSS_.E5.85.BC.E5.AE.B9.E6.80.A7)
    *   [1.4 PulseAudio compatibility](#PulseAudio_compatibility)
    *   [1.5 ALSA 和 Systemd](#ALSA_.E5.92.8C_Systemd)
    *   [1.6 ALSA Firmware](#ALSA_Firmware)
*   [2 解除各声道的静音](#.E8.A7.A3.E9.99.A4.E5.90.84.E5.A3.B0.E9.81.93.E7.9A.84.E9.9D.99.E9.9F.B3)
    *   [2.1 测试你改变的设置](#.E6.B5.8B.E8.AF.95.E4.BD.A0.E6.94.B9.E5.8F.98.E7.9A.84.E8.AE.BE.E7.BD.AE)
    *   [2.2 附加注释](#.E9.99.84.E5.8A.A0.E6.B3.A8.E9.87.8A)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 基本语法](#.E5.9F.BA.E6.9C.AC.E8.AF.AD.E6.B3.95)
        *   [3.1.1 赋值与分隔符](#.E8.B5.8B.E5.80.BC.E4.B8.8E.E5.88.86.E9.9A.94.E7.AC.A6)
        *   [3.1.2 数据类型](#.E6.95.B0.E6.8D.AE.E7.B1.BB.E5.9E.8B)
        *   [3.1.3 操作模式](#.E6.93.8D.E4.BD.9C.E6.A8.A1.E5.BC.8F)
            *   [3.1.3.1 使用“默认”节点的默认设备设定示例](#.E4.BD.BF.E7.94.A8.E2.80.9C.E9.BB.98.E8.AE.A4.E2.80.9D.E8.8A.82.E7.82.B9.E7.9A.84.E9.BB.98.E8.AE.A4.E8.AE.BE.E5.A4.87.E8.AE.BE.E5.AE.9A.E7.A4.BA.E4.BE.8B)
        *   [3.1.4 嵌套](#.E5.B5.8C.E5.A5.97)
        *   [3.1.5 引用配置文件](#.E5.BC.95.E7.94.A8.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
    *   [3.2 设置默认声卡](#.E8.AE.BE.E7.BD.AE.E9.BB.98.E8.AE.A4.E5.A3.B0.E5.8D.A1)
        *   [3.2.1 使用环境变量选择默认PCM设备](#.E4.BD.BF.E7.94.A8.E7.8E.AF.E5.A2.83.E5.8F.98.E9.87.8F.E9.80.89.E6.8B.A9.E9.BB.98.E8.AE.A4PCM.E8.AE.BE.E5.A4.87)
        *   [3.2.2 另外一种方式](#.E5.8F.A6.E5.A4.96.E4.B8.80.E7.A7.8D.E6.96.B9.E5.BC.8F)
    *   [3.3 确认所有声音模块都已经加载](#.E7.A1.AE.E8.AE.A4.E6.89.80.E6.9C.89.E5.A3.B0.E9.9F.B3.E6.A8.A1.E5.9D.97.E9.83.BD.E5.B7.B2.E7.BB.8F.E5.8A.A0.E8.BD.BD)
    *   [3.4 启用 SPDIF 输出](#.E5.90.AF.E7.94.A8_SPDIF_.E8.BE.93.E5.87.BA)
    *   [3.5 系统级均衡器](#.E7.B3.BB.E7.BB.9F.E7.BA.A7.E5.9D.87.E8.A1.A1.E5.99.A8)
        *   [3.5.1 使用 AlsaEqual（包含界面）](#.E4.BD.BF.E7.94.A8_AlsaEqual.EF.BC.88.E5.8C.85.E5.90.AB.E7.95.8C.E9.9D.A2.EF.BC.89)
            *   [3.5.1.1 管理 AlsaEqual 配置](#.E7.AE.A1.E7.90.86_AlsaEqual_.E9.85.8D.E7.BD.AE)
        *   [3.5.2 使用 mbeq](#.E4.BD.BF.E7.94.A8_mbeq)
*   [4 高质量重采样](#.E9.AB.98.E8.B4.A8.E9.87.8F.E9.87.8D.E9.87.87.E6.A0.B7)
*   [5 上混和缩混](#.E4.B8.8A.E6.B7.B7.E5.92.8C.E7.BC.A9.E6.B7.B7)
    *   [5.1 上混（upmixing）](#.E4.B8.8A.E6.B7.B7.EF.BC.88upmixing.EF.BC.89)
    *   [5.2 缩混（downmixing）](#.E7.BC.A9.E6.B7.B7.EF.BC.88downmixing.EF.BC.89)
*   [6 混音](#.E6.B7.B7.E9.9F.B3)
    *   [6.1 手动启用 dmix](#.E6.89.8B.E5.8A.A8.E5.90.AF.E7.94.A8_dmix)
*   [7 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [7.1 USB声卡热插拔](#USB.E5.A3.B0.E5.8D.A1.E7.83.AD.E6.8F.92.E6.8B.94)
    *   [7.2 同时输出](#.E5.90.8C.E6.97.B6.E8.BE.93.E5.87.BA)
    *   [7.3 键盘控制声音](#.E9.94.AE.E7.9B.98.E6.8E.A7.E5.88.B6.E5.A3.B0.E9.9F.B3)
*   [8 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [8.1 Audigy 2 ZS 不发出声音](#Audigy_2_ZS_.E4.B8.8D.E5.8F.91.E5.87.BA.E5.A3.B0.E9.9F.B3)
    *   [8.2 VirtualBox中无声音](#VirtualBox.E4.B8.AD.E6.97.A0.E5.A3.B0.E9.9F.B3)
    *   [8.3 使用CPU频率动态调整时，音频发生跳跃](#.E4.BD.BF.E7.94.A8CPU.E9.A2.91.E7.8E.87.E5.8A.A8.E6.80.81.E8.B0.83.E6.95.B4.E6.97.B6.EF.BC.8C.E9.9F.B3.E9.A2.91.E5.8F.91.E7.94.9F.E8.B7.B3.E8.B7.83)
    *   [8.4 同时只能有一个用户播放音频](#.E5.90.8C.E6.97.B6.E5.8F.AA.E8.83.BD.E6.9C.89.E4.B8.80.E4.B8.AA.E7.94.A8.E6.88.B7.E6.92.AD.E6.94.BE.E9.9F.B3.E9.A2.91)
    *   [8.5 无法同时播放多个音频](#.E6.97.A0.E6.B3.95.E5.90.8C.E6.97.B6.E6.92.AD.E6.94.BE.E5.A4.9A.E4.B8.AA.E9.9F.B3.E9.A2.91)
    *   [8.6 有时候开机无声](#.E6.9C.89.E6.97.B6.E5.80.99.E5.BC.80.E6.9C.BA.E6.97.A0.E5.A3.B0)
    *   [8.7 特定程序的问题](#.E7.89.B9.E5.AE.9A.E7.A8.8B.E5.BA.8F.E7.9A.84.E9.97.AE.E9.A2.98)
    *   [8.8 特定型号的配置](#.E7.89.B9.E5.AE.9A.E5.9E.8B.E5.8F.B7.E7.9A.84.E9.85.8D.E7.BD.AE)
    *   [8.9 与蜂鸣器冲突](#.E4.B8.8E.E8.9C.82.E9.B8.A3.E5.99.A8.E5.86.B2.E7.AA.81)
    *   [8.10 麦克风输入无声音](#.E9.BA.A6.E5.85.8B.E9.A3.8E.E8.BE.93.E5.85.A5.E6.97.A0.E5.A3.B0.E9.9F.B3)
    *   [8.11 设置默认的麦克风/录音设备](#.E8.AE.BE.E7.BD.AE.E9.BB.98.E8.AE.A4.E7.9A.84.E9.BA.A6.E5.85.8B.E9.A3.8E.2F.E5.BD.95.E9.9F.B3.E8.AE.BE.E5.A4.87)
    *   [8.12 内置麦克风无效](#.E5.86.85.E7.BD.AE.E9.BA.A6.E5.85.8B.E9.A3.8E.E6.97.A0.E6.95.88)
    *   [8.13 Intel 板载声卡无声](#Intel_.E6.9D.BF.E8.BD.BD.E5.A3.B0.E5.8D.A1.E6.97.A0.E5.A3.B0)
    *   [8.14 Intel 板载声卡耳机无声](#Intel_.E6.9D.BF.E8.BD.BD.E5.A3.B0.E5.8D.A1.E8.80.B3.E6.9C.BA.E6.97.A0.E5.A3.B0)
    *   [8.15 消除耳机电流声的方法](#.E6.B6.88.E9.99.A4.E8.80.B3.E6.9C.BA.E7.94.B5.E6.B5.81.E5.A3.B0.E7.9A.84.E6.96.B9.E6.B3.95)
    *   [8.16 安装支持 S/PDIF 输出的显卡后无声](#.E5.AE.89.E8.A3.85.E6.94.AF.E6.8C.81_S.2FPDIF_.E8.BE.93.E5.87.BA.E7.9A.84.E6.98.BE.E5.8D.A1.E5.90.8E.E6.97.A0.E5.A3.B0)
    *   [8.17 音效差或卡顿](#.E9.9F.B3.E6.95.88.E5.B7.AE.E6.88.96.E5.8D.A1.E9.A1.BF)
    *   [8.18 开始或停止音频播放时出现噪音](#.E5.BC.80.E5.A7.8B.E6.88.96.E5.81.9C.E6.AD.A2.E9.9F.B3.E9.A2.91.E6.92.AD.E6.94.BE.E6.97.B6.E5.87.BA.E7.8E.B0.E5.99.AA.E9.9F.B3)
    *   [8.19 S/PDIF 输出无效](#S.2FPDIF_.E8.BE.93.E5.87.BA.E6.97.A0.E6.95.88)
    *   [8.20 HDMI 输出无效](#HDMI_.E8.BE.93.E5.87.BA.E6.97.A0.E6.95.88)
    *   [8.21 HDMI多通道PCM输出无法工作(Intel)](#HDMI.E5.A4.9A.E9.80.9A.E9.81.93PCM.E8.BE.93.E5.87.BA.E6.97.A0.E6.B3.95.E5.B7.A5.E4.BD.9C.28Intel.29)
    *   [8.22 HP TX2500](#HP_TX2500)
    *   [8.23 播放 MP3 时有声音跳跃](#.E6.92.AD.E6.94.BE_MP3_.E6.97.B6.E6.9C.89.E5.A3.B0.E9.9F.B3.E8.B7.B3.E8.B7.83)
    *   [8.24 使用USB头戴设备和外接USB声卡](#.E4.BD.BF.E7.94.A8USB.E5.A4.B4.E6.88.B4.E8.AE.BE.E5.A4.87.E5.92.8C.E5.A4.96.E6.8E.A5USB.E5.A3.B0.E5.8D.A1)
        *   [8.24.1 USB设备输出劈啪声](#USB.E8.AE.BE.E5.A4.87.E8.BE.93.E5.87.BA.E5.8A.88.E5.95.AA.E5.A3.B0)
        *   [8.24.2 热插拔USB设备](#.E7.83.AD.E6.8F.92.E6.8B.94USB.E8.AE.BE.E5.A4.87)
    *   [8.25 内核升级后出现'Unknown hardware'错误](#.E5.86.85.E6.A0.B8.E5.8D.87.E7.BA.A7.E5.90.8E.E5.87.BA.E7.8E.B0.27Unknown_hardware.27.E9.94.99.E8.AF.AF)
    *   [8.26 HDA Analyzer](#HDA_Analyzer)
    *   [8.27 ALSA 与 SDL 协同工作的问题](#ALSA_.E4.B8.8E_SDL_.E5.8D.8F.E5.90.8C.E5.B7.A5.E4.BD.9C.E7.9A.84.E9.97.AE.E9.A2.98)
    *   [8.28 Low Sound Workaround](#Low_Sound_Workaround)
    *   [8.29 暂停后继续播放发出噼叭声](#.E6.9A.82.E5.81.9C.E5.90.8E.E7.BB.A7.E7.BB.AD.E6.92.AD.E6.94.BE.E5.8F.91.E5.87.BA.E5.99.BC.E5.8F.AD.E5.A3.B0)
    *   [8.30 Virtual sound device using snd-aloop](#Virtual_sound_device_using_snd-aloop)
*   [9 配置文件范例](#.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6.E8.8C.83.E4.BE.8B)
*   [10 相关阅读](#.E7.9B.B8.E5.85.B3.E9.98.85.E8.AF.BB)

## 安装

Arch 默认的内核已经通过一套模块提供了 ALSA，不必特别安装。

[udev](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udev (简体中文)")会在系统启动时自动检测硬件，并加载相应的声音设备驱动模块。这时，你的声卡已经可以工作了，只是所有声道默认都被设置成静音了。

### 用户权限

一般情况下，本地用户（通过虚拟终端或登录管理器）有权限播放音频和改变音频的音质。

要让远程登录的用户拥有这些权限，必须把用户[加入](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E7.94.A8.E6.88.B7.E7.BB.84.E7.AE.A1.E7.90.86 "Users and groups (简体中文)") `audio` 用户组。

**注意:** 该组的成员可以直接访问声音设备，会导致某些程序独占音频输出。这会让软件混音或快速用户切换无法工作。因此，除非真的有某些[特殊需求](https://wiki.ubuntu.com/Audio/TheAudioGroup)，**不建议**把用户加入 `audio` 用户组。

### ALSA 工具

[安装](/index.php/Pacman "Pacman") 软件包 [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils)，其中包含的 `alsamixer` 工具允许用户在控制台或终端中配置声音设备。 如果你需要 [高质量重采样](#.E9.AB.98.E8.B4.A8.E9.87.8F.E9.87.8D.E9.87.87.E6.A0.B7) 、 [#上混和缩混](#.E4.B8.8A.E6.B7.B7.E5.92.8C.E7.BC.A9.E6.B7.B7)和其他高级特性的话 ，请另外安装 [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) 软件包。

### OSS 兼容性

**注意:** 如果你的应用抱怨说缺少`/dev/dsp`或者`/dev/snd/seq`，这一部分很重要

ALSA能够截获[OSS](/index.php/OSS "OSS")调用，然后转而在ALSA中重新发送他们。例如，对于试图打开`/dev/dsp`并向里面写入声音数据的传统应用，这个模仿层很有用。没有OSS或者这个模仿库的话，会缺少`/dev/dsp`，应用程序从而不会产生任何声音。

如果你希望[OSS](/index.php/OSS "OSS")应用和[dmix](#.E7.BC.A9.E6.B7.B7)一起工作，也安装[alsa-oss](https://www.archlinux.org/packages/?name=alsa-oss)。然后载入`snd-seq-oss`， `snd-pcm-oss` 和 `snd-mixer-oss` [核心模块](/index.php/Kernel_modules_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel modules (简体中文)") 来激活OSS模仿。

### PulseAudio compatibility

[apulse](https://aur.archlinux.org/packages/apulse/) lets you use ALSA for applications that support only [PulseAudio](/index.php/PulseAudio "PulseAudio") for sound. Usage is simply `$ apulse *yourapplication*`.

### ALSA 和 Systemd

[alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) 软件包提供了 [systemd](/index.php/Systemd "Systemd") unit 配置文件 `alsa-restore.service` 和 `alsa-state.service`。

这两个服务会在安装的时候自动启用，不需要额外的操作。可以通过 `systemctl` 检查服务的状态。

**Note:** ALSA 将设置保存在 `/var/lib/alsa/asound.state`

### ALSA Firmware

[alsa-firmware](https://www.archlinux.org/packages/?name=alsa-firmware) 软件包提供了一些声卡需要的固件，比如 Creative SB0400 Audigy2 就需要此软件包。

## 解除各声道的静音

目前版本的 ALSA 安装后，所有声道**默认是静音的**，必须手动解除。

使用 `alsamixer` 的 ncurses 界面，配置十分简单：

```
$ alsamixer

```

此外，还可以在命令行下使用 `amixer`：

```
$ amixer sset Master unmute

```

在 `alsamixer` 中，下方标有 `MM` 的声道是静音的，而标有 `00` 的通道已经启用。

使用 `←` 和 `→` 方向键，选中 `Master` 和 `PCM` 声道。按下 `m` 键解除静音。使用 `↑` 方向键增加音量，直到增益值为`0`。该值显示在左上方 `Item:` 字段后。过高的增益值会导致声音失真。

要想得到完整的 5.1 或 7.1 环绕立体声，还得解除 Front、Surround、Center、LFE (subwoofer) 和 Side 这些声道的静音（上述名称是 Intel HD Audio 声卡使用的声道名，可能因设备不同而有所差异）。注意，仅有这些设置，系统不会自动将立体声源（多数音乐）提升（upmix）成环绕立体声。如果需要这些功能，请阅读[#上混和缩混](#.E4.B8.8A.E6.B7.B7.E5.92.8C.E7.BC.A9.E6.B7.B7)。

要启用麦克风，切换至 Capture 选项卡，按下 `F4`，按下 `空格` 启用其中一个声道即可。

按下 `Esc` 键退出 alsamixer。

**注意:**

*   有一些声卡，需要关闭数字输出或将其调成静音，才能输出模拟音频信号。对于 Soundblaster Audigy LS 声卡，需要把 IEC958 通道设成静音。
*   有些机器（如 Thinkpad T61），有一个 Speaker 通道，必须按照上述方法打开调整。
*   有些机器（如 Dell E6400），可能还需要把 `Front` 和 `Headphone` 声道打开调整。
*   华硕Asus上网本在xfce4等桌面环境设置请参考[ASUS Eee PC](/index.php/ASUS_Eee_PC "ASUS Eee PC")

### 测试你改变的设置

接下来，测试声卡是否工作：

```
$ speaker-test -c 2

```

根据扬声器的实际情况，调整 `-c` 后的数值。对于 7.1 声道，这个数字是 `8`：

```
$ speaker-test -c 8

```

如果声音输出到了错误的设备，可以试试用 `-D` 参数手动指定。

```
$ speaker-test -D default:PCH -c 8

```

`-D` 的值应该是 PCM 通道的名字，可以通过下面命令获得：

 `$ aplay -L | grep :CARD` 
```
default:CARD=PCH  # 'default:PCH' is the PCM channel name for -D
sysdefault:CARD=PCH
front:CARD=PCH,DEV=0
surround21:CARD=PCH,DEV=0
surround40:CARD=PCH,DEV=0
surround41:CARD=PCH,DEV=0
surround50:CARD=PCH,DEV=0
surround51:CARD=PCH,DEV=0
surround71:CARD=PCH,DEV=0
```

如果没有正常工作，请继续阅读 [#配置](#.E9.85.8D.E7.BD.AE) 以及 [#疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94) 部分。和 [ALSA/Troubleshooting](/index.php/ALSA/Troubleshooting "ALSA/Troubleshooting") 页面。

### 附加注释

*   如果你的系统有多个声卡， 那么你可以按`F6`在它们中切换。

*   Some cards need to have digital output muted or disabled in order to hear analog sound. For the Soundblaster Audigy LS mute the channel labeled `IEC958`.

*   有些机器，（像Thinkpad T61），有`Speaker`通道，此通道必须被解除静音然后调整。

*   有些机器，(像Dell E6400) 可能需要解除`Front` 和 `Headphone` 通道的静音并调整它们。

*   如果重起以后，你的声音调整似乎丢失了，尝试以root运行alsamixer。

## 配置

系统配置文件是 `/etc/asound.conf`, 每个用户的配置文件是 `~/.asoundrc`.

### 基本语法

Alsa 设置文件遵循一个由分级值到参数（键值）的分配的简单语法。下面（修改过的）摘录来自 asoundrc.txt，asoundrc.txt 一般可以在 `alsa-lib` 软件包中或是在[这里](http://www.alsa-project.org/alsa-doc/alsa-lib/conf.html) 取得。

#### 赋值与分隔符

赋值能够定义一个键值的具体值，其中有不同的赋值类型和方式可供使用。

 `简单赋值` 
```
#  使用 # 符号来注释文字，该符号后所有到行尾的符号能够被注释掉。 
key = value  # 句中等号通常可以省略，因为空格也能够被用作分隔符。

key value  # 此句意义与上句 key = value 等同

```

分隔符被用作指示赋值的开始和结束。使用半角符号来当作赋值分隔符是很普遍的现象，不过逗号或是空白字符也是可以使用的。

 `分隔符` 
```
key value0; key valueN;
key value0, key valueN, # 所有赋值操作都是等同意义的
key value0 key valueN

key	
value0
	key		
valueN

```

复合赋值使用分号来当作分隔符。

 `复合赋值` 
```
key {	subkey0 value0;
	subkeyN valueN;	} 

key.subkey0 value0; # 与上述语句意义相同
key.subkeyN valueN;

```

出于便于阅读的考虑，我们推荐使用第一种方式来定义三种以上的参数。

序列定义使用中括号当作分隔符。

 `单列` 
```
key [	"value0";
	"valueN";	]

key.0 "value0"; # 与上述语句意义相同
key.N "valueN";

```

不同风格的设置都取决于使用者的偏好，但是为了统一经验规则，我们必须避免的是在一个配置文件中混合多种不同的赋值风格。更多的基础设置能够在 [这里](http://www.volkerschatz.com/noise/alsa.html#basicconf) 找到。

#### 数据类型

对于不同参数值 Alsa 使用的不同的数据类型, 这些肯定会在设置文件中见到。 一些键值接受多种数据类型。 一个包含所有选项可用数据类型的PCM插件设置文件能够在[这里](http://www.alsa-project.org/alsa-doc/alsa-lib/pcm_plugins.html) 找到。

#### 操作模式

对parsing nodes有许多操作模式, 其默认模式为 merge 和 create。如果操作模式为merge/create或是merge类型的话，那么检查就完成了。只有同样的类型的变量能够被合并，举例来说，一个字符串不能与整形数合并。在默认操作模式中尝试定义一个简单变量到一个复杂变量是没有作用的，反之亦然。

操作模式前缀符号:

*   "+" -- merge and create
*   "-" -- merge
*   "?" -- 不要覆盖
*   "!" -- 覆盖

 `操作模式` 
```
# Merge/create - 如果不存在node,它将被创建. 如果其存在并且类型符合,
# subkeyN is merged into key.
key.subkeyN valueN;

# Merge/create - 与上面相同
key.+subkeyN valueN;

# Merge - 节点 key.subkeyN 必须已经存在同时拥有相同类型
key.-subkeyN valueN;

# 不要覆盖 - 如果 key.subkeyN 节点已经存在，便忽略新设定
key.?subkeyN valueN;

# 覆盖 - 移除 subkeyN 及其以下所有值, 然后创建节点 key.subkeyN
key.!subkeyN valueN;

```

使用覆盖操作模式, 如果被正确执行的话,通常来说是安全的, 但是每个人都应记在心中的是, 在一个节点中也许会有正确执行的必须值。

**警告:** 覆盖 pcm 节点通常来说会使 alsa 无法使用, 因为所有插件定义都会被删除。 因此 **不要使用 !pcm.key** ，除非你在scratch中设定设置。

##### 使用“默认”节点的默认设备设定示例

假设 "默认" 节点设定在 /usr/share/alsa/alsa.conf, where defaults.pcm.card and its ctl counterpart have assignment values "0" (type integer), user wants to set default pcm and control device to (third) sound card "2" or "SB" for an Azalia sound card.

 `Defaults node` 
```
defaults.ctl.card 2; # Sets default device and control to third card (counting begins with 0).
defaults.pcm.card 2; # This does not change addressing type.

defaults.ctl.+card 2; # Equivalent to above.
defaults.pcm.+card 2;

defaults.ctl.-card 2; # Same effect on a default setup, however if defaults node was removed or
defaults.pcm.-card 2; # type has been changed merge operation mode will result in no changes.

defaults.pcm.?card 2; # This does nothing, since this assignment already exists.
defaults.ctl.?card 2;

defaults.pcm.!card "SB"; # The override operation mode is necessary here, because of
defaults.ctl.!card "SB"; # different value types.

```

Using double quotes here automatically sets values data type to string, so in the above example setting defaults.pcm.!card "2" would result in retaining last default device, in this case card 0\. Using double quotes for strings is not mandatory as long as no special characters are used, which ideally should never be the case. This may be irrelevant in other assignments.

**Note:** From a configuration point of view those are not equivalent to setting a compound "default" pcm device, since most users specify addressing type in there also, which actually may be the same, but the assignment itself still differs. Also defaults.pcm.card is referred to multiple times in alsa configuration files, usually as a fallback assignment, where different environment variables take precedence.

#### 嵌套

嵌套在配置中是一件很有效的方式。

 `嵌套 pcm 插件` 
```
pcm.azalia {	type hw; card 0	}
pcm.!default {	type plug; slave.pcm "azalia"	}

# 等于

pcm.!default {	type plug; slave.pcm {	type hw; card 0;	}	}

# 也等于

pcm.!default.type plug;
pcm.default.slave.pcm.type hw;            
pcm.default.slave.pcm.card 0;

```

#### 引用配置文件

 `引用其他的外部配置文件` 
```
</path/to/configuration-file> # 引用一个配置文件
<confdir:/path/to/configuration-file> # 全局配置目录的引用

```

### 设置默认声卡

如果发现开机时声卡次序会发生变化，可以在通过 `/etc/modprobe.d` 中的 `.conf` 文件（比如 `/etc/modprobe.d/alsa-base.conf`）手动设置次序。 比如，要让 mia 声卡成为 #0、Intel HDA 声卡成为 #1：

 `/etc/modprobe.d/alsa-base.conf` 
```
options snd slots=snd_mia,snd_hda_intel
options snd_mia index=0
options snd_hda_intel index=1
```

使用命令`$ cat /proc/asound/modules` 来获得当前已经载入的声音模块及其参数。这个列表通常对于载入序列来说就是全部所需的了。使用 `$ lsmod | grep snd`来获得设备和模块的列表。这个设置假设你有一个使用着 `snd_mia` 的mia声卡 和 一个使用着 `snd_hda_intel` 的声卡。

如果使用 -2 的 index 值，ALSA 就不会将对应的设备作为主声卡使用。Linux Mint 和 Ubuntu 等发行版使用了以下配置，避免 USB 声卡和其他“非主流”设备变成 index 为 0 的主声卡：

 `/etc/modprobe.d/alsa-base.conf` 
```
options bt87x index=-2
options cx88_alsa index=-2
options saa7134-alsa index=-2
options snd-atiixp-modem index=-2
options snd-intel8x0m index=-2
options snd-via82xx-modem index=-2
options snd-usb-audio index=-2
options snd-usb-caiaq index=-2
options snd-usb-ua101 index=-2
options snd-usb-us122l index=-2
options snd-usb-usx2y index=-2
# Keep snd-pcsp from being loaded as first soundcard
options snd-pcsp index=-2
# Keep snd-usb-audio from beeing loaded as first soundcard
options snd-usb-audio index=-2
```

以上配置会在系统重启后生效。

当载入被多个卡（比如，snd-hda-intel）使用的模块时，推荐您加入供应商和设备认证信息到选项中。为了获得 `vid` 和 `pid` 信息，使用以下命令：

 `$ lspci -nn | grep -i audio` 
```
00:14.2 Audio device [0403]: Advanced Micro Devices, Inc. [AMD/ATI] SBx00 Azalia (Intel HDA) [1002:4383] (rev 40)
01:00.1 Audio device [0403]: Advanced Micro Devices, Inc. [AMD/ATI] RV770 HDMI Audio [Radeon HD 4850/4870] [1002:aa30]
07:05.0 Multimedia audio controller [0401]: VIA Technologies Inc. VT1720/24 [Envy24PT/HT] PCI Multi-Channel Audio Controller [1412:1724] (rev 01)

```

Last numbers in square brackets are `[vid:pid]`, so for the above example, for setting Azalia as default card following is correct:

 `/etc/modprobe.d/alsa-base.conf` 
```
# SB [HDA ATI SB]
options snd-hda-intel index=0 model=auto vid=1002 pid=4383
# HDMI [HDA ATI HDMI]
options snd-hda-intel index=1 model=auto vid=1002 pid=aa30
# HiFi [Audiotrak Prodigy 7.1 HiFi]
options snd-ice1724 index=2 model=prodigy71hifi vid=1412 pid=1724

```

#### 使用环境变量选择默认PCM设备

**Tip:** An explanation of the terminology of a "card", "device", "subdevice" (a "card" is not a "device") and "PCM" can be found on [wikipedia:Advanced Linux Sound Architecture#Concepts](https://en.wikipedia.org/wiki/Advanced_Linux_Sound_Architecture#Concepts "wikipedia:Advanced Linux Sound Architecture").

在你的设置文件中，最好是以全局方式加入以下命令:

```
 pcm.!default {
   type plug
   slave.pcm {
     @func getenv
     vars [ ALSAPCM ]
     default "hw:Audigy2"
   }
 }

```

你需要将 default 替换成你自己的声卡名，(本例中是`Audigy2`）。你可以使用`aplay -l`或是像**surround51**一样的PCM通用设定。不过，如果你需要使用麦克风的话，选择全双工PCM声卡为默认设备是个不错的选择。

选择你能够启动选择声卡的软件，通过其改变环境变量 `ALSAPCM`。对于那些不允许选择声卡的程序，这样的机制运行得很好，而对于其他的程序你需要确保你选择的是默认声卡。 举例来说，假设你给一个缩混PCM命名为 **mix51to20**，那么你就能够在`mplayer`中使用命令行`ALSAPCM=mix51to20 mplayer example_6_channel.wav`来调用它。

为了替代使用新的变量，你能够在全局默认设定中使用选择以下的变量名：

 `/etc/share/alsa/alsa.conf:` 
```
变量名 # 定义
ALSA_CARD # pcm.default pcm.hw pcm.plughw ctl.sysdefault ctl.hw rawmidi.default rawmidi.hw hwdep.hw
ALSA_CTL_CARD # ctl.sysdefault ctl.hw
ALSA_HWDEP_CARD # hwdep.default hwdep.hw
ALSA_HWDEP_DEVICE # hwdep.default hwdep.hw
ALSA_PCM_CARD # pcm.default pcm.hw pcm.plughw
ALSA_PCM_DEVICE # pcm.hw pcm.plughw
ALSA_RAWMIDI_CARD # rawmidi.default rawmidi.hw
ALSA_RAWMIDI_DEVICE # rawmidi.default rawmidi.hw
```

**Note:** 请注意默认地址类型。

#### 另外一种方式

**提示：** This process can be partly automated using [asoundconf](https://aur.archlinux.org/packages/asoundconf/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

首先，运行 `aplay -l`，获取声卡的声卡ID和设备ID：

 `$ aplay -l` 
```
**** List of PLAYBACK Hardware Devices ****
card 0: Intel [HDA Intel], device 0: CONEXANT Analog [CONEXANT Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: Intel [HDA Intel], device 1: Conexant Digital [Conexant Digital]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: JamLab [JamLab], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 2: Audio [Altec Lansing XT1 - USB Audio], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0

```

**Warning:** Simply setting a `type hw` as default card is equivalent to addressing hardware directly, which leaves the device unavailable to other applications. This method is only recommended if it is a part of a more sophisticated setup `~/.asoundrc` or if user deliberately wants to address sound card directly (digital output through `eic958` or dedicated music server for example).

拿输出中的最后一项来说，这个声卡的声卡ID为2，设备ID为0。若要把这块声卡作为默认声卡，可以把下列配置添加到系统级别的 `/etc/asound.conf` 或用户级别的 `~/.asoundrc` 文件。如果文件不存在，可以手动创建。其中的各个ID，请根据实际情况调整：

```
pcm.!default {
	type hw
	card 2
}

ctl.!default {
	type hw           
	card 2
}

```

**Note:** For the Asus U32U serie it seems that card should be set to 1 for both pcm and ctl.

在大部分情况下，推荐您使用声卡名来代替数字形式的参考名，同时这也能够解决启动顺序的问题。因此下面所示配置对上面所示的示例通常是正确的。

```
pcm.!default {
	type hw
	card Audio
}

ctl.!default {
	type hw           
	card Audio
}

```

为了获得卡的名称，任选一个下面的命令：

```
$ aplay -l | awk -F \: '/,/{print $2}' | awk '{print $1}' | uniq
$ cat /proc/asound/card*/id
```

```
Intel
JamLab
Audio
```

Alternatively use *cat*, which might return unused devices:

 `$ cat /proc/asound/card*/id` 
```
PCH
ThinkPadEC

```

**Note:** 这种方法在有多个相同(alsa)名字的声卡的时候很可能会出现问题。

The 'pcm' options affect which card and device will be used for audio playback while the 'ctl' option affects which card is used by control utilities like alsamixer .

The changes should take effect as soon as you (re-)start an application (MPlayer etc.). You can also test with a command like *aplay*.

```
$ aplay -D default:PCH *your_favourite_sound.wav*

```

If you receive an error regarding your asound configuration, check the [upstream documentation](http://www.alsa-project.org/main/index.php/Asoundrc#The_default_plugin) for possible changes to the config file format.

Simply setting a `type hw` as default card is equivalent to addressing hardware directly, which leaves the device unavailable to other applications. This method is only recommended if it is a part of a more sophisticated setup `~/.asoundrc` or if user deliberately wants to address sound card directly (digital output through `eic958` or dedicated music server for example).

### 确认所有声音模块都已经加载

一般 udev 都会自动识别出声卡。使用以下命令确认：

 `$ lsmod | grep '^snd' | column -t` 
```
snd_hda_codec_hdmi     22378   4
snd_hda_codec_realtek  294191  1
snd_hda_intel          21738   1
snd_hda_codec          73739   3  snd_hda_codec_hdmi,snd_hda_codec_realtek,snd_hda_intel
snd_hwdep              6134    1  snd_hda_codec
snd_pcm                71032   3  snd_hda_codec_hdmi,snd_hda_intel,snd_hda_codec
snd_timer              18992   1  snd_pcm
snd                    55132   9  snd_hda_codec_hdmi,snd_hda_codec_realtek,snd_hda_intel,snd_hda_codec,snd_hwdep,snd_pcm,snd_timer
snd_page_alloc         7017    2  snd_hda_intel,snd_pcm

```

如果你的输出和上面类似，那就说明声卡已经被正确识别。

**注意:** 从[udev](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udev (简体中文)")的171版本开始，默认情况下 OSS 仿真模块（`snd_seq_oss`、`snd_pcm_oss`、`snd_mixer_oss`）不再自动加载。如有需要，请[手动加载](/index.php/Kernel_modules_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel modules (简体中文)")。

还可以检查一下 `/dev/snd/` 目录，看看是否有这些设备文件：

 `$ ls -l /dev/snd` 
```
total 0
crw-rw----  1 root audio 116,  0 Apr  8 14:17 controlC0
crw-rw----  1 root audio 116, 32 Apr  8 14:17 controlC1
crw-rw----  1 root audio 116, 24 Apr  8 14:17 pcmC0D0c
crw-rw----  1 root audio 116, 16 Apr  8 14:17 pcmC0D0p
crw-rw----  1 root audio 116, 25 Apr  8 14:17 pcmC0D1c
crw-rw----  1 root audio 116, 56 Apr  8 14:17 pcmC1D0c
crw-rw----  1 root audio 116, 48 Apr  8 14:17 pcmC1D0p
crw-rw----  1 root audio 116,  1 Apr  8 14:17 seq
crw-rw----  1 root audio 116, 33 Apr  8 14:17 timer

```

**注意:** 在 IRC 或论坛寻求这方面帮助时，别忘了贴出上面几个命令的输出。

如果你的输出跟上面类似，或至少有 **controlC0** 和 **pcmC0D0p**，那么声卡就已经正常加载了。

如果出现问题，声卡模块没有正确加载，那么请尝试手动加载模块：

*   确定声卡对应的驱动模块：[ALSA Soundcard Matrix](http://www.alsa-project.org/main/index.php/Matrix:Main)。这些模块都会有一个”snd-“前缀（例如：`snd-via82xx`）。
*   [加载模块](/index.php/Kernel_modules_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel modules (简体中文)")。
*   检查 `/dev/snd` 目录中的设备文件（参见上文）；或者，检查 `alsamixer` 或 `amixer` 的输出是否正确。
*   修改配置，使 `snd-<模块名>` 和 `snd-pcm-oss` 模块[开机自动加载](/index.php/Kernel_modules_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel modules (简体中文)")。

### 启用 SPDIF 输出

[S/PDIF](https://en.wikipedia.org/wiki/S/PDIF "wikipedia:S/PDIF") is a digital audio interface often used to connect a computer to a digital amplifier (such as a home theatre with 5.1/7.1 surround sound).

**Note:** With some soundcards this disables analog sound output (eg. Audigy2).

*   在 `~/.xinitrc` 中加入下面一行:

```
amixer -c 0 cset name='IEC958 Playback Switch' on

```

使用以下命令，获取你的声卡的数字输出的名称：

```
 $ amixer scontrols

```

### 系统级均衡器

#### 使用 AlsaEqual（包含界面）

从 [AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)") 安装 [alsaequal](https://aur.archlinux.org/packages/alsaequal/)。

安装后，把下列内容添加到 ALSA 配置文件（`~/.asoundrc` 或 `/etc/asound.conf`）：

```
ctl.equal {
 type equal;
}

pcm.plugequal {
  type equal;
  # Modify the line below if you do not
  #slave.pcm "plughw:0,0";
  #by default we want to play from more sources at time:
  slave.pcm "plug:dmix";
}
#pcm.equal {
  # If you do not want the equalizer to be your
  # default soundcard comment the following
  # line and uncomment the above line. (You can
  # choose it as the output device by addressing
  # it with specific apps,eg mpg123 -a equal 06.Back_In_Black.mp3)
pcm.!default {
  type plug;
  slave.pcm plugequal;
}

```

如果使用的是64位系统，而又安装了32位的 Flash 插件，这里的设置会导致 Flash 无声。you have to specify the sound card manually in the line `pcm "hw:0,0"` (use `aplay -l` to list the available sound card and relative card and device number):

 `/etc/asound.conf` 
```
pcm.dmixer {
    type dmix
    ipc_key 2048
    slave {
        pcm "hw:0,0"
        buffer_size 16384
    }
}

ctl.equal {
    type equal;
}

pcm.equalizer {
    type equal
    slave.pcm "plug:dmixer"
}

pcm.!default {
    type plug
    slave.pcm equalizer
}
```

设置好后，切换均衡器：

```
$ alsamixer -D equal

```

需要注意，每个用户的 alsaequal 配置文件都是独立的，位于 `~/.alsaequal.bin`。因此，如果想在 [mpd](/index.php/Mpd "Mpd") 之类的以独立用户身份运行的程序中使用 AlsaEqual，就得像下面这样：

```
# su mpd -c 'alsamixer -D equal'

```

或者，在其他用户的主目录下创建符号链接，指向你的 `.alsaequal.bin`……

##### 管理 AlsaEqual 配置

从 [Xyne 的软件仓库](http://xyne.archlinux.ca/repos/) 或 [AUR](https://aur.archlinux.org/packages.php?ID=62420) 安装 [alsaequal-mgr](http://xyne.archlinux.ca/projects/alsaequal-mgr/)。

同上，配置均衡器：

```
$alsamixer -D equal

```

如果对效果感到满意，将其命名（如“foo”）并保存该配置：

```
$alsaequal-mgr save foo

```

重新加载“foo”中的配置：

```
$alsaequal-mgr load foo

```

这样，就可以为游戏、电影、不同音乐流派、网络电话等等创建不同的均衡器配置，以便随时切换。

参见[项目主页](http://xyne.archlinux.ca/projects/alsaequal-mgr/)和程序的帮助信息，了解更多设置。

#### 使用 mbeq

**注意:** 该软件用到了一个 ladspa 插件，可能导致播放音频时 CPU 占用率偏高。In addition, this was made with stereophonic sound (e.g. headphones) in mind.

安装 [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins)、[ladspa](https://www.archlinux.org/packages/?name=ladspa) 和 [swh-plugins](https://www.archlinux.org/packages/?name=swh-plugins) 软件包。

*   在 `~/.asoundrc` 或 `/etc/asound.conf` 中添加如下内容：

 `/etc/asound.conf` 
```
pcm.eq {
  type ladspa

  # The output from the EQ can either go direct to a hardware device
  # (if you have a hardware mixer, e.g. SBLive/Audigy) or it can go
  # to the software mixer shown here.
  #slave.pcm "plughw:0,0"
  slave.pcm "plug:dmix"

  # Sometimes you may need to specify the path to the plugins,
  # especially if you have just installed them.  Once you have logged
  # out/restarted this should not be necessary, but if you get errors
  # about being unable to find plugins, try uncommenting this.
  #path "/usr/lib/ladspa"

  plugins [
    {
      label mbeq
      id 1197
      input {
        #this setting is here by example, edit to your own taste
        #bands: 50hz, 100hz, 156hz, 220hz, 311hz, 440hz, 622hz, 880hz, 1250hz, 1750hz, 25000hz,
        #50000hz, 10000hz, 20000hz
        controls [ -5 -5 -5 -5 -5 -10 -20 -15 -10 -10 -10 -10 -10 -3 -2 ]
      }
    }
  ]
 }

 # Redirect the default device to go via the EQ - you may want to do
 # this last, once you are sure everything is working.  Otherwise all
 # your audio programs will break/crash if something has gone wrong.

 pcm.!default {
  type plug
  slave.pcm "eq"
 }

 # Redirect the OSS emulation through the EQ too (when programs are running through "aoss")

 pcm.dsp0 {
  type plug
  slave.pcm "eq"
 }

```

*   完成。若有问题，欢迎前往论坛咨询。

## 高质量重采样

启用软件混音时，ALSA 会强制把所有音频重采样到相同的频率（如果系统支持，默认是 48000）。dmix 的重采样算法很糟糕，会导致显著的质量损失。

安装 [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) 和 [libsamplerate](https://www.archlinux.org/packages/?name=libsamplerate)。

将默认的采样率转换器更改为 libsamplerate：

 `/etc/asound.conf`  `defaults.pcm.rate_converter "samplerate_best"` 

或：

 `~/.asoundrc`  `defaults.pcm.rate_converter "samplerate_best"` 

**samplerate_best** 输出的声音质量最佳，但需要耗费大量CPU资源进行实时重采样。还有其他的算法可供选择（如 **samplerate** 等），但比起默认的算法，这些算法的改进并不明显。

**警告:** 某些系统中，启用 samplerate_best 可能导致 Flash 播放器无声音。

## 上混和缩混

**注意:** 由于未找到 upmix 和 downmix 的常用翻译，译者暂时采用字面翻译（上混、缩混）。所谓“上混”，即将声道较少的立体声（如常见的双声道立体声）信号，通过软件或硬件处理，模拟为声道较多的立体声（如5.1环绕立体声）信号。反之即为“缩混”。

### 上混（upmixing）

播放双声道立体声音源（如音乐）时，利用上混，即可充分利用 5.1 或 7.1 环绕立体声的所有声道。以前，上混很麻烦，还经常出错。但如今就方便多了，只需要安装一些插件即可。这些插件由 [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) 软件包提供。

安装后，在配置文件（`/etc/asound.conf` 或 `~/.asoundrc`）中添加如下内容：

```
pcm.upmix71 {
    type upmix
    slave.pcm "surround71"
    delay 15
    channels 8
}

```

该范例适用于7.1声道上混。类比该范例，同样能设置5.1或4.0声道上混。

该设置添加了一个新的用于上混的 pcm。如果希望所有音频源都通过该 pcm 输出，在上述设置后添加如下配置即可：

```
pcm.!default "plug:upmix71"

```

插件默认配置就允许多个音频源同时通过它输出，一般无需额外配置。如果不行，就得向下面这样为上混配置 dmixer：

```
pcm.dmix6 {
    type asym
    playback.pcm {
        type dmix
        ipc_key 567829
        slave {
            pcm "hw:0,0"
            channels 6
        }
    }
}

```

注意要用 dmix6 而非 surround71。

如果遇到声音卡顿或混乱，可能需要增加 buffer_size（比如增加到 32768），或使用[高质量重采样](#.E9.AB.98.E8.B4.A8.E9.87.8F.E9.87.8D.E9.87.87.E6.A0.B7)。

### 缩混（downmixing）

有时也会用到缩混，比如在只支持双声道立体声的电脑上观看5.1声道的电影时。这一功能由 ALSA 插件 vdownmix 实现（同样在 [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) 软件包里）。

在配置文件中添加如下内容：

```
pcm.!surround51 {
    type vdownmix
    slave.pcm "default"
}
pcm.!surround40 {
    type vdownmix
    slave.pcm "default"
}

```

**Note:** 如果这不能让 缩混 工作，请参见 [[1]](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=541786) 。所以，你也许需要添加 `pcm.!default "plug:surround51"` 或是 `pcm.!default "plug:surround40"`。只有一个 `vdownmix` 插件能够使用；如果你有7.1声道音响，你需要使用 `surround71` 来代替上面所述的配置文件。一个让 `vdownmix` 和 `dmix` 同时工作的配置文件的示例可以在 [这里](https://bbs.archlinux.org/viewtopic.php?id=167275) 找到。

## 混音

Mixing enables multiple applications to output sound at the same time. Most discrete sound cards support hardware mixing, which is enabled by default if available. Integrated motherboard sound cards (such as Intel HD Audio), usually do not support hardware mixing. On such cards, software mixing is done by an ALSA plugin called dmix. This feature is enabled automatically if hardware mixing is unavailable.

### 手动启用 dmix

**注意:** 在 ALSA 1.0.9rc2 及以上版本中，如果声卡不支持硬件混音，模拟输出将默认使用 dmix 混音，无需额外设置。

要手动启用，那么可以创建 `~/.asoundrc`，加入以下内容：

```
pcm.dsp {
    type plug
    slave.pcm "dmix"
}

```

这样就启用了软件混音，多个程序能够同时使用声卡。如果不能，尝试用上述内容来替换 /etc/asound.conf 中的所有内容.

至于 S/PDIF 之类的数字音频输出，目前的 ALSA 还不会默认启用 dmix。因此，必须像上面这样手动启用。

常见问题的解答，参见[#疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)部分。

## 提示和技巧

### USB声卡热插拔

参见 [Writing Udev rules for ALSA](http://alsa.opensrc.org/Udev).

### 同时输出

你可能会希望同时使用一个用mini jack连接的外置扬声器和内置扬声器同时播放一个音乐。这个可以同时使用`alsamixer` 或 `amixer`解静音**Auto-Mute**来实现：

```
$ amixer sset "Auto-Mute" unmute

```

然后解静音其他需要的项目, 比如 **Headphones**, **Speaker**, **Bass Speaker**...

**注意:** 如果之后你在耳机连接器(mini-jack)中听到劈里啪啦的声音，参见 [这里](/index.php/ALSA/Troubleshooting#Crackling_sound_through_mini-jack_.28headphones_connector.29 "ALSA/Troubleshooting").

### 键盘控制声音

将下列命令映射倒你的声音键: `XF86AudioRaiseVolume`, `XF86AudioLowerVolume`, `XF86AudioMute`

增加音量:

```
amixer set Master 5%+

```

减小音量:

```
amixer set Master 5%-

```

静音/解静音:

```
amixer set Master toggle

```

## 疑难解答

### Audigy 2 ZS 不发出声音

如果你在使用 Audigy 2 ZS 声卡不出声并且尝试alsamixer不成功的时候，推荐你安装 `gnome-alsamixer` 并且取消 "**Audigy Analog/Digital Output Jack**" 选项的勾选状态。

### VirtualBox中无声音

如果你在使用VirtualBox的时候出现了无声的问题，尝试以下命令：

 `$ alsactl init` 
```

Found hardware: "ICH" "SigmaTel STAC9700,83,84" "AC97a:83847600" "0x8086" "0x0000"
Hardware is initialized using a generic method

```

同时你需要在你的音频软件中激活ALSA输出。

### 使用CPU频率动态调整时，音频发生跳跃

使用 `ondemand` 或 `conservative` 频率策略、启用CPU频率动态调整时，某些声卡和某些 ALSA 驱动会出现声音跳跃的情况。目前，唯一的解决方案是使用固定的频率，如 `performance` 性能策略。

详情参见 [CPU frequency scaling (简体中文)](/index.php/CPU_frequency_scaling_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "CPU frequency scaling (简体中文)")。

### 同时只能有一个用户播放音频

有时会出现一个用户独占软件混音器的情况。多数情况下这没什么影响，但在使用 [mpd](/index.php/Mpd "Mpd") 这样以独立用户身份运行的程序时，就会出现问题。当 mpd 运行时，用户自己就无法播放其他音频了。一种解决方法是，以正在使用的用户身份运行 mpd。另一种方法是，在 ALSA 配置文件的 `pcm.dmixer` 部分添加 `ipc_key_add_uid 0` 禁止独占。以下是 `asound.conf` 示例的片段，省略的部分无需修改：

```
...
pcm.dmixer {
 type dmix
 ipc_key 1024
 ipc_key_add_uid 0
 ipc_perm 0660
slave {
...

```

### 无法同时播放多个音频

如果安装了 [PulseAudio](/index.php/PulseAudio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PulseAudio (简体中文)")（可能作为 [GNOME](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)") 的依赖被安装），可能出现无法同步播放的问题，因为 PulseAudio 的默认配置是“独占”声卡。ALSA 的用户可能对自己的配置已经很满意、不希望使用 [PulseAudio](/index.php/PulseAudio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PulseAudio (简体中文)")。解决方案是编辑 `/etc/asound.conf` 并注释掉以下内容：

```
# Use PulseAudio by default
#pcm.!default {
#  type pulse
#  fallback "sysdefault"
#  hint {
#    show on
#    description "Default ALSA Output (currently PulseAudio Sound Server)"
#  }
#}

```

可能还需要注释掉下面的内容：

```
#ctl.!default {
#  type pulse
#  fallback "sysdefault"
#}

```

比起完全卸载 [PulseAudio](/index.php/PulseAudio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PulseAudio (简体中文)")，这大概是个更简单的方法。

以下是 `/etc/asound.conf` 配置文件的一个示例：

```
pcm.dmixer {
        type dmix
        ipc_key 1024
        ipc_key_add_uid 0
        ipc_perm 0660
}
pcm.dsp {
        type plug
        slave.pcm "dmix"
}

```

**注意:** 本 `/etc/asound.conf` 本来是配合 [MPD](/index.php/MPD "MPD") 全局配置使用的。参见[该节](#.E5.90.8C.E6.97.B6.E5.8F.AA.E8.83.BD.E6.9C.89.E4.B8.80.E4.B8.AA.E7.94.A8.E6.88.B7.E6.92.AD.E6.94.BE.E9.9F.B3.E9.A2.91)关于多用户的内容。

### 有时候开机无声

如果会随机地出现开机无声的问题，原因可能是多声卡的顺序发生了变化。如果是这种情况，请参照[#设置默认声卡](#.E8.AE.BE.E7.BD.AE.E9.BB.98.E8.AE.A4.E5.A3.B0.E5.8D.A1)进行设置。

对于 mpd 用户，上述配置无效，请参考[该文](http://mpd.wikia.com/wiki/Configuration#ALSA_MPD_software_volume_control)设置。

### 特定程序的问题

对于不使用系统声音配置的程序，如 XMMS 和 Mplayer，必须特别设置以应用 ALSA 配置。

对于 mplayer，将以下内容添加到 `~/.mplayer/config` （或系统全局配置文件 `/etc/mplayer/mplayer.conf`）：

```
ao=alsa

```

对于 XMMS 和 Beep Media Player，打开选项窗口，要把声音驱动设置为 ALSA 而不是 OSS。

XMMS 的设置方法：

*   启动 XMMS
    *   选项 -> 首选项
    *   选择 Alsa 输出插件

对于未提供 ALSA 输出的程序，可以使用 alsa-oss 软件包中的 aoss 工具启动。使用方法是：在要运行的程序的命令行前加上 `aoss`。例如：

```
aoss realplay

```

pcm.!default{ ... } 貌似已经不管用了。但下面的设置有效：

```
 pcm.default pcm.dmixer

```

### 特定型号的配置

ALSA 会通过 BIOS 检测[声卡型号](http://www.kernel.org/doc/Documentation/sound/alsa/HD-Audio-Models.txt)，少数情况下也可能无法正确识别。声卡芯片类型可以在 `alsamixer` 界面上找到（如 ALC662），而型号则要设置在 `/etc/modprobe.d/modprobe.conf` 或 `/etc/modprobe.d/sound.conf` 文件中：

```
options snd-hda-intel model=<型号>

```

具体设置因声卡型号而异。多数情况下不需要特地这样做。如果想知道具体声卡型号的设置，请查阅 [Alsa Soundcard List](http://bugtrack.alsa-project.org/main/index.php/Matrix:Main)，找到你的声卡型号，点击“Details”，然后查看“Setting up modprobe...”小节，将其中的内容插入 `/etc/modprobe.d/modprobe.conf` 文件即可。例如，Intel AC97 的配置如下：

```
# ALSA portion
alias char-major-116 snd
alias snd-card-0 snd-intel8x0
# module options should go here

# OSS/Free portion
alias char-major-14 soundcore
alias sound-slot-0 snd-card-0

# card #1
alias sound-service-0-0 snd-mixer-oss
alias sound-service-0-1 snd-seq-oss
alias sound-service-0-3 snd-pcm-oss
alias sound-service-0-8 snd-seq-oss
alias sound-service-0-12 snd-pcm-oss
```

### 与蜂鸣器冲突

如果你确认所有声道都已解除静音，声卡驱动配置正确，且音量大小也合适，但还是听不到声音，那么请试试将下面的内容添加到 `/etc/modprobe.d/modprobe.conf`：

（如果是 `via82xx` 驱动）

```
options snd-<模块名请自行补充> ac97_quirk=0

```

（如果是 `snd_intel8x0` 驱动）

```
options snd-NAME-OF-MODULE ac97_quirk=1

```

### 麦克风输入无声音

In alsamixer, make sure that all the volume levels are up under recording, and that CAPTURE is toggled active on the microphone (e.g. Mic, Internal Mic) and/or on Capture (in alsamixer, select these items and press space). Try making positive Mic Boost and raising Capture and Digital levels higher; this make make static or distortion, but then you can adjust them back down once you are hearing *something* when you record

因为在alsaminxer中pulseaudio wapper是默认设置，你也许需要按下F6来选择你的实际使用的声卡。你也许需要在回放环节启用并增大输入的音量。

使用以下命令来测试麦克风 (参考arecord的手册页面获取更多信息):

```
 arecord -d 5 test-mic.wav
 aplay test-mic.wav

```

If all fails, you may want to eliminate hardware failure by testing the microphone with a different device.

For at least some computers, muting a microphone (MM) simply means its input does not go immediately to the speakers. It still receives input.

Many Dell laptops need "-dmic" to be appended to the model name in `/etc/modprobe.d/modprobe.conf`:

```
 options snd-hda-intel model=dell-m6-dmic

```

Some programs use try to use OSS as the main input software. Add the following lines to `/etc/modprobe.d/modprobe.conf` to prevent OSS modules from being loaded:

**Note:** The OSS modules are no longer autoloaded anyway.

```
blacklist snd_pcm_oss
blacklist snd_mixer_oss
blacklist snd_seq_oss

```

See also:

*   [http://www.alsa-project.org/main/index.php/SoundcardTesting](http://www.alsa-project.org/main/index.php/SoundcardTesting)
*   [http://alsa.opensrc.org/Record_from_mic](http://alsa.opensrc.org/Record_from_mic)

### 设置默认的麦克风/录音设备

某些程序（Pidgin、Adobe Flash）提供了设置录音设备的选项。如果录音设备不是内置的声卡，而是外接的（如USB摄像头、麦克风），就会有些问题。如果只想更改默认的录音设备、不更改回放设备，需要像下面这样设置 `~/.asoundrc`：

```
pcm.usb
{
    type hw
    card U0x46d0x81d
}

pcm.!default
{
    type asym
    playback.pcm
    {
        type plug
        slave.pcm "dmix"
    }
    capture.pcm
    {
        type plug
        slave.pcm "usb"
    }
}

```

把“U0x46d0x81d”替换为你的录音设备的名称。可以通过 `arecord -L` 查看所有 ALSA 识别到的录音设备。

### 内置麦克风无效

首先，请检查 alsamixer，确保所有的录音声道的音量都达到可以录制的程度。如果还是不行，试试修改 /etc/sound.conf 并重载 snd-* 模块。这样就会多出来一个名叫 Capture 的音频控制，可以用它调节内置麦克风的音量。例如，对于 snd-hda-intel 模块，配置如下：

```
 options snd-hda-intel enable_msi=1

```

然后，输入下面的命令重载模块，调整音量并测试。

 `# rmmod snd-hda-intel && modprobe snd-hda-intel` 

### Intel 板载声卡无声

可能由两个相互冲突的驱动模块引起，分别是 `snd_intel8x0` 和 `snd_intel8x0m`。如果是的话，屏蔽 snd_intel8x0m 即可：

 `/etc/modprobe.d/modprobe.conf`  `blacklist snd_intel8x0m` 

以下方法可能也有效：在 `alsamixer` 或 `amixer` 把 “External Amplifier” 设置为静音。参见：[ALSA wiki 相关条目](http://alsa.opensrc.org/Intel8x0#Dell_Inspiron_8600_.28and_probably_others.29)。

也可以试试解除“Mix”的静音。

### Intel 板载声卡耳机无声

对于笔记本电脑上的 **Intel Corporation 82801 I (ICH9 Family) HD Audio Controller** 声卡，可能需要添加如下内容到 modprobe 配置文件或 sound.conf，以解决耳机无声的问题：

```
options snd-hda-intel model=$model

```

$model 在下列型号中选择：

*   dell-vostro
*   olpc-xo-1_5
*   laptop
*   dell-m6
*   laptop-hpsense

**注意:** 可能需要在配置文件的 "alias" 语句之后添加上述内容。

可以在内核文档中找到所有支持的型号，如[该文](http://git.kernel.org/?p=linux/kernel/git/stable/linux-2.6.35.y.git;a=blob;f=Documentation/sound/alsa/HD-Audio-Models.txt;h=dc25bb84b83b49665a7ed850e7bf5423d50cd3ba;hb=HEAD)。这是 2.6.35 版本内核的文档，你需要自己查找适用于自己内核版本的文档。

也可以从[这里](http://www.mjmwired.net/kernel/Documentation/sound/alsa/HD-Audio-Models.txt)获取型号列表。要查看你的声卡芯片名称，输入下列命令（其中的“*”请根据实际情况替换）。注意，有些芯片名称被更改过，因此实际名称与文件中的可能不匹配。

```
cat /proc/asound/card*/codec* | grep Codec

```

注意，这么做很可能导致所有输入设备（内置和外置麦克风）无法工作，即要么让麦克风正常、要么让耳机正常。如果遇到这一问题，请向 ALSA 开发者报告。

另外，如果蜂鸣器（pcspkr）出现问题，可以试试使用以下配置修复：

```
options snd-hda-intel model=$model enable=1 index=0

```

### 消除耳机电流声的方法

```
1.终端输入alsamixer回车-输入密码后进入alsa高级控制面板
2.按F5,显示所有音轨,左右键移动音轨,上下键调节音量,将其中的Internal选项的音量设置为00

```

### 安装支持 S/PDIF 输出的显卡后无声

检测已加载的相关模块，并记录顺序：

```
$ cat /proc/asound/modules
0 snd_hda_intel
1 snd_ca0106

```

在 `/etc/modprobe.d/modprobe.conf` 中禁用不希望使用的显卡的音频解码模块：

```
# /etc/modprobe.d/modprobe.conf
#
install snd_hda_intel /bin/false

```

如果不同设备使用同一模块，那么只能在 BIOS 中禁用其中之一。

### 音效差或卡顿

如果发现音效特别差，试试在 alsamixer 中调节一下 PCM 音量，到增益（gain）为0的水平。

若使用 snd-usb-audio 驱动，可以试试在 `/etc/asound.conf` 中启用 `softvol`。下面是针对第一个声音设备的配置范例：

```
 pcm.!default {
   type plug
   slave.pcm "softvol"
 }
 pcm.dmixer {
      type dmix
      ipc_key 1024
      slave {
          pcm "hw:0"
          period_time 0
          period_size 4096
          buffer_size 131072
          rate 50000
      }
      bindings {
          0 0
          1 1
      }
 }
 pcm.dsnooper {
      type dsnoop
      ipc_key 1024
      slave {
          pcm "hw:0"
          channels 2
          period_time 0
          period_size 4096
          buffer_size 131072
          rate 50000
      }
      bindings {
          0 0
          1 1
      }
 }
 pcm.softvol {
      type softvol
      slave { pcm "dmixer" }
      control {
          name "Master"
          card 0
      }
 }
 ctl.!default {
   type hw
   card 0
 }
 ctl.softvol {
   type hw
   card 0
 }
 ctl.dmixer {
   type hw
   card 0
 }

```

### 开始或停止音频播放时出现噪音

某些驱动模块（如 snd_ac97_codec 和 snd_hda_intel）会在声卡闲置时关闭它以节约用电。声卡启动或关闭时，就会发出刺耳的噪音。在调节音量或开关窗口（KDE4）时也可能发生这种情况。要消除这一问题，需要添加特定模块参数（通过 `modinfo snd_MY_MODULE` 查询）关闭该功能。

例如：对于 snd_hda_intel 模块，要禁用自动节电并解决噪音问题，需在 `/etc/modprobe.d/modprobe.conf` 中添加如下内容：

```
options snd_hda_intel power_save=0

```

或：

```
options snd_hda_intel power_save=0 power_save_controller=N

```

可以先使用 `modprobe snd_hda_intel power_save=0` 测试一下效果。

对于 VIA VT1708S 板载声卡（使用 snd_hda_intel 模块）等一些声卡，即使把 power_save 参数设置为0可能仍会有噪音。还得在 alsamixer 中把“Line”声道激活才能生效，只要激活并调到一个非0的音量即可（1即可，不要太高）。

内核模块文档：[[2]](https://www.kernel.org/doc/Documentation/sound/alsa/powersave.txt)

对于笔记本，即使在 `/etc/modprobe.d` 设置了 `power_save` 参数，当切换电池时 pm-utils 仍会将该值重置为1。需要禁用相关的脚步才行（详情参见：[Pm-utils#Disabling a hook](/index.php/Pm-utils#Disabling_a_hook "Pm-utils")）：

```
# touch /etc/pm/power.d/intel-audio-powersave

```

### S/PDIF 输出无效

如果你已经在 alsamixer 中启用相关声道，但声卡的光学/同轴数字输出还是无效，试试以 root 身份运行：

```
# iecset audio on

```

每次开机都需要重新设置。如果嫌麻烦，可以自己写一个 [systemd 服务](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)")。

### HDMI 输出无效

若遇到声卡或主板的HDMI输出无法工作的问题，请首先确认 alsamixer 中的相关声道已经解除静音。如果还是不行，请进行下列操作：

查询回放设备：

```
 $ aplay -l
 **** List of PLAYBACK Hardware Devices ****
 card 0: NVidia [HDA NVidia], device 0: ALC1200 Analog [ALC1200 Analog]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 0: NVidia [HDA NVidia], device 1: ALC1200 Digital [ALC1200 Digital]
   Subdevices: 1/1
   Subdevice #0: subdevice #0
 card 0: NVidia [HDA NVidia], device 3: NVIDIA HDMI [NVIDIA HDMI]
   Subdevices: 0/1
   Subdevice #0: subdevice #0

```

我们需要的是 HDMI 设备的信息，下面来做一个测试（在该例中，0是声卡编号，3是设备编号）：

```
 $ aplay -D plughw:0,3 /usr/share/sounds/alsa/Front_Center.wav

```

如果 aplay 没有给出错误信息，但还是听不到声音，请尝试重启通过HDMI链接的播放设备（显示器或电视）。HDMI接口会在链接时执行一次握手，有可能因为当时没有检测到音频流而禁用了音频解码。特别是，如果使用了独立的窗口管理器（不太清楚 Gnome 和 KDE 的情况），可能就必须一边播放音乐、一边链接HDMI线。

**注意:** 如果你正在使用AMD显卡和3.0版Linux内核，就需要修改启动引导程序（Grub）的内核参数 `radeon.audio=1`，或在 modprobe 的配置文件中添加相关参数。进行上述操作前，请阅读 [Radeon Feature Matrix](http://www.x.org/wiki/RadeonFeature#fndef-72849d6d6eb3927d486f50ece74a739042965a6c-25)，看看你的显卡是否已经被支持。[S. Islands](http://www.x.org/wiki/RadeonFeature#Decoder_ring_for_engineering_vs_marketing_names) 中列举的一些显卡（从HD7750到HD7970）尚不支持 HDMI 音频输出。

若测试成功，接下来编辑或创建 `~/.asoundrc`，把 HDMI 设置为默认音频设备。

 `~/.asoundrc` 
```
pcm.!default {
  type hw
  card 0
  device 3
}

```

如果上述配置无效，试试下面这个：

 `~/.asoundrc` 
```
defaults.pcm.card 0
defaults.pcm.device 3
defaults.ctl.card 0

```

### HDMI多通道PCM输出无法工作(Intel)

As of Linux 3.1 multi-channel PCM output through HDMI with a Intel card (Intel Eaglelake, IbexPeak/Ironlake,SandyBridge/CougarPoint and IvyBridge/PantherPoint) is not yet supported. Support for it has been recently added and expected to be available in Linux 3.2\. To make it work in Linux 3.1 you need to apply the following patches:

*   [drm: support routines for HDMI/DP ELD](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=patch;h=76adaa34db407f174dd06370cb60f6029c33b465)
*   [drm/i915: pass ELD to HDMI/DP audio driver](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=patch;h=e0dac65ed45e72fe34cc7ccc76de0ba220bd38bb)

### HP TX2500

Add these 2 lines into `/etc/modprobe.d/modprobe.conf`:

```
options snd-cmipci mpu_port=0x330 fm_port=0x388
options snd-hda-intel index=0 model=toshiba position_fix=1

```

```
options snd-hda-intel model=hp (works for tx2000cto)

```

### 播放 MP3 时有声音跳跃

如果你在播放MP3文件的时候有声音跳过的情况，同时有超过2个音箱连接到你的电脑上（比如，声道大于2的多声道系统），运行alsamixer并禁用你**没有的**音箱所对应的频道（比如，在没有centre音箱的时候不要启用centre音箱的声音）

### 使用USB头戴设备和外接USB声卡

如果你在ALSA下使用USB头戴设备，那么你可以试试使用 [asoundconf](https://aur.archlinux.org/packages/asoundconf/) （当前只有在[AUR](/index.php/AUR "AUR")内获得）来设置头戴设备为主要声音输出设备。运行前别忘了确认你的USB音频模块已经启用(`modprobe snd-usb-audio`)。

```
# asoundconf is-active
# asoundconf list
# asoundconf set-default-card <chosen soundcard>

```

#### USB设备输出劈啪声

如果你在使用USB设备的时候发出了劈啪声，你可以试试 snd-usb-audio 设置最小时延。 加入下面这条命令到你的 `/etc/modprobe.d/modprobe.conf` 文件中:

```
options snd-usb-audio nrpacks=1

```

source: [http://alsa.opensrc.org/Usb-audio#Tuning_USB_devices_for_minimal_latencies](http://alsa.opensrc.org/Usb-audio#Tuning_USB_devices_for_minimal_latencies)

#### 热插拔USB设备

为了自动设置USB声卡为主要输出设备，在声卡插入以后，你可以使用下面的udev规则（比方说，将下面的两条命令加入到 `/etc/udev/rules.d/00-local.rules` 并重启）。

```
KERNEL=="pcmC[D0-9cp]*", ACTION=="add", PROGRAM="/bin/sh -c 'K=%k; K=$${K#pcmC}; K=$${K%%D*}; echo defaults.ctl.card $$K > /etc/asound.conf; echo defaults.pcm.card $$K >>/etc/asound.conf'"
KERNEL=="pcmC[D0-9cp]*", ACTION=="remove", PROGRAM="/bin/sh -c 'echo defaults.ctl.card 0 > /etc/asound.conf; echo defaults.pcm.card 0 >>/etc/asound.conf'"
```

### 内核升级后出现'Unknown hardware'错误

升级内核后，在启动ALSA的过程中有可能会输出下面的错误信息：

```
Unknown hardware "foo" "bar" ...
Hardware is initialized using a guess method
/usr/sbin/alsactl: set_control:nnnn:failed to obtain info for control #mm (No such file or directory)

```

或是

```
Found hardware: "HDA-Intel" "VIA VT1705" "HDA:11064397,18490397,00100000" "0x1849" "0x0397"
Hardware is initialized using a generic method
/usr/sbin/alsactl: set_control:1328: failed to obtain info for control #1 (No such file or directory)
/usr/sbin/alsactl: set_control:1328: failed to obtain info for control #2 (No such file or directory)
/usr/sbin/alsactl: set_control:1328: failed to obtain info for control #25 (No such file or directory)
/usr/sbin/alsactl: set_control:1328: failed to obtain info for control #26 (No such file or directory)

```

出现这种问题很简单，仅仅需要在 root 账户下再次存储ALSA设定：

```
# alsactl -f /var/lib/alsa/asound.state store

```

有必要使用alsamixer重新设置ALSA

### HDA Analyzer

If the mappings to your audio pins(plugs) do not correspond but ALSA works fine, you could try HDA Analyzer -- a pyGTK2 GUI for HD-audio control can be found [at the ALSA wiki](http://www.alsa-project.org/main/index.php/HDA_Analyzer). 如果映射你的音频 Try tweaking the Widget Control section of the PIN nodes, to make microphones IN and headphone jacks OUT. Referring to the Config Defaults heading is a good idea.

NOTE: the script is done by such way that it is incompatible with python3 (which is now shipped with ArchLinux) but tries to use it. The workaround is: open "run.py", find all occurences of "python" (2 occurences - one on the first line, and the second on the last line) and replace them all by "python2".

NOTE2: the script requires root acces, but running it via su/sudo is bogus. Run it via `kdesu` or `gksu`.

### ALSA 与 SDL 协同工作的问题

如果你使用SDL没有声音同时在应用中无法选择ALSA。试试设定SDL_AUDIODRIVER环境变量到ALSA。

```
# export SDL_AUDIODRIVER=alsa

```

### Low Sound Workaround

If you are facing low sound even after maxing out your speakers/headphones, you can give the softvol plugin a try. Add the following to `/etc/asound.conf`.

```
pcm.!default {
      type plug
      slave.pcm "softvol"
  }

pcm.softvol {
    type softvol
    slave {
        pcm "dmix"
    }
    control {
        name "Pre-Amp"
        card 0
    }
    min_dB -5.0
    max_dB 20.0
    resolution 6
}

```

**Note:** You will probably have to restart the computer, as restarting the alsa daemon did not load the new configuration for me. Also, if the configuration does not work even after restarting, try changing `plug` with `hw` in the above configuration.

After the changes are loaded successfully, you will see a `Pre-Amp` section in alsamixer. You can adjust the levels there.

**Note:** Setting a high value for `Pre-Amp` can cause sound distortion, so adjust it according to the level that suits you.

### 暂停后继续播放发出噼叭声

如果你在暂停后继续播放听到噼叭声，那么你可以通过修改 `/etc/pm/sleep.d/90alsa` 中的 `aplay -d 1 /dev/zero`行来修复错误。

### Virtual sound device using snd-aloop

You might want a jack alternative to create a virtual recording or play device in order to mix different sources, using the snd-aloop module:

```
modprobe snd-aloop

```

List your new virtual devices using:

```
aplay -l

```

now you can for example using ffmpeg:

```
ffmpeg -f alsa -i hw:1,1,0 -f alsa -i hw:1,1,1 -filter_complex amerge output.mp3

```

In the hw:R,W,N format R is your virtual card device number, W 1 recording devices 0 for writing, R is your sub device you can use all the virtual devices available and play/stop using applications like mplayer:

```
mplayer -ao alsa:device=hw=1,0,0 fileA
mplayer -ao alsa:device=hw=1,0,1 fileB 

```

Another thing you could do with this approach, is using festival to generate a voice into a recording stream using an script like this:

```
#!/bin/bash
echo $1|iconv -f utf-8 -t iso-8859-1| text2wave  > "_tmp_.wav";   
mplayer -ao alsa:device=hw=2,0,0 "_tmp.wav";
rm "_tmp.wav";

```

## 配置文件范例

参见：[Advanced Linux Sound Architecture/Example Configurations](/index.php/Advanced_Linux_Sound_Architecture/Example_Configurations "Advanced Linux Sound Architecture/Example Configurations")。

## 相关阅读

*   [ALSA 模块高级配置](http://www.mjmwired.net/kernel/Documentation/sound/alsa/ALSA-Configuration.txt)
*   [非官方的 ALSA Wiki](http://alsa.opensrc.org/Main_Page)
*   [如何从 svn 获取驱动代码并编译](https://bbs.archlinux.org/viewtopic.php?id=36815)
*   [ALSA wiki](http://www.alsa-project.org/)
*   [Asoundrc](http://www.alsa-project.org/main/index.php/Asoundrc/)
*   [Unofficial ALSA wiki](http://alsa.opensrc.org/)
*   [Advanced ALSA module configuration](http://www.mjmwired.net/kernel/Documentation/sound/alsa/ALSA-Configuration.txt)
*   [HOWTO: compile driver from svn](https://bbs.archlinux.org/viewtopic.php?id=36815)
*   [A close look at ALSA: ALSA concept introduction](http://www.volkerschatz.com/noise/alsa.html)
*   [Linux ALSA sound notes](http://www.sabi.co.uk/Notes/linuxSoundALSA.html)