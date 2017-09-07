Ссылки по теме

*   [TORQUE](/index.php/TORQUE "TORQUE")
*   [Slurm](/index.php/Slurm "Slurm")

Distcc это программа, предназначенная для распределения задач компиляции между компьютерами в сети на таких языках как C, C++, Objective C or Objective C++. Приведет к тем же результатам, что и локальная сборка, простота в установке и использовании и как правило, гораздо быстрее, чем локальная компиляция. Круто то что можно использовать его вместе с родными утилитами для компиляции Arch, такими как makepkg.

## Contents

*   [1 Условия](#.D0.A3.D1.81.D0.BB.D0.BE.D0.B2.D0.B8.D1.8F)
*   [2 Приступая к работе](#.D0.9F.D1.80.D0.B8.D1.81.D1.82.D1.83.D0.BF.D0.B0.D1.8F_.D0.BA_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B5)
*   [3 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
    *   [3.1 Ведомый (Slaves)](#.D0.92.D0.B5.D0.B4.D0.BE.D0.BC.D1.8B.D0.B9_.28Slaves.29)
    *   [3.2 Мастер](#.D0.9C.D0.B0.D1.81.D1.82.D0.B5.D1.80)
        *   [3.2.1 Для использования с makepkg](#.D0.94.D0.BB.D1.8F_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D1.81_makepkg)
        *   [3.2.2 For use without makepkg](#For_use_without_makepkg)
*   [4 Compile](#Compile)
    *   [4.1 With makepkg](#With_makepkg)
    *   [4.2 Without makepkg](#Without_makepkg)
*   [5 Monitoring progress](#Monitoring_progress)
*   [6 "Cross Compiling" with distcc](#.22Cross_Compiling.22_with_distcc)
    *   [6.1 X86](#X86)
        *   [6.1.1 Chroot method (preferred)](#Chroot_method_.28preferred.29)
            *   [6.1.1.1 Add port numbers to DISTCC_HOSTS on the i686 chroot](#Add_port_numbers_to_DISTCC_HOSTS_on_the_i686_chroot)
            *   [6.1.1.2 Invoke makepkg from the Native Environment](#Invoke_makepkg_from_the_Native_Environment)
        *   [6.1.2 Multilib GCC method (not recommended)](#Multilib_GCC_method_.28not_recommended.29)
    *   [6.2 Other architectures](#Other_architectures)
        *   [6.2.1 Arch ARM](#Arch_ARM)
        *   [6.2.2 Additional toolchains](#Additional_toolchains)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Journalctl](#Journalctl)
    *   [7.2 code 110](#code_110)
    *   [7.3 Adjust log level](#Adjust_log_level)
    *   [7.4 Limit HDD/SSD usage by relocating $HOME/.distcc](#Limit_HDD.2FSSD_usage_by_relocating_.24HOME.2F.distcc)

## Условия

	master

	Мастер-это компьютер, на котором выполняется компиляция.

	slaves

	The slave(s) accept compilation requests send by the master.

**Примечание:** как Мастер так и Слев машин(ы) должны быть запущены по distcc.

## Приступая к работе

[Установить](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C "Установить") пакет [distcc](https://www.archlinux.org/packages/?name=distcc) на всех компьютерах в кластере:

Для других дистрибутивов, или даже операционных систем, включая Windows использование через cygwin, обратитесь к [distcc docs](http://distcc.samba.org/doc.html).

## Конфигурация

### Ведомый (Slaves)

Конфигурация для slaves хранится в `/etc/conf.d/distccd`. Параметры командной строки указаны в [distcc(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/distcc.1). Как минимум, настроить разрешенные диапазонов адресов в [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing "wikipedia:Classless Inter-Domain Routing") формат:

```
DISTCC_ARGS="--allow 192.168.0.0/24"

```

Хороший инструмент для преобразования диапазонов адресов CIDR можно найти здесь: [CIDR Utility Tool](http://www.ipaddressguide.com/cidr).

[Запустить](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D1%8C "Запустить") `distccd.service` на всех участвующих slave. Для запуска `distccd.service` при загрузке, [enable](/index.php/Enable "Enable") на каждой участвующей машине.

### Мастер

#### Для использования с makepkg

Редактировать `/etc/makepkg.conf` в следующих трех разделах:

1.  BUILDENV has distcc unbanged i.e. without exclamation point.
2.  Uncomment the *DISTCC_HOSTS* line and add the IP addresses of the slaves then a slash and the number of threads they are to use. The subsequent IP address/threads should be separated by a white space. This list is ordered from most powerful to least powerful (processing power).
3.  Adjust the MAKEFLAGS variable to correspond to the number of sum of the number of individual values specified for the max threads per server. In the example below, this is 5+3+3=11\. If users specify more than this sum, the extra theoretical thread(s) will be blocked by distcc and appear as such in monitoring utils such as *distccmon-text* described below.

**Note:** It is common practice although optional to define the number of threads as the number of physical core+hyperhtreaded cores (if they exist) plus 1\. Do this on a per-server basis, NOT in the MAKEFLAGS!

Example using relevant lines:

```
BUILDENV=(distcc fakeroot color !ccache check !sign)
MAKEFLAGS="-j11"
DISTCC_HOSTS="192.168.0.2/5 192.168.0.3/3 192.168.0.4/3"

```

If users wish to use distcc through SSH, add an "@" symbol in front of the IP address in this section. If key-based auth is not setup on the systems, set the DISTCC_SSH variable to ignore checking for authenticated hosts, i.e. DISTCC_SSH="ssh -i"

**Warning:** Make sure that neither the **CFLAGS** and **CXXFLAGS** have -march=native set or else distccd will not distribute work to other machines! Using the Arch defaults for these variables is recommended.

#### For use without makepkg

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

## Compile

### With makepkg

Compile via makepkg as normal.

### Without makepkg

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

## Monitoring progress

Progress can be monitored via several methods.

1.  distccmon-text
2.  tailing log file

Invoke distccmon-text to check on compilation status:

```
$ distccmon-text
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

One can have this program run continuously by using watch or by appending a space followed by integer to the command which corresponds to the number of sec to wait for a repeat query:

```
$ watch distccmon-text

```

or

```
$ distccmon-text 2

```

One can also simply tail `systemd journal log` on daemon:

```
# journalctl -f -u distccd

```

## "Cross Compiling" with distcc

### X86

There are currently two methods from which to select to have the ability of distcc distribution of tasks over a cluster building i686 packages from a native x86_64 environment. Neither is ideal, but to date, there are the only two methods documented on the wiki.

An ideal setup is one that uses the unmodified ARCH packages for distccd running only once one each node regardless of building from the native environment or from within a chroot AND one that works with makepkg. Again, this Utopian setup is not currently known.

A [discussion thread](https://bbs.archlinux.org/viewtopic.php?id=129762) has been started on the topic; feel free to contribute.

#### Chroot method (preferred)

**Note:** This method works, but is not very elegant requiring duplication of distccd on all nodes AND need to have a 32-bit chroots on all nodes.

Assuming the user has a [32-bit chroot](/index.php/Install_bundled_32-bit_system_in_Arch64 "Install bundled 32-bit system in Arch64") setup and configured on **each node** of the distcc cluster, the strategy is to have two separate instances of distccd running on different ports on each node -- one runs in the native x86_64 environment and the other in the x86 chroot on a modified port. Start makepkg via a [schroot command](/index.php/Install_bundled_32-bit_system_in_64-bit_system#Schroot "Install bundled 32-bit system in 64-bit system") invoking makepkg.

##### Add port numbers to DISTCC_HOSTS on the i686 chroot

Append the port number defined eariler (3692) to each of the hosts in `/opt/arch32/etc/makepkg.conf` as follows:

```
DISTCC_HOSTS="192.168.1.101/5:3692 192.168.1.102/5:3692 192.168.1.103/3:3692"

```

**Note:** This only needs to be setup on the "master" i686 chroot. Where "master" is defined as the one from which the compilation will take place.

##### Invoke makepkg from the Native Environment

Setup [schroot](/index.php/Install_bundled_32-bit_system_in_64-bit_system#Schroot "Install bundled 32-bit system in 64-bit system") on the native x86_64 environment. Invoke makepkg to build an i686 package from the native x86_64 environment, simply by:

```
$ schroot -p -- makepkg -src

```

#### Multilib GCC method (not recommended)

See [Makepkg#Build 32-bit packages on a 64-bit system](/index.php/Makepkg#Build_32-bit_packages_on_a_64-bit_system "Makepkg").

### Other architectures

#### Arch ARM

When building on an Arch ARM device, the developers *highly* recommend using the official project toolchains.

*   [ARMv8](https://archlinuxarm.org/builder/xtools/x-tools8.tar.xz)
*   [ARMv7l hard](https://archlinuxarm.org/builder/xtools/x-tools7h.tar.xz)
*   [ARMv6l hard](https://archlinuxarm.org/builder/xtools/x-tools6h.tar.xz)
*   [ARMv5te soft](https://archlinuxarm.org/builder/xtools/x-tools.tar.xz)

Extract the toolchain corresponding to the requisite architecture somewhere on the **slave filesystem** and edit `/etc/conf.d/distccd` adjusting the PATH to allow the toolchain to be used.

Example with the toolchain extracted to `/mnt/data`:

```
PATH=/mnt/data/x-tools8/aarch64-unknown-linux-gnueabi/bin:$PATH

```

To read in the configuration file, [restart](/index.php/Restart "Restart") `distcc.service`.

Optionally link it to your user's homedir if planning to build without makepkg. Example:

```
$ ln -s /mnt/data/x-tools8 x-tools8

```

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

### Adjust log level

By default, distcc will log to `/var/log/messages.log` as it goes along. One trick (actually recommended in the distccd manpage) is to log to an alternative file directly. Again, one can locate this in RAM via /tmp. Another trick is to lower to log level of minimum severity of error that will be included in the log file. Useful if only wanting to see error messages rather than an entry for each connection. LEVEL can be any of the standard syslog levels, and in particular critical, error, warning, notice, info, or debug.

Either call distcc with the arguments mentioned here on the master or appended it to DISTCC_ARGS in `/etc/conf.d/distccd` on the slaves:

```
DISTCC_ARGS="--allow 192.168.0.0/24 --log-level error --log-file /tmp/distccd.log"

```

### Limit HDD/SSD usage by relocating $HOME/.distcc

By default, distcc creates `$HOME/.distcc` which stores transient relevant info as it serves up work for nodes to compile. Create a directory named *.distcc* in RAM such as /tmp and soft link to it in $HOME. This will avoid needless HDD read/writes and is particularly important for SSDs.

```
$ mv $HOME/.distcc /tmp
$ ln -s /tmp/.distcc $HOME/.distcc

```

Use systemd to re-create this directory on a reboot (the soft link will remain until it is manually removed like any other file):

Create the following tmpfile.

 `/etc/tmpfiles.d/tmpfs-create.conf` 
```
d /tmp/.distcc 0755 <username> users -

```