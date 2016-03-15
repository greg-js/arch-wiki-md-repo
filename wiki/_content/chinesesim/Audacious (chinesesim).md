**翻译状态：** 本文是英文页面 [Audacious](/index.php/Audacious "Audacious") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-10-06，点击[这里](https://wiki.archlinux.org/index.php?title=Audacious&diff=0&oldid=277182)可以查看翻译后英文页面的改动。

[Audacious](http://audacious-media-player.org/) 是轻量级、自由软件、基于GTK+开发的GUI音乐播放器，注重音质且支持广泛的文件编码格式，并可透过第三方附加组件扩充功能。

Audacious有着Winamp风格且支持界面更换，使用过WinAMP的人应该相当熟悉。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 Audtool](#Audtool)
*   [3 GTK UI](#GTK_UI)
*   [4 标准 UI 面板](#.E6.A0.87.E5.87.86_UI_.E9.9D.A2.E6.9D.BF)
    *   [4.1 使用 Winamp 面板](#.E4.BD.BF.E7.94.A8_Winamp_.E9.9D.A2.E6.9D.BF)
    *   [4.2 加入Winamp面板](#.E5.8A.A0.E5.85.A5Winamp.E9.9D.A2.E6.9D.BF)

## 安装

[audacious](https://www.archlinux.org/packages/?name=audacious) 位于 [官方软件仓库](/index.php/Official_repositories "Official repositories"). 可以通过 [pacman](/index.php/Pacman "Pacman") 进行安装。如果要音频 CD 支持，请安装[libcdio](https://www.archlinux.org/packages/?name=libcdio).

## Audtool

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

## GTK UI

Audacious有选项可使用不同的UI(用户介面)。 要使用新的 GTK UI，用以下方式启动 audacious2 ，或者在 外观-->界面 中调整

```
audacious -i gtkui

```

## 标准 UI 面板

### 使用 Winamp 面板

Audacious 支持 Winamp classic 界面，你可以在 Audacious 随意使用它们。 启动方式:

```
audacious -i skinned

```

### 加入Winamp面板

加入 Winamp 面板到 Audacious 很简单，只要复制你的面板(.zip, .wsz, .tgz, .tar.gz, 和 .tar.bz2 档)到 **`/usr/share/audacious/Skins`**。 之后你就能在 主选单 > *Preferences* > *Skinned Interface* 选择面板使用。

这些地方可以找到面板：

*   [http://www.customize.org/list/winamp2](http://www.customize.org/list/winamp2)
*   [http://www.deviantart.com/#catpath=customization/skins/media/winamp/classic](http://www.deviantart.com/#catpath=customization/skins/media/winamp/classic)
*   [http://www.1001skins.com](http://www.1001skins.com)