**翻译状态：** 本文是英文页面 [Xinitrc](/index.php/Xinitrc "Xinitrc") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-08-02，点击[这里](https://wiki.archlinux.org/index.php?title=Xinitrc&diff=0&oldid=389609)可以查看翻译后英文页面的改动。

`~/.xinitrc` 文件是 `xinit` 和它的前端 `startx` 第一次启动时会读取的脚本。通常用在启动 X 时执行[窗口管理器](/index.php/Window_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window manager (简体中文)") 和其他程序，例如启动守护进程和设置环境变量。`xinit`程序用来启动[X窗口系统](/index.php/Xorg "Xorg")，是不使用[显示管理器](/index.php/Display_manager "Display manager")时的第一个客户端。

`~/.xinitrc` 一个主要功能是根据单个用户的设置决定 `/usr/bin/startx` 或 `/usr/bin/xinit` 程序启动的窗口系统。`~/.xinitrc` 中还可以加入许多系统定制选项。大部分显示管理器也会在 xinit 前读取相似的 [xprofile](/index.php/Xprofile "Xprofile") 文件。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
*   [3 在启动的时候自动启用X](#.E5.9C.A8.E5.90.AF.E5.8A.A8.E7.9A.84.E6.97.B6.E5.80.99.E8.87.AA.E5.8A.A8.E5.90.AF.E7.94.A8X)
    *   [3.1 自动登录到虚拟终端](#.E8.87.AA.E5.8A.A8.E7.99.BB.E5.BD.95.E5.88.B0.E8.99.9A.E6.8B.9F.E7.BB.88.E7.AB.AF)
*   [4 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [4.1 从命令行覆盖 xinitrc](#.E4.BB.8E.E5.91.BD.E4.BB.A4.E8.A1.8C.E8.A6.86.E7.9B.96_xinitrc)
    *   [4.2 Making a DE/WM choice](#Making_a_DE.2FWM_choice)
    *   [4.3 不启动窗口管理器，直接启动程序](#.E4.B8.8D.E5.90.AF.E5.8A.A8.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8.EF.BC.8C.E7.9B.B4.E6.8E.A5.E5.90.AF.E5.8A.A8.E7.A8.8B.E5.BA.8F)

## 安装

[安装](/index.php/Install "Install") 软件包 [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit). 此软件包提供了 *xinit* 和 *startx*。

## 配置

如果用户主目录中存在 `.xinitrc`，*startx* 和 *xinit* 会执行此文件。如果不存在，*startx* 会执行 `/etc/X11/xinit/xinitrc`。这个文件默认启动 [Twm](/index.php/Twm "Twm") 和 [Xterm](/index.php/Xterm "Xterm") (*xinit* 的默认行为不一样，请参阅 `man 1 xinit`). 所以要设置窗口管理器或桌面环境，先通过复制创建默认文件：

```
$ cp /etc/X11/xinit/xinitrc ~/.xinitrc

```

根据示例文件修改可以保留一些默认行为，例如会引用 `/etc/X11/xinit/xinitrc.d` 中以 `.sh` 结尾的脚本。

然后编辑 `~/.xinitrc` ，例如要使用 [Openbox](/index.php/Openbox "Openbox")，修改为：

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
...

if [ -d /etc/X11/xinit/xinitrc.d ] ; then
    for f in /etc/X11/xinit/xinitrc.d/**?*** ; do
        [ -x "$f" ] && . "$f"
    done
    unset f
fi

# exec gnome-session
# exec startkde
# exec startxfce4
# exec wmaker
# exec icewm
# exec blackbox
# exec fluxbox
# exec openbox-session
# ...or the Window Manager of your choice

xscreensaver **&**
xsetroot -cursor_name left_ptr **&**
**exec** openbox-session

```

`~/.xinitrc` 中应该只有 **一个** 未注释掉的 `exec` 行，而且 exec 行必须位于配置文件的末尾。exec 后面的所有命令只有窗口退出后才会被执行。在窗口管理器前启动的命令应该用 **&** 在后台启动, 否则启动程序会等待它们退出。使用 `exec` 作为前缀会替换当前的进程，这样进程进入后台时 X 不会退出。

现在以普通用户启动 X：

```
 $ startx

```

或者

```
$ xinit -- :1 -nolisten tcp vt$XDG_VTNR

```

*   上面命令在用户登录的虚拟终端执行 [Xorg](/index.php/Xorg "Xorg")，[[1]](http://blog.falconindy.com/articles/back-to-basics-with-x-and-systemd.html) 这样 `logind` 就可以保持认证会话，而且切换虚拟终端也无法跳过屏保。
*   在 xinit 命令中必须使用 `vt$XDG_VTNR` 才能 [保持会话权限](/index.php/General_troubleshooting#Session_permissions "General troubleshooting").
*   *xinit* 在登录了不同的虚拟终端是不会处理多个会话。所以必须通过`-- :*session_no*` 指定会话。如果 X 已经在运行，需要指定 :1 或更高。

## 在启动的时候自动启用X

**注意:** 这种方式将在登陆 tty 启动 X，只有这样才能保持登录会话。

如果使用[Bash](/index.php/Bash "Bash"), 编辑 `~/.bash_profile`,加入如下内容. 如果文件不存在，从 `/etc/skel/.bash_profile` 复制一个框架版本。

如果使用 [zsh](/index.php/Zsh "Zsh")，则编辑 `~/.zprofile``~/.zlogin`.

```
[[ -z $DISPLAY && $XDG_VTNR -eq 1 ]] && exec startx

```

**注意:**

*   如果想在多个 VT 上使用图形登陆，可以将`-eq 1`修改为`-le 3` (vt1 到 vt3)
*   X 必须在登陆 TTY 启动，这样才能保持 logind 会话。默认的`/etc/X11/xinit/xserverrc`，已经进行了处理。
*   `xinit` may be faster than `startx`, but needs additional parameter such as `-nolisten tcp`.
*   If you would like to remain logged in when the X session ends, remove `exec`.

*   此方法与[automatic login to virtual console](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console")一起可以实现自动登陆。
*   如果 X 被关闭，用户将自动退出。要避免这个问题，删除 `exec`。
*   要将 X 会话的输出重定向到一个文件，请创建一个别名[alias](/index.php/Alias "Alias"):

	 `alias startx='startx &> ~/.xlog'` 

See also [Fish#Start X at login](/index.php/Fish#Start_X_at_login "Fish") and [Systemd/User#Automatic login into Xorg without display manager](/index.php/Systemd/User#Automatic_login_into_Xorg_without_display_manager "Systemd/User").

### 自动登录到虚拟终端

This method can be combined with [automatic login to virtual console](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console"). When doing this you have to set correct dependencies for the autologin systemd service to ensure that dbus is started before `~/.xinitrc` is read and hence pulseaudio started (see: [BBS#155416](https://bbs.archlinux.org/viewtopic.php?id=155416))

## 提示和技巧

### 从命令行覆盖 xinitrc

如果你有一个可用的 `~/.xinitrc`, 件，只想尝试下其他的窗口管理器/桌面环境，你可从命令行给 `startx` 完整路径

```
$ startx /full/path/to/window-manager

```

Note that the full path is **required**. Optionally, you can also override `/etc/X11/xinit/xserverrc` file (which stores the default X server options) with custom options by appending them after `--`, e.g.:

```
$ startx /usr/bin/enlightenment -- -nolisten tcp -br +bs -dpi 96 vt$XDG_VTNR

```

or

```
$ xinit /usr/bin/enlightenment -- -nolisten tcp -br +bs -dpi 96 vt$XDG_VTNR

```

参阅 `man startx`.

### Making a DE/WM choice

If you are frequently switching between different DEs/WMs, it is recommended to either use a [Display manager](/index.php/Display_manager "Display manager") or add code to `.xinitrc`. The code described next consists of a simple few lines, which will take the argument and load the desired desktop environment or window manager.

The following example `~/.xinitrc` shows how to start a particular DE/WM with an argument:

 `~/.xinitrc` 
```
...

# Here Xfce is kept as default
session=${1:-xfce}

case $session in
    awesome           ) exec awesome;;
    bspwm             ) exec bspwm;;
    catwm             ) exec catwm;;
    cinnamon          ) exec cinnamon-session;;
    dwm               ) exec dwm;;
    enlightenment     ) exec enlightenment_start;;
    ede               ) exec startede;;
    fluxbox           ) exec startfluxbox;;
    gnome             ) exec gnome-session;;
    gnome-classic     ) exec gnome-session --session=gnome-classic;;
    i3|i3wm           ) exec i3;;
    icewm             ) exec icewm-session;;
    jwm               ) exec jwm;;
    kde               ) exec startkde;;
    mate              ) exec mate-session;;
    monster|monsterwm ) exec monsterwm;;
    notion            ) exec notion;;
    openbox           ) exec openbox-session;;
    unity             ) exec unity;;
    xfce|xfce4        ) exec startxfce4;;
    xmonad            ) exec xmonad;;
    # No known session, try to run it as command
    *) exec $1;;
esac

```

Then copy the `/etc/X11/xinit/xserverrc` file to your home directory:

```
$ cp /etc/X11/xinit/xserverrc ~/.xserverrc

```

After that, you can easily start a particular DE/WM by passing an argument, e.g.:

```
$ xinit
$ xinit gnome
$ xinit kde
$ xinit wmaker

```

or

```
$ startx
$ startx ~/.xinitrc gnome
$ startx ~/.xinitrc kde
$ startx ~/.xinitrc wmaker

```

### 不启动窗口管理器，直接启动程序

It is possible to start only specific applications without a window manager, although most likely this is only useful with a single application shown in full-screen mode. For example:

 `~/.xinitrc` 
```
...

exec chromium

```

With this method you need to set each application window's geometry through its own configuration files, if possible at all.

**Tip:** This method can be useful to launch graphical games, especially on systems where excluding the memory or CPU usage of a window manager or desktop environment, and possible accessory applications, can help improve the game's execution performance.

See also [Display manager#Starting applications without a window manager](/index.php/Display_manager#Starting_applications_without_a_window_manager "Display manager").