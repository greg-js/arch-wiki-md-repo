相关文章

*   [systemd/User (简体中文)](/index.php/Systemd/User_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd/User (简体中文)")
*   [systemd/Timers (简体中文)](/index.php/Systemd/Timers_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd/Timers (简体中文)")
*   [Systemd FAQ (简体中文)](/index.php/Systemd_FAQ_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd FAQ (简体中文)")
*   [Daemons#List of deamons](/index.php/Daemons#List_of_deamons "Daemons")
*   [udev (简体中文)](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udev (简体中文)")
*   [Improve Boot Performance (简体中文)](/index.php/Improve_Boot_Performance_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Improve Boot Performance (简体中文)")
*   [Allow users to shutdown](/index.php/Allow_users_to_shutdown "Allow users to shutdown")

**翻译状态：** 本文是英文页面 [Systemd](/index.php/Systemd "Systemd") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-05-09，点击[这里](https://wiki.archlinux.org/index.php?title=Systemd&diff=0&oldid=517689)可以查看翻译后英文页面的改动。

摘自[项目主页](http://freedesktop.org/wiki/Software/systemd)：

	*systemd* 是一个 Linux 系统基础组件的集合，提供了一个系统和服务管理器，运行为 PID 1 并负责启动其它程序。功能包括：支持并行化任务；同时采用 socket 式与 [D-Bus](/index.php/D-Bus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "D-Bus (简体中文)") 总线式激活服务；按需启动守护进程（daemon）；利用 Linux 的 [cgroups](/index.php/Cgroups "Cgroups") 监视进程；支持快照和系统恢复；维护挂载点和自动挂载点；各服务间基于依赖关系进行精密控制。*systemd* 支持 SysV 和 LSB 初始脚本，可以替代 sysvinit。除此之外，功能还包括日志进程、控制基础系统配置，维护登陆用户列表以及系统账户、运行时目录和设置，可以运行容器和虚拟机，可以简单的管理网络配置、网络时间同步、日志转发和名称解析等。

**注意:** [Arch Linux 论坛的这篇帖子](https://bbs.archlinux.org/viewtopic.php?pid=1149530#p1149530) 详细地解释了 Arch Linux 迁移到 systemd 的原因。

## Contents

*   [1 systemd 基本工具](#systemd_基本工具)
    *   [1.1 分析系统状态](#分析系统状态)
    *   [1.2 使用单元](#使用单元)
    *   [1.3 电源管理](#电源管理)
*   [2 编写单元文件](#编写单元文件)
    *   [2.1 处理依赖关系](#处理依赖关系)
    *   [2.2 服务类型](#服务类型)
    *   [2.3 修改现存单元文件](#修改现存单元文件)
        *   [2.3.1 替换单元文件](#替换单元文件)
        *   [2.3.2 附加配置片段](#附加配置片段)
        *   [2.3.3 重置到软件包版本](#重置到软件包版本)
        *   [2.3.4 示例](#示例)
*   [3 目标（target）](#目标（target）)
    *   [3.1 获取当前目标](#获取当前目标)
    *   [3.2 创建自定义目标](#创建自定义目标)
    *   [3.3 "SysV 运行级别" 与 "systemd 目标" 对照表](#"SysV_运行级别"_与_"systemd_目标"_对照表)
    *   [3.4 切换当前运行目标](#切换当前运行目标)
    *   [3.5 更改开机默认启动目标](#更改开机默认启动目标)
*   [4 临时文件](#临时文件)
*   [5 定时器](#定时器)
*   [6 挂载](#挂载)
*   [7 日志](#日志)
    *   [7.1 优先级](#优先级)
    *   [7.2 功能](#功能)
    *   [7.3 过滤输出](#过滤输出)
    *   [7.4 日志大小限制](#日志大小限制)
    *   [7.5 配合 syslog 使用](#配合_syslog_使用)
    *   [7.6 手动清理日志](#手动清理日志)
    *   [7.7 Journald in conjunction with syslog](#Journald_in_conjunction_with_syslog)
    *   [7.8 转发 journald 到 /dev/tty12](#转发_journald_到_/dev/tty12)
    *   [7.9 查看特定位置的日志](#查看特定位置的日志)
*   [8 Tips and tricks](#Tips_and_tricks)
    *   [8.1 Running services after the network is up](#Running_services_after_the_network_is_up)
    *   [8.2 Enable installed units by default](#Enable_installed_units_by_default)
    *   [8.3 Sandboxing application environments](#Sandboxing_application_environments)
*   [9 疑难解答](#疑难解答)
    *   [9.1 寻找错误](#寻找错误)
    *   [9.2 诊断启动问题](#诊断启动问题)
    *   [9.3 诊断一个服务](#诊断一个服务)
    *   [9.4 关机/重启十分缓慢](#关机/重启十分缓慢)
    *   [9.5 短时进程无日志记录](#短时进程无日志记录)
    *   [9.6 禁止在程序崩溃时转储内存](#禁止在程序崩溃时转储内存)
    *   [9.7 启动的时间太长](#启动的时间太长)
    *   [9.8 systemd-tmpfiles-setup.service 在启动时启动失败](#systemd-tmpfiles-setup.service_在启动时启动失败)
    *   [9.9 启动时显示的 systemd 版本和安装版本不一致](#启动时显示的_systemd_版本和安装版本不一致)
    *   [9.10 禁用远程机器的 emergency 模式](#禁用远程机器的_emergency_模式)
*   [10 相关资源](#相关资源)

## systemd 基本工具

监视和控制systemd的主要命令是`systemctl`。该命令可用于查看系统状态和管理系统及服务。详见[systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1)。、

**提示：**

*   在 `systemctl` 参数中添加 `-H <用户名>@<主机名>` 可以实现对其他机器的远程控制。该功能使用 [SSH](/index.php/SSH_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SSH (简体中文)") 连接。
*   [Plasma](/index.php/Plasma "Plasma") 用户可以安装 *systemctl* 图形前端 [systemd-kcm](https://aur.archlinux.org/packages/systemd-kcm/)。安装后可以在 *System administration* 下找到。

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

一个单元配置文件可以描述如下内容之一：系统服务（`.service`）、挂载点（`.mount`）、sockets（`.sockets`） 、系统设备（`.device`）、交换分区（`.swap`）、文件路径（`.path`）、启动目标（`.target`）、由 systemd 管理的计时器（`.timer`）。详情参阅 [systemd.unit(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.unit.5) 。

使用 `systemctl` 控制单元时，通常需要使用单元文件的全名，包括扩展名（例如 `sshd.service` ）。但是有些单元可以在 `systemctl` 中使用简写方式。

*   如果无扩展名，systemctl 默认把扩展名当作 `.service` 。例如 `netcfg` 和 `netcfg.service` 是等价的。
*   挂载点会自动转化为相应的 `.mount` 单元。例如 `/home` 等价于 `home.mount` 。
*   设备会自动转化为相应的 `.device` 单元，所以 `/dev/sda2` 等价于 `dev-sda2.device` 。

**注意:** 有一些单元的名称包含一个 `@` 标记（例如： `name@*string*.service` ），这意味着它是模板单元 `name@.service` 的一个 [实例](http://0pointer.de/blog/projects/instances.html)。 `*string*` 被称作实例标识符，在 *systemctl* 调用模板单元时，会将其当作一个参数传给模板单元，模板单元会使用这个传入的参数代替模板中的 `%I` 指示符。

在实例化之前，*systemd* 会先检查 `name@string.suffix` 文件是否存在（如果存在，就直接使用这个文件，而不是模板实例化）。大多数情况下，包含 `@` 标记都意味着这个文件是模板。如果一个模板单元没有实例化就调用，该调用会返回失败，因为模板单元中的 `%I` 指示符没有被替换。

**提示：**

*   下面的大部分命令都可以跟多个单元名, 详细信息参见 [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1)。
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

设置单元为自动启动并立即启动这个单元:

```
# systemctl enable --now *unit*

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

`systemd` [单元文件](http://www.freedesktop.org/software/systemd/man/systemd.unit.html)的语法来源于 XDG 桌面项配置文件`.desktop`文件，最初的源头则是Microsoft Windows的`.ini`文件。单元文件可以从多个地方加载，`systemctl show --property=UnitPath` 可以按优先级从低到高显示加载目录：

*   `/usr/lib/systemd/system/` ：软件包安装的单元
*   `/etc/systemd/system/` ：系统管理员安装的单元

**注意:**

*   当 `systemd` 运行在[用户模式](/index.php/Systemd/User#How_it_works "Systemd/User")下时，使用的加载路径是完全不同的。
*   systemd 单元名仅能包含 ASCII 字符，下划线和点号和有特殊意义的字符('@', '-')。其它字符需要用 C-style "\x2d" 替换。参阅 [systemd.unit(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.unit.5) 和 [systemd-escape(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-escape.1) 。

单元文件的语法，可以参考系统已经安装的单元，也可以参考 [systemd.service(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5) 中的[EXAMPLES章节](http://www.freedesktop.org/software/systemd/man/systemd.service.html#Examples)。

**提示：** 以 `#` 开头的注释可能也能用在 unit-files 中，但是只能在新行中使用。不要在 *systemd* 的参数后面使用行末注释， 否则 unit 将会启动失败。

### 处理依赖关系

使用 systemd 时，可通过正确编写单元配置文件来解决其依赖关系。典型的情况是，单元 `A` 要求单元 `B` 在 `A` 启动之前运行。在此情况下，向单元 `A` 配置文件中的 `[Unit]` 段添加 `Requires=B` 和 `After=B` 即可。若此依赖关系是可选的，可添加 `Wants=B` 和 `After=B` 。请注意 `Wants=` 和 `Requires=` 并不意味着 `After=` ，即如果 `After=` 选项没有制定，这两个单元将被并行启动。

依赖关系通常被用在服务（service）而不是[目标（target）](#目标（target）)上。例如， `network.target` 一般会被某个配置网络接口的服务引入，所以，将自定义的单元排在该服务之后即可，因为 `network.target` 已经启动。

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

为了避免和 pacman 冲突，不应该直接编辑软件包提供的文件。有两种方法可以不改动原始文件就做到修改单元文件：创建一个优先级更高的本地单元文件或创建一个片段，应用到原始单元文件之上。两种方法都需要在修改后重新加载单元，用 `systemctl edit` 编辑单元(会自动重载单元)或通过下面命令重新加载单元：

```
# systemctl daemon-reload

```

**提示：**

*   `systemd-delta` 命令用来查看哪些单元文件被覆盖、哪些被修改。系统维护的时候需要及时了解哪些单元已经有了更新。
*   使用 `systemctl cat *unit*` 可以查看单元的内容和所有相关的片段.
*   安装 [vim-systemd](https://www.archlinux.org/packages/?name=vim-systemd) 软件包，可以使单元配置文件在 [Vim](/index.php/Vim "Vim") 下支持语法高亮。

#### 替换单元文件

要替换 `/usr/lib/systemd/system/*unit*`, 创建文件 `/etc/systemd/system/*unit*` 并重新启用单元以更新链接：

```
# systemctl reenable *unit*

```

或者运行：

```
# systemctl edit --full *unit*

```

这将会在记事本中打开 `/etc/systemd/system/*unit*`，如果文件不存在，可以将安装的版本复制到这里，在编辑完成之后，会自动加载新版本。

**注意:** 即使 Pacman 更新了新的单元文件，软件包中的版本也不会被使用，所以这个方式会增加系统维护的难度，推荐使用下面一种方法。

#### 附加配置片段

要附加配置片段，先创建名为 `/etc/systemd/system/<单元名>.d/` 的目录，然后放入 `*.conf` 文件，其中可以添加或重置参数。这里设置的参数优先级高于原来的单元文件。下面的更新方式比较简单：

```
# systemctl edit *unit*

```

这将会在编辑器中打开文件 `/etc/systemd/system/*unit*.d/override.conf`，编辑完成之后自动加载。

**Note:** 并不是所有参数都会被子配置文件覆盖。例如要修改 `Conflicts=` 就必须 [替换原始文件](https://lists.freedesktop.org/archives/systemd-devel/2017-June/038976.html)。

#### 重置到软件包版本

要回退单元的变更，使用 `systemctl edit` 并执行:

```
# systemctl revert *unit*

```

#### 示例

例如，如果想添加一个额外的依赖，创建如下文件即可：

 `/etc/systemd/system/<unit>.d/customdependency.conf` 
```
[Unit]
Requires=<新依赖>
After=<新依赖>
```

要修改一个非 `oneshot` 单元的 `ExecStart` 命令，创建下面文件:

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

## 目标（target）

运行级别（runlevel）是一个旧的概念。现在，systemd 引入了一个和运行级别功能相似又不同的概念——目标（target）。不像数字表示的启动级别，每个*目标*都有名字和独特的功能，并且能同时启用多个。一些*目标*继承其他*目标*的服务，并启动新服务。systemd 提供了一些模仿 sysvinit 运行级别的*目标*，仍可以使用旧的 `telinit 运行级别` 命令切换。

### 获取当前目标

不要使用 `runlevel` 命令了：

```
$ systemctl list-units --type=target

```

### 创建自定义目标

在 *sysvinit* 中有明确定义的运行级别（如：0、1、3、5、6）与 *systemd* 中特定的 *目标* 存在一一对应的关系。然而，对于用户自定义运行级别（2、4）却没有。如需要同样功能，建议你以原有运行级别所对应的 systemd 目标为基础，新建一个`/etc/systemd/system/*<目标名>.target*`（可参考`/usr/lib/systemd/system/graphical.target`）, 然后创建目录`/etc/systemd/system/<目标名>.wants`，并向其中加入需启用的服务链接（指向`/ur/lib/systemd/system/`）。

### "SysV 运行级别" 与 "systemd 目标" 对照表

| SysV 运行级别 | Systemd 目标 | 注释 |
| 0 | runlevel0.target, poweroff.target | 中断系统（halt） |
| 1, s, single | runlevel1.target, rescue.target | 单用户模式 |
| 2, 4 | runlevel2.target, runlevel4.target, multi-user.target | 用户自定义运行级别，通常识别为级别3。 |
| 3 | runlevel3.target, multi-user.target | 多用户，无图形界面。用户可以通过终端或网络登录。 |
| 5 | runlevel5.target, graphical.target | 多用户，图形界面。继承级别3的服务，并启动图形界面服务。 |
| 6 | runlevel6.target, reboot.target | 重启 |
| emergency | emergency.target | 急救模式（Emergency shell） |

### 切换当前运行目标

systemd中，运行目标通过“目标单元”访问。通过如下命令切换：

```
# systemctl isolate graphical.target

```

该命令仅更改当前运行目标，对下次启动无影响。这等价于sysvinit中的 `telinit 3` 或 `telinit 5` 命令。

### 更改开机默认启动目标

开机启动的目标是 `default.target`，默认链接到 `graphical.target` （大致相当于原来的运行级别5）。

用 *systemctl* 验证当前的默认启动目标：

```
# systemctl get-default

```

用 *systemctl* 修改`default.target`以变更开机默认启动目标：

 `$ systemctl set-default multi-user.target` 
```
Removed /etc/systemd/system/default.target.
Created symlink /etc/systemd/system/default.target -> /usr/lib/systemd/system/graphical.target.
```

另一方法是向bootloader添加[内核参数](/index.php/Kernel_parameters_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel parameters (简体中文)")：

*   `systemd.unit=multi-user.target` （大致相当于运行级别3）
*   `systemd.unit=rescue.target` （大致相当于运行级别1）

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

详情参见`systemd-tmpfiles(8)` 和 [tmpfiles.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tmpfiles.d.5)。

**注意:** 该方法不能向 `/sys` 中的配置文件添加参数，因为 `systemd-tmpfiles-setup` 有可能在相关模块加载前运行。这种情况下，需要首先通过 `modinfo <模块名>` 确认需要的参数，然后在 [`/etc/modprobe.d` 目录下的配置文件](/index.php/Kernel_modules_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#选项 "Kernel modules (简体中文)")中修改配置参数。另外，还可以使用 [udev 规则](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#udev_规则 "Udev (简体中文)")，在设备就绪时设置相应属性。

## 定时器

一个定时器是一个以 `.timer` 为结尾的单元配置文件并包含由 `systemd` 控制和监督的信息。[systemd/Timers (简体中文)](/index.php/Systemd/Timers_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd/Timers (简体中文)")

**注意:** 定时器很大程度上可取代 `cron`。[systemd/Timers (简体中文)#替代 cron](/index.php/Systemd/Timers_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#替代_cron "Systemd/Timers (简体中文)")

## 挂载

因为 systemd 也负责按 `/etc/fstab` 挂载目录。在系统启动和重新加载系统管理器时，[systemd-fstab-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-fstab-generator.8) 会将 `/etc/fstab` 中的配置转化为 systemd 单元。

*systemd* 扩展了 [fstab](/index.php/Fstab "Fstab") 的传统功能，提供了额外的挂载选项。例如可以确保一个挂载仅在网络已经连接时进行，或者仅当另外一个分区已挂载时再挂载。这些选项通常以 `x-systemd.` 开头，[systemd.mount(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.mount.5#FSTAB) 中包含了完整说明。

*automounting* 也是一个例子，可以在使用时，而不是启动时挂载分区，详情请参考 [fstab#Automount with systemd](/index.php/Fstab#Automount_with_systemd "Fstab")。

## 日志

systemd 提供了自己的日志系统（logging system），称为 journal。使用 systemd 日志，无需额外安装日志服务（syslog）。读取日志的命令：

```
# journalctl

```

默认情况下（当 `Storage=` 在文件 `/etc/systemd/journald.conf` 中被设置为 `auto`），日志记录将被写入 `/var/log/journal/`。该目录是 [systemd](https://www.archlinux.org/packages/?name=systemd) 软件包的一部分。若被删除，systemd **不会**自动创建它，直到下次升级软件包时重建该目录。如果该目录缺失，systemd 会将日志记录写入 `/run/systemd/journal`。这意味着，系统重启后日志将丢失。

**提示：** 如果 `/var/log/journal/` 位于 [btrfs](/index.php/Btrfs "Btrfs") 文件系统，应该考虑对这个目录禁用写入时复制，方法参阅[Btrfs#Copy-on-Write (CoW)](/index.php/Btrfs#Copy-on-Write_(CoW) "Btrfs")。

Systemd 日志事件提示信息的记录安装优先级和更能进行分离，符合经典的 BSD syslog 协议风格（[维基百科](https://en.wikipedia.org/wiki/Syslog "wikipedia:Syslog")，[RFC 5424](https://tools.ietf.org/html/rfc5424)）。

### 优先级

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

### 功能

A syslog facility code is used to specify the type of program that is logging the message [RFC 5424 Section 6.2.1](https://tools.ietf.org/html/rfc5424#section-6.2.1).

| Facility code | Keyword | Description | Info |
| 0 | kern | kernel messages |
| 1 | user | user-level messages |
| 2 | mail | mail system | Archaic POSIX still supported and sometimes used system, for more [mail(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mail.1)) |
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

详情参阅[journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1)、[systemd.journal-fields(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.journal-fields.7)，以及 Lennert 的这篇[博文](http://0pointer.de/blog/projects/journalctl.html)。

### 日志大小限制

如果按上面的操作保留日志的话，默认日志最大限制为所在文件系统容量的 10%，即：如果 `/var/log/journal` 储存在 50GiB 的根分区中，那么日志最多存储 5GiB 数据。可以修改配置文件指定最大限制。如限制日志最大 50MiB：

 `/etc/systemd/journald.conf`  `SystemMaxUse=50M` 

还可以通过配置片段而不是全局配置文件进行设置：

 `/etc/systemd/journald.conf.d/00-journal-size.conf` 
```
[Journal]
SystemMaxUse=50M
```

修改配置后要立即生效，请[重启](/index.php/Restart "Restart") `systemd-journald.service` 服务。

详情参见 [journald.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journald.conf.5).

### 配合 syslog 使用

systemd 提供了 socket `/run/systemd/journal/syslog`，以兼容传统日志服务。所有系统信息都会被传入。要使传统日志服务工作，需要让服务链接该 socket，而非 `/dev/log`（[官方说明](http://lwn.net/Articles/474968/)）。Arch 软件仓库中的 [syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng) 已经包含了需要的配置。

`journald.conf` 使用 `no` 转发socket . 为了使 *syslog-ng* 配合 *journald* , 你需要在 `/etc/systemd/journald.conf` 中设置 `ForwardToSyslog=yes` . 参阅 [Syslog-ng#Overview](/index.php/Syslog-ng#Overview "Syslog-ng") 了解更多细节.

如果你选择使用 [rsyslog](https://aur.archlinux.org/packages/rsyslog/) , 因为 [rsyslog](/index.php/Rsyslog "Rsyslog") 从日志中 [直接](http://lists.freedesktop.org/archives/systemd-devel/2014-August/022295.html#journald) 传出消息,所以不再必要改变那个选项..

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

参阅 [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1) 获得更多信息.

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

### Running services after the network is up

To delay a service after the network is up, include the following dependencies in the *.service* file:

 `/etc/systemd/system/*foo*.service` 
```
[Unit]	
...
**Wants=network-online.target**
**After=network-online.target**	
...
```

The network wait service of the particular application that manages the network, must also be enabled so that `network-online.target` properly reflects the network status.

*   For the ones using [NetworkManager](/index.php/NetworkManager "NetworkManager"), [enable](/index.php/Enable "Enable") `NetworkManager-wait-online.service`.
*   If using [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd"), `systemd-networkd-wait-online.service` is by default enabled automatically whenever `systemd-networkd.service` has been enabled; check this is the case with `systemctl is-enabled systemd-networkd-wait-online.service`, there is no other action needed.

For more detailed explanations see [Running services after the network is up](https://www.freedesktop.org/wiki/Software/systemd/NetworkTarget/) in the systemd wiki.

### Enable installed units by default

Arch Linux ships with `/usr/lib/systemd/system-preset/99-default.preset` containing `disable *`. This causes *systemctl preset* to disable all units by default, such that when a new package is installed, the user must manually enable the unit.

If this behavior is not desired, simply create a symlink from `/etc/systemd/system-preset/99-default.preset` to `/dev/null` in order to override the configuration file. This will cause *systemctl preset* to enable all units that get installed—regardless of unit type—unless specified in another file in one *systemctl preset'*s configuration directories. User units are not affected. See the manpage for `systemd.preset` for more information.

**Note:** Enabling all units by default may cause problems with packages that contain two or more mutually exclusive units. *systemctl preset* is designed to be used by distributions and spins or system administrators. In the case where two conflicting units would be enabled, you should explicitly specify which one is to be disabled in a preset configuration file as specified in the manpage for `systemd.preset`.

### Sandboxing application environments

A unit file can be created as a sandbox to isolate applications and their processes within a hardened virtual environment. systemd leverages [namespaces](https://en.wikipedia.org/wiki/Linux_namespaces "wikipedia:Linux namespaces"), white-/blacklisting of [Capabilities](/index.php/Capabilities "Capabilities"), and [control groups](/index.php/Control_groups "Control groups") to container processes through an extensive [execution environment configuration](https://www.freedesktop.org/software/systemd/man/systemd.exec.html).

The enhancement of an existing systemd unit file with application sandboxing typically requires trial-and-error tests accompanied by the generous use of [strace](https://www.archlinux.org/packages/?name=strace), [stderr](https://en.wikipedia.org/wiki/Standard_streams#Standard_error_.28stderr.29 "wikipedia:Standard streams") and [journalctl](https://www.freedesktop.org/software/systemd/man/journalctl.html) error logging and output facilities. You may want to first search upstream documentation for already done tests to base trials on.

Some examples on how sandboxing with systemd can be deployed:

*   `CapabilityBoundingSet` defines a whitelisted set of allowed capabilities, but may also be used to blacklist a specific capability for a unit.
    *   The `CAP_SYS_ADM` capability, for example, which should be one of the [goals of a secure sandbox](https://lwn.net/Articles/486306/): `CapabilityBoundingSet=~ CAP_SYS_ADM`

## 疑难解答

### 寻找错误

这个例子中的失败的服务是 `systemd-modules-load` :

**1.** 通过 *systemd* 寻找启动失败的服务:

 `$ systemctl --state=failed`  `systemd-modules-load.service   loaded **failed failed**  Load Kernel Modules` 

或者使用 *systemd* 消息:

```
$ journalctl -fp err

```

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

### 诊断启动问题

使用如下内核参数引导： `systemd.log_level=debug systemd.log_target=kmsg log_buf_len=1M`

更多有关调试的信息，参见[该文](http://freedesktop.org/wiki/Software/systemd/Debugging)。

### 诊断一个服务

如果某个 *systemd* 服务的工作状况不合预期,希望调试的话,设置 `SYSTEMD_LOG_LEVEL` [环境变量](/index.php/Environment_variable "Environment variable") 为 `debug` . 例如以调试模式运行 *systemd-networkd* 服务:

在此服务的配置文件片段中加入：

```
[Service]
Environment=SYSTEMD_LOG_LEVEL=debug

```

或者等价的,临时编辑系统单元文件,例如:

1.  SYSTEMD_LOG_LEVEL=debug /lib/systemd/systemd-networkd

[重启](/index.php/Restart "Restart") *systemd-networkd* 服务，用 `--follow` 选项检查日志。

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

### 启动时显示的 systemd 版本和安装版本不一致

需要 [重新生成 initramfs](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio")。

**提示：** 可以使用 pacman 钩子在更新 [systemd](https://www.archlinux.org/packages/?name=systemd)时重新生成 initramfs。参考 [这个帖子](https://bbs.archlinux.org/viewtopic.php?id=215411) 和 [Pacman#Hooks](/index.php/Pacman#Hooks "Pacman").

### 禁用远程机器的 emergency 模式

如果远程机器位于云主机，emergency 模式会导致系统无法远程连接，可以通过下面方式禁用紧急模式：

```
# systemctl mask emergency.service
# systemctl mask emergency.target

```

## 相关资源

*   [Wikipedia article](https://en.wikipedia.org/wiki/systemd "wikipedia:systemd")
*   [systemd Official web site](http://www.freedesktop.org/wiki/Software/systemd)
*   [systemd optimizations](http://www.freedesktop.org/wiki/Software/systemd/Optimizations)
*   [systemd FAQ](http://www.freedesktop.org/wiki/Software/systemd/FrequentlyAskedQuestions)
*   [systemd Tips and tricks](http://www.freedesktop.org/wiki/Software/systemd/TipsAndTricks)
*   [Gentoo Wiki systemd page](http://wiki.gentoo.org/wiki/Systemd)
*   [Fedora Project - About systemd](http://fedoraproject.org/wiki/Systemd)
*   [Fedora Project - How to debug systemd problems](http://fedoraproject.org/wiki/How_to_debug_Systemd_problems)
*   [Fedora Project - SysVinit to systemd cheatsheet](http://fedoraproject.org/wiki/SysVinit_to_Systemd_Cheatsheet)
*   [Debian Wiki systemd page](https://wiki.debian.org/systemd "debian:systemd")
*   [Manual pages](http://0pointer.de/public/systemd-man/)
*   [Lennart's blog story](http://0pointer.de/blog/projects/systemd.html), [update 1](http://0pointer.de/blog/projects/systemd-update.html), [update 2](http://0pointer.de/blog/projects/systemd-update-2.html), [update 3](http://0pointer.de/blog/projects/systemd-update-3.html), [summary](http://0pointer.de/blog/projects/why.html)
*   [systemd for Administrators (PDF)](http://0pointer.de/public/systemd-ebook-psankar.pdf)
*   [How To Use Systemctl to Manage Systemd Services and Units](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units)
*   [Session management with systemd-logind](https://dvdhrm.wordpress.com/2013/08/24/session-management-on-linux/)
*   [Emacs Syntax highlighting for Systemd files](/index.php/Emacs#Syntax_highlighting_for_systemd_Files "Emacs")
*   [Two](http://www.h-online.com/open/features/Control-Centre-The-systemd-Linux-init-system-1565543.html) [part](http://www.h-online.com/open/features/Booting-up-Tools-and-tips-for-systemd-1570630.html) introductory article in *The H Open* magazine.