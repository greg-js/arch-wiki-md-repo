*rescached* is a daemon that caching internet name and address on local memory when running and in local disk when not running.

*rescached* is not a reimplementation of DNS server like BIND. *rescached* primary goal is only to caching DNS queries and answers, used by personal or small group of users, to minimize unneeded traffic to outside network.

## Contents

*   [1 Features](#Features)
*   [2 How cache in rescached works](#How_cache_in_rescached_works)
*   [3 Installation](#Installation)
*   [4 Post-installation configuration](#Post-installation_configuration)
*   [5 See also](#See_also)

## Features

*   Enable to handle request from UDP and TCP
*   Saving/loading cache to/from disk
*   Load and serve addresses and hostnames in `/etc/hosts`

## How cache in rescached works

Each of query and answer data in cache have a number of accessed field, which defined how the cache will be ordered in memory. The frequently queried host-name will be at the top of cache list, and less queried host-name will at the bottom of cache list. This, obviously, will make a cache list based on user habit (frequently accessed host-name), which effect on the search time on cache list: fast reply.

```
+-----+------------------+
| #   | host-name        |
+-----+------------------+
| 529 | www.reddit.com   |
+-----+------------------+
| 233 | www.google.com   |
+-----+------------------+
| ... |        ...       |
+-----+------------------+
| 1   | www.kilabit.info |
+-----+------------------+

```

The number of cache that rescached can hold in memory is depend on the value of *cache.max* in configuration file. When the number of cache in memory reached it *cache.max* value, it will remove all cache data that has the number of frequently accessed less than *cache.threshold*.

## Installation

Install from [rescached-git](https://aur.archlinux.org/packages/rescached-git/).

## Post-installation configuration

Default configuration setting is already working as expected.

Rescached configuration is reside in `/etc/rescached/rescached.cfg`.

*   Set your parent DNS server.

	Edit rescached configuration change the value of `server.parent` based on your preferred DNS server.

*   Set maximum caches.

	Edit rescached configuration, change the value of `cache.max` and/or `cache.threshold` to match your needs.

*   Set your system DNS server to point to rescached.

```
# mv /etc/resolv.conf /etc/resolv.conf.org
# echo "nameserver 127.0.0.1" > /etc/resolv.conf

```

*   [Start](/index.php/Start "Start") and possibly [enable](/index.php/Enable "Enable") `rescached.service`.

## See also

*   For more information and configuration see manpage of rescached
*   For non-technical explanation you can read it [here](http://kilabit.info/journal/2009/12/04__rescached_is_here/index.html)
*   For user documentation you can read it [here](http://kilabit.info/projects/rescached/doc/user/index.html)
*   Report bug and feature request [here](https://github.com/shuLhan/rescached/issues)