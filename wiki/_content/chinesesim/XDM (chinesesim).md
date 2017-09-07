相关文章

*   [Display Manager](/index.php/Display_Manager "Display Manager")

来自 [XDM 手册页](http://www.xfree86.org/current/xdm.1.html):

	*Xdm 能为本地和远程服务器提供一系列图形显示功能。xdm的设计满足图形显示的基本要求并遵循开放组织标准(XDMCPX Display Manager Control Protocol)，即X显示管理协议。Xdm提供的功能与init, getty等以文本登录为主的程序相似:提供登录会话，获取用户名和密码，并将授权给予登录用户并提供工作会话。*

XDM 提供了一个简单而又直观的图形登录界面。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 设置墙纸](#.E8.AE.BE.E7.BD.AE.E5.A2.99.E7.BA.B8)
*   [3 Multiple X sessions & Login in the window](#Multiple_X_sessions_.26_Login_in_the_window)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 XDM loops back to itself after login](#XDM_loops_back_to_itself_after_login)
    *   [4.2 XDM does not update login records](#XDM_does_not_update_login_records)

## 安装

安装 XDM:

 `# pacman -S xorg-xdm xorg-xconsole` 

更改 .xsession 为可执行文件:

 `$ chmod 744 .xsession` 

除此之外, 你可以为XDM安装Arch Linux 主题(可选):

 `# pacman -S xdm-archlinux` 

参看 [Display manager](/index.php/Display_manager "Display manager") 以获取详细信息。

## 设置墙纸

这里有些小贴士能让 [XDM](/index.php/XDM "XDM") 变得美观些:

*   安装 Quick Image Viewer:

 `# pacman -S qiv` 

*   创建一个文件夹用于存放图片。 (例如 `/root/backgrounds` 或者 `/usr/local/share/backgrounds`)

*   把图片放进文件夹。如果你没有适合的墙纸可以看看[www.digitablasphemy.com](http://www.digitalblasphemy.com/)。

*   编辑 `/etc/X11/xdm/Xsetup_0`. 改变 `xconsole` 命令为:

```
 /usr/bin/qiv -zr /root/backgrounds/*

```

*   编辑 `/etc/X11/xdm/Xresources`. 添加/替换 下面字段:

```
 xlogin**greetFont:  -adobe-helvetica-bold-o-normal--20-**-**-**-**-**-iso8859-1
 xlogin**font:       -adobe-helvetica-medium-r-normal--14-**-**-**-**-**-iso8859-1
 xlogin**promptFont: -adobe-helvetica-bold-r-normal--14-**-**-**-**-**-iso8859-1
 xlogin**failFont:   -adobe-helvetica-bold-r-normal--14-**-**-**-**-**-iso8859-1
 xlogin*frameWidth: 1
 xlogin*innerFramesWidth: 1
 xlogin*logoPadding: 0
 xlogin*geometry:    300x175-0-0

```

注释掉以下字段:

```
 #xlogin*logoFileName: /usr/X11R6/lib/X11/xdm/pixmaps/xorg.xpm
 #xlogin*logoFileName: /usr/X11R6/lib/X11/xdm/pixmaps/xorg-bw.xpm

```

如想了解各字段的确切意义,可查阅xdm的手册页。

*   更新 `/etc/pacman.conf` 以确保所作的更改不会丢失:

```
 ~NoUpgrade   = etc/X11/xdm/Xsetup_0 etc/X11/xdm/Xresources

```

以上的处理能让登录界面随机显示文件夹里地墙纸，并且登录会话在屏幕的右下方显示。

## Multiple X sessions & Login in the window

With the [XDMCP](/index.php/XDMCP "XDMCP") enable, you can easily run multiple X sessions simultaneously on the same machine.

 `# X -query ip_xdmcp_server :2 ` 

This will launch the second session, in window you need [xorg-server-xephyr](https://www.archlinux.org/packages/?name=xorg-server-xephyr)

 `# Xephyr -query this_machine_ip :2 ` 

## Troubleshooting

### XDM loops back to itself after login

The current version of the [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm) package, available in the [Official repositories](/index.php/Official_repositories "Official repositories") is patched to register sessions with [ConsoleKit](/index.php/ConsoleKit "ConsoleKit") by default.

When using pure systemd with logind, instead of consolekit which is now deprecated, systemd will start dbus automatically. To use xdm use `# systemctl enable xdm.service` or `# systemctl enable xdm-archlinux.service` 

Also, make sure that you are actually starting your window manager, for example with the command `xmonad` in `~/.xsession`, and that `~/.xsession` has the correct permissions of `774`.

### XDM does not update login records

The vanilla config of XDM calls `/etc/X11/xdm/GiveConsolve` for the startup of display :0, whereas otherwise it calls `/etc/X11/xdm/Xstartup`. Since only the latter contains a call to `/usr/bin/sessreg`, the login record `/var/run/utmp` is not updated for a login on display :0\. As a consequence, the output of `who` does not necessarily list the user after login through XDM. This was already discussed in the bug report [FS#26395](https://bugs.archlinux.org/task/26395).

As a simple fix, append the following line to `/etc/X11/xdm/GiveConsole`:

```
exec /usr/bin/sessreg -a -w /var/log/wtmp -u /var/run/utmp -x /etc/X11/xdm/Xservers -l $DISPLAY -h "" $USER

```

This change also enables the `getuser` function presented in [Acpid](/index.php/Acpid#Getting_user_name_of_the_current_display "Acpid") to work.