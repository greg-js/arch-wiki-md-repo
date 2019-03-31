Related articles

*   [Bluetooth](/index.php/Bluetooth "Bluetooth")
*   [Bluez4](/index.php/Bluez4 "Bluez4")

**翻译状态：** 本文是英文页面 [Bluetooth_headset](/index.php/Bluetooth_headset "Bluetooth headset") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-08-31，点击[这里](https://wiki.archlinux.org/index.php?title=Bluetooth_headset&diff=0&oldid=396614)可以查看翻译后英文页面的改动。

Arch Linux 现在默认支持 A2DP profile (Audio Sink)，可以实现远程音频播放功能。

**提示：**

*   Bluez5 只能通过 [PulseAudio](/index.php/PulseAudio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PulseAudio (简体中文)") 来支持耳机的录音/播放，不支持 [ALSA](/index.php/Advanced_Linux_Sound_Architecture_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Advanced Linux Sound Architecture (简体中文)")。如果你不想使用 PulseAudio，你需要从 AUR 安装老版本的 Bluez 来支持。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 通过 Bluez5/PulseAudio 支持耳机](#通过_Bluez5/PulseAudio_支持耳机)
    *   [1.1 常见问题及解决方案](#常见问题及解决方案)
        *   [1.1.1 已经选择音频配置，但耳机没有激活，不能重定向音频](#已经选择音频配置，但耳机没有激活，不能重定向音频)
        *   [1.1.2 授权失败导致配对失败](#授权失败导致配对失败)
        *   [1.1.3 配对成功, 但连接失败](#配对成功,_但连接失败)
        *   [1.1.4 连接成功，但不能播放声音](#连接成功，但不能播放声音)
        *   [1.1.5 UUIDs has unsupported type](#UUIDs_has_unsupported_type)
*   [2 Legacy method: ALSA-BTSCO](#Legacy_method:_ALSA-BTSCO)
*   [3 Legacy method: PulseAudio](#Legacy_method:_PulseAudio)
*   [4 Legacy documentation: ALSA, bluez5 and PulseAudio method](#Legacy_documentation:_ALSA,_bluez5_and_PulseAudio_method)
*   [5 在 HSV 和 A2DP 配置间切换](#在_HSV_和_A2DP_配置间切换)
    *   [5.1 PulseAudio下A2DP不能工作](#PulseAudio下A2DP不能工作)
        *   [5.1.1 Socket Interface problem](#Socket_Interface_problem)
        *   [5.1.2 Gnome with GDM](#Gnome_with_GDM)
*   [6 Tested headsets](#Tested_headsets)
*   [7 See also](#See_also)

## 通过 Bluez5/PulseAudio 支持耳机

PulseAudio 5.x 开始默认支持 A2DP。 确保这些包已经安装[Install](/index.php/Install "Install"): [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa), [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth), [bluez](https://www.archlinux.org/packages/?name=bluez), [bluez-libs](https://www.archlinux.org/packages/?name=bluez-libs), [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils), [bluez-firmware](https://aur.archlinux.org/packages/bluez-firmware/). 如果没有安装 [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth)，蓝牙设备在配对完成后，连接会失败，而且你不会得到任何有用的提示。

启动bluetooth服务:

```
# systemctl start bluetooth

```

现在我们可以使用 *bluetoothctl* 命令来实现配对和连接。 如果在使用这个命令过程中出现问题或想了解*bluetoothctl*的更多帮助，参见 [Bluetooth](/index.php/Bluetooth "Bluetooth")。运行：

```
# bluetoothctl

```

进入内部命令行提示，然后输入：

```
# power on
# agent on
# default-agent
# scan on

```

现在让你的蓝牙耳机进入配对模式，它很快就能发现新的设备。如：

```
[NEW] Device 00:1D:43:6D:03:26 Lasmex LBT10

```

这里发现了一个名字是"Lasmex LBT10"，对应MAC地址是*00:1D:43:6D:03:26*的设备。接下来我们使用这个MAC地址来配对：

```
# pair 00:1D:43:6D:03:26

```

配对成功后，你需要手动连接设备(every time?):

```
# connect 00:1D:43:6D:03:26

```

如果一切正常，你现在可以在[PulseAudio](/index.php/PulseAudio "PulseAudio")看到一个独立的输出设备。

**提示：** 设备默认情况下可能是停止的。你可以在[pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol)的"Configuration"标签页里选择配置(*OFF*, A2DP, HFP)

你现在可以通过[pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol)的"Playback"和"Pecording"标签页重定向音频的输入、输出了。

除了[pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol)，这里也可以通过*pacmd*命令来选择配置:

```
# pacmd set-card-profile bluez_card.00_1E_7C_30_86_FA a2dp_sink
a2dp_sink          -- High Fidelity Playback (A2DP Sink) (sinks: 1, sources: 0, priority: 10, available: yes)
headset_head_unit  -- Headset Head Unit (HSP/HFP) (sinks: 1, sources: 1, priority: 20, available: yes)
off                -- Off (sinks: 0, sources: 0, priority: 0, available: yes)

```

这里可选择"a2dp_sink"或"headset_head_unit"两种配置，其中"headset_head_unit"可以支持音频输入/输出，"a2dp_sink"只支持输出。

**提示：** 如果shell安装了对应的自动补全包[bash-completion](https://www.archlinux.org/packages/?name=bash-completion)或[zsh-completions](https://www.archlinux.org/packages/?name=zsh-completions)，可以通过tab键快速补全命令

你现在可以停止扫描，并退出*bluetoothctl*命令：

```
# scan off
# exit

```

### 常见问题及解决方案

有很多用户报告 A2DP/蓝牙耳机不能正常工作。

#### 已经选择音频配置，但耳机没有激活，不能重定向音频

音频配置的菜单项在设备还没有成功连接的时候就已经存在了，但它并不能起作用。这个菜单项似乎是在设备被发现的时候就马上创建了。

确认一下bluetoothctl是在root用户下或在sudo环境下执行的；然后手动连接设备。有配置选项可以避免每次都需要手动连接，但是配对和信任并不会导致自动连接。

#### 授权失败导致配对失败

如果配对失败，你可以尝试[disabling SSPMode](https://stackoverflow.com/questions/12888589/linux-command-line-howto-accept-pairing-for-bluetooth-device-without-pin):

```
# hciconfig hci0 sspmode 0

```

#### 配对成功, 但连接失败

你可能在 *bluetoothctl* 里面看到下面的错误:

```
[bluetooth]# connect 00:1D:43:6D:03:26
Attempting to connect to 00:1D:43:6D:03:26
Failed to connect: org.bluez.Error.Failed

```

你可以通过以下命令查看日志以进一步定位问题：

```
# systemctl status bluetooth
# journalctl -n 20

```

你可能会在日志里看到下面类似的信息:

```
bluetoothd[5556]: a2dp-sink profile connect failed for 00:1D:43:6D:03:26: Protocol not available

```

这是因为没有安装[pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth) 包导致的。 如果确实没有安装，安装一下这个包，然后重启一下[PulseAudio](/index.php/PulseAudio "PulseAudio")。

如果不是因为缺失包导致的， 很可能是PulseAudio没收到消息，一般重启一下PulseAudio就可以解决问题。 注意*bluetoothctl*和PulseAudio不需要在相同的用户下运行，*bluetooth*在root环境下运行，而PulseAudio在用户环境下运行也可以很好的工作。 重启PulseAudio后，不需要重新配对，直接重连即可。

如果重启PulseAudio后，仍然不能正常工作，你需要重新加载 module-bluetooth-discover 模块。

```
# pactl load-module module-bluetooth-discover

```

你可以把同样的加载命令添加到 `/etc/pulse/default.pa`，让PulseAudio启动时自动加载。

如果仍然不能正常工作，或者你使用的是系统级别的PulseAudio，下面的模块也需要加载一下(同样可以把他们加到default.pa或system.pa里面):

```
module-bluetooth-policy
module-bluez5-device
module-bluez5-discover

```

你可以通过加载PulseAudio的 switch-on-connect 模块，使得蓝牙耳机连接后，自动切换到耳机上。添加如下加载语句:

 `/etc/pulse/default.pa` 
```
# automatically switch to newly-connected devices
load-module module-switch-on-connect

```

同时，你需要告诉*bluetoothctl*信任你的蓝牙耳机，否则你将会看到如下报错：

```
bluetoothd[487]: Authentication attempt without agent
bluetoothd[487]: Access denied: org.bluez.Error.Rejected

```

```
[bluetooth]# trust 00:1D:43:6D:03:26

```

重启后，你的蓝牙适配器默认是不会启用的，你需要添加udev规则来启用它：

 `/etc/udev/rules.d/10-local.rules` 
```
# Set bluetooth power up
ACTION=="add", SUBSYSTEM=="bluetooth", KERNEL=="hci[0-9]*", RUN+="/usr/bin/hciconfig %k up"
```

#### 连接成功，但不能播放声音

确定你在系统日志里面可以看到如下信息:

```
bluetoothd[5556]: Endpoint registered: sender=:1.83 path=/MediaEndpoint/A2DPSource
bluetoothd[5556]: Endpoint registered: sender=:1.83 path=/MediaEndpoint/A2DPSink

```

如果你可以看到类似的信息，说明蓝牙没有问题，你可以去检查PulseAudio的配置问题了。否则的话，退回来再次确认蓝牙是否已经连接成功。

如果使用的是[GDM](/index.php/GDM "GDM")， PulseAudio 的另外一个实例可能已经启动，并且“捕获”了你的蓝牙连接。这种情况可以通过屏蔽GDM用户的pulseaudio socket来解决：

```
# mkdir -p ~gdm/.config/systemd/user
# ln -s /dev/null ~gdm/.config/systemd/user/pulseaudio.socket

```

需要确保这个文件的用户权限是 `gdm:gdm`， 如果不是，使用 [chown](/index.php/Chown "Chown") 修改。 重启电脑后，PulseAudio的第二个实例将不再启动。

#### UUIDs has unsupported type

在配对的时候，你可能会在*bluetoothctl*看到如下信息:

```
[CHG] Device 00:1D:43:6D:03:26 UUIDs has unsupported type

```

这种情况很常见，没有影响，可以被忽略。

## Legacy method: ALSA-BTSCO

bluez4相关，不翻译，直接参考英文版本[Bluetooth headset#Legacy method: ALSA-BTSCO](/index.php/Bluetooth_headset#Legacy_method:_ALSA-BTSCO "Bluetooth headset")

## Legacy method: PulseAudio

bluez4相关，不翻译，直接参考英文版本[Bluetooth headset#Legacy method: PulseAudio](/index.php/Bluetooth_headset#Legacy_method:_PulseAudio "Bluetooth headset")

## Legacy documentation: ALSA, bluez5 and PulseAudio method

争议章节，不翻译，直接参考英文版本[Bluetooth headset#Legacy documentation: ALSA, bluez5 and PulseAudio method](/index.php/Bluetooth_headset#Legacy_documentation:_ALSA,_bluez5_and_PulseAudio_method "Bluetooth headset")

## 在 HSV 和 A2DP 配置间切换

通过下面命令可以很容易的在两者间做切换：

```
# pacmd set-card-profile 2 a2dp_sink

```

这里2是配置文件的索引，根据实际情况确定。更简单的方法是使用tab键来补全。

### PulseAudio下A2DP不能工作

#### Socket Interface problem

If PulseAudio fails when changing the profile to A2DP with bluez 4.1+ and PulseAudio 3.0+, you can try disabling the Socket interface from `/etc/bluetooth/audio.conf` by removing the line `Enable=Socket` and adding line `Disable=Socket`.

#### Gnome with GDM

**Note:** 下面的方法在 Gnome 3.16.2 和 PulseAudio 6.0 下已经验证过

在GNOME和GDM下，如果PulseAudio切换到A2DP配置不能正常工作，你需要阻止GDM自己启动一个PulseAudio实例。参照[#连接成功，但不能播放声音](#连接成功，但不能播放声音)操作。

**Note:** 针对这个问题的讨论可以参考 [这里](https://bbs.archlinux.org/viewtopic.php?id=194006) 和 [这里](https://bbs.archlinux.org/viewtopic.php?id=196689)

## Tested headsets

| Model | Version | Comments | Compatible |
| **Philips SHB9150** | bluez5, pulseaudio 5 | Pause and resume does not work. With at least mpv and Banshee hitting the pause button stops audio output but does not pause the player. | Limited |
| **Philips SHB9100** | Pause and resume is flaky. See [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1315428#p1315428) for the underlying issue and a temporary solution to improve audio quality. | Limited |
| **Philips SHB7000** | Pause and resume is flaky. | Limited |
| **Philips SHB7100** | bluez 5.32, pulseaudio 6.0 | Next/previous buttons work. Pause and resume is flaky (sometimes works in VLC, not at all in Audacious). Tested only A2DP and Handsfree audio out, built-in mic was broken. | Limited |
| **Philips SHB7150** | bluez 5.32, pulseaudio 6.0 | Next/previous buttons work. Pause and resume work in VLC. Tested only A2DP profile. | Yes |
| **Philips SHB5500BK/00** | bluez 5.28, PulseAudio 6.0 | Pause and resume is not working. | Limited |
| **Parrot Zik** | Firmware 1.04\. The microphone is detected, but does not work. Sometimes it lags (but does not stutter); usually this is not noticeable unless playing games, in which case you may switch to a wired connection. | Limited |
| **Sony DR-BT50** | bluez{4,5} | Works for a2dp, see [[3]](http://vlsd.blogspot.com/2013/11/bluetooth-headphones-and-arch-linux.html)). Adapter: D-Link DBT-120 USB dongle. | Yes |
| **Sony SBH50** | bluez5 | Works for a2dp, Adapter: Broadcom Bluetooth 2.1 Device (Vendor=0a5c ProdID=219b Rev=03.43). Requires the `btusb` [module](/index.php/Modprobe "Modprobe"). | Yes |
| **Sony MDR-XB950BT** | pulseaudio | Tested a2dp. Adapter: Grand-X BT40G. Doesn't auto-connect, need to connect manually. Other functionality works fine. | Limited |
| **Sony MUC-M1BT1** | bluez5, [pulseaudio-git](https://aur.archlinux.org/packages/pulseaudio-git/) | Both A2DP & HSP/HFP work fine. | Yes |
| **SoundBot SB220** | bluez5, [pulseaudio-git](https://aur.archlinux.org/packages/pulseaudio-git/) | Yes |
| **Auna Air 300** | bluez5, pulseaudio-git | For some reason, a few restarts were required, and eventually it just started working. | Limited |
| **Sennheiser MM 400-X** | bluez5, pulseaudio 4.0-6 | Yes |
| **Sennheiser MM 550-X Travel** | bluez 5.27-1, pulseaudio 5.0-1 | Next/Previous buttons work out-of-the-box, Play/Pause does not | Yes |
| **Audionic BlueBeats (B-777)** | bluez5, pulseaudio 4.0-6 | Yes |
| **Logitech Wireless Headset** | bluez 5.14, pulseaudio-git | part number PN 981-000381, advertised for use with iPad | Yes |
| **HMDX Jam Classic Bluetooth** | bluez, pulseaudio-git | Yes |
| **PT-810** | bluez 5.14, pulseaudio-git | Generic USB-Powered Bluetooth Audio Receiver with 3.5mm headset jack and a2dp profile. Widely available as "USB Bluetooth Receiver." IDs as PT-810. | Yes |
| **Philips SHB4000WT** | bluez5 | A2DP works, HDP distorted. | Yes |
| **Philips AEA2000/12** | bluez5 | Yes |
| **Nokia BH-104** | bluez4 | Yes |
| **Creative AirwaveHD** | bluez 5.23 | Bluetooth adapter Atheros Communications usb: 0cf3:0036 | Yes |
| **Creative HITZ WP380** | bluez 5.27, pulseaudio 5.0-1 | A2DP Profile only. Buttons work (Play, Pause, Prev, Next). Volume buttons are hardware-only. Auto-connect works but you should include the bluetooth module in "pulseaudio" to switch to it automatically. Clear HD Music Audio (This device support APTx codec but it isn't supported in linux yet). You may have some latency problems which needs pulseaudio restart. | Yes |
| **deleyCON Bluetooth Headset** | bluez 5.23 | Adapter: CSL - USB nano Bluetooth-Adapter V4.0\. Tested a2dp profile. Untested microphone. Does not auto-connect (even when paired and trusted), must connect manually. Play/pause button mutes/unmutes the headphones, not the playback. Playback fwd/bwd buttons do not work (nothing visible with *xev*). | Limited |
| **UE BOOM** | bluez 5.27, pulseaudio-git 5.99 | Update to latest UE BOOM fw 1.3.58\. Sound latency in video solved by configuring pavucontrol. Works with UE BOOM x2. | Yes |
| **LG HBS-730** | bluez 5.30, pulseaudio 6.0 | Works out of box with A2DP profile. | Yes |
| **LG HBS-750** | bluez 5.30, pulseaudio-git 6.0 | Works out of box with A2DP profile. | Yes |
| **Beats Studio Wireless** | bluez 5.28, pulseaudio 6.0 | Works out of box. Not tested multimedia buttons. | Yes |
| **AKG Y45BT** | bluez 5.30, pulseaudio 6.0 | Pause and resume does not work. Needs `Enable=Socket` in `/etc/bluetooth/audio.conf` and `load-module module-bluetooth-discover` in `/etc/pulse/default.pa`. | Yes |
| **Bluedio Turbine/Turbine 2+** | bluez5.3, pulseaudio 6.0 | HSP/HFP work fine, A2DP work fine. | Yes |
| **Sony SBH20** | bluez 5.30, pulseaudio 6.0 | Works out of box with A2DP profile. | Yes |
| **Nokia BH-111** | bluez 5.30, pulseaudio 6.0 | Works with both HSP/HFP and A2DP. Buttons work in certain apps. | Yes |
| **Sony MDR-ZX330BT** | bluez 5.31, pulseaudio 6.0 | Works out of box (HSP/HFP and A2DP). Buttons work in certain apps. | Yes |
| **Samsung Level Link** | bluez 5.33, pulseaudio 6.0 | Works out of box (HSP/HFP and A2DP). Buttons work in certain apps. | Yes |

## See also

Using the same device on Windows and Linux without pairing the device over and over again

*   [Dual booting with a Bluetooth keyboard](http://ubuntuforums.org/showthread.php?p=9363229#post9363229)