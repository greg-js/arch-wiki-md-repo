[NSD](https://www.nlnetlabs.nl/projects/nsd/) is "an authoritative only, high performance, simple and open source name server."

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Migration to nsd for bind users](#Migration_to_nsd_for_bind_users)
*   [3 Initial setup](#Initial_setup)
*   [4 Starting and running nsd](#Starting_and_running_nsd)
*   [5 Testing nsd](#Testing_nsd)
*   [6 Configuring unbound](#Configuring_unbound)
*   [7 WAN facing dns](#WAN_facing_dns)

## Installation

[Install](/index.php/Install "Install") the [nsd](https://www.archlinux.org/packages/?name=nsd) package.

## Migration to nsd for bind users

Once the package is installed there are useful migration notes for users who currently run bind as their dns server in the file:

```
/usr/share/doc/nsd/NSD-FOR-BIND-USERS

```

Many users will wish to run nsd as their authoritative dns server concurrently with unbound as the validating, recursive, caching dns server on a single machine. It may be useful to refer to the wiki page for [unbound](/index.php/Unbound "Unbound").

## Initial setup

Most likely you will run nsd with a DNS caching servers such as [Unbound](/index.php/Unbound "Unbound"). So, to avoid void conflicts, this configuration use port 53530 for nsd, since port 53 is used by the DNS caching server. nsd will listen for requests on *localhost*. Additionally, the only firewall port that then needs to be open for dns queries coming from external machines (or other machines on the same local network) is port 53.

When installed, a commented sample configuration file is placed at `/etc/nsd/nsd.conf.sample`. Below is a minimal working example:

 `/etc/nsd/nsd.conf` 
```
server:
    server-count: 1
    ip-address: 127.0.0.1
    port: 53530
    do-ip4: yes
    hide-version: yes
    identity: "Home network authoritative DNS"
    zonesdir: "//etc/nsd"
key:
    name: "*keyname*"
    algorithm: hmac-md5
    secret: "*secretkey*"
zone:
    name: "*example.com*"
    zonefile: "*example.com.zone*"

```

See [[1]](https://calomel.org/nsd_dns.html) for more examples.

## Starting and running nsd

Before starting up nsd you can check the zone files using the *nsd-checkconf* command with the zone file name as a parameter.

In order to build the zone database that makes nsd run exceptionally quickly the database file must be rebuilt each time a zone or config file is changed, and the following command is executed:

```
# nsd-control reload

```

In order to start nsd, [start/enable](/index.php/Start/enable "Start/enable") the `nsd.service` systemd service.

## Testing nsd

nsd can be run concurrently with bind during the testing phase. You can check forward and reverse local lookups on the port at 53530 using:

```
drill @127.0.0.1 -p 53530 mylocalmachine1.myhomenet.com
drill @127.0.0.1 -p 53530 -x w.x.y.z

```

where w.x.y.z is a local address within the LAN.

## Configuring unbound

Once this is working then if you are running [unbound](/index.php/Unbound "Unbound") as the caching recursive server then you can switch the unbound configuration to forward queries from local machines on the same network to query nsd by using the following structure in unbound.conf (and see [unbound](/index.php/Unbound "Unbound")), where it is assumed that nsd is listening to port 53530:

```
do-not-query-localhost: no
local-zone: "*example.com*" nodefault
domain-insecure: "*example.com*"

```

```
stub-zone:
       name: "*example.com*"
       stub-addr: 127.0.0.1@53530

```

Once the unbound.conf contains the above then restart unbound and check that local queries for the nsd zone entries works. Once it is all tested then you can switch unbound to listen on both 127.0.0.1 as well as on the external interface for the local network by having the lines in unbound.conf including:

```
   interface: 127.0.0.1
   interface: 10.0.0.1

```

where 10.0.0.1 is the ip address of the dns server running both nsd and unbound and providing local dns for other machines on the 10.x.x.x network.

The examples here all assume that only ipv4 is being used. Corresponding configurations for ipv6 should be included where necessary, and further details on the parameters for that can be found in the man files for the two packages as well as examples that can be found with web searches.

## WAN facing dns

It is also possible to change the configuration files and interfaces on which the server is listening so that dns queries from machines outside of the local network can access specific machines within the LAN. This is useful for web and mail servers which are accessible from anywhere, and the same techniques can be employed as has been achieved using bind for many years, in combination with appropriate port forwarding in the network firewall machines, to allow incoming requests to access the correct machine.