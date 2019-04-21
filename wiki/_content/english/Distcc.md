Related articles

*   [TORQUE](/index.php/TORQUE "TORQUE")
*   [Slurm](/index.php/Slurm "Slurm")

[distcc](https://en.wikipedia.org/wiki/distcc "wikipedia:distcc") is a program to distribute builds of C, C++, Objective C or Objective C++ code across several machines on a network to speed up building. It should always generate the same results as a local build, is simple to install and use, and is usually much faster than a local compile. Further, one can use it together with native Arch build tools such as makepkg.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Terms](#Terms)
*   [2 Getting started](#Getting_started)
*   [3 Configuration](#Configuration)
    *   [3.1 Volunteers](#Volunteers)
    *   [3.2 Client](#Client)
        *   [3.2.1 For use with makepkg](#For_use_with_makepkg)
        *   [3.2.2 For use without makepkg](#For_use_without_makepkg)
*   [4 Compile](#Compile)
    *   [4.1 With makepkg](#With_makepkg)
    *   [4.2 Without makepkg](#Without_makepkg)
*   [5 Monitoring progress](#Monitoring_progress)
*   [6 Cross Compiling with distcc](#Cross_Compiling_with_distcc)
    *   [6.1 Arch Linux ARM](#Arch_Linux_ARM)
        *   [6.1.1 Volunteers](#Volunteers_2)
        *   [6.1.2 Client](#Client_2)
    *   [6.2 Additional toolchains](#Additional_toolchains)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Journalctl](#Journalctl)
    *   [7.2 Adjust log level](#Adjust_log_level)
    *   [7.3 Limit HDD/SSD usage by relocating $HOME/.distcc](#Limit_HDD/SSD_usage_by_relocating_$HOME/.distcc)
    *   [7.4 For distccd-alarm](#For_distccd-alarm)
        *   [7.4.1 No such file or directory](#No_such_file_or_directory)
        *   [7.4.2 Monitoring does not work](#Monitoring_does_not_work)
*   [8 See also](#See_also)

## Terms

	client

	The client is the computer initiating the compilation.

	volunteer

	The volunteer is the computer accepting compilation requests send by the client. One can setup multiple volunteers or just a single one.

## Getting started

[Install](/index.php/Install "Install") the [distcc](https://www.archlinux.org/packages/?name=distcc) package on all participating PCs in the distcc cluster. For other distros, or even operating systems including Windows through using Cygwin, refer to the [distcc docs](http://distcc.samba.org/doc.html). Be sure to allow traffic on the port on which distcc runs (the default is 3632/tcp), see [Category:Firewalls](/index.php/Category:Firewalls "Category:Firewalls") and [distcc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/distcc.1).

## Configuration

### Volunteers

The configuration for the volunteer is stored in `/etc/conf.d/distccd`. At a minimum, configure the allowed address ranges in [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing "wikipedia:Classless Inter-Domain Routing") format:

```
DISTCC_ARGS="--allow 192.168.10.0/24"

```

A nice tool for converting address ranges to CIDR format can be found here: [CIDR Utility Tool](http://www.ipaddressguide.com/cidr). Other commandline options can be defined as well. Refer to [distcc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/distcc.1).

[Start](/index.php/Start "Start") `distccd.service` on every participating volunteer. To have `distccd.service` start at boot-up, [enable](/index.php/Enable "Enable") it.

### Client

#### For use with makepkg

Edit `/etc/makepkg.conf` in the following sections:

1.  The BUILDENV array will need to have *distcc* unbanged i.e. list it without exclamation point.
2.  Uncomment the *DISTCC_HOSTS* line and add the host name or IP addresses of the volunteers. Optionally, follow this with a forward slash and the max number of threads they are to use. The subsequent nodes should be separated by a white space. This list should be ordered from most powerful to least powerful (processing power).
3.  Adjust the MAKEFLAGS variable to correspond to the number of sum of the number of individual values specified for the max threads per server. In the example below, this is 5+3+3=11.

Example using relevant lines:

```
BUILDENV=(distcc fakeroot color !ccache check !sign)
MAKEFLAGS="-j11"
DISTCC_HOSTS="192.168.10.2/5 192.168.10.3/3 192.168.10.4/3"

```

**Warning:** The `-march=native` flag cannot be used in the `CFLAGS` and `CXXFLAGS` variables, otherwise distccd will not distribute work to other machines.

#### For use without makepkg

The minimal configuration for distcc on the client includes the setting of the available volunteers. This can either be done by setting the addresses in the environment variable `DISTCC_HOSTS` or in either of the configuration files `$DISTCC_HOSTS`, `$DISTCC_DIR/hosts`, `~/.distcc/hosts` or `/etc/distcc/hosts`.

Example for setting the volunteer address using `DISTCC_HOSTS`:

```
$ export DISTCC_HOSTS="192.168.10.3,lzo,cpp 192.168.10.4,lzo,cpp"

```

**Note:** This is a white space separated list.

Example for setting the volunteer addresses in the hosts configuration file:

 `~/.distcc/hosts` 
```
192.168.10.3,lzo,cpp 192.168.10.4,lzo,cpp

```

Instead of explicitly listing the server addresses one can also use the avahi zeroconf mode. To use this mode `+zeroconf` must be in place instead of the server addresses and the distcc daemons on the volunteers have to be started using the `--zeroconf` option. Note that this option does not support the pump mode!

The examples add the following options to the address:

*   `lzo`: Enables LZO compression for this TCP or SSH host (volunteer).
*   `cpp`: Enables distcc-pump mode for this host (volunteer). Note: the build command must be wrapped in the pump script in order to start the include server.

A description for the pump mode can be found here: [distcc's pump mode: A New Design for Distributed C/C++ Compilation](http://google-opensource.blogspot.de/2008/08/distccs-pump-mode-new-design-for.html)

To use distcc-pump mode for a volunteer, users must start the compilation using the pump script otherwise the compilation will fail.

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
29291 Preprocess  probe_64.c                                 192.168.10.2[0]
30954 Compile     apic_noop.c                                192.168.10.2[0]
30932 Preprocess  kfifo.c                                    192.168.10.2[0]
30919 Compile     blk-core.c                                 192.168.10.2[1]
30969 Compile     i915_gem_debug.c                           192.168.10.2[3]
30444 Compile     block_dev.c                                192.168.10.3[1]
30904 Compile     compat.c                                   192.168.10.3[2]
30891 Compile     hugetlb.c                                  192.168.10.3[3]
30458 Compile     catalog.c                                  192.168.10.4[0]
30496 Compile     ulpqueue.c                                 192.168.10.4[2]
30506 Compile     alloc.c                                    192.168.10.4[0]

```

## Cross Compiling with distcc

One can use distcc to help cross compile.

*   A machine running the target architecture should be used as the client.
*   Non-native architecture volunteers will help compile but they require the corresponding toolchain to be installed and their distcc to point to it.

### Arch Linux ARM

#### Volunteers

The developers *highly* recommend using the official project [toolchains](https://archlinuxarm.org/wiki/Distcc_Cross-Compiling) which should be installed on the x86_64 volunteer(s). Rather than manually managing these, the [AUR](/index.php/AUR "AUR") provides all four toolchains as well as simple systemd service units:

*   [distccd-alarm-armv5](https://aur.archlinux.org/packages/distccd-alarm-armv5/)
*   [distccd-alarm-armv6h](https://aur.archlinux.org/packages/distccd-alarm-armv6h/)
*   [distccd-alarm-armv7h](https://aur.archlinux.org/packages/distccd-alarm-armv7h/)
*   [distccd-alarm-armv8](https://aur.archlinux.org/packages/distccd-alarm-armv8/)

Setup on the volunteer containing the toolchain is identical to [#Volunteers](#Volunteers) except that the name of the configuration and systemd service file matches that of the respective package. For example, for armv7h the config file is `/etc/conf.d/distccd-armv7h` and the systemd service unit is `distccd-armv7h.service`.

Note that each of the toolchains runs on a unique port thus allowing them to co-exist on the volunteer if needed. Be sure to allow traffic to the port on which distcc runs see [Category:Firewalls](/index.php/Category:Firewalls "Category:Firewalls") and [distcc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/distcc.1).

| Target architecture | Distcc Port |
| *armv5* | 3633 |
| *armv6h* | 3634 |
| *armv7h* | 3635 |
| *armv8h/aarch64* | 3636 |

#### Client

Setup of the client is identical to [#Client](#Client) except, one needs to modify the following two files to define the now non-standard port the volunteers are expected to use. Refer to the table above if using the AUR package.

1.  `/etc/conf.d/distcc`: example on an armv7h machine: `DISTCC_ARGS="--allow 127.0.0.1 --allow 192.168.10.0/24 --port 3635`
2.  `/etc/makepkg.conf`: example on an armv7h machine: `DISTCC_HOSTS="192.168.10.2/5:3635 192.168.10.3/5:3635"`

### Additional toolchains

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

### Adjust log level

By default, distcc will log to `/var/log/messages.log` as it goes along. One trick (actually recommended in the distccd manpage) is to log to an alternative file directly. Again, one can locate this in RAM via /tmp. Another trick is to lower to log level of minimum severity of error that will be included in the log file. Useful if only wanting to see error messages rather than an entry for each connection. LEVEL can be any of the standard syslog levels, and in particular critical, error, warning, notice, info, or debug.

Either call distcc with the arguments mentioned here on the client or appended it to DISTCC_ARGS in `/etc/conf.d/distccd` on the volunteers:

```
DISTCC_ARGS="--allow 192.168.10.0/24 --log-level error --log-file /tmp/distccd.log"

```

### Limit HDD/SSD usage by relocating $HOME/.distcc

By default, distcc creates `$HOME/.distcc` which stores transient relevant info as it serves up work for nodes to compile. This will avoid needless HDD read/writes and is particularly important for SSDs.

```
$ export DISTCC_DIR=/tmp/distcc

```

### For distccd-alarm

#### No such file or directory

Errors similar to the following indicate that the user is mistakenly running the distccd service provided by [distcc](https://www.archlinux.org/packages/?name=distcc) and NOT provided by the distccd-alarm packages (ie [distccd-alarm-armv5](https://aur.archlinux.org/packages/distccd-alarm-armv5/), [distccd-alarm-armv6h](https://aur.archlinux.org/packages/distccd-alarm-armv6h/), [distccd-alarm-armv7h](https://aur.archlinux.org/packages/distccd-alarm-armv7h/), or [distccd-alarm-armv8](https://aur.archlinux.org/packages/distccd-alarm-armv8/).)

Be sure to start the correct service for the target architecture.

```
distcc[25479] (dcc_execvp) ERROR: failed to exec armv7l-unknown-linux-gnueabihf-g++: No such file or directory

```

#### Monitoring does not work

Since the distccd-alarm-arm* services use the `nobody` user, `/usr/bin/distccmon-text` does not work to monitor compilation. One can inspect the output of the actually distcc log to troubleshoot if needed, `tail -f /tmp/distccd-armv7h.log` for example.

## See also

*   [https://github.com/distcc/distcc](https://github.com/distcc/distcc)

*   [icecream](https://aur.archlinux.org/packages/icecream/) - An easier to configure fork of distcc that some find brings notably better results and improved utilisation of available cores.