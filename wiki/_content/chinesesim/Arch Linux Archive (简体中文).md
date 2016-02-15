**翻译状态：** 本文是英文页面 [Arch_Linux_Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-11-11，点击[这里](https://wiki.archlinux.org/index.php?title=Arch_Linux_Archive&diff=0&oldid=408495)可以查看翻译后英文页面的改动。

Arch Linux 存档（**A**rch **L**inux **Archive**，_简称 ala_），以前称为 _Arch Linux 回滚机器（Arch Linux Rollback Machine_，_简称 ARM_），保存了 _官方仓库快照_、_iso 镜像_ 和 _引导程序包_ 的历史版本。

**用途**

*   将某个包降级到某个早期版本（最新版本不能用，我需要之前的版本）
*   将所有包恢复到某个指定的历史时刻（所有包都不能用，我要恢复到两个月之前的状态）
*   查找某个历史版本的 ISO 镜像

## Contents

*   [1 位置](#.E4.BD.8D.E7.BD.AE)
*   [2 目录](#.E7.9B.AE.E5.BD.95)
    *   [2.1 /repos](#.2Frepos)
    *   [2.2 /packages](#.2Fpackages)
    *   [2.3 /iso](#.2Fiso)
*   [3 agetpkg](#agetpkg)
    *   [3.1 Download a previous version of ferm package](#Download_a_previous_version_of_ferm_package)
    *   [3.2 Download xterm version 296](#Download_xterm_version_296)
    *   [3.3 List all zsh versions](#List_all_zsh_versions)
    *   [3.4 Install all gvfs packages in version 1.26.0 release 3](#Install_all_gvfs_packages_in_version_1.26.0_release_3)
    *   [3.5 Download all pwgen packages](#Download_all_pwgen_packages)
*   [4 常见问题](#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98)
    *   [4.1 如何降级某个包](#.E5.A6.82.E4.BD.95.E9.99.8D.E7.BA.A7.E6.9F.90.E4.B8.AA.E5.8C.85)
    *   [4.2 如何恢复所有包到指定日期](#.E5.A6.82.E4.BD.95.E6.81.A2.E5.A4.8D.E6.89.80.E6.9C.89.E5.8C.85.E5.88.B0.E6.8C.87.E5.AE.9A.E6.97.A5.E6.9C.9F)
*   [5 源码](#.E6.BA.90.E7.A0.81)
*   [6 未来计划](#.E6.9C.AA.E6.9D.A5.E8.AE.A1.E5.88.92)
*   [7 历史](#.E5.8E.86.E5.8F.B2)

## 位置

Arch Linux 存档目前位于 [https://archive.archlinux.org/](https://archive.archlinux.org/) (即以前的 [http://ala.seblu.net/](http://ala.seblu.net/) ) 。

此前的下列网址即将关闭，建议不要再使用：

*   [http://seblu.net/a/archive](http://seblu.net/a/archive)
*   [ftp://seblu.net/archlinux/archive](ftp://seblu.net/archlinux/archive)

下列网址已关闭：

*   [http://seblu.net/a/arm](http://seblu.net/a/arm)
*   [ftp://seblu.net/archlinux/arm](ftp://seblu.net/archlinux/arm)

## 目录

**存档**分为下列三个主目录：

```
├── iso
├── packages
└── repos

```

### /repos

[repos](http://ala.seblu.net/repos) 这个目录包含官方仓库镜像的每日快照，按下例结构组织：

```
repos
├── 2013
│   ├── 08
│   │   └── 31
│   │       ├── community
│   │       ├── community-staging
│   │       ├── community-testing
│   │       ├── core
│   │       ├── extra
│   │       ├── gnome-unstable
│   │       ├── kde-unstable
│   │       ├── lastsync
│   │       ├── multilib
│   │       ├── multilib-staging
│   │       ├── multilib-testing
│   │       ├── pool
│   │       ├── staging
│   │       └── testing
│   ├── 09
│   │   ├── 01
│   │   ├── 02
│   │   ├── ...
│   │   ├── 21
│   │   └── 22
│   ├── 10
│   │   ├── 01
│   │   ├── 02
│   │   ├── ...
│   │
│   ├── 11
│   └── 12
├── 2014
│   ├── 01
│   │   ├── 01
│   │   ├── 02
│   │   ├── ...
│   │
│   ├── 02
│   ├── 03
│   ├── ...
│   └── 09
│       ├── 01
│       ├── ...
│       └── 28
├── last
├── month
└── week

```

注意: 最下面的三个特定目录（**last**、**week** 和 **month**）分别链接到**已同步的最新仓库版本**、**本周星期一版本**和**本月一日版本**。

### /packages

[packages](http://ala.seblu.net/packages) 这个目录包含每个包的所有版本及其相应的数字签名。每个包一个目录，按首字母排序。

```
├── packages
│   ├── a
│   │   ├── awesome
│   │   │   ├── awesome-3.5.0-1-i686.pkg.tar.xz
│   │   │   ├── awesome-3.5.0-1-i686.pkg.tar.xz.sig
│   │   │   ├── awesome-3.5.0-1-x86_64.pkg.tar.xz
│   │   │   ├── awesome-3.5.0-1-x86_64.pkg.tar.xz.sig
│   │   │   ├── awesome-3.5.1-1-i686.pkg.tar.xz
│   │   │   ├── awesome-3.5.1-1-i686.pkg.tar.xz.sig
│   │   │   ├── ...
│   │   │ 
│   │   ├── ...
│   │   ├── awstats
│   │   └── axel
│   │   
│   ├── b
│   ├── ...
│   └── z

```

你可以使用“魔法目录”[.all](http://ala.seblu.net/packages/.all) 按包名访问所有包。In a nutshell, all versions of each package in one flat directory. No clear-text listing allowed here.

```
├── packages
│   ├── .all
│   │   ├── awesome-3.5.1-1-i686.pkg.tar.xz
│   │   ├── ...
│   │   ├── zsh-5.0.2-3-i686.pkg.tar.xz
│   │   ├── zsh-5.0.2-4-i686.pkg.tar.xz
│   │   └── ...

```

An lightweight index, named [index.0.xz](http://ala.seblu.net/packages/.all/index.0.xz) is available to list all package in once.

### /iso

The [iso](http://ala.seblu.net/iso) directory contains official ISO images and bootstrap tarballs sorted by release date.

```
├── 2014.09.03
├── 2014.10.01
├── 2014.11.01
├── 2014.12.01
├── 2015.07.01
├── 2015.08.01
├── 2015.09.01
└── 2015.10.01
    ├── arch
    ├── archlinux-2015.10.01-dual.iso
    ├── archlinux-2015.10.01-dual.iso.sig
    ├── archlinux-2015.10.01-dual.iso.torrent
    ├── archlinux-bootstrap-2015.10.01-i686.tar.gz
    ├── archlinux-bootstrap-2015.10.01-i686.tar.gz.sig
    ├── archlinux-bootstrap-2015.10.01-x86_64.tar.gz
    ├── archlinux-bootstrap-2015.10.01-x86_64.tar.gz.sig
    ├── md5sums.txt
    └── sha1sums.txt

```

## agetpkg

[agetpkg](https://www.archlinux.org/packages/?name=agetpkg) is a command line tool used to quickly list/get/install packages stored in the Archive.

##### Download a previous version of ferm package

```
agetpkg ferm

```

##### Download xterm version 296

```
agetpkg ^xterm 296

```

##### List all zsh versions

```
agetpkg -l zsh$

```

##### Install all gvfs packages in version 1.26.0 release 3

```
agetpkg -i gvfs 1.26.0 3

```

##### Download all pwgen packages

```
agetpkg -g -a pwgen

```

## 常见问题

### 如何降级某个包

You can use [#agetpkg](#agetpkg) to easily download a specific package version from the Archive.

Or you can do it manually:

1.  Run your favorite internet browser and go to [http://ala.seblu.net/packages](http://ala.seblu.net/packages);
2.  Go to the package you need and download it;
3.  Run `pacman -U _pkgname_.pkg.tar.xz` as root.

### 如何恢复所有包到指定日期

如果想恢复所有包到指定日期（比如2014年3月30日），你必须如下例所示编辑 `/etc/pacman.conf`，从而让 [pacman](/index.php/Pacman "Pacman") 保持在这个时间点并且直接使用指定的服务器：

```
[core]
SigLevel = PackageRequired
Server=http://ala.seblu.net/repos/2014/03/30/$repo/os/$arch

[extra]
SigLevel = PackageRequired
Server=http://ala.seblu.net/repos/2014/03/30/$repo/os/$arch

[community]
SigLevel = PackageRequired
Server=http://ala.seblu.net/repos/2014/03/30/$repo/os/$arch

```

或者如下例编辑 `/etc/pacman.d/mirrorlist`：

```
##                                                                              
## Arch Linux repository mirrorlist                                             
## Generated on 2042-01-01                                                      
##
Server=http://ala.seblu.net/repos/2014/03/30/$repo/os/$arch

```

然后同步包数据库以强制降级：

```
# pacman -Syyuu

```

**注意:** 混用归档和更新镜像很不安全。万一降级失败，In case of download failure, you can fall-back on an upstream package and you will have packages not from the same epoch as the rest of the system.

## 源码

*   [archivetools](https://github.com/seblu/archivetools) -- Software to run an Archive server
*   [agetpkg](https://github.com/seblu/agetpkg) -- Software to easy downgrade package from the Archive

## 未来计划

*   Move to official infrastructure.
*   Automatic clean-up after a defined amount of time?
*   Archive more stuff?

## 历史

*   New URL and closing the old ARM hierarchy on 2015-10-13\. A new software, agetpkg was introduced.
*   The original ARM (_Archlinux Rollback Machine_) was closed on 2013-08-18 [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1313360#p1313360).
*   The new one is hosted on [seblu.net](http://seblu.net) since 2013-08-31.