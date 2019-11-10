Related articles

*   [Redis](/index.php/Redis "Redis")

From [Wikipedia:memcached](https://en.wikipedia.org/wiki/memcached "wikipedia:memcached"):

Memcached (pronunciation: mem-cashed, mem-cash-dee) is a general-purpose distributed memory caching system. It is often used to speed up dynamic database-driven websites by caching data and objects in RAM to reduce the number of times an external data source (such as a database or API) must be read.

The system uses a client–server architecture. The servers maintain a key–value associative array; the clients populate this array and query it by key. Keys are up to 250 bytes long and values can be at most 1 megabyte in size.

Clients use client-side libraries to contact the servers which, by default, expose their service at port 11211\. Both TCP and UDP are supported. Each client knows all servers; the servers do not communicate with each other. If a client wishes to set or read the value corresponding to a certain key, the client's library first computes a hash of the key to determine which server to use. This gives a simple form of sharding and scalable shared-nothing architecture across the servers.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Client-side software](#Client-side_software)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [memcached](https://www.archlinux.org/packages/?name=memcached) package.

## Configuration

Since 1.5.6 memcached defaults to listening only on TCP. `-l` allows you to bind to specific interfaces or IP addresses By default, memcached listens for connections only on local network interfaces. It may be preferred to change the `-l` option to allow listening on external addresses instead. The service does not have a configuration file in `/etc`, The options for the service can be edited by editing the systemd unit. See `man memcached`.

```
systemctl edit memcached.service --full

```

This will copy /usr/lib/systemd/system/memcached.service to /etc/systemd/system/memcached.service and open an editor for the latter file.

**Note:** The default editor is nano. To change the editor used by systemd change `SYSTEMD_EDITOR` environment variable like: `SYSTEMD_EDITOR=vim systemctl edit memcached.service --full` See `man systemctl` for details.

Then start and/or enable the server with:

```
systemctl start memcached.service
systemctl enable memcached.service

```

## Client-side software

*   C/C++: [libmemcached](https://www.archlinux.org/packages/?name=libmemcached)
*   Python: [python-binary-memcached](https://www.archlinux.org/packages/?name=python-binary-memcached), [python-memcached](https://www.archlinux.org/packages/?name=python-memcached), [python-pylibmc](https://www.archlinux.org/packages/?name=python-pylibmc), [python2-memcached](https://www.archlinux.org/packages/?name=python2-memcached) and [python2-pylibmc](https://www.archlinux.org/packages/?name=python2-pylibmc)
*   Perl: [perl-cache-memcached](https://www.archlinux.org/packages/?name=perl-cache-memcached)
*   Gambas: [gambas3-gb-memcached](https://www.archlinux.org/packages/?name=gambas3-gb-memcached)

## See also

*   [unix.stackexchange.com](https://unix.stackexchange.com/questions/176916/where-is-the-memcached-configuration-file-in-archlinux)
*   [Github wiki Configuring Server](https://github.com/memcached/memcached/wiki/ConfiguringServer)