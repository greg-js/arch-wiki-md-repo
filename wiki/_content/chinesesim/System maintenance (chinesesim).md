相关文章

*   [General recommendations (简体中文)](/index.php/General_recommendations_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "General recommendations (简体中文)")

**翻译状态：** 本文是英文页面 [System_maintenance](/index.php/System_maintenance "System maintenance") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-11-02，点击[这里](https://wiki.archlinux.org/index.php?title=System_maintenance&diff=0&oldid=546559)可以查看翻译后英文页面的改动。

要持续使用 Arch linux，需要进行系统日常维护，每个用户都应该及时维护系统。

## Contents

*   [1 检查错误](#.E6.A3.80.E6.9F.A5.E9.94.99.E8.AF.AF)
    *   [1.1 systemd 服务问题](#systemd_.E6.9C.8D.E5.8A.A1.E9.97.AE.E9.A2.98)
    *   [1.2 日志文件](#.E6.97.A5.E5.BF.97.E6.96.87.E4.BB.B6)
*   [2 备份](#.E5.A4.87.E4.BB.BD)
    *   [2.1 配置文件](#.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
    *   [2.2 安装的软件包](#.E5.AE.89.E8.A3.85.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [2.3 Pacman 数据库](#Pacman_.E6.95.B0.E6.8D.AE.E5.BA.93)
    *   [2.4 LUKS headers](#LUKS_headers)
    *   [2.5 系统和用户数据](#.E7.B3.BB.E7.BB.9F.E5.92.8C.E7.94.A8.E6.88.B7.E6.95.B0.E6.8D.AE)
*   [3 更新系统](#.E6.9B.B4.E6.96.B0.E7.B3.BB.E7.BB.9F)
    *   [3.1 升级前的准备](#.E5.8D.87.E7.BA.A7.E5.89.8D.E7.9A.84.E5.87.86.E5.A4.87)
    *   [3.2 避免某些 Pacman 命令](#.E9.81.BF.E5.85.8D.E6.9F.90.E4.BA.9B_Pacman_.E5.91.BD.E4.BB.A4)
    *   [3.3 不支持部分升级](#.E4.B8.8D.E6.94.AF.E6.8C.81.E9.83.A8.E5.88.86.E5.8D.87.E7.BA.A7)
    *   [3.4 注意更新时的提醒](#.E6.B3.A8.E6.84.8F.E6.9B.B4.E6.96.B0.E6.97.B6.E7.9A.84.E6.8F.90.E9.86.92)
    *   [3.5 处理配置文件更新](#.E5.A4.84.E7.90.86.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6.E6.9B.B4.E6.96.B0)
    *   [3.6 回退有问题的更新](#.E5.9B.9E.E9.80.80.E6.9C.89.E9.97.AE.E9.A2.98.E7.9A.84.E6.9B.B4.E6.96.B0)
    *   [3.7 检查孤立和未使用软件包](#.E6.A3.80.E6.9F.A5.E5.AD.A4.E7.AB.8B.E5.92.8C.E6.9C.AA.E4.BD.BF.E7.94.A8.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [3.8 使用包管理器安装软件](#.E4.BD.BF.E7.94.A8.E5.8C.85.E7.AE.A1.E7.90.86.E5.99.A8.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6)
    *   [3.9 选择开源驱动](#.E9.80.89.E6.8B.A9.E5.BC.80.E6.BA.90.E9.A9.B1.E5.8A.A8)
    *   [3.10 谨慎使用非官方或测试不足的软件包](#.E8.B0.A8.E6.85.8E.E4.BD.BF.E7.94.A8.E9.9D.9E.E5.AE.98.E6.96.B9.E6.88.96.E6.B5.8B.E8.AF.95.E4.B8.8D.E8.B6.B3.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [3.11 更新镜像列表](#.E6.9B.B4.E6.96.B0.E9.95.9C.E5.83.8F.E5.88.97.E8.A1.A8)
*   [4 清理文件系统](#.E6.B8.85.E7.90.86.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
    *   [4.1 软件包缓存](#.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.BC.93.E5.AD.98)
    *   [4.2 不需要的软件包](#.E4.B8.8D.E9.9C.80.E8.A6.81.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [4.3 旧配置文件](#.E6.97.A7.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
    *   [4.4 破损的软链接](#.E7.A0.B4.E6.8D.9F.E7.9A.84.E8.BD.AF.E9.93.BE.E6.8E.A5)
*   [5 技巧](#.E6.8A.80.E5.B7.A7)
    *   [5.1 使用经过验证的软件包](#.E4.BD.BF.E7.94.A8.E7.BB.8F.E8.BF.87.E9.AA.8C.E8.AF.81.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [5.2 安装内核的长期支持版本](#.E5.AE.89.E8.A3.85.E5.86.85.E6.A0.B8.E7.9A.84.E9.95.BF.E6.9C.9F.E6.94.AF.E6.8C.81.E7.89.88.E6.9C.AC)
*   [6 参阅](#.E5.8F.82.E9.98.85)

## 检查错误

### systemd 服务问题

检查是否有 systemd 服务失败:

```
$ systemctl --failed

```

更多信息请参考 [Systemd#Analyzing the system state](/index.php/Systemd#Analyzing_the_system_state "Systemd").

### 日志文件

检查 `/var/log` 日志文件中是否存在错误, 检查[systemd 日志](/index.php/Systemd#Journal "Systemd")中的高优先级错误：

```
 # journalctl -p 3 -xb

```

Xorg 的相关错误可以查看 [Xorg#Troubleshooting](/index.php/Xorg#Troubleshooting "Xorg")。

## 备份

把重要数据的备份作为日常维护任务。

其它备份方案可以参考 [同步和备份程序页面](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")，[Category:System recovery](/index.php/Category:System_recovery "Category:System recovery") 包含其它相关文章。

可以通过 [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers") 自动备份.

### 配置文件

在编辑任何配置文件前，先保留备份。这样出问题是可以直接还原。[vim](/index.php/Vim "Vim") 和 [emacs](/index.php/Emacs "Emacs") 编辑器会自动备份，[etckeeper](/index.php/Etckeeper "Etckeeper") 可以将 `/etc` 纳入版本控制系统。详情请参考 [dotfiles#Version control](/index.php/Dotfiles#Version_control "Dotfiles")。

### 安装的软件包

维护一个所有安装软件包的列表，这样在不得己进行系统重装时，可以很快恢复到初始环境。

详情参考 [Pacman tips#List of installed packages](/index.php/Pacman_tips#List_of_installed_packages "Pacman tips")。

### Pacman 数据库

参考 [pacman/Tips and tricks#Backup the pacman database](/index.php/Pacman/Tips_and_tricks#Backup_the_pacman_database "Pacman/Tips and tricks").

### LUKS headers

如果 LUKS 使用密码加密，建议定期检查和同步 LUKS 加密分区的头部数据。参考 [Dm-crypt/Device encryption#Backup and restore](/index.php/Dm-crypt/Device_encryption#Backup_and_restore "Dm-crypt/Device encryption").

### 系统和用户数据

参考 [System backup](/index.php/System_backup "System backup")。

## 更新系统

建议日常进行[系统完整更新](/index.php/Pacman#Upgrading_packages "Pacman")，这样既能享受到最新的问题修复和安全更新，还可以避免一次更新太多的软件包，手动处理是分批进行的。从社区寻求帮助时，其他人会假定系统进行了完整更新。

手头上保留 Arch 安装盘或其它 Linux "Live" 环境，这样有问题是可以进行修正。如果在生产环境使用 Arch，无法接受任何的停机，那么在更新前请在非关键系统上测试新配置文件和软件包，没有问题的时候再部署到生产环境。

如果软件包来自 [AUR](/index.php/AUR "AUR"), 请注意更新完整.

### 升级前的准备

建议升级前访问 [Arch Linux 主页](https://www.archlinux.org/)查看最新消息（或订阅 [RSS](https://www.archlinux.org/feeds/news/)，或订阅 [arch-announce 邮件列表](https://mailman.archlinux.org/mailman/listinfo/arch-announce/)，或关注 [@archlinux](https://twitter.com/archlinux)。如果升级需要不寻常的用户操作介入时（无法简单地按照 *pacman* 的输出信息处理），以上信息总会给出合适的方法。

在更新[kernel](/index.php/Kernel "Kernel"), [xorg](/index.php/Xorg "Xorg"), [systemd](/index.php/Systemd "Systemd") 和 [glibc](https://www.archlinux.org/packages/?name=glibc)等重要软件之前, 查看[论坛](https://bbs.archlinux.org/)看是否有被报告的出错等问题.

有时候系统更新会出现问题并需要进行一些手动调整，请不要在重要任务前进行系统更新。

### 避免某些 Pacman 命令

避免 [部分更新](#.E4.B8.8D.E6.94.AF.E6.8C.81.E9.83.A8.E5.88.86.E5.8D.87.E7.BA.A7)，不要运行 `pacman -Sy` 而是运行 `pacman -Syu`.

一般情况下，避免使用 pacman 的 `--force` 选项，**尤其要避免** `pacman -Syu --force` 这种可能更新多个软件包的指令。`--force` 忽略文件冲突，可能导致文件丢失！如果系统按正常维护，Arch 开发者会给出明确的指导，在 Arch 主页会有通知。

避免使用 `-d` 选项，`pacman -Rdd package` 会在删除软件包时跳过依赖关系检查。如果删除了系统必要的依赖关系，可能导致系统损坏。

### 不支持部分升级

Arch Linux 是滚动发行版，新[库](https://en.wikipedia.org/wiki/Library_(computing) 版本将不断被推送到源。开发者和信任用户会按照需要重新构建源中的所有软件包。如果有本地安装的版本(例如 AUR 软件包)，需要在它们的依赖关系升级了[soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname")时重新编译。

也就是说，部分升级是**不被支持的**。

不要使用 `pacman -Sy package` 或等价命令如 `pacman -Sy` 之后再 `pacman -S package`。在安装软件包前请更新源并升级。同理请特别注意 IgnorePkg/IgnoreGroup 的使用。

如果进行了部分升级，二进制包因为找不到链接库而损坏，**不要通过简单的符号链接进行修正**。库升级 [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname") 是因为它们**不再向前兼容**。只要 *pacman* 可以运行，使用更新的源进行 `pacman -Syu` 就能修复这些问题。

[pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib) 软件包提供的 *checkupdates* 脚本可以检查更新但不进行实际安装。

### 注意更新时的提醒

当升级系统时， 请一定要注意[pacman](/index.php/Pacman "Pacman")输出的注意信息。 如果有需要用户手动操作的，请一定要立即搞定。 如果不明白 pacman 输出的信息， 请去论坛搜索或者看Arch Linux首页的新闻。

### 处理配置文件更新

pacman 可能会创建 `.pacnew` 和 `.pacsave` 文件，这是 pacman 会通知用户，而用户需要主动处理这些文件。详细的操作说明请参考：[Pacnew and Pacsave files](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files").

同样，注意所有你可能会复制或创建的配置文件。如果软件包提供了一个空配置文件，这个文件被复制到主目录，请注意查看示例文件是否有更新。

### 回退有问题的更新

如果软件包可能导致问题，软件包维护者会在更新时给出提示信息。在更新后遇到问题，请先确认 `/var/log/pacman.log` 中有没有提醒信息.

**Tip:** 可以使用 [wat-git](https://aur.archlinux.org/packages/wat-git/) 等工具搜索 pacman 日志。

然后看看 [https://www.archlinux.org/](https://www.archlinux.org/) 中有没有新闻，然后再到论坛上查找类似的问题，如果都没有找到，可用到 [论坛](https://bbs.archlinux.org), [IRC](/index.php/IRC "IRC") 中发帖求助。

[降级](/index.php/Downgrading_packages "Downgrading packages") 是最后的解决方案。

### 检查孤立和未使用软件包

更新系统后，可能有些软件包不再需要，或者不再属于官方软件仓库。

用 `pacman -Qtd` 命令查找之前作为依赖安装，现在不再需要的软件包。如果孤立的包还是需要的，可用修改 [安装原因](/index.php/Installation_reason "Installation reason")。如果不再需要，可用将其删除。

除此之外，有些软件包可能已经不再属于远程仓库，但是依然还安装在本地，用 `pacman -Qm` 命令查找所有这些软件包。注意此命令会包含手动安装的软件，例如 [AUR](/index.php/AUR "AUR") 中的软件。

### 使用包管理器安装软件

软件包管理 [pacman](/index.php/Pacman "Pacman") 可以比你更好的记录安装的文件。如果你手动地安装软件，你会过了一会就不知道你到底安装了什么，到底安装在哪里，安装导致的那些冲突，是否安装在了错误的地方，等等问题.

*   使用 [Pacman#Installing packages](/index.php/Pacman#Installing_packages "Pacman") 中介绍的方法安装官方软件包。
*   如果找不到需要的软件包，看看 [AUR](/index.php/AUR "AUR") 中有没有提供软件包打包脚本。
*   如果都没有找到，请学习[创建软件包](/index.php/Creating_packages "Creating packages")。

要清理自己安装的文件，可以[这里](/index.php/Pacman/Tips_and_tricks#Identify_files_not_owned_by_any_package "Pacman/Tips and tricks").

### 选择开源驱动

尽可能地选择开源驱动。避免私有驱动。大多数时候，开源驱动比私有驱动更加稳定可靠。开源驱动的bugs修改起来比较容易快速，但同时私有驱动提供更多的特性和性能，不过也可能带来稳定性的代价。为了避免这个两难选择，可以选择已知的有很好的开源驱动支持的硬件。关于硬件和开源Linux驱动的信息可以在这里找到：[linux-drivers.org](http://www.linux-drivers.org/).

### 谨慎使用非官方或测试不足的软件包

在使用 AUR 或 [非官方软件仓库](/index.php/Unofficial_user_repository "Unofficial user repository")中的软件包时应有预防措施。大部分软件包都是由用户提供的，并不能提供和官方软件仓库相同的质量。谨慎使用 [AUR helpers](/index.php/AUR_helpers "AUR helpers") ，他们简化了 AUR 中的软件包的安装过程, 在编译和安装 AUR 中的软件包之前，**务必**检查软件包的 PKGBUILD 确保其中不含有错误或恶意的代码。

只在绝对必要的情况下使用第三方的软件仓库.[pacman/Tips and tricks#Maintenance](/index.php/Pacman/Tips_and_tricks#Maintenance "Pacman/Tips and tricks")提供了清理软件的方法。

### 更新镜像列表

镜像的质量会随着时间而变化，有些镜像会下线或者同步和下载出问题，所以请注意更新 pacman 的镜像列表，详情参考 [mirrors](/index.php/Mirrors "Mirrors")。

## 清理文件系统

检查磁盘空间的使用状况，删除占用空间较大的无用文件：

*   [List of applications#Disk usage display](/index.php/List_of_applications#Disk_usage_display "List of applications").
*   [List of applications#Disk cleaning](/index.php/List_of_applications#Disk_cleaning "List of applications").

### 软件包缓存

从 `/var/cache/pacman/pkg/` 删除不需要的 `.pkg` 可以减少空间占用。详情参考 [Pacman#Cleaning the package cache](/index.php/Pacman#Cleaning_the_package_cache "Pacman").

### 不需要的软件包

从系统里面删除不需要的软件包可以减少空间占用和维护难度。详情参考 [Pacman/Tips and tricks#Removing unused packages (orphans)](/index.php/Pacman/Tips_and_tricks#Removing_unused_packages_.28orphans.29 "Pacman/Tips and tricks").

### 旧配置文件

旧的配置文件可能和新软件版本不兼容，所以请定期清理和更新配置文件，尤其是主目录和 `~/.config`. 在重新安装或共享 /home 时，注意下面文件夹：

*   `~/.config/` -- 软件保存配置文件的地方
*   `~/.cache/` -- 程序缓存大小可能持续增加
*   `~/.local/share/` -- 可能有旧文件

参考 [XDG Base Directory support](/index.php/XDG_Base_Directory_support "XDG Base Directory support").

为了帮助清理 home 目录，建议维护一份不需要的文件列表并定期清理，例如使用 [rmshit.py](https://github.com/lahwaacz/Scripts/blob/master/rmshit.py).

[rmlint](https://www.archlinux.org/packages/?name=rmlint) 也可以用来查找不需要的重复文件，空文件和损坏的软链接。

### 破损的软链接

系统中可能存在老的，损坏的软链接，应该删除它们。方法可以参考 [here](https://unix.stackexchange.com/questions/34248/how-can-i-find-broken-symlinks) 和 [here](http://www.commandlinefu.com/commands/view/8260/find-broken-symlinks).

下面命令可以列出所有有问题的软链接，可以检查并删除列表中的文件。

```
  # find -xtype l -print

```

## 技巧

### 使用经过验证的软件包

Arch 的滚动发行让用户可以使用最新的功能和上游更新，但是这也增加了系统维护的难度。为了增加稳定性，可以尽量使用经过验证的稳定版本。这些软件包不太容易在升级时遇到问题。选用具有活跃开发社区的软件，选用用户能力更出众的软件，这样在出问题是更容易获得帮助。

避免使用测试仓库，这些软件包都是实验性质，不适合安装到稳定系统。因此对于[AUR](/index.php/AUR "AUR")中的包以及部分 community 中的包需要一些谨慎，这些开发中的包是直接从上游开发版分支中获取到的，通常会在包的名字上注有：dev, devel, svn, cvs, git, hg, 或是 darcs 的信息。

### 安装内核的长期支持版本

[linux-lts](https://www.archlinux.org/packages/?name=linux-lts) 是 Arch 官方提供的 Linux kernel 的长期支持版本。内核上游开发者针对此版本提供了长期支持，包括安全补丁和功能 backports。适用于需要长期支持的用户，也可以将此内核作为新内核升级的后备内核。

需要编辑 [bootloader](/index.php/Bootloader "Bootloader") 的启动加载项，启动到 `vmlinuz-linux-lts` 和 `initramfs-linux-lts.img`。

## 参阅

*   [Arch News Bash Script](https://bbs.archlinux.org/viewtopic.php?id=146850)
*   [Automatic Arch System Maintenance](https://bbs.archlinux.org/viewtopic.php?pid=1791008)