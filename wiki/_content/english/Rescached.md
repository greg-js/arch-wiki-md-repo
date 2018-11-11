[rescached](https://github.com/shuLhan/rescached-go) is a daemon to cache internet name and address resolution in local memory when running and in a disk cache when not running.

*rescached* is not a reimplementation of a DNS server like BIND. The primary goal of *rescached* is only to cache DNS queries and answers to minimize unneeded traffic to the outside network. It is intended for personal systems or serving a small group of users.

## Contents

*   [1 Features](#Features)
*   [2 How cache in rescached works](#How_cache_in_rescached_works)
*   [3 Installation](#Installation)
*   [4 Post-installation configuration](#Post-installation_configuration)
*   [5 See also](#See_also)

## Features

*   Enable to handle requests via UDP and TCP
*   Saving/loading cache to/from disk
*   Load and serve addresses and hostnames in `/etc/hosts`

## How cache in rescached works

Each query and answer data pair in the cache is enriched with statistical usage to define how the cache will be ordered in memory. The frequently queried hostnames will be at the top of the cache list, and less queried hostnames will be at the bottom of the cache list. This, obviously, results in a cache list based on user's habits (frequently accessed hosts) and speeds up resolving accordingly.

| # | host-name |
| 529 | www.reddit.com |
| 233 | www.google.com |
| ... | ... |
| 1 | www.kilabit.info |

The number of cache entries that rescached holds in memory depends on the value of *cache.max* in the configuration file. When the *cache.max* limit is reached, the daemon will remove all cached entries which are accessed less frequently than set in *cache.threshold*.

## Installation

[Install](/index.php/Install "Install") the [rescached-git](https://aur.archlinux.org/packages/rescached-git/) package.

## Post-installation configuration

The default configuration enables a direct start of the daemon.

Rescached configuration resides in `/etc/rescached/rescached.cfg`. Select entries to change are:

*   Set your parent DNS server:

	Change the value of `server.parent` based on your preferred DNS server.

*   Set maximum caches.

	Change the value of `cache.max` and/or `cache.threshold` to match your needs.

After finishing the configuration file, modify the [resolv.conf](/index.php/Resolv.conf "Resolv.conf") file and replace the current set of resolver addresses with address for *localhost*:

```
nameserver 127.0.0.1

```

Other programs may overwrite this setting; see [Domain name resolution#Overwriting of /etc/resolv.conf](/index.php/Domain_name_resolution#Overwriting_of_.2Fetc.2Fresolv.conf "Domain name resolution") for details.

Finally, [start](/index.php/Start "Start") and possibly [enable](/index.php/Enable "Enable") `rescached.service`.

## See also

*   For more information and configuration see the manpage of rescached
*   For non-technical explanation you can read it [here](http://kilabit.info/journal/2009/12/04__rescached_is_here/index.html)
*   For user documentation you can read it [here](http://kilabit.info/projects/rescached/doc/user/index.html)
*   Report bug and feature requests are preferred on the [GitHub](https://github.com/shuLhan/rescached-go/issues)