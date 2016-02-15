[ipset](http://ipset.netfilter.org/) is a companion application for the [iptables](/index.php/Iptables "Iptables") Linux [firewall](/index.php/Firewall "Firewall"). It allows you to setup rules to quickly and easily block a set of IP addresses, among other things.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Blocking a list of addresses](#Blocking_a_list_of_addresses)
    *   [2.2 Making ipset persistent](#Making_ipset_persistent)
    *   [2.3 Blocking With PeerGuardian and Other Blocklists](#Blocking_With_PeerGuardian_and_Other_Blocklists)
*   [3 Other Commands](#Other_Commands)

## Installation

[Install](/index.php/Install "Install") [ipset](https://www.archlinux.org/packages/?name=ipset) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

### Blocking a list of addresses

Start by creating a new "set" of network addresses. This creates a new "hash" set of "net" network addresses named "myset".

```
# ipset create myset hash:net

```

Add any IP address that you'd like to block to the set.

```
# ipset add myset 14.144.0.0/12
# ipset add myset 27.8.0.0/13
# ipset add myset 58.16.0.0/15

```

Finally, configure [iptables](/index.php/Iptables "Iptables") to block any address in that set. This command will add a rule to the top of the "INPUT" chain to "-m" match the set named "myset" from ipset (--match-set) when it's a "src" packet and "DROP", or block, it.

```
# iptables -I INPUT -m set --match-set myset src -j DROP

```

### Making ipset persistent

ipset you have created is stored in memory and will be gone after reboot. To make the ipset persistent you have to do the followings:

First save the ipset to /etc/ipset.conf:

```
# ipset save > /etc/ipset.conf

```

Then [enable](/index.php/Enable "Enable") `ipset.service`, which works similarly to `iptables.service` for restoring [iptables rules](/index.php/Iptables#Configuration_and_usage "Iptables").

### Blocking With PeerGuardian and Other Blocklists

The [pg2ipset](https://aur.archlinux.org/packages/pg2ipset/) tool by the author of maeyanie.com, coupled with the [ipset-update.sh](https://github.com/ilikenwf/pg2ipset/blob/master/ipset-update.sh) script can be used with cron to automatically update various blocklists. Currently, by default country blocking, tor exit node blocking, and pg2 list blocking from Bluetack are implemented.

## Other Commands

To view the sets:

```
# ipset list

```

To delete a set named "myset":

```
# ipset destroy myset

```

To delete all sets:

```
# ipset destroy

```

Please see the man page for ipset for further information.