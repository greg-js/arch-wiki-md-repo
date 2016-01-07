# Deepin Desktop Environment (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**翻译状态：** 本文是英文页面 [Deepin_Desktop_Environment](/index.php/Deepin_Desktop_Environment "Deepin Desktop Environment") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-07-30，点击[这里](https://wiki.archlinux.org/index.php?title=Deepin_Desktop_Environment&diff=0&oldid=373183)可以查看翻译后英文页面的改动。

[DDE](http://www.linuxdeepin.com/feature2014.en.html) (Deepin Desktop Environment) 是deepin linux默认的桌面环境。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 启动Deepin 桌面环境](#.E5.90.AF.E5.8A.A8Deepin_.E6.A1.8C.E9.9D.A2.E7.8E.AF.E5.A2.83)
    *   [2.1 使用登录管理器](#.E4.BD.BF.E7.94.A8.E7.99.BB.E5.BD.95.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [2.2 使用xinitrc](#.E4.BD.BF.E7.94.A8xinitrc)
*   [3 热区](#.E7.83.AD.E5.8C.BA)
*   [4 反馈bugs](#.E5.8F.8D.E9.A6.88bugs)

## 安装

如果你想安装一个最小化的dde，安装deepin组即可，但我们推荐你安装完整的dde，这会给你带来更多的特性，包括:

*   **deepin-game-center**: Deepin游戏中心，可能会无法启动
*   **deepin-movie**: Deepin 视频播放器，可能会无法启动。
*   **deepin-music-player**: Deepin 音乐播放器
*   **deepin-screenshot**: Deepin截图工具
*   **deepin-terminal**: Deepin 终端

```
pacman -S deepin deepin-extra

```

## 启动Deepin 桌面环境

### 使用登录管理器

deepin默认lightdm greeter是lightdm-deepin-greeter，可通过pacman安装，安装后需编辑lightdm.conf:

 `/etc/lightdm/lightdm.conf` 

```
[SeatDefaults]
...
greeter-session=lightdm-deepin-greeter
```

### 使用xinitrc

_查看 [xinitrc](/index.php/Xinitrc "Xinitrc") 页面以获得更多详情._

 `~/.xinitrc` 

```
exec startdde

```

Execute `startx` or `xinit` to start DDE.

**Note:** 如果你想在开机时自动启动xorg，请参阅 [Start X at login](/index.php/Start_X_at_login "Start X at login") .

## 热区

默认的热区为:左上角打开启动器，右下角打开控制中心。热区设置可在控制中心更改。

## 反馈bugs

Any upstream or arch packaging related bugs should be reported [here](https://github.com/fasheng/arch-deepin/issues). FaSheng is one of the Deepin developers and also a contributor/maintainer for arch-deepin and if you file bug reports on his github page then there's much greater chance that the bug will be fixed. ;-)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Deepin_Desktop_Environment_(简体中文)&oldid=414538](https://wiki.archlinux.org/index.php?title=Deepin_Desktop_Environment_(简体中文)&oldid=414538)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments")