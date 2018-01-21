相关文章

*   [Display manager (简体中文)](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")
*   [Start X at Login (简体中文)](/index.php/Start_X_at_Login_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Start X at Login (简体中文)")
*   [Xorg_(简体中文)](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")
*   [Xprofile_(简体中文)](/index.php/Xprofile_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xprofile (简体中文)")
*   [Xresources](/index.php/Xresources "Xresources")

**翻译状态：** 本文是英文页面 [xinit](/index.php/Xinit "Xinit") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-04，点击[这里](https://wiki.archlinux.org/index.php?title=xinit&diff=0&oldid=442881)可以查看翻译后英文页面的改动。

`~/.xinitrc` 文件是 `xinit` 和它的前端 `startx` 第一次启动时会读取的脚本。通常用在启动 X 时执行[窗口管理器](/index.php/Window_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window manager (简体中文)") 和其他程序，例如启动守护进程和设置环境变量。`xinit`程序用来启动[X窗口系统](/index.php/Xorg "Xorg")，是不使用[显示管理器](/index.php/Display_manager "Display manager")时的第一个客户端。

`~/.xinitrc` 一个主要功能是根据单个用户的设置决定 `/usr/bin/startx` 或 `/usr/bin/xinit` 程序启动的窗口系统。`~/.xinitrc` 中还可以加入许多系统定制选项。大部分显示管理器也会在 xinit 前读取相似的 [xprofile](/index.php/Xprofile "Xprofile") 文件。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 xserverrc](#xserverrc)
    *   [2.2 xinitrc](#xinitrc)
*   [3 使用](#.E4.BD.BF.E7.94.A8)
*   [4 在启动时自动启用 X](#.E5.9C.A8.E5.90.AF.E5.8A.A8.E6.97.B6.E8.87.AA.E5.8A.A8.E5.90.AF.E7.94.A8_X)
    *   [4.1 自动登录到虚拟终端](#.E8.87.AA.E5.8A.A8.E7.99.BB.E5.BD.95.E5.88.B0.E8.99.9A.E6.8B.9F.E7.BB.88.E7.AB.AF)
*   [5 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [5.1 从命令行覆盖 xinitrc](#.E4.BB.8E.E5.91.BD.E4.BB.A4.E8.A1.8C.E8.A6.86.E7.9B.96_xinitrc)
    *   [5.2 Making a DE/WM choice](#Making_a_DE.2FWM_choice)
    *   [5.3 不启动窗口管理器，直接启动程序](#.E4.B8.8D.E5.90.AF.E5.8A.A8.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8.EF.BC.8C.E7.9B.B4.E6.8E.A5.E5.90.AF.E5.8A.A8.E7.A8.8B.E5.BA.8F)

## 安装

[安装](/index.php/Install "Install") 软件包 [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit). 此软件包提供了 *xinit*、*startx*和默认的 xinitrc 文件。

## 配置

### xserverrc

`xserverrc` 文件是一个启动 X server 的 shell 脚本。如果存在 `~/.xserverrc` ，*startx* 和 *xinit* 都会执行这个文件。如果文件不存在，*startx* 会使用 `/etc/X11/xinit/xserverrc`.

为了维护 `logind` 的 [authenticated session 会话](/index.php/General_troubleshooting#Session_permissions "General troubleshooting")，避免切换终端时跳过屏幕锁， 必须找用户登录的虚拟终端启动 [Xorg](/index.php/Xorg "Xorg")。[[1]](http://blog.falconindy.com/articles/back-to-basics-with-x-and-systemd.html) 所以建议在 `~/.xserverrc` 中指定 `vt$XDG_VTNR`:

 `~/.xserverrc` 
```

#!/bin/sh
exec /usr/bin/Xorg -nolisten tcp "$@" vt$XDG_VTNR

```

如果要让 X 在其他的终端启动，可以使用 `/usr/lib/systemd/systemd-multi-seat-x` 提供的 X server 包裹程序。修改 `~/.xserverrc`，可以让 *xinit* 和*startx* 都使用这个包裹程序.

### xinitrc

如果用户主目录中存在 `.xinitrc`，*startx* 和 *xinit* 会执行此文件。如果不存在，*startx* 会执行默认的 `/etc/X11/xinit/xinitrc`。这个文件默认启动 [Twm](/index.php/Twm "Twm") 和 [Xterm](/index.php/Xterm "Xterm"). *xinit* 的默认行为不一样，请参阅 [xinit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xinit.1)。要设置窗口管理器或桌面环境，先通过复制创建默认文件：

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
    for f in /etc/X11/xinit/xinitrc.d/**?*.sh** ; do
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

## some applications that should be run in the background
xscreensaver **&**
xsetroot -cursor_name left_ptr **&**
**exec** openbox-session

```

`~/.xinitrc` 中应该只有 **一个** 未注释掉的 `exec` 行，而且 exec 行必须位于配置文件的末尾。exec 后面的所有命令只有窗口退出后才会被执行。在窗口管理器前启动的命令应该用 **&** 在后台启动, 否则启动程序会等待它们退出。使用 `exec` 作为前缀会替换当前的进程，这样进程进入后台时 X 不会退出。

## 使用

现在以普通用户启动 X：

```
 $ startx

```

或者

```
$ xinit -- :1

```

**Note:** *xinit* 无法在其它 X server 启动时处理多个显示，要使用多显示，需要通过 `-- :*display_number*` 指定，`*display_number*` 是 1 或更高的数值。

选择的窗口管理器或桌面环境就应该正常启动了.

要退出 X, 运行窗口管理器的退出功能，如果窗口管理器未提供此功能，可以运行：

```
$ pkill -15 Xorg

```

**Note:** *pkill* 会杀死所有 X 实例，如果仅希望杀死当前虚拟终端的窗口管理器，运行：
```
$ pkill -15 -t tty"$XDG_VTNR" Xorg

```

`xprop` 是软件包 [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop)提供的。

## 在启动时自动启用 X

先确保 *startx* 已经配置好了。

**注意:** 这种方式将在登陆 tty 启动 X，只有这样才能保持登录会话。

如果使用[Bash](/index.php/Bash "Bash"), 编辑 `~/.bash_profile`,加入如下内容. 如果文件不存在，从 `/etc/skel/.bash_profile` 复制一个框架版本。

如果使用 [zsh](/index.php/Zsh "Zsh")，则编辑 `~/.zprofile`.

```
[ -z "$DISPLAY" -a "$(fgconsole)" -eq 1 ] && exec startx

```

**注意:**

*   如果想在多个 VT 上使用图形登陆，可以将`-eq 1`修改为`-le 3` (vt1 到 vt3)
*   如果希望在 X 会话终止时保持登入状态，删除 `exec`.

*   此方法与[automatic login to virtual console](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console")一起可以实现自动登陆。
*   如果 X 被关闭，用户将自动退出。要避免这个问题，删除 `exec`。
*   要将 X 会话的输出重定向到一个文件，请创建一个别名[alias](/index.php/Alias "Alias"):

	 `alias startx='startx &> ~/.xlog'` 

参阅 [Fish#Start X at login](/index.php/Fish#Start_X_at_login "Fish") 和 [Systemd/User#Automatic login into Xorg without display manager](/index.php/Systemd/User#Automatic_login_into_Xorg_without_display_manager "Systemd/User").

### 自动登录到虚拟终端

可以和 [自动登录到虚拟终端](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console")一起使用.

## 提示和技巧

### 从命令行覆盖 xinitrc

如果你有一个可用的 `~/.xinitrc`, 件，只想尝试下其他的窗口管理器/桌面环境，你可从命令行给 `startx` 完整路径

```
$ startx /full/path/to/window-manager

```

Note that the full path is **required**. Optionally, you can also specify custom options for [#xserverrc](#xserverrc) script by appending them after `--`, e.g.:

```
 $ startx /usr/bin/enlightenment -- -br +bs -dpi 96

```

参阅 [startx(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/startx.1).

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