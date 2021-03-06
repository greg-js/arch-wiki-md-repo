**翻译状态：** 本文是英文页面 [LXDM](/index.php/LXDM "LXDM") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-03-07，点击[这里](https://wiki.archlinux.org/index.php?title=LXDM&diff=0&oldid=560379)可以查看翻译后英文页面的改动。

相关文章

*   [LXDE](/index.php/LXDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXDE (简体中文)")
*   [显示管理器](/index.php/Display_manager "Display manager")

LXDM 是轻量级的 [LXDE](/index.php/LXDE "LXDE") [桌面环境](/index.php/Desktop_environment "Desktop environment") 使用的 [显示管理器](/index.php/Display_manager "Display manager")。界面使用 [GTK+](/index.php/GTK%2B "GTK+") 2.

LXDM 不支持 XDMCP 协议，要使用 XDMCP，请使用 [LightDM](/index.php/LightDM "LightDM").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 登录时解锁密钥环](#登录时解锁密钥环)
        *   [2.1.1 默认会话](#默认会话)
        *   [2.1.2 全局](#全局)
        *   [2.1.3 分用户配置](#分用户配置)
    *   [2.2 自动登录](#自动登录)
    *   [2.3 注销行为](#注销行为)
    *   [2.4 会话列表](#会话列表)
*   [3 提示和技巧](#提示和技巧)
    *   [3.1 Adding face icons](#Adding_face_icons)
    *   [3.2 自动用户和切换用户](#自动用户和切换用户)
    *   [3.3 主题](#主题)
    *   [3.4 高级会话配置](#高级会话配置)
*   [4 问题处理](#问题处理)
    *   [4.1 白闪](#白闪)

## 安装

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") [lxdm](https://www.archlinux.org/packages/?name=lxdm) 软件包或安装 GTK 软件包 [lxdm-gtk3](https://www.archlinux.org/packages/?name=lxdm-gtk3)。

或者安装[AUR](/index.php/AUR "AUR")中的 [lxdm-git](https://aur.archlinux.org/packages/lxdm-git/).

[启用](/index.php/Enable "Enable") [systemd](/index.php/Systemd "Systemd") 服务 `lxdm.service`。

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
#autologin=dgod

```

取消前面的注释，并将dgod改成要自动登录的用户名。

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

A 96x96 px image (jpg or png) can optionally be displayed on a per-user basis replacing the stock icon. Simply copy or symlink the target image to `$HOME/.face`. The [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) package supplies some default icons suitable for the lxdm screen. Look under `/usr/share/pixmaps/faces` after installing that package.

**Note:** Users need not keep [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) installed to use this images. Simply install it, copy them elsewhere, and remove it.

**Note:** The user's directory needs have r-x permissions for others and the .face file needs have r-- permissions for others. Obviously though this has security and access implications as now anyone can browse your home directory.

**Note:** A graphical tool `lxdm-config` shipped with lxdm can be used to place a `.face` file in the home directory, along with other configuration.

### 自动用户和切换用户

LXDM 可以让多个用户同时登陆到不同 ttys，使用此用户可以自动以新用户登陆，并保留老用户的会话：

```
$ lxdm -c USER_SWITCH

```

**注意:** 当新用户登陆时，使用的是下一个tty。例如 tty7 上的用户甲登陆并使用 USER_SWITCH 命令后，新登陆的用户乙将会位于 tty8。

[XScreenSaver](/index.php/XScreenSaver "XScreenSaver") 也支持此功能，参见 [XScreenSaver#LXDM](/index.php/XScreenSaver#LXDM "XScreenSaver").

### 主题

LXDM 主题位于 `/usr/share/lxdm/themes`.

LXDM 仅提供了一个主题 Industrial. 要显示主题背景文件 `wave.svg`，请安装软件包 [librsvg](https://www.archlinux.org/packages/?name=librsvg).

[lxdm-themes](https://aur.archlinux.org/packages/lxdm-themes/) 提供了 6 个额外的主题：Archlinux, ArchlinuxFull, ArchlinuxTop, Arch-Dark, Arch-Stripes 和 IndustrialArch. [lxdm-git](https://aur.archlinux.org/packages/lxdm-git/) 也提供了 ArchStripes 和 ArchDark(名字改了一下以避免冲突).

主题文件通过 `/etc/lxdm/lxdm.conf` 配置:

```
## the theme of greeter
theme=theme_name

```

要让 LXDM 使用 GTK 主题(位于 `/usr/share/themes`)，在配置文件中设置：

```
## GTK theme
gtk_theme=gtk_theme_name

```

### 高级会话配置

用户登录后，LXDM 会按下面顺序引用全部文件：

1.  `/etc/profile`
2.  `~/.profile`
3.  `/etc/xprofile`
4.  `~/.xprofile`

这些文件可以设置会话的环境变量，启动必须的服务例如 ssh-agent. 详情请参考 [Xprofile](/index.php/Xprofile "Xprofile").

LXDM **不会** 引用 `~/.xinitrc`，所以如果需要从使用这些文件的显示管理器迁移到 LXDM，需要将设置移动到其它文件，例如 `~/.xprofile`. LXDM 也不会引用 `~/.bash_profile`.

如果还想使用 `~/.xinitrc`，可以在 `/etc/lxdm/PostLogin` 中加入：

```
source ~/.xinitrc

```

LXDM 也会使用 .[Xresources](/index.php/Xresources "Xresources"), .[Xkbmap](/index.php/Xkbmap "Xkbmap"), 和 .[Xmodmap](/index.php/Xmodmap "Xmodmap"). LXDM 系统配置和用户配置的详细状况可以参考 `/etc/lxdm/Xsession`[[1]](https://projects.archlinux.org/svntogit/community.git/tree/trunk/Xsession?h=packages/lxdm)

## 问题处理

### 白闪

When using the default LXDM `theme=Industrial` and a dark background image (e.g. `bg=/usr/share/backgrounds/img.png`) there may be a short bright flash before LXDM starts. This is caused by the `bg_color:` property of the selected [GTK+](/index.php/GTK%2B "GTK+") theme. To avoid this change `gtk_theme=Adwaita` to `gtk_theme=Adwaita-dark` or to another dark theme.