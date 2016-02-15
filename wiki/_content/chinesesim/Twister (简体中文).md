**翻译状态：** 本文是英文页面 [Twister](/index.php/Twister "Twister") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-02-12，点击[这里](https://wiki.archlinux.org/index.php?title=Twister&diff=0&oldid=360447)可以查看翻译后英文页面的改动。

[Twister](http://twister.net.co/) twister是一个还在测试阶段的P2P微博软件。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 准备](#.E5.87.86.E5.A4.87)
*   [3 Gui](#Gui)
*   [4 JSON/CLI](#JSON.2FCLI)
    *   [4.1 创建用户](#.E5.88.9B.E5.BB.BA.E7.94.A8.E6.88.B7)
    *   [4.2 发推和看推](#.E5.8F.91.E6.8E.A8.E5.92.8C.E7.9C.8B.E6.8E.A8)
    *   [4.3 私信](#.E7.A7.81.E4.BF.A1)
    *   [4.4 设置管理](#.E8.AE.BE.E7.BD.AE.E7.AE.A1.E7.90.86)
    *   [4.5 帮助](#.E5.B8.AE.E5.8A.A9)

## 安装

AUR中有 [twister-core-git](https://aur.archlinux.org/packages/twister-core-git/) 和 [twister-html-git](https://aur.archlinux.org/packages/twister-html-git/)这两个包。

## 准备

启动伺服机：

```
# systemctl start twister

```

让twister随系统启动：

```
# systemctl enable twister

```

这会同时加载twister-core daemon和twister-html gui.

然后尝试进入: [http://127.0.0.1:28332/home.html](http://127.0.0.1:28332/home.html).

进入“网络”（network）选项卡，然后等待块链（blockchain）下载完成。 进入“注册”（setup account）选项卡，注册。等待你的注册完毕，然后进行你的个人设置，你的设置需要被另一个块接收，所以，请耐心等待“保存”（save）按钮的出现。

## Gui

Twister-html包含一个在web上的GUI交互界面，你可以访问[[1]](http://127.0.0.1:28332/home.html)从而完全操纵你计算机上的twister；你也可以发推（post）和收推。

## JSON/CLI

twister有基于JSON-RPC的CLI界面，但是这基本上使用来debug或者develop的，详细介绍请看[[2]](http://twister.net.co/?page_id=58)，以下给出此页面的一些摘要

### 创建用户

此命令创建用户：

```
# twisterd createwalletuser myname

```

此命令将用户传播到Twister网络上：

```
# twisterd sendnewusertransaction myname

```

### 发推和看推

```
# twisterd newpostmsg myname 1 "hello world"

```

```
# twisterd getposts 5 '[{"username":"myname"},{"username":"myfriend"}]'

```

### 私信

```
# twisterd newdirectmsg myname 2 myfriend "secret message"

```

```
# twisterd getdirectmsgs myname 10 '[{"username":"myfriend"}]'

```

### 设置管理

```
# twisterd dhtput myname profile s '{"fullname":"My Name","bio":"just another user","location":"nowhere","url":"twister.net.co"}' myname 1

```

```
# twisterd dhtget myfriend profile s

```

### 帮助

```
# twisterd help

```