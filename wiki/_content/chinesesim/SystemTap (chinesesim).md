**翻译状态：** 本文是英文页面 [Systemtap](/index.php/Systemtap "Systemtap") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-12-25，点击[这里](https://wiki.archlinux.org/index.php?title=Systemtap&diff=0&oldid=512991)可以查看翻译后英文页面的改动。

[Systemtap](http://sourceware.org/systemtap/) 是一种在运行时收集 Linux 系统信息的自由软件(GPL)框架。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 SystemTap](#SystemTap)
*   [2 标准内核](#标准内核)
*   [3 内核重新编译](#内核重新编译)
    *   [3.1 Prepare](#Prepare)
    *   [3.2 修改config文件](#修改config文件)
    *   [3.3 更新校验值](#更新校验值)
    *   [3.4 编译并安装](#编译并安装)
    *   [3.5 Systemtap](#Systemtap_2)
*   [4 编译自定义内核](#编译自定义内核)
*   [5 问题处理](#问题处理)
    *   [5.1 版本匹配问题](#版本匹配问题)
    *   [5.2 System.map is missing](#System.map_is_missing)
    *   [5.3 Process return probes not available](#Process_return_probes_not_available)

## SystemTap

安装 [systemtap](https://aur.archlinux.org/packages/systemtap/) 或 [systemtap-git](https://aur.archlinux.org/packages/systemtap-git/)。和上游版本的对比：[[1]](https://sourceware.org/systemtap/wiki/SystemTapReleases).

要从源代码编译，请访问 [这里](https://sourceware.org/git/?p=systemtap.git;a=summary)。最新代码会包含新内核版本和发行版的支持。

## 标准内核

至少需要安装软件包 [linux-headers](https://www.archlinux.org/packages/?name=linux-headers)。

Arch 会从发布的二进制文件,包括内核中删除调试数据。很多 systmetap 功能就不能使用了。[stapprobes 手册](https://sourceware.org/systemtap/man/stapprobes.3stap.html)记录了 NON-DWARF 和 AUTO-DWARF 类型下什么功能可用：

*   kernel tracepoints: kernel.trace("*")
*   user-space probes: process("...").function("...") (for programs you build yourself with -g)
*   user-space markers: process("...").mark("...") (if they were configured with the *<sys/sdt.h>* markers)
*   perfctr-based probes: perf.*
*   non-dwarf kernel probes: kprobe.function("...") and nd_syscall.* tapset (if a /boot/System.map* file is available, see below).

## 内核重新编译

可用自定义 *linux-custom* 软件包之后再运行 SystemTap。重新编译 [linux](https://www.archlinux.org/packages/?name=linux) 软件包也非常方便。参考 [Kernels/Traditional compilation](/index.php/Kernels/Traditional_compilation "Kernels/Traditional compilation")。

### Prepare

First, run `cd ~/ && mkdir build && cd build/ && asp checkout linux && cd linux/trunk` to get the original kernel build files. Then use `makepkg --verifysource` to get the additional files. By performing the verification, you can safely **skip** the steps on "Update checksum".

### 修改config文件

编辑 **config** (32位内核) 或 **config.x86_64** (64位内核), 确保打开这些选项:

*   CONFIG_KPROBES=y
*   CONFIG_KPROBES_SANITY_TEST=n
*   CONFIG_KPROBE_EVENT=y
*   CONFIG_NET_DCCPPROBE=m
*   CONFIG_NET_SCTPPROBE=m
*   CONFIG_NET_TCPPROBE=y
*   CONFIG_DEBUG_INFO=y
*   CONFIG_DEBUG_INFO_REDUCED=n
*   CONFIG_X86_DECODER_SELFTEST=n
*   CONFIG_DEBUG_INFO_VTA=y

默认只有*CONFIG_DEBUG_INFO* 和*CONFIG_DEBUG_INFO_REDUCED*没被打开，修改这两个即可.

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

从 [AUR](/index.php/AUR "AUR") 中安装systemtap即可: [systemtap](https://aur.archlinux.org/packages/systemtap/), 完成.

## 编译自定义内核

参考这个 [官方README](http://sourceware.org/git/?p=systemtap.git;a=blob_plain;f=README;hb=HEAD)

## 问题处理

### 版本匹配问题

如果出现如下错误：

```
   /usr/share/systemtap/runtime/stat.c:214:2: error: 'cpu_possible_map' undeclared (first use in this function)

```

请安装 systemtap-git。

### System.map is missing

You can recover it where you build your linux kernel with DEBUG_INFO enabled

```
   cp src/linux-3.6/System.map /boot/System.map-3.6.7-1-ARCH

```

Alternately,

```
   sudo cp /proc/kallsyms /boot/System.map-`uname -r`

```

### Process return probes not available

If you are sure that your kernel configuration is correct, but on launching `stap` you get **both** of the following messages:

```
   WARNING: Kernel function symbol table missing [man warning::symbols]

```

```
   semantic error: process return probes not available [man error::inode-uprobes]

```

then SystemTap may have failed to verify support for this feature. You can fix this by following the steps in [System.map is missing](#System.map_is_missing).