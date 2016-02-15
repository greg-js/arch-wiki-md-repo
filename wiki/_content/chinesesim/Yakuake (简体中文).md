**翻译状态：** 本文是英文页面 [Yakuake](/index.php/Yakuake "Yakuake") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-8-6，点击[这里](https://wiki.archlinux.org/index.php?title=Yakuake&diff=0&oldid=328823)可以查看翻译后英文页面的改动。

[Yakuake](http://yakuake.kde.org/) 是 [KDE](/index.php/KDE "KDE"),里的下拉式终端,与 [Guake](/index.php/Guake "Guake") 或者 [Tilda](/index.php/Tilda "Tilda") 类似.

## 安装

在[官方仓库](/index.php/Official_repositories "Official repositories")[安装](/index.php/Pacman "Pacman") [yakuake](https://www.archlinux.org/packages/?name=yakuake)。

## 使用

在终端用以下命令打开Yakuake

```
$ yakuake

```

你可以点击右下角的扳手按钮，选择管理配置文件来配置你的Yukuake，点击Configure Shortcuts来配置快捷键。同样的，如果你要将Yukuake锁定在屏幕上，你可以点击扳手右边的锁按钮。

## 打开Yakuake并自定义终端

像 [Guake](/index.php/Guake "Guake") 一样，Yakuake 允许用户用自定义脚本配置终端。 简单的说，当 Yakuake 启动的时候，在每个终端里的程序会根据用户所定义的自动运行。 另外，Yakuake 也允许用户配置每个会话的名字。

然而与[Guake](/index.php/Guake "Guake")不相同的是， Yakuake 依赖于Qt框架，所以打开新的会话的语法与[Guake](/index.php/Guake "Guake")不同。以下是一个简单的用来打开用户自定义终端的脚本（已在 2.9.9-1 版本中测试过）。

```
~/editme.sh

```

```
# 自定义打开Yakuake。 基于 http://forums.gentoo.org/viewtopic-t-873915-start-0.html
# 还有 http://pawelkoston.pl/blog/sublime-text-3-cheatsheet-modules-web-develpment/
# 如果你的fcitx在Yakuake上打不出字，你就需要这一行
/usr/bin/yakuake --im /usr/bin/fcitx --inputstyle onthespot

# 在当前会话打开iotop程序并命名当前会话为iotop
qdbus-qt4 org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus-qt4 org.kde.yakuake /yakuake/tabs setTabTitle 0 "iotop" 
qdbus-qt4 org.kde.yakuake /yakuake/sessions runCommandInTerminal 0 "iotop"

# 在当前会话打开htop程序并命名当前会话为htop.
qdbus-qt4 org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus-qt4 org.kde.yakuake /yakuake/tabs setTabTitle 1 "htop"
qdbus-qt4 org.kde.yakuake /yakuake/sessions runCommandInTerminal 1 "htop"

# 在当前会话打开atop程序并命名当前会话为atop.
qdbus-qt4 org.kde.yakuake /yakuake/sessions org.kde.yakuake.addSession
qdbus-qt4 org.kde.yakuake /yakuake/tabs setTabTitle 2 "atop"
qdbus-qt4 org.kde.yakuake /yakuake/sessions runCommandInTerminal 2 "atop"

# 关闭2号会话
qdbus-qt4 org.kde.yakuake /yakuake/sessions org.kde.yakuake.removeSession 10
```