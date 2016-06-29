**翻译状态：** 本文是英文页面 [Audacious](/index.php/Audacious "Audacious") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-06-28，点击[这里](https://wiki.archlinux.org/index.php?title=Audacious&diff=0&oldid=437889)可以查看翻译后英文页面的改动。

[Audacious](http://audacious-media-player.org/) 是轻量级、自由软件、基于GTK+开发的GUI音乐播放器，注重音质且支持广泛的文件编码格式，并可透过第三方附加组件扩充功能。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 界面](#.E7.95.8C.E9.9D.A2)
    *   [2.2 加入 Winamp 皮肤](#.E5.8A.A0.E5.85.A5_Winamp_.E7.9A.AE.E8.82.A4)
*   [3 技巧和问题](#.E6.8A.80.E5.B7.A7.E5.92.8C.E9.97.AE.E9.A2.98)
    *   [3.1 Audtool](#Audtool)
    *   [3.2 MP3 问题](#MP3_.E9.97.AE.E9.A2.98)
    *   [3.3 Audacious 将自己设置为默认文件管理器](#Audacious_.E5.B0.86.E8.87.AA.E5.B7.B1.E8.AE.BE.E7.BD.AE.E4.B8.BA.E9.BB.98.E8.AE.A4.E6.96.87.E4.BB.B6.E7.AE.A1.E7.90.86.E5.99.A8)

## 安装

[安装](/index.php/Pacman "Pacman") 软件包 [audacious](https://www.archlinux.org/packages/?name=audacious)。如果要音频 CD 支持，请安装[libcdio](https://www.archlinux.org/packages/?name=libcdio).

## 配置

### 界面

Audacious有两种不同的界面，可以通过配置进行设置：

*   Winamp 经典界面
*   GTK+ 界面（默认）

### 加入 Winamp 皮肤

加入 Winamp 面板到 Audacious 很简单，只要复制你的面板(.zip, .wsz, .tgz, .tar.gz, 和 .tar.bz2 档)到 **`/usr/share/audacious/Skins`**或全局的`/usr/share/audacious/Skins`。然后就能在 主选单 > *Preferences* > *Skinned Interface* 选择使用的皮肤。

## 技巧和问题

### Audtool

Audacious附带有威力强大的管理工具Audtool，可以从播放器取得信息或控制播放器。

例如，取得目前播放的歌名或歌手：

```
audtool current-song

```

```
audtool current-song-tuple-data artist

```

其它还有播放控制、编辑播放列表、调整平衡器和主界面等功能。完整的选项列表:

```
audtool --help

```

### MP3 问题

安装 [mpg123](https://www.archlinux.org/packages/?name=mpg123).

### Audacious 将自己设置为默认文件管理器

请阅读 [File manager functionality#Directories are not opened in the file manager](/index.php/File_manager_functionality#Directories_are_not_opened_in_the_file_manager "File manager functionality").