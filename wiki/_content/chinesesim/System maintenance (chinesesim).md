**翻译状态：** 本文是英文页面 [Arch_Linux_System_Maintenance](/index.php/Arch_Linux_System_Maintenance "Arch Linux System Maintenance") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-11-10，点击[这里](https://wiki.archlinux.org/index.php?title=Arch_Linux_System_Maintenance&diff=0&oldid=408000)可以查看翻译后英文页面的改动。

Regular system maintenance is necessary for the proper function of Arch over a period of time. Timely-maintenance is a practice many users get accustomed to.

## Contents

*   [1 Check for errors](#Check_for_errors)
    *   [1.1 Failed systemd services](#Failed_systemd_services)
    *   [1.2 Logfiles](#Logfiles)
*   [2 Backup](#Backup)
    *   [2.1 Configuration files](#Configuration_files)
    *   [2.2 Important data](#Important_data)
    *   [2.3 List of installed packages](#List_of_installed_packages)
    *   [2.4 Pacman database](#Pacman_database)
*   [3 Upgrading the system](#Upgrading_the_system)
    *   [3.1 Avoid certain pacman commands](#Avoid_certain_pacman_commands)
    *   [3.2 不支持部分升级](#.E4.B8.8D.E6.94.AF.E6.8C.81.E9.83.A8.E5.88.86.E5.8D.87.E7.BA.A7)
    *   [3.3 Read before upgrading the system](#Read_before_upgrading_the_system)
    *   [3.4 Act on alerts during an upgrade](#Act_on_alerts_during_an_upgrade)
    *   [3.5 Deal promptly with new configuration files](#Deal_promptly_with_new_configuration_files)
    *   [3.6 Revert broken updates](#Revert_broken_updates)
    *   [3.7 使用包管理器安装软件](#.E4.BD.BF.E7.94.A8.E5.8C.85.E7.AE.A1.E7.90.86.E5.99.A8.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6)
    *   [3.8 选择开源驱动](#.E9.80.89.E6.8B.A9.E5.BC.80.E6.BA.90.E9.A9.B1.E5.8A.A8)
    *   [3.9 谨慎使用非官方或测试不足的软件包](#.E8.B0.A8.E6.85.8E.E4.BD.BF.E7.94.A8.E9.9D.9E.E5.AE.98.E6.96.B9.E6.88.96.E6.B5.8B.E8.AF.95.E4.B8.8D.E8.B6.B3.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [3.10 Update the mirrorlist](#Update_the_mirrorlist)
*   [4 Clean the filesystem](#Clean_the_filesystem)
    *   [4.1 Old configuration files](#Old_configuration_files)
    *   [4.2 Unused packages](#Unused_packages)
    *   [4.3 Package cache](#Package_cache)
    *   [4.4 Broken symlinks](#Broken_symlinks)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 使用经过验证的软件包](#.E4.BD.BF.E7.94.A8.E7.BB.8F.E8.BF.87.E9.AA.8C.E8.AF.81.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [5.2 安装内核的长期支持版本](#.E5.AE.89.E8.A3.85.E5.86.85.E6.A0.B8.E7.9A.84.E9.95.BF.E6.9C.9F.E6.94.AF.E6.8C.81.E7.89.88.E6.9C.AC)

## Check for errors

### Failed systemd services

Check if any systemd services have entered in a failed state:

```
$ systemctl --failed

```

See [Systemd#Analyzing the system state](/index.php/Systemd#Analyzing_the_system_state "Systemd") for more information.

### Logfiles

Look for errors in the log files located at `/var/log`, as well as high priority errors in the systemd journal:

```
# journalctl -p 0..3 -xn

```

See [Systemd#Journal](/index.php/Systemd#Journal "Systemd") for more information.

## Backup

Backups may be automated with [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers").

### Configuration files

Before editing any configuration files, create a backup. This way, you can revert to a working version in case of problems. Editors like [vim](/index.php/Vim "Vim") and [emacs](/index.php/Emacs "Emacs") can do this automatically, as well as tools like [etckeeper](/index.php/Etckeeper "Etckeeper") which keep `/etc` in a version control system (VCS).

### Important data

Create backups of important data at regular intervals. Directories to consider are `/etc`, `/home` and `/var`, and, for server installations, also `/srv`.

See [Backup programs](/index.php/Backup_programs "Backup programs") for many alternative applications that may better suit your case. See [Category:System recovery](/index.php/Category:System_recovery "Category:System recovery") for other articles of interest.

### List of installed packages

Maintain a list of all installed packages, so that if a complete re-installation is inevitable, it is easier to re-create the original environment.

See [Pacman tips#Backing up and retrieving a list of installed packages](/index.php/Pacman_tips#Backing_up_and_retrieving_a_list_of_installed_packages "Pacman tips") for details.

### Pacman database

See [Pacman tips#Back-up the pacman database](/index.php/Pacman_tips#Back-up_the_pacman_database "Pacman tips").

## Upgrading the system

It is recommended to perform full system upgrades regularly, to enjoy both the latest bug fixes and security updates, and also to avoid having to deal with too many package upgrades that require manual intervention at once. See [Pacman#Upgrading packages](/index.php/Pacman#Upgrading_packages "Pacman") for details.

Make sure to have the Arch install media or another Linux "live" CD/USB available so you can easily rescue your system if there is a problem after updating. If you are running Arch in a production environment, or cannot afford downtime for any reason, test changes to configuration files, as well as updates to software packages, on a non-critical duplicate system first. Then, if no problems arise, roll out the changes to the production system.

If the system has packages from the [AUR](/index.php/AUR "AUR"), carefully upgrade all of them.

### Avoid certain pacman commands

Avoid doing [partial upgrades](#Partial_upgrades_are_unsupported), i.e. never run `pacman -Sy` and instead use `pacman -Syu`.

Avoid using the `--force` option with pacman, **especially** in commands such as `pacman -Syu --force` involving more than one package. The `--force` option ignores file conflicts and can even cause file loss when files are relocated between different packages! In a properly maintained system, it should only be used when explicitly recommended by the Arch developers (see [#Read before upgrading the system](#Read_before_upgrading_the_system)).

Avoid using the `-d` option with pacman. `pacman -Rdd package` skips dependency checks during package removal. As a result, a package providing a critical dependency could be removed, resulting in a broken system.

### 不支持部分升级

Arch Linux 是滚动发行版，新[库](https://en.wikipedia.org/wiki/Library_(computing) 版本将不断被推送到源。开发者和信任用户会按照需要重新构建源中的所有软件包。如果有本地安装的版本(例如 AUR 软件包)，需要在它们的依赖关系升级了[soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname")时重新编译。

也就是说，部分升级是**不被支持的**。

不要使用 `pacman -Sy package` 或等价命令如 `pacman -Sy` 之后再 `pacman -S package`。在安装软件包前请更新源并升级。同理请特别注意 IgnorePkg/IgnoreGroup 的使用。

如果进行了部分升级，二进制包因为找不到链接库而损坏，**不要通过简单的符号链接进行修正**。库升级 [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname") 是因为它们**不再向前兼容**。只要 *pacman* 可以运行，使用更新的源进行 `pacman -Syu` 就能修复这些问题。

The bash script *checkupdates*, included with the pacman package, provides a safe way to check for upgrades to installed packages without running a system update at the same time. See also [BBS##1563725](https://bbs.archlinux.org/viewtopic.php?pid=1563725#p1563725).

### Read before upgrading the system

Before upgrading Arch, always read the latest [Arch News](https://www.archlinux.org/news/) to find out if there are any major software or configuration changes with the latest packages. Before upgrading fundamental software (such as the [kernel](/index.php/Kernel "Kernel"), [xorg](/index.php/Xorg "Xorg"), [systemd](/index.php/Systemd "Systemd"), or [glibc](https://www.archlinux.org/packages/?name=glibc)) to a new version, look over the appropriate [forum](https://bbs.archlinux.org/) to see if there have been any reported problems.

在升级Arch前, 一定要阅读[Arch News](https://www.archlinux.org/news/)来查看是否有主要的软件更改和最新软件包的是否配置文件的更改. 在更新如：内核，xorg和库文件到一个新版本等重要软件之前, 仔细查看[论坛](https://bbs.archlinux.org/)看是否有被报告的出错等问题.

### Act on alerts during an upgrade

When upgrading the system, be sure to pay attention to the alert notices provided by [pacman](/index.php/Pacman "Pacman"). If any additional actions are required by the user, be sure to take care of them right away. If a pacman alert is confusing, search the forums and the recent news posts for more detailed instructions.

当升级系统时， 请一定要注意pacman输出的注意信息。 如果有需要用户手动操作的，请一定要立即搞定。 如果不明白pacman输出的信息， 请去论坛搜索或者看Arch Linux首页的新闻。

### Deal promptly with new configuration files

When pacman is invoked `.pacnew`, `.pacsave`, and `.pacorig` files can be created. Pacman provides notice when this happens and users must deal with these files promptly. Users are referred to the [Pacnew and Pacsave files](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files") wiki page for detailed instructions.

Also, think about other configuration files you may have copied or created. If a package had an example configuration that you copied to your home directory, check to see if a new one has been created.

### Revert broken updates

If a package update is expected/known to cause problems, packagers will ensure that pacman displays an appropriate message when the package is updated. If experiencing trouble after an update, double-check pacman's output by looking at `/var/log/pacman.log`.

At this point, only after ensuring there is no information available through pacman, there is no relative news on [https://www.archlinux.org/](https://www.archlinux.org/), and there are no forum posts regarding the update, consider seeking help on the [forum](https://bbs.archlinux.org), over [IRC](/index.php/IRC "IRC"), or by [downgrading](/index.php/Downgrading_packages "Downgrading packages") the offending package.

### 使用包管理器安装软件

软件包管理 [pacman](/index.php/Pacman "Pacman") 可以比你更好的记录安装的文件。如果你手动地安装软件，你会过了一会就不知道你到底安装了什么，到底安装在哪里，安装导致的那些冲突，是否安装在了错误的地方，等等问题. 避免安装自编译的软件包,可以自己[创建软件包](/index.php/Creating_packages "Creating packages")。

要清理自己安装的文件，可以查看[这里](/index.php/Pacman/Tips_and_tricks#Identify_files_not_owned_by_any_package "Pacman/Tips and tricks").

### 选择开源驱动

尽可能地选择开源驱动。避免私有驱动。大多数时候，开源驱动比私有驱动更加稳定可靠。开源驱动的bugs修改起来比较容易快速，但同时私有驱动提供更多的特性和性能，不过也可能带来稳定性的代价。为了避免这个两难选择，可以选择已知的有很好的开源驱动支持的硬件。关于硬件和开源Linux驱动的信息可以在这里找到：[linux-drivers.org](http://www.linux-drivers.org/).

### 谨慎使用非官方或测试不足的软件包

在使用 AUR 或 [非官方软件仓库](/index.php/Unofficial_user_repository "Unofficial user repository")中的软件包时应有预防措施。大部分软件包都是由用户提供的，并不能提供和官方软件仓库相同的质量。谨慎使用 [AUR helpers](/index.php/AUR_helpers "AUR helpers") ，他们简化了 AUR 中的软件包的安装过程, 在编译和安装 AUR 中的软件包之前，**务必**检查软件包的 PKGBUILD 确保其中不含有错误或恶意的代码。

只在绝对必要的情况下使用第三方的软件仓库.[pacman/Tips and tricks#Maintenance](/index.php/Pacman/Tips_and_tricks#Maintenance "Pacman/Tips and tricks")提供了清理软件的方法。

### Update the mirrorlist

Update pacman's mirrorlist, as the quality of mirrors can vary over time, and some might go offline or their download rate might degrade.

See [mirrors](/index.php/Mirrors "Mirrors") for details.

## Clean the filesystem

When looking for files to remove, it is important to find the files that take up the most disk space. Programs that help with this are found in:

*   [List of applications#Disk usage display](/index.php/List_of_applications#Disk_usage_display "List of applications").
*   [List of applications#Disk cleaning](/index.php/List_of_applications#Disk_cleaning "List of applications").

### Old configuration files

Old configuration files may conflict with newer software versions, or corrupt over time. Remove unneeded configurations periodically, particularly in your home folder and `~/.config`. For similar reasons, be careful when sharing home folders between installations.

Look for the following folders:

*   `~/.config/` -- where apps stores their configuration
*   `~/.cache/` -- cache of some programs may grow in size
*   `~/.local/share/` -- old files may be lying there

See [XDG Base Directory support](/index.php/XDG_Base_Directory_support "XDG Base Directory support") for more information.

To keep the home directory clean from temporary files created at the wrong place, it is a good idea to manage a list of unwanted files and remove them regularly, for example with [rmshit.py](https://github.com/lahwaacz/Scripts/blob/master/rmshit.py).

[rmlint](https://www.archlinux.org/packages/?name=rmlint) can be used to find and optionally remove duplicate files, empty files, recursive empty directories and broken symlinks.

### Unused packages

Remove unused packages from the system to free up disk space and simplify maintenance.

See [Pacman/Tips and tricks#Removing unused packages](/index.php/Pacman/Tips_and_tricks#Removing_unused_packages "Pacman/Tips and tricks") for details.

### Package cache

Remove unwanted `.pkg` files from `/var/cache/pacman/pkg/`to free up disk space.

See [Pacman#Cleaning the package cache](/index.php/Pacman#Cleaning_the_package_cache "Pacman") for more information.

### Broken symlinks

Old, broken symbolic links might be sitting around your system; you should remove them. Examples on achieving this can be found [here](https://unix.stackexchange.com/questions/34248/how-can-i-find-broken-symlinks) and [here](http://www.commandlinefu.com/commands/view/8260/find-broken-symlinks).

To quickly list all the broken symlinks of your system, use:

```
 # find . -type l -! -exec test -e {} \; -print

```

Then inspect and remove unnecessary entries from this list.

## Tips and tricks

The following tips are generally not required, but certain users may find them useful.

### 使用经过验证的软件包

Arch's rolling releases can be a boon for users who want to try the latest features and get upstream updates as soon as possible, but they can also make system maintenance more difficult. To simplify maintenance and improve stability, try to avoid cutting edge software and install only mature and proven software. Such packages are less likely to receive difficult upgrades such as major configuration changes or feature removals. Prefer software that has a strong and active development community, as well as a high number of competent users, in order to simplify support in the event of a problem.

避免使用测试仓库，这些软件包都是实验性质，不适合安装到稳定系统。因此对于[AUR](/index.php/AUR "AUR")中的包以及部分 community 中的包需要一些谨慎，这些开发中的包是直接从上游开发版分支中获取到的，通常会在包的名字上注有：dev, devel, svn, cvs, git, hg, 或是 darcs 的信息。

### 安装内核的长期支持版本

[linux-lts](https://www.archlinux.org/packages/?name=linux-lts) 是 Arch 官方提供的 Linux kernel 的长期支持版本。内核上游开发者针对此版本提供了长期支持，包括安全补丁和功能 backports。适用于需要长期支持的用户，也可以将此内核作为新内核升级的后备内核。

需要编辑 [bootloader](/index.php/Bootloader "Bootloader") 的启动加载项，启动到 `vmlinuz-linux-lts` 和 `initramfs-linux-lts.img`。