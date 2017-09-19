相关文章

*   [常见问题](/index.php/FAQ_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "FAQ (简体中文)")
*   [安装指南](/index.php/Installation_Guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installation Guide (简体中文)")
*   [软件列表](/index.php/List_of_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of applications (简体中文)")

**翻译状态：** 本文是英文页面 [General_Recommendations](/index.php/General_Recommendations "General Recommendations") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-25，点击[这里](https://wiki.archlinux.org/index.php?title=General_Recommendations&diff=0&oldid=447656)可以查看翻译后英文页面的改动。

本文是各种重要或常用的文章的详细索引。阅读本文前，读者应该先通过 [官方安装指南](/index.php/%E5%AE%98%E6%96%B9%E5%AE%89%E8%A3%85%E6%8C%87%E5%8D%97 "官方安装指南") 安装 Arch Linux 基本系统。

**注意:** 中国用户可以特别留意 [#中国大陆用户的推荐解决方案](#.E4.B8.AD.E5.9B.BD.E5.A4.A7.E9.99.86.E7.94.A8.E6.88.B7.E7.9A.84.E6.8E.A8.E8.8D.90.E8.A7.A3.E5.86.B3.E6.96.B9.E6.A1.88) 内容。

## Contents

*   [1 系统管理](#.E7.B3.BB.E7.BB.9F.E7.AE.A1.E7.90.86)
    *   [1.1 用户和用户组](#.E7.94.A8.E6.88.B7.E5.92.8C.E7.94.A8.E6.88.B7.E7.BB.84)
    *   [1.2 权限提升](#.E6.9D.83.E9.99.90.E6.8F.90.E5.8D.87)
    *   [1.3 系统服务](#.E7.B3.BB.E7.BB.9F.E6.9C.8D.E5.8A.A1)
    *   [1.4 系统维护](#.E7.B3.BB.E7.BB.9F.E7.BB.B4.E6.8A.A4)
*   [2 软件包管理](#.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.AE.A1.E7.90.86)
    *   [2.1 Pacman](#Pacman)
    *   [2.2 软件仓库镜像](#.E8.BD.AF.E4.BB.B6.E4.BB.93.E5.BA.93.E9.95.9C.E5.83.8F)
    *   [2.3 软件仓库](#.E8.BD.AF.E4.BB.B6.E4.BB.93.E5.BA.93)
    *   [2.4 Arch编译系统（ABS）](#Arch.E7.BC.96.E8.AF.91.E7.B3.BB.E7.BB.9F.EF.BC.88ABS.EF.BC.89)
    *   [2.5 Arch用户软件源（AUR）](#Arch.E7.94.A8.E6.88.B7.E8.BD.AF.E4.BB.B6.E6.BA.90.EF.BC.88AUR.EF.BC.89)
*   [3 启动](#.E5.90.AF.E5.8A.A8)
    *   [3.1 硬件自动探测](#.E7.A1.AC.E4.BB.B6.E8.87.AA.E5.8A.A8.E6.8E.A2.E6.B5.8B)
    *   [3.2 微代码](#.E5.BE.AE.E4.BB.A3.E7.A0.81)
    *   [3.3 保留启动信息](#.E4.BF.9D.E7.95.99.E5.90.AF.E5.8A.A8.E4.BF.A1.E6.81.AF)
    *   [3.4 开机启动 X](#.E5.BC.80.E6.9C.BA.E5.90.AF.E5.8A.A8_X)
    *   [3.5 开机时打开 Num Lock](#.E5.BC.80.E6.9C.BA.E6.97.B6.E6.89.93.E5.BC.80_Num_Lock)
*   [4 图形界面](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2)
    *   [4.1 显示服务](#.E6.98.BE.E7.A4.BA.E6.9C.8D.E5.8A.A1)
    *   [4.2 显卡驱动](#.E6.98.BE.E5.8D.A1.E9.A9.B1.E5.8A.A8)
    *   [4.3 桌面环境](#.E6.A1.8C.E9.9D.A2.E7.8E.AF.E5.A2.83)
    *   [4.4 窗口管理器](#.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [4.5 显示管理器](#.E6.98.BE.E7.A4.BA.E7.AE.A1.E7.90.86.E5.99.A8)
*   [5 电源管理](#.E7.94.B5.E6.BA.90.E7.AE.A1.E7.90.86)
    *   [5.1 ACPI 事件](#ACPI_.E4.BA.8B.E4.BB.B6)
    *   [5.2 CPU 频率调节](#CPU_.E9.A2.91.E7.8E.87.E8.B0.83.E8.8A.82)
    *   [5.3 笔记本电脑](#.E7.AC.94.E8.AE.B0.E6.9C.AC.E7.94.B5.E8.84.91)
    *   [5.4 待机和休眠](#.E5.BE.85.E6.9C.BA.E5.92.8C.E4.BC.91.E7.9C.A0)
*   [6 多媒体](#.E5.A4.9A.E5.AA.92.E4.BD.93)
    *   [6.1 声音](#.E5.A3.B0.E9.9F.B3)
    *   [6.2 浏览器插件](#.E6.B5.8F.E8.A7.88.E5.99.A8.E6.8F.92.E4.BB.B6)
    *   [6.3 解码器](#.E8.A7.A3.E7.A0.81.E5.99.A8)
*   [7 网络](#.E7.BD.91.E7.BB.9C)
    *   [7.1 时钟同步](#.E6.97.B6.E9.92.9F.E5.90.8C.E6.AD.A5)
    *   [7.2 DNS 安全](#DNS_.E5.AE.89.E5.85.A8)
    *   [7.3 DNSSEC 验证](#DNSSEC_.E9.AA.8C.E8.AF.81)
    *   [7.4 配置防火墙](#.E9.85.8D.E7.BD.AE.E9.98.B2.E7.81.AB.E5.A2.99)
    *   [7.5 资源共享](#.E8.B5.84.E6.BA.90.E5.85.B1.E4.BA.AB)
*   [8 输入](#.E8.BE.93.E5.85.A5)
    *   [8.1 键盘布局](#.E9.94.AE.E7.9B.98.E5.B8.83.E5.B1.80)
    *   [8.2 鼠标按键配置](#.E9.BC.A0.E6.A0.87.E6.8C.89.E9.94.AE.E9.85.8D.E7.BD.AE)
    *   [8.3 笔记本触摸板](#.E7.AC.94.E8.AE.B0.E6.9C.AC.E8.A7.A6.E6.91.B8.E6.9D.BF)
    *   [8.4 TrackPoints](#TrackPoints)
*   [9 性能优化](#.E6.80.A7.E8.83.BD.E4.BC.98.E5.8C.96)
    *   [9.1 性能测试](#.E6.80.A7.E8.83.BD.E6.B5.8B.E8.AF.95)
    *   [9.2 性能最大化](#.E6.80.A7.E8.83.BD.E6.9C.80.E5.A4.A7.E5.8C.96)
    *   [9.3 固态硬盘](#.E5.9B.BA.E6.80.81.E7.A1.AC.E7.9B.98)
*   [10 系统服务](#.E7.B3.BB.E7.BB.9F.E6.9C.8D.E5.8A.A1_2)
    *   [10.1 文件索引和搜索](#.E6.96.87.E4.BB.B6.E7.B4.A2.E5.BC.95.E5.92.8C.E6.90.9C.E7.B4.A2)
    *   [10.2 打印](#.E6.89.93.E5.8D.B0)
    *   [10.3 本地邮件交换](#.E6.9C.AC.E5.9C.B0.E9.82.AE.E4.BB.B6.E4.BA.A4.E6.8D.A2)
*   [11 外观美化](#.E5.A4.96.E8.A7.82.E7.BE.8E.E5.8C.96)
    *   [11.1 字体](#.E5.AD.97.E4.BD.93)
    *   [11.2 GTK and Qt themes](#GTK_and_Qt_themes)
*   [12 控制台优化](#.E6.8E.A7.E5.88.B6.E5.8F.B0.E4.BC.98.E5.8C.96)
    *   [12.1 别名](#.E5.88.AB.E5.90.8D)
    *   [12.2 命令别名](#.E5.91.BD.E4.BB.A4.E5.88.AB.E5.90.8D)
    *   [12.3 其它 shells](#.E5.85.B6.E5.AE.83_shells)
    *   [12.4 Bash 增强功能](#Bash_.E5.A2.9E.E5.BC.BA.E5.8A.9F.E8.83.BD)
    *   [12.5 彩色输出](#.E5.BD.A9.E8.89.B2.E8.BE.93.E5.87.BA)
    *   [12.6 压缩文件](#.E5.8E.8B.E7.BC.A9.E6.96.87.E4.BB.B6)
        *   [12.6.1 控制台提示符](#.E6.8E.A7.E5.88.B6.E5.8F.B0.E6.8F.90.E7.A4.BA.E7.AC.A6)
        *   [12.6.2 Emacs shell](#Emacs_shell)
    *   [12.7 鼠标支持](#.E9.BC.A0.E6.A0.87.E6.94.AF.E6.8C.81)
    *   [12.8 页面回滚缓冲](#.E9.A1.B5.E9.9D.A2.E5.9B.9E.E6.BB.9A.E7.BC.93.E5.86.B2)
    *   [12.9 会话管理](#.E4.BC.9A.E8.AF.9D.E7.AE.A1.E7.90.86)
*   [13 系统中文化](#.E7.B3.BB.E7.BB.9F.E4.B8.AD.E6.96.87.E5.8C.96)
*   [14 中国大陆用户的推荐解决方案](#.E4.B8.AD.E5.9B.BD.E5.A4.A7.E9.99.86.E7.94.A8.E6.88.B7.E7.9A.84.E6.8E.A8.E8.8D.90.E8.A7.A3.E5.86.B3.E6.96.B9.E6.A1.88)
    *   [14.1 办公](#.E5.8A.9E.E5.85.AC)
    *   [14.2 中文输入法](#.E4.B8.AD.E6.96.87.E8.BE.93.E5.85.A5.E6.B3.95)
    *   [14.3 在线音乐](#.E5.9C.A8.E7.BA.BF.E9.9F.B3.E4.B9.90)
    *   [14.4 代理](#.E4.BB.A3.E7.90.86)
    *   [14.5 即时通讯工具](#.E5.8D.B3.E6.97.B6.E9.80.9A.E8.AE.AF.E5.B7.A5.E5.85.B7)
    *   [14.6 电子商务](#.E7.94.B5.E5.AD.90.E5.95.86.E5.8A.A1)
    *   [14.7 校园网](#.E6.A0.A1.E5.9B.AD.E7.BD.91)

## 系统管理

这一部分提供系统管理方面的信息。更多内容，参见：[系统管理分类](/index.php/Category:System_administration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:System administration (简体中文)") 和 [System maintenance](/index.php/System_maintenance "System maintenance")。

### 用户和用户组

新安装的系统只有一个超级用户，即 root。使用root进行日常操作是不安全的做法。用户应当[创建](/index.php/User_Management_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "User Management (简体中文)")一个普通用户进行日常操作，而仅仅在管理系统时使用root。也不要在服务器上给 root 开放[SSH](/index.php/SSH "SSH")登录权限。普通用户的创建方法请参阅 [用户和用户组](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Users and groups (简体中文)")。

[用户和用户组](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Users and groups (简体中文)")是GNU/Linux 权限控制机制的基础。管理员通过调整用户组的成员、所有者，可以控制用户使用系统资源。

一个典型的桌面系统普通用户示例；创建一个名为`archie`的用户，并使用[zsh](/index.php/Zsh_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Zsh (简体中文)")作默认shell（在此之前，请不要忘记安装zsh：`pacman -S zsh`）：

```
# useradd -m -g users -G wheel -s /bin/zsh archie

```

并为所创建用户设定密码：

```
# passwd archie

```

### 权限提升

使用 [su](/index.php/Su_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Su (简体中文)") 命令可以方便的切换用户，而[sudo](/index.php/Sudo_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Sudo (简体中文)")命令则是更为简单的选择。

### 系统服务

这一部分涉及[守护进程](/index.php/%E5%AE%88%E6%8A%A4%E8%BF%9B%E7%A8%8B "守护进程")（daemon）。Arch Linux 使用 [systemd (简体中文)](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") 管理系统服务。新用户有必要了解其基本使用方法。通常使用 `# systemctl` 命令进行系统管理，参见[此文](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#systemd_.E5.9F.BA.E6.9C.AC.E5.B7.A5.E5.85.B7 "Systemd (简体中文)").

### 系统维护

Arch 是滚动发行系统，软件包的更新速度很快，用户需要花些时间进行 [系统维护](/index.php/System_maintenance "System maintenance"). [安全](/index.php/Security "Security")页面也给出了很多加强系统安全性的建议和技巧。

## 软件包管理

此部分提供了软件包管理的信息，参见：[Category:Package management (简体中文)](/index.php/Category:Package_management_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Package management (简体中文)")。

**注意:** Arch 的升级有时候需要手动处理。请订阅[arch-announce 邮件列表](https://mailman.archlinux.org/mailman/listinfo/arch-announce/) ，每次升级前查看 [Arch 新闻](https://www.archlinux.org/)或者订阅 [RSS feed](https://www.archlinux.org/feeds/news/)。

### Pacman

Pacman 是 Arch 的软件包管理器。[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 和 [FAQ](/index.php/FAQ_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.AE.A1.E7.90.86 "FAQ (简体中文)") 页面提供了安装、升级和管理软件包的信息。

[Pacman tips (简体中文)](/index.php/Pacman_tips_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman tips (简体中文)")中有很多方便 pacman 使用的技巧。

### 软件仓库镜像

参见[软件仓库镜像](/index.php/Mirrors_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mirrors (简体中文)")一文，获取寻找更快更新pacman镜像的方法。此外，可以查看[镜像状态](https://www.archlinux.org/mirrors/status/)获取最新镜像站点同步信息。

### 软件仓库

[官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库")包含了各个仓库的详细介绍。[非官方软件仓库](/index.php/%E9%9D%9E%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "非官方软件仓库")包含很多个人维护的软件仓库。

如果安装的是 Arch Linux x86_64，并计划使用 32 位程序，建议[启用 [multilib] 仓库](/index.php/Multilib "Multilib")。

### Arch编译系统（ABS）

**Ports**是BSD发行版最初使用的一套系统，它是本地系统中包含各种软件编译脚本的目录树。

[ABS](/index.php/ABS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ABS (简体中文)")系统相当于Arch的Ports，其中提供Arch官方仓库软件包的编译脚本——[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")。编译脚本提供了哈希验证、软件主页、版本、协议、编译步骤等信息。通过[makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)")从编译脚本生成软件包，然后用pacman安装。

实际上，Arch的所有软件包（包括官方库、AUR）都是通过makepkg生成的。

### Arch用户软件源（AUR）

[ABS](/index.php/ABS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ABS (简体中文)")提供了编译官方库软件的脚本，而[AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")则提供了用户提交的、非官方的软件包编译脚本。这是一个基于[web界面](https://aur.archlinux.org/index.php) 或通过[AUR工具](/index.php/AUR_helper_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR helper (简体中文)") 访问的非官方软件仓库。

## 启动

这部分包含系统启动方面的信息。关于Arch开机过程，参见：[Arch 启动过程](/index.php/Arch_boot_process_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch boot process (简体中文)")。更多信息，参见：[启动过程分类](/index.php/Category:Boot_process_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Boot process (简体中文)")。

### 硬件自动探测

默认情况下，[udev](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udev (简体中文)")会在开机时自动探测硬件。禁止加载某些内核模块、手动选择要使用的模块。此外，[Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")也使用udev探测硬件，用户也可以调整这方面配置。

### 微代码

处理器可能有 [错误行为](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly), kernel 可以通过更新启动时的 *微码* 来修正这些错误行为。 Intel 的处理器需要一个单独的包来达到这种效果。 参考 [Microcode](/index.php/Microcode "Microcode") 获取更多细节。

### 保留启动信息

当系统启动完毕，启动信息会被清除并显示登录提示符，使得用户无法获得启动进程的反馈信息，[Disable clearing of boot messages](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages") 教会你如何解决这个问题。

### 开机启动 X

Linux下，一般由[X图形服务器](/index.php/X_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "X (简体中文)")提供图形用户界面。如果想在开机时加载图形用户界面，可以使用[登陆管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")或者[开机时直接启动X](/index.php/Start_X_at_Login_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Start X at Login (简体中文)")。

### 开机时打开 Num Lock

大多数键盘都有一个Num Lock键，通过它控制小键盘的开关。用户可能希望在系统启动时打开Num Lock，参见：[启动时激活 Numlock](/index.php/Activating_Numlock_on_Bootup_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Activating Numlock on Bootup (简体中文)")。

## 图形界面

本部分提供了在系统上安装图形程序，参阅 [Category:X server (简体中文)](/index.php/Category:X_server_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:X server (简体中文)")。

### 显示服务

[X 窗口管理系统](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System")(**X11**或者**X**) 是基于网络的显示协议，提供了窗口功能，包含建立图形用户界面(GUI)的标准工具和协议。[Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")是X窗口系统11版本的开源实现，提供图形用户界面, 安装和配置请阅读[Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")。

[Wayland](/index.php/Wayland_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wayland (简体中文)") 是新的显示服务协议，Weston 是参考实现。目前还处于开发阶段，支持的程序很少。

### 显卡驱动

默认的**vesa**显卡驱动对于大多数显卡都是兼容的，但性能远不如专门的驱动。根据显卡制造商，参见：[ATI (简体中文)](/index.php/ATI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ATI (简体中文)")，[Intel (简体中文)](/index.php/Intel_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Intel (简体中文)")，[NVIDIA (简体中文)](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NVIDIA (简体中文)")。

### 桌面环境

[Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")只提供图形环境的基本框架，完整的用户体验还需要其他组件。 [桌面环境](/index.php/%E6%A1%8C%E9%9D%A2%E7%8E%AF%E5%A2%83 "桌面环境")(DE): 在**X**之上并与其共同运作，提供完整的功能和动态图形界面。桌面环境通常提供图标、小程序（applets）、窗口、工具栏、文件夹、壁纸、应用程序和拖放等功能。使用[GNOME](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)")、[KDE](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)")、[LXDE](/index.php/LXDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXDE (简体中文)")、[Xfce](/index.php/Xfce_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xfce (简体中文)")这类[桌面环境](/index.php/%E6%A1%8C%E9%9D%A2%E7%8E%AF%E5%A2%83 "桌面环境")，是最简单的配置方法. [Category:Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments") 包含了各种桌面环境。

### 窗口管理器

完整的桌面环境提供了完全的用户界面，但是通常会占用不少系统资源。希望系统性能最大化的用户可以只安装[窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")，然后加入需要的其他软件。大部分的桌面环境都可以换用其它的窗口管理器。 [动态](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs"), [堆栈式](/index.php/Category:Stacking_WMs "Category:Stacking WMs") 和 [平铺](/index.php/Category:Tiling_WMs "Category:Tiling WMs") 窗口管理器处理窗口的方式各不相同。

### 显示管理器

除了手动启动 X 的方法外，可以让图形界面自动启动，[显示管理器](/index.php/%E6%98%BE%E7%A4%BA%E7%AE%A1%E7%90%86%E5%99%A8 "显示管理器") 介绍了启动管理器的使用方法。 [Start X at Login](/index.php/Start_X_at_Login_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Start X at Login (简体中文)") 提供了直接从终端启动的轻量方法。

## 电源管理

本章对笔记本用户可能更为有用。更多信息，参见: [Category:Power management (简体中文)](/index.php/Category:Power_management_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Power management (简体中文)")。

### ACPI 事件

电源按键或者合上笔记本会发出 ACPI 事件，可以配置系统在收到这些事件时的相应。推荐的方式是使用 [systemd (简体中文)](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)"), 参阅 [Systemd 电源管理](/index.php/Power_management#Power_management_with_systemd "Power management"). 老的方法是使用 [acpid (简体中文)](/index.php/Acpid_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Acpid (简体中文)")，不推荐使用。.

### CPU 频率调节

最新的CPU通常都有自动调节频率的功能。通过该功能可以有效节约电能、减少发热，提升硬件寿命。[Cpufrequtils (简体中文)](/index.php/Cpufrequtils_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Cpufrequtils (简体中文)")是配置该功能的工具集。

### 笔记本电脑

针对特定型号笔记本电脑的配置信息，参见：[Category:Laptops (简体中文)](/index.php/Category:Laptops_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Laptops (简体中文)")。有关笔记本电脑文章的概览，参见： [Laptop](/index.php/Laptop_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Laptop (简体中文)")。

### 待机和休眠

待机，指系统将当前状态保存于内存中，进入的低能耗状态（保持开机）。休眠，与待机有所不同，是将当前状态保存于硬盘中，然后可以完全断电。参阅[Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate")。

## 多媒体

[Category:Multimedia](/index.php/Category:Multimedia "Category:Multimedia")包含更多多媒体方面的资源

### 声音

内核声卡驱动提供了[声音](/index.php/Sound "Sound")：

*   [ALSA](/index.php/ALSA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ALSA (简体中文)") 是Linux内核组件，推荐使用。只需要解除静音,安装[alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils)软件包，它包含了`alsamixer`)工具，然后按照[此文](/index.php/Advanced_Linux_Sound_Architecture_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.8F.96.E6.B6.88.E9.80.9A.E9.81.93.E9.9D.99.E9.9F.B3 "Advanced Linux Sound Architecture (简体中文)")进行设置即可。
*   如果 Alsa 不能工作，可以试试[OSS](/index.php/OSS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "OSS (简体中文)")。

另外，用户可能希望安装且配置一个 [sound server](/index.php/Sound#Sound_servers "Sound")，例如[PulseAudio](/index.php/PulseAudio "PulseAudio"). 对于高级声音需求, 可浏览 [professional audio](/index.php/Professional_audio "Professional audio").

### 浏览器插件

用户可以安装Adobe Acrobat Reader、Adobe Flash Player，Java之类的[浏览器插件](/index.php/Browser_plugins_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Browser plugins (简体中文)")，以使用更多的富媒体互联网资源。

### 解码器

多媒体应用程序利用[解码器](/index.php/Codecs_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Codecs (简体中文)")编码或解码音频、视频流媒体。要播放多媒体文件，正确安装编码器是必不可少的。

## 网络

本文包含网络方面的配置信息。更多信息参见：[网络](/index.php/Network_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network (简体中文)")，[网络分类](/index.php/Category:Networking_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Networking (简体中文)")。

### 时钟同步

[NTP](/index.php/Network_Time_Protocol_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network Time Protocol (简体中文)")，是最常用的网络同步时间的协议。

### DNS 安全

当在浏览网站，在线支付，连接 [SSH](/index.php/SSH "SSH") 服务 和类似的事情的时候，为了更安全，考虑使用 [DNSSEC](/index.php/DNSSEC "DNSSEC")-enabled 浏览器，它可以验证 [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") 记录的签名, 也可以用 [DNSCrypt](/index.php/DNSCrypt "DNSCrypt") 来加密 DNS 的传输.

### DNSSEC 验证

网络安全方面安全，[SSH](/index.php/SSH_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SSH (简体中文)")提供加密的网络链接。而使用支持[DNSSEC](/index.php/DNSSEC "DNSSEC")的客户端，为提供DNS记录验证，将更进一步加强网络安全。

### 配置防火墙

[防火墙](/index.php/Firewalls "Firewalls")为Linux网络访问提供额外保护。作为[Netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter")计划的一部分，Linux 内核内置了iptables——一种[状态防火墙](https://en.wikipedia.org/wiki/Stateful_firewall "wikipedia:Stateful firewall")（Stateful firewall）。可以通过直接或间接的方式配置它。Arch默认不打开任何端口，因此一般没有必要使用防火墙。

### 资源共享

可以通过 [NFS](/index.php/NFS "NFS") 或 [SSHFS](/index.php/SSHFS "SSHFS") 在网络间共享文件.

用户可以使用[Samba](/index.php/Samba_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Samba (简体中文)")进行 Windows 与 Arch Linux 间的网络传输。

要将 Arch Linux 系统连接到 Active Directory 认证的网络，请阅读文章[Active Directory 整合](/index.php/Active_Directory_Integration "Active Directory Integration").

参阅 [Category:Network sharing](/index.php/Category:Network_sharing "Category:Network sharing").

## 输入

这一部分包含常用的输入设备配置建议。更多信息，参见：[输入设备分类](/index.php/Category:Input_devices_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Input devices (简体中文)").

### 键盘布局

默认配置下，非英语或非标准键盘可能不能正确工作。需要在[`/etc/vconsole.conf`](/index.php/Systemd#Console_and_keymap "Systemd")中设置[按键映射](/index.php/KEYMAP_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KEYMAP (简体中文)")环境变量配置键盘布局。Xorg用户需要做额外的配置，参见：[Xorg#Keyboard layout](/index.php/Xorg#Keyboard_layout "Xorg")。

### 鼠标按键配置

一些高级鼠标可能有许多按键，默认情况下系统并不能正确配置它们。这方面的信息，参见：[Get All Mouse Buttons Working](/index.php/Get_All_Mouse_Buttons_Working "Get All Mouse Buttons Working")。

### 笔记本触摸板

[Synaptics](http://www.synaptics.com/)和[ALPS](http://www.alps.com/)是笔记本常用的两种触摸板。对于Synaptics用户，参见[Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")获取配置信息。

### TrackPoints

见 [TrackPoint](/index.php/TrackPoint "TrackPoint") 文章来配置您的TrackPoint设备。

## 性能优化

这一部分包含一些实用的性能优化技巧。通过使用这些技巧，可以有效提升程序性能。

### 性能测试

[性能测试](/index.php/Benchmarking "Benchmarking")帮助用户评估系统性能，为优化系统性能提供信息。

### 性能最大化

[性能最大化](/index.php/Maximizing_performance_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Maximizing performance (简体中文)")一文提供了提升Arch系统性能的方法。

### 固态硬盘

[固态硬盘](/index.php/%E5%9B%BA%E6%80%81%E7%A1%AC%E7%9B%98 "固态硬盘") 一文包含固态硬盘的各个方面，包括配置和提高寿命。

## 系统服务

### 文件索引和搜索

大部分发行版都提供了 `locate` 命令进行快速文件搜索，在 Arch 中建议安装软件包 [mlocate](https://www.archlinux.org/packages/?name=mlocate)。安装后请执行`updatedb`建立文件系统索引。

### 打印

[CUPS](/index.php/CUPS "CUPS")是苹果公司开发的、符合标准的开源打印系统。特定型号打印机的配置信息，参见：[打印机分类](/index.php/Category:Printers_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Printers (简体中文)")。

### 本地邮件交换

参见[使用Postfix进行本地邮件交换](/index.php/Local_Mail_Delivery_with_Postfix "Local Mail Delivery with Postfix")简单配置邮件交换。此外，用户还可以选择：[SSMTP](/index.php/SSMTP "SSMTP")，[Msmtp](/index.php/Msmtp "Msmtp")和[fdm](/index.php/Fdm "Fdm")。

## 外观美化

本栏讨论ArchLinux界面的美化。更多信息请参考：[Category:Eye candy (简体中文)](/index.php/Category:Eye_candy_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Eye candy (简体中文)")。

### 字体

在安装桌面环境/窗口管理器**之前**，也许你会先安装些美观的字体。Dejavu 是不错的字体集。英文字体优先选择dejavu字体

```
# pacman -S ttf-dejavu

```

对于中文字体，开源的文泉驿正黑矢量字体是不错的选择，它还内嵌了9pt-12pt的点阵宋体：

 `# pacman -S wqy-zenhei` 

当然现在流行的是安装1个字体:

 `# pacman -S wqy-microhei` 

可能有人需要安装微软视窗下的字体，如下安装之: [ttf-win7-fonts](https://aur.archlinux.org/packages/ttf-win7-fonts/), [ttf-office-2007-fonts](https://aur.archlinux.org/packages/ttf-office-2007-fonts/)

请访问 [字体配置](/index.php/Font_configuration "Font configuration") 获取配置字体渲染的详细信息，[Fonts (简体中文)](/index.php/Fonts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fonts (简体中文)") 提供了字体选择建议和安装方法。

对于经常使用虚拟终端的用户，可以通过配置字体提高可读性，参见：[Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts")。

### GTK and Qt themes

Linux 下的图形界面基本都使用 [GTK+](/index.php/GTK%2B "GTK+") 或者 [Qt](/index.php/Qt "Qt") 工具集。这些文章和 [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") 提供了让程序更美观的方法。

## 控制台优化

本部分保护控制台的优化和微调方法。参阅 [Category:Command shells](/index.php/Category:Command_shells "Category:Command shells").

### 别名

给一个命令取别名, or a group thereof, 是使用控制台时的一种节省时间的方式。这种方式对于重复的任务特别有用，这些任务的参数在多次执行期间不需要大的改变。通常使用的省时的别名可以在这里找到 [Bash#Aliases](/index.php/Bash#Aliases "Bash")， 这些别名也能很容易地移植到 [zsh](/index.php/Zsh "Zsh") 。

### 命令别名

用户可以[自定义常用命令的别名](/index.php/Core_utilities#alias "Core utilities")，以方便使用。

### 其它 shells

[Bash](/index.php/Bash "Bash") 是 Arch 默认按照的 shell，而安装的时候使用的是 [zsh](/index.php/Zsh "Zsh") 并使用 [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config) 插件。其它选择参阅 [Command shell#List of shells](/index.php/Command_shell#List_of_shells "Command shell")。

### Bash 增强功能

[Bash#Tips and tricks](/index.php/Bash#Tips_and_tricks "Bash")介绍了些Bash的杂项设置，包括：命令补全，历史记录，宏等等。

### 彩色输出

参考 [Color output in console](/index.php/Color_output_in_console "Color output in console")。

### 压缩文件

压缩包，或归档，在GNU/Linux十分常用。[Tar](/index.php/Tar "Tar")是最常用的归档工具，此外还有Arch软件包使用的xz压缩包。参见：[Core utilities#extract](/index.php/Core_utilities#extract "Core utilities")。

#### 控制台提示符

控制台提示符可以通过PS1环境变量灵活定制，参见论坛帖子：[What's your PS1?](https://bbs.archlinux.org/viewtopic.php?id=50885)。另见：[Bash彩色提示符](/index.php/Color_Bash_Prompt "Color Bash Prompt")（Zsh用户参见：[Zsh：提示符](/index.php/Zsh#Prompts "Zsh")）。

#### Emacs shell

Emacs除了用作编辑器，其高级功能更为出名，其中一项就是把Emacs变成全功能shell。参见：[Emacs打开彩色输出后的乱码问题](/index.php/Emacs#Colored_output_issues "Emacs")。

### 鼠标支持

在控制台中，使用鼠标复制粘贴比传统 GNU [screen](/index.php/Screen "Screen") 操作方式方便许多。参见：[Console mouse support](/index.php/Console_mouse_support "Console mouse support")。

### 页面回滚缓冲

通过设置[页面回滚缓冲](/index.php/Scrollback_buffer "Scrollback buffer")节省显示空间。

### 会话管理

[tmux](/index.php/Tmux "Tmux")或[screen](/index.php/Screen "Screen")之类的终端复用器提供会话管理，在其中运行的程序不会因杀死终端、关闭X或用户登出而终止，只要终端复用器服务保持运行。随后，用户可以重新连接会话。

## 系统中文化

[Arch Linux 中文化](/index.php/Arch_Linux_%E4%B8%AD%E6%96%87%E5%8C%96 "Arch Linux 中文化") 页面包含了详尽的中文化指南。

## 中国大陆用户的推荐解决方案

**注意:** 本章节独立于原英文翻译。

众所周知，中国大陆用户有别于国际上的特殊需求，此章节旨在提供解决方案。

### 办公

[WPS Office (简体中文)](/index.php/WPS_Office_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "WPS Office (简体中文)")

[LibreOffice (简体中文)](/index.php/LibreOffice_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LibreOffice (简体中文)")

一些在线办公套件网站可以提供基础的办公功能:

[Office Online](https://en.wikipedia.org/wiki/Office_Online "wikipedia:Office Online"): Microsoft提供的Office办公套件的网页版

[Google Docs, Sheets and Slides](https://en.wikipedia.org/wiki/Google_Docs,_Sheets_and_Slides "wikipedia:Google Docs, Sheets and Slides"): Google提供的在线文字处理、电子制表和演示程序。

### 中文输入法

参见 [Fcitx (简体中文)](/index.php/Fcitx_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fcitx (简体中文)")或[Ibus](/index.php/IBus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "IBus (简体中文)")。

### 在线音乐

*   网易云音乐[netease-cloud-music](https://aur.archlinux.org/packages/netease-cloud-music/)。
*   酷我音乐（第三方）[kwplayer](https://aur.archlinux.org/packages/kwplayer/)。

### 代理

即科学上网。

*   [Shadowsocks (简体中文)](/index.php/Shadowsocks_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Shadowsocks (简体中文)")
*   Lantern（蓝灯）：安装[lantern](https://aur.archlinux.org/packages/lantern/)（如安装有archlinuxcn源可直接使用`pacman -S lantern`安装）即可。
*   [XX-Net (简体中文)](/index.php/XX-Net_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "XX-Net (简体中文)")
*   更改hosts： 获取可以科学上网的hosts文件，修改或替换`/etc/hosts`即可。

示例：从[[1]](https://github.com/googlehosts/hosts)项目获取[hosts](https://raw.githubusercontent.com/googlehosts/hosts/master/hosts-files/hosts)文件，将其内容加入`/etc/hosts`（如原hosts文件无需使用，也可直接覆盖）即可。也可执行更新hosts文件：

 `sudo wget [https://raw.githubusercontent.com/googlehosts/hosts/master/hosts-files/hosts](https://raw.githubusercontent.com/googlehosts/hosts/master/hosts-files/hosts) -O /etc/hosts` 

为方便起见，可将其使用alias别名方式写入.bashrc，首先编辑~/.bashrc，在其中添加：

```
alias hosts='sudo wget [https://raw.githubusercontent.com/googlehosts/hosts/master/hosts-files/hosts](https://raw.githubusercontent.com/googlehosts/hosts/master/hosts-files/hosts) -O /etc/hosts'

```

然后执行:

 `source ~/.bashrc` 

以后更新hosts文件只需要执行

 `hosts` 

即可。

**提示：** 可以使用 [crontab](/index.php/Crontab "Crontab") 定时执行脚本 (root 身份运行或 sudo 免密码)

**提示：** 除hosts方法外，你可能还需要进行相应的代理设置，如对程序单独设置代理或者使用工具设置临时代理（如使用[proxchains](https://www.archlinux.org/packages/?name=proxchains)工具，配置好代理和proxychains的配置文件后，使用`proxchians 程序名`使该程序从代理进行联网）或者全局代理（如桌面环境的设置中可能提供该选项），可参考各工具的相应文档进行设置，或者参考[Proxy_settings](/index.php/Proxy_settings "Proxy settings")一文。

### 即时通讯工具

*   QQ:请查阅 [Tencent QQ (简体中文)](/index.php/Tencent_QQ_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Tencent QQ (简体中文)") 页面。
*   Telegram:Telegram Messenger是一个跨平台的实时通信软件。请查阅 [Telegram (简体中文)](/index.php/Telegram_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Telegram (简体中文)") 页面。

### 电子商务

很可惜并没有现成的维基页面，不过 [Acgtyrant](/index.php/User:Acgtyrant "User:Acgtyrant") 用户在其博客上提供了 [電子商務在 Arch Linux 下的簡易解決方案](http://arch.acgtyrant.com/2014/02/20/e-commerce/) 。

### 校园网

中国大陆众多高校采用各种客户端拨号上网，如城市热点drcom，锐捷。一些学校提供有网页登录或者linux版客户端，可参照相关说明文档安装使用。 ~未提供网页登录以及客户端者

* * *

尝试寻找第三方客户端使用（解决成功率不高），如[drcom](https://github.com/searchtf8=✓&q=drcom&type=Repositories&ref=searchresults)，锐捷用户可参照[MentoHUST (简体中文)](/index.php/MentoHUST_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "MentoHUST (简体中文)") 指导您通过借助 MentoHUST 进行锐捷拨号。

* * *

借助[wine](/index.php/Wine_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wine (简体中文)")尝试安装使用。

* * *

使用虚拟机运行，可在虚拟机中登录客户端上网，虚拟机开启桥接，安装ssh服务端，在linux下ssh登录虚拟机上网。