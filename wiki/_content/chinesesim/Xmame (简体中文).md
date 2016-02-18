## Contents

*   [1 用Xmame玩模拟游戏](#.E7.94.A8Xmame.E7.8E.A9.E6.A8.A1.E6.8B.9F.E6.B8.B8.E6.88.8F)
    *   [1.1 背景：](#.E8.83.8C.E6.99.AF.EF.BC.9A)
    *   [1.2 下载 与 配置](#.E4.B8.8B.E8.BD.BD_.E4.B8.8E_.E9.85.8D.E7.BD.AE)
    *   [1.3 下载ROM](#.E4.B8.8B.E8.BD.BDROM)
    *   [1.4 配置xmame](#.E9.85.8D.E7.BD.AExmame)
    *   [1.5 开始玩游戏](#.E5.BC.80.E5.A7.8B.E7.8E.A9.E6.B8.B8.E6.88.8F)

## 用Xmame玩模拟游戏

### 背景：

[Xmame](http://x.mame.net)是Linux下优秀的游戏模拟器。模拟器的作用就是在PC上模拟游戏机的硬件平台。在Archlinux下，我们能很方便得到经过优化的xmame。有了模拟器，我们还需要ROM，才能玩游戏。如果说模拟器提供硬件平台，那ROM就运行在此之上的软件，有主机ROM、游戏ROM两种。

### 下载 与 配置

用 **pacman** 把 xmame 拉下来：

```
#pacman -S xmame-sdl

```

然后 **su** 到普通用户，生成配置文件：

```
$xmame -showconfig > ~/.xmame/xmamerc

```

### 下载ROM

*   ROM是受知识产权保护的。您要自己努力，在网络上找了。

1.  对于主机ROM，放到/usr/share/xmame/roms下。
2.  对于游戏ROM，放到/usr/share/xmame/roms下，或是您自己喜欢的一个文件夹，如：~/mygames/roms里面。

### 配置xmame

其实 *~/.xmame/xmamerc* 里已经有了简单的配置信息了。如果您把游戏 ROM 放在了别处，就需要给 rompath 加一条~/mygames/roms。

```
rompath                 /usr/share/xmame/roms:~/mygames/roms

```

配置的细节，就不一一介绍了。这里只说一处：可以把effect这一条设为5。对大多数游戏。5是最好的effect。您也可以到　xmame 的主页去看看配置和快捷键。

### 开始玩游戏

**cd** 到~/mygames/roms下，用以下命令开始

```
$xmame game.zip 

```

看到画面以后，用TAB键配置游戏按键。 **Happy emulating!**