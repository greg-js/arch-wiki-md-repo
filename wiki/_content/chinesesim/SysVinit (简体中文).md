**翻译状态：** 本文是英文页面 [SysVinit](/index.php/SysVinit "SysVinit") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-09-20，点击[这里](https://wiki.archlinux.org/index.php?title=SysVinit&diff=0&oldid=228574)可以查看翻译后英文页面的改动。

**init**是Linux内核加载后执行的第一个进程。Arch的默认的 init 程序是[systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat)提供的`/sbin/init`(新安装的系统已经默认使用[systemd](/index.php/Systemd "Systemd")) 或 [sysvinit](https://aur.archlinux.org/packages/sysvinit/).。本文中，**init**指sysvinit。

**inittab**文件位于/etc目录，是init的启动配置文件，其中指定了一些启动脚本、程序的路径，并指定在哪些运行级别执行它们。

**Note:** Arch's initscripts has been officially unsupported since 2012-11-04[[1]](https://www.archlinux.org/news/end-of-initscripts-support/).

## Contents

*   [1 迁移到 Systemd](#.E8.BF.81.E7.A7.BB.E5.88.B0_Systemd)
    *   [1.1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.2 附加信息](#.E9.99.84.E5.8A.A0.E4.BF.A1.E6.81.AF)
*   [2 init、inittab 概览](#init.E3.80.81inittab_.E6.A6.82.E8.A7.88)
*   [3 调整运行级别](#.E8.B0.83.E6.95.B4.E8.BF.90.E8.A1.8C.E7.BA.A7.E5.88.AB)
    *   [3.1 通过启动加载器](#.E9.80.9A.E8.BF.87.E5.90.AF.E5.8A.A8.E5.8A.A0.E8.BD.BD.E5.99.A8)
    *   [3.2 启动之后](#.E5.90.AF.E5.8A.A8.E4.B9.8B.E5.90.8E)
*   [4 inittab](#inittab)
    *   [4.1 默认运行级别](#.E9.BB.98.E8.AE.A4.E8.BF.90.E8.A1.8C.E7.BA.A7.E5.88.AB)
    *   [4.2 主启动脚本](#.E4.B8.BB.E5.90.AF.E5.8A.A8.E8.84.9A.E6.9C.AC)
    *   [4.3 单用户启动](#.E5.8D.95.E7.94.A8.E6.88.B7.E5.90.AF.E5.8A.A8)
    *   [4.4 终端初始化](#.E7.BB.88.E7.AB.AF.E5.88.9D.E5.A7.8B.E5.8C.96)
    *   [4.5 Ctrl-Alt-Del](#Ctrl-Alt-Del)
    *   [4.6 X 程序](#X_.E7.A8.8B.E5.BA.8F)
    *   [4.7 电源检测脚本](#.E7.94.B5.E6.BA.90.E6.A3.80.E6.B5.8B.E8.84.9A.E6.9C.AC)
    *   [4.8 自定义键盘请求](#.E8.87.AA.E5.AE.9A.E4.B9.89.E9.94.AE.E7.9B.98.E8.AF.B7.E6.B1.82)
        *   [4.8.1 触发 kbrequest](#.E8.A7.A6.E5.8F.91_kbrequest)
*   [5 另见](#.E5.8F.A6.E8.A7.81)
*   [6 外部链接](#.E5.A4.96.E9.83.A8.E9.93.BE.E6.8E.A5)

## 迁移到 Systemd

从[2012-10-13版安装介质](https://www.archlinux.org/news/systemd-is-now-the-default-on-new-installations/)开始，安装程序已经默认安装[systemd](https://www.archlinux.org/packages/?name=systemd) 和 [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat)。本部分帮助还在使用[sysvinit](https://aur.archlinux.org/packages/sysvinit/) 和 initscripts 的用户迁移到 **systemd**.

**注意:** 如果是在 VPS 中使用 Arch，请先阅读：[Virtual_Private_Server#Moving_your_VPS_from_initscripts_to_systemd](/index.php/Virtual_Private_Server#Moving_your_VPS_from_initscripts_to_systemd "Virtual Private Server")。

*   阅读[该站](http://freedesktop.org/wiki/Software/systemd/)，了解 systemd。
*   systemd 自己有一套日志（**journal**）系统，用于代替 **syslog**。两者也可以共存，参见后面的[日志部分](#.E6.97.A5.E5.BF.97)。
*   虽然 systemd 可以替换 **cron**、**acpid**、**xinetd** 等的部分功能。至少目前还可以继续使用这些服务，无需立即切换。
*   交互式 initscripts 启动脚本在 systemd 中无法工作。

### 安装

1.  从[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")安装 [systemd](https://www.archlinux.org/packages/?name=systemd) 并添加[内核参数](/index.php/Kernel_parameters "Kernel parameters")`init=/usr/lib/systemd/systemd`
2.  使用 `systemctl enable <服务名>` 启用需要的服务（大致相当于以前 `DAEMONS` 数组的作用，新的服务名称参见 [Daemons_List_(简体中文)](/index.php/Daemons_List_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Daemons List (简体中文)")）。
3.  重启系统，执行命令 `cat /proc/1/comm`，如果返回`systemd`，表示 systemd 已经正常启动。
4.  确认主机名已经正确设置：`hostnamectl set-hostname myhostname`。
5.  删除 initscripts 和 sysvinit，并安装[systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat).
6.  （可选）删除`init=/usr/lib/systemd/systemd`内核参数，现在已经不需要它了。[systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat) 软件包提供了一个软链接，使 systemd 成为默认 init。

### 附加信息

*   如果内核参数中有 `quiet`，建议在一开始先去掉，以便调试。
*   使用 systemd 的时候**无需**将用户加入特殊[用户组](/index.php/Users_and_Groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Users and Groups (简体中文)")（如`sys`、`disk`、`lp`、`network`、`video`、`audio`、`optical`、`storage`、`scanner`、`power`等等）。加入这些组反而会有问题，例如audio组会导致程序阻塞软件混声。每个 PAM 登录都拥有一个 logind 会话，它通过[POSIX ACLs](https://en.wikipedia.org/wiki/Access_control_list "wikipedia:Access control list")，赋予本地会话以声音设备访问权限、通过[udisks](/index.php/Udisks "Udisks")挂载和卸载移动设备的权限等。
*   阅读 [Network Configuration (简体中文)](/index.php/Network_Configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network Configuration (简体中文)")，了解如何配置网络。

## init、inittab 概览

init总是Linux的1号进程，并且是**一切**进程的父进程。通过`pstree`可以形象看出init在所有进程中所处的地位。

 `$ pstree -Ap` 
```
init(1)-+-acpid(3432)
        |-crond(3423)
        |-dbus-daemon(3469)
        |-gpm(3485)
        |-mylogin(3536)
        |-ngetty(3535)---login(3954)---zsh(4043)---pstree(4326)
        |-polkitd(4033)---{polkitd}(4035)
        |-syslog-ng(3413)---syslog-ng(3414)
        `-udevd(643)-+-udevd(3194)
                     `-udevd(3218)

```

除了系统初始化，init还负责重启、关机、单用户恢复模式。为了支持上述操作，inittab把条目分到不同的**运行级别**(runlevel)中去。Arch使用以下运行级别：0——关机，1（又叫S）——单用户模式，3——普通的多用户模式，5——X使用，6——重启。其他发行版可能有所不同，但0、1、6级别是通用的。

运行时，init检查inittab并进行适当的操作。inittab中的启动项目格式如下：

```
id:runlevels:action:process

```

`id`是项目独一无二的标识符（但只是个名称，对init没任何作用）；`runlevels`是一串无分隔字符串，设置运行级别；当init进入了指定的`runlevels`，执行`action`；如果顺利，执行`process`。某些特殊的`action`会忽略`runlevels`，使用特殊的匹配方法。下一节有更详细的介绍。

## 调整运行级别

### 通过启动加载器

想要改变系统启动时的运行级别，只需要添加想要的运行级别 `n` 到启动加载器的内核参数。这通常的应用是 [Start X at login#/etc/inittab](/index.php/Start_X_at_login#.2Fetc.2Finittab "Start X at login")。要启动到需要的运行级别，将号码加入 [内核参数](/index.php/Kernel_parameters "Kernel parameters") (例如 `3` 则启动要运行级别 3)。

运行级别追加到最后，这样内核就知道用哪个运行级别启动。想要使用另一个 init 程序(如 [systemd](/index.php/Systemd "Systemd"))，添加`init=/usr/lib/systemd/systemd`或者类似的命令到内核行。

**注意:** 如果你使用 sysvinit 之外的 init 程序，运行级别参数可能被忽略。

### 启动之后

系统启动后，可以调用`telinit n`通知init切换到运行级别`n`。然后init读取inittab，并做出当前运行级别到新的运行级别需要的改变——杀死新级别中没有的进程，执行旧级别未执行过的操作。两个级别共有的进程此时都会保留不动。杀死进程的过程有些复杂，技术信息参见init的manpage。

init不会监视inittab的改动，需要执行`telinit`应用更改。`telinit q` 命令只应用inittab而不会修改运行级别。

## inittab

这一部分将探究inittab中的常见项目，之后会给出几个inittab项目的实例。叙述顺序按照Arch默认的inittab。

**警告:** 重启之前，务必使用 `telinit q` 测试修改过的 `/etc/inittab`，任何小小的语法错误都将导致系统无法启动。

### 默认运行级别

默认运行级别为3。如果想要设置默认运行级别为5（通常X使用的级别），添加下面一行内容：

```
id:5:initdefault:

```

### 主启动脚本

下面几行描述了主启动脚本：

```
rc::sysinit:/etc/rc.sysinit
rs:S1:wait:/etc/rc.single
rm:2345:wait:/etc/rc.multi
rh:06:wait:/etc/rc.shutdown

```

### 单用户启动

有时，因为重要文件丢失、文件系统损坏或硬件问题，内核可能启动失败。此时init可能自动进入**单用户模式**，此模式只允许使用root登陆，使用/sbin/sulogin（而非/sbin/login）控制login进程。也可以在 [GRUB](/index.php/GRUB "GRUB"), [LILO](/index.php/LILO "LILO") 或 [syslinux](/index.php/Syslinux "Syslinux") 启动项添加S参数进入单用户模式。如果不想使用sulogin，可以在这里设置：

```
su:S:wait:/sbin/sulogin -p

```

### 终端初始化

该部分是初始化虚拟终端的关键。默认设置会在tty1-6开启6个[getty](/index.php/Getty "Getty")，显示终端登陆提示。另见：openvt， chvt，stty，ioctl。

```
c1:234:respawn:/sbin/agetty 9600 tty1 xterm-color
c5:5:respawn:/sbin/agetty 57600 tty2 xterm-256color

```

### Ctrl-Alt-Del

以下内容定义按下`Ctrl+Alt+Del`组合键时进行的操作：

```
ca::ctrlaltdel:/sbin/shutdown -t3 -r now

```

### X 程序

如果不怕麻烦，在inittab中启动各种程序都是可以的。以下内容示范了如何设置系统进入运行级别5时启动登陆管理器 [SLiM](/index.php/SLiM "SLiM") ：

```
x:5:respawn:/usr/bin/slim >/dev/null 2>&1
#x:5:respawn:/usr/bin/xdm -nodaemon -confi /etc/X11/xdm/archlinux/xdm-config

```

### 电源检测脚本

init可以根据UPS设备状态执行相应进程，示例如下：

```
pf::powerfail:/sbin/shutdown -f -h +2 "Power Failure; System Shutting Down"
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

```

### 自定义键盘请求

类似`Ctrl+Alt+Del`，下面的内容添加了按下特定组合键时执行命令的功能：

```
kb::kbrequest:/usr/bin/wall "Keyboard Request -- edit /etc/inittab to customize"

```

#### 触发 kbrequest

使用root用户，可以通过向init发送WINCH信号触发**kbrequest**。对于上述例子，命令：

```
kill -WINCH 1

```

会导致`wall`命令执行，向所有用户发送信息：

```
Broadcast message from root@askapachehost (console) (Wed Oct 27 14:02:26 2010):  
Keyboard Request -- edit /etc/inittab to customize

```

## 另见

*   [Automatic login to virtual console](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console")
*   [Disable clearing of boot messages](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages")
*   [开机启动 X](/index.php/Start_X_at_Login_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Start X at Login (简体中文)")
*   [Xinitrc (简体中文)](/index.php/Xinitrc_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xinitrc (简体中文)")
*   [登陆管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")
*   [SLiM (简体中文)](/index.php/SLiM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SLiM (简体中文)")

## 外部链接

*   [维基百科：init](http://zh.wikipedia.org/wiki/Init)
*   [Linux Knowledge Base and Tutorial：运行级别](http://www.linux-tutorial.info/modules.php?name=MContent&pageid=65)
*   [Linux.com：runlevels 和 inittab 的介绍](http://www.linux.com/articles/114107)
*   [Linux.com：服务、运行级别、rc.d脚本的介绍](http://www.linux.com/news/enterprise/systems-management/8116-an-introduction-to-services-runlevels-and-rcd-scripts)