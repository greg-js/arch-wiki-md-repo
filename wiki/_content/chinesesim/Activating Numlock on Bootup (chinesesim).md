**翻译状态：** 本文是英文页面 [Activating_Numlock_on_Bootup](/index.php/Activating_Numlock_on_Bootup "Activating Numlock on Bootup") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-08-22，点击[这里](https://wiki.archlinux.org/index.php?title=Activating_Numlock_on_Bootup&diff=0&oldid=486330)可以查看翻译后英文页面的改动。

## Contents

*   [1 控制台](#控制台)
    *   [1.1 使用单独服务](#使用单独服务)
    *   [1.2 扩展getty@.service](#扩展getty@.service)
    *   [1.3 Bash alternative](#Bash_alternative)
*   [2 X window](#X_window)
    *   [2.1 startx](#startx)
    *   [2.2 KDE Plasma 用户](#KDE_Plasma_用户)
    *   [2.3 GDM](#GDM)
    *   [2.4 GNOME](#GNOME)
    *   [2.5 Xfce](#Xfce)
    *   [2.6 SDDM](#SDDM)
    *   [2.7 SLiM](#SLiM)
    *   [2.8 OpenBox](#OpenBox)
    *   [2.9 LightDM](#LightDM)
    *   [2.10 LXDM](#LXDM)
    *   [2.11 LXQt](#LXQt)

## 控制台

### 使用单独服务

**Tip:** 这些步骤可以被[install](/index.php/Install "Install") [systemd-numlockontty](https://aur.archlinux.org/packages/systemd-numlockontty/) 并 [enabling](/index.php/Enabling "Enabling") `numLockOnTty` service替代.

首先创造在相关 TTY 上设置 numlock 的脚本：

 `/usr/bin/numlock` 
```
#!/bin/bash

for tty in /dev/tty{1..6}
do
    /usr/bin/setleds -D +num < "$tty";
done

```

然后创建并 [enable](/index.php/Enable "Enable") systemd 服务:

 `/etc/systemd/system/numlock.service` 
```
[Unit]
Description=numlock

[Service]
ExecStart=/usr/bin/numlock
StandardInput=tty
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

### 扩展`getty@.service`

这个方法比使用单独服务简单，不需要在脚本中写入 VT 编号。在原始 gettty unit 文件上添加一段扩展：

 `# systemctl edit getty\@.service` 
```
[Service]
ExecStartPre=/bin/sh -c 'setleds +num < /dev/%I'

```

要禁用登录屏幕上打数字键启用提示，编辑 getty@tty1.service，添加 `--nohints` 到 agetty 选项:

 `# systemctl edit getty@tty1.service` 
```
[Service]
ExecStart=
ExecStart=-/sbin/agetty --nohints --noclear %I $TERM

```

### Bash alternative

将 `setleds -D +num` 加入到 `~/.bash_profile`. 需要注意的是，不同于其他方法，这种方式将会在你登录后才生效。

## X window

有许多可选方案：

### startx

如果你使用startx来启动X window会话，只需安装 [numlockx](https://www.archlinux.org/packages/?name=numlockx) 软件包并将其加入到`~/.xinitrc`中`exec`之前:

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#

numlockx &
exec your_window_manager

```

### KDE Plasma 用户

系统设置的硬件/输入设备/键盘一项中，包含了 NumLock 行为的配置方法。

### GDM

因为`numlock-state`设置,要更改它，您必须更改相应的dconf键（并以`gdm`用户身份执行）

```
# su
# su gdm -s /bin/sh #become gdm user with a shell
sh$ export $(dbus-launch)
sh$ GSETTINGS_BACKEND=dconf gsettings set org.gnome.settings-daemon.peripherals.keyboard numlock-state on
sh$ exit 
$ systemctl restart gdm
#

```

### GNOME

不使用 GDM 的时候，可以将 `numlockx` 加入 GNOME 的启动程序中。 先 [安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") [numlockx](https://www.archlinux.org/packages/?name=numlockx)。然后，添加一个启动命令来启动 numlockx：

```
$ gnome-session-properties

```

在**Startup Applications Preferences** 程序中，点击***添加*** 然后输入：

| Name: | *Numlockx* |
| Command: | */usr/bin/numlockx on* |
| Comment: | *Turns on numlock.* |

**注意:** 这不是系统设置，每个用户都需要单独设置。

### Xfce

在`~/.config/xfce4/xfconf/xfce-perchannel-xml/keyboards.xml`中确保以下值设定为true:

```
<property name="Numlock" type="bool" value="true"/>
<property name="RestoreNumlock" type="bool" value="true"/>

```

### SDDM

在`/etc/sddm.conf`配置文件中, 在`[General]`部分中添加以下行:

```
[General]
Numlock=on

```

### SLiM

取消文件`/etc/slim.conf`中如下行的注释(删除`#`):

```
#numlock             on

```

### OpenBox

在文件 `~/.config/openbox/autostart` 中加入如下内容：

```
numlockx &

```

### LightDM

参见 [LightDM (简体中文)#默认打开小键盘](/index.php/LightDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#默认打开小键盘 "LightDM (简体中文)").

### LXDM

在 `/etc/lxdm/lxdm.conf` 中设置:

```
numlock=1

```

### LXQt

在 `~/.config/lxqt/session.conf` 中设置:

```
numlock=true

```