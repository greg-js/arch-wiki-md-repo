**翻译状态：** 本文是英文页面 [Intel_C++](/index.php/Intel_C%2B%2B "Intel C++") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-12-09，点击[这里](https://wiki.archlinux.org/index.php?title=Intel_C%2B%2B&diff=0&oldid=239486)可以查看翻译后英文页面的改动。

## Contents

*   [1 在开始之前](#.E5.9C.A8.E5.BC.80.E5.A7.8B.E4.B9.8B.E5.89.8D)
*   [2 设置和安装](#.E8.AE.BE.E7.BD.AE.E5.92.8C.E5.AE.89.E8.A3.85)
*   [3 通过makepkg使用ICC](#.E9.80.9A.E8.BF.87makepkg.E4.BD.BF.E7.94.A8ICC)
    *   [3.1 方法 1 (2012年12月08日)](#.E6.96.B9.E6.B3.95_1_.282012.E5.B9.B412.E6.9C.8808.E6.97.A5.29)
*   [4 icc CFLAGS](#icc_CFLAGS)
    *   [4.1 -xX](#-xX)
    *   [4.2 -Ox](#-Ox)
    *   [4.3 -w](#-w)
*   [5 用Intel C / C++编译的软件](#.E7.94.A8Intel_C_.2F_C.2B.2B.E7.BC.96.E8.AF.91.E7.9A.84.E8.BD.AF.E4.BB.B6)

## 在开始之前

**Note:** 通过ICC编译的软件，必须包含 **intel-openmp**库才能运行. 由于 **intel-openmp** 依赖 **intel-compiler-base**，用户必须在任何时候都安装有这两个包！

## 设置和安装

[intel-parallel-studio-xe](https://aur.archlinux.org/packages/intel-parallel-studio-xe/) 位于 [AUR](/index.php/AUR "AUR"). 为了构建这个包，用户必须有一个许可文件，这个许可文件对个人和非商业用途免费。 这份许可文件可以通过电子邮件发送给用户 [注册](https://registrationcenter.intel.com/RegCenter/AutoGen.aspx?ProductID=1517&AccountID=&EmailID=&ProgramID=&RequestDt=&rm=NCOM&lang=) 并且应该在运行mkaepkg前复制到 $startdir 里. 当前的PKGBUILD需要7到8个包:

*   **intel-compiler-base** - Intel C/C++ 编译器和基本库
*   **intel-fortran-compiler** - Intel fortran 编译器和基本库 (仅 Parallel Studio XE)
*   **intel-openmp** - Intel OpenMP 库
*   intel-idb- Intel C/C++ 调试器
*   intel-ipp - Intel 集成性能原件
*   intel-mkl - Intel 数学核心库 (Intel® MKL)
*   intel-sourcechecker - Intel 源代码检测器
*   intel-tbb - Intel 线程构建模块 (TBB)

**Note:** 至少需要两个标为**粗体**的包.

## 通过makepkg使用ICC

**Note:** 不是每个包都能在不大量修改源代码的情况下通过ICC编译。

目前没有通过makepkg运行ICC的官方指南。本节的目的是收集用户使用的各种方法。如果您愿意提出您宝贵的建议，请将您的建议建立一个新的小节。

### 方法 1 (2012年12月08日)

修改`/etc/makepkg.conf` 中的**CXXFLAGS**以使makepkg使用ICC。 在现有的文件里添加以下代码。调用makepkg时不需要什么特殊的开关。

```
_CC=icc
if [ $_CC = "icc" ]; then
export CC="icc"
export CXX="icpc"
export CFLAGS="-march=native -O3 -no-prec-div -fno-alias -pipe"
export CXXFLAGS="${CFLAGS}"
export LDFLAGS="-Wl,-O1,--sort-common,--as-needed"
export AR="xiar"
export LD="xild"
fi
```

**Note:** 可以简单地通过注释 **_CC**变量切换GCC或ICC。

**Note:** 如果用以上的方法编译失败请使用 *gcc*编译, 所以你应该测试你的程序是否能用 *icc*正确编译。

测试你的软件是否真的是用ICC编译的:

*   输入命令 **ldd [你的程序] | grep intel** 如果这个程序连接到一个位于 **/opt/intel/lib/**中的共享库，那么它就是ICC编译的。

*   另一种方法是观察编译时的输出，看他是否使用了*icc* 或者 *icpc* 命令。

*   最后一种方法是看警告信息是不是*icc*风格的。

## icc CFLAGS

In general, icc supports many of the same CFLAGS gcc supports and is also pretty tolerant to gcc flags it cannot use. In most cases it will happily ignore the flag warning the user and moving on. For an exhaustive list and explanation of available compiler flags, consult the icc manpage or better yet by invoking the compiler with the help flag:

```
icc --help

```

### -xX

Use to generate specialized code to run exclusively on processors supporting it. If unsure which option to use, simply inspect the **flags** section of `/proc/cpuinfo`. In the example below, **SSE4.1** would be the correct selection:

```
$ cat /proc/cpuinfo  | grep -m 1 flags
flags: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush 
dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx lm constant_tsc arch_perfmon pebs 
bts rep_good nopl aperfmperf pni dtes64 monitor ds_cpl vmx smx est tm2 ssse3 cx16 xtpr
pdcm sse4_1 lahf_lm dts tpr_shadow vnmi flexpriority
```

*   -xHost
*   -xSSE2
*   -xSSE3
*   -xSSSE3
*   -xSSE4.1
*   -xSSE4.2
*   -xAVX
*   -xCORE-AVX-I
*   -xSSSE3_ATOM

**Tip:** 使用 **-xHost** 如果你不确定你的处理器支持什么。

### -Ox

和gcc一样. x 是下列选上之一:

*   0 - 不进行优化
*   1 - 优化以使得执行速度变快，但是不进行那些增加代码但是提高速度有限的优化
*   2 - 缺省，优化以使得执行速度变快
*   3 - 优化以使得执行速度最快，除了O2的优化外，还包含一些比较激进的优化（不是对所有程序都会提高性能）

### -w

与gcc类似:

*   -w - 关闭所有警告 (推荐在编译包时使用)
*   -Wbrief - print brief one-line diagnostics
*   -Wall - 开启所有警告
*   -Werror - 强制将警告视为错误

## 用Intel C / C++编译的软件

在下面的表格中我们发布了一个我们用Intel C/C++ 编译器尝试过编译的包列表 .应该可以用ABS取得源码。

| Application | Compile | Comments |
| **xz** | OK | Works with the [Method 1](/index.php/Intel_C%2B%2B#Method_1 "Intel C++") |
| **zlib** | OK | Works with the [Method 1](/index.php/Intel_C%2B%2B#Method_1 "Intel C++") |
| **GIMP 2.8** | OK | Works with the [Method 1](/index.php/Intel_C%2B%2B#Method_1 "Intel C++") |
| **Pacman 4.0.3** | OK | Works with the [Method 1](/index.php/Intel_C%2B%2B#Method_1 "Intel C++") |
| **x264** | OK | Works with the [Method 1](/index.php/Intel_C%2B%2B#Method_1 "Intel C++") |
| **MySQL** | OK | Works with the [Method 1](/index.php/Intel_C%2B%2B#Method_1 "Intel C++") |
| **SQLite** | OK | Works with the [Method 1](/index.php/Intel_C%2B%2B#Method_1 "Intel C++") |
| **LAME** | OK | Works with the [Method 1](/index.php/Intel_C%2B%2B#Method_1 "Intel C++") |
| **xaos** | OK | Works with the [Method 1](/index.php/Intel_C%2B%2B#Method_1 "Intel C++") |
| **VLC** | Out of date | There's some problem with the compiler flags |
| **MPlayer** | Out of date | It don't recognize the Intel compiler |
| **optipng** | OK | Works with the [Method 1](/index.php/Intel_C%2B%2B#Method_1 "Intel C++"). Comment out LD=xild in makepkg.conf |
| **python-numpy** | OK | We must edit the PKGBUILD. [python-numpy-mkl](https://aur.archlinux.org/packages/python-numpy-mkl/) |
| **python-scipy** | OK | We must edit the PKGBUILD. [python-scipy-mkl](https://aur.archlinux.org/packages/python-scipy-mkl/) |
| **Qt** | OK | We must add the option *-platform linux-icc-64 (or 32)* in the configure command |
| **systemd** | Fail | undefined reference to `server_dispatch_message' |

**图例:**

| OK | 可以用icc编译并且工作 |
| OK | 可以用icc编译并且工作，但是需要编辑PKGBUILD |
| Unsuccessful | 可以编译，但有错误 |
| Not recommended | 可以编译，但不推荐 |
| Fail | 无法使用ICC编译这个包 |
| Out of date | 用以前的CFLAGS不成功，你可以试试新的[方法1](#Method_1)，别忘了把结果贴上来！ |