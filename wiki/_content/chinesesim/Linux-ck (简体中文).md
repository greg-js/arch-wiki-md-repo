**Linux-ck and headers**

*   当前版本:**3.7.6-2**
*   BFS CPU 调度器: v0.427
*   CK 补丁集: 3.7-ck1
*   发行日期: 07-Feb-2013

## Contents

*   [1 通用包细节](#.E9.80.9A.E7.94.A8.E5.8C.85.E7.BB.86.E8.8A.82)
    *   [1.1 发布周期](#.E5.8F.91.E5.B8.83.E5.91.A8.E6.9C.9F)
    *   [1.2 包默认信息](#.E5.8C.85.E9.BB.98.E8.AE.A4.E4.BF.A1.E6.81.AF)
*   [2 安装选项](#.E5.AE.89.E8.A3.85.E9.80.89.E9.A1.B9)
    *   [2.1 1\. 从源代码编译](#1._.E4.BB.8E.E6.BA.90.E4.BB.A3.E7.A0.81.E7.BC.96.E8.AF.91)
    *   [2.2 2\. 使用编译好的包](#2._.E4.BD.BF.E7.94.A8.E7.BC.96.E8.AF.91.E5.A5.BD.E7.9A.84.E5.8C.85)
        *   [2.2.1 通用和优化的内核包](#.E9.80.9A.E7.94.A8.E5.92.8C.E4.BC.98.E5.8C.96.E7.9A.84.E5.86.85.E6.A0.B8.E5.8C.85)
        *   [2.2.2 添加源到 /etc/pacman.conf](#.E6.B7.BB.E5.8A.A0.E6.BA.90.E5.88.B0_.2Fetc.2Fpacman.conf)
        *   [2.2.3 安装范例](#.E5.AE.89.E8.A3.85.E8.8C.83.E4.BE.8B)
        *   [2.2.4 怎样启用 BFQ I/O 调度器](#.E6.80.8E.E6.A0.B7.E5.90.AF.E7.94.A8_BFQ_I.2FO_.E8.B0.83.E5.BA.A6.E5.99.A8)
            *   [2.2.4.1 全局(对所有设备)](#.E5.85.A8.E5.B1.80.28.E5.AF.B9.E6.89.80.E6.9C.89.E8.AE.BE.E5.A4.87.29)
            *   [2.2.4.2 选择(对指定设备)](#.E9.80.89.E6.8B.A9.28.E5.AF.B9.E6.8C.87.E5.AE.9A.E8.AE.BE.E5.A4.87.29)
*   [3 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [3.1 与 Linux-ck 运行 Virtualbox](#.E4.B8.8E_Linux-ck_.E8.BF.90.E8.A1.8C_Virtualbox)
    *   [3.2 论坛支持](#.E8.AE.BA.E5.9D.9B.E6.94.AF.E6.8C.81)
*   [4 Package Trivia/Repo Statistics](#Package_Trivia.2FRepo_Statistics)
*   [5 一点关于 BFS 的说明](#.E4.B8.80.E7.82.B9.E5.85.B3.E4.BA.8E_BFS_.E7.9A.84.E8.AF.B4.E6.98.8E)
    *   [5.1 BFS 设计目标](#BFS_.E8.AE.BE.E8.AE.A1.E7.9B.AE.E6.A0.87)
    *   [5.2 一个排队论的视频](#.E4.B8.80.E4.B8.AA.E6.8E.92.E9.98.9F.E8.AE.BA.E7.9A.84.E8.A7.86.E9.A2.91)
    *   [5.3 Some Performance-Based Metrics: BFS vs. CFS](#Some_Performance-Based_Metrics:_BFS_vs._CFS)
*   [6 更多关于 BFS 和 CK 补丁集的内容](#.E6.9B.B4.E5.A4.9A.E5.85.B3.E4.BA.8E_BFS_.E5.92.8C_CK_.E8.A1.A5.E4.B8.81.E9.9B.86.E7.9A.84.E5.86.85.E5.AE.B9)
*   [7 Linux-ck Package Changelog](#Linux-ck_Package_Changelog)

## 通用包细节

[Linux-ck](https://aur.archlinux.org/packages/Linux-ck/) 是 [AUR](/index.php/AUR "AUR") 中的一个包，在[非官方 linux-ck 源](#2._.E4.BD.BF.E7.94.A8.E7.BC.96.E8.AF.91.E5.A5.BD.E7.9A.84.E5.8C.85)中允许用户运行一个定制的内核/头文件，基于 Con Kolivas 的 ck1 补丁集，包括 Brain Fuck Scheduler (BFS)。许多 Archer 选择使用这个包，因为 BFS 在任意负载状况下都具有优异的桌面交互性能和敏捷反应特性。

### 发布周期

Linux-ck大致跟随官方Arch内核的发布周期。 但受以下要求的限制：

*   上游代码
*   CK的补丁集
*   BFQ补丁集
*   ARCH config/config.x86_64只为主要版本设置

### 包默认信息

默认对config文件有**三个**修改:

1.  ck补丁集的开启或禁用选项。
2.  不需要人工干预的编译BFQ补丁集选项。
3.  应用 [GCC 补丁](https://github.com/graysky2/kernel_gcc_patch) 来启用编译时可选 CPU 优化 (这些选项不是标准 linux-ck 软件包的选项，只有用户启用自定义选项时编译才可用)。

**所有其他选项都和ARCH官方默认内核的主要内核config文件一致！**当然，用户可以自由地修改它们。linux-ck包包括一个选项切换**nconfig**config编辑器 (详细见下一节). 从CK的[BFS 设置 FAQ](http://ck.kolivas.org/patches/bfs/bfs-configuration-faq.txt)获取一些建议。

## 安装选项

**注意:** 与其他**可选**内核一样，如果使用的是 [GRUB](/index.php/GRUB "GRUB")，用户需要手动编辑 `/boot/grub/menu.lst` 如果使用 [GRUB2](/index.php/GRUB2 "GRUB2")，可以通过 "grub-mkconfig -o /boot/grub/grub.cfg" 更新 `/boot/grub/grub.cfg`为 linux-ck 添加一个新条目。

用户有两个选项得到这些内核包。

### 1\. 从源代码编译

[AUR](/index.php/AUR "AUR") 包含了上面提到的各个包。根据需要下载并安装其他的 AUR 包。

用户通过调整 PKGBUILD 中的选项可以自定义 linux-ck 包：

*   可选的 nconfig 可以提供用户指定的调节选项(Optional nconfig for user specific tweaking.)
*   选择通过一个 make localmodconfig 编译一个最小模块集合(Option to compile a minimal set of modules via a make localmodconfig.)
*   选择传递标准的 ARCH 配置选项或者简单的使用当前内核的 .config 文件
*   可选设置[BFQ I/O 调度器](http://algo.ing.unimo.it/people/paolo/disk_sched/)为默认值

更多细节可见 PKGBUILD 文件中的注释。如果从 AUR 编译一定要仔细阅读。

**注意:** 在 AUR 中有一些 PKGBUILD 提供其他适用于 linux-ck 的通用模块。例如 [nvidia-ck](https://aur.archlinux.org/packages/nvidia-ck/), [lirc-ck](https://aur.archlinux.org/packages/lirc-ck/), 和 [broadcom-wl-ck](https://aur.archlinux.org/packages/broadcom-wl-ck/).

### 2\. 使用编译好的包

如果用户不想花费时间自己编译，一个由 [graysky](/index.php/User:Graysky "User:Graysky") 维护的非官方源可以使用。

**注意:** 源中的包包含了作为模块编译的 BFQ I/O 调度器。如果你想加载或启用它，阅读下面的[小节](#.E6.80.8E.E6.A0.B7.E5.90.AF.E7.94.A8_BFQ_I.2FO_.E8.B0.83.E5.BA.A6.E5.99.A8)。

[[Graysky 的公钥](http://pgp.mit.edu:11371/pks/lookup?op=get&search=0x6D605D846176ED4B)]被用来为包签名。Pacman v4 会自动请求这个公钥服务器，但是如果你想手动下载和添加这个公钥，从上面的链接下载。

#### 通用和优化的内核包

这个源包含了通用的包以及针对 CPU 的包。许多 ARCH 用户很熟悉通用包的概念。官方的 ARCH 内核包含两种口味(i686 或者 x86_64)，它们都是**通用**的包，i686 可以在**任何**兼容的 x86 CPU 上使用，x86_64 可以在**任何**兼容的 x86_64 CPU 上使用。

这个源为用户提供了在通用的 linux-ck 包和针对 CPU 优化过的包之间的选择：

_通用的_

*   **ck-generic** ==> 使用通用的优化选项编译，适合**任何**兼容的 CPU，与官方的 ARCH linux 包一样。这对于 Intel 和 AMD 芯片都是适用的。

_针对 CPU 优化的_

*   **ck-atom** ==> Intel Atom 平台针对性优化。 Intel Atom CPUs 有一个按顺序的流水线架构，因此会从据此优化过的代码获益。
*   **ck-corex** ==> Intel Core 2 系列，包括 Dual 和 Quads (Core 2/新 Xeon/基于 Core2 的 Mobile Celeron) 以及 Core i3/i5/i7 系列针对性的优化 (Gulftown, Bloomfield, Lynnfield, Clarksfield, Arrendale, 和 Sandy/Ivybridge CPU).
*   **ck-kx** ==> AMD K7 (Athlon/Athlon XP)/K8 (Athlon 64, Athlon 64 X2, 23xx Quad-Core Barcelona, Sempron, Sempron 64)/K10 系列 (Athlon X2 7x50, Phenom X3/X4, Phenom II, Athlon II X2/X3/X4, Sempron 64 (Socket AM3 only), 61xx Eight-Core Magny-Cours) 针对性的优化。允许使用一些扩展的指令集，同时向 GCC 传递了合适的优化标志。
*   **ck-p4** ==> Intel Pentium-4 针对性的优化 (P4/基于 P4 的 Celeron/Pentium-4 M/旧 Xeon).
*   **ck-pentm** ==> Intel Pentium-M 针对性的优化 (Pentium-M 笔记本芯片/非 Pentium-4 M).

CPU-specific optimization are invoked at compilation by selecting the corresponding option under **Processor type and features>Processor family** or by setting-up the .config file accordingly. These changes setup make specific gcc options including the $CFLAGS. For more, see the following files:

*   $srcdir/linux-$pkgver/arch/x86/[Makefile](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob;f=arch/x86/Makefile;h=b02e509072a790b1fbea3387f8749b5326beb822;hb=HEAD)
*   $srcdir/linux-$pkgver/arch/x86/[Makefile_32](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob;f=arch/x86/Makefile_32.cpu;h=86cee7b749e1bc387522752ba2a5f200ccc172c0;hb=HEAD)

#### 添加源到 `/etc/pacman.conf`

1) 添加下面的代码到 `/etc/pacman.conf` (我把这个条目放在文件末尾):

```
[repo-ck]
Server = [http://repo-ck.com/$arch](http://repo-ck.com/$arch)

```

2) 添加验证Key（本项目来自[ck内核官网](http://repo-ck.com/) ，原条目没有此项，导致无法通过签名验证，无法安装。）

```
# pacman-key -r 5EE46C4C && pacman-key --lsign-key 5EE46C4C

```

3) 通过 _pacman -Syy_ 刷新

完成了。想查看这个源的内容，这样搜索：

```
# pacman -Sl repo-ck

```

#### 安装范例

使用 **ck-X** 组，然后选择想要安装的包。有6个组包含了6个包集合。**ck-generic, ck-atom, ck-corex, ck-kx, ck-p4,** 和 **ck-pentm**.

```
# pacman -S ck-generic
:: There are 4 members in group ck-generic:
:: Repository repo-ck
   1) broadcom-wl-ck  2) linux-ck  3) linux-ck-headers  4) nvidia-ck

Enter a selection (default=all):
```

另外，也可以直接用 Pacman 安装包：

```
# pacman -S linux-ck linux-ck-headers

```

#### 怎样启用 BFQ I/O 调度器

从版本 3.0.4-2 开始，BFQ 补丁集默认被应用到包中。用户必须启用 BFQ 调度器才能使用它，默认是处于休眠状态。

##### 全局(对所有设备)

追加 "elevator=bfq" 到 `/boot/grub/menu.lst` 内核启动行中(如果你使用 grub)或者在 `/etc/default/grub` 中的**GRUB_CMDLINE_LINUX_DEFAULT="quiet"** 一行下面，然后通过标准的 "grub-mkconfig -o /boot/grub/grub.cfg" 命令，重新编译 `/boot/grub/grub.cfg`

##### 选择(对指定设备)

设定内核逐个设备使用。例如，如果想为 `/dev/sda` 启用只需要：

```
# echo bfq > /sys/block/sda/queue/scheduler

```

想验证一下，只需要 _cat_ 同一个文件：

```
# cat /sys/block/sda/queue/scheduler
noop deadline cfq [bfq] 

```

**注意:** 这种方法在重启后会失效。想要下次启动自动更改，把 echo 这行命令放在 `/etc/rc.local`

**注意:** 从 AUR 编译包的用户在 PKGBUILD 中会有一个选项全局启用 BFQ 作为默认的 I/O 调度器。

## 疑难解答

### 与 Linux-ck 运行 Virtualbox

Virtualbox works just fine with custom kernels such as Linux-ck _without_ the need to keep any of the official ARCH kernel packages on the system (i.e. linux and linux-headers from [core]). The trick to keeping pacman from bringing down the ARCH kernel packages is to install virtualbox with the virtualbox-source package. Why? Wonder kindly responded to [FS#26721](https://bugs.archlinux.org/task/26721).

```
# pacman -S virtualbox virtualbox-source

```

After pacman finishes, simply generate the kernel modules (for linux-ck) like this (assuming the system is booted into the linux-ck kernel):

```
# /usr/bin/vboxbuild

```

### 论坛支持

Please use [this discussion thread](https://bbs.archlinux.org/viewtopic.php?id=111715) to voice comments, questions, suggestions, requests, etc. Note from graysky, "I can add other CPU-specific builds upon request. I just wanna be sure people will actually use them if I take the time to compile them."

## Package Trivia/Repo Statistics

*   Various package sets are compiled via a Bash wrapper script for makepkg. The script is publicly accessible at graysky's [github](https://github.com/graysky2/repo-ck) repo.
*   Repo [statistics](http://repo-ck.com/stats.pdf) are available (popularity of packages, which CPU is most popular, # of downloads, etc.).

**Note:** The statistics are not updated daily but do give a snapshot of the data.

## 一点关于 BFS 的说明

### BFS 设计目标

BFS 有两个主要的设计目标：

1.  获得极佳的桌面交互和响应性能，同时不使用启发式的，或者是难以理解、无法建模和预测效果、当调度到一个任务时会影响到另一个任务的调度机制。
2.  完全抛弃传统的cpu进程调度器的复杂设计，实现一个从底层就很简洁的调度器。

参见本文的 [#更多关于 BFS 和 CK 补丁集的内容](#.E6.9B.B4.E5.A4.9A.E5.85.B3.E4.BA.8E_BFS_.E5.92.8C_CK_.E8.A1.A5.E4.B8.81.E9.9B.86.E7.9A.84.E5.86.85.E5.AE.B9) 部分获取更多信息。

### 一个排队论的视频

See [this video](http://www.youtube.com/watch?v=F5Ri_HhziI0) about queuing theory for an interesting parallel with supermarket checkouts. Quote from CK, "the relevance of that video is that BFS uses a single queue, whereas the mainline Linux kernel uses a multiple queue design. The people are tasks, and the checkouts are CPUs. Of course there's a lot more to a CPU scheduler than just the queue design, but I thought this video was very relevant."

### Some Performance-Based Metrics: BFS vs. CFS

A major benefit of using the BFS is increased responsiveness. The benefits however, are not limited to desktop feel. [Graysky](/index.php/User:Graysky "User:Graysky") put together some non-responsiveness based benchmarks to compare it to the CFS contained in the "stock" linux kernel. Recognize however, that it was not implicitly designed to provide superior performance. The purpose of the benchmarks was to evaluate the CPU scheduler in the stock Linux kernel against the BFS in the corresponding kernel patched with the ck1 patchset on different machines to see if differences exist and to what degree they scale using **performance based metrics** even though these end points were never within the scope of primary design goals of the BFS.

It is noteworthy to mention that this is not a novel idea, Phoronix also benchmarking using non-latency based endpoints about which Con subsequently [blogged](http://ck-hack.blogspot.com/2011/08/phoronix-revisits-bfs.html).

[[Benchmark results](http://repo-ck.com/bench/benchmark.pdf)] are available for download in pdf format.

For those not wanting to see the data and just wanting the highlights:

*   7 different machines ranging from 1 to 16 cores were benchmark using both a make and a x264-based video benchmark.
*   Each machine ran both the "standard" linux kernel (linux-3.0.1-2 from [core]) and the ck1-patched version of this kernel (linux-ck-3.0.6-2 from graysky's unofficial repo).
*   All 7 machines preformed better using the linux-ck package on the make benchmark.
*   x264 encoding results were mixed. 4 machines performed better on the BFS scheduler; 1 gave same results; and 3 performed worse. It should be noted that an experimental version (svn) of handbrake was used for these tests.

## 更多关于 BFS 和 CK 补丁集的内容

*   [Con Kolivas' White Paper on the BFS](http://ck.kolivas.org/patches/bfs/sched-BFS.txt)
*   [Con Kolivas' BFS FAQ](http://ck.kolivas.org/patches/bfs/bfs-faq.txt)
*   [Wikipedia's BFS Article](http://en.wikipedia.org/wiki/Brain_Fuck_Scheduler)
*   [Con Kolivas' Blog](http://ck-hack.blogspot.com/)

## [Linux-ck Package Changelog](/index.php/Linux-ck/Changelog "Linux-ck/Changelog")