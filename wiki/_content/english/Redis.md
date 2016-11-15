From [Wikipedia:Redis](https://en.wikipedia.org/wiki/Redis "wikipedia:Redis"):

	*Redis is a software project that implements data structure servers. It is open-source, networked, in-memory, and stores keys with optional durability.*

## Installation

[Install](/index.php/Install "Install") the [redis](https://www.archlinux.org/packages/?name=redis) package.

[Start/enable](/index.php/Start/enable "Start/enable") `redis.service`.

## Configuration

The Redis configuration file is well-documented and located at `/etc/redis.conf`.

*   By default, if no "bind" configuration directive is specified, Redis listens for connections from all the network interfaces. it may be preferred to allow only access on the host instead:

```
bind 127.0.0.1

```

*   Accept connections on the specified port (default is 6379), specify `port 0` to disable listing on TCP:

```
port 6379 

```

### Listen on socket

Using Redis over an Unix socket may give a performance increase, compared to TCP/IP [[1]](http://redis.io/topics/benchmarks).

The following changes should be made in `/etc/redis.conf` to enable use of the unix socket:

*   Enable and update the Redis socket path:

```
unixsocket /var/run/redis/redis.sock

```

*   Set permission to the socket to all members of the redis [group](/index.php/Group "Group"):

```
unixsocketperm 770

```

*   Create the directory which contains the socket:

```
mkdir /var/run/redis
chown redis:redis /var/run/redis
chmod 755 /var/run/redis

```

*   Persist the directory which contains the socket:

 `/etc/tmpfiles.d/redis.conf`  `d  /var/run/redis  0755  redis  redis  10d  -` 

*   Add users (e.g. *git*, *http*) to the *redis* [group](/index.php/Group "Group") so they can access and use the socket.

Finally restart the `redis.service`.