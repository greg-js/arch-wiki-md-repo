**Warning:** slim登录管理器已经停止开发，[slim的官网](http://slim.berlios.de/)已经关闭，此外，slim与[systemd](/index.php/Systemd "Systemd")也不是特别的兼容，请考虑换一个 [登录管理器](/index.php/Display_manager "Display manager")，或直接使用startx。

[SLiM](http://slim.berlios.de/) 是**S**imple **L**og**i**n **M**anager（简单登录管理器）的缩写。SLiM是简单、轻量级和容易配置的，相对较易在低端和高端的系统中使用。对于那些希望寻找一个不依赖于[GNOME](/index.php/GNOME "GNOME")或者[KDE](/index.php/KDE "KDE")，可以在[Xfce](/index.php/Xfce "Xfce")、[Openbox](/index.php/Openbox "Openbox")、[Fluxbox](/index.php/Fluxbox "Fluxbox")等环境下使用的登录管理器的人来说，SLiM也是非常合适的。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 启用SLiM](#.E5.90.AF.E7.94.A8SLiM)
    *   [2.2 单用户环境](#.E5.8D.95.E7.94.A8.E6.88.B7.E7.8E.AF.E5.A2.83)
    *   [2.3 自动登陆](#.E8.87.AA.E5.8A.A8.E7.99.BB.E9.99.86)
    *   [2.4 Zsh](#Zsh)
    *   [2.5 多桌面环境](#.E5.A4.9A.E6.A1.8C.E9.9D.A2.E7.8E.AF.E5.A2.83)
    *   [2.6 主题](#.E4.B8.BB.E9.A2.98)
        *   [2.6.1 多屏幕设置](#.E5.A4.9A.E5.B1.8F.E5.B9.95.E8.AE.BE.E7.BD.AE)
    *   [2.7 增强Slim功能](#.E5.A2.9E.E5.BC.BASlim.E5.8A.9F.E8.83.BD)
    *   [2.8 设置和Splashy一起工作时正常关机](#.E8.AE.BE.E7.BD.AE.E5.92.8CSplashy.E4.B8.80.E8.B5.B7.E5.B7.A5.E4.BD.9C.E6.97.B6.E6.AD.A3.E5.B8.B8.E5.85.B3.E6.9C.BA)
    *   [2.9 Slim的登录信息](#Slim.E7.9A.84.E7.99.BB.E5.BD.95.E4.BF.A1.E6.81.AF)
    *   [2.10 设置默认DPI](#.E8.AE.BE.E7.BD.AE.E9.BB.98.E8.AE.A4DPI)
    *   [2.11 使用随机主题](#.E4.BD.BF.E7.94.A8.E9.9A.8F.E6.9C.BA.E4.B8.BB.E9.A2.98)
*   [3 更多的Slim参数](#.E6.9B.B4.E5.A4.9A.E7.9A.84Slim.E5.8F.82.E6.95.B0)
*   [4 更多](#.E6.9B.B4.E5.A4.9A)

## 安装

[安装](/index.php/Pacman "Pacman")位于[官方软件仓库](/index.php/Official_repositories "Official repositories")的软件包 [slim](https://www.archlinux.org/packages/?name=slim)。

## 配置

### 启用SLiM

**注意:** [slim](https://www.archlinux.org/packages/?name=slim)已经不提供 ConsoleKit 支持，而是使用 systemd-logind，所以系统需要通过 systemd 启动。

启用**slim** [服务](/index.php/Daemons "Daemons"). 启用 systemd 之后，已经无法使用 `inittab` 启动 slim。

### 单用户环境

要将SLiM配置为加载某个特定的环境，只需编辑[~/.xinitrc](/index.php/Xinitrc "Xinitrc") 如下：

```
#!/bin/sh

#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#

exec [session-command]

```

将_**[session-command]**_替换为适当的会话命令。例如：

```
exec awesome
exec dwm
exec startfluxbox
exec fvwm2
exec gnome-session
exec openbox-session
exec startkde
exec startlxde
exec startxfce4
exec enlightenment_start

```

如果你的桌面环境不在上述列表中，请参考你的软件文档。

Remember to make `~/.xinitrc` executable:

```
chmod +x ~/.xinitrc

```

**Note:** [slim](https://www.archlinux.org/packages/?name=slim) no longer has ConsoleKit support, but relies on systemd-logind, and the system being booted with systemd.

### 自动登陆

想要使SLiM自动以特定用户身份登录（无须输入密码），需要修改 `/etc/slim.conf` 中的以下几行。

```
# default_user        simone

```

取消该行的注释，然后将“simone”改为需要自动登录的用户名。

```
# auto_login          no

```

取消该行的注释，然后将‘no’改为‘yes’。自动登录功能就被启用了。

### Zsh

默认的登录命令不能正确初始化你的环境 [[source](http://www.edsel.nu/2010/06/04/slim-simple-login-manager-on-freebsd/)]。 将 login_cmd 一行改为：

```
#login_cmd           exec /bin/sh - ~/.xinitrc %session
login_cmd           exec /bin/zsh -l ~/.xinitrc %session

```

### 多桌面环境

如果你希望可以加载多个不同的桌面环境，SLiM可以设置为登录到你指定的任何一个桌面环境。

在你的/etc/X11/xinit/xinitrc文件中加入一段类似下面内容的case语句，并且编辑/etc/slim.conf中的sessions变量。 你可以在登录界面上按F1选择会话。请注意这个特性仍处于实验阶段。

```
# The following variable defines the session which is started if the user doesn't explicitly select a session

DEFAULT_SESSION=twm

case $1 in
kde)
	exec startkde
	;;
xfce4)
	exec startxfce4
	;;
icewm)
	icewmbg &
	icewmtray &
	exec icewm
	;;
wmaker)
	exec wmaker
	;;
blackbox)
	exec blackbox
	;;
*)
	exec $DEFAULT_SESSION
	;;
esac

```

范例源码： [http://svn.berlios.de/svnroot/repos/slim/trunk/xinitrc.sample](http://svn.berlios.de/svnroot/repos/slim/trunk/xinitrc.sample)

SLiM的文档： [http://slim.berlios.de/manual.php](http://slim.berlios.de/manual.php)

### 主题

安装[slim-themes](https://www.archlinux.org/packages/?name=slim-themes)软件包：

```
# pacman -S slim-themes archlinux-themes-slim

```

软件包 [archlinux-themes-slim](https://www.archlinux.org/packages/?name=archlinux-themes-slim) 包含了多个不同主题。可以在 `/usr/share/slim/themes` 中查看。在to see the themes available. Enter the theme name on the `current_theme` line in `/etc/slim.conf`:

编辑`/etc/slim.conf`中的`current_theme`那行，将"default"改为你想要的主题名：

```
#current_theme       default
current_theme       archlinux-simplyblack

```

要预览一个主题，可以运行

```
$ slim -p /usr/share/slim/themes/<theme name>

```

要退出，只需在登录行输入 "exit" 并回车。

#### 多屏幕设置

定制 `/usr/share/slim/themes/<your-theme>/slim.theme` 中的主题，修改百分比，就可以在多屏幕环境使用。假设宽为 450 高为 250 :

```
input_panel_x           50%
input_panel_y           50%

```

修改为:

```
# 将 "archlinux-simplyblack" 面板放在 1440x900 屏幕的中间
input_panel_x           495
input_panel_y           325

```

```
# 将 "archlinux-retro" 面板放在 1680x1050 屏幕的中间
input_panel_x           615
input_panel_y           400

```

如果主题有背景图片，可以设置背景样式('stretch', 'tile', 'center' 或 'color')。更多信息请访问 [slim 主题的标准文档](http://slim.berlios.de/themes_howto.php)。

### 增强Slim功能

slim登录脚本主要靠你自己写，这对很多人来说比较困难，比如自动加载一些配置文件如~/.xprofile, ~/.xmodmap等。而且slim还无法记住上次登录使用的桌面环境。

AUR里面有个包[slim-plus](https://aur.archlinux.org/packages.php?ID=31601)可以解决这些问题。提供了一个Xsession脚本增强slim功能，加载配置文件，记住上次会话等。非常适合xfce等小型桌面环境。而且包含很多实用补丁。如果你想自己编写启动脚本，那里带的Xsession脚本可以做参考。

安装完成后，如果以前使用的就是slim，那么需要编辑slim来使用/etc/X11/Xsession来加载会话，找到如下行：

```
 login_cmd           exec /bin/bash -login ~/.xinitrc %session

```

替换为

```
 login_cmd           exec /bin/bash -login /etc/X11/Xsession %session

```

只需要修改/etc/slim.conf的Sessions行，添加你需要的会话，slim启动后按F1选择就可以了。会话的名称可以在/usr/share/xsessions/下的*.desktop处得到。

如果你安装的桌面环境没有提供.desktop文件，就需要自行编辑/etc/X11/Xsession文件尾部，不过脚本本身带有提供很多窗口管理器的启动脚本。

Xsession脚本会自动加载常见配置文件。使用ck-launch-session加载桌面，解决一些挂载，无法关机等问题。并且使用~/.dmrc记录上次会话。由于slim功能有限，暂时无法选择语言。你自己可以编辑~/.dmrc来设置语言为中文。

```
 Language=zh_CN.UTF-8

```

### 设置和Splashy一起工作时正常关机

如果你同时使用splashy和slim，有时你无法在gnome，xfce，lxde，等桌面环境中正常关机或者重启。 那么请检查你的/etc/slim.conf 和 /etc/splash.conf, 设置需要为 DEFAULT_TTY=7 或者 xserver_arguments vt07.

### Slim的登录信息

By default, Slim fails to log logins to utmp and wtmp which causes who, last, etc.. to misreport login information. 修正这些你需要编辑你的slim.conf:

```
 sessionstart_cmd    /usr/bin/sessreg -a -l $DISPLAY %user
 sessionstop_cmd     /usr/bin/sessreg -d -l $DISPLAY %user

```

### 设置默认DPI

如果你设置DPI是通过在/etc/X11/Xinit/Xserverrc中添加参数-dpi 96，那么设置在slim中是不起作用的。你需要在slim.conf中这样设置：

```
 xserver_arguments   -nolisten tcp vt07 

```

更改为：

```
 xserver_arguments   -nolisten tcp vt07 -dpi 96

```

### 使用随机主题

在slim.conf中的current_theme行，添加多个主题，使用`,`分隔就可以使用随机主题了。

## 更多的Slim参数

这个列表显示了所有的参数变量以及其默认值。

**Note:** welcome_msg 允许2个变量**%host** 与 **%domain**
sessionstart_cmd 读取 **%user** _(execd right before login_cmd)_ 并且它也会读取 sessionstop_cmd
login_cmd allows **%session** and **%theme**

| Option Name | Default Value |
| default_path | <tt>/bin:/usr/bin:/usr/local/bin</tt> |
| default_xserver | <tt>/usr/bin/X</tt> |
| xserver_arguments | <tt>vt07 -auth /var/run/slim.auth</tt> |
| numlock |
| daemon | <tt>yes</tt> |
| xauth_path | <tt>/usr/bin/xauth</tt> |
| login_cmd | <tt>exec /bin/bash -login ~/.xinitrc %session</tt> |
| halt_cmd | <tt>/sbin/shutdown -h now</tt> |
| reboot_cmd | <tt>/sbin/shutdown -r now</tt> |
| suspend_cmd |
| sessionstart_cmd |
| sessionstop_cmd |
| console_cmd | <tt>/usr/bin/xterm -C -fg white -bg black +sb -g %dx%d+%d+%d -fn %dx%d -T</tt> |
| screenshot_cmd | <tt>import -window root /slim.png</tt> |
| welcome_msg | <tt>Welcome to %host</tt> |
| session_msg | <tt>Session:</tt> |
| default_user |
| focus_password | <tt>no</tt> |
| auto_login | <tt>no</tt> |
| current_theme | <tt>default</tt> |
| lockfile | <tt>/var/run/slim.lock</tt> |
| logfile | <tt>/var/log/slim.log</tt> |
| authfile | <tt>/var/run/slim.auth</tt> |
| shutdown_msg | <tt>The system is halting...</tt> |
| reboot_msg | <tt>The system is rebooting...</tt> |
| sessions | <tt>wmaker,blackbox,icewm</tt> |
| sessiondir |
| hidecursor | <tt>false</tt> |
| input_panel_x | <tt>50%</tt> |
| input_panel_y | <tt>40%</tt> |
| input_name_x | <tt>200</tt> |
| input_name_y | <tt>154</tt> |
| input_pass_x | <tt>-1</tt> |
| input_pass_y | <tt>-1</tt> |
| input_font | <tt>Verdana:size=11</tt> |
| input_color | <tt>#000000</tt> |
| input_cursor_height | <tt>20</tt> |
| input_maxlength_name | <tt>20</tt> |
| input_maxlength_passwd | <tt>20</tt> |
| input_shadow_xoffset | <tt>0</tt> |
| input_shadow_yoffset | <tt>0</tt> |
| input_shadow_color | <tt>#FFFFFF</tt> |
| welcome_font | <tt>Verdana:size=14</tt> |
| welcome_color | <tt>#FFFFFF</tt> |
| welcome_x | <tt>-1</tt> |
| welcome_y | <tt>-1</tt> |
| welcome_shadow_xoffset | <tt>0</tt> |
| welcome_shadow_yoffset | <tt>0</tt> |
| welcome_shadow_color | <tt>#FFFFFF</tt> |
| intro_msg |
| intro_font | <tt>Verdana:size=14</tt> |
| intro_color | <tt>#FFFFFF</tt> |
| intro_x | <tt>-1</tt> |
| intro_y | <tt>-1</tt> |
| background_style | <tt>stretch</tt> |
| background_color | <tt>#CCCCCC</tt> |
| username_font | <tt>Verdana:size=12</tt> |
| username_color | <tt>#FFFFFF</tt> |
| username_x | <tt>-1</tt> |
| username_y | <tt>-1</tt> |
| username_msg | <tt>Please enter your username</tt> |
| username_shadow_xoffset | <tt>0</tt> |
| username_shadow_yoffset | <tt>0</tt> |
| username_shadow_color | <tt>#FFFFFF</tt> |
| password_x | <tt>-1</tt> |
| password_y | <tt>-1</tt> |
| password_msg | <tt>Please enter your password</tt> |
| msg_color | <tt>#FFFFFF</tt> |
| msg_font | <tt>Verdana:size=16:bold</tt> |
| msg_x | <tt>40</tt> |
| msg_y | <tt>40</tt> |
| msg_shadow_xoffset | <tt>0</tt> |
| msg_shadow_yoffset | <tt>0</tt> |
| msg_shadow_color | <tt>#FFFFFF</tt> |
| session_color | <tt>#FFFFFF</tt> |
| session_font | <tt>Verdana:size=16:bold</tt> |
| session_x | <tt>50%</tt> |
| session_y | <tt>90%</tt> |
| session_shadow_xoffset | <tt>0</tt> |
| session_shadow_yoffset | <tt>0</tt> |
| session_shadow_color | <tt>#FFFFFF</tt> |

## 更多

*   [Display manager](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")
*   [SLiM 官方网站](http://slim.berlios.de/)