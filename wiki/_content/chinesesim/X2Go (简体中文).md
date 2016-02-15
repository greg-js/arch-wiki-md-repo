**翻译状态：** 本文是英文页面 [X2Go](/index.php/X2Go "X2Go") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-08-20，点击[这里](https://wiki.archlinux.org/index.php?title=X2Go&diff=0&oldid=389933)可以查看翻译后英文页面的改动。

[X2Go](http://wiki.x2go.org) 使你可以通过网络访问一台计算机的图形化桌面。访问时的网络传输使用了 [Secure Shell](/index.php/Secure_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Secure Shell (简体中文)") 协议，因而传输是加密的。

**注意:** X2Go 并不能兼容所有桌面环境。你可以先查阅 [X2Go 桌面环境兼容性](http://wiki.x2go.org/doku.php/doc:de-compat)，尤其是当你要映射当前的桌面环境时。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 服务器端配置](#.E6.9C.8D.E5.8A.A1.E5.99.A8.E7.AB.AF.E9.85.8D.E7.BD.AE)
    *   [2.1 配置 Secure Shell 守护进程](#.E9.85.8D.E7.BD.AE_Secure_Shell_.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
    *   [2.2 加载 fuse 内核模块](#.E5.8A.A0.E8.BD.BD_fuse_.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97)
    *   [2.3 设置 SQLite 数据库](#.E8.AE.BE.E7.BD.AE_SQLite_.E6.95.B0.E6.8D.AE.E5.BA.93)
    *   [2.4 启动 X2Go 服务器端守护进程](#.E5.90.AF.E5.8A.A8_X2Go_.E6.9C.8D.E5.8A.A1.E5.99.A8.E7.AB.AF.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
*   [3 桌面映射](#.E6.A1.8C.E9.9D.A2.E6.98.A0.E5.B0.84)
*   [4 客户端配置](#.E5.AE.A2.E6.88.B7.E7.AB.AF.E9.85.8D.E7.BD.AE)
*   [5 Various](#Various)
*   [6 排错](#.E6.8E.92.E9.94.99)
    *   [6.1 认证错误](#.E8.AE.A4.E8.AF.81.E9.94.99.E8.AF.AF)
    *   [6.2 No selection screen in x2goclient](#No_selection_screen_in_x2goclient)
*   [7 相关链接](#.E7.9B.B8.E5.85.B3.E9.93.BE.E6.8E.A5)

## 安装

[官方仓库](/index.php/Official_repositories "Official repositories")中提供了下列两个软件包供 [安装](/index.php/Pacman "Pacman") ：

*   [x2goserver](https://www.archlinux.org/packages/?name=x2goserver) - X2Go 服务器
*   [x2goclient](https://www.archlinux.org/packages/?name=x2goclient) - X2Go 基于 Qt4 的客户端

## 服务器端配置

### 配置 Secure Shell 守护进程

X2Go 使用 [Secure Shell](/index.php/Secure_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Secure Shell (简体中文)") 才能工作，所以你首先需要配置 sshd 守护进程使其允许 X11 转发并启动它。参阅 [Secure Shell - X11 转发](/index.php/Secure_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#X11_.E8.BD.AC.E5.8F.91 "Secure Shell (简体中文)") 和 [Secure Shell - 管理 sshd 守护进程](/index.php/Secure_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E7.AE.A1.E7.90.86_sshd_.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B "Secure Shell (简体中文)")。

如果你使用非 POSIX (C) 本地化环境，则需要在[配置文件](/index.php/Secure_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B "Secure Shell (简体中文)")中添加下列配置行：

```
# Allow client to pass locale environment variables（允许客户端跳过本地化环境变量）
AcceptEnv LANG LC_*

```

### 加载 fuse 内核模块

为使服务器端能够访问客户端计算机上的文件，你需要加载 `fuse` [内核模块](/index.php/Kernel_modules_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel modules (简体中文)")。

### 设置 SQLite 数据库

执行下列命令以初始化 SQLite 数据库

```
# x2godbadmin --createdb

```

### 启动 X2Go 服务器端守护进程

至此，只需 [启动](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") `x2goserver.service` 即可。

## 桌面映射

To gain access to the "local desktop" (as opposed to a unique session/desktop environment) you need to install [x2godesktopsharing](https://aur.archlinux.org/packages/x2godesktopsharing/) from the [AUR](/index.php/AUR "AUR"). Then, launch `x2godesktopsharing`.

Note, you do not need x2godesktopsharing to access "local desktop" of user "foo" by user "foo". x2godesktopsharing is for accessing "foo"'s desktop by "foo2" user. Just choose "Connection to local desktop" in "session type" in x2goclient.

## 客户端配置

确保你可以打开一个从客户端到服务器的 ssh 会话

```
ssh username@host

```

然后运行 X2Go 客户端

```
x2goclient

```

现在，你可以创建多个会话，它们将出现在右面并且可以用鼠标点击选中。每一项都是由你的用户名、主机名、IP 地址和 SSH 连接端口组成。进一步，你可以基于不同连接速度（从 modem 到 LAN）以及想要远程启动的不同桌面环境定义若干个配置文件。

**常见错误：** 不要简单地选择 KDE 或 Gnome 的默认设置，since the executables startkde or startgnome are usually not in the PATH when logging in using ssh. Use full paths to startkde or startgnome. You can also start openbox or another window manager.

You should be asked for your password for your user at the server now and after login you will see the X2Go logo for a short time, and -- voila -- the desktop.

**客户端与服务器（桌面）交换数据：** 在 x2go 客户端（例如：笔记本电脑）上，本地目录可被共享。服务器端将通过 fuse 和 sshfs 访问这些目录并将其挂载到服务器端你的家目录下的若干子目录上。这样你就可以在服务器上访问你的笔记本电脑上的数据或者互传文件。也可以每次启动会话时自动挂载共享目录。

**临时离开一个会话：** X2Go 的另一个特色功能就是可以挂起一个会话。这意味着你可以从一个客户端里离开某一个会话，然后用另一个客户端重新打开这个会话（即便是同一地点的另一个客户端）。This can be used to to start a session in the LAN and to reopen it later on a laptop.在此期间，会话数据由一个 postgres 数据库存储和管理。会话的状态由一个名为 x2gocleansessions 的进程来保持。

## Various

**Workaround for failing compositing window manager for remote session**

This is useful for situations, when the computer running x2goserver is used also for local sessions with e.g. compiz as the window manager. For remote connections with x2goclient, compiz fails to load and metacity should be used instead. The following is for GNOME, but could be modified for other desktop environments. (Getting compiz ready is not part of this how-to.)

Create /usr/local/share/applications/gnome-wm-test.desktop:

```
[Desktop Entry]
Type=Application
Encoding=UTF-8
Name=gnome-wm-test
Exec=/usr/local/bin/gnome-wm-test.sh
NoDisplay=true

```

Create script /usr/local/bin/gnome-wm-test.sh:

```
#!/bin/sh
# Script for choosing compiz when possible, otherwise metacity
# Proper way to use this script is to set the key to mk-gnome-wm
# /desktop/gnome/session/required_components/windowmanager
xdpyinfo 2> /dev/null | grep -q "^ *Composite$" 2> /dev/null
IS_X_COMPOSITED=$?
if [ $IS_X_COMPOSITED -eq 0 ] ; then
    gtk-window-decorator &
    WM="compiz ccp --indirect-rendering --sm-client-id $DESKTOP_AUTOSTART_ID"
else
    WM="metacity --sm-client-id=$DESKTOP_AUTOSTART_ID"
fi
exec bash -c "$WM"

```

Modify the following gconf key to start the session with gnome-wm-test window manager:

```
$ gconftool-2 --type string --set /desktop/gnome/session/required_components/windowmanager "gnome-wm-test"

```

## 排错

### 认证错误

如果出现下列错误：

```
Authentification Failed:
The host key for this server was not found but an othertype of key exists.
An Attacker might change the default server key to confuse  
your client into thinking the key does not exist
（认证失败：
  这台服务器的主机密钥未找到，但存在一个其他类型的密钥。
  可能有攻击者改变了默认的服务器密钥以迷惑你的客户端，使之认为该密钥不存在）

```

从 `~/.ssh/known_hosts` 文件中删除该服务器的相应项并尝试重新认证。

### No selection screen in x2goclient

A regression in [iproute2](https://www.archlinux.org/packages/?name=iproute2) causes _ss_ to show no result when specifying the `-u` flag, as done in `/usr/bin/x2golistdesktops`. [[1]](https://marc.info/?l=linux-netdev&m=143018447007958&w=2)

See [[2]](http://bugs.x2go.org/cgi-bin/bugreport.cgi?bug=799), [[3]](https://bbs.archlinux.org/viewtopic.php?pid=1541035) for more information.

## 相关链接

*   [截屏 KDE 会话](http://wiki.archlinux.de/?title=Bild:X2go-1.png)
*   [截屏 配置对话框](http://wiki.archlinux.de/?title=Bild:X2go-2.png)
*   [项目主页](http://x2go.org)