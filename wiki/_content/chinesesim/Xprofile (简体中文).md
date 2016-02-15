**翻译状态：** 本文是英文页面 [Xprofile](/index.php/Xprofile "Xprofile") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-03-10，点击[这里](https://wiki.archlinux.org/index.php?title=Xprofile&diff=0&oldid=364903)可以查看翻译后英文页面的改动。

xprofile 文件，`~/.xprofile` 以及 `/etc/xprofile`, 允许您在刚打开 X 会话时运行命令 - 在[窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")运行之前。Xprofile 用于随会话自动运行程序，或从[显示管理器](/index.php/%E6%98%BE%E7%A4%BA%E7%AE%A1%E7%90%86%E5%99%A8 "显示管理器")启动,尤其是那个会话没有自带自动启动程序功能时 - 比如一个独立的[窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")。

xprofile 文件在语法和概念上类似 [xinitrc (简体中文)](/index.php/Xinitrc_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xinitrc (简体中文)"), `~/.xinitrc` 和 `/etc/X11/xinit/xinitrc.d/`.

## 兼容性

xprofile 和 [xinitrc](/index.php/Xinitrc "Xinitrc") 文件在原生情况下会被以下显示管理器引用:

*   [GDM](/index.php/GDM "GDM") - `/etc/gdm/Xsession`
*   [KDM](/index.php/KDM "KDM") - `/usr/share/config/kdm/Xsession`
*   [LightDM](/index.php/LightDM "LightDM") - `/etc/lightdm/Xsession`
*   [LXDM](/index.php/LXDM "LXDM") - `/etc/lxdm/Xsession`

### 在用 init 开启会话之时引用 xprofile

使用以下程序启动会话时能够引用 xprofile 文件:

*   `startx`
*   `xinit`
*   [XDM](/index.php/XDM "XDM")
*   [SLiM](/index.php/SLiM "SLiM")
*   任何其他 `~/.xsession` 使用 `~/.xinitrc` 的[显示管理器](/index.php/%E6%98%BE%E7%A4%BA%E7%AE%A1%E7%90%86%E5%99%A8 "显示管理器")

执行以上程序，不管是直接还是间接，`~/.xinitrc` (如果不存在的话，通常是复制自 `/etc/skel/.xinitrc`) 或 `/etc/X11/xinit/xinitrc`. 这就是为什么我们要从以下文件引用 xprofile.

 `~/.xinitrc 和 /etc/X11/xinit/xinitrc 和 /etc/skel/.xinitrc` 

```
#!/bin/sh

# Make sure this is before the 'exec' command or it won't be sourced.
[ -f /etc/xprofile ] && source /etc/xprofile
[ -f ~/.xprofile ] && source ~/.xprofile

...

```

`xinitrc.d/*` 文件已经引用自默认 xinitrc 文件。

## 配置

首先，如果文件不存在的话创建 `~/.xprofile`. 然后只需加入你想要随会话一同启动的程序的命令。见以下:

 `~/.xprofile` 

```
tint2 &
nm-applet &

```