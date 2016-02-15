**翻译状态：** 本文是英文页面 [Allow_Users_to_Shutdown](/index.php/Allow_Users_to_Shutdown "Allow Users to Shutdown") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-12-15，点击[这里](https://wiki.archlinux.org/index.php?title=Allow_Users_to_Shutdown&diff=0&oldid=239434)可以查看翻译后英文页面的改动。

## 使用 systemd-logind

如果你正在使用Arch的默认 [systemd](/index.php/Systemd "Systemd")，非远程会话中的用户可以使用电源相关的命令只要安装了 [polkit](https://www.archlinux.org/packages/?name=polkit) 并且 [会话不中断](/index.php/Xinitrc#Preserving_the_session "Xinitrc")。关机命令：

```
# systemctl poweroff

```

按下待机、关机和休眠按钮和盖下显示屏的事件也由 logind 处理（参见 `man logind.conf`）。

## 使用 sudo

首先安装 sudo：

```
# pacman -S sudo

```

然后，在 root 用户下用 `visudo` 命令添加以下到 `/etc/sudoers` 文件的末端。替换其中的 `**user**` 为你的用户名， `**hostname**` 为你的主机名。

```
**user** **hostname** =NOPASSWD: /sbin/shutdown -h now,/sbin/halt,/sbin/poweroff,/sbin/reboot

```

现在你的用户可以用 `sudo shutdown -h now` 命令关机， `sudo reboot` 命令重启了。用户也可以使用 `poweroff` 或 `halt` 关闭系统。如果你不想被提示输入密码，使用`NOPASSWD:`标记。

为了方便起见，如果你已经启用了 `~/.bashrc`，你可以把这些[别名](/index.php/Bash#Aliases "Bash")添加到里面（或者添加到 `/etc/bash.bashrc` 使全系统生效）：

```
alias reboot="sudo reboot"
alias poweroff="sudo poweroff"
alias halt="sudo halt"

```

## 使用 acpid

使用[acpid](/index.php/Acpid "Acpid")可以允许任何人通过电源按钮物理关机。