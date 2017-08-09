**翻译状态：** 本文是英文页面 [Systemd](/index.php/Systemd "Systemd") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-09-01，点击[这里](https://wiki.archlinux.org/index.php?title=Systemd&diff=0&oldid=448461)可以查看翻译后英文页面的改动。

摘自[项目主页](http://freedesktop.org/wiki/Software/systemd)：

***systemd** 是 Linux 下的一款系统和服务管理器，兼容 SysV 和 LSB 的启动脚本。systemd 的特性有：支持并行化任务；同时采用 socket 式与 [D-Bus](/index.php/D-Bus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "D-Bus (简体中文)") 总线式激活服务；按需启动守护进程（daemon）；利用 Linux 的 [cgroups](/index.php/Cgroups "Cgroups") 监视进程；支持快照和系统恢复；维护挂载点和自动挂载点；各服务间基于依赖关系进行精密控制。*

**注意:** [Arch Linux 论坛的这篇帖子](https://bbs.archlinux.org/viewtopic.php?pid=1149530#p1149530) 详细地解释了 Arch Linux 迁移到 systemd 的原因。

## Contents

*   [1 systemd 基本工具](#systemd_.E5.9F.BA.E6.9C.AC.E5.B7.A5.E5.85.B7)
    *   [1.1 分析系统状态](#.E5.88.86.E6.9E.90.E7.B3.BB.E7.BB.9F.E7.8A.B6.E6.80.81)
    *   [1.2 使用单元](#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83)
    *   [1.3 电源管理](#.E7.94.B5.E6.BA.90.E7.AE.A1.E7.90.86)
*   [2 编写单元文件](#.E7.BC.96.E5.86.99.E5.8D.95.E5.85.83.E6.96.87.E4.BB.B6)
    *   [2.1 处理依赖关系](#.E5.A4.84.E7.90.86.E4.BE.9D.E8.B5.96.E5.85.B3.E7.B3.BB)
    *   [2.2 服务类型](#.E6.9C.8D.E5.8A.A1.E7.B1.BB.E5.9E.8B)
    *   [2.3 修改现存单元文件](#.E4.BF.AE.E6.94.B9.E7.8E.B0.E5.AD.98.E5.8D.95.E5.85.83.E6.96.87.E4.BB.B6)
*   [3 目标（target）](#.E7.9B.AE.E6.A0.87.EF.BC.88target.EF.BC.89)
    *   [3.1 获取当前目标](#.E8.8E.B7.E5.8F.96.E5.BD.93.E5.89.8D.E7.9B.AE.E6.A0.87)
    *   [3.2 创建新目标](#.E5.88.9B.E5.BB.BA.E6.96.B0.E7.9B.AE.E6.A0.87)
    *   [3.3 目标表](#.E7.9B.AE.E6.A0.87.E8.A1.A8)
    *   [3.4 切换运行级别/目标](#.E5.88.87.E6.8D.A2.E8.BF.90.E8.A1.8C.E7.BA.A7.E5.88.AB.2F.E7.9B.AE.E6.A0.87)
    *   [3.5 修改默认运行级别/目标](#.E4.BF.AE.E6.94.B9.E9.BB.98.E8.AE.A4.E8.BF.90.E8.A1.8C.E7.BA.A7.E5.88.AB.2F.E7.9B.AE.E6.A0.87)
*   [4 临时文件](#.E4.B8.B4.E6.97.B6.E6.96.87.E4.BB.B6)
*   [5 定时器](#.E5.AE.9A.E6.97.B6.E5.99.A8)
*   [6 挂载](#.E6.8C.82.E8.BD.BD)
*   [7 日志](#.E6.97.A5.E5.BF.97)
    *   [7.1 Facility](#Facility)
    *   [7.2 Priority level](#Priority_level)
    *   [7.3 过滤输出](#.E8.BF.87.E6.BB.A4.E8.BE.93.E5.87.BA)
    *   [7.4 日志大小限制](#.E6.97.A5.E5.BF.97.E5.A4.A7.E5.B0.8F.E9.99.90.E5.88.B6)
    *   [7.5 配合 syslog 使用](#.E9.85.8D.E5.90.88_syslog_.E4.BD.BF.E7.94.A8)
    *   [7.6 手动清理日志](#.E6.89.8B.E5.8A.A8.E6.B8.85.E7.90.86.E6.97.A5.E5.BF.97)
    *   [7.7 Journald in conjunction with syslog](#Journald_in_conjunction_with_syslog)
    *   [7.8 转发 journald 到 /dev/tty12](#.E8.BD.AC.E5.8F.91_journald_.E5.88.B0_.2Fdev.2Ftty12)
    *   [7.9 查看特定位置的日志](#.E6.9F.A5.E7.9C.8B.E7.89.B9.E5.AE.9A.E4.BD.8D.E7.BD.AE.E7.9A.84.E6.97.A5.E5.BF.97)
*   [8 Tips and tricks](#Tips_and_tricks)
    *   [8.1 Enable installed units by default](#Enable_installed_units_by_default)
*   [9 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [9.1 寻找错误](#.E5.AF.BB.E6.89.BE.E9.94.99.E8.AF.AF)
    *   [9.2 诊断启动问题](#.E8.AF.8A.E6.96.AD.E5.90.AF.E5.8A.A8.E9.97.AE.E9.A2.98)
    *   [9.3 诊断一个特定服务](#.E8.AF.8A.E6.96.AD.E4.B8.80.E4.B8.AA.E7.89.B9.E5.AE.9A.E6.9C.8D.E5.8A.A1)
    *   [9.4 关机/重启十分缓慢](#.E5.85.B3.E6.9C.BA.2F.E9.87.8D.E5.90.AF.E5.8D.81.E5.88.86.E7.BC.93.E6.85.A2)
    *   [9.5 短时进程无日志记录](#.E7.9F.AD.E6.97.B6.E8.BF.9B.E7.A8.8B.E6.97.A0.E6.97.A5.E5.BF.97.E8.AE.B0.E5.BD.95)
    *   [9.6 禁止在程序崩溃时转储内存](#.E7.A6.81.E6.AD.A2.E5.9C.A8.E7.A8.8B.E5.BA.8F.E5.B4.A9.E6.BA.83.E6.97.B6.E8.BD.AC.E5.82.A8.E5.86.85.E5.AD.98)
    *   [9.7 启动的时间太长](#.E5.90.AF.E5.8A.A8.E7.9A.84.E6.97.B6.E9.97.B4.E5.A4.AA.E9.95.BF)
    *   [9.8 systemd-tmpfiles-setup.service 在启动时启动失败](#systemd-tmpfiles-setup.service_.E5.9C.A8.E5.90.AF.E5.8A.A8.E6.97.B6.E5.90.AF.E5.8A.A8.E5.A4.B1.E8.B4.A5)
    *   [9.9 不能设定在开机时启动软链接到 /etc/systemd/system 的服务](#.E4.B8.8D.E8.83.BD.E8.AE.BE.E5.AE.9A.E5.9C.A8.E5.BC.80.E6.9C.BA.E6.97.B6.E5.90.AF.E5.8A.A8.E8.BD.AF.E9.93.BE.E6.8E.A5.E5.88.B0_.2Fetc.2Fsystemd.2Fsystem_.E7.9A.84.E6.9C.8D.E5.8A.A1)
    *   [9.10 启动时显示的 systemd 版本和安装版本不一致](#.E5.90.AF.E5.8A.A8.E6.97.B6.E6.98.BE.E7.A4.BA.E7.9A.84_systemd_.E7.89.88.E6.9C.AC.E5.92.8C.E5.AE.89.E8.A3.85.E7.89.88.E6.9C.AC.E4.B8.8D.E4.B8.80.E8.87.B4)
*   [10 相关资源](#.E7.9B.B8.E5.85.B3.E8.B5.84.E6.BA.90)

## systemd 基本工具

监视和控制systemd的主要命令是`systemctl`。该命令可用于查看系统状态和管理系统及服务。详见`man 1 systemctl`。

**提示：**

*   在 `systemctl` 参数中添加 `-H <用户名>@<主机名>` 可以实现对其他机器的远程控制。该功能使用 [SSH](/index.php/SSH_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SSH (简体中文)") 连接。
*   `systemadm` 是 systemd 的官方图形前端。[官方软件仓库](/index.php/Official_repositories "Official repositories")提供了稳定版本 [systemd-ui](https://www.archlinux.org/packages/?name=systemd-ui) 。
*   [Plasma](/index.php/Plasma "Plasma") 用户可以安装 *systemctl* 图形前端 [systemd-kcm](https://www.archlinux.org/packages/?name=systemd-kcm)。安装后可以在 *System administration* 下找到。

### 分析系统状态

显示 **系统状态**：

```
$ systemctl status

```

输出激活的单元：

```
$ systemctl

```

以下命令等效：

```
$ systemctl list-units

```

输出运行失败的单元：

```
$ systemctl --failed

```

所有可用的单元文件存放在 `/usr/lib/systemd/system/` 和 `/etc/systemd/system/` 目录（后者优先级更高）。查看所有已安装服务：

```
$ systemctl list-unit-files

```

### 使用单元

一个单元配置文件可以描述如下内容之一：系统服务（`.service`）、挂载点（`.mount`）、sockets（`.sockets`） 、系统设备（`.device`）、交换分区（`.swap`）、文件路径（`.path`）、启动目标（`.target`）、由 systemd 管理的计时器（`.timer`）。详情参阅 `man 5 systemd.unit` 。

使用 `systemctl` 控制单元时，通常需要使用单元文件的全名，包括扩展名（例如 `sshd.service` ）。但是有些单元可以在 `systemctl` 中使用简写方式。

*   如果无扩展名，systemctl 默认把扩展名当作 `.service` 。例如 `netcfg` 和 `netcfg.service` 是等价的。
*   挂载点会自动转化为相应的 `.mount` 单元。例如 `/home` 等价于 `home.mount` 。
*   设备会自动转化为相应的 `.device` 单元，所以 `/dev/sda2` 等价于 `dev-sda2.device` 。

**注意:** 有一些单元的名称包含一个 `@` 标记（例如： `name@*string*.service` ），这意味着它是模板单元 `name@.service` 的一个 [实例](http://0pointer.de/blog/projects/instances.html)。 `*string*` 被称作实例标识符，在 *systemctl* 调用模板单元时，会将其当作一个参数传给模板单元，模板单元会使用这个传入的参数代替模板中的 `%I` 指示符。

在实例化之前，*systemd* 会先检查 `name@string.suffix` 文件是否存在（如果存在，就直接使用这个文件，而不是模板实例化）。大多数情况下，包含 `@` 标记都意味着这个文件是模板。如果一个模板单元没有实例化就调用，该调用会返回失败，因为模板单元中的 `%I` 指示符没有被替换。

**提示：**

*   下面的大部分命令都可以跟多个单元名, 详细信息参见 `man systemctl`。
*   `systemctl`命令在`enable`、`disable`和`mask`子命令中增加了`--now`选项，可以实现激活的同时启动服务，取消激活的同时停止服务。
*   一个软件包可能会提供多个不同的单元。如果你已经安装了软件包，可以通过`pacman -Qql *package* | grep systemd`命令检查这个软件包提供了哪些单元。

立即激活单元：

```
# systemctl start <单元>

```

立即停止单元：

```
# systemctl stop <单元>

```

重启单元：

```
# systemctl restart <单元>

```

重新加载配置：

```
# systemctl reload <单元>

```

输出单元运行状态：

```
$ systemctl status <单元>

```

检查单元是否配置为自动启动：

```
$ systemctl is-enabled <单元>

```

开机自动激活单元：

```
# systemctl enable <单元>

```

取消开机自动激活单元：

```
# systemctl disable <单元>

```

禁用一个单元（禁用后，间接启动也是不可能的）：

```
# systemctl mask <单元>

```

取消禁用一个单元：

```
# systemctl unmask <单元>

```

显示单元的手册页（必须由单元文件提供）：

```
# systemctl help <单元>

```

重新载入 systemd，扫描新的或有变动的单元：

```
# systemctl daemon-reload

```

### 电源管理

安装 [polkit](/index.php/Polkit "Polkit") 后才能以普通用户身份使用电源管理。

如果你正登录在一个本地的 `systemd-logind` 用户会话，且当前没有其它活动的会话，那么以下命令无需 root 权限即可执行。否则（例如，当前有另一个用户登录在某个 tty ）， systemd 将会自动请求输入root密码。

重启：

```
$ systemctl reboot

```

退出系统并关闭电源：

```
$ systemctl poweroff

```

待机：

```
$ systemctl suspend

```

休眠：

```
$ systemctl hibernate

```

混合休眠模式（同时休眠到硬盘并待机）：

```
$ systemctl hybrid-sleep

```

## 编写单元文件

`systemd` [单元文件](http://www.freedesktop.org/software/systemd/man/systemd.unit.html)的语法来源于 XDG 桌面项配置文件`.desktop`文件，最初的源头则是Microsoft Windows的`.ini`文件。单元文件可以从两个地方加载，优先级从低到高分别是：

*   `/usr/lib/systemd/system/` ：软件包安装的单元
*   `/etc/systemd/system/` ：系统管理员安装的单元

*   当 `systemd` 运行在[用户模式](/index.php/Systemd/User#How_it_works "Systemd/User")下时，使用的加载路径是完全不同的。
*   systemd 单元名仅能包含 ASCII 字符，下划线和点号。其它字符需要用 C-style "\x2d" 替换。参阅 `man systemd.unit` 和 `man systemd-escape` 。}}

单元文件的语法，可以参考系统已经安装的单元，也可以参考 `man systemd.service` 中的[EXAMPLES章节](http://www.freedesktop.org/software/systemd/man/systemd.service.html#Examples)。

**提示：** 以 `#` 开头的注释可能也能用在 unit-files 中，但是只能在新行中使用。不要在 *systemd* 的参数后面使用行末注释， 否则 unit 将会启动失败。

### 处理依赖关系

使用 systemd 时，可通过正确编写单元配置文件来解决其依赖关系。典型的情况是，单元 `A` 要求单元 `B` 在 `A` 启动之前运行。在此情况下，向单元 `A` 配置文件中的 `[Unit]` 段添加 `Requires=B` 和 `After=B` 即可。若此依赖关系是可选的，可添加 `Wants=B` 和 `After=B` 。请注意 `Wants=` 和 `Requires=` 并不意味着 `After=` ，即如果 `After=` 选项没有制定，这两个单元将被并行启动。

依赖关系通常被用在服务（service）而不是[目标（target）](#.E7.9B.AE.E6.A0.87.EF.BC.88target.EF.BC.89)上。例如， `network.target` 一般会被某个配置网络接口的服务引入，所以，将自定义的单元排在该服务之后即可，因为 `network.target` 已经启动。

### 服务类型

编写自定义的 service 文件时，可以选择几种不同的服务启动方式。启动方式可通过配置文件 `[Service]` 段中的 `Type=` 参数进行设置。

*   `Type=simple` ：（默认值） systemd认为该服务将立即启动。服务进程不会 fork 。如果该服务要启动其他服务，不要使用此类型启动，除非该服务是socket 激活型。
*   `Type=forking` ：systemd认为当该服务进程fork，且父进程退出后服务启动成功。对于常规的守护进程（daemon），除非你确定此启动方式无法满足需求，使用此类型启动即可。使用此启动类型应同时指定 `PIDFile=`，以便 systemd 能够跟踪服务的主进程。
*   `Type=oneshot` ：这一选项适用于只执行一项任务、随后立即退出的服务。可能需要同时设置 `RemainAfterExit=yes` 使得 systemd 在服务进程退出之后仍然认为服务处于激活状态。
*   `Type=notify` ：与 `Type=simple` 相同，但约定服务会在就绪后向 systemd 发送一个信号。这一通知的实现由 `libsystemd-daemon.so` 提供。
*   `Type=dbus` ：若以此方式启动，当指定的 `BusName` 出现在DBus系统总线上时，systemd认为服务就绪。
*   `Type=idle` ：`systemd`会等待所有任务处理完成后，才开始执行 `idle` 类型的单元。其他行为与 `Type=simple` 类似。

`type` 的更多解释可以参考 [systemd.service(5)](http://www.freedesktop.org/software/systemd/man/systemd.service.html#Type=)。

### 修改现存单元文件

为了避免和 pacman 冲突，不应该直接编辑软件包提供的文件。要更改由软件包提供的单元文件，先创建名为 `/etc/systemd/system/<单元名>.d/` 的目录（如 `/etc/systemd/system/httpd.service.d/`） ，然后放入 `*.conf` 文件，其中可以添加或重置参数。这里设置的参数优先级高于原来的单元文件。例如，如果想添加一个额外的依赖，创建如下文件即可：

 `/etc/systemd/system/<unit>.d/customdependency.conf` 
```
[Unit]
Requires=<新依赖>
After=<新依赖>
```

As another example, in order to replace the `ExecStart` directive for a unit that is not of type `oneshot`, create the following file:

 `/etc/systemd/system/*unit*.d/customexec.conf` 
```
[Service]
ExecStart=
ExecStart=*new command*
```

修改 `ExecStart` 前必须将其置空，参见 ([[1]](https://bugzilla.redhat.com/show_bug.cgi?id=756787#c9) 。所有可能多次赋值的变量都需要这个操作，例如定时器的 `OnCalendar` 。

下面是自动重启服务的一个例子：

 `/etc/systemd/system/*unit*.d/restart.conf` 
```
[Service]
Restart=always
RestartSec=30
```

然后运行以下命令使更改生效：

```
# systemctl daemon-reload
# systemctl restart <单元>

```

此外，把旧的单元文件从 `/usr/lib/systemd/system/` 复制到 `/etc/systemd/system/`，然后进行修改，也可以达到同样效果。在 `/etc/systemd/system/` 目录中的单元文件的优先级总是高于 `/usr/lib/systemd/system/` 目录中的同名单元文件。注意，当 `/usr/lib/` 中的单元文件因软件包升级变更时，`/etc/` 中自定义的单元文件不会同步更新。此外，你还得执行 `systemctl reenable <unit>`，手动重新启用该单元。因此，建议使用前面一种利用 `*.conf` 的方法。

**提示：** `systemd-delta` 命令用来查看哪些单元文件被覆盖、哪些被修改。系统维护的时候需要及时了解哪些单元已经有了更新。

安装 [vim-systemd](https://www.archlinux.org/packages/?name=vim-systemd) 软件包，可以使单元配置文件在 [Vim](/index.php/Vim "Vim") 下支持语法高亮。

## 目标（target）

运行级别（runlevel）是一个旧的概念。现在，systemd 引入了一个和运行级别功能相似又不同的概念——目标（target）。不像数字表示的启动级别，每个*目标*都有名字和独特的功能，并且能同时启用多个。一些*目标*继承其他*目标*的服务，并启动新服务。systemd 提供了一些模仿 sysvinit 运行级别的*目标*，仍可以使用旧的 `telinit 运行级别` 命令切换。

### 获取当前目标

不要使用 `runlevel` 命令了：

```
$ systemctl list-units --type=target

```

### 创建新目标

在 Fedora 中，运行级别 0、1、3、5、6 都被赋予特定用途，并且都对应一个 systemd 的*目标*。然而，移植用户定义的运行级别（2、4）没有什么好方法。要实现类似功能，可以以原有的启动级别为基础，创建一个新的*目标* `/etc/systemd/system/<新目标>`（可以参考 `/usr/lib/systemd/system/graphical.target`），创建 `/etc/systemd/system/<新目标>.wants` 目录，向其中加入额外服务的链接（指向 `/usr/lib/systemd/system/` 中的单元文件）。

### 目标表

| SysV 运行级别 | Systemd 目标 | 注释 |
| 0 | runlevel0.target, poweroff.target | 中断系统（halt） |
| 1, s, single | runlevel1.target, rescue.target | 单用户模式 |
| 2, 4 | runlevel2.target, runlevel4.target, multi-user.target | 用户自定义运行级别，通常识别为级别3。 |
| 3 | runlevel3.target, multi-user.target | 多用户，无图形界面。用户可以通过终端或网络登录。 |
| 5 | runlevel5.target, graphical.target | 多用户，图形界面。继承级别3的服务，并启动图形界面服务。 |
| 6 | runlevel6.target, reboot.target | 重启 |
| emergency | emergency.target | 急救模式（Emergency shell） |

### 切换运行级别/目标

systemd 中，运行级别通过“目标单元”访问。通过如下命令切换：

```
# systemctl isolate graphical.target

```

该命令对下次启动无影响。等价于`telinit 3` 或 `telinit 5`。

### 修改默认运行级别/目标

开机启动的目标是 `default.target`，默认链接到 `graphical.target` （大致相当于原来的运行级别5）。可以通过[内核参数](/index.php/Kernel_parameters_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel parameters (简体中文)")更改默认运行级别：

*   `systemd.unit=multi-user.target` （大致相当于级别3）
*   `systemd.unit=rescue.target` （大致相当于级别1）

另一个方法是修改 `default.target`。可以通过 `systemctl` 修改它：

```
# systemctl set-default multi-user.target

```

要覆盖已经设置的*default.target*，请使用 force:

```
# systemctl set-default -f multi-user.target

```

可以在 `systemctl` 的输出中看到命令执行的效果：链接 `/etc/systemd/system/default.target` 被创建，指向新的默认运行级别。

## 临时文件

`/usr/lib/tmpfiles.d/` 和 `/etc/tmpfiles.d/` 中的文件描述了 systemd-tmpfiles 如何创建、清理、删除临时文件和目录，这些文件和目录通常存放在 `/run` 和 `/tmp` 中。配置文件名称为 `/etc/tmpfiles.d/<program>.conf`。此处的配置能覆盖 `/usr/lib/tmpfiles.d/` 目录中的同名配置。

临时文件通常和服务文件同时提供，以生成守护进程需要的文件和目录。例如 [Samba](/index.php/Samba_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Samba (简体中文)") 服务需要目录 `/run/samba` 存在并设置正确的权限位，就象这样：

 `/usr/lib/tmpfiles.d/samba.conf` 
```
D /run/samba 0755 root root

```

此外，临时文件还可以用来在开机时向特定文件写入某些内容。比如，要禁止系统从USB设备唤醒，利用旧的 `/etc/rc.local` 可以用 `echo USBE > /proc/acpi/wakeup`，而现在可以这么做：

 `/etc/tmpfiles.d/disable-usb-wake.conf` 
```
w /proc/acpi/wakeup - - - - USBE

```

详情参见`systemd-tmpfiles(8)` 和 `man 5 tmpfiles.d`。

**注意:** 该方法不能向 `/sys` 中的配置文件添加参数，因为 `systemd-tmpfiles-setup` 有可能在相关模块加载前运行。这种情况下，需要首先通过 `modinfo <模块名>` 确认需要的参数，然后在 [`/etc/modprobe.d` 目录下的配置文件](/index.php/Kernel_modules_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E9.80.89.E9.A1.B9 "Kernel modules (简体中文)")中修改配置参数。另外，还可以使用 [udev 规则](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#udev_.E8.A7.84.E5.88.99 "Udev (简体中文)")，在设备就绪时设置相应属性。

## 定时器

一个定时器是一个以 `.timer` 为结尾的单元配置文件并包含由 `systemd` 控制和监督的信息。[systemd/Timers (简体中文)](/index.php/Systemd/Timers_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd/Timers (简体中文)")

**注意:** 定时器很大程度上可取代 `cron`。[systemd/Timers (简体中文)#替代 cron](/index.php/Systemd/Timers_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E6.9B.BF.E4.BB.A3_cron "Systemd/Timers (简体中文)")

## 挂载

因为 systemd 替代了 System V init, 所以也负责按 `/etc/fstab` 定义挂载目录。除此之外，还实现了以 `x-systemd.` 开头的挂载选项. [Fstab#Automount with systemd](/index.php/Fstab#Automount_with_systemd "Fstab") 包含了使用此扩展的 *automounting* (按需挂载)。完整扩展请参考 [[2]](https://www.freedesktop.org/software/systemd/man/systemd.mount.html#fstab)。

## 日志

systemd 提供了自己的日志系统（logging system），称为 journal。使用 systemd 日志，无需额外安装日志服务（syslog）。读取日志的命令：

```
# journalctl

```

默认情况下（当 `Storage=` 在文件 `/etc/systemd/journald.conf` 中被设置为 `auto`），日志记录将被写入 `/var/log/journal/`。该目录是 [systemd](https://www.archlinux.org/packages/?name=systemd) 软件包的一部分。若被删除，systemd **不会**自动创建它，直到下次升级软件包时重建该目录。如果该目录缺失，systemd 会将日志记录写入 `/run/systemd/journal`。这意味着，系统重启后日志将丢失。

**提示：** 如果 `/var/log/journal/` 位于 [btrfs](/index.php/Btrfs "Btrfs") 文件系统，应该考虑对这个目录禁用写入时复制，方法参阅[Btrfs#Copy-on-Write (CoW)](/index.php/Btrfs#Copy-on-Write_.28CoW.29 "Btrfs")。

Systemd 日志事件提示信息的记录分级方式符合经典的 BSD syslog 协议风格（[维基百科](https://en.wikipedia.org/wiki/Syslog "wikipedia:Syslog")，[RFC 5424](https://tools.ietf.org/html/rfc5424)）。详情请参阅 [Facility](#Facility)、[Priority level](#Priority_level)等章节，用例请参阅 [Filtering output](#Filtering_output)。

### Facility

A syslog facility code is used to specify the type of program that is logging the message [RFC 5424 Section 6.2.1](https://tools.ietf.org/html/rfc5424#section-6.2.1).

| Facility code | Keyword | Description | Info |
| 0 | kern | kernel messages |
| 1 | user | user-level messages |
| 2 | mail | mail system | Archaic POSIX still supported and sometimes used system, for more `man mail`) |
| 3 | daemon | system daemons | All deamons, including systemd and its subsystems |
| 4 | auth | security/authorization messages | Also watch for different facility 10 |
| 5 | syslog | messages generated internally by syslogd | As it standartized for syslogd, not used by systemd (see facility 3) |
| 6 | lpr | line printer subsystem (archaic subsystem) |
| 7 | news | network news subsystem (archaic subsystem) |
| 8 | uucp | UUCP subsystem (archaic subsystem) |
| 9 | clock daemon | systemd-timesyncd |
| 10 | authpriv | security/authorization messages | Also watch for different facility 4 |
| 11 | ftp | FTP daemon |
| 12 | - | NTP subsystem |
| 13 | - | log audit |
| 14 | - | log alert |
| 15 | cron | scheduling daemon |
| 16 | local0 | local use 0 (local0) |
| 17 | local1 | local use 1 (local1) |
| 18 | local2 | local use 2 (local2) |
| 19 | local3 | local use 3 (local3) |
| 20 | local4 | local use 4 (local4) |
| 21 | local5 | local use 5 (local5) |
| 22 | local6 | local use 6 (local6) |
| 23 | local7 | local use 7 (local7) |

So, useful facilities to watch: 0,1,3,4,9,10,15.

### Priority level

A syslog severity code (in systemd called priority) is used to mark the importance of a message [RFC 5424 Section 6.2.1](https://tools.ietf.org/html/rfc5424#section-6.2.1).

| Value | Severity | Keyword | Description | Examples |
| 0 | Emergency | emerg | System is unusable | Severe Kernel BUG, systemd dumped core.
This level should not be used by applications. |
| 1 | Alert | alert | Should be corrected immediately | Vital subsystem goes out of work. Data loss.
`kernel: BUG: unable to handle kernel paging request at ffffc90403238ffc`. |
| 2 | Critical | crit | Critical conditions | Crashes, coredumps. Like familiar flash:
`systemd-coredump[25319]: Process 25310 (plugin-containe) of user 1000 dumped core`
Failure in the system primary application, like X11. |
| 3 | Error | err | Error conditions | Not severe error reported:
`kernel: usb 1-3: 3:1: cannot get freq at ep 0x84`,
`systemd[1]: Failed unmounting /var.`,
`libvirtd[1720]: internal error: Failed to initialize a valid firewall backend`). |
| 4 | Warning | warning | May indicate that an error will occur if action is not taken. | A non-root file system has only 1GB free.
`org.freedesktop. Notifications[1860]: (process:5999): Gtk-WARNING **: Locale not supported by C library. Using the fallback 'C' locale`. |
| 5 | Notice | notice | Events that are unusual, but not error conditions. | `systemd[1]: var.mount: Directory /var to mount over is not empty, mounting anyway`. `gcr-prompter[4997]: Gtk: GtkDialog mapped without a transient parent. This is discouraged`. |
| 6 | Informational | info | Normal operational messages that require no action. | `lvm[585]: 7 logical volume(s) in volume group "archvg" now active`. |
| 7 | Debug | debug | Information useful to developers for debugging the application. | `kdeinit5[1900]: powerdevil: Scheduling inhibition from ":1.14" "firefox" with cookie 13 and reason "screen"`. |

If issue you are looking for, was not found on according level, search it on couple of priority levels above and below. This rules are recommendations. Some errors considered a normal occasion for program so they marked low in priority by developer, and on the contrary, sometimes too many messages plaques too high priorities for them, but often it's an arguable situation. And often you really should solve an issue, also to understand architecture and adopt best practices.

Examples:

*   Info message: `pulseaudio[2047]: W: [pulseaudio] alsa-mixer.c: Volume element Master has 8 channels. That's too much! I can't handle that!` It is an warning or error by definition.
*   Plaguing alert message: `sudo[21711]:     user : a password is required ; TTY=pts/0 ; PWD=/home/user ; USER=root ; COMMAND=list /usr/bin/pacman --color auto -Sy` The [reason](https://bbs.archlinux.org/viewtopic.php?id=184455) - user was manually added to sudoers file, not to wheel group, which is arguably normal action, but sudo produced an alert on every occasion.

### 过滤输出

`journalctl`可以根据特定字段过滤输出。如果过滤的字段比较多，需要较长时间才能显示出来。

示例：

显示本次启动后的所有日志：

```
# journalctl -b

```

不过，一般大家更关心的不是本次启动后的日志，而是上次启动时的（例如，刚刚系统崩溃了）。可以使用 `-b` 参数：

*   `journalctl -b -0` 显示本次启动的信息
*   `journalctl -b -1` 显示上次启动的信息
*   `journalctl -b -2` 显示上上次启动的信息 `journalctl -b -2`
*   只显示错误、冲突和重要告警信息 `# journalctl -p err..alert` 也可以使用数字， `journalctl -p 3..1`。If single number/keyword used, `journalctl -p 3` - all higher priority levels also included.

*   显示从某个日期 ( 或时间 ) 开始的消息: `# journalctl --since="2012-10-30 18:17:16"` 
*   显示从某个时间 ( 例如 20分钟前 ) 的消息: `# journalctl --since "20 min ago"` 
*   显示最新信息 `# journalctl -f` 
*   显示特定程序的所有消息: `# journalctl /usr/lib/systemd/systemd` 
*   显示特定进程的所有消息: `# journalctl _PID=1` 
*   显示指定单元的所有消息： `# journalctl -u netcfg` 
*   显示内核环缓存消息r: `# journalctl -k` 
*   Show auth.log equivalent by filtering on syslog facility: `# journalctl -f -l SYSLOG_FACILITY=10` 

详情参阅`man journalctl`、`man systemd.journal-fields`，以及 Lennert 的这篇[博文](http://0pointer.de/blog/projects/journalctl.html)。

### 日志大小限制

如果按上面的操作保留日志的话，默认日志最大限制为所在文件系统容量的 10%，即：如果 `/var/log/journal` 储存在 50GiB 的根分区中，那么日志最多存储 5GiB 数据。可以修改配置文件指定最大限制。如限制日志最大 50MiB：

 `/etc/systemd/journald.conf`  `SystemMaxUse=50M` 

还可以通过配置片段而不是全局配置文件进行设置：

 `/etc/systemd/journald.conf.d/00-journal-size.conf` 
```
[Journal]
SystemMaxUse=50M
```

详情参见 `man journald.conf`.

### 配合 syslog 使用

systemd 提供了 socket `/run/systemd/journal/syslog`，以兼容传统日志服务。所有系统信息都会被传入。要使传统日志服务工作，需要让服务链接该 socket，而非 `/dev/log`（[官方说明](http://lwn.net/Articles/474968/)）。Arch 软件仓库中的 [syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng) 已经包含了需要的配置。

`journald.conf` 使用 `no` 转发socket . 为了使 *syslog-ng* 配合 *journald* , 你需要在 `/etc/systemd/journald.conf` 中设置 `ForwardToSyslog=yes` . 参阅 [Syslog-ng#Overview](/index.php/Syslog-ng#Overview "Syslog-ng") 了解更多细节.

如果你选择使用 [rsyslog](https://www.archlinux.org/packages/?name=rsyslog) , 因为 [rsyslog](/index.php/Rsyslog "Rsyslog") 从日志中 [直接](http://lists.freedesktop.org/archives/systemd-devel/2014-August/022295.html#journald) 传出消息,所以不再必要改变那个选项..

设置开机启动 syslog-ng：

```
 # systemctl enable syslog-ng

```

[这里](http://0pointer.de/blog/projects/)有一份很不错的 `journalctl` 指南。

### 手动清理日志

`/var/log/journal` 存放着日志, `rm` 应该能工作. 或者使用`journalctl`,

例如:

*   清理日志使总大小小于 100M: `# journalctl --vacuum-size=100M` 
*   清理最早两周前的日志. `# journalctl --vacuum-time=2weeks` 

参阅 `man journalctl` 获得更多信息.

### Journald in conjunction with syslog

Compatibility with a classic, non-journald aware [syslog](/index.php/Syslog-ng "Syslog-ng") implementation can be provided by letting *systemd* forward all messages via the socket `/run/systemd/journal/syslog`. To make the syslog daemon work with the journal, it has to bind to this socket instead of `/dev/log` ([official announcement](http://lwn.net/Articles/474968/)).

As of *systemd* 216 the default `journald.conf` for forwarding to the socket was changed to `ForwardToSyslog=no` to avoid system overhead, because [rsyslog](/index.php/Rsyslog "Rsyslog") or [syslog-ng](/index.php/Syslog-ng "Syslog-ng") (since 3.6) pull the messages from the journal by [itself](http://lists.freedesktop.org/archives/systemd-devel/2014-August/022295.html#journald).

See [Syslog-ng#Overview](/index.php/Syslog-ng#Overview "Syslog-ng") and [Syslog-ng#syslog-ng and systemd journal](/index.php/Syslog-ng#syslog-ng_and_systemd_journal "Syslog-ng"), or [rsyslog](/index.php/Rsyslog "Rsyslog") respectively, for details on configuration.

### 转发 journald 到 /dev/tty12

建立一个 [drop-in directory](#Editing_provided_units) `/etc/systemd/journald.conf.d` 然后在其中建立 `fw-tty12.conf` :

 `/etc/systemd/journald.conf.d/fw-tty12.conf` 
```
[Journal]
ForwardToConsole=yes
TTYPath=/dev/tty12
MaxLevelConsole=info
```

然后重新启动 systemd-journald.

### 查看特定位置的日志

有时你希望查看另一个系统上的日志.例如从 Live 环境修复现存的系统.

这种情况下你可以挂载目标系统 ( 例如挂载到 `/mnt` ),然后用 `-D`/`--directory` 参数指定目录,像这样:

```
$ journalctl -D */mnt*/var/log/journal -xe

```

## Tips and tricks

### Enable installed units by default

Arch Linux ships with `/usr/lib/systemd/system-preset/99-default.preset` containing `disable *`. This causes *systemctl preset* to disable all units by default, such that when a new package is installed, the user must manually enable the unit.

If this behavior is not desired, simply create a symlink from `/etc/systemd/system-preset/99-default.preset` to `/dev/null` in order to override the configuration file. This will cause *systemctl preset* to enable all units that get installed—regardless of unit type—unless specified in another file in one *systemctl preset'*s configuration directories. User units are not affected. See the manpage for `systemd.preset` for more information.

**Note:** Enabling all units by default may cause problems with packages that contain two or more mutually exclusive units. *systemctl preset* is designed to be used by distributions and spins or system administrators. In the case where two conflicting units would be enabled, you should explicitly specify which one is to be disabled in a preset configuration file as specified in the manpage for `systemd.preset`.

## 疑难解答

### 寻找错误

这个例子中的失败的服务是 `systemd-modules-load` :

**1.** 通过 *systemd* 寻找启动失败的服务:

 `$ systemctl --state=failed`  `systemd-modules-load.service   loaded **failed failed**  Load Kernel Modules` 

**2.** 我们发现了启动失败的 `systemd-modules-load` 服务. 我们想知道更多信息:

 `$ systemctl status systemd-modules-load` 
```
systemd-modules-load.service - Load Kernel Modules
   Loaded: loaded (/usr/lib/systemd/system/systemd-modules-load.service; static)
   Active: **failed** (Result: exit-code) since So 2013-08-25 11:48:13 CEST; 32s ago
     Docs: man:systemd-modules-load.service(8).
           man:modules-load.d(5)
  Process: **15630** ExecStart=/usr/lib/systemd/systemd-modules-load (**code=exited, status=1/FAILURE**)
```

如果没列出 `Process ID`, 通过 `systemctl` 重新启动失败的服务 ( 例如 `systemctl restart systemd-modules-load` )

**3.** 现在得到了 PID ,你就可以进一步探查错误的详细信息了.通过下列的命令收集日志,PID 参数是你刚刚得到的 `Process ID` (例如 15630):

 `$ journalctl -b _PID=15630` 
```
-- Logs begin at Sa 2013-05-25 10:31:12 CEST, end at So 2013-08-25 11:51:17 CEST. --
Aug 25 11:48:13 mypc systemd-modules-load[15630]: **Failed to find module 'blacklist usblp'**
Aug 25 11:48:13 mypc systemd-modules-load[15630]: **Failed to find module 'install usblp /bin/false'**
```

**4.** 我们发现有些内核模块的配置文件不正确,因此在 `/etc/modules-load.d/` 中检查一下:

 `$ ls -Al /etc/modules-load.d/` 
```
...
-rw-r--r--   1 root root    79  1\. Dez 2012  blacklist.conf
-rw-r--r--   1 root root     1  2\. Mär 14:30 encrypt.conf
-rw-r--r--   1 root root     3  5\. Dez 2012  printing.conf
-rw-r--r--   1 root root     6 14\. Jul 11:01 realtek.conf
-rw-r--r--   1 root root    65  2\. Jun 23:01 virtualbox.conf
...

```

**5.** 错误消息 `Failed to find module 'blacklist usblp'` 也许和 `blacklist.conf` 相关. 让我们注释掉第三步发现的错误的选项:

 `/etc/modules-load.d/blacklist.conf` 
```
**#** blacklist usblp
**#** install usblp /bin/false

```

**6.** 最后重新启动 `systemd-modules-load` 服务:

```
$ systemctl start systemd-modules-load

```

如果服务成功启动,不会有任何输出.如果你还是遇到了错误,回到步骤三,获得新的 PID 来跟踪日志并解决错误.

可以像这样确认服务成功启动:

 `$ systemctl status systemd-modules-load` 
```
systemd-modules-load.service - Load Kernel Modules
   Loaded: **loaded** (/usr/lib/systemd/system/systemd-modules-load.service; static)
   Active: **active (exited)** since So 2013-08-25 12:22:31 CEST; 34s ago
     Docs: man:systemd-modules-load.service(8)
           man:modules-load.d(5)
 Process: 19005 ExecStart=/usr/lib/systemd/systemd-modules-load (code=exited, status=0/SUCCESS)
Aug 25 12:22:31 mypc systemd[1]: **Started Load Kernel Modules**.
```

参阅 [#诊断启动问题](#.E8.AF.8A.E6.96.AD.E5.90.AF.E5.8A.A8.E9.97.AE.E9.A2.98) 一节获得更多探查错误的方法.

### 诊断启动问题

使用如下内核参数引导： `systemd.log_level=debug systemd.log_target=kmsg log_buf_len=1M`

更多有关调试的信息，参见[该文](http://freedesktop.org/wiki/Software/systemd/Debugging)。

### 诊断一个特定服务

如果某个 *systemd* 服务的工作状况不合你的预期因此你希望调试的话,设置 `SYSTEMD_LOG_LEVEL` [环境变量](/index.php/Environment_variable "Environment variable") 为 `debug` . 例如以调试模式运行 *systemd-networkd* 服务:

```
# systemctl stop systemd-networkd
# SYSTEMD_LOG_LEVEL=debug /lib/systemd/systemd-networkd

```

或者等价的,临时编辑系统单元文件,例如:

 `/lib/systemd/system/systemd-networkd.service` 
```
[Service]
...
Environment=SYSTEMD_LOG_LEVEL=debug
....
```

如果经常需要调试信息,以[一般方法](#.E4.BF.AE.E6.94.B9.E7.8E.B0.E5.AD.98.E5.8D.95.E5.85.83.E6.96.87.E4.BB.B6)添加环境变量.

### 关机/重启十分缓慢

如果关机特别慢（甚至跟死机了一样），很可能是某个拒不退出的服务在作怪。systemd 会等待一段时间，然后再尝试杀死它。请阅读[这篇文章](http://freedesktop.org/wiki/Software/systemd/Debugging#Shutdown_Completes_Eventually)，确认你是否是该问题受害者。

### 短时进程无日志记录

若 `journalctl -u foounit.service` 没有显示某个短时进程的任何输出，那么改用 PID 试试。例如，若 `systemd-modules-load.service` 执行失败，那么先用 `systemctl status systemd-modules-load` 查询其 PID（比如是123），然后检索该 PID 相关的日志 `journalctl -b _PID=123`。运行时进程的日志元数据（诸如 _SYSTEMD_UNIT 和 _COMM）被乱序收集在 `/proc` 目录。要修复该问题，必须修改内核，使其通过套接字连接来提供上述数据，该过程类似于 SCM_CREDENTIALS。

### 禁止在程序崩溃时转储内存

要使用老的内核转储，创建下面文件:

 `/etc/sysctl.d/49-coredump.conf` 
```
kernel.core_pattern = core
kernel.core_uses_pid = 0
```

然后运行：

```
# /usr/lib/systemd/systemd-sysctl

```

同样可能需要执行“unlimit”设置文件大小：

```
$ ulimit -c unlimited

```

更多信息请参阅 [sysctl.d](http://www.freedesktop.org/software/systemd/man/sysctl.d.html) 和 [/proc/sys/kernel 文档](https://www.kernel.org/doc/Documentation/sysctl/kernel.txt)。

### 启动的时间太长

不少用户用了 `systemd-analyze` 命令以后报告启动的时间比预计的要长,通常会说 `systemd-analyze` 分析结果表示 [NetworkManager](/index.php/NetworkManager "NetworkManager") 占据了太多的启动的时间.

有些用户的问题是 `/var/log/journal` 文件夹似乎过大.这也许也会对像`systemctl status` 或 `journalctl` 的命令有影响.一种解决方案是删除其中的文件 (但最好将它们备份到某处) 然后限制日志文件的大小.

### systemd-tmpfiles-setup.service 在启动时启动失败

从 systemd 219 开始, `/usr/lib/tmpfiles.d/systemd.conf` 指定 `/var/log/journal` 的 ACL 属性和目录, 因此日志所在的文件系统上要启用ACL.

参阅 [Access Control Lists#Enabling ACL](/index.php/Access_Control_Lists#Enabling_ACL "Access Control Lists") 获得如何包含 `/var/log/journal` 启动 ACL 的详细信息.

### 不能设定在开机时启动软链接到 /etc/systemd/system 的服务

如果 `/etc/systemd/system/*foo*.service` 是个符号链接, 运行 `systemctl enable *foo*.service` 时可能遇到这样的错误:

```
Failed to issue method call: No such file or directory

```

这是 systemd 的 [设计选择](https://bugzilla.redhat.com/show_bug.cgi?id=955379#c14) ,可以通过输入绝对路径来规避这个错误:

```
# systemctl enable */absolute/path/foo*.service

```

### 启动时显示的 systemd 版本和安装版本不一致

需要 [重新生成 initramfs](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio")。

**提示：** 可以使用 pacman 钩子在更新 [systemd](https://www.archlinux.org/packages/?name=systemd)时重新生成 initramfs。参考 [这个帖子](https://bbs.archlinux.org/viewtopic.php?id=215411) 和 [Pacman#Hooks](/index.php/Pacman#Hooks "Pacman").

## 相关资源

*   [官方网站](http://www.freedesktop.org/wiki/Software/systemd)
*   [维基百科上的介绍](https://en.wikipedia.org/wiki/zh:systemd "wikipedia:zh:systemd")
*   [man 手册页](http://0pointer.de/public/systemd-man/)
*   [systemd 优化](http://freedesktop.org/wiki/Software/systemd/Optimizations)
*   [常见问题 FAQ](http://www.freedesktop.org/wiki/Software/systemd/FrequentlyAskedQuestions)
*   [小技巧](http://www.freedesktop.org/wiki/Software/systemd/TipsAndTricks)
*   [systemd for Administrators (PDF)](http://0pointer.de/public/systemd-ebook-psankar.pdf)
*   [Fedora 项目对 systemd 的介绍](http://fedoraproject.org/wiki/Systemd)
*   [如何调试 systemd 故障](http://fedoraproject.org/wiki/How_to_debug_Systemd_problems)
*   *The H Open* 杂志上的[两](http://www.h-online.com/open/features/Control-Centre-The-systemd-Linux-init-system-1565543.html)[篇](http://www.h-online.com/open/features/Booting-up-Tools-and-tips-for-systemd-1570630.html)科普文章
*   [Lennart 的博文](http://0pointer.de/blog/projects/systemd.html)
*   [更新报告](http://0pointer.de/blog/projects/systemd-update.html)
*   [更新报告2](http://0pointer.de/blog/projects/systemd-update-2.html)
*   [更新报告3](http://0pointer.de/blog/projects/systemd-update-3.html)
*   [最新动态](http://0pointer.de/blog/projects/why.html)
*   [Fedora Wiki 上的 SysVinit 和 systemd 命令对比表](https://fedoraproject.org/wiki/SysVinit_to_Systemd_Cheatsheet/zh)