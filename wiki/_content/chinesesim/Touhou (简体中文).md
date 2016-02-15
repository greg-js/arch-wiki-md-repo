**翻译状态：** 本文是英文页面 [Touhou](/index.php/Touhou "Touhou") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-03-20，点击[这里](https://wiki.archlinux.org/index.php?title=Touhou&diff=0&oldid=305737)可以查看翻译后英文页面的改动。

[东方系列](https://zh.wikipedia.org/wiki/%E6%9D%B1%E6%96%B9Project) 是一种 [弹幕游戏](http://zh.wikipedia.org/wiki/%E5%BD%88%E5%B9%95%E5%B0%84%E6%93%8A%E9%81%8A%E6%88%B2) (在西方又被叫做 "bullet-hell shooters")

东方系列(Touhou project)是一个弹幕类游戏系列的合称. 弹幕类游戏是一种2D射击类游戏, 大多由美丽的弹幕和难度大到蛋碎的弹幕组成. 东方众作为现在最大的弹幕类游戏,现在已经渗透到各个领域,比如说linux这个和一款windows游戏八杆子打不着的地方...

虽然东方的难度极大,但同时也是一个让人上瘾的游戏[抖M啊~

本wiki的目标是帮助ArchLinux用户安装东方本作及其他东方相关的包.

## Contents

*   [1 包](#.E5.8C.85)
    *   [1.1 如何打包一个游戏](#.E5.A6.82.E4.BD.95.E6.89.93.E5.8C.85.E4.B8.80.E4.B8.AA.E6.B8.B8.E6.88.8F)
    *   [1.2 Python引擎](#Python.E5.BC.95.E6.93.8E)
*   [2 其他](#.E5.85.B6.E4.BB.96)
    *   [2.1 安装完整版游戏](#.E5.AE.89.E8.A3.85.E5.AE.8C.E6.95.B4.E7.89.88.E6.B8.B8.E6.88.8F)
    *   [2.2 MIDI 音源](#MIDI_.E9.9F.B3.E6.BA.90)
*   [3 See also](#See_also)

## 包

PC-98上的游戏可以使用 Linux-native X Neko Project II emulator ([xnp2](https://aur.archlinux.org/packages/xnp2/) in [AUR](/index.php/AUR "AUR"))来运行.

以下的AUR包都需要[wine](/index.php/Wine "Wine")来运行(以及timidity++来播放MIDI音乐).有一个基于pythone的引擎正在开发中,并会用来代替wine.在AUR中的游戏都是免费试用版.你可以简单的用完整版把试用版换掉(如果你有完整版的话).

下面是已经在AUR中打包好的:

*   东方红魔乡 〜 the Embodiment of Scarlet Devil. — [th06-demo-wine](https://aur.archlinux.org/packages/th06-demo-wine/) 或 [th06-demo-pytouhou](https://aur.archlinux.org/packages/th06-demo-pytouhou/)
*   东方妖妖梦 〜 Perfect Cherry Blossom. — [th07](https://aur.archlinux.org/packages/th07/)
*   东方永夜抄 〜 Imperishable Night. — [th08](https://aur.archlinux.org/packages/th08/)

接下来一些是尚未打包到AUR中,但是有免费版放出,需要其他人对这些进行打包:

*   东方花映塚 〜 Phantasmagoria of Flower View.
*   东方风神录 〜 Mountain of Faith.
*   东方地灵殿 〜 Subterranean Animism.
*   东方星莲船 〜 Undefined Fantastic Object.
*   东方神灵庙 〜 Ten Desires.

### 如何打包一个游戏

右转[Wine PKGBUILD Guidelines](/index.php/Wine_PKGBUILD_Guidelines "Wine PKGBUILD Guidelines").

### Python引擎

[Linkmauve](http://linkmauve.fr/doc/touhou/) 制作了一个实验性质的基于python的游戏引擎.现在这个引擎还不稳定, 和正式作比起来更像是一个目标. 参考 [pytouhou-hg](https://aur.archlinux.org/packages/pytouhou-hg/) and [th06-demo-data](https://aur.archlinux.org/packages/th06-demo-data/) in AUR.

## 其他

### 安装完整版游戏

如果你有永夜抄或者妖妖梦的完整版的话,你可以放到你的主文件夹或者overlay里.这样就能在liveCD/磁盘里安装了.

注意:**.th08** 是永夜抄的 wineprefix 文件夹, and **.th07** 妖妖梦的.

1.  找到完整游戏的文件夹
2.  在主文件夹下查看隐藏文件并找到.th08/.th07
3.  把完整游戏文件复制掉到隐藏文件
4.  运行游戏

### MIDI 音源

试用版只提供MIDI文件,所以你需要安装Timidity++ ([timidity++](https://www.archlinux.org/packages/?name=timidity%2B%2B)) 和一些音源([timidity-freepats](https://www.archlinux.org/packages/?name=timidity-freepats)).

然后把一下几行加入Timidity++ 的配置文件

 `/etc/timidity++/timidity.cfg` 

```
dir /usr/share/timidity/freepats
source /etc/timidity++/freepats/freepats.cfg

```

请记住要在玩游戏之前[运行](/index.php/Daemons "Daemons") **timidity++** .

## See also

*   [维基百科上的东方系列](https://zh.wikipedia.org/wiki/%E6%9D%B1%E6%96%B9Project)
*   [于LINUX运行](http://zh.touhouwiki.net/wiki/%E4%BA%8ELinux%E8%BF%90%E8%A1%8C)