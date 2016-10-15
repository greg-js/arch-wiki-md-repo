[sysctl](https://en.wikipedia.org/wiki/sysctl "wikipedia:sysctl") is a tool for examining and changing [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") at runtime (package [procps-ng](https://www.archlinux.org/packages/?name=procps-ng) in [official repositories](/index.php/Official_repositories "Official repositories")). sysctl is implemented in procfs, the virtual process file system at `/proc/`.

## Contents

*   [1 Configuration](#Configuration)
*   [2 Security](#Security)
*   [3 Networking](#Networking)
    *   [3.1 Improving performance](#Improving_performance)
    *   [3.2 TCP/IP stack hardening](#TCP.2FIP_stack_hardening)
*   [4 Virtual memory](#Virtual_memory)
*   [5 MDADM](#MDADM)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Small periodic system freezes](#Small_periodic_system_freezes)
*   [7 See also](#See_also)

## Configuration

**Note:** From version 207 and 21x, [systemd](/index.php/Systemd "Systemd") only applies settings from `/etc/sysctl.d/*.conf` and `/usr/lib/sysctl.d/*.conf`. If you had customized `/etc/sysctl.conf`, you need to rename it as `/etc/sysctl.d/99-sysctl.conf`. If you had e.g. `/etc/sysctl.d/foo`, you need to rename is to `/etc/sysctl.d/foo.conf`.

The **sysctl** preload/configuration file can be created at `/etc/sysctl.d/99-sysctl.conf`. For [systemd](/index.php/Systemd "Systemd"), `/etc/sysctl.d/` and `/usr/lib/sysctl.d/` are drop-in directories for kernel sysctl parameters. The naming and source directory decide the order of processing, which is important since the last parameter processed may override earlier ones. For example, parameters in a `/usr/lib/sysctl.d/50-default.conf` will be overriden by equal parameters in `/etc/sysctl.d/50-default.conf` and any configuration file processed later from both directories.

To load all configuration files manually, execute

```
# sysctl --system 

```

which will also output the applied hierarchy. A single parameter file can also be loaded explicitly with

```
# sysctl -p *filename.conf*

```

See [the new configuration files](http://0pointer.de/blog/projects/the-new-configuration-files) and more specifically [systemd's sysctl.d man page](http://0pointer.de/public/systemd-man/sysctl.d.html) for more information.

The parameters available are those listed under `/proc/sys/`. For example, the `kernel.sysrq` parameter refers to the file `/proc/sys/kernel/sysrq` on the file system. The `sysctl -a` command can be used to display all currently available values.

**Note:** If you have the kernel documentation installed ([linux-docs](https://www.archlinux.org/packages/?name=linux-docs)), you can find detailed information about sysctl settings in `/usr/lib/modules/$(uname -r)/build/Documentation/sysctl/`. It is highly recommended reading these before changing sysctl settings.

Settings can be changed through file manipulation or using the `sysctl` utility. For example, to temporarily enable the [magic SysRq key](https://en.wikipedia.org/wiki/Magic_SysRq_key "wikipedia:Magic SysRq key"):

```
# sysctl kernel.sysrq=1

```

or:

```
# echo "1" > /proc/sys/kernel/sysrq

```

To preserve changes between reboots, add or modify the appropriate lines in `/etc/sysctl.d/99-sysctl.conf` or another applicable parameter file in `/etc/sysctl.d/`.

**Tip:** Some parameters that can be applied may depend on kernel modules which in turn might not be loaded. For example parameters in `/proc/sys/net/bridge/*` depend on the `br_netfilter` module. If it is not loaded at runtime (or after a reboot), those will *silently* not be applied. See [Kernel modules](/index.php/Kernel_modules "Kernel modules").

## Security

See [Security#Kernel hardening](/index.php/Security#Kernel_hardening "Security").

## Networking

### Improving performance

**Warning:** This may cause dropped frames with load-balancing and NATs, only use this for a server that communicates only over your local network.

```
# reuse/recycle time-wait sockets
net.ipv4.tcp_tw_reuse = 1
net.ipv4.tcp_tw_recycle = 1

```

### TCP/IP stack hardening

The following specifies a parameter set to tighten network security options of the kernel for the IPv4 protocol and related IPv6 parameters where an equivalent exists.

For some usecases, for example using the system as a [router](/index.php/Router "Router"), other parameters may be useful or required as well.

```
#### ipv4 networking and equivalent ipv6 parameters ####

## TCP SYN cookie protection (default)
## helps protect against SYN flood attacks
## only kicks in when net.ipv4.tcp_max_syn_backlog is reached
net.ipv4.tcp_syncookies = 1

## protect against tcp time-wait assassination hazards
## drop RST packets for sockets in the time-wait state
## (not widely supported outside of linux, but conforms to RFC)
net.ipv4.tcp_rfc1337 = 1

## sets the kernels reverse path filtering mechanism to value 1(on)
## will do source validation of the packet's recieved from all the interfaces on the machine
## protects from attackers that are using ip spoofing methods to do harm
net.ipv4.conf.all.rp_filter = 1
net.ipv6.conf.all.rp_filter = 1

## tcp timestamps
## + protect against wrapping sequence numbers (at gigabit speeds)
## + round trip time calculation implemented in TCP
## - causes extra overhead and allows uptime detection by scanners like nmap
## enable @ gigabit speeds
net.ipv4.tcp_timestamps = 0
#net.ipv4.tcp_timestamps = 1

## log martian packets
net.ipv4.conf.all.log_martians = 1

## ignore echo broadcast requests to prevent being part of smurf attacks (default)
net.ipv4.icmp_echo_ignore_broadcasts = 1

## ignore bogus icmp errors (default)
net.ipv4.icmp_ignore_bogus_error_responses = 1

## send redirects (not a router, disable it)
net.ipv4.conf.all.send_redirects = 0

## ICMP routing redirects (only secure)
#net.ipv4.conf.all.secure_redirects = 1 (default)
net.ipv4.conf.default.accept_redirects=0
net.ipv4.conf.all.accept_redirects=0
net.ipv6.conf.default.accept_redirects=0
net.ipv6.conf.all.accept_redirects=0
```

## Virtual memory

There are several key parameters to tune the operation of the virtual memory (VM) subsystem of the Linux kernel and the writeout of dirty data to disk. See the [Linux kernel documentation](https://www.kernel.org/doc/Documentation/sysctl/vm.txt) for more information. For example:

*   `vm.dirty_ratio = 3`

	Contains, as a percentage of total available memory that contains free pages and reclaimable pages, the number of pages at which a process which is generating disk writes will itself start writing out dirty data.

*   `vm.dirty_background_ratio = 2`

	Contains, as a percentage of total available memory that contains free pages and reclaimable pages, the number of pages at which the background kernel flusher threads will start writing out dirty data.

As noted in the comments for the parameters, one needs to consider the total amount of RAM when setting these values. For example, simplifying by taking the installed system RAM instead of available memory:

*   Consensus is that setting `vm.dirty_ratio` to 10% of RAM is a sane value if RAM is say 1 GB (so 10% is 100 MB). But if the machine has much more RAM, say 16 GB (10% is 1.6 GB), the percentage may be out of proportion as it becomes several seconds of writeback on spinning disks. A more sane value in this case is 3 (3% of 16 GB is approximately 491 MB).
*   Similarly, setting `vm.dirty_background_ratio` to 5 may be just fine for small memory values, but again, consider and adjust accordingly for the amount of RAM on a particular system.

## MDADM

When the kernel performs a resync operation of a software raid device it tries not to create a high system load by restricting the speed of the operation. Using sysctl it is possible to change the lower and upper speed limit.

```
# Set maximum and minimum speed of raid resyncing operations
dev.raid.speed_limit_max = 10000
dev.raid.speed_limit_min = 1000
```

If mdadm is compiled as a module `md_mod`, the above settings are available only after the module has been loaded. If the settings shall be loaded on boot via `/etc/sysctl.d`, the module `md_mod` may be loaded beforehand through `/etc/modules-load.d`.

## Troubleshooting

### Small periodic system freezes

Set dirty bytes to small enough value (for example 4M):

```
vm.dirty_background_bytes = 4194304
vm.dirty_bytes = 4194304

```

Try to change `kernel.io_delay_type` (x86 only):

*   0 - IO_DELAY_TYPE_0X80
*   1 - IO_DELAY_TYPE_0XED
*   2 - IO_DELAY_TYPE_UDELAY
*   3 - IO_DELAY_TYPE_NONE

## See also

*   The [sysctl(8)](http://linux.die.net/man/8/sysctl) and [sysctl.conf(5)](http://www.unixlore.net/cgi-bin/man/man2html?5+sysctl.conf) man pages
*   Linux kernel documentation (`<kernel source dir>/Documentation/sysctl/`)
*   Kernel Documentation: [IP Sysctl](https://www.kernel.org/doc/Documentation/networking/ip-sysctl.txt)
*   SysCtl.conf Tweaked for Security and Cable Speed [[1]](http://blog.gotux.net/code/config/sysctl/)
*   Kernel network parameters for sysctl [[2]](http://tldp.org/HOWTO/Adv-Routing-HOWTO/lartc.kernel.html)