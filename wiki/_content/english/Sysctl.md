[sysctl](https://en.wikipedia.org/wiki/sysctl "wikipedia:sysctl") is a tool for examining and changing [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") at runtime (package [procps-ng](https://www.archlinux.org/packages/?name=procps-ng) in [official repositories](/index.php/Official_repositories "Official repositories")). sysctl is implemented in procfs, the virtual process file system at `/proc/`.

## Contents

*   [1 Configuration](#Configuration)
*   [2 Security](#Security)
*   [3 Networking](#Networking)
    *   [3.1 Improving performance](#Improving_performance)
        *   [3.1.1 Increasing the size of the receive queue.](#Increasing_the_size_of_the_receive_queue.)
        *   [3.1.2 Increase the maximum connections](#Increase_the_maximum_connections)
        *   [3.1.3 Increase the memory dedicated to the network interfaces](#Increase_the_memory_dedicated_to_the_network_interfaces)
        *   [3.1.4 Enable TCP Fast Open](#Enable_TCP_Fast_Open)
        *   [3.1.5 Tweak the pending connection handling](#Tweak_the_pending_connection_handling)
        *   [3.1.6 Change TCP keepalive parameters](#Change_TCP_keepalive_parameters)
        *   [3.1.7 Enable MTU probing](#Enable_MTU_probing)
        *   [3.1.8 TCP Timestamps](#TCP_Timestamps)
    *   [3.2 TCP/IP stack hardening](#TCP.2FIP_stack_hardening)
        *   [3.2.1 TCP SYN cookie protection](#TCP_SYN_cookie_protection)
        *   [3.2.2 TCP rfc1337](#TCP_rfc1337)
        *   [3.2.3 Reverse path filtering](#Reverse_path_filtering)
        *   [3.2.4 Log martian packets](#Log_martian_packets)
        *   [3.2.5 Ignore echo broadcast requests](#Ignore_echo_broadcast_requests)
        *   [3.2.6 ICMP routing and redirecting](#ICMP_routing_and_redirecting)
*   [4 Virtual memory](#Virtual_memory)
*   [5 MDADM](#MDADM)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Small periodic system freezes](#Small_periodic_system_freezes)
*   [7 See also](#See_also)

## Configuration

**Note:** From version 207 and 21x, [systemd](/index.php/Systemd "Systemd") only applies settings from `/etc/sysctl.d/*.conf` and `/usr/lib/sysctl.d/*.conf`. If you had customized `/etc/sysctl.conf`, you need to rename it as `/etc/sysctl.d/99-sysctl.conf`. If you had e.g. `/etc/sysctl.d/foo`, you need to rename it to `/etc/sysctl.d/foo.conf`.

The **sysctl** preload/configuration file can be created at `/etc/sysctl.d/99-sysctl.conf`. For [systemd](/index.php/Systemd "Systemd"), `/etc/sysctl.d/` and `/usr/lib/sysctl.d/` are drop-in directories for kernel sysctl parameters. The naming and source directory decide the order of processing, which is important since the last parameter processed may override earlier ones. For example, parameters in a `/usr/lib/sysctl.d/50-default.conf` will be overriden by equal parameters in `/etc/sysctl.d/50-default.conf` and any configuration file processed later from both directories.

To load all configuration files manually, execute

```
# sysctl --system 

```

which will also output the applied hierarchy. A single parameter file can also be loaded explicitly with

```
# sysctl -p *filename.conf*

```

See [the new configuration files](http://0pointer.de/blog/projects/the-new-configuration-files) and more specifically [sysctl.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sysctl.d.5) for more information.

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

#### Increasing the size of the receive queue.

The received frames will be stored in this queue after taking them from the ring buffer on the network card.

Increasing this value for high speed cards may help prevent losing packets.

```
net.core.netdev_max_backlog = 65536

```

**Note:** In real time application like SIP routers, this option requires a high speed CPU otherwise the data in the queue will be out of date.

Increase the maximum ancillary buffer size allowed per socket.

The ancillary buffer is a sequence that contains the size and protocol of incoming packets.

```
net.core.optmem_max = 65536

```

#### Increase the maximum connections

The upper limit on how many connections the kernel will accept.

```
net.core.somaxconn = 16384

```

**Note:** Increasing this value will only improve performance in high load servers with high/bursty traffic

#### Increase the memory dedicated to the network interfaces

*   The default and maximum amount for the receive/send socket memory
*   By default the Linux network stack is not configured for high speed large file transfer across WAN links.
*   This is done to save memory resources.
*   You can easily tune Linux network stack by increasing network buffers size for high-speed networks that connect server systems to handle more network packets.

```
net.core.rmem_default = 1048576
net.core.wmem_default = 1048576
net.core.rmem_max = 16777216
net.core.wmem_max = 16777216
net.ipv4.tcp_rmem = 4096 87380 16777216
net.ipv4.tcp_wmem = 4096 65536 16777216
net.ipv4.udp_rmem_min = 16384
net.ipv4.udp_wmem_min = 16384

```

#### Enable TCP Fast Open

TCP Fast Open is an extension to the transmission control protocol (TCP) that helps reduce network latency by enabling data to be exchanged during the sender’s initial TCP SYN.

```
net.ipv4.tcp_fastopen = 3

```

**Note:** If both of your server and client are deployed on Linux 3.7.1 or higher, you can turn on fast_open for lower latency

#### Tweak the pending connection handling

`tcp_max_syn_backlog` is the maximum queue length of pending connections 'Waiting Acknowledgment'.

In the event of a synflood DOS attack, this queue can fill up pretty quickly, at which point tcp_syncookies will kick in allowing your system to continue to respond to legitimate traffic, and allowing you to gain access to block malicious IPs.

If the server suffers from overloads at peak times, you may want to increase this value a little bit:

```
net.ipv4.tcp_max_syn_backlog = 65536

```

`tcp_max_tw_buckets` is the maximum number of sockets in 'TIME_WAIT' state.

After reaching this number the system will start destroying the socket that are in this state.

Increase this to prevent simple DOS attacks:

```
net.ipv4.tcp_max_tw_buckets = 65536

```

`tcp_slow_start_after_idle` sets whether TCP should start at the default window size only for new connections or also for existing connections that have been idle for too long.

This setting kills persistent single connection performance and could be turned off:

```
net.ipv4.tcp_slow_start_after_idle = 0

```

`tcp_tw_reuse` sets whether TCP should reuse an existing connection in the TIME-WAIT state for a new outgoing connection if the new timestamp is strictly bigger than the most recent timestamp recorded for the previous connection.

This helps avoid from running out of available network sockets:

```
net.ipv4.tcp_tw_reuse = 1

```

Fast-fail FIN connections which are useless:

```
net.ipv4.tcp_fin_timeout = 15

```

The TCP window scale option is an option to increase the receive window size allowed in Transmission Control Protocol above its former maximum value of 65,535 bytes:

```
net.ipv4.tcp_window_scaling = 1

```

#### Change TCP keepalive parameters

*   TCP keepalive is a mechanism for TCP connections that help to determine whether the other end has stopped responding or not.
*   TCP will send the keepalive probe contains null data to the network peer several times after a period of idle time. If the peer does not respond, the socket will be closed automatically.
*   By default, TCP keepalive process waits for two hours (7200 secs) for socket activity before sending the first keepalive probe, and then resend it every 75 seconds. As long as there is TCP/IP socket communications going on and active, no keepalive packets are needed.

**Note:** With the following settings, your application will detect dead TCP connections after 120 seconds (60s + 10s + 10s + 10s + 10s + 10s + 10s)

```
net.ipv4.tcp_keepalive_time = 60
net.ipv4.tcp_keepalive_intvl = 10
net.ipv4.tcp_keepalive_probes = 6

```

#### Enable MTU probing

The longer the MTU the better for performance, but the worse for reliability.

This is because a lost packet means more data to be retransmitted and because many routers on the Internet can't deliver very long packets.

```
net.ipv4.tcp_mtu_probing = 1

```

#### TCP Timestamps

TCP timestamps protect against wrapping sequence numbers (at gigabit speeds) and round trip time calculation implemented in TCP.

Disabling timestamp generation will reduce spikes and may give a performance boost on gigabit networks:

```
net.ipv4.tcp_timestamps = 0

```

### TCP/IP stack hardening

The following specifies a parameter set to tighten network security options of the kernel for the IPv4 protocol and related IPv6 parameters where an equivalent exists.

For some use-cases, for example using the system as a [router](/index.php/Router "Router"), other parameters may be useful or required as well.

#### TCP SYN cookie protection

Helps protect against SYN flood attacks. Only kicks in when `net.ipv4.tcp_max_syn_backlog` is reached:

```
net.ipv4.tcp_syncookies = 1

```

#### TCP rfc1337

Protect against tcp time-wait assassination hazards, drop RST packets for sockets in the time-wait state. Not widely supported outside of Linux, but conforms to RFC:

```
net.ipv4.tcp_rfc1337 = 1

```

#### Reverse path filtering

Sets the kernels reverse path filtering mechanism to value 1 (on). Will do source validation of the packet's received from all the interfaces on the machine. Protects from attackers that are using ip spoofing methods to do harm (default):

```
net.ipv4.conf.default.rp_filter = 1
net.ipv4.conf.all.rp_filter = 1

```

#### Log martian packets

```
net.ipv4.conf.default.log_martians = 1
net.ipv4.conf.all.log_martians = 1

```

#### Ignore echo broadcast requests

Prevent being part of smurf attacks:

```
net.ipv4.icmp_echo_ignore_broadcasts = 1

```

#### ICMP routing and redirecting

```
net.ipv4.icmp_ignore_bogus_error_responses = 1
#net.ipv4.conf.default.secure_redirects = 1 (default)
#net.ipv4.conf.all.secure_redirects = 1 (default)
net.ipv4.conf.default.send_redirects = 0
net.ipv4.conf.all.send_redirects = 0
net.ipv4.conf.default.accept_redirects = 0
net.ipv4.conf.all.accept_redirects = 0
net.ipv6.conf.default.accept_redirects = 0
net.ipv6.conf.all.accept_redirects = 0

```

## Virtual memory

There are several key parameters to tune the operation of the virtual memory (VM) subsystem of the Linux kernel and the write out of dirty data to disk. See the official [Linux kernel documentation](https://www.kernel.org/doc/Documentation/sysctl/vm.txt) for more information. For example:

*   `vm.dirty_ratio = 3`

	Contains, as a percentage of total available memory that contains free pages and reclaimable pages, the number of pages at which a process which is generating disk writes will itself start writing out dirty data.

*   `vm.dirty_background_ratio = 2`

	Contains, as a percentage of total available memory that contains free pages and reclaimable pages, the number of pages at which the background kernel flusher threads will start writing out dirty data.

As noted in the comments for the parameters, one needs to consider the total amount of RAM when setting these values. For example, simplifying by taking the installed system RAM instead of available memory:

*   Consensus is that setting `vm.dirty_ratio` to 10% of RAM is a sane value if RAM is say 1 GB (so 10% is 100 MB). But if the machine has much more RAM, say 16 GB (10% is 1.6 GB), the percentage may be out of proportion as it becomes several seconds of writeback on spinning disks. A more sane value in this case is 3 (3% of 16 GB is approximately 491 MB).
*   Similarly, setting `vm.dirty_background_ratio` to 5 may be just fine for small memory values, but again, consider and adjust accordingly for the amount of RAM on a particular system.

Another parameter is:

*   `vm.vfs_cache_pressure = 60`

	The value controls the tendency of the kernel to reclaim the memory which is used for caching of directory and inode objects (VFS cache). Lowering it from the default value of 100 makes the kernel less inclined to reclaim VFS cache (do not set it to 0, this may produce out-of-memory conditions).

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

*   [sysctl(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sysctl.8) and [sysctl.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sysctl.conf.5)
*   [Linux kernel documentation for /proc/sys/](https://www.kernel.org/doc/Documentation/sysctl/)
*   Kernel Documentation: [IP Sysctl](https://www.kernel.org/doc/Documentation/networking/ip-sysctl.txt)
*   [Kernel network parameters for sysctl](http://tldp.org/HOWTO/Adv-Routing-HOWTO/lartc.kernel.html)