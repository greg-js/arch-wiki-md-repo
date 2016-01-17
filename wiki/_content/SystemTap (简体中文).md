# SystemTap (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**翻译状态：** 本文是英文页面 [Systemtap](/index.php/Systemtap "Systemtap") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-10-05，点击[这里](https://wiki.archlinux.org/index.php?title=Systemtap&diff=0&oldid=225189)可以查看翻译后英文页面的改动。

[Systemtap](http://sourceware.org/systemtap/) 是一种在运行时收集系统信息的基础架构，它是自由软件（Free Software）。

## Contents

*   [1 又快又容易](#.E5.8F.88.E5.BF.AB.E5.8F.88.E5.AE.B9.E6.98.93)
    *   [1.1 准备](#.E5.87.86.E5.A4.87)
    *   [1.2 修改config文件](#.E4.BF.AE.E6.94.B9config.E6.96.87.E4.BB.B6)
    *   [1.3 更新校验值](#.E6.9B.B4.E6.96.B0.E6.A0.A1.E9.AA.8C.E5.80.BC)
    *   [1.4 编译并安装](#.E7.BC.96.E8.AF.91.E5.B9.B6.E5.AE.89.E8.A3.85)
    *   [1.5 Systemtap](#Systemtap)
*   [2 编译自定义内核](#.E7.BC.96.E8.AF.91.E8.87.AA.E5.AE.9A.E4.B9.89.E5.86.85.E6.A0.B8)

## 又快又容易

官方推荐编译一个linux-custom内核，但是重新编译原始的[linux](https://www.archlinux.org/packages/?name=linux)包更方便有效，这里介绍重新编译（同名的）linux包的方法。

### 准备

执行 `sudo abs; cp -r /var/abs/core/linux .` 获得PKGBUILD等文件.

### 修改config文件

编辑 **config** (32位内核) 或 **config.x86_64** (64位内核), 确保打开这些选项:

*   CONFIG_DEBUG_INFO=y
*   CONFIG_DEBUG_INFO_REDUCED=n
*   CONFIG_KPROBES=y
*   CONFIG_RELAY=y
*   CONFIG_DEBUG_FS=y
*   CONFIG_MODULES=y
*   CONFIG_MODULE_UNLOAD=y

默认只有_CONFIG_DEBUG_INFO_ 和_CONFIG_DEBUG_INFO_REDUCED_没被打开，修改这两个即可.

对于当前的 core/linux (3.7.10)，只要这样做就可以了:

 `x86_64` 

```
echo '
CONFIG_KPROBES=y
CONFIG_KPROBES_SANITY_TEST=n
CONFIG_KPROBE_EVENT=y
CONFIG_NET_DCCPPROBE=m
CONFIG_NET_SCTPPROBE=m
CONFIG_NET_TCPPROBE=y
CONFIG_DEBUG_INFO=y
CONFIG_DEBUG_INFO_REDUCED=n
CONFIG_X86_DECODER_SELFTEST=n
' >> config.x86_64

```

### 更新校验值

执行 `md5sum config[.x86_64]` 获得新的文件校验值.

编辑 **PKGBUILD** 文件, 这一部分 `md5sums=('sum-of-first' ... 'sum-of-last')` 和这一部分 `source=('first-source' ... 'last-source')` 是个数相同，顺序相同的, 把新获得的校验值在合适的位置替换.

`makepkg --skipchecksums` 使用命令可以跳过校验，但这样做对其它文件（比如下载的内核源码包）来说不安全，**因此建议按这里给出的方法操作**。

### 编译并安装

可选步骤: 可以在 `/etc/makepkg.conf` 文件中设置 `MAKEFLAGS="-j16"` 加速编译.

执行 `makepkg` 开始编译, 然后 `sudo pacman -U *.pkg.tar.gz` 安装编译好的包. **pacman** 会提示你这是重新安装 （**reinstall**）, 这就对了！

[linux](https://www.archlinux.org/packages/?name=linux) 和 [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) 需要安, [linux-docs](https://www.archlinux.org/packages/?name=linux-docs) 则随意.

通过这个方法, 外部内核模块 (例如 [nvidia](https://www.archlinux.org/packages/?name=nvidia) 和 [virtualbox](https://www.archlinux.org/packages/?name=virtualbox)) 就不需要被重新编译了.

### Systemtap

从 [AUR](/index.php/AUR "AUR") 中安装systemtap即可: [systemtap](https://aur.archlinux.org/packages/systemtap/)<sup><small>AUR</small></sup>, 完成.

## 编译自定义内核

参考这个 [官方README](http://sourceware.org/git/?p=systemtap.git;a=blob_plain;f=README;hb=HEAD)

Retrieved from "[https://wiki.archlinux.org/index.php?title=SystemTap_(简体中文)&oldid=415645](https://wiki.archlinux.org/index.php?title=SystemTap_(简体中文)&oldid=415645)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Kernel (简体中文)](/index.php/Category:Kernel_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Kernel (简体中文)")