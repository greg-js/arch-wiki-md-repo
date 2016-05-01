部分内容来自[维基百科](https://zh.wikipedia.org/wiki/Telegram): Telegram Messenger是一个跨平台的实时通信软件，它的客户端是自由及开放源代码软件，但是它的服务器是专有软件。用户可以相互交换加密与自析构的消息，以及照片、视频、文件，支持所有的文件类型。官方网站有正式发布Android、iOS、Mac OS X与正在Beta的Windows Phone的版本；其他版本皆为非正式的版本，而且是由独立研发人员利用官方的应用程序接口来开发的。

## 安装

目前在官方库中还没有有关的软件包，但是在AUR中有[telegram-desktop](https://aur.archlinux.org/packages/telegram-desktop/)、[telegram-dev](https://aur.archlinux.org/packages/telegram-dev/)、[telegram-desktop-cn](https://aur.archlinux.org/packages/telegram-desktop-cn/)等包，对于中日韩等需要使用输入法的，请安装[telegram-desktop-cn](https://aur.archlinux.org/packages/telegram-desktop-cn/)。

官方的 telegram 从 0.8.50 版本开始已经修复了中文输入法问题，推荐使用。您有可能需要设置 QT_IM_MODULE 环境变量，详情参考 [Fcitx (简体中文)#非桌面环境](/index.php/Fcitx_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E9.9D.9E.E6.A1.8C.E9.9D.A2.E7.8E.AF.E5.A2.83 "Fcitx (简体中文)")

您也可以直接添加[archlinuxcn](/index.php/Unofficial_user_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#archlinuxcn "Unofficial user repositories (简体中文)")源：

 `# vim /etc/pacman.conf ` 
```
[archlinuxcn]
SigLevel = Optional TrustedOnly
Server = http://repo.archlinuxcn.org/$arch

```

```
# pacman -S archlinuxcn-keyring
# pacman -S telegram-desktop-cn

```

在AUR中还有对于适用于包括[pidgin](/index.php/Pidgin "Pidgin")在内的软件的插件[telegram-purple](https://aur.archlinux.org/packages/telegram-purple/)、[telegram-purple-git](https://aur.archlinux.org/packages/telegram-purple-git/)，但是目前不够稳定。

## 参见

[Telegram 官方网站](https://www.telegram.org/) [Telegram 中文群组列表](https://github.com/jqs7/telegram-chinese-groups)