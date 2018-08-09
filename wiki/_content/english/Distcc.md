Related articles

*   [TORQUE](/index.php/TORQUE "TORQUE")
*   [Slurm](/index.php/Slurm "Slurm")

Distcc is a program to distribute builds of C, C++, Objective C or Objective C++ code across several machines on a network to speed up building. It should always generate the same results as a local build, is simple to install and use, and is usually much faster than a local compile. Further, one can use it together with native Arch build tools such as makepkg.

## Contents

*   [1 Terms](#Terms)
*   [2 Getting started](#Getting_started)
*   [3 Configuration](#Configuration)
    *   [3.1 Slaves](#Slaves)
    *   [3.2 Master](#Master)
        *   [3.2.1 For use with makepkg](#For_use_with_makepkg)
        *   [3.2.2 For use without makepkg](#For_use_without_makepkg)
*   [4 Compile](#Compile)
    *   [4.1 With makepkg](#With_makepkg)
    *   [4.2 Without makepkg](#Without_makepkg)
*   [5 Monitoring progress](#Monitoring_progress)
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
    *   [7.3 Adjust log level](#Adjust_log_level)
    *   [7.4 Limit HDD/SSD usage by relocating $HOME/.distcc](#Limit_HDD.2FSSD_usage_by_relocating_.24HOME.2F.distcc)

## Terms

	master

	The master is the computer which initiates the compilation.

	slave

	The slave accepts compilation requests send by the master. One can setup multiple slave systems or just a single one.

## Getting started

[Install](/index.php/Install "Install") the [distcc](https://www.archlinux.org/packages/?name=distcc) package on all participating PCs in the distcc cluster. For other distros, or even operating systems including Windows through using Cygwin, refer to the [distcc docs](http://distcc.samba.org/doc.html).

## Configuration

### Slaves

The configuration for the slave machine is stored in `/etc/conf.d/distccd`. At a minimum, configure the allowed address ranges in [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing "wikipedia:Classless Inter-Domain Routing") format:

```
DISTCC_ARGS="--allow 192.168.0.0/24"

```

A nice tool for converting address ranges to CIDR format can be found here: [CIDR Utility Tool](http://www.ipaddressguide.com/cidr). Other commandline options can be defined as well. Refer to [distcc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/distcc.1).

[Start](/index.php/Start "Start") `distccd.service` on every participating slave. To have `distccd.service` start at boot-up, [enable](/index.php/Enable "Enable") it.

### Master

#### For use with makepkg

Edit `/etc/makepkg.conf` in the following sections:

1.  The BUILDENV array will need to have *distcc* unbanged i.e. list it without exclamation point.
2.  Uncomment the *DISTCC_HOSTS* line and add the IP addresses of the slaves then a slash and the number of threads they are to use. The subsequent IP address/threads should be separated by a white space. This list is ordered from most powerful to least powerful (processing power).
3.  Adjust the MAKEFLAGS variable to correspond to the number of sum of the number of individual values specified for the max threads per server. In the example below, this is 5+3+3=11.

**Note:** The number of threads is commonly set as the number of cores plus 1\. Do this on a per-server basis, *not* in the `MAKEFLAGS` variable.

Example using relevant lines:

```
BUILDENV=(distcc fakeroot color !ccache check !sign)
MAKEFLAGS="-j11"
DISTCC_HOSTS="192.168.0.2/5 192.168.0.3/3 192.168.0.4/3"

```

**Note:** The `-march=native` flag cannot be used in the `CFLAGS` and `CXXFLAGS` variables, otherwise distccd will not distribute work to other machines.

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

A description for the pump mode can be found here: [distcc's pump mode: A New Design for Distributed C/C++ Compilation](http://google-opensource.blogspot.de/2008/08/distccs-pump-mode-new-design-for.html)

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

### Adjust log level

By default, distcc will log to `/var/log/messages.log` as it goes along. One trick (actually recommended in the distccd manpage) is to log to an alternative file directly. Again, one can locate this in RAM via /tmp. Another trick is to lower to log level of minimum severity of error that will be included in the log file. Useful if only wanting to see error messages rather than an entry for each connection. LEVEL can be any of the standard syslog levels, and in particular critical, error, warning, notice, info, or debug.

Either call distcc with the arguments mentioned here on the master or appended it to DISTCC_ARGS in `/etc/conf.d/distccd` on the slaves:

```
DISTCC_ARGS="--allow 192.168.0.0/24 --log-level error --log-file /tmp/distccd.log"

```

### Limit HDD/SSD usage by relocating $HOME/.distcc

By default, distcc creates `$HOME/.distcc` which stores transient relevant info as it serves up work for nodes to compile. This will avoid needless HDD read/writes and is particularly important for SSDs.

```
$ export DISTCC_DIR=/tmp/distcc

```