This page is for planning.

## Contents

*   [1 Packaging notes](#Packaging_notes)
    *   [1.1 Units](#Units)
        *   [1.1.1 Example of a simple conversion](#Example_of_a_simple_conversion)
    *   [1.2 tmpfiles.d](#tmpfiles.d)
    *   [1.3 modules-load.d](#modules-load.d)
    *   [1.4 sysctl.d](#sysctl.d)

## Packaging notes

### Units

*   Use the upstream unit files whenever they exist
*   Try not to do anything Arch-specific. This will maximize chances of not having to change behavior in the future once the unit files are provided by upstream. In particular avoid `EnvironmentFile=`, especially if it points to the Arch-specific `/etc/conf.d`
*   Always separate initialization behavior from the actual daemon behavior. If necessary, use a separate unit for the initialization, blocked on a ConditionFoo from `systemd.unit(5)`. An example of this is `sshd.service` and `sshdgenkeys.service`.

Not using an `EnvironmentFile=` is OK if:

*   Either the daemon has its own configuration file where the same settings can be specified
*   The default service file "just works" in the most common case. Users who want to change the behavior should then override the default service file. If it is not possible to provide a sane default service file, it should be discussed on a case-by-case basis

A few comments about service files, assuming current behavior should be roughly preserved, and fancy behavior avoided:

*   If your service requires the network to be configured before it starts, use `After=network.target`. Do **not** use `Wants=network.target` or `Requires=network.target`
*   Use `Type=forking`, unless you know it's not necessary
    *   Many daemons use the exit of the first process to signal that they are ready, so to minimize problems, it is safest to use this mode
    *   To make sure that systemd is able to figure out which process is the main process, tell the daemon to write a pidfile and point systemd to it using `PIDFile=`
    *   If the daemon in question is dbus-activated, socket-activated, or specifically supports `Type=notify`, that's a different matter, but currently only the case for a minority of daemons
*   Arch's rc scripts do not support dependencies, but with systemd they should be added add where necessary
    *   The most typical case is that `A` requires the service `B` to be running before `A` is started. In that case add `Requires=B` and `After=B` to `A`.
    *   If the dependency is optional then add `Wants=B` and `After=B` instead
    *   Dependencies are typically placed on services and not on targets

If you want to get fancy, you should know what you are doing.

#### Example of a simple conversion

|  `rc script` 
```
#!/bin/bash

. /etc/rc.conf
. /etc/rc.d/functions

case "$1" in
  start)
    stat_busy "Starting NIS Server"
    /usr/sbin/ypserv
    if [ $? -gt 0 ]; then
      stat_fail
    else
      add_daemon ypserv
      stat_done
    fi
    ;;
  stop)
    stat_busy "Stopping NIS Server"
    killall -q /usr/sbin/ypserv
    if [ $? -gt 0 ]; then
      stat_fail
    else
      rm_daemon ypserv
      stat_done
    fi
    ;;
  restart)
    $0 stop
    sleep 1
    $0 start
    ;;
  *)
    echo "usage: $0 {start
```
 |  `systemd service file` 
```
[Unit]
Description=NIS/YP (Network Information Service) Server
Requires=rpcbind.service
After=network.target rpcbind.service

[Service]
Type=forking
PIDFile=/run/ypserv.pid
ExecStart=/usr/sbin/ypserv

[Install]
WantedBy=multi-user.target
```
 |

**Note:** Keep in mind that values to keys such as ExecStart and ExecStop are **not** run within a shell, but only passed to `execv`

### tmpfiles.d

*   Instead of creating necessary runtime directories and files when a service is started (as some rc scripts do), ship a `tmpfiles.d(5)` config file in `/usr/lib/tmpfiles.d`.
*   A pacman hook included in systemd will run `systemd-tmpfiles --create foo.conf` upon install to ensure the necessary runtime files are created right away, not just on the next boot

**Tip:** This feature can be used for a whole lot of other things, e.g. for writing to arbitrary files, even in /sys

### modules-load.d

*   Instead of loading necessary modules when a service is started (as some rc scripts do), ship a `modules-load.d(5)` config file in `/usr/lib/modules-load.d`.
*   Add `modprobe` lines to `post_install` (and `post_upgrade` if needed) to ensure the necessary modules are loaded on install, not just on the next boot

### sysctl.d

*   IMO(dreisner): This should generally be avoided, as tying low level kernel behavior to a package might be considered evil.