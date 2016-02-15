**翻译状态：** 本文是英文页面 [Activating_Numlock_on_Bootup](/index.php/Activating_Numlock_on_Bootup "Activating Numlock on Bootup") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-04-16，点击[这里](https://wiki.archlinux.org/index.php?title=Activating_Numlock_on_Bootup&diff=0&oldid=250957)可以查看翻译后英文页面的改动。

## Contents

*   [1 控制台](#.E6.8E.A7.E5.88.B6.E5.8F.B0)
    *   [1.1 使用单独服务](#.E4.BD.BF.E7.94.A8.E5.8D.95.E7.8B.AC.E6.9C.8D.E5.8A.A1)
    *   [1.2 扩展getty@.service](#.E6.89.A9.E5.B1.95getty.40.service)
    *   [1.3 Bash alternative](#Bash_alternative)
*   [2 X window](#X_window)
    *   [2.1 startx](#startx)
    *   [2.2 KDM](#KDM)
    *   [2.3 KDE4](#KDE4)
    *   [2.4 GDM](#GDM)
    *   [2.5 GNOME](#GNOME)
    *   [2.6 Xfce](#Xfce)
    *   [2.7 SDDM](#SDDM)
    *   [2.8 SLiM](#SLiM)
    *   [2.9 OpenBox](#OpenBox)
    *   [2.10 LightDM](#LightDM)

## 控制台

### 使用单独服务

*   从 [AUR](/index.php/AUR "AUR") 安装 [systemd-numlockontty](https://aur.archlinux.org/packages/systemd-numlockontty/)，然后启用服务`numLockOnTty.service`。
*   或者，如果您不想安装 aur 软件包来实现这一点，你可以简单地创建一个服务文件在 /etc/systemd/system:

```
[Unit]
Description=Switch on numlock from tty1 to tty6

[Service]
ExecStart=/bin/bash -c 'for tty in /dev/tty{1..6};do /usr/bin/setleds -D +num < \"$tty\";done'

[Install]
WantedBy=multi-user.target
```

**Note:** 文件名应该有一个`.service`后缀，例如`numlock1to6.service`.

创建它后不要忘记启用服务.

### 扩展`getty@.service`

创建目录：

 `# mkdir /etc/systemd/system/getty@.service.d` 

在新建的目录中加入如下文件：

 `activate-numlock.conf` 

```
[Service]
ExecStartPost=/bin/sh -c 'setleds +num < /dev/%I'
```

### Bash alternative

Add `setleds -D +num` to `~/.bash_profile`. Note that, unlike the other methods, this will not take effect until after you log in.

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

### KDM

如果你使用KDM作为登录管理器，可以在`/opt/kde/share/config/kdm/Xsetup`中加入这行：

```
numlockx on

```

### KDE4

系统设置的硬件/输入设备/键盘一项中，包含了 NumLock 行为的配置方法。

### GDM

GDM用户可以将以下代码加入到/etc/gdm/Init/Default：

```
if [ -x /usr/bin/numlockx ]; then
      /usr/bin/numlockx on
fi

```

### GNOME

不使用 GDM 的时候，可以将 `numlockx` 加入 GNOME 的启动程序中。 先从[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)") [安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") [numlockx](https://www.archlinux.org/packages/?name=numlockx)。然后，添加一个启动命令来启动 numlockx：

```
$ gnome-session-properties

```

在**Startup Applications Preferences** 程序中，点击_**添加**_ 然后输入：

| Name: | _Numlockx_ |
| Command: | _/usr/bin/numlockx on_ |
| Comment: | _Turns on numlock._ |

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

参见 [LightDM (简体中文)#默认打开小键盘](/index.php/LightDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E9.BB.98.E8.AE.A4.E6.89.93.E5.BC.80.E5.B0.8F.E9.94.AE.E7.9B.98 "LightDM (简体中文)").