# Snmpd

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

_**[SNMP](http://en.wikipedia.org/wiki/Simple_Network_Management_Protocol)** is a tool designed for the management and monitoring of network devices. The Net-SNMP package is one implementation of SNMP that is available for Arch Linux. This article discusses the configuration and testing of the snmpd daemon that ships with Arch's net-snmp package._

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Daemon](#Daemon)
    *   [2.2 SNMP 1 and 2c](#SNMP_1_and_2c)
    *   [2.3 SNMP 3](#SNMP_3)
    *   [2.4 Start Daemon](#Start_Daemon)
*   [3 Testing](#Testing)

## Installation

There is one package for net-snmp in Arch Linux which contains both the snmpd daemon, and the accompanying utilities.

```
# pacman -S net-snmp

```

## Configuration

Note that it is crucial that the snmpd service is not running while editing configuration files for it, especially `/var/net-snmp/snmpd.conf`.

### Daemon

Enable the daemon

```
systemctl enable snmpd

```

### SNMP 1 and 2c

There are three versions of SNMP which are supported by net-snmp: 1, 2c and 3\. Versions 1 and 2c start with the same basic configuration, using `/etc/snmp/snmpd.conf`.

```
mkdir /etc/snmp/
echo rocommunity _read_only_user_ >> /etc/snmp/snmpd.conf

```

The above commands will add a user that can be used for monitoring. Optionally, you can add another user used for management. This is not recommended unless you have a specific reason.

```
echo rwcommunity _read_write_user_ >> /etc/snmp/snmpd.conf

```

### SNMP 3

SNMP v3 adds security and encrypted authentication/communication. It uses a different configuration scheme in `/etc/snmp/snmpd.conf` and additional configuration in `/var/net-snmp/snmpd.conf`.

```
mkdir /etc/snmp/
echo rouser _read_only_user_ >> /etc/snmp/snmpd.conf
mkdir -p /var/net-snmp/
echo createUser _read_only_user_ SHA _password1_ AES _password2_ > /var/net-snmp/snmpd.conf

```

Note that once snmpd is restarted, `/var/net-snmp/snmpd.conf` will be rewritten, and the clear-text passwords that you have entered will be encrypted. If this file is modified while snmpd is running, any changes will be reset when the daemon is stopped. Therefore, it is crucial that snmpd is not running while this file is being updated.

### Start Daemon

After configuring the daemon, start it

```
systemctl start snmpd

```

## Testing

If using SNMP 1 or 2c, use one of the following commands to test configuration:

```
# snmpwalk -v 1 -c _read_only_user_ localhost | less
# snmpwalk -v 2c -c _read_only_user_ localhost | less

```

If using SNMP 3, use the following command to test configuration:

```
# snmpwalk -v 3 -u _read_only_user_ -a SHA -A _password1_ -x AES -X _password2_ -l authNoPriv localhost | less

```

Either way, you should see several lines of data looking something like:

```
SNMPv2-MIB::sysDescr.0 = STRING: Linux myhost 2.6.37-ARCH #1 SMP PREEMPT Sat Jan 29 20:00:33 CET 2011 x86_64
SNMPv2-MIB::sysObjectID.0 = OID: ccitt.1
DISMAN-EVENT-MIB::sysUpTimeInstance = Timeticks: (307772) 0:51:17.72
SNMPv2-MIB::sysContact.0 = STRING: root@localhost
SNMPv2-MIB::sysName.0 = STRING: myhost
...SNIP...

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Snmpd&oldid=363973](https://wiki.archlinux.org/index.php?title=Snmpd&oldid=363973)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Network monitoring](/index.php/Category:Network_monitoring "Category:Network monitoring")