相关文章

*   [常见问题](/index.php/FAQ_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "FAQ (简体中文)")
*   [安装指南](/index.php/Installation_Guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installation Guide (简体中文)")
*   [软件列表](/index.php/List_of_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of applications (简体中文)")

**翻译状态：** 本文是英文页面 [General recommendations](/index.php/General_recommendations "General recommendations") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-11-23，点击[这里](https://wiki.archlinux.org/index.php?title=General+recommendations&diff=0&oldid=549342)可以查看翻译后英文页面的改动。

本文是各种重要或常用的文章的详细索引。阅读本文前，读者应该先通过 [官方安装指南](/index.php/%E5%AE%98%E6%96%B9%E5%AE%89%E8%A3%85%E6%8C%87%E5%8D%97 "官方安装指南") 安装 Arch Linux 基本系统。然后理解系统管理和软件包管理中解释的概念，再阅读 wiki 中的其它文章。

**注意:** 中国用户可以特别留意 [#中国大陆用户的推荐解决方案](#中国大陆用户的推荐解决方案) 内容。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 系统管理](#系统管理)
    *   [1.1 用户和用户组](#用户和用户组)
    *   [1.2 权限提升](#权限提升)
    *   [1.3 服务管理](#服务管理)
    *   [1.4 系统维护](#系统维护)
*   [2 软件包管理](#软件包管理)
    *   [2.1 Pacman](#Pacman)
    *   [2.2 软件仓库](#软件仓库)
    *   [2.3 软件仓库镜像](#软件仓库镜像)
    *   [2.4 Arch编译系统（ABS）](#Arch编译系统（ABS）)
    *   [2.5 Arch用户软件源（AUR）](#Arch用户软件源（AUR）)
*   [3 启动](#启动)
    *   [3.1 硬件自动探测](#硬件自动探测)
    *   [3.2 Microcode](#Microcode)
    *   [3.3 保留启动信息](#保留启动信息)
    *   [3.4 开机时打开 Num Lock](#开机时打开_Num_Lock)
*   [4 图形界面](#图形界面)
    *   [4.1 显示服务](#显示服务)
    *   [4.2 显卡驱动](#显卡驱动)
    *   [4.3 桌面环境](#桌面环境)
    *   [4.4 窗口管理器](#窗口管理器)
    *   [4.5 显示管理器](#显示管理器)
*   [5 电源管理](#电源管理)
    *   [5.1 ACPI 事件](#ACPI_事件)
    *   [5.2 CPU 频率调节](#CPU_频率调节)
    *   [5.3 笔记本电脑](#笔记本电脑)
    *   [5.4 待机和休眠](#待机和休眠)
*   [6 多媒体](#多媒体)
    *   [6.1 声音](#声音)
    *   [6.2 浏览器插件](#浏览器插件)
    *   [6.3 解码器](#解码器)
*   [7 网络](#网络)
    *   [7.1 时钟同步](#时钟同步)
    *   [7.2 DNS 安全](#DNS_安全)
    *   [7.3 DNSSEC 验证](#DNSSEC_验证)
    *   [7.4 配置防火墙](#配置防火墙)
    *   [7.5 资源共享](#资源共享)
*   [8 输入](#输入)
    *   [8.1 键盘布局](#键盘布局)
    *   [8.2 鼠标按键配置](#鼠标按键配置)
    *   [8.3 笔记本触摸板](#笔记本触摸板)
    *   [8.4 TrackPoints](#TrackPoints)
*   [9 性能优化](#性能优化)
    *   [9.1 性能测试](#性能测试)
    *   [9.2 性能最大化](#性能最大化)
    *   [9.3 固态硬盘](#固态硬盘)
*   [10 系统服务](#系统服务)
    *   [10.1 文件索引和搜索](#文件索引和搜索)
    *   [10.2 打印](#打印)
    *   [10.3 本地邮件交换](#本地邮件交换)
*   [11 外观美化](#外观美化)
    *   [11.1 字体](#字体)
    *   [11.2 GTK 和 Qt 主题](#GTK_和_Qt_主题)
*   [12 控制台优化](#控制台优化)
    *   [12.1 Tab 自动补全](#Tab_自动补全)
    *   [12.2 别名](#别名)
    *   [12.3 命令别名](#命令别名)
    *   [12.4 其它 shells](#其它_shells)
    *   [12.5 Bash 增强功能](#Bash_增强功能)
    *   [12.6 彩色输出](#彩色输出)
    *   [12.7 压缩文件](#压缩文件)
        *   [12.7.1 控制台提示符](#控制台提示符)
        *   [12.7.2 Emacs shell](#Emacs_shell)
    *   [12.8 鼠标支持](#鼠标支持)
    *   [12.9 页面回滚缓冲](#页面回滚缓冲)
    *   [12.10 会话管理](#会话管理)
*   [13 系统中文化](#系统中文化)
*   [14 中国大陆用户的推荐解决方案](#中国大陆用户的推荐解决方案)
    *   [14.1 办公](#办公)
    *   [14.2 中文输入法](#中文输入法)
    *   [14.3 在线音乐](#在线音乐)
    *   [14.4 代理](#代理)
    *   [14.5 即时通讯工具](#即时通讯工具)
    *   [14.6 电子商务](#电子商务)
    *   [14.7 校园网](#校园网)

## 系统管理

这一部分提供系统管理方面的信息。更多内容，参见：[系统管理分类](/index.php/Category:System_administration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:System administration (简体中文)")。

### 用户和用户组

新安装的系统只有一个[超级用户](https://en.wikipedia.org/wiki/Superuser "wikipedia:Superuser")，即 root。使用 root 进行日常操作是不安全的。应当[创建](/index.php/User_Management_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "User Management (简体中文)")普通用户进行日常操作，仅在管理系统时使用 root。不要在服务器上给 root 开放[SSH](/index.php/SSH "SSH")登录权限。普通用户的创建方法请参阅 [用户和用户组](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Users and groups (简体中文)")。

[用户和用户组](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Users and groups (简体中文)")是GNU/Linux 权限控制机制的基础。管理员通过调整用户组的成员、所有者，可以控制用户使用系统资源。

### 权限提升

使用 [su](/index.php/Su_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Su (简体中文)") 命令可以方便的切换用户，而[sudo](/index.php/Sudo_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Sudo (简体中文)")命令则是更为简单的选择。默认配置时，*su* 将改用 root 用户登录 shell，而 *sudo* 会给单个命令临时的超级用户权限。

### 服务管理

Arch Linux 使用 [systemd (简体中文)](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") 管理系统服务。新用户有必要了解其基本使用方法。通常使用 `# systemctl` 命令进行系统管理，参见[此文](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#systemd_基本工具 "Systemd (简体中文)").

### 系统维护

Arch 是滚动发行系统，软件包的更新速度很快，用户需要花些时间进行 [系统维护](/index.php/System_maintenance "System maintenance"). [安全](/index.php/Security "Security")页面也给出了很多加强系统安全性的建议和技巧。

## 软件包管理

此部分提供了软件包管理的信息，参见：[FAQ#Package management](/index.php/FAQ#Package_management "FAQ") 和 [Category:Package management (简体中文)](/index.php/Category:Package_management_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Package management (简体中文)")。

**注意:** Arch 的升级有时候需要手动处理。请订阅[arch-announce 邮件列表](https://mailman.archlinux.org/mailman/listinfo/arch-announce/) ，每次升级前查看 [Arch 新闻](https://www.archlinux.org/)或者订阅 [RSS feed](https://www.archlinux.org/feeds/news/)。

### Pacman

Pacman 是 Arch 的软件包管理器。[pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 和 [FAQ](/index.php/FAQ_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#软件包管理 "FAQ (简体中文)") 页面提供了安装、升级和管理软件包的信息。

[Pacman tips (简体中文)](/index.php/Pacman_tips_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman tips (简体中文)")中有很多方便 pacman 使用的技巧。

### 软件仓库

[官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库")包含了各个仓库的详细介绍。[非官方软件仓库](/index.php/%E9%9D%9E%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "非官方软件仓库")包含很多个人维护的软件仓库。

如果计划使用 32 位程序，建议启用 [multilib](/index.php/Multilib "Multilib") 仓库。

安装 [pkgstats](/index.php/Pkgstats "Pkgstats")，可以让软件开发人员统计软件包的使用情况。

### 软件仓库镜像

参见[软件仓库镜像](/index.php/Mirrors_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mirrors (简体中文)")一文，获取寻找更快更新pacman镜像的方法。此外，可以查看[镜像状态](https://www.archlinux.org/mirrors/status/)获取最新镜像站点同步信息。

### Arch编译系统（ABS）

**Ports**是 BSD 发行版最初使用的一套系统，它是本地系统中包含各种软件编译脚本的目录树。

[ABS](/index.php/ABS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ABS (简体中文)")系统相当于 Arch 的 Ports，包含 Arch 官方软件包的编译脚本——[PKGBUILD](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")。编译脚本提供了哈希验证、软件主页、版本、协议、编译步骤等信息。通过 [makepkg](/index.php/Makepkg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Makepkg (简体中文)") 从编译脚本生成软件包，然后用 pacman 安装。

实际上，Arch 的所有软件包（包括官方库、AUR）都是通过 makepkg 生成的。

### Arch用户软件源（AUR）

Arch 编译系统提供了编译官方库软件的脚本，而 [AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 则提供了用户提交的、非官方的软件包编译脚本。这是一个基于 [web 界面](https://aur.archlinux.org/index.php)或通过 [AUR 工具](/index.php/AUR_helper_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR helper (简体中文)")访问的非官方软件仓库。

## 启动

这部分包含系统启动方面的信息。关于Arch开机过程，参见：[Arch 启动过程](/index.php/Arch_boot_process_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch boot process (简体中文)")。更多信息，参见：[启动过程分类](/index.php/Category:Boot_process_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Boot process (简体中文)")。

### 硬件自动探测

默认情况下，[udev](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udev (简体中文)")会在开机时自动探测硬件。禁止加载某些内核模块、手动选择要使用的模块。此外，[Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)") 也使用 udev 探测硬件，用户也可以调整这方面配置。

### Microcode

处理器可能有 [错误行为](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly), kernel 可以通过更新启动时的 *Microcode* 来修正这些错误行为。参考 [Microcode](/index.php/Microcode "Microcode") 获取更多细节。

### 保留启动信息

当系统启动完毕，启动信息会被清除并显示登录提示符，使得用户无法获得启动进程的反馈信息，[Disable clearing of boot messages](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages") 可以解决这个问题。

### 开机时打开 Num Lock

大多数键盘都有一个Num Lock键，通过它控制小键盘的开关。用户可能希望在系统启动时打开Num Lock，参见：[启动时激活 Numlock](/index.php/Activating_Numlock_on_Bootup_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Activating Numlock on Bootup (简体中文)")。

## 图形界面

本部分提供了在系统上安装图形程序，参阅 [Category:X server (简体中文)](/index.php/Category:X_server_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:X server (简体中文)")。

### 显示服务

[X 窗口管理系统](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System")(**X11**或者**X**) 是基于网络的显示协议，提供了窗口功能，包含建立图形用户界面(GUI)的标准工具和协议。[Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")是X窗口系统11版本的开源实现，提供图形用户界面, 安装和配置请阅读[Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")。

[Wayland](/index.php/Wayland_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wayland (简体中文)") 是新的显示服务协议，Weston 是参考实现。目前还处于开发阶段，支持的程序很少。

### 显卡驱动

默认的**vesa**显卡驱动对于大多数显卡都是兼容的，但是通过为ATI ， Intel或NVIDIA产品安装适当的驱动程序，可以明显地改善性能并利用附加功能。根据显卡制造商，分别参见：[ATI (简体中文)](/index.php/ATI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ATI (简体中文)")，[Intel (简体中文)](/index.php/Intel_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Intel (简体中文)")，[NVIDIA (简体中文)](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NVIDIA (简体中文)")。

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

*   [ALSA](/index.php/ALSA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ALSA (简体中文)") 是Linux内核组件，推荐使用。只需要解除静音,安装[alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils)软件包，它包含了`alsamixer`)工具，然后按照[此文](/index.php/Advanced_Linux_Sound_Architecture_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#取消通道静音 "Advanced Linux Sound Architecture (简体中文)")进行设置即可。
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

[防火墙](/index.php/Firewalls "Firewalls")为Linux网络访问提供额外保护。作为[Netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter")计划的一部分，Linux 内核内置了iptables——一种[状态防火墙](https://en.wikipedia.org/wiki/Stateful_firewall "wikipedia:Stateful firewall")（Stateful firewall）。可以通过直接或间接的方式配置它。非常推荐建立一个防火墙，参考[防火墙](/index.php/Firewalls "Firewalls")。

### 资源共享

可以通过 [NFS](/index.php/NFS "NFS") 或 [SSHFS](/index.php/SSHFS "SSHFS") 在网络间共享文件.

用户可以使用[Samba](/index.php/Samba_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Samba (简体中文)")进行 Windows 与 Arch Linux 间的网络传输。

要将 Arch Linux 系统连接到 Active Directory 认证的网络，请阅读文章[Active Directory 整合](/index.php/Active_Directory_integration "Active Directory integration").

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

### GTK 和 Qt 主题

Linux 下的图形界面基本都使用 [GTK+](/index.php/GTK%2B "GTK+") 或者 [Qt](/index.php/Qt "Qt") 工具集。这些文章和 [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") 提供了让程序更美观的方法。

## 控制台优化

本部分包括控制台的优化和微调方法。参阅 [Category:Command shells](/index.php/Category:Command_shells "Category:Command shells").

### Tab 自动补全

建议参考所选 shell 的文档，立即设置增强的 [Tab 自动补全](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion")。

### 别名

给一个命令取别名, or a group thereof, 是使用控制台时的一种节省时间的方式。这种方式对于重复的任务特别有用，这些任务的参数在多次执行期间不需要大的改变。通常使用的省时的别名可以在这里找到 [Bash#Aliases](/index.php/Bash#Aliases "Bash")， 这些别名也能很容易地移植到 [zsh](/index.php/Zsh "Zsh") 。

### 命令别名

用户可以[自定义常用命令的别名](/index.php/Core_utilities#alias "Core utilities")，以方便使用。

### 其它 shells

[Bash](/index.php/Bash "Bash") 是 Arch 默认安装的 shell，而安装的时候使用的是 [zsh](/index.php/Zsh "Zsh") 并使用 [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config) 插件。其它选择参阅 [Command shell#List of shells](/index.php/Command_shell#List_of_shells "Command shell")。

### Bash 增强功能

[Bash#Tips and tricks](/index.php/Bash#Tips_and_tricks "Bash")介绍了些Bash的杂项设置，包括：命令补全，历史记录，宏等等。

### 彩色输出

参考 [Color output in console](/index.php/Color_output_in_console "Color output in console")。

### 压缩文件

压缩包，或称为归档，在GNU/Linux十分常用。[Tar](/index.php/Tar "Tar")是最常用的归档工具，用户应该熟悉它的语法。此外还有Arch软件包使用的xz压缩包。参见：[Core utilities#extract](/index.php/Core_utilities#extract "Core utilities")。

#### 控制台提示符

控制台提示符可以通过PS1环境变量灵活定制，参见论坛帖子：[What's your PS1?](https://bbs.archlinux.org/viewtopic.php?id=50885)。另见：[Bash彩色提示符](/index.php/Color_Bash_Prompt "Color Bash Prompt")（Zsh用户参见：[Zsh：提示符](/index.php/Zsh#Prompts "Zsh")）。

#### Emacs shell

Emacs除了用作编辑器，其高级功能更为出名，其中一项就是把Emacs变成全功能shell。参见：[Emacs打开彩色输出后的乱码问题](/index.php/Emacs#Colored_output_issues "Emacs")。

### 鼠标支持

在控制台中，使用鼠标复制粘贴比传统 [GNU screen](/index.php?title=GNU_screen&action=edit&redlink=1 "GNU screen (page does not exist)") 操作方式方便许多。参见：[Console mouse support](/index.php/Console_mouse_support "Console mouse support")。

### 页面回滚缓冲

通过设置[页面回滚缓冲](/index.php/Scrollback_buffer "Scrollback buffer")节省显示空间。

### 会话管理

[tmux](/index.php/Tmux "Tmux")或[GNU screen](/index.php?title=GNU_screen&action=edit&redlink=1 "GNU screen (page does not exist)")之类的终端复用器提供会话管理，在其中运行的程序不会因杀死终端、关闭X或用户登出而终止，只要终端复用器服务保持运行。随后，用户可以重新连接会话。

## 系统中文化

[Arch Linux 中文化](/index.php/Arch_Linux_%E4%B8%AD%E6%96%87%E5%8C%96 "Arch Linux 中文化") 页面包含了详尽的中文化指南。

## 中国大陆用户的推荐解决方案

**注意:** 本章节独立于原英文翻译。

众所周知，中国大陆用户有别于国际上的特殊需求，此章节旨在提供解决方案。

### 办公

*   [WPS Office (简体中文)](/index.php/WPS_Office_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "WPS Office (简体中文)")
*   [LibreOffice (简体中文)](/index.php/LibreOffice_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LibreOffice (简体中文)")

一些在线办公套件网站可以提供基础的办公功能:

*   [Office Online](https://en.wikipedia.org/wiki/Office_Online "wikipedia:Office Online"): Microsoft提供的Office办公套件的网页版
*   [Google Docs, Sheets and Slides](https://en.wikipedia.org/wiki/Google_Docs,_Sheets_and_Slides "wikipedia:Google Docs, Sheets and Slides"): Google提供的在线文字处理、电子制表和演示程序。

### 中文输入法

参见 [Fcitx (简体中文)](/index.php/Fcitx_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fcitx (简体中文)")或[Ibus](/index.php/IBus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "IBus (简体中文)")。

### 在线音乐

*   网易云音乐[netease-cloud-music](https://aur.archlinux.org/packages/netease-cloud-music/)。
*   酷我音乐（第三方）[kwplayer](https://aur.archlinux.org/packages/kwplayer/)。

### 代理

即科学上网。

*   [Shadowsocks (简体中文)](/index.php/Shadowsocks_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Shadowsocks (简体中文)")
*   Lantern（蓝灯）：安装[lantern](https://aur.archlinux.org/packages/lantern/)（如安装有archlinuxcn源可直接使用`pacman -S lantern-bin`安装）即可。
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

**提示：** 除hosts方法外，你可能还需要进行相应的代理设置，如对程序单独设置代理或者使用工具设置临时代理（如使用[proxychains](https://www.archlinux.org/packages/?name=proxychains)工具，配置好代理和proxychains的配置文件后，使用`proxchians 程序名`使该程序从代理进行联网）或者全局代理（如桌面环境的设置中可能提供该选项），可参考各工具的相应文档进行设置，或者参考[Proxy settings](/index.php/Proxy_settings "Proxy settings")一文。

### 即时通讯工具

*   QQ:请查阅 [Tencent QQ (简体中文)](/index.php/Tencent_QQ_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Tencent QQ (简体中文)") 页面。
*   Telegram:Telegram Messenger是一个跨平台的实时通信软件。请查阅 [Telegram (简体中文)](/index.php/Telegram_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Telegram (简体中文)") 页面。

### 电子商务

很可惜并没有现成的维基页面，不过 [Acgtyrant](/index.php/User:Acgtyrant "User:Acgtyrant") 用户在其博客上提供了 [電子商務在 Arch Linux 下的簡易解決方案](http://arch.acgtyrant.com/2014/02/20/e-commerce/)([archive.org的存档](https://web.archive.org/web/20150706100009/http://arch.acgtyrant.com/2014/02/20/e-commerce/))。

### 校园网

中国大陆众多高校采用各种客户端拨号上网，如城市热点drcom，锐捷。一些学校提供有网页登录或者linux版客户端，可参照相关说明文档安装使用。对于未提供网页登录以及客户端者：

*   Drcom用户可参考[Drcom](/index.php/Drcom_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Drcom (简体中文)")，锐捷用户可参照[MentoHUST (简体中文)](/index.php/MentoHUST_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "MentoHUST (简体中文)") 指导您通过借助 MentoHUST 进行锐捷拨号。
*   借助[wine](/index.php/Wine_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Wine (简体中文)")尝试安装使用。
*   使用虚拟机运行，可在虚拟机中登录客户端上网，虚拟机开启桥接，安装ssh服务端，在linux下ssh登录虚拟机上网。