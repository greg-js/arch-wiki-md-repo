抓取是将音频或视频从移动媒体或媒体流复制到硬盘的过程。[wikipedia:Ripping](https://en.wikipedia.org/wiki/Ripping "wikipedia:Ripping")

通常 DVD 抓取可以分为两个部分:

1.  数据提取 -- 将声音或视频数据复制到硬盘
2.  [转码](https://en.wikipedia.org/wiki/Transcode "wikipedia:Transcode") -- 将提取的数据转换为需要的格式

一些软件可以同时完成，而另一些专注于单一功能。

## Contents

*   [1 dvdbackup](#dvdbackup)
*   [2 使用 DVD::Rip](#.E4.BD.BF.E7.94.A8_DVD::Rip)
*   [3 HandBrake](#HandBrake)
*   [4 MEncoder](#MEncoder)
    *   [4.1 Bash 脚本](#Bash_.E8.84.9A.E6.9C.AC)
    *   [4.2 Mencoder 的图形界面](#Mencoder_.E7.9A.84.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2)

## dvdbackup

[dvdbackup](/index.php/Dvdbackup "Dvdbackup") 仅用于数据获取，不提供转码功能。此工具可以和 [libdvdcss](https://www.archlinux.org/packages/?name=libdvdcss) 协同工作，创建加密 DVD 的**完全** 副本，还可以和其它不能读取加密 DVD 的工具一起解码视频。

## 使用 DVD::Rip

dvd::rip 是 [transcode](https://www.archlinux.org/packages/?name=transcode) 的前端，用来快速抓取和转码。

需要先安装以下几个软件：

*   [dvdrip](https://www.archlinux.org/packages/?name=dvdrip): [transcode](https://www.archlinux.org/packages/?name=transcode)的 GTK 前端，用于抓取和编码
*   [libdv](https://www.archlinux.org/packages/?name=libdv): DVD 视频的软件解码器
*   [xvidcore](https://www.archlinux.org/packages/?name=xvidcore): 可以转码为 XviD 的开源 MPEG-4 视频编码解码器(DivX 的自由替代)
*   [divx4linux](https://aur.archlinux.org/packages/divx4linux/): 将抓取的数据编码为 DivX (位于 [AUR](/index.php/AUR "AUR"))

```
# pacman -S dvdrip libdv xvidcore

```

dvd::rip 选项都有帮助说明/简单明了，如果需要帮助，请阅读 [http://www.exit1.org/dvdrip/doc/gui-gui_pref.cipp](http://www.exit1.org/dvdrip/doc/gui-gui_pref.cipp).

抓取 DVD 只需选择需要的编码格式，设置标题并点击 "Rip" 按钮。

## HandBrake

HandBrake 多线程转码器，同时提供了命令行和图形界面，有许多预置的选项。软件包位于[Community]: [handbrake](https://www.archlinux.org/packages/?name=handbrake)。

## MEncoder

[MEncoder](/index.php/MEncoder "MEncoder") 是自由命令行视频解码、编码和过滤工具，以 GPL 协议发布。与 MPlayer 紧密结合，可以转换所有 MPlayer 识别的格式到压缩和非压缩编码格式。[wikipedia:MEncoder](https://en.wikipedia.org/wiki/MEncoder "wikipedia:MEncoder")

MEncoder 在 [mplayer](https://www.archlinux.org/packages/?name=mplayer) 软件包中。

### Bash 脚本

这个是我用来压缩DVD的脚本，它虽不完美，但在我这它工作正常。这个脚本并不能完成象剪接这样的高级功能，但它能保持原有画面的比例。

```
#!/bin/sh

# Dvd2Avi 0.2
# Only does one title at a time, but "avimerge" from Transcode
# can sort it from there.

# by yyz

echo -n "Enter the name of output file (without extension):"
read FILE

echo -n "Enter the title you wish to rip:"
read TITLE

echo -n "Select a quality level (h/n/l)[[n]]:"
read Q

if [[ -z $Q ]];then 
    # If no quality passed, default to normal
    Q=n
fi

if [[ $Q = h ]]; then 
# If h passed, use high quality
mencoder dvd://$TITLE -alang en -oac mp3lame -lameopts br=320:cbr -ovc lavc -lavcopts vcodec=mpeg4:vhq -vop scale -zoom -xy 800 -o $FILE.avi
exit 0
fi

if [[ $Q = n ]]; then 
# If n passed, use normal quality (recommended)
mencoder dvd://$TITLE -alang en -oac mp3lame -lameopts br=160:cbr -ovc lavc -lavcopts vcodec=mpeg4:vhq -vop scale -zoom -xy 640 -o $FILE.avi
exit 0
fi

if [[ $Q = l ]]; then 
# If l passed, use low quality. not really worth it, 
# hardly any smaller but much crappier
mencoder dvd://$TITLE -alang en -oac mp3lame -lameopts br=96:vbr -ovc lavc -lavcopts vcodec=mpeg4:vhq -vop scale -zoom -xy 320 -o $FILE.avi
exit 0
fi

```

这是三个压缩质量等级的说明：

*   High: 画面宽800px，音频为320kbps的mp3
*   Normal: 画面宽640px，音频为160kbps的mp3
*   Low: 画面宽320px，音频为96kbps的mp3

要使用此脚本，把它拷贝并粘贴到一个文件中（如dvdrip.sh），赋予执行权限 `chmod +x <file>` ，然后执行它。

希望此脚本对您来说并不太难懂。您可以随意更改它，以达到您所期望效果。想了解更多信息，请参阅`man mencoder`。

### Mencoder 的图形界面

如果您不喜欢使用命令行环境，或是想使用更多mencoder的功能选项，您还可以使用它的一些图形界面。

MPlayer的 [官方网站](http://www.mplayerhq.hu/homepage/design3/projects.html#mencoder_frontends) 上有一个详尽的图形界面列表。