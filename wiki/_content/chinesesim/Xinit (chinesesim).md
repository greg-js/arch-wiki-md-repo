相关文章

*   [Display manager (简体中文)](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")
*   [Start X at Login (简体中文)](/index.php/Start_X_at_Login_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Start X at Login (简体中文)")
*   [Xorg_(简体中文)](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")
*   [Xprofile_(简体中文)](/index.php/Xprofile_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xprofile (简体中文)")
*   [Xresources](/index.php/Xresources "Xresources")

**翻译状态：** 本文是英文页面 [xinit](/index.php/Xinit "Xinit") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-05-10，点击[这里](https://wiki.archlinux.org/index.php?title=xinit&diff=0&oldid=516945)可以查看翻译后英文页面的改动。

摘自 [Wikipedia](https://en.wikipedia.org/wiki/xinit "wikipedia:xinit"):

	用户可以通过 **xinit** 程序手动启动 [Xorg](/index.php/Xorg "Xorg") 显示服务器，[startx(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/startx.1) 脚本是 [xinit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xinit.1) 的前端。

*xinit* 和 *startx* 可以带一个可选的客户端程序参数，如果未提供这个参数，它们会从 `~/.xinitrc` 确认要启动的客户端。所以 `xinit /usr/bin/foo` 等价于在 `~/.xinitrc` 中设置 `exec foo` 并执行 `xinit`。

*xinit* 通常用在启动 X 时执行[窗口管理器](/index.php/Window_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window manager (简体中文)") 或 [桌面环境](/index.php/Desktop_environment "Desktop environment")。虽然可以使用 *xinit* 在无窗口管理器的情况下启动图形程序，大部分图形程序都需要一个兼容 [EWMH](https://en.wikipedia.org/wiki/Extended_Window_Manager_Hints "wikipedia:Extended Window Manager Hints") 的窗口管理器。`~/.xinitrc` 可以启动依赖 X 的程序，并在 X 启动时设置环境变量。[显示管理器](/index.php/Display_manager "Display manager") 启动 [Xorg](/index.php/Xorg "Xorg") 并读取 [xprofile](/index.php/Xprofile "Xprofile")。

## Contents

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 xinitrc](#xinitrc)
    *   [2.2 xserverrc](#xserverrc)
*   [3 使用](#使用)
*   [4 在启动时自动启用 X](#在启动时自动启用_X)
*   [5 提示和技巧](#提示和技巧)
    *   [5.1 从命令行覆盖 xinitrc](#从命令行覆盖_xinitrc)
    *   [5.2 Switching between desktop environments/window managers](#Switching_between_desktop_environments/window_managers)
    *   [5.3 不启动窗口管理器，直接启动程序](#不启动窗口管理器，直接启动程序)
    *   [5.4 Output redirection using startx](#Output_redirection_using_startx)

## 安装

[安装](/index.php/Install "Install") 软件包 [xorg-xinit](https://www.archlinux.org/packages/?name=xorg-xinit)。

## 配置

### xinitrc

如果用户主目录中存在 `.xinitrc`，*startx* 和 *xinit* 会执行此文件。如果不存在，*startx* 会执行默认的 `/etc/X11/xinit/xinitrc`。这个文件默认启动 [Twm](/index.php/Twm "Twm") 和 [Xterm](/index.php/Xterm "Xterm"). *xinit* 的默认行为不一样，请参阅 [xinit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xinit.1)。要设置窗口管理器或桌面环境，先通过复制创建默认文件：

```
$ cp /etc/X11/xinit/xinitrc ~/.xinitrc

```

根据示例文件修改可以保留一些默认行为，例如会引用 `/etc/X11/xinit/xinitrc.d` 中以 `.sh` 结尾的脚本。

然后编辑 `~/.xinitrc` ，例如要使用 [Openbox](/index.php/Openbox "Openbox")，修改为：

```
...
xscreensaver **&**
xsetroot -cursor_name left_ptr **&**
**exec** openbox-session

```

`~/.xinitrc` 中应该只有 **一个** 未注释掉的 `exec` 行，而且 exec 行必须位于配置文件的末尾。exec 后面的所有命令只有窗口退出后才会被执行。在窗口管理器前启动的命令，例如屏保和壁纸程序，必须自行 fork 后台进程或用`&`在后台启动, 否则启动程序会等待它们退出才会启动窗口管理器或桌面环境。使用 `exec` 作为前缀会替换当前的进程，这样进程进入后台时 X 不会退出。

某些程序，比如 [xrdb](/index.php/Xrdb "Xrdb")，不应该被 fork. 使用 `exec` 前缀时，程序将会用窗口管理器进程替换脚本进程，所以即使进程进入后台 X 也不会退出。

### xserverrc

`xserverrc` 文件是一个启动 X server 的 shell 脚本。如果存在 `~/.xserverrc` ，*startx* 和 *xinit* 都会执行这个文件。如果文件不存在，*startx* 会使用 `/etc/X11/xinit/xserverrc`.

为了维护 `logind` 的 [authenticated session 会话](/index.php/General_troubleshooting#Session_permissions "General troubleshooting")，避免切换终端时跳过屏幕锁， 必须找用户登录的虚拟终端启动 [Xorg](/index.php/Xorg "Xorg")。[[1]](http://blog.falconindy.com/articles/back-to-basics-with-x-and-systemd.html) 所以建议在 `~/.xserverrc` 中指定 `vt$XDG_VTNR`:

 `~/.xserverrc` 
```

#!/bin/sh
exec /usr/bin/Xorg -nolisten tcp "$@" vt$XDG_VTNR

```

如果要让 X 在其他的终端启动，可以使用 `/usr/lib/systemd/systemd-multi-seat-x` 提供的 X server 包裹程序。修改 `~/.xserverrc`，可以让 *xinit* 和*startx* 都使用这个包裹程序.

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

## 在启动时自动启用 X

先确保 *startx* 已经配置好了。

**注意:** 这种方式将在登陆 tty 启动 X，只有这样才能保持登录会话。

如果使用[Bash](/index.php/Bash "Bash"), 编辑 `~/.bash_profile`,加入如下内容. 如果文件不存在，从 `/etc/skel/.bash_profile` 复制一个框架版本。

如果使用 [zsh](/index.php/Zsh "Zsh")，则编辑 `~/.zprofile`.

```
if [[ ! $DISPLAY && $XDG_VTNR -eq 1 ]]; then
  exec startx
fi

```

**注意:**

*   如果想在多个 VT 上使用图形登陆，可以将`-eq 1`修改为`-le 3` (vt1 到 vt3)
*   如果希望在 X 会话终止时保持登入状态，删除 `exec`.

*   此方法与[automatic login to virtual console](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console")一起可以实现自动登陆。
*   如果 X 被关闭，用户将自动退出。要避免这个问题，删除 `exec`。
*   要将 X 会话的输出重定向到一个文件，请创建一个别名[alias](/index.php/Alias "Alias"):

	 `alias startx='startx &> ~/.xlog'` 

参阅 [Fish#Start X at login](/index.php/Fish#Start_X_at_login "Fish") 和 [Systemd/User#Automatic login into Xorg without display manager](/index.php/Systemd/User#Automatic_login_into_Xorg_without_display_manager "Systemd/User").

可以和 [自动登录到虚拟终端](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console")一起使用.

## 提示和技巧

### 从命令行覆盖 xinitrc

如果你有一个可用的 `~/.xinitrc`, 件，只想尝试下其他的窗口管理器/桌面环境，你可从命令行给 `startx` 完整路径

```
$ startx /full/path/to/window-manager

```

必须使用完整 **required**. 还有一个选项是为 [#xserverrc](#xserverrc) 提供额外参数，加在 `--` 后面，例如：

```
 $ startx /usr/bin/enlightenment -- -br +bs -dpi 96

```

参阅 [startx(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/startx.1).

### Switching between desktop environments/window managers

If you are frequently switching between different desktop environments or window managers, it is convenient to either use a [display manager](/index.php/Display_manager "Display manager") or expand `.xinitrc` to make the switching possible.

The following example `~/.xinitrc` shows how to start a particular desktop environment or window manager with an argument:

 `~/.xinitrc` 
```
...

# Here Xfce is kept as default
session=${1:-xfce}

case $session in
    i3|i3wm           ) exec i3;;
    kde               ) exec startkde;;
    xfce|xfce4        ) exec startxfce4;;
    # No known session, try to run it as command
    *                 ) exec $1;;
esac

```

To pass the argument *session*:

```
$ xinit *session*

```

or

```
$ startx ~/.xinitrc *session*

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

### Output redirection using startx

See [Xorg#Broken redirection](/index.php/Xorg#Broken_redirection "Xorg") for details.