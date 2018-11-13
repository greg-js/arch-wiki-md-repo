相关文章

*   [Display manager (简体中文)](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")

**翻译状态：** 本文是英文页面 [Getty](/index.php/Getty "Getty") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-08-31，点击[这里](https://wiki.archlinux.org/index.php?title=Getty&diff=0&oldid=532676)可以查看翻译后英文页面的改动。

[getty](https://en.wikipedia.org/wiki/getty_(Unix) "w:getty (Unix)") 是管理终端线路及其所连终端的程序的通用名称。其目的是保护系统，防止未经授权的访问。通常，每个 getty 进程由 [systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") 启动，一个进程管理一条终端线路。

## Contents

*   [1 安装](#安装)
*   [2 添加额外的虚拟控制台](#添加额外的虚拟控制台)
*   [3 自动登录到虚拟控制台](#自动登录到虚拟控制台)
    *   [3.1 虚拟控制台](#虚拟控制台)
    *   [3.2 串口控制台](#串口控制台)
    *   [3.3 Nspawn 控制台](#Nspawn_控制台)
*   [4 将引导消息保留在 tty1 上](#将引导消息保留在_tty1_上)
*   [5 参考资料](#参考资料)

## 安装

*agetty* 是 Arch Linux 中默认的 getty 程序，它是 [util-linux](https://www.archlinux.org/packages/?name=util-linux) 包的一部分。它在等待登录时修改 TTY 设置，使得换行符不会转换为 CR-LF，否则会使打印到控制台的消息产生“阶梯效应”。Agetty 管理着虚拟控制台，Arch Linux 中默认提供六个虚拟控制台。一般按 `Ctrl+Alt+F1` 到 `Ctrl+Alt+F6` 来访问它们。

其他可选替代包括：

*   **mingetty** — 一个允许自动登录的最小化 getty。

	[mingetty](https://aur.archlinux.org/packages/mingetty/) || [mingetty](https://aur.archlinux.org/packages/mingetty/)

*   **fbgetty** — 类似于 mingetty，支持帧缓冲。

	[http://projects.meuh.org/fbgetty/](http://projects.meuh.org/fbgetty/) || [fbgetty](https://aur.archlinux.org/packages/fbgetty/)

*   **mgetty** — 在 Unix 下处理调制解调器各个方面功能的程序。

	[http://mgetty.greenie.net/](http://mgetty.greenie.net/) || [mgetty](https://aur.archlinux.org/packages/mgetty/)

## 添加额外的虚拟控制台

打开 `/etc/systemd/logind.conf` 文件并将 **NAutoVTs=6** 设置为你想要在启动时得到的虚拟控制台数量。

如果你想临时获取一个控制台，可以为所需的 TTY 启动一个 getty 服务，执行：

```
$ systemctl start getty@ttyN.service

```

## 自动登录到虚拟控制台

配置自动登录要使用 systemd 的 [附加代码片段 (drop-in snippet)](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#修改现存单元文件 "Systemd (简体中文)") 功能来重写传递给 *agetty* 的默认参数。

虚拟控制台和串口控制台的配置是不同的。大多数情况下，你应该是想在虚拟控制台下设置自动登录（这种控制台的设备名称为 `tty*N*`，其中 `*N*` 是一个数字）。串口控制台的自动登录配置稍有不同，它们的设备名称类似于 `ttyS*N*`，其中 `*N*` 是一个数字。

### 虚拟控制台

**注意:** [根据用户报告](https://bbs.archlinux.org/viewtopic.php?id=238576)这种方法可能会影响系统休眠。

要 [修改现存单元文件](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#修改现存单元文件 "Systemd (简体中文)")，可以手动创建下列附加文件，或执行 `systemctl edit getty@tty1` 并输入附加代码片段 (drop-in snippet) 的内容：

 `/etc/systemd/system/getty@tty1.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=-/usr/bin/agetty --autologin *username* --noclear %I $TERM
```

**提示：** 默认 `getty@.service` 中的 `Type=idle` 选项将会推迟该服务的启动时间，直到所有任务（该单元的前置任务）已经完成，防止启动信息淹没了登录提示符。当 [自动启动 X](/index.php/Start_X_at_login "Start X at login") 时，可以通过添加 `Type=simple` 到 [附加代码片段 (drop-in snippet)](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#修改现存单元文件 "Systemd (简体中文)") 来立即启动 `getty@tty1.service`，因为此时 init 进程和 *startx* 都被 [屏蔽](/index.php/Silent_boot "Silent boot") 了输出，避免残留启动时的信息。

如果你想用 *tty* 而不是 *tty1*，请参阅 [Systemd 常见问题](/index.php/Systemd_FAQ_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#如何修改默认的_tty_控制台（getty）数量？ "Systemd FAQ (简体中文)")。

### 串口控制台

创建以下文件（及目录）：

 `/etc/systemd/system/serial-getty@ttyS0.service.d/autologin.conf` 
```
[Service]
ExecStart=
ExecStart=-/usr/bin/agetty --autologin *username* -s %I 115200,38400,9600 vt102
```

### Nspawn 控制台

要为 [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") 容器配置自动登录，需要重写 *console-getty* 服务：

 `/etc/systemd/system/console-getty.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=-/sbin/agetty --noclear --autologin *username* --keep-baud console 115200,38400,9600 $TERM
```

## 将引导消息保留在 tty1 上

默认情况下，Arch 会启动 `getty@tty1` 服务。该服务单元文件已经写入了 `--noclear` 参数，它可以阻止 agetty 清空屏幕。但是 [systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") 会在启动该服务之前清空屏幕。要关闭这项特性，请创建 `/etc/systemd/system/getty@tty1.service.d/noclear.conf` 文件：

 `/etc/systemd/system/getty@tty1.service.d/noclear.conf` 
```
[Service]
TTYVTDisallocate=no
```

这将仅改写 TTY1 上的 *agetty* 的 `TTYVTDisallocate` 参数，并保持全局服务文件 `/usr/lib/systemd/system/getty@.service` 不变。可参阅 [Systemd (简体中文)#修改现存单元文件](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#修改现存单元文件 "Systemd (简体中文)")。

**注意:**

*   确保从 [内核参数](/index.php/Kernel_parameters_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel parameters (简体中文)") 中移除了 `quiet`。
*   KMS 晚启动可能会造成部分早期启动信息丢失。请参阅 [Kernel mode setting (简体中文)#KMS 早启动](/index.php/Kernel_mode_setting_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#KMS_早启动 "Kernel mode setting (简体中文)") 或 [Kernel mode setting (简体中文)#禁用 KMS](/index.php/Kernel_mode_setting_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#禁用_KMS "Kernel mode setting (简体中文)")。

## 参考资料

*   [Systemd (简体中文)#修改默认运行级别/目标](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#修改默认运行级别/目标 "Systemd (简体中文)")
*   [The TTY demystified](http://www.linusakesson.net/programming/tty/)
*   [Wikipedia:Tty (unix)](https://en.wikipedia.org/wiki/Tty_(unix) "wikipedia:Tty (unix)")