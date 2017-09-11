相关文章

*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [PKGBUILD (简体中文)](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)")
*   [.SRCINFO](/index.php/.SRCINFO ".SRCINFO")
*   [Arch User Repository (简体中文)](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")
*   [pacman (简体中文)](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")
*   [Official repositories (简体中文)](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")
*   [Arch Build System (简体中文)](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)")

**翻译状态：** 本文是英文页面 [Makepkg](/index.php/Makepkg "Makepkg") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-04-07，点击[这里](https://wiki.archlinux.org/index.php?title=Makepkg&diff=0&oldid=428988)可以查看翻译后英文页面的改动。

[makepkg](https://projects.archlinux.org/pacman.git/tree/scripts/makepkg.sh.in)是一个软件包自动编译脚本。使用时需要一个 Unix 环境和 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

makepkg 是由 [pacman](https://www.archlinux.org/packages/?name=pacman) 包提供的。

## Contents

*   [1 配置](#.E9.85.8D.E7.BD.AE)
    *   [1.1 打包人信息](#.E6.89.93.E5.8C.85.E4.BA.BA.E4.BF.A1.E6.81.AF)
    *   [1.2 包输出](#.E5.8C.85.E8.BE.93.E5.87.BA)
    *   [1.3 验证签名](#.E9.AA.8C.E8.AF.81.E7.AD.BE.E5.90.8D)
*   [2 使用](#.E4.BD.BF.E7.94.A8)
*   [3 使用技巧](#.E4.BD.BF.E7.94.A8.E6.8A.80.E5.B7.A7)
    *   [3.1 体系结构，编译标志](#.E4.BD.93.E7.B3.BB.E7.BB.93.E6.9E.84.EF.BC.8C.E7.BC.96.E8.AF.91.E6.A0.87.E5.BF.97)
        *   [3.1.1 MAKEFLAGS](#MAKEFLAGS)
    *   [3.2 生成新 md5sums](#.E7.94.9F.E6.88.90.E6.96.B0_md5sums)
    *   [3.3 减少编译时间](#.E5.87.8F.E5.B0.91.E7.BC.96.E8.AF.91.E6.97.B6.E9.97.B4)
        *   [3.3.1 tmpfs](#tmpfs)
        *   [3.3.2 ccache](#ccache)
    *   [3.4 生成新校验和](#.E7.94.9F.E6.88.90.E6.96.B0.E6.A0.A1.E9.AA.8C.E5.92.8C)
    *   [3.5 创建非压缩软件包](#.E5.88.9B.E5.BB.BA.E9.9D.9E.E5.8E.8B.E7.BC.A9.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [3.6 Utilizing multiple cores on compression](#Utilizing_multiple_cores_on_compression)
    *   [3.7 Build 32-bit packages on a 64-bit system](#Build_32-bit_packages_on_a_64-bit_system)
*   [4 问题处理](#.E9.97.AE.E9.A2.98.E5.A4.84.E7.90.86)
    *   [4.1 Makepkg sometimes fails to sign a package without asking for signature passphrase](#Makepkg_sometimes_fails_to_sign_a_package_without_asking_for_signature_passphrase)
    *   [4.2 CFLAGS/CXXFLAGS/CPPFLAGS in makepkg.conf do not work for QMAKE based packages](#CFLAGS.2FCXXFLAGS.2FCPPFLAGS_in_makepkg.conf_do_not_work_for_QMAKE_based_packages)
    *   [4.3 Specifying install directory for QMAKE based packages](#Specifying_install_directory_for_QMAKE_based_packages)
    *   [4.4 WARNING:Referencing $srcdir in PKGBUILD](#WARNING:Referencing_.24srcdir_in_PKGBUILD)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 配置

makepkg 的详细配置选项可以通过 [makepkg.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/makepkg.conf.5) 查询。

`/etc/makepkg.conf` 是 makepkg 的主配置文件。用户的自定义配置位于 `$XDG_CONFIG_HOME/pacman/makepkg.conf` 或 `~/.makepkg.conf`. 建议用户在编译软件包之前检查 makepkg 配置。

### 打包人信息

每个软件包都会有元数据信息，其中就包含 *packager*. 默认情况下，用户自己打包的软件标记为 `Unknown Packager`. 如果多个用户会在系统上编译，或者需要发布软件包给其他人，最好提供真实的联系人。可以通过 `makepkg.conf` 中的 `PACKAGER` 变量设置。

检查安装软件包的打包人：

 `pacman -Qi package` 
```
...
Packager       : Unknown Packager
...

```

修改之后：

 `pacman -Qi package` 
```
...
Packager       : John Doe <john@doe.com>
...

```

要自动签名过程，请同时在 `makepkg.conf` 中设置 `GPGKEY` 变量.

### 包输出

*makepkg* 默认会在工作目录创建软件包，并把源代码下载到 `src/` 目录。可以配置到自定义的路径，比如所有安装的软件包放到 `~/build/packages/`，所有源代码放到 `~/build/sources/`.

配置以下`makepkg.conf`,如果需要配置变量:

*   `PKGDEST` — 目录中存储产生的包
*   `SRCDEST` — 目录中存储的[source](/index.php/PKGBUILD#source "PKGBUILD") 数据 (符号链接将被放置到 `src/` 如果点其他地方)
*   `SRCPKGDEST` —目录存储产生的源代码包 (构建用 `makepkg -S`)

### 验证签名

如果签名文件是以 `.sig` 或 `.asc` 形式作为 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 代码的一部分，makepkg 会自动[验证](/index.php/GnuPG#Verify_a_signature "GnuPG") 软件包. 如果用户未提供需要的签名公钥，*makepkg* 会停止安装过程并提示用户说无法验证 PGP 密钥。

如果缺少公钥或希望其他开发者进行签名，可以手动 [导入](/index.php/GnuPG#Import_a_key "GnuPG")或通过 [密钥服务器](/index.php/GnuPG#Use_a_keyserver "GnuPG") 导入。要临时禁用签名检查请在执行 makepkg 命令时加上 `--skippgpcheck` 选项。

**注意:** makepkg 中的签名验证并不使用 pacman 的密钥环, 而是使用用户的密钥。

## 使用

继续之前，确保 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 软件组已经安装。属于这个组的软件包不会列在 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 文件的依赖中。输入以下命令安装 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 软件包组 (用 root 运行)：

```
# pacman -S base-devel

```

**注意:** 在抱怨丢失(编译)依赖之前，记得 [base](https://www.archlinux.org/groups/x86_64/base/) 组是被视为在所有的 Arch Linux 系统中安装的。在使用 makepkg 编译时，[base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 组默认假设安装过。

要编译软件包，用户必须首先建立一个 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")，或者编译脚本(在 [创建软件包](/index.php/%E5%88%9B%E5%BB%BA%E8%BD%AF%E4%BB%B6%E5%8C%85 "创建软件包") 中有详细描述)，或者从 [ABS tree](/index.php/Arch_Build_System "Arch Build System")、 [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") 或其他来源获取。

**警告:** 只从信任的来源编译和/或安装软件包。

拥有一个 `PKGBUILD` 之后，切换到存放这个文件的目录，输入下面的命令编译 `PKGBUILD` 描述的软件包：

```
$ makepkg

```

如果需要的依赖不满足，makepkg 会输出一个警告然后失败。想要编译软件包然后自动安装必须的依赖，只需要输入以下命令：

```
$ makepkg -s

```

注意这些依赖必须在已配置的软件源之中。参见 [pacman#Repositories](/index.php/Pacman#Repositories "Pacman") 获取更多细节。另外，用户也可以在编译前手动安装需要的依赖(`pacman -S --asdeps dep1 dep2`)。

一旦所有的依赖都满足并且软件包成功编译，一个软件包文件 (`pkgname-pkgver.pkg.tar.xz`) 会在工作目录下创建。想安装，运行

```
$ makepkg -i

```

要清空残余的文件和目录，例如解压到 $srcdir 的文件，输入下面的选项。这对于在使用同一个文件夹多次编译同一个软件包或者升级软件包版本时很有用。它防止过期的或残余的文件呈递到新的编译任务中。

```
$ makepkg -c

```

更多信息请阅读[makepkg(8)](https://www.archlinux.org/pacman/makepkg.8.html).

## 使用技巧

### 体系结构，编译标志

在使用 makepkg 编译软件时，[make](https://www.archlinux.org/packages/?name=make), [gcc](https://www.archlinux.org/packages/?name=gcc) 和 `g++` 会使用 `MAKEFLAGS`, `CFLAGS` 和 `CXXFLAGS` 选项。默认情况下，这些选项产生的是通用的包，可以在不同的机器上安装。使用针对目标机器的设置，可以获得性能提升，但编译出的包也许无法在其他机器上运行。

**注意:** 记住不是所有的包创建系统都会使用你设置的变量。一些包的 Makefiles 或者 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")文件会覆盖设置。
 `/etc/makepkg.conf` 
```
...

#########################################################################
# ARCHITECTURE, COMPILE FLAGS
#########################################################################
#
CARCH="x86_64"
CHOST="x86_64-unknown-linux-gnu"

#-- Exclusive: will only run on x86_64
# -march (or -mcpu) builds exclusively for an architecture
# -mtune optimizes for an architecture, but builds for whole processor family
CFLAGS="-march=x86-64 -mtune=generic -O2 -pipe -fstack-protector --param=ssp-buffer-size=4 -D_FORTIFY_SOURCE=2"
CXXFLAGS="-march=x86-64 -mtune=generic -O2 -pipe -fstack-protector --param=ssp-buffer-size=4 -D_FORTIFY_SOURCE=2"
LDFLAGS="-Wl,-O1,--sort-common,--as-needed,-z,relro"
#-- Make Flags: change this for DistCC/SMP systems
#MAKEFLAGS="-j2"

...

```

默认的 makepkg.conf `CFLAGS` 和 `CXXFLAGS` 是与所有机器各自的体系结构兼容的。

在 x86_64 机器上，不要花费时间进行编译选项优化，绝大部分情况下优化效果都不明显。使用非标准的 CFLAGS 非常容易降低性能，因为编译器倾向于快速增大生成的文件，例如解开循环、错误的向量化和非理性的内联函数。除非通过测评得出性能提升的结论，否则最好不要做优化。

GCC 的手册页面有完整的选项列表。Gentoo [编译器优化指南](http://www.gentoo.org/doc/en/gcc-optimization.xml) 和 [安全 Cflags](http://wiki.gentoo.org/wiki/Safe_CFLAGS) wiki 文章提供了深入信息。

从 4.3.0 版本开始, GCC 可以进行 CPU 自动检测，可以在编译时自动选择本地机器支持的优化。要使用它，删除所有 `-march` 和 `-mtune`，然后添加 `-march=native`. 例如：

```
CFLAGS="-march=native -O2 -pipe -fstack-protector-strong"
CXXFLAGS="${CFLAGS}"

```

要查看`march=native`启用的选项，运行：

```
 $ gcc -march=native -v -Q --help=target

```

*   If you specify different value than `-march=native`, then `-Q --help=target` **will not** work as expected.[[1]](https://bbs.archlinux.org/viewtopic.php?pid=1616694#p1616694) You need to go through a compilation phase to find out which options are really enabled. See [Find CPU-specific options](https://wiki.gentoo.org/wiki/Safe_CFLAGS#Find_CPU-specific_options) on Gentoo wiki for instructions.

*   To find out the optimal options for a **32 bit** x86 architecture, you can use the script [gcccpuopt](https://github.com/pixelb/scripts/blob/master/scripts/gcccpuopt).

#### MAKEFLAGS

`MAKEFLAGS` 选项可以用来指定 make 的额外选项。使用多核系统的用户可以设定同时运行的任务数。可以用`nproc`获得可用处理器的个数，如果结果是 4， 则使用`-j4`. 有些 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 强制使用 `-j1`，因为某些版本会产生冲突或者软件包并不支持。如果出现软件包因为此原因无法编译，请在 bug 系统中[报告](/index.php/Reporting_bug_guidelines_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Reporting bug guidelines (简体中文)")。

完整的选项请阅读 [make(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/make.1)。

### 生成新 md5sums

从 [pacman 4.1](http://allanmcrae.com/2013/04/pacman-4-1-released/) pacman-contrib 和其中的 `updpkgsums` 已经 [合并](https://projects.archlinux.org/pacman.git/tree/NEWS) 进入 pacman，生成和替换 PKGBUILD 中的校验和:

```
$ updpkgsums

```

### 减少编译时间

#### tmpfs

编译过程需要大量的读写操作，要处理很多小文件。将工作目录移动到 [tmpfs](/index.php/Tmpfs "Tmpfs") 可以减少编译时间。

使用`BUILDDIR`变量可以临时将 *makepkg* 的编译目录设置到 tmpfs：

```
$ BUILDDIR=/tmp/makepkg makepkg

```

**Warning:** 编译大文件将导致内存不足。

修改 `makepkg.conf` 的 `BUILDDIR` 选项可以永久变更编译目录。Arch 的默认 tmpfs 目录是 `/tmp`. 此变量可以设置为：`BUILDDIR=/tmp/makepkg`。

**Note:**

*   [tmpfs](/index.php/Tmpfs "Tmpfs") 目录挂载时不能使用 `noexec` 选项，否则编译命令可能无法执行。
*   在 [tmpfs](/index.php/Tmpfs "Tmpfs") 中编译的文件重起后会消失，设置 [PKGDEST](#Package_output) 选项可以将编译结果保存到其它目录。

#### ccache

[ccache](/index.php/Ccache "Ccache") 可以将编译结果缓存起来，减少编译时间。

### 生成新校验和

Pacman 包含了 `updpkgsums` 脚本，可以生成新校验和并替换 PKGBUILD 中的内容，只需要执行：

```
$ updpkgsums

```

### 创建非压缩软件包

如果只是本地安装，可以用下面设置跳过 [LZMA2](https://en.wikipedia.org/wiki/xz "wikipedia:xz") 压缩和解压缩：

 `/etc/makepkg.conf` 
```
[...]
#PKGEXT='.pkg.tar.xz'
PKGEXT='.pkg.tar'
[...]
```

### Utilizing multiple cores on compression

[xz](https://www.archlinux.org/packages/?name=xz) supports [symmetric multiprocessing (SMP)](https://en.wikipedia.org/wiki/Symmetric_multiprocessing "wikipedia:Symmetric multiprocessing") on compression. This can be done by using the `-T 0`/`--threads=0` flag, which makes *xz* use as many threads as there are cores on the system:

 `/etc/makepkg.conf` 
```
[...]
 COMPRESSXZ=(xz -c -z - **--threads=0**)
[...]
```

### Build 32-bit packages on a 64-bit system

**Warning:** Errors have been reported when using this method to build the [linux](https://www.archlinux.org/packages/?name=linux) package. The [chroot method](/index.php/Install_bundled_32-bit_system_in_64-bit_system "Install bundled 32-bit system in 64-bit system") is preferred and has been verified to work for building the kernel packages.

First, enable the [multilib](/index.php/Multilib "Multilib") repository and [install](/index.php/Install "Install") [multilib-devel](https://www.archlinux.org/groups/x86_64/multilib-devel/). Reply yes when asked about removing the conflicting `gcc` and `gcc-libs` packages; gcc-multilib is capable of building both 64-bit and 32-bit software.

Then create a 32-bit configuration file

 `~/.makepkg.i686.conf` 
```

CARCH="i686"
CHOST="i686-unknown-linux-gnu"
CFLAGS="-m32 -march=i686 -mtune=generic -O2 -pipe -fstack-protector-strong"
CXXFLAGS="${CFLAGS}"
LDFLAGS="-m32 -Wl,-O1,--sort-common,--as-needed,-z,relro"
```

and invoke makepkg as such

```
$ linux32 makepkg --config ~/.makepkg.i686.conf

```

## 问题处理

### Makepkg sometimes fails to sign a package without asking for signature passphrase

With [gnupg 2.1](https://www.gnupg.org/faq/whats-new-in-2.1.html), gpg-agent no longer has to be started manually and will be started automatically on the first invokation of gpg. Thus if you do not manually start gpg-agent, makepkg will start it.

The problem is that makepkg runs gpg inside a fakeroot, so gpg-agent is also started in that same environment. This leads to bad behavior. The obvious remedy is to manually start the gpg-agent, either on boot or by command, before you run makepkg.

See [GnuPG#gpg-agent](/index.php/GnuPG#gpg-agent "GnuPG") for ways to do this.

### CFLAGS/CXXFLAGS/CPPFLAGS in makepkg.conf do not work for QMAKE based packages

Qmake automatically sets the variable `CFLAGS` and `CXXFLAGS` according to what it thinks should be the right configuration. In order to let qmake use the variables defined in the makepkg configuration file, you must edit the PKGBUILD and pass the variables [QMAKE_CFLAGS_RELEASE](http://doc.qt.io/qt-5/qmake-variable-reference.html#qmake-cflags-release) and [QMAKE_CXXFLAGS_RELEASE](http://doc.qt.io/qt-5/qmake-variable-reference.html#qmake-cxxflags-release) to qmake. For example:

 `PKGBUILD` 
```
...

build() {
  cd "$srcdir/$_pkgname-$pkgver-src"
  qmake-qt4 "$srcdir/$_pkgname-$pkgver-src/$_pkgname.pro" \
    PREFIX=/usr \
    CONFIG+=LINUX_INTEGRATED \
    INSTALL_ROOT_PATH="$pkgdir"\
    QMAKE_CFLAGS_RELEASE="${CFLAGS}"\
    QMAKE_CXXFLAGS_RELEASE="${CXXFLAGS}"

  make
}

...

```

Alternatively, for a system wide configuration, you can create your own `qmake.conf` and set the [QMAKESPEC](http://doc.qt.io/qt-5/qmake-environment-reference.html#qmakespec) environment variable.

### Specifying install directory for QMAKE based packages

The makefile generated by qmake uses the environment variable INSTALL_ROOT to specify where the program should be installed. Thus this package function should work:

 `PKGBUILD` 
```
...

package() {
	cd "$srcdir/${pkgname%-git}"
	make INSTALL_ROOT="$pkgdir" install
}

...

```

Note, that qmake also has to be configured appropriately. For example put this in your .pro file:

 `YourProject.pro` 
```
...

target.path = /usr/local/bin
INSTALLS += target

...

```

### WARNING:Referencing $srcdir in PKGBUILD

有时 `$pkgdir` 或 `$srcdir` 进入了软件包中的文件，用下面命令检查：

```
grep -R "$(pwd)/src" pkg/

```

讨论此问题的[链接](http://www.mail-archive.com/arch-general@archlinux.org/msg15561.html)。

## 参阅

*   [makepkg(8) Manual Page](https://www.archlinux.org/pacman/makepkg.8.html)
*   [makepkg.conf(5) Manual Page](https://www.archlinux.org/pacman/makepkg.conf.5.html)
*   [A Brief Tour of the Makepkg Process](https://gist.github.com/Earnestly/bebad057f40a662b5cc3)
*   [gcccpuopt](https://github.com/pixelb/scripts/blob/master/scripts/gcccpuopt): 一个根据当前 CPU，输出 cpu 专有选项的脚本
*   [makepkg source code](https://projects.archlinux.org/pacman.git/tree/scripts/makepkg.sh.in)