## Contents

*   [1 Users](#Users)
*   [2 Firewall](#Firewall)
    *   [2.1 Incoming traffic to dom0 (INPUT chain)](#Incoming_traffic_to_dom0_(INPUT_chain))
    *   [2.2 Outgoing traffoc from dom0 (OUTPUT chain)](#Outgoing_traffoc_from_dom0_(OUTPUT_chain))
    *   [2.3 Incoming traffic to gerolde (FORWARD chain)](#Incoming_traffic_to_gerolde_(FORWARD_chain))
    *   [2.4 Incoming traffic to gudrun (FORWARD chain)](#Incoming_traffic_to_gudrun_(FORWARD_chain))
    *   [2.5 Traffic from gudrun to gerolde (FORWARD chain)](#Traffic_from_gudrun_to_gerolde_(FORWARD_chain))
    *   [2.6 Outgoing traffic from gerolde (FORWARD chain)](#Outgoing_traffic_from_gerolde_(FORWARD_chain))
    *   [2.7 Outgoing traffic from gudrun (FORWARD chain)](#Outgoing_traffic_from_gudrun_(FORWARD_chain))

## Users

| UID | User | Primary Purpose | Cronjobs | Owned Directories |
 dale | Emergency access from the console | no |
 aaron | Overlord stuff | no |
 jgc | Xen maintenance | no |
 thomas | Firewall maintenance | no |

## Firewall

The firewall script is in */usr/sbin/firewall.sh*. It is being maintained in a git repository. Clone it using

```
git clone file:///srv/firewall.git

```

Make sure to commit and push all changes when copying the script to /usr/sbin. Obviously, also don't break the script.

The firewall divides traffic into seven groups:

### Incoming traffic to dom0 (INPUT chain)

The only allowed incoming traffic to dom0 is *ssh* access from a small set of hosts.

### Outgoing traffoc from dom0 (OUTPUT chain)

All outgoing traffic is allowed.

### Incoming traffic to gerolde (FORWARD chain)

Limited to *ssh*, *rsync*, *smtp(s)*, developer package access and munin monitoring from Dan's server.

### Incoming traffic to gudrun (FORWARD chain)

Limited to *http(s)*, *svnserve*, *git* and munin monitoring from Dan's server.

### Traffic from gudrun to gerolde (FORWARD chain)

Only *smtp(s)*, package access and NFS/portmap are allowed. All NFS server services on gerolde must use fixed ports.

### Outgoing traffic from gerolde (FORWARD chain)

All outgoing traffic is allowed.

### Outgoing traffic from gudrun (FORWARD chain)

Only DNS is allowed, everything else is blocked.