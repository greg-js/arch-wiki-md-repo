**翻译状态：** 本文是英文页面 [Systemd/User](/index.php/Systemd/User "Systemd/User") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-09-25，点击[这里](https://wiki.archlinux.org/index.php?title=Systemd%2FUser&diff=0&oldid=401745)可以查看翻译后英文页面的改动。

[systemd (简体中文)](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") 会给每个用户生成一个systemd实例，用户可以在这个实例下管理服务，启动、停止、启用以及禁用他们自己的单元。 这个能力大大方便了那些通常在特定用户下运行的守护进程和服务，比如 [mpd](/index.php/Mpd "Mpd"), 还有像拉取邮件等需要自动执行的任务。 在某些场景下，它甚至可以在指定用户下运行xorg以及整个窗口管理系统。

## Contents

*   [1 工作原理](#.E5.B7.A5.E4.BD.9C.E5.8E.9F.E7.90.86)
*   [2 基础设置](#.E5.9F.BA.E7.A1.80.E8.AE.BE.E7.BD.AE)
    *   [2.1 D-Bus](#D-Bus)
    *   [2.2 环境变量](#.E7.8E.AF.E5.A2.83.E5.8F.98.E9.87.8F)
        *   [2.2.1 DISPLAY和XAUTHORITY](#DISPLAY.E5.92.8CXAUTHORITY)
        *   [2.2.2 PATH](#PATH)
    *   [2.3 随系统自动启动systemd用户实例](#.E9.9A.8F.E7.B3.BB.E7.BB.9F.E8.87.AA.E5.8A.A8.E5.90.AF.E5.8A.A8systemd.E7.94.A8.E6.88.B7.E5.AE.9E.E4.BE.8B)
*   [3 Xorg and systemd](#Xorg_and_systemd)
    *   [3.1 Automatic login into Xorg without display manager](#Automatic_login_into_Xorg_without_display_manager)
    *   [3.2 Xorg as a systemd user service](#Xorg_as_a_systemd_user_service)
*   [4 开发用户单元](#.E5.BC.80.E5.8F.91.E7.94.A8.E6.88.B7.E5.8D.95.E5.85.83)
    *   [4.1 例子](#.E4.BE.8B.E5.AD.90)
    *   [4.2 使用变量的例子](#.E4.BD.BF.E7.94.A8.E5.8F.98.E9.87.8F.E7.9A.84.E4.BE.8B.E5.AD.90)
    *   [4.3 X应用程序须知](#X.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.E9.A1.BB.E7.9F.A5)
*   [5 Some use cases](#Some_use_cases)
    *   [5.1 Persistent terminal multiplexer](#Persistent_terminal_multiplexer)
    *   [5.2 Window manager](#Window_manager)
*   [6 See also](#See_also)

## 工作原理

从systemd 226版本开始，`/etc/pam.d/system-login`默认配置中的`pam_systemd`模块会在用户首次登陆的时候, 自动运行一个 `systemd --user` 实例。 只要用户还有会话存在，这个进程就不会退出；用户所有会话退出时，进程将会被销毁。当 [#随系统自动启动systemd用户实例](#.E9.9A.8F.E7.B3.BB.E7.BB.9F.E8.87.AA.E5.8A.A8.E5.90.AF.E5.8A.A8systemd.E7.94.A8.E6.88.B7.E5.AE.9E.E4.BE.8B) 启用时, 这个用户实例将在系统启动时加载，并且不会被销毁。systemd用户实例负责管理用户服务，用户服务可以使用systemd提供的各种便捷机制来运行守护进程或自动化任务，如socket激活、定时器、依赖体系以及通过cgroup限制进程等。

和系统单元类似，用户单元可以在以下目录找到(按优先级从低到高排序）：

*   `/usr/lib/systemd/user/` 这里存放的是各个软件包安装的服务。
*   `/etc/systemd/user/` 这里存放的是由系统管理员维护的系统范围的用户服务。
*   `~/.config/systemd/user/` 这里存放的是用户自身的服务。

当systemd用户实例启动时，它会将 `default.target` 带起来。其他用户单元可以通过`systemctl --user`来管理。

**Note:**

*   从systemd 206版本开始，`systemd --user` 实例是针对每个用户处理的，而不是针对会话。这样做的原理是用户服务处理的大部分资源，像socket或状态文件是针对每个用户的（存活于用户的主目录下）而不是会话。这意味着所有的用户服务是独立于会话之外运行的。最终，我们得出结论：基于会话运行的程序可能会导致用户服务中断。systemd处理用户会话的方式是非常生硬的(pretty much in flux)。 单会话支持的进展参考 [[1]](https://mail.gnome.org/archives/desktop-devel-list/2014-January/msg00079.html) 和 [[2]](http://lists.freedesktop.org/archives/systemd-devel/2014-March/017552.html) 。
*   `systemd --user` 和 `systemd --system`运行于不同的进程里面，所以用户单元不能引用或依赖于系统单元。

## 基础设置

所有的用户服务都位于 `~/.config/systemd/user` 路径下。 如果你想在首次用户登陆时运行服务，对想要自动启动的服务执行 `systemctl --user enable *service*` 即可。

### D-Bus

有些程序会使用到 [D-Bus (简体中文)](/index.php/D-Bus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "D-Bus (简体中文)") 用户消息总线。 传统的方式是由桌面环境调用 `dbus-launch` 来启动dbus。但从systemd 226版本开始，将由systemd管理用户消息总线。[[3]](https://www.archlinux.org/news/d-bus-now-launches-user-buses/) systemd会为每个用户启动一个*dbus-daemon*，提供`dbus.socket` 和 `dbus.service`用户单元，供用户下的所有会话使用。

**Note:** 如果你之前在`/etc/systemd/user/` 或 `~/.config/systemd/user/` 下创建过这两个单元，现在可以删掉了。

### 环境变量

systemd用户实例不会继承类似`.bashrc`中定义的 [环境变量](/index.php/Environment_variables "Environment variables")。systemd用户实例有三种设置环境变量的方式：

1.  对于有`$HOME`目录的用户，可以在`~/.config/systemd/user.conf`文件中使用`DefaultEnvironment`选项，

这些设置只对当前用户的用户单元有效。

1.  在 `/etc/systemd/user.conf`文件中使用 `DefaultEnvironment` 选项。这个配置在所有的用户单元中可见。
2.  在 `/etc/systemd/system/user@.service.d/` 下增加配置文件设置。 这个配置在所有的用户单元中可见。
3.  在任何时候， 使用 `systemctl --user set-environment` 或 `systemctl --user import-environment`. 对设置之后启动的所有用户单元有效，但已经启动的用户单元不会生效。

**Tip:** 如果想一次设置多个环境变量，可以写一个配置文件，文件里面每一行定义一个环境变量，用"key=value"的键值对表示，然后在你的启动脚本里添加`xargs systemctl --user set-environment < /path/to/file.conf`。

一般情况下，你需要设置`PATH` 这个环境变量。

#### DISPLAY和XAUTHORITY

任何一个X应用程序都需要使用`DISPLAY`来指示使用哪个显示器，而{{|XAUTHORITY}}则是保存了用户授权文件`.Xauthority`的路径，X应用需要用户授权文件中的cookie信息才能访问X Server。如果你想通过systemd单元启动一个X应用，必须先设置这两个环境变量。systemd从[219版本](http://cgit.freedesktop.org/systemd/systemd/tree/NEWS?id=v219#n194)开始提供了一个脚本`/etc/X11/xinit/xinitrc.d/50-systemd-user.sh`，在X启动的时候，将这些环境变量导入到systemd用户会话中。所以除非你不是通过正常的途径启动X，systemd用户服务应该已经包含了这两个变量。

#### PATH

通过 `.bashrc` 或者 `.bash_profile` 设置的环境变量，对systemd都是不可见的。 如果你改变了你的 `PATH` 变量，并且准备在systemd单元运行的应用中使用这个环境变量，你必须在systemd的环境中设置`PATH`。假设你在 `.bash_profile` 中设置了 `PATH`，让systemd感知到这个变化的最好方法是在修改`PATH` 之后，加入以下行通知systemd：

 `~/.bash_profile` 
```
systemctl --user import-environment PATH

```

### 随系统自动启动systemd用户实例

systemd用户实例在用户首次登陆时启动，并在最有一个会话退出时终止。 但有时候，对于一些不依赖于会话的用户进程，在系统启动时加载用户实例，在会话全部结束时，也不停止用户实例是比较有用的。Lingering 就是用来实现这个的。 使用以下命令来启用驻留指定用户：

```
# loginctl enable-linger *username*

```

**Warning:** systemd 服务是 **没有** 会话的， 它们在 *logind* 状态之外运行， 所以不要在 lingering 中启用自动登陆的功能，这会导致 [会话中断](/index.php/General_troubleshooting#Session_permissions "General troubleshooting")。

## Xorg and systemd

使用systemd单元来运行Xorg有好几种方法，下面介绍其中两种，一种是启动一个新的用户会话，在里面运行Xorg服务，另外一种是用systemd用户服务启动Xorg。

### Automatic login into Xorg without display manager

这种方法通过一个系统单元将用户会话带起来，并在用户会话里面启动一个xorg服务，并运行 `~/.xinitrc` 将窗口管理器等启动起来。

你需要配置好[#D-Bus](#D-Bus) 并安装 [xlogin-git](https://aur.archlinux.org/packages/xlogin-git/)。

配置你的[xinitrc](/index.php/Xinitrc "Xinitrc")文件, 让它source `/etc/X11/xinit/xinitrc.d/`目录下的所有文件。`~/.xinitrc` 在运行的时候不要返回(返回意味着会话结束)。你可以通过在xinitrc的最后加上 `wait`命令，或使用`exec` 来运行最后一条命令，最后一条命令应该在整个用户会话都不会退出(如你的窗口管理器)。

会话会使用它自己的dbus守护，而需要用到`dbus.service`的systemd工具会自动连接到会话的dbus实例上。

最后，在 (**root**) 用户下，启用*xlogin*服务，使其开机自启动：

```
# systemctl enable xlogin@*username*

```

整个用户会话都在systemd的作用域下运行，会话内的一切都能正常工作。

### Xorg as a systemd user service

另外一种选择是将[xorg](/index.php/Xorg "Xorg")作为一个systemd用户服务。这是一种不错的方案，因为其他的 X-related units 可以依赖于xorg服务。 但另一方面，这个方案存在某些倒退，这在下面会提到。

从 1.16 版本开始，[xorg-server](https://www.archlinux.org/packages/?name=xorg-server) 提供了两种更好的整合到systemd的方法:

*   可以在无特权模式下运行，设备管理由logind代为管理(参考 Hans de Goede 的 [这个提交](http://cgit.freedesktop.org/xorg/xserver/commit/?id=82863656ec449644cd34a86388ba40f36cea11e9)).
*   可以实现通过socket激活服务 (参考 [这个提交](http://cgit.freedesktop.org/xorg/xserver/commit/?id=b3d3ffd19937827bcbdb833a628f9b1814a6e189)). 这点使得我们不再需要依赖于[systemd-xorg-launch-helper-git](https://aur.archlinux.org/packages/systemd-xorg-launch-helper-git/).

但非常不幸，xorg的无特权模式需要在用户会话里面运行。所以，xorg的用户服务只能在root权限下运行(和1.16版本之前一样)，而不能使用1.16版本提供的无特权模式。

**Note:** 这并不是logind强加的限制，而是xorg需要知道它将要接管的是哪个会话，而现在它通过调用 [logind](http://www.freedesktop.org/wiki/Software/systemd/logind)'s `GetSessionByPID`来获取这个信息(使用xorg自身的pid作为参数)。参见 [这个话题](http://lists.x.org/archives/xorg-devel/2014-February/040476.html) 和 [xorg源码](http://cgit.freedesktop.org/xorg/xserver/tree/hw/xfree86/os-support/linux/systemd-logind.c). 看上去如果xorg通过其依附的tty来获取会话信息的话，这个问题将得到解决。

下面是从用户服务运行xorg的步骤：

1\. 通过编辑`/etc/X11/Xwrapper.config`文件，允许所有用户使用root权限运行xorg：

 `/etc/X11/Xwrapper.config` 
```
allowed_users=anybody
needs_root_rights=yes

```

2\. 把下面systemd单元加到`~/.config/systemd/user`目录下：

 `~/.config/systemd/user/xorg@.socket` 
```
[Unit]
Description=Socket for xorg at display %i

[Socket]
ListenStream=/tmp/.X11-unix/X%i

```
 `~/.config/systemd/user/xorg@.service` 
```
[Unit]
Description=Xorg server at display %i

Requires=xorg@%i.socket
After=xorg@%i.socket

[Service]
Type=simple
SuccessExitStatus=0 1

ExecStart=/usr/bin/Xorg :%i -nolisten tcp -noreset -verbose 2 "vt${XDG_VTNR}"

```

这里`${XDG_VTNR}` 表示xorg将要运行的虚拟终端，可以在服务单元文件里面硬编码，也可像下面那样在环境变量里指定：

```
$ systemctl --user set-environment XDG_VTNR=1

```

**Note:** xorg应该在用户登录的虚拟终端上运行，否则 logind 会认为会话没有激活。

3\. 确保`DISPLAY` 环境变量已经配置，参考 [这里](#DISPLAY).

4\. 接下来，执行以下命令，使得xorg在display 0 和 tty 2 上可以通过socket激活：

```
$ systemctl --user set-environment XDG_VTNR=2     # So that xorg@.service knows which vt use
$ systemctl --user start xorg@0.socket            # Start listening on the socket for display 0

```

现在，在tty 2上运行任意的X应用，xorg都会自动启动。

可以在`.bash_profile`里面把环境变量 `XDG_VTNR` 设置到systemd环境里面。在这之后，你可以使用systemd单元启动任意的X应用，包括窗口管理器。当然，这些systemd单元必须依赖于`xorg@0.socket`。

**Warning:** 当前，通过用户服务启动窗口管理器意味着它是在会话之外运行的，这将带来以下问题: [break the session](/index.php/General_troubleshooting#Session_permissions "General troubleshooting"). 但是，systemd的开发者看上去更倾向于这样(?)。参见 [[4]](https://mail.gnome.org/archives/desktop-devel-list/2014-January/msg00079.html) 和 [[5]](http://lists.freedesktop.org/archives/systemd-devel/2014-March/017552.html)

## 开发用户单元

### 例子

下面是 mpd 服务用户版本的例子:

 `~/.config/systemd/user/mpd.service` 
```
[Unit]
Description=Music Player Daemon

[Service]
ExecStart=/usr/bin/mpd --no-daemon

[Install]
WantedBy=default.target

```

### 使用变量的例子

下面是 `sickbeard.service` 用户版本的例子, 在配置中，使用了主目录变量(%h):

 `~/.config/systemd/user/sickbeard.service` 
```
[Unit]
Description=SickBeard Daemon

[Service]
ExecStart=/usr/bin/env python2 /opt/sickbeard/SickBeard.py --config %h/.sickbeard/config.ini --datadir %h/.sickbeard

[Install]
WantedBy=default.target

```

在`man systemd.unit`的SPECIFIERS章节中，详细介绍了各种变量, `%h` 指示符将使用运行该服务的用户的主目录替代。更多的变量参考 [systemd](/index.php/Systemd "Systemd") 的 manpages。

### X应用程序须知

大多数X应用运行都需要 `DISPLAY` 变量。如何让所有systemd用户实例看到这个环境变量，参考 [#DISPLAY和XAUTHORITY](#DISPLAY.E5.92.8CXAUTHORITY)。

## Some use cases

### Persistent terminal multiplexer

You may wish your user session to default to running a terminal multiplexer, such as [GNU Screen](/index.php/GNU_Screen "GNU Screen") or [Tmux](/index.php/Tmux "Tmux"), in the background rather than logging you into a window manager session. Separating login from X login is most likely only useful for those who boot to a TTY instead of to a display manager (in which case you can simply bundle everything you start in with myStuff.target).

To create this type of user session, procede as above, but instead of creating wm.target, create multiplexer.target:

```
[Unit]
Description=Terminal multiplexer
Documentation=info:screen man:screen(1) man:tmux(1)
After=cruft.target
Wants=cruft.target

[Install]
Alias=default.target
```

`cruft.target`, like `mystuff.target` above, should start anything you think should run before tmux or screen starts (or which you want started at boot regardless of timing), such as a GnuPG daemon session.

You then need to create a service for your multiplexer session. Here is a sample service, using tmux as an example and sourcing a gpg-agent session which wrote its information to `/tmp/gpg-agent-info`. This sample session, when you start X, will also be able to run X programs, since DISPLAY is set.

```
[Unit]
Description=tmux: A terminal multiplixer 
Documentation=man:tmux(1)
After=gpg-agent.service
Wants=gpg-agent.service

[Service]
Type=forking
ExecStart=/usr/bin/tmux start
ExecStop=/usr/bin/tmux kill-server
Environment=DISPLAY=:0
EnvironmentFile=/tmp/gpg-agent-info

[Install]
WantedBy=multiplexer.target
```

Once this is done, `systemctl --user enable` `tmux.service`, `multiplexer.target` and any services you created to be run by `cruft.target` and you should be set to go! Activated `user-session@.service` as described above, but be sure to remove the `Conflicts=getty@tty1.service` from `user-session@.service`, since your user session will not be taking over a TTY. Congratulations! You have a running terminal multiplexer and some other useful programs ready to start at boot!

### Window manager

To run a window manager as a systemd service, you first need to run [#Xorg as a systemd user service](#Xorg_as_a_systemd_user_service). In the following we will use awesome as an example:

 `~/.config/systemd/user/awesome.service` 
```
[Unit]
Description=Awesome window manager
After=xorg.target
Requires=xorg.target

[Service]
ExecStart=/usr/bin/awesome
Restart=always
RestartSec=10

[Install]
WantedBy=wm.target

```

**Note:** The `[Install]` section includes a `WantedBy` part. When using `systemctl --user enable` it will link this as `~/.config/systemd/user/wm.target.wants/*window_manager*.service`, allowing it to be started at login. Is recommended to enable this service, not to link it manually.

## See also

*   [KaiSforza's Bitbucket wiki](https://bitbucket.org/KaiSforza/systemd-user-units/wiki/Home)
*   [Zoqaeski's units on GitHub](https://github.com/zoqaeski/systemd-user-units)
*   [Collection of useful systemd user units](https://github.com/grawity/systemd-user-units)
*   [Arch forum thread about changes in systemd 206 user instances](https://bbs.archlinux.org/viewtopic.php?id=167115)