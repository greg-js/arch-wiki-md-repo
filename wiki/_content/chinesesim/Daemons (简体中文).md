**翻译状态：** 本文是英文页面 [Daemon](/index.php/Daemon "Daemon") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-01-03，点击[这里](https://wiki.archlinux.org/index.php?title=Daemon&diff=0&oldid=236086)可以查看翻译后英文页面的改动。

**守护进程**（daemon），指后台运行的、等待特定事件发生并提供服务的程序。典型的例子如网页服务器，等待网页传输请求并提供传输服务；又如ssh服务器，等待用户登入操作。许多守护进程提供**不可见的服务**，比如记录日志（syslog，metalog）、校准时间（ntpd）。详情见手册: `man 7 daemon`

尽管实际意义有所不同，守护进程也可以叫做**系统服务**。实际上，后者似乎是个更好理解的名称。

有时 daemon 也会指在系统启动时运行，但是运行之后不会保留进程的程序。因为它们使用相同的启动关闭框架 (例如 `/etc/rc.d/` 脚本)，所以也叫 daemon. 例如 `/etc/rc.d` 中的 *alsa* 和 *cpufreq* 提供了固定内核模块参数功能，但是完成后不会保留后台进程。

## Contents

*   [1 管理守护进程](#.E7.AE.A1.E7.90.86.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
    *   [1.1 开机时自动启动](#.E5.BC.80.E6.9C.BA.E6.97.B6.E8.87.AA.E5.8A.A8.E5.90.AF.E5.8A.A8)
    *   [1.2 手动启动](#.E6.89.8B.E5.8A.A8.E5.90.AF.E5.8A.A8)
    *   [1.3 重启服务](#.E9.87.8D.E5.90.AF.E6.9C.8D.E5.8A.A1)
    *   [1.4 查看运行状态](#.E6.9F.A5.E7.9C.8B.E8.BF.90.E8.A1.8C.E7.8A.B6.E6.80.81)
    *   [1.5 检查服务是否开机启动](#.E6.A3.80.E6.9F.A5.E6.9C.8D.E5.8A.A1.E6.98.AF.E5.90.A6.E5.BC.80.E6.9C.BA.E5.90.AF.E5.8A.A8)
*   [2 手动添加开机运行的服务](#.E6.89.8B.E5.8A.A8.E6.B7.BB.E5.8A.A0.E5.BC.80.E6.9C.BA.E8.BF.90.E8.A1.8C.E7.9A.84.E6.9C.8D.E5.8A.A1)
*   [3 systemd](#systemd)
*   [4 守护进程列表](#.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B.E5.88.97.E8.A1.A8)
*   [5 参见](#.E5.8F.82.E8.A7.81)

## 管理守护进程

在Arch Linux中, 守护进程是用[systemd](/index.php/Systemd "Systemd")管理的. 用户用[systemctl](/index.php/Systemd#Basic_systemctl_usage "Systemd")命令来管理. systemctl读取*<service>*.service文件中包含怎么和什么时候启动相关的进程. Service的文件保存在`/{etc,usr/lib,run}/systemd/system`中. 看看[systemd#Using units](/index.php/Systemd#Using_units "Systemd") 有关怎么使用systemctl管理守护进程的完整信息.

### 开机时自动启动

在启动的时候添加，删除服务使用 `systemctl enable|disable *<service_name>*`命令

### 手动启动

在系统运行时启动，停止服务, 使用 `systemctl start|stop *<service_name>*`命令.

### 重启服务

为了重启服务, 使用 `systemctl restart *<service_name>*`命令.

### 查看运行状态

查看当前服务的运行状态, 使用 `systemctl status *<service_name>*`命令.

### 检查服务是否开机启动

检查服务是否开机启动，使用 `systemctl is-enabled *<service_name>*; echo $?`命令.

## 手动添加开机运行的服务

`ln -sf /lib/systemd/system/*<service_name>* /etc/systemd/system/*<service_name>*`

## systemd

[systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)")有更详细的介绍。

## 守护进程列表

[此处](/index.php/Daemons_List_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Daemons List (简体中文)")是守护进程的不完全列表, 每个守护进程给出了 initscripts 使用的脚本和 [systemd](/index.php/Systemd "Systemd") 使用的服务文件。

## 参见

*   [Systemd](/index.php/Systemd "Systemd")