**翻译状态：** 本文是英文页面 [LXDM](/index.php/LXDM "LXDM") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-09-21，点击[这里](https://wiki.archlinux.org/index.php?title=LXDM&diff=0&oldid=391151)可以查看翻译后英文页面的改动。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 用法](#.E7.94.A8.E6.B3.95)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 登录时解锁密钥环](#.E7.99.BB.E5.BD.95.E6.97.B6.E8.A7.A3.E9.94.81.E5.AF.86.E9.92.A5.E7.8E.AF)
        *   [3.1.1 默认会话](#.E9.BB.98.E8.AE.A4.E4.BC.9A.E8.AF.9D)
        *   [3.1.2 全局](#.E5.85.A8.E5.B1.80)
        *   [3.1.3 分用户配置](#.E5.88.86.E7.94.A8.E6.88.B7.E9.85.8D.E7.BD.AE)
    *   [3.2 自动登录](#.E8.87.AA.E5.8A.A8.E7.99.BB.E5.BD.95)
    *   [3.3 注销行为](#.E6.B3.A8.E9.94.80.E8.A1.8C.E4.B8.BA)
    *   [3.4 会话列表](#.E4.BC.9A.E8.AF.9D.E5.88.97.E8.A1.A8)
*   [4 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [4.1 Adding face icons](#Adding_face_icons)
    *   [4.2 自动用户和切换用户](#.E8.87.AA.E5.8A.A8.E7.94.A8.E6.88.B7.E5.92.8C.E5.88.87.E6.8D.A2.E7.94.A8.E6.88.B7)
    *   [4.3 主题](#.E4.B8.BB.E9.A2.98)

## 安装

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的 [lxdm](https://www.archlinux.org/packages/?name=lxdm) 软件包。

或者安装[AUR](/index.php/AUR "AUR")中的[lxdm-git](https://aur.archlinux.org/packages/lxdm-git/).

## 用法

现在 [lxdm](https://www.archlinux.org/packages/?name=lxdm) 提供了 lxdm.service 文件。启用：

```
# systemctl enable lxdm.service

```

## 配置

**警告:** **lxdm.conf** 中必须包含语言选择控制，请设置 **lang=1** 否则 LXDM 会不停循环启动，无法载入会话。

LXDM 的配置文件都位于 `/etc/lxdm`。主配置文件是 `lxdm.conf`，注释非常详细。`Xsession` 是系统 X 会话配置文件，一般不需要修改。目录中的其他文件都是 bash 脚本，在 LXDM 发生相应事件时运行：

1.  `LoginReady`: 在 LXDM 准备显示登录窗口时以 root 权限运行。
2.  `PreLogin`: 用户登录前以 root 权限运行。
3.  `PostLogin`: 用户登录后以登录的用户运行。
4.  `PostLogout`: 用户注销后以用户权限运行。
5.  `PreReboot`: 通过 LXDM 重启时以 root 运行。
6.  `PreShutdown`: 通过 LXDM关机时以 root 运行。

### 登录时解锁密钥环

使用 gnome-keyring 等密钥管理器管理 ssh 密钥密码时，`/etc/pam.d/lxdm` 应该调整成允许用户在登录时解锁密钥，在文件中加入：

```
auth            optional        pam_gnome_keyring.so
session         optional        pam_gnome_keyring.so auto_start

```

#### 默认会话

#### 全局

要修改 LXDM 的默认会话或桌面环境，请编辑 `/etc/lxdm/lxdm.conf` 将下行配置：

 `session=/usr/bin/startlxde` 

例如 [Xfce](/index.php/Xfce "Xfce"):

 `session=/usr/bin/startxfce4` 

例如 [Openbox](/index.php/Openbox "Openbox"):

 `session=/usr/bin/openbox-session` 

例如 [GNOME](/index.php/GNOME "GNOME"):

 `session=/usr/bin/gnome-session` 

在使用无法选择会话的主题或者登录有问题时，这个配置很有用。

#### 分用户配置

要定义独立用户的会话，请编辑 `~/.dmrc` 并定义会话。

例如：用户1要用 xfce4，用户2要用cinnamon,用户3要用GNOME:

For user1:

```
[Desktop]
Session=xfce

```

For user2:

```
[Desktop]
Session=cinnamon

```

For user3:

```
[Desktop]
Session=gnome

```

### 自动登录

如果要不输入密码就自动登录一个用户，找到 `/etc/lxdm/lxdm.conf` 中的:

```
#autologin=username

```

取下前面的注释，并改成要自动登录的用户名。

这样 LXDM 就会在第一次启动时自动登录到指定的账户。但是如果注销了账户，下次登录的时候还是需要密码。如果密码为空，那么就没有办法再登录。要不使用密码就登录，先删除密码：

```
$ passwd -d USERNAME

```

然后编辑 LXDM 的 PAM 文件 `/etc/pam.d/lxdm`。此目录中的文件描述各个程序给用户的权限，将

```
auth    required    pam_unix.so

```

改为:

```
auth    required    pam_unix.so nullok

```

这样 pam_unix 认证模块就会接受空密码了。

### 注销行为

LXDM 有点让人意外的是用户注销时并不会清空用户的桌面背景和用户进程。如果要修改这个行为，请编辑 `/etc/lxdm/PostLogout` 为：

```
#!/bin/sh

# Kills all your processes when you log out.
killall --user $USER -TERM

# Set's the desktop background to solid black. Useful if you have multiple monitors.
xsetroot -solid black

```

**注意:** 这将会停止 tmux、urxvtd 等用户进程。

将 killall 命令替换为下列内容可以不停止 ssh 和 screen：

```
 ps --user $USER | egrep -v "ssh|screen" | cut -b11-15 | xargs -t kill

```

### 会话列表

要配置 LXDM 的会话列表，可以修改`/usr/share/xsessions` 中的 Desktop 文件，示例：

```
[Desktop Entry]
Encoding=UTF-8
Name=Openbox
Comment=Log in using the Openbox window manager (without a session manager)
Exec=/usr/bin/openbox-session
TryExec=/usr/bin/openbox-session
Icon=openbox.png
Type=XSession

```

## 提示和技巧

### Adding face icons

A 96x96 px image (jpg or png) can optionally be displayed on a per-user basis replacing the stock icon. Simply copy or symlink the target image to `$HOME/.FACE`. The [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) package supplies some default icons suitable for the lxdm screen. Look under `/usr/share/pixmaps/faces` after installing that package.

**Note:** Users need not keep [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) installed to use this images. Simply install it, copy them elsewhere, and remove it.

**Note:** The user's directory needs have r-x permissions for others and the .face file needs have r-- permissions for others. Obviously though this has security and access implications as now anyone can browse your home directory.

### 自动用户和切换用户

LXDM 可以让多个用户同时登陆到不同 ttys，使用此用户可以自动以新用户登陆，并保留老用户的会话：

```
$ lxdm -c USER_SWITCH

```

**注意:** 当新用户登陆是，使用的是下一个tty。例如 tty7 上的用户甲登陆并使用 USER_SWITCH 命令后，新登陆的用户乙将会位于 tty8。

[XScreenSaver](/index.php/XScreenSaver "XScreenSaver") 也支持此功能，参见 [XScreenSaver#LXDM](/index.php/XScreenSaver#LXDM "XScreenSaver").

If you use the [Xfce](/index.php/Xfce "Xfce") desktop, the Switch User functionality of its Action Button panel item specifically looks for the *gdmflexiserver* executable in order to enable itself. If you provide it with an executable shell script `/usr/bin/gdmflexiserver` consisting of

```
#!/bin/sh
/usr/bin/lxdm -c USER_SWITCH

```

then user switching in Xfce should work fine also with LXDM.

[XScreenSaver](/index.php/XScreenSaver "XScreenSaver") can also perform this task. For more, see the [this section](/index.php/XScreenSaver#LXDM "XScreenSaver") of the Xscreensaver article.

### 主题

The LXDM themes are located in `/usr/share/lxdm/themes`.

There is only one theme provided with LXDM, namely Industrial. To display the background file `wave.svg` which is part of this theme, make sure you have [librsvg](https://www.archlinux.org/packages/?name=librsvg) installed.

[lxdm-themes](https://aur.archlinux.org/packages/lxdm-themes/) provides 6 extra themes. Archlinux, ArchlinuxFull, ArchlinuxTop, Arch-Dark, Arch-Stripes and IndustrialArch. The ArchStripes and ArchDark themes are also provided with [lxdm-git](https://aur.archlinux.org/packages/lxdm-git/) (with different names to avoid file conflicts).

You can configure them on `/etc/lxdm/lxdm.conf`:

```
## the theme of greeter
theme=theme_name

```