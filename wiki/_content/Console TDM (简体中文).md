# Console TDM (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Display manager](/index.php/Display_manager "Display manager")
*   [CDM](/index.php/CDM "CDM")

**翻译状态：** 本文是英文页面 [Console_TDM](/index.php/Console_TDM "Console TDM") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-05-22，点击[这里](https://wiki.archlinux.org/index.php?title=Console_TDM&diff=0&oldid=371133)可以查看翻译后英文页面的改动。

[Console TDM](http://code.google.com/p/t-display-manager/)是一个用纯bash脚本写出的xorg-xinit扩展组件. 它的灵感来自于CDM,这个软件可以替代诸如GDM这样的显示管理器的工作.

## 安装

[AUR](https://aur.archlinux.org/)中已经收录了[console-tdm](https://aur.archlinux.org/packages/console-tdm/)<sup><small>AUR</small></sup>.

现在，您需要通过这个命令`systemctl disable`来保证没有其他的显示管理器在开机时被运行.

比如,你正在使用GDM显示管理器,你需要使他在开机时不被运行：

```
# systemctl disable gdm.service

```

or

```
# systemctl disable graphical.target
# systemctl enable multi-user.target

```

当安装Console TDM完成后,你需要修改你的`~/.bash_profile`文件,请加入以下文字

```
source /usr/bin/tdm

```

如果你使用[zsh](/index.php/Zsh "Zsh")，将以下的字段加入你的～/.zprofile中

```
bash /usr/bin/tdm 

```

或

```
tdm

```

并编辑你的~/.xinitrc配置文件,加入以下字段并注释掉其他以`exec`开头的字段

```
exec tdm --xstart

```

## 配置

您需要将WM/DE启动器的链接复制到~/.tdm/sessions中, 然后将然后将非X程序连接到~/.tdm/extra. 为了方便,你也可以运行`tdmctl init`来达到同样效果.

`tdmctl`组件的功能非常像systemctl,并且它也是调整Console TDM设置的强有力工具.

您可以通过编辑`~/.tdm/tdminit`使Console TDM更具个性化.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Console_TDM_(简体中文)&oldid=415652](https://wiki.archlinux.org/index.php?title=Console_TDM_(简体中文)&oldid=415652)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Display managers (简体中文)](/index.php/Category:Display_managers_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Display managers (简体中文)")