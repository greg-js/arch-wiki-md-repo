# Pacman (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

相关文章

*   [Downgrading packages](/index.php/Downgrading_packages "Downgrading packages")
*   [Improve pacman performance](/index.php/Improve_pacman_performance "Improve pacman performance")
*   [Pacman GUI Frontends](/index.php/Pacman_GUI_Frontends "Pacman GUI Frontends")
*   [Pacman Rosetta](/index.php/Pacman_Rosetta "Pacman Rosetta")
*   [Pacman tips](/index.php/Pacman_tips "Pacman tips")
*   [Pacman package signing](/index.php/Pacman_package_signing "Pacman package signing")
*   [FAQ#Package Management](/index.php/FAQ#Package_Management "FAQ")
*   [pacman-key](/index.php/Pacman-key "Pacman-key")
*   [Pacnew and Pacsave files](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files")
*   [List of Applications/Utilities#Package management](/index.php/List_of_Applications/Utilities#Package_management "List of Applications/Utilities")
*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System")
*   [Official repositories (简体中文)](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")
*   [Arch User Repository (简体中文)](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")

**翻译状态：** 本文是英文页面 [pacman](/index.php/Pacman "Pacman") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-08-02，点击[这里](https://wiki.archlinux.org/index.php?title=pacman&diff=0&oldid=327709)可以查看翻译后英文页面的改动。

**[pacman](https://archlinux.org/pacman/)** 包管理器是 Arch Linux 的一大亮点。它将一个简单的二进制包格式和易用的构建系统结合了起来(参见[makepkg](/index.php/Makepkg "Makepkg")和[ABS](/index.php/ABS "ABS"))。不管软件包是来自官方的 Arch 库还是用户自己创建，_pacman_ 都能方便得管理。

_pacman_ 通过和主服务器同步软件包列表来进行系统更新，这使得注重安全的系统管理员的维护工作成为轻而易举的事情。这种服务器/客户端模式可以使用一条命令就下载/安装软件包，同时安装必需的依赖包。

_pacman_ 用 C 语言编写，使用 `.pkg.tar.xz` 打包格式。

**小贴士:** 官方的 **pacman** 软件包还提供了其它有用工具，例如**makepkg**、**pactree**、**vercomp**等。可以通过 `pacman -Ql pacman | grep bin` 获取工具列表。

## Contents

*   [1 配置](#.E9.85.8D.E7.BD.AE)
    *   [1.1 通用选项](#.E9.80.9A.E7.94.A8.E9.80.89.E9.A1.B9)
        *   [1.1.1 不升级软件包](#.E4.B8.8D.E5.8D.87.E7.BA.A7.E8.BD.AF.E4.BB.B6.E5.8C.85)
        *   [1.1.2 不升级软件包组](#.E4.B8.8D.E5.8D.87.E7.BA.A7.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.BB.84)
        *   [1.1.3 跳过](#.E8.B7.B3.E8.BF.87)
    *   [1.2 软件仓库](#.E8.BD.AF.E4.BB.B6.E4.BB.93.E5.BA.93)
    *   [1.3 软件包的安全性](#.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.9A.84.E5.AE.89.E5.85.A8.E6.80.A7)
*   [2 用法](#.E7.94.A8.E6.B3.95)
    *   [2.1 安装软件包](#.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85)
        *   [2.1.1 安装指定的包](#.E5.AE.89.E8.A3.85.E6.8C.87.E5.AE.9A.E7.9A.84.E5.8C.85)
        *   [2.1.2 安装包组](#.E5.AE.89.E8.A3.85.E5.8C.85.E7.BB.84)
    *   [2.2 删除软件包](#.E5.88.A0.E9.99.A4.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [2.3 升级软件包](#.E5.8D.87.E7.BA.A7.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [2.4 查询包数据库](#.E6.9F.A5.E8.AF.A2.E5.8C.85.E6.95.B0.E6.8D.AE.E5.BA.93)
    *   [2.5 清理软件包缓存](#.E6.B8.85.E7.90.86.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.BC.93.E5.AD.98)
    *   [2.6 其它命令](#.E5.85.B6.E5.AE.83.E5.91.BD.E4.BB.A4)
    *   [2.7 不支持部分升级](#.E4.B8.8D.E6.94.AF.E6.8C.81.E9.83.A8.E5.88.86.E5.8D.87.E7.BA.A7)
    *   [2.8 一般注意事项](#.E4.B8.80.E8.88.AC.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A1.B9)
*   [3 问题解决](#.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
    *   [3.1 软件包 XYZ 升级搞坏了系统!](#.E8.BD.AF.E4.BB.B6.E5.8C.85_XYZ_.E5.8D.87.E7.BA.A7.E6.90.9E.E5.9D.8F.E4.BA.86.E7.B3.BB.E7.BB.9F.21)
    *   [3.2 我知道软件包 ABC 已经发布，但 pacman 说系统已经是最新!](#.E6.88.91.E7.9F.A5.E9.81.93.E8.BD.AF.E4.BB.B6.E5.8C.85_ABC_.E5.B7.B2.E7.BB.8F.E5.8F.91.E5.B8.83.EF.BC.8C.E4.BD.86_pacman_.E8.AF.B4.E7.B3.BB.E7.BB.9F.E5.B7.B2.E7.BB.8F.E6.98.AF.E6.9C.80.E6.96.B0.21)
    *   [3.3 升级时遇到问题: "file exists in filesystem"(文件系统上已经存在文件)!](#.E5.8D.87.E7.BA.A7.E6.97.B6.E9.81.87.E5.88.B0.E9.97.AE.E9.A2.98:_.22file_exists_in_filesystem.22.28.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E4.B8.8A.E5.B7.B2.E7.BB.8F.E5.AD.98.E5.9C.A8.E6.96.87.E4.BB.B6.29.21)
    *   [3.4 安装软件包时提示 "not found in sync db"](#.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85.E6.97.B6.E6.8F.90.E7.A4.BA_.22not_found_in_sync_db.22)
    *   [3.5 安装软件包出错：“target not found”](#.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85.E5.87.BA.E9.94.99.EF.BC.9A.E2.80.9Ctarget_not_found.E2.80.9D)
    *   [3.6 pacman 重复升级同一个包！](#pacman_.E9.87.8D.E5.A4.8D.E5.8D.87.E7.BA.A7.E5.90.8C.E4.B8.80.E4.B8.AA.E5.8C.85.EF.BC.81)
    *   [3.7 pacman 更新时崩溃!](#pacman_.E6.9B.B4.E6.96.B0.E6.97.B6.E5.B4.A9.E6.BA.83.21)
    *   [3.8 我通过 make install 安装软件，它们不属于任何软件包！](#.E6.88.91.E9.80.9A.E8.BF.87_make_install_.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.EF.BC.8C.E5.AE.83.E4.BB.AC.E4.B8.8D.E5.B1.9E.E4.BA.8E.E4.BB.BB.E4.BD.95.E8.BD.AF.E4.BB.B6.E5.8C.85.EF.BC.81)
    *   [3.9 我需要有一个指定文件的包。我怎么知道谁提供了这个文件？](#.E6.88.91.E9.9C.80.E8.A6.81.E6.9C.89.E4.B8.80.E4.B8.AA.E6.8C.87.E5.AE.9A.E6.96.87.E4.BB.B6.E7.9A.84.E5.8C.85.E3.80.82.E6.88.91.E6.80.8E.E4.B9.88.E7.9F.A5.E9.81.93.E8.B0.81.E6.8F.90.E4.BE.9B.E4.BA.86.E8.BF.99.E4.B8.AA.E6.96.87.E4.BB.B6.EF.BC.9F)
    *   [3.10 pacman 完全坏掉，如何修复?](#pacman_.E5.AE.8C.E5.85.A8.E5.9D.8F.E6.8E.89.EF.BC.8C.E5.A6.82.E4.BD.95.E4.BF.AE.E5.A4.8D.3F)
    *   [3.11 升级系统重启后，出现"unable to find root device"错误，无法登陆](#.E5.8D.87.E7.BA.A7.E7.B3.BB.E7.BB.9F.E9.87.8D.E5.90.AF.E5.90.8E.EF.BC.8C.E5.87.BA.E7.8E.B0.22unable_to_find_root_device.22.E9.94.99.E8.AF.AF.EF.BC.8C.E6.97.A0.E6.B3.95.E7.99.BB.E9.99.86)
        *   [3.11.1 Fallback 启动项](#Fallback_.E5.90.AF.E5.8A.A8.E9.A1.B9)
        *   [3.11.2 Chroot 修复](#Chroot_.E4.BF.AE.E5.A4.8D)
    *   [3.12 Signature from "User <email@gmail.com>" is unknown trust, installation failed](#Signature_from_.22User_.3Cemail.40gmail.com.3E.22_is_unknown_trust.2C_installation_failed)
    *   [3.13 不停看到错误 "PackageName: signature from "User <email@archlinux.org>" is invalid"](#.E4.B8.8D.E5.81.9C.E7.9C.8B.E5.88.B0.E9.94.99.E8.AF.AF_.22PackageName:_signature_from_.22User_.3Cemail.40archlinux.org.3E.22_is_invalid.22)
    *   [3.14 不停收到错误error: failed to commit transaction (invalid or corrupted package)](#.E4.B8.8D.E5.81.9C.E6.94.B6.E5.88.B0.E9.94.99.E8.AF.AFerror:_failed_to_commit_transaction_.28invalid_or_corrupted_package.29)
    *   [3.15 如果每次使用 pacman 时都报告：'warning: current locale is invalid; using default "C" locale'. 怎么办?](#.E5.A6.82.E6.9E.9C.E6.AF.8F.E6.AC.A1.E4.BD.BF.E7.94.A8_pacman_.E6.97.B6.E9.83.BD.E6.8A.A5.E5.91.8A.EF.BC.9A.27warning:_current_locale_is_invalid.3B_using_default_.22C.22_locale.27._.E6.80.8E.E4.B9.88.E5.8A.9E.3F)
    *   [3.16 怎样让pacman使用我的代理设置?](#.E6.80.8E.E6.A0.B7.E8.AE.A9pacman.E4.BD.BF.E7.94.A8.E6.88.91.E7.9A.84.E4.BB.A3.E7.90.86.E8.AE.BE.E7.BD.AE.3F)
    *   [3.17 如何重装所有包并保留安装和依赖信息？](#.E5.A6.82.E4.BD.95.E9.87.8D.E8.A3.85.E6.89.80.E6.9C.89.E5.8C.85.E5.B9.B6.E4.BF.9D.E7.95.99.E5.AE.89.E8.A3.85.E5.92.8C.E4.BE.9D.E8.B5.96.E4.BF.A1.E6.81.AF.EF.BC.9F)
    *   [3.18 pacman 出错："error: failed to init transaction (unable to lock database)"](#pacman_.E5.87.BA.E9.94.99.EF.BC.9A.22error:_failed_to_init_transaction_.28unable_to_lock_database.29.22)
*   [4 参见](#.E5.8F.82.E8.A7.81)

## 配置

_pacman_ 的配置文件位于`/etc/pacman.conf`。 [man pacman.conf](https://www.archlinux.org/pacman/pacman.conf.5.html) 可以查看配置文件的进一步信息。

### 通用选项

通用选项都在`[options]`段。阅读 man 手册或者查看默认的 pacman.conf 可以获得有关信息和用法。

#### 不升级软件包

如果由于某种原因，用户不希望升级某个软件包，可以加入内容如下：

```
IgnorePkg = 软件包名

```

多软件包可以用空格隔开，也可是用 glob 模式。如果只打算忽略一次升级，可以使用 `--ignore` 选项。

忽略了的软件包可通过 `pacman -S` 升级。

#### 不升级软件包组

和软件包一样，也可以不升级某个软件包组：

```
IgnoreGroup = gnome

```

#### 跳过

要跳过某些文件夹的安装，可以将它们放到 `NoExtract` 中，例如不想安装 [systemd](/index.php/Systemd "Systemd") unit 文件：

```
NoExtract=usr/lib/systemd/system/*

```

### 软件仓库

这部分定义使用的软件仓库，在 `/etc/pacman.conf` 中引用，可以直接设置或者从其它文件包含。

所有官方软件仓库都使用同一个包含了'`$repo`' 的 `/etc/pacman.d/mirrorlist`文件，因此只需要维护一个列表。 下面例子中使用[官方软件仓库](/index.php/Official_repositories "Official repositories")，用 mirrorlist 设定[镜像](/index.php/Mirrors "Mirrors")的一个范例。

```
#[testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

[core]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

[extra]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

#[community-testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

[community]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

# 如果打算在 x86_64 系统上运行32位软件，启用 multilib 软件仓库。

#[multilib-testing]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

#[multilib]
#SigLevel = PackageRequired
#Include = /etc/pacman.d/mirrorlist

# 自定义软件仓库实例，如何创建软件仓库参见 pacman man手册页。
#[custom]
#SigLevel = Optional TrustAll
#Server = file:///home/custompkgs

```

**警告:** 使用 `[testing]` 仓库的时候要谨慎，这个仓库里面开发比较活跃，可能导致某些软件包不能工作。推荐使用 `[testing]` 的用户订阅 [arch-dev-public 邮件列表](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public)以获得最新信息。

### 软件包的安全性

_pacman_ 4 支持软件包签名。语句 `SigLevel = Required DatabaseOptional` 将启用全局签名验证，但会被每个软件仓库的 `SigLevel` 行所覆盖。详情参见 [pacman-key](/index.php/Pacman-key_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman-key (简体中文)").

## 用法

_pacman_ 的其他示例请阅读[man pacman](https://archlinux.org/pacman/pacman.8.html)。下面只是一个可执行操作的小部分示范。

### 安装软件包

#### 安装指定的包

安装或者升级单个软件包，或者一列软件包（包含依赖包），使用如下命令：

```
# pacman -S package_name1 package_name2 ...

```

用正则表达式安装多个软件包（参见 [pacman 小贴士](/index.php/Pacman_tips_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.B7.A7.E7.94.A8_Bash_.E8.AF.AD.E6.B3.95 "Pacman tips (简体中文)")和[这个帖子](https://bbs.archlinux.org/viewtopic.php?id=7179)）：

```
# pacman -S $(pacman -Ssq package_regex)

```

有时候在不同的软件仓库中，一个软件包有多个版本（比如[extra]和[testing]）。可以选择一个来安装：

```
# pacman -S extra/package_name

```

#### 安装包组

一些包属于一个可以同时安装的包组。例如，运行下面的命令

```
# pacman -S gnome

```

会提醒用户选择 `gnome` 内需要安装的包。

有的包组包含大量的软件包，有时用户只需其中几个。除了逐一键入序号外，pacman 还支持选择或排除某个区间内的的软件包：

```
Enter a selection (default=all): 1-10 15

```

这将选中序号 1 至 10 和 15 的软件包。而

```
Enter a selection (default=all): ^5-8 ^2

```

将会选中除了序号 5 至 8 和 2 之外的所有软件包。

想要查看哪些包属于 gnome 组，运行：

```
# pacman -Sg gnome

```

也可以访问 [https://www.archlinux.org/groups/](https://www.archlinux.org/groups/) 查看可用的包组。

**注意:** 如果列表中的包已经安装在系统中，它会被重新安装，即使它已经是最新的。可以用 `--needed` 选项覆盖这种行为。

**Warning:** 未[更新](#.E5.8D.87.E7.BA.A7.E8.BD.AF.E4.BB.B6.E5.8C.85)系统前，**不要**在安装软件包时更新软件包数据库（`pacman -Sy _package_name_`），否则会有依赖问题。参见[#不支持部分升级](#.E4.B8.8D.E6.94.AF.E6.8C.81.E9.83.A8.E5.88.86.E5.8D.87.E7.BA.A7)和 [https://bbs.archlinux.org/viewtopic.php?id=89328](https://bbs.archlinux.org/viewtopic.php?id=89328).

### 删除软件包

删除单个软件包，保留其全部已经安装的依赖关系

```
pacman -R package_name

```

删除指定软件包，及其所有没有被其他已安装软件包使用的依赖关系：

```
pacman -Rs package_name

```

要删除软件包和所有依赖这个软件包的程序:

```
# pacman -Rsc package_name

```

**警告:** 此操作是递归的，请小心检查，可能会一次删除大量的软件包。

要删除软件包，但是不删除依赖这个软件包的其他程序：

```
# pacman -Rdd package_name

```

_pacman_ 删除某些程序时会备份重要配置文件，在其后面加上*.pacsave扩展名。-n 选项可以删除这些文件：

```
pacman -Rn package_name
pacman -Rsn package_name

```

**注意:** _pacman_ 不会删除软件自己创建的文件(例如主目录中的 `.dot` 文件不会被删除。

### 升级软件包

一个 _pacman_ 命令就可以升级整个系统。花费的时间取决于系统有多老。这个命令会同步非本地(local)软件仓库并升级系统的软件包：

```
# pacman -Syu

```

**警告:** 由于 Arch 的滚动升级特性，升级系统有着不可预见的结果。因此，除非有着空闲时间并准备好处理突发问题，请谨慎升级。

_pacman_ 是强大的软件包管理工具，但是不会做所有的事情。若有疑问，请阅读[Arch 之道](/index.php/Arch_Linux_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Linux (简体中文)")。用户需要负责维护自己的系统。**执行系统升级时，请务必阅读 _pacman_ 输出的所有信息。**如果修改过的配置文件需要更新，新的配置文件会被保存为 `.pacnew` 文件以免覆盖了用户的配置。_pacman_ 会提醒用户合并新旧文件。这些文件需要手动干预。在升级或删除软件包后，应该立即着手处理。参见 [Pacnew 和 pacsave 文件](/index.php/Pacnew_and_Pacsave_files_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacnew and Pacsave files (简体中文)")。

**小贴士:** _pacman_ 输出会记录到 `/var/log/pacman.log`。

建议升级前访问 [Arch Linux 主页](https://www.archlinux.org/)查看最新消息（或订阅 [RSS](https://www.archlinux.org/feeds/news/)，或订阅 [arch-announce 邮件列表](https://mailman.archlinux.org/mailman/listinfo/arch-announce/)，或关注 [@archlinux](https://twitter.com/archlinux)。如果升级需要不寻常的用户介入（无法简单地按照 _pacman_ 的输出信息处理），总会给出合适的方法。

如果遇到问题，无法按照给出方法解决。请搜索下论坛，很有可能已经有人遇到并解决了。

### 查询包数据库

_pacman_ 使用 -Q 参数查询本地软件包数据库。参见：

```
$ pacman -Q --help

```

使用 -S 参数来查询远程同步的数据库。参见：

```
$ pacman -S --help

```

_pacman_ 可以在包数据库中查询软件包，查询位置包含了软件包的名字和描述：

```
$ pacman -Ss _string1_ _string2_ ...

```

要查询已安装的软件包：

```
$ pacman -Qs _string1_ _string2_ ...

```

显示软件包的详尽的信息：

```
$ pacman -Si _package_name_

```

查询本地安装包的详细信息：

```
$ pacman -Qi _package_name_

```

使用两个 `-i` 将同时显示备份文件和修改状态：

```
$ pacman -Qii _package_name_

```

要获取已安装软件包所包含文件的列表：

```
$ pacman -Ql _package_name_

```

未安装的软件包使用 [pkgfile](/index.php/Pkgfile_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pkgfile (简体中文)")。

检查软件包安装的文件是否都存在：

```
$ pacman -Qk _package_name_

```

查询数据库获取某个文件属于哪个软件包：

```
$ pacman -Qo _/path/to/file_name_

```

要罗列所有不再作为依赖的软件包(孤立orphans)：

```
$ pacman -Qdt

```

要显示软件包的依赖树：

```
$ pactree _package_name_

```

检查一个_安装_的软件包被那些包依赖，可以使用 [pkgtools](/index.php?title=Pkgtools_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Pkgtools (简体中文) (page does not exist)") 提供的 `whoneeds`：

```
$ whoneeds _package_name_

```

### 清理软件包缓存

_pacman_ 将下载的软件包保存在 `/var/cache/pacman/pkg/` 并且不会自动移除旧的和未安装版本的软件包，因此需要手动清理，以免该文件夹过于庞大。

使用内建选项即可清除未安装软件包的缓存：

```
# pacman -Sc

```

**警告:**

*   仅在确定当前安装的软件包足够稳定且不需要[降级](/index.php/Downgrading_packages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Downgrading packages (简体中文)")时才执行清理。旧版本的软件包能系统更新崩溃时派上用场。如果旧版本的软件包被清理掉了，那只能从其他地方获取了，如 [Arch Rollback Machine](/index.php?title=Arch_Rollback_Machine_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Arch Rollback Machine (简体中文) (page does not exist)")。
*   `pacman -Scc` 可以清理所有缓存，但这样 pacman 在重装软件包时就只能重新下载了。除非空间不足，否则不应这么做。

由于以上种种局限，建议使用专门的脚本去处理清理哪些、清理多少缓存：

*   [pacman](https://www.archlinux.org/packages/?name=pacman) 提供的 _paccache_ 命令默认会删除近3个版本前的软件包: `$ paccache -r` 但是 _paccache_ _不会_检查某一个包是否安装了，因此会遗留未安装的包。运行一次，再运行 `$ paccache -ruk0` 可解决此问题。更多功能参见`paccache -h`。

*   除了 _paccache_，还可以使用 [Arch User Repository](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 中的 [pkgcacheclean](https://aur.archlinux.org/packages/pkgcacheclean/)<sup><small>AUR</small></sup>： `# pkgcacheclean` 

### 其它命令

升级系统时安装其他软件包：

```
# pacman -Syu _package_name1_ _package_name2_ ...

```

下载包而不安装它：

```
# pacman -Sw package_name

```

安装一个**本地**包(不从源里下载）：

```
# pacman -U /path/to/package/package_name-version.pkg.tar.xz

```

**小贴士:** 要将本地包保存至缓存，可执行：

```
# pacman -U file://path/to/package/package_name-version.pkg.tar.xz

```

安装一个**远程**包（不在 _pacman_ 配置的源里面）：

```
# pacman -U http://www.example.com/repo/example.pkg.tar.xz

```

### 不支持部分升级

Arch Linux 是滚动发行版，新[库](https://en.wikipedia.org/wiki/Library_(computing) "wikipedia:Library (computing)") 版本将不断被推送到源。开发者和信任用户会按照需要重新构建源中的所有软件包。如果有本地安装的版本(例如 AUR 软件包)，需要在它们的依赖关系升级了[soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname")时重新编译。

也就是说，部分升级是**不被支持的**。不要使用 `pacman -Sy package` 或等价命令如 `pacman -Sy` 之后再 `pacman -S package`。在安装软件包前请更新源并升级。同理请特别注意 IgnorePkg/IgnoreGroup 的使用。

如果进行了部分升级，二进制包因为找不到链接库而损坏，**不要通过简单的符号链接进行修正**。库升级 [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname") 是因为它们**不再向前兼容**。只要 _pacman_ 可以运行，使用更新的源进行 `pacman -Syu` 就能修复这些问题。

### 一般注意事项

**警告:** 小心使用 `--force` 开关。使用不当会造成大问题。 请_只_在 Arch 新闻里要求这么做的时候才用。

_pacman_ 附带了许多实用工具能让系统使用更加便捷。所有工具功能都能通过 `--help` 开关查看。运行：

```
$ pacman -Ql pacman | awk -F"[/ ]" '/\/usr\/bin/ {print $5}'

```

查看完整列表

## 问题解决

### 软件包 XYZ 升级搞坏了系统!

Arch Linux 是滚动发行的前沿版本。软件包稳定度只要能够满足日常使用，就会发布新版本。但是，升级有时需要用户参与：更新配置文件、修改依赖关系等。

最重要的是不要"盲目"升级系统。每次都查看更新软件包列表，看看是不是有"关键"软件包升级(`linux`、 `xorg-server`等)。如果有，最好查看 [https://www.archlinux.org](https://www.archlinux.org) 和最近的论坛帖子，看看有没有人在升级时遇到问题。

如果软件包升级会导致问题，软件打包者会保证 _pacman_ 在升级时显示相关信息。如果升级后遇到问题，请再次查看(`/var/log/pacman.log`) 中的 _pacman_ 日志。

这时，**如果确定 _pacman_ 中没有更多信息，[https://www.archlinux.org](https://www.archlinux.org) 没有新闻，论坛没有相关帖子**，可以考虑通过如下方式寻求帮助：论坛、[IRC](/index.php/IRC_Channel "IRC Channel") 或 [降级软件包](/index.php/Downgrading_packages "Downgrading packages")。

### 我知道软件包 ABC 已经发布，但 pacman 说系统已经是最新!

_pacman_ 镜像没有同步完成，一般 24 小时之后升级才会可用。

要么耐心等待，要么换镜像。从[镜像状态页面](https://www.archlinux.org/mirrors/status/)可以找到同步的镜像。

### 升级时遇到问题: "file exists in filesystem"(文件系统上已经存在文件)!

ASIDE: _来自 [https://bbs.archlinux.org/viewtopic.php?id=56373](https://bbs.archlinux.org/viewtopic.php?id=56373) Misfit138 的帖子_

```
error: could not prepare transaction
error: failed to commit transaction (conflicting files)
package: /path/to/file exists in filesystem
Errors occurred, no packages were upgraded.

```

发生了什么事: _pacman_ 检测到文件冲突，而且按照设计，_pacman_ 不会覆盖文件。这是设计功能，不是缺陷。先用 (`pacman -Qo 文件的完整路径` 检查哪个软件包提供了文件。如果是其它软件包，请[报告问题](/index.php/Reporting_bug_guidelines "Reporting bug guidelines")。如果不是其它软件包提供，将已经存在的文件重命名并重新升级。如果一切顺利，可以删掉备份文件。

### 安装软件包时提示 "not found in sync db"

首先，确保软件包已经存在(注意不要有打字错误)。如果确认软件包存在，软件包可能没有和源同步，或者软件源配置不正确。请试着运行 `pacman -Syy` 强制更新全部软件包列表。

### 安装软件包出错：“target not found”

首先确认软件包确实存在（并注意错别字）。如果确认软件包存在，可能本地数据库过时了或者软件仓库没有配置好，试试 `pacman -Syyu` 强制数据库更新和升级。

也有可能包含该软件包的软件仓库没有启动。例如，该软件包可能在 _multilib_ 仓库里，但该仓库没有在 _pacman.conf_ 中启用。

### pacman 重复升级同一个包！

这是因为在 `/var/lib/pacman/local/` 有重复的条目，例如有两个 `linux` 条目。`pacman -Qi` 输出正确的版本，但是 `pacman -Qu` 识别了旧版本，因此尝试升级。

解决方法：删除 `/var/lib/pacman/local/` 中多余的条目。

**注意:** _pacman_ 版本 3.4 在遇到重复条目时会显示错误，因此这个问题过时了。

### pacman 更新时崩溃!

如果 _pacman_ 在删除、重新安装或更新软件包时 "数据库写入" 出错：

1.  从 Arch 安装媒体启动
2.  挂载根文件系统
3.  通过 `pacman -Syy` 更新数据库
4.  通过 `pacman -r 根文件系统路径 -S 软件包` 重新安装

### 我通过 `make install` 安装软件，它们不属于任何软件包！

如果收到 "文件冲突" 错误，注意如果用 `--force` 选项， _pacman_ 会覆盖手动安装的软件包 `pacman -S --force`.

**警告:** 在明确可以使用`--force` 的时候再使用它，否则可能导致系统无法启动。

[不属于任何软件包的文件列表](/index.php/Pacman_tips#Identify_files_not_owned_by_any_package "Pacman tips")一文中提供了查找这些文件的脚本。

### 我需要有一个指定文件的包。我怎么知道谁提供了这个文件？

安装 [pkgfile](/index.php/Pkgfile "Pkgfile")，它使用一个单独的数据库保存所有文件的软件包归属。

### pacman 完全坏掉，如何修复?

如果 _pacman_ 完全坏掉不能使用，需要手动下载或构建需要的软件包([openssl](https://www.archlinux.org/packages/?name=openssl), [libarchive](https://www.archlinux.org/packages/?name=libarchive), [libfetch](https://www.archlinux.org/packages/?name=libfetch)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): package not found]</sup>, 和 [pacman](https://www.archlinux.org/packages/?name=pacman)) 并解压到根目录。_pacman_ 会和默认配置文件一起恢复。之后，用 _pacman_ 重新安装这些软件包以保证数据库的完整性。

### 升级系统重启后，出现"unable to find root device"错误，无法登陆

很有可能 initramfs 在内核升级时损坏，例如错误的使用 _pacman_ 的 `--force` 选项。有两个选择：

#### Fallback 启动项

**Tip:** 如果删除了此启动项，可以在启动时进入启动加载器的手动模式，将 initramfs 修改为 `initramfs-linux-fallback.img` 继续启动。

如果系统可以启动，运行如下命令可以生产原始内核 [linux](https://www.archlinux.org/packages/?name=linux) 的 initramfs:

 `# mkinitcpio -p linux` 

#### Chroot 修复

如果上面方法不行，请下载 2012 年之后发布的安装程序进行启动，执行:

```
# mount /dev/sdxY /mnt         #Your root partition.
# mount /dev/sdxZ /mnt/boot    #If you use a separate /boot partition.
# arch-chroot /mnt
# pacman -Syu mkinitcpio systemd-tools linux
```

重新安装内核([linux](https://www.archlinux.org/packages/?name=linux) 软件包)将会自动运行 `mkinitcpio -p linux` 重新生成 initramfs 镜像，不需要单独生成。

之后建议执行 `exit`, `umount /mnt/{boot,}` 然后 `reboot`.

**Note:** 如果无法进入 arch-chroot 或 chroot 环境，但是需要重新安装软件包，可以使用 pacman -r /mnt -Syu foo bar

### Signature from "User <email@gmail.com>" is unknown trust, installation failed

查看[pacman-key#Resetting all the keys](/index.php/Pacman-key#Resetting_all_the_keys "Pacman-key"). 或试试手动升级`archlinux-keyring`软件包：`pacman -S archlinux-keyring`.

### 不停看到错误 "PackageName: signature from "User <email@archlinux.org>" is invalid"

```
error: PackageName: signature from "User <email@archlinux.org>" is invalid
error: failed to commit transaction (invalid or corrupted package (PGP signature))
Errors occured, no packages were upgraded. 

```

系统时间可能不对，参阅 [time](/index.php/Time "Time") 并运行 `# hwclock -w` 

### 不停收到错误`error: failed to commit transaction (invalid or corrupted package)`

看看`/var/cache/pacman/pkg`中是否有`*.part`结尾的文件，它们是没有完全下载的文件，删除它们并重新执行更新。这些程序一般是自定义的`XferCommand` 下载命令造成的。

### 如果每次使用 pacman 时都报告：'warning: current locale is invalid; using default "C" locale'. 怎么办?

错误信息已经很明确了，locale 设置不正确，请阅读[Locale](/index.php/Locale "Locale")进行设置。

### 怎样让pacman使用我的代理设置?

正确设置环境变量(`$http_proxy`, `$ftp_proxy` etc.)如果使用[sudo](/index.php/Sudo "Sudo"),需要让 sudo [将这些变量传递给 pacman](/index.php/Sudo#Environment_variables_.28Outdated.3F.29 "Sudo").

### 如何重装所有包并保留安装和依赖信息？

重装所有软件包：`pacman -S $(pacman -Qnq)`（`-S` 选项会保留安装缘由）。  
接着需要重装外来包（不在官方仓库里的软件包）。外来包可通过`pacman -Qmq`查看。

### pacman 出错："error: failed to init transaction (unable to lock database)"

_pacman_ 在更新软件包数据库时，比如安装软件包时会创建一个文件锁 `/var/lib/pacman/db.lck`。该文件会阻止其他 _pacman_ 实例在同一时间修改软件包数据库。如果 _pacman_ 在更新数据库时收到干扰，旧锁会一直存在。如果确认 _pacman_ 没有在运行，那么删掉文件锁：

```
# rm /var/lib/pacman/db.lck

```

## 参见

*   [libalpm(3) Manual Page](https://www.archlinux.org/pacman/libalpm.3.html)
*   [pacman(8) Manual Page](https://www.archlinux.org/pacman/pacman.8.html)
*   [pacman.conf(5) Manual Page](https://www.archlinux.org/pacman/pacman.conf.5.html)
*   [repo-add(8) Manual Page](https://www.archlinux.org/pacman/repo-add.8.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Pacman_(简体中文)&oldid=413303](https://wiki.archlinux.org/index.php?title=Pacman_(简体中文)&oldid=413303)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package management (简体中文)](/index.php/Category:Package_management_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Package management (简体中文)")