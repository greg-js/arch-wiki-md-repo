**翻译状态：** 本文是英文页面 [Multilib](/index.php/Multilib "Multilib") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-04-07，点击[这里](https://wiki.archlinux.org/index.php?title=Multilib&diff=0&oldid=429996)可以查看翻译后英文页面的改动。

*multilib* 仓库让用户可以在 64 位 Arch Linux 系统上运行和编译 32 位程序。

## Contents

*   [1 目录结构](#.E7.9B.AE.E5.BD.95.E7.BB.93.E6.9E.84)
*   [2 启用](#.E5.90.AF.E7.94.A8)
*   [3 禁用](#.E7.A6.81.E7.94.A8)
*   [4 参考](#.E5.8F.82.E8.80.83)

## 目录结构

启用 *multilib* 的 64 位系统使用了类似 Debian 的目录结构。 32位库位于 `/usr/lib32/`, 而64位库位于 `/usr/lib/`.

## 启用

想使用 [multilib](/index.php/Official_repositories#multilib "Official repositories") 仓库，编辑 `/etc/pacman.conf`，取消下面内容的注释：

```
[multilib]
Include = /etc/pacman.d/mirrorlist

```

更新软件包列表并升级系统 `pacman -Syu`.

**Note:** 需要仅运行 `pacman -Sy`, [Arch 不支持部分升级](/index.php/System_maintenance#Partial_upgrades_are_unsupported "System maintenance").

## 禁用

要恢复到纯 64 位系统，删除 *multilib*:

运行下面命令可以删除所有从 *multilib* 安装的软件:

```
# pacman -R $(paclist multilib | cut -f1 -d' ')

```

如果有 gcc-libs 冲突，重新安装 64-bit 版本并执行下面命令：

```
# pacman -S gcc-libs base-devel

```

在 `/etc/pacman.conf` 中注释掉 `[multilib]` 段落：

```
#[multilib]
#Include = /etc/pacman.d/mirrorlist

```

用 `pacman -Syu` 更新软件包列表和软件包.

## 参考

*   [Makepkg#Build 32-bit packages on a 64-bit system](/index.php/Makepkg#Build_32-bit_packages_on_a_64-bit_system "Makepkg")
*   [arch-multilib](https://mailman.archlinux.org/mailman/listinfo/arch-multilib) mailing list