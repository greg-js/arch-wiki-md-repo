相关文章

*   [TORQUE](/index.php/TORQUE "TORQUE")
*   [Slurm](/index.php/Slurm "Slurm")

**翻译状态：** 本文是英文页面 [Distcc](/index.php/Distcc "Distcc") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-07-13，点击[这里](https://wiki.archlinux.org/index.php?title=Distcc&diff=0&oldid=520230)可以查看翻译后英文页面的改动。

Distcc 是一个将 C、C++、Objective C 或 Objective C++ 等程序的编译任务分发到网络中多个主机的程序。distcc 的结果和本地编译一模一样，安装后使用方便，通常比本地编译快很多。

## Contents

*   [1 名词定义](#.E5.90.8D.E8.AF.8D.E5.AE.9A.E4.B9.89)
*   [2 开始](#.E5.BC.80.E5.A7.8B)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 从机配置](#.E4.BB.8E.E6.9C.BA.E9.85.8D.E7.BD.AE)
    *   [3.2 主机配置](#.E4.B8.BB.E6.9C.BA.E9.85.8D.E7.BD.AE)
        *   [3.2.1 makepkg 编译](#makepkg_.E7.BC.96.E8.AF.91)
        *   [3.2.2 非 makepkg 编译](#.E9.9D.9E_makepkg_.E7.BC.96.E8.AF.91)
*   [4 编译](#.E7.BC.96.E8.AF.91)
    *   [4.1 makepkg 编译](#makepkg_.E7.BC.96.E8.AF.91_2)
    *   [4.2 非 makepkg 编译](#.E9.9D.9E_makepkg_.E7.BC.96.E8.AF.91_2)
*   [5 监视进度](#.E7.9B.91.E8.A7.86.E8.BF.9B.E5.BA.A6)
*   [6 "Cross Compiling" with distcc](#.22Cross_Compiling.22_with_distcc)
    *   [6.1 32-bit x86 (i686)](#32-bit_x86_.28i686.29)
        *   [6.1.1 Chroot method (preferred)](#Chroot_method_.28preferred.29)
            *   [6.1.1.1 Add port numbers to DISTCC_HOSTS on the i686 chroot](#Add_port_numbers_to_DISTCC_HOSTS_on_the_i686_chroot)
            *   [6.1.1.2 Invoke makepkg from the Native Environment](#Invoke_makepkg_from_the_Native_Environment)
        *   [6.1.2 Multilib GCC method (not recommended)](#Multilib_GCC_method_.28not_recommended.29)
    *   [6.2 Other architectures](#Other_architectures)
        *   [6.2.1 Arch Linux ARM](#Arch_Linux_ARM)
        *   [6.2.2 Additional toolchains](#Additional_toolchains)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Journalctl](#Journalctl)
    *   [7.2 code 110](#code_110)
    *   [7.3 修改 $HOME/.distcc 位置以限制硬盘使用](#.E4.BF.AE.E6.94.B9_.24HOME.2F.distcc_.E4.BD.8D.E7.BD.AE.E4.BB.A5.E9.99.90.E5.88.B6.E7.A1.AC.E7.9B.98.E4.BD.BF.E7.94.A8)
    *   [7.4 修改日志级别](#.E4.BF.AE.E6.94.B9.E6.97.A5.E5.BF.97.E7.BA.A7.E5.88.AB)

## 名词定义

	主机

	启动编译的机器.

	从机

	接受 master 的编译请求，一个系统可以包含一个或多个从机。

## 开始

将所有用到的计算机都[安装](/index.php/Install "Install")软件包 [distcc](https://www.archlinux.org/packages/?name=distcc)。如果是其他的发行版甚至使用 Cygwin 的 Windows 操作系统,请阅读 [distcc 文档](http://distcc.samba.org/doc.html)。

## 配置

### 从机配置

编辑 `/etc/conf.d/distccd`，修改唯一没有被注释掉的那一行，设置正确的 IP 地址或整个子网。

```
DISTCC_ARGS="--user nobody --allow 192.168.0.0/24"

```

```
DISTCC_ARGS="--allow 192.168.0.0/24"

```

[CIDR Utility Tool](http://www.ipaddressguide.com/cidr)可以帮助进行地址转换，其它设置请参考 [distcc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/distcc.1).

在所有从机上[启动](/index.php/Start "Start") 服务 `distccd.service`。要开机启动，请[启用](/index.php/Enable "Enable") 此服务。

### 主机配置

#### makepkg 编译

编辑`/etc/makepkg.conf`：

1.  确保 BUILDENV 中的 distcc 没有被禁用(前面没有感叹号)
2.  编辑*DISTCC_HOSTS* ，加入可以使用的编译服务器的 IP 地址 + 反斜杠 + 线程数，不同 IP 地址用空格隔开，按照处理器性能排列
3.  修改 MAKEFLAGS 中的 N 为所有使用线程的和。在下面的示例为 5+3+3=11\. 如果超过这个值，超出的线程将会被 distcc阻塞。

**Note:** 在单机编译时一般定义为 CPU 数加一，仅在单机编译时才是对的，这里不应该使用这个方法。

相关行的示例:

```
BUILDENV=(distcc fakeroot color !ccache check !sign)
MAKEFLAGS="-j11"
DISTCC_HOSTS="192.168.0.2/5 192.168.0.3/3 192.168.0.4/3"

```

**注意:** `CFLAGS` 和 `CXXFLAGS` 中不能使用 `-march=native` 选项，否则 distccd 不会将编译任务发给其它机器。

#### 非 makepkg 编译

The minimal configuration for distcc on the master includes the setting of the available slaves. This can either be done by setting the addresses in the environment variable `DISTCC_HOSTS` or in either of the configuration files `$DISTCC_HOSTS`, `$DISTCC_DIR/hosts`, `~/.distcc/hosts` or `/etc/distcc/hosts`.

Example for setting the slave address using `DISTCC_HOSTS`:

```
$ export DISTCC_HOSTS="192.168.0.3,lzo,cpp 192.168.0.4,lzo,cpp"

```

**Note:** This is a white space separated list.

Example for setting the slave addresses in the hosts configuration file:

 `~/.distcc/hosts` 
```
192.168.0.3,lzo,cpp 192.168.0.4,lzo,cpp

```

Instead of explicitly listing the server addresses one can also use the avahi zeroconf mode. To use this mode `+zeroconf` must be in place instead of the server addresses and the distcc daemons on the slaves have to be started using the `--zeroconf` option. Note that this option does not support the pump mode!

The examples add the following options to the address:

*   `lzo`: Enables LZO compression for this TCP or SSH host (slave).
*   `cpp`: Enables distcc-pump mode for this host (slave). Note: the build command must be wrapped in the pump script in order to start the include server.

A description for the pump mode can be found here: [HOW DISTCC-PUMP MODE WORKS](http://distcc.googlecode.com/svn%20...%20%3Cdiv%20class=/trunk/doc/web/man/distcc_1.html#TOC_8) and [distcc's pump mode: A New Design for Distributed C/C++ Compilation](http://google-opensource.blogspot.de/2008/08/distccs-pump-mode-new-design-for.html)

To use distcc-pump mode for a slave, users must start the compilation using the pump script otherwise the compilation will fail.

## 编译

### makepkg 编译

然后正常运行 makepkg 即可。

### 非 makepkg 编译

To compile a source file using the distcc pump mode, use the following command:

```
$ pump distcc g++ -c hello_world.cpp

```

In this case the pump script will execute distcc which in turn calls g++ with "-c hello_world.cpp" as parameter.

To compile a Makefile project, first find out which variables are set by the compiler. For example in gzip-1.6, one can find the following line in the Makefile: `CC = gcc -std=gnu99`. Normally the variables are called `CC` for C projects and `CXX` for C++ projects. To compile the project using distcc it would look like this:

```
$ wget [ftp://ftp.gnu.org/pub/gnu/gzip/gzip-1.6.tar.xz](ftp://ftp.gnu.org/pub/gnu/gzip/gzip-1.6.tar.xz)
$ tar xf gzip-1.6.tar.xz
$ cd gzip-1.6
$ ./configure
$ pump make -j2 CC="distcc gcc -std=gnu99"

```

This example would compile gzip using distcc's pump mode with two compile threads. For the correct `-j` setting have a look at [What -j level to use?](https://cdn.rawgit.com/distcc/distcc/master/doc/web/faq.html)

## 监视进度

[distcc](https://www.archlinux.org/packages/?name=distcc) ships with a cli monitor `distccmon-text` and a gtk monitor `distccmon-gnome` one can use to check on compilation status.

The cli monitor can run continuously by appending a space followed by integer to the command which corresponds to the number of sec to wait for a repeat query:

```
$ distccmon-text 3
29291 Preprocess  probe_64.c                                 192.168.0.2[0]
30954 Compile     apic_noop.c                                192.168.0.2[0]
30932 Preprocess  kfifo.c                                    192.168.0.2[0]
30919 Compile     blk-core.c                                 192.168.0.2[1]
30969 Compile     i915_gem_debug.c                           192.168.0.2[3]
30444 Compile     block_dev.c                                192.168.0.3[1]
30904 Compile     compat.c                                   192.168.0.3[2]
30891 Compile     hugetlb.c                                  192.168.0.3[3]
30458 Compile     catalog.c                                  192.168.0.4[0]
30496 Compile     ulpqueue.c                                 192.168.0.4[2]
30506 Compile     alloc.c                                    192.168.0.4[0]

```

## "Cross Compiling" with distcc

### 32-bit x86 (i686)

There are currently two methods from which to select to have the ability of distcc distribution of tasks over a cluster building i686 packages from a native x86_64 environment. Neither is ideal, but to date, there are the only two methods documented on the wiki.

An ideal setup is one that uses the unmodified ARCH packages for distccd running only once one each node regardless of building from the native environment or from within a chroot AND one that works with makepkg. Again, this Utopian setup is not currently known.

A [discussion thread](https://bbs.archlinux.org/viewtopic.php?id=129762) has been started on the topic; feel free to contribute.

#### Chroot method (preferred)

**Note:** This method works, but is not very elegant requiring duplication of distccd on all nodes AND need to have a 32-bit chroots on all nodes.

Assuming the user has a [32-bit chroot](/index.php/Install_bundled_32-bit_system_in_64-bit_system "Install bundled 32-bit system in 64-bit system") setup and configured on **each node** of the distcc cluster, the strategy is to have two separate instances of distccd running on different ports on each node -- one runs in the native x86_64 environment and the other in the x86 chroot on a modified port. Start makepkg via a [schroot(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/schroot.1) command invoking makepkg.

##### Add port numbers to DISTCC_HOSTS on the i686 chroot

Append the port number defined eariler (3692) to each of the hosts in `/opt/arch32/etc/makepkg.conf` as follows:

```
DISTCC_HOSTS="192.168.1.101/5:3692 192.168.1.102/5:3692 192.168.1.103/3:3692"

```

**Note:** This only needs to be setup on the "master" i686 chroot. Where "master" is defined as the one from which the compilation will take place.

##### Invoke makepkg from the Native Environment

Set up [schroot](https://www.archlinux.org/packages/?name=schroot) on the native x86_64 environment. Invoke makepkg to build an i686 package from the native x86_64 environment, simply by:

```
$ schroot -p -- makepkg -src

```

#### Multilib GCC method (not recommended)

See [Makepkg#Build 32-bit packages on a 64-bit system](/index.php/Makepkg#Build_32-bit_packages_on_a_64-bit_system "Makepkg").

### Other architectures

#### Arch Linux ARM

When building on an Arch Linux ARM device, the developers *highly* recommend using the official project [toolchains](https://archlinuxarm.org/wiki/Distcc_Cross-Compiling) which should be installed on the x86_64 slave machine(s). Rather than manually managing these, the [AUR](/index.php/AUR "AUR") provides all four toolchains as well as simple systemd service units:

*   [distccd-alarm-armv5](https://aur.archlinux.org/packages/distccd-alarm-armv5/)
*   [distccd-alarm-armv6h](https://aur.archlinux.org/packages/distccd-alarm-armv6h/)
*   [distccd-alarm-armv7h](https://aur.archlinux.org/packages/distccd-alarm-armv7h/)
*   [distccd-alarm-armv8](https://aur.archlinux.org/packages/distccd-alarm-armv8/)

Setup on the slave machine containing the toolchain is identical to [#Slaves](#Slaves) except that the name of the configuration file matches that of the respective package. For example, `/etc/conf.d/distccd-armv7h`.

A systemd service unit is provided for each respective package. For example, `distccd-armv7h.service`.

#### Additional toolchains

*   [EmbToolkit](https://embtoolkit.org/): Tool for creating cross compilation tool chain; supports ARM and MIPS architectures; supports building of an LLVM based tool chain
*   [crosstool-ng](http://crosstool-ng.org/): Similar to EmbToolkit; supports more architectures (see website for more information)
*   [Linaro](https://www.linaro.org/downloads/): Provides tool chains for ARM development

The `EmbToolkit` provides a nice graphical configuration menu (`make xconfig`) for configuring the tool chain.

## Troubleshooting

### Journalctl

Use `journalctl` to find out what was going wrong:

```
$ journalctl $(which distccd) -e --since "5 min ago"

```

### code 110

Make sure that the tool chain works for the user account under which the distcc daemon process gets started (default is nobody). The following will test if the tool chain works for user nobody. In `/etc/passwd` change the login for the nobody user to the following:

 `$ cat /etc/passwd` 
```
...
nobody:x:99:99:nobody:/:/bin/bash
...

```

Then cd into the directory containing the cross compiler binaries and try to execute the compiler:

```
# su nobody
$ ./gcc --version
bash: ./gcc: Permission denied

```

Users experiencing this error should make sure that groups permissions as described in [#Other architectures](#Other_architectures) are correctly in setup.

Make sure to change back `/etc/passwd` to its original state after these modifications.

Alternatively, use sudo without changing the shell in /etc/passwd.

```
 # sudo -u nobody gcc --version

```

### 修改 $HOME/.distcc 位置以限制硬盘使用

distcc 默认会在 `$HOME/.distcc` 保存中间结果。在内存 /tmp 中创建 *.distcc* 并链接到 $HOME 可以避免磁盘读写。

```
$ export DISTCC_DIR=/tmp/distcc

```

### 修改日志级别

默认日志放在 `/var/log/messages.log`，也可以放到一个单独的文件，例如通过 /tmp 放到 RAM 中。同时降低日志级别也可以只显示错误信息。LEVEL 可以是任意 syslog 级别，例如 critical, error, warning, notice, info, 或 debug.

把它们**附加**到 `/etc/conf.d/distccd` 的 DISTCC_ARGS 中。

```
DISTCC_ARGS="--user nobody --allow 192.168.0.0/24 --log-level error --log-file /tmp/distccd.log"

```