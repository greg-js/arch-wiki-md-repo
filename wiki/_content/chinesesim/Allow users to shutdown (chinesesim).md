**翻译状态：** 本文是英文页面 [Allow_Users_to_Shutdown](/index.php/Allow_Users_to_Shutdown "Allow Users to Shutdown") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-08-29，点击[这里](https://wiki.archlinux.org/index.php?title=Allow_Users_to_Shutdown&diff=0&oldid=463509)可以查看翻译后英文页面的改动。

## 按键和翻转屏幕事件

睡眠、休眠和关机按键的事件以及笔记本屏幕翻转事件由 *logind* 处理，请参考 [Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management").

## 使用 systemd-logind

如果使用 Arch 默认的 [systemd](/index.php/Systemd "Systemd")，安装了 [polkit](https://www.archlinux.org/packages/?name=polkit)，只要会话[没有中断](/index.php/General_troubleshooting#Session_permissions "General troubleshooting")，非远程用户就可以使用电源相关的命令。

要检查会话是否活跃：

```
$ loginctl show-session $XDG_SESSION_ID --property=Active

```

关机命令：

```
$ systemctl poweroff

```

重启命令:

```
$ systemctl reboot

```

按下待机、关机和休眠按钮和盖下显示屏的事件也由 logind 处理（参见 [logind.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/logind.conf.5)）。

## 使用 sudo

首先安装 [sudo](https://www.archlinux.org/packages/?name=sudo), 给用户 [sudo 权限](/index.php/Sudo "Sudo") 或者设置用户仅能执行关机命令，以 root 用户执行 `visudo` 修改 [/etc/sudoers](/index.php/Sudo "Sudo")，替换 *user* 和 *hostname*。

```
*user* *hostname* =NOPASSWD: /usr/bin/systemctl poweroff,/usr/bin/systemctl halt,/usr/bin/systemctl reboot

```

现在这个用户可以用 `sudo shutdown -h now` 命令关机， `sudo reboot` 命令重启了。用户也可以使用 `poweroff` 或 `halt` 关闭系统。