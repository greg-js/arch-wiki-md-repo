From [Wikipedia:Redis](https://en.wikipedia.org/wiki/Redis "wikipedia:Redis"):

	*Redis is a software project that implements data structure servers. It is open-source, networked, in-memory, and stores keys with optional durability.*

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Client-side software](#Client-side_software)
*   [2 Configuration](#Configuration)
    *   [2.1 Listen on socket](#Listen_on_socket)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Warning about Transparent Huge Pages (THP)](#Warning_about_Transparent_Huge_Pages_.28THP.29)
    *   [3.2 Warning about TCP backlog](#Warning_about_TCP_backlog)
    *   [3.3 Warning about overcommit_memory is set to 0](#Warning_about_overcommit_memory_is_set_to_0)

## Installation

[Install](/index.php/Install "Install") the [redis](https://www.archlinux.org/packages/?name=redis) package.

[Start/enable](/index.php/Start/enable "Start/enable") `redis.service`.

### Client-side software

*   Python: [python-redis](https://www.archlinux.org/packages/?name=python-redis) and [python2-redis](https://www.archlinux.org/packages/?name=python2-redis)
*   PHP: [php-redis](https://aur.archlinux.org/packages/php-redis/)

## Configuration

The Redis configuration file is well-documented and located at `/etc/redis.conf`.

*   By default, if no "bind" configuration directive is specified, Redis listens for connections from all the network interfaces. It may be preferred to allow only access on the host instead:

```
bind 127.0.0.1

```

*   Accept connections on the specified port (default is 6379), specify `port 0` to disable listening on TCP:

```
port 6379

```

**Note:** If you change the default port, [edit](/index.php/Edit "Edit") `redis.service` and update the `ExecStop` command accordingly. Either specify the port with `-p` or the socket path with `-s`.

### Listen on socket

Using Redis over a Unix socket may give a performance increase, compared to TCP/IP [[1]](http://redis.io/topics/benchmarks).

The following changes should be made in `/etc/redis.conf` to enable use of the unix socket:

*   Enable and update the Redis socket path:

```
unixsocket /run/redis/redis.sock

```

*   Set permission to the socket to all members of the `redis` [user group](/index.php/User_group "User group"):

```
unixsocketperm 770

```

*   Add users (e.g. *git*, *http*) to the `redis` [user group](/index.php/User_group "User group") so they can access and use the socket.

Finally [restart](/index.php/Restart "Restart") the `redis.service`.

## Troubleshooting

### Warning about Transparent Huge Pages (THP)

To solve warning messages as `*you have Transparent Huge Pages (THP) support enabled in your kernel. This will create latency and memory usage issues with Redis.*`, you may want to permanently disable this feature:

 `/etc/tmpfiles.d/redis.conf` 
```
w /sys/kernel/mm/transparent_hugepage/enabled - - - - never
w /sys/kernel/mm/transparent_hugepage/defrag - - - - never

```

### Warning about TCP backlog

To solve warning messages as `*The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.*`, increase the current value:

 `/etc/sysctl.d/99-sysctl.conf` 
```
net.core.somaxconn=512

```

### Warning about overcommit_memory is set to 0

To solve warning messages as `*overcommit_memory is set to 0! Background save may fail under low memory condition*`:

 `/etc/sysctl.d/99-sysctl.conf` 
```
vm.overcommit_memory=1

```