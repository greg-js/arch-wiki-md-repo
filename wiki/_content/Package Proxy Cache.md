# Package Proxy Cache

If you want to install the same Arch packages over and over - like for testing AIF profiles - it could help if you wouldn't have to get the packages every time from the internet. This article shows you how to setup a [Squid](/index.php/Squid "Squid") proxy that only caches arch packages and can be used with aif/pacman/wget/etc with minimal configuration on the client system.

## Contents

*   [1 Install Squid](#Install_Squid)
*   [2 Configure Squid](#Configure_Squid)
    *   [2.1 Cache Rules](#Cache_Rules)
    *   [2.2 Maximum Filesize](#Maximum_Filesize)
    *   [2.3 Cache Directory](#Cache_Directory)
    *   [2.4 Shutdown Lifetime](#Shutdown_Lifetime)
*   [3 Start Squid](#Start_Squid)
*   [4 Follow Squid access log](#Follow_Squid_access_log)
*   [5 Manual Arch Install](#Manual_Arch_Install)

## Install Squid

 `# pacman -S squid` 

## Configure Squid

This is the minimum configuration to get squid cache arch packages.

### Cache Rules

Before defining these rules, remove/comment (if you do not need them) all the default refresh_patterns

 `/etc/squid/squid.conf ` 

```
refresh_pattern \.pkg\.tar\.   0       20%     4320      reload-into-ims
refresh_pattern .              0       0%      0
```

That should define that *.pkg.tar.* gets cached, and anything else should not.

**Tip:** [http://www.squid-cache.org/Doc/config/refresh_pattern](http://www.squid-cache.org/Doc/config/refresh_pattern)

### Maximum Filesize

Objects larger than this size will NOT be saved on disk:

 `/etc/squid/squid.conf `  `maximum_object_size 256 MB` 

**Tip:** [http://www.squid-cache.org/Doc/config/maximum_object_size](http://www.squid-cache.org/Doc/config/maximum_object_size)

### Cache Directory

Set the cache dir and its maximum size and subdirs:

 `/etc/squid/squid.conf `  `cache_dir aufs /var/cache/squid 10000 16 256` 

**Tip:** [http://www.squid-cache.org/Doc/config/cache_dir](http://www.squid-cache.org/Doc/config/cache_dir)

### Shutdown Lifetime

Time to wait until all active client sockets are closed:

 `/etc/squid/squid.conf `  `shutdown_lifetime 1 seconds ` 

**Tip:** [http://www.squid-cache.org/Doc/config/shutdown_lifetime](http://www.squid-cache.org/Doc/config/shutdown_lifetime)

**Note:**

Every time you change the cache_dir path (and after fresh install), you need to (re)create this directory:

 `# squid -z` 

and it could be helpful to check the config file before running squid:

 `# squid -k check` 

## Start Squid

 `# systemctl start squid.service` 

or if squid is already running:

 `# systemctl restart squid.service` 

**Note:**

It could be helpful to check the config file before running:

 `# squid -k check` 

## Follow Squid access log

To see the access to squid:

 `# tail -f /var/log/squid/access.log` 

You should see this for packages that are directed to original host:

 `...TCP_MISS/200...DIRECT...` 

and for packages that are delivered from the cache:

 `...TCP_HIT/200...NONE...` 

## Manual Arch Install

Before running /arch/setup, add variables for your proxy. To do so, run on the console:

```
# export http_proxy='[http://your_squid_machine_ip:3128'](http://your_squid_machine_ip:3128')
# export ftp_proxy='[ftp://your_squid_machine_ip:3128'](ftp://your_squid_machine_ip:3128')
```

Now just use /arch/setup to normally install the system, and it should use your proxy. Watch the squid logs to verify this.

**Note:** If you want to use the proxy settings in the installed system, you need to add the http_proxy and/or ftp_proxy variables in an appropriate place on the installed system. (like /etc/profile.d/proxy.sh)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Package_Proxy_Cache&oldid=404877](https://wiki.archlinux.org/index.php?title=Package_Proxy_Cache&oldid=404877)"