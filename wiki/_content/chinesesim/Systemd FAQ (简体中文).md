**翻译状态：** 本文是英文页面 [Systemd_FAQ](/index.php/Systemd_FAQ "Systemd FAQ") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-10-18，点击[这里](https://wiki.archlinux.org/index.php?title=Systemd_FAQ&diff=0&oldid=338039)可以查看翻译后英文页面的改动。

## Contents

*   [1 常见问题](#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98)
    *   [1.1 为什么控制台上会显示日志信息？](#.E4.B8.BA.E4.BB.80.E4.B9.88.E6.8E.A7.E5.88.B6.E5.8F.B0.E4.B8.8A.E4.BC.9A.E6.98.BE.E7.A4.BA.E6.97.A5.E5.BF.97.E4.BF.A1.E6.81.AF.EF.BC.9F)
    *   [1.2 如何修改默认的 tty 控制台（getty）数量？](#.E5.A6.82.E4.BD.95.E4.BF.AE.E6.94.B9.E9.BB.98.E8.AE.A4.E7.9A.84_tty_.E6.8E.A7.E5.88.B6.E5.8F.B0.EF.BC.88getty.EF.BC.89.E6.95.B0.E9.87.8F.EF.BC.9F)
    *   [1.3 怎样输出更详细的开机信息？](#.E6.80.8E.E6.A0.B7.E8.BE.93.E5.87.BA.E6.9B.B4.E8.AF.A6.E7.BB.86.E7.9A.84.E5.BC.80.E6.9C.BA.E4.BF.A1.E6.81.AF.EF.BC.9F)
    *   [1.4 开机后控制台信息会被清空，如何避免？](#.E5.BC.80.E6.9C.BA.E5.90.8E.E6.8E.A7.E5.88.B6.E5.8F.B0.E4.BF.A1.E6.81.AF.E4.BC.9A.E8.A2.AB.E6.B8.85.E7.A9.BA.EF.BC.8C.E5.A6.82.E4.BD.95.E9.81.BF.E5.85.8D.EF.BC.9F)
    *   [1.5 Systemd 需要哪些内核模块?](#Systemd_.E9.9C.80.E8.A6.81.E5.93.AA.E4.BA.9B.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97.3F)
    *   [1.6 怎样知道一个目标需要哪些进程服务？](#.E6.80.8E.E6.A0.B7.E7.9F.A5.E9.81.93.E4.B8.80.E4.B8.AA.E7.9B.AE.E6.A0.87.E9.9C.80.E8.A6.81.E5.93.AA.E4.BA.9B.E8.BF.9B.E7.A8.8B.E6.9C.8D.E5.8A.A1.EF.BC.9F)
    *   [1.7 电脑关闭了但电源没有断。](#.E7.94.B5.E8.84.91.E5.85.B3.E9.97.AD.E4.BA.86.E4.BD.86.E7.94.B5.E6.BA.90.E6.B2.A1.E6.9C.89.E6.96.AD.E3.80.82)
    *   [1.8 切换到 systemd 后，为什么 fakeRAID 没有挂载?](#.E5.88.87.E6.8D.A2.E5.88.B0_systemd_.E5.90.8E.EF.BC.8C.E4.B8.BA.E4.BB.80.E4.B9.88_fakeRAID_.E6.B2.A1.E6.9C.89.E6.8C.82.E8.BD.BD.3F)
    *   [1.9 如何在启动的时候，运行自定义的一个脚本？](#.E5.A6.82.E4.BD.95.E5.9C.A8.E5.90.AF.E5.8A.A8.E7.9A.84.E6.97.B6.E5.80.99.EF.BC.8C.E8.BF.90.E8.A1.8C.E8.87.AA.E5.AE.9A.E4.B9.89.E7.9A.84.E4.B8.80.E4.B8.AA.E8.84.9A.E6.9C.AC.EF.BC.9F)
    *   [1.10 .service 状态显示绿色的 "active (exited)" (例如 iptables)](#.service_.E7.8A.B6.E6.80.81.E6.98.BE.E7.A4.BA.E7.BB.BF.E8.89.B2.E7.9A.84_.22active_.28exited.29.22_.28.E4.BE.8B.E5.A6.82_iptables.29)
    *   [1.11 Failed to issue method call: File exists 错误](#Failed_to_issue_method_call:_File_exists_.E9.94.99.E8.AF.AF)

## 常见问题

最新的已知问题，参见：[TODO](http://cgit.freedesktop.org/systemd/systemd/tree/TODO)。

### 为什么控制台上会显示日志信息？

请自行设置内核日志等级（loglevel）。以前，`/etc/rc.sysinit` 帮我们把 dmesg 的日志等级设置为 `3`，是比较合适的。 [内核参数](/index.php/Kernel_parameters "Kernel parameters")中加入 `loglevel=3` 或 `quiet` 即可。

### 如何修改默认的 tty 控制台（getty）数量？

目前默认仅启动一个 getty，如果切换到其它 tty, 一改新的 getty 会通过 socket 激活方式启动。例如 [Ctl] [Alt] [F2] 会在 tty2 启动 gettty.

默认情况下，最多可以自动启动 6 个 gettty. [F7] 到 [F12] 不会启动 getty. 要修改最大值，在 `/etc/systemd/logind.conf` 中修改 `NAutoVTs`. 如果要启用所有的 [F*x*]，可以将其设置为 12\. 如果要把 [日志输出到 tty12](/index.php/Systemd#Forward_journald_to_.2Fdev.2Ftty12 "Systemd")，可以把 NAutoVTs 设置为 11.

修改启动时启用的 tty 个数，可以采取下面方法：

添加新的 getty：

在 `/etc/systemd/system/getty.target.wants/` 添加新的软链接即可：

```
# ln -sf /usr/lib/systemd/system/getty@.service /etc/systemd/system/getty.target.wants/getty@tty9.service
# systemctl start getty@tty9.service

```

移除 getty：

从 `/etc/systemd/system/getty.target.wants/` 删除对应的软链接即可：

```
# rm /etc/systemd/system/getty.target.wants/getty@tty5.service /etc/systemd/system/getty.target.wants/getty@tty6.service
# systemctl stop getty@tty5.service getty@tty6.service

```

systemd 不使用 `/etc/inittab` 文件。

### 怎样输出更详细的开机信息？

如果内核信息输出后就什么信息都不输出了，很可能是因为你在内核参数中添加了 `quiet`。删除即可，然后你就可以看到一列列绿色的 [ OK ] 和红色的 [ FAILED ]了。

所有信息都记录在系统日志，可以通过 `$ systemctl` 查看系统状态，通过 `journalctl` 查看日志。

### 开机后控制台信息会被清空，如何避免？

自己写一个 getty@tty1.service 文件

把 `/usr/lib/systemd/system/getty@.service` 复制到 `/etc/systemd/system/getty@tty1.service`，修改 `TTYVTDisallocate` 为 `no`.

### Systemd 需要哪些内核模块?

systemd 不支持 3.0 版本之前的内核。

如果是自己编译内核，需要开启一些选项。请参考`/usr/share/doc/systemd/README`.

自己编译 Systemd，请参考[systemd git](http://cgit.freedesktop.org/systemd/systemd/tree/README) 中的版本.

### 怎样知道一个目标需要哪些进程服务？

例如，你可能想搞明白目标单元 `multi-user.target` 究竟启用了哪些服务，那么以下命令即可：

 `$ systemctl show -p "Wants" multi-user.target`  `Wants=rc-local.service avahi-daemon.service rpcbind.service NetworkManager.service acpid.service dbus.service atd.service crond.service auditd.service ntpd.service udisks.service bluetooth.service org.cups.cupsd.service wpa_supplicant.service getty.target modem-manager.service portreserve.service abrtd.service yum-updatesd.service upowerd.service test-first.service pcscd.service rsyslog.service haldaemon.service remote-fs.target plymouth-quit.service systemd-update-utmp-runlevel.service sendmail.service lvm2-monitor.service cpuspeed.service udev-post.service mdmonitor.service iscsid.service livesys.service livesys-late.service irqbalance.service iscsi.service` 

除了 `Wants`，还可以查看各种形式的依赖和被依赖信息：`WantedBy`、`Requires`、`RequiredBy`、`Conflicts`、`ConflictedBy`、`Before`、`After`。

### 电脑关闭了但电源没有断。

使用`systemctl poweroff` 而不是 `systemctl halt`.

### 切换到 systemd 后，为什么 fakeRAID 没有挂载?

请确保使用了 `# systemctl enable dmraid.service` 

### 如何在启动的时候，运行自定义的一个脚本？

在`/etc/systemd/system` 中新建一个文件(名称可以为 *myscript*.service) 然后在其中写入如下内容：

```
[Unit]
Description=My script

[Service]
ExecStart=/usr/bin/my-script

[Install]
WantedBy=multi-user.target 

```

然后开启该守护进程

```
# systemctl enable *myscript*.service

```

本例是说当目标multi-usr载入的时候，会启动你这个自定义脚本。脚本需要有可执行权限。

**注意:** 如果要启动 shell 脚本，请把 `#!/bin/sh` 加到脚本的第一行，下面的做法不会成功`ExecStart=/bin/sh /path/to/script.sh`。

### .service 状态显示绿色的 "active (exited)" (例如 iptables)

这很正常，本例中的 iptables 并不是守护进程，而是由内核控制，所以装载完规则后自动退出了。通过下面命令检查规则是否正确加载

```
# iptables --list

```

### Failed to issue method call: File exists 错误

此错误一般发生在`systemctl enable`创建系统连接到`/etc/systemd/system/`的时候。一般是在切换显示管理器(例如从 GDM 到 KDM)时出现，这时`/etc/systemd/system/display-manager.service` 已经存在。

要解决此问题，禁用原来的显示管理器或者使用 `systemctl -f enable` 覆盖原有链接。