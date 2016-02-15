## Contents

*   [1 Introduction](#Introduction)
*   [2 6in4-tunnel rc.d script](#6in4-tunnel_rc.d_script)
    *   [2.1 6in4-tunnel configuration](#6in4-tunnel_configuration)
    *   [2.2 6in4-tunnel usage](#6in4-tunnel_usage)
    *   [2.3 Boot-time configuration](#Boot-time_configuration)

## Introduction

[http://en.wikipedia.org/wiki/6in4](http://en.wikipedia.org/wiki/6in4)

## 6in4-tunnel rc.d script

Arch Linux uses a BSD-style network interface configuration located in _/etc/rc.conf_, which can make exotic network configurations interesting, to say the least. The following rc.d script is meant to help remedy the situation by providing a configurable wrapper to sanely manage a 6in4 link interface.

*   This script uses the _route2_ method; make sure that the **iproute2** package is installed.

As _root_, write the following rc.d init script to _/etc/rc.d/6in4-tunnel_:

```
#!/bin/bash

### begin user configuration

##############################################
#                                            #
#  Stop this script before you reconfigure!  #
#                                            #
##############################################

# if_name     - interface name that is to be created for the 6in4 link
if_name=6in4

# server_ipv4 - ipv4 address of the server that is providing the 6in4 tunnel
server_ipv4=127.0.0.1

# client_ipv4 - ipv4 address of the client that is receiving the 6in4 tunnel
client_ipv4=127.0.0.1

# client_ipv6 - ipv6 address of the client 6in4 tunnel endpoint
client_ipv6=2001:feed:face:beef::2/64

# link_mtu    - set the mtu for the 6in4 link
link_mtu=1480

# tunnel_ttl  - set the ttl for the 6in4 tunnel
tunnel_ttl=64

### end user configuration

daemon_name=6in4-tunnel

. /etc/rc.conf
. /etc/rc.d/functions

case "$1" in
  start)
    stat_busy "Starting $daemon_name daemon"

    ifconfig $if_name &>/dev/null
    if [ $? -eq 0 ]; then
      stat_busy "Interface $if_name already exists"
      stat_fail
      exit 1
    fi

    ip tunnel add $if_name mode sit remote $server_ipv4 local $client_ipv4 ttl $tunnel_ttl
    ip link set $if_name up mtu $link_mtu
    ip addr add $client_ipv6 dev $if_name
    ip route add ::/0 dev $if_name

    add_daemon $daemon_name
    stat_done
    ;;

  stop)
    stat_busy "Stopping $daemon_name daemon"

    ifconfig $if_name &>/dev/null
    if [ $? -ne 0 ]; then
      stat_busy "Interface $if_name does not exist"
      stat_fail
      exit 1
    fi

    ip link set $if_name down
    ip tunnel del $if_name

    rm_daemon $daemon_name
    stat_done
    ;;

  *)
    echo "usage: $0 {start|stop}"
esac
exit 0

```

### 6in4-tunnel configuration

You will need to provide your 6in4 link configuration between the following sections of _/etc/rc.d/6in4-tunnel_:

```
### begin user configuration

```

```
### end user configuration

```

Once _/etc/rc.d/6in4-tunnel_ has been configured properly, give it permission to be executed:

```
# chmod +x /etc/rc.d/6in4-tunnel

```

### 6in4-tunnel usage

To create the 6in4 tunnel link and bring up the interface:

```
# /etc/rc.d/6in4-tunnel start

```

To delete the 6in4 tunnel link and remove the interface:

```
# /etc/rc.d/6in4-tunnel stop

```

### Boot-time configuration

The following method allows _/etc/rc.d/6in4-tunnel_ to start automatically at system startup.

*   Verify that the 6in4 tunnel link is configured and working properly before doing this!

As _root_, insert _6in4-tunnel_ right after _network_ in the **DAEMONS** line of _/etc/rc.conf_.

After this addition, the **DAEMONS** line in _/etc/rc.conf_ should look something like this:

```
...

# 
# -----------------------------------------------------------------------
# DAEMONS
# -----------------------------------------------------------------------
#
# Daemons to start at boot-up (in this order)
#   - prefix a daemon with a ! to disable it
#   - prefix a daemon with a @ to start it up in the background
#
DAEMONS=(syslog-ng iptables ip6tables network 6in4-tunnel openntpd ...

...

```