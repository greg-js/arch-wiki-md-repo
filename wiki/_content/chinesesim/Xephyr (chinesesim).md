**翻译状态：** 本文是英文页面 [Xephyr](/index.php/Xephyr "Xephyr") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-09-25，点击[这里](https://wiki.archlinux.org/index.php?title=Xephyr&diff=0&oldid=491123)可以查看翻译后英文页面的改动。

**Xephyr** 以一个 X 应用的方式运行一个嵌套的 X 服务器。

## 安装

[xorg-server-xephyr](https://www.archlinux.org/packages/?name=xorg-server-xephyr) 已收录于[官方仓库](/index.php/Official_repositories "Official repositories")中。可以用 [pacman](/index.php/Pacman "Pacman") 安装。

## 运行

如果希望运行一个嵌套的 X 窗口，你需要指定一个 **DISPLAY**。

```
$ Xephyr -br -ac -noreset -screen 800x600 :1

```

这样将会启动一个新的 Xephyr 窗口，这个窗口的 **DISPLAY** 序号是“:1”。为了在这个窗口里运行一个应用，你需要明确指定这个 **DISPLAY**：

```
$ DISPLAY=:1 xterm

```

如果想启动其他窗口管理器（例如 [spectrwm](/index.php/Spectrwm "Spectrwm") ），则输入：

```
$ DISPLAY=:1 spectrwm

```

也可以通过 startx 命令让 Xephyr 使用你的 [xinitrc](/index.php/Xinitrc "Xinitrc") ：

```
 $ startx -- /usr/bin/Xephyr :1

```