[Unbound](https://unbound.net/) is a validating, recursive, and caching DNS resolver. According to [Wikipedia:Unbound (DNS Server)](https://en.wikipedia.org/wiki/Unbound_(DNS_Server) "wikipedia:Unbound (DNS Server)"), "Unbound has supplanted the Berkeley Internet Name Domain ([BIND](/index.php/BIND "BIND")) as the default, base-system name server in several open source projects, where it is perceived as smaller, more modern, and more secure for most applications."

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Access control](#Access_control)
    *   [2.2 Root hints](#Root_hints)
    *   [2.3 Local DNS server](#Local_DNS_server)
    *   [2.4 DNSSEC validation](#DNSSEC_validation)
    *   [2.5 Forwarding queries](#Forwarding_queries)
*   [3 Usage](#Usage)
    *   [3.1 Starting Unbound](#Starting_Unbound)
    *   [3.2 Remotely control Unbound](#Remotely_control_Unbound)
        *   [3.2.1 Setting up unbound-control](#Setting_up_unbound-control)
        *   [3.2.2 Using unbound-control](#Using_unbound-control)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Block advertising](#Block_advertising)
    *   [4.2 Adding an authoritative DNS server](#Adding_an_authoritative_DNS_server)
    *   [4.3 WAN facing DNS](#WAN_facing_DNS)
    *   [4.4 Roothints systemd timer](#Roothints_systemd_timer)
    *   [4.5 Sandboxing](#Sandboxing)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Issues concerning num-threads](#Issues_concerning_num-threads)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [unbound](https://www.archlinux.org/packages/?name=unbound) package.

Additionally, the [expat](https://www.archlinux.org/packages/?name=expat) package is required for [DNSSEC](/index.php/DNSSEC "DNSSEC") validation.

## Configuration

A default configuration is already included at`/etc/unbound/unbound.conf`. Additionally, there is a commented sample configuration file with other available options located at `/etc/unbound/unbound.conf.example`. The following sections highlight different settings for the configuration file. See `man unbound.conf` for other settings and more details.

Unless otherwise specified, any options listed in this section are to be placed under the `server` section in the configuration like so:

 `/etc/unbound/unbound.conf` 
```
server:
  ...
  *setting*: *value*
  ...

```

### Access control

You can specify the interfaces to answer queries from by IP address. To listen on *localhost*, use the default setting:

```
interface: 127.0.0.1

```

To listen on all interfaces, use the following:

```
interface: 0.0.0.0

```

To control which systems can access the server by IP address, use the `access-control` option:

```
access-control: *subnet* *action*

```

For example:

```
access-control: 192.168.1.0/24 allow

```

*action* can be one of `deny` (drop message), `refuse` (polite error reply), `allow` (recursive ok), or `allow_snoop` (recursive and nonrecursive ok). By default everything is refused except for localhost.

### Root hints

For querying a host that is not cached as an address the resolver needs to start at the top of the server tree and query the root servers to know where to go for the top level domain for the address being queried. Unbound comes with default builtin hints, but it is good practice to use a root-hints file since the builtin hints may become outdated.

First point *unbound* to the `root.hints` file:

```
root-hints: "/etc/unbound/root.hints"

```

Then, put a *root hints* file into the *unbound* configuration directory. The simplest way to do this is to run the command:

 `# curl -o /etc/unbound/root.hints https://www.internic.net/domain/named.cache` 

It is a good idea to update `root.hints` every six months or so in order to make sure the list of root servers is up to date. This can be done manually or by using [Systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers"). See [#Roothints systemd timer](#Roothints_systemd_timer) for an example.

### Local DNS server

If you want to use *unbound* as your local DNS server, set your nameserver to `127.0.0.1` in your [resolv.conf](/index.php/Resolv.conf "Resolv.conf"). You will want to have your nameserver be [preserved](/index.php/Resolv.conf#Preserve_DNS_settings "Resolv.conf").

**Tip:** A simple way to do this is to install the [openresolv](https://www.archlinux.org/packages/?name=openresolv) package and uncomment the line containing `name_servers=127.0.0.1` in `/etc/resolvconf.conf`. Then run `resolvconf -u` to generate `/etc/resolv.conf`.

See [Resolv.conf#Testing](/index.php/Resolv.conf#Testing "Resolv.conf") on how to test your settings.

Check specifically that the server being used is `127.0.0.1` after making permanent changes to [resolv.conf](/index.php/Resolv.conf "Resolv.conf").

### DNSSEC validation

*unbound* automatically copies the root server trust key anchor file from `/etc/trusted-key.key` to `/etc/unbound/trusted-key.key`. To use DNSSEC validation, point *unbound* to this file by adding the following setting:

```
trust-anchor-file: trusted-key.key

```

Also make sure that if a general [forward](#Forwarding_queries) to a DNS server has been set, then comment them out; otherwise, DNS queries will fail. DNSSEC validation will only be done if the DNS server being queried supports it.

**Note:** Including DNSSEC checking significantly increases DNS lookup times for initial lookups. Once an address is cached locally, then the lookup is virtually instantaneous.

To test if DNSSEC is working, use *drill*:

```
$ drill sigfail.verteiltesysteme.net
$ drill sigok.verteiltesysteme.net

```

The first command should give an `rcode` of `SERVFAIL`. The second should give an `rcode` of `NOERROR`.

### Forwarding queries

**Tip:** Unbound can be used with [DNSCrypt](/index.php/DNSCrypt "DNSCrypt") by setting up forwarding. See [DNSCrypt#Example: configuration for Unbound](/index.php/DNSCrypt#Example:_configuration_for_Unbound "DNSCrypt").

If you have a local network which you wish to have DNS queries for and there is a local DNS server that you would like to forward queries to then you should include this line:

```
private-address: *local_subnet/subnet_mask*

```

For example:

```
private-address: 10.0.0.0/24

```

**Note:** You can use private-address to protect against DNS Rebind attacks. Therefore you may enable RFC1918 networks (10.0.0.0/8 172.16.0.0/12 192.168.0.0/16 169.254.0.0/16 fd00::/8 fe80::/10). Unbound may enable this feature by default in future releases.

To include a local DNS server for both forward and reverse local addresses a set of lines similar to these below is necessary with a forward and reverse lookup (choose the IP address of the server providing DNS for the local network accordingly by changing 10.0.0.1 in the lines below):

```
local-zone: "10.in-addr.arpa." transparent

```

This line above is important to get the reverse lookup to work correctly.

```
forward-zone:
name: "mynetwork.com."
forward-addr: 10.0.0.1

```

```
forward-zone:
name: "10.in-addr.arpa."
forward-addr: 10.0.0.1

```

**Note:** There is a difference between forward zones and stub zones - stub zones will only work when connected to an authoritative DNS server directly. This would work for lookups from a [BIND](/index.php/BIND "BIND") DNS server if it is providing authoritative DNS - but if you are referring queries to an *unbound* server in which internal lookups are forwarded on to another DNS server, then defining the referral as a stub zone in the machine here will not work. In that case it is necessary to define a forward zone as above, since forward zones can have daisy chain lookups onward to other DNS servers. i.e. forward zones can refer queries to recursive DNS servers. This distinction is important as you do not get any error messages indicating what the problem is if you use a stub zone inappropriately.

You can set up the localhost forward and reverse lookups with the following lines:

```
local-zone: "localhost." static
local-data: "localhost. 10800 IN NS localhost."
local-data: "localhost. 10800 IN SOA localhost. nobody.invalid. 1 3600 1200 604800 10800"
local-data: "localhost. 10800 IN A 127.0.0.1"
local-zone: "127.in-addr.arpa." static
local-data: "127.in-addr.arpa. 10800 IN NS localhost."
local-data: "127.in-addr.arpa. 10800 IN SOA localhost. nobody.invalid. 2 3600 1200 604800 10800"
local-data: "1.0.0.127.in-addr.arpa. 10800 IN PTR localhost."

```

Then to use specific servers for default forward zones that are outside of the local machine and outside of the local network (i.e. all other queries will be forwarded to them, and then cached) add this to the configuration file (and in this example the first two addresses are the fast google DNS servers):

```
forward-zone:
  name: "."
  forward-addr: 8.8.8.8
  forward-addr: 8.8.4.4
  forward-addr: 208.67.222.222
  forward-addr: 208.67.220.220

```

This will make *unbound* use Google and OpenDNS servers as the forward zone for external lookups.

**Note:** OpenDNS strips DNSSEC records from responses. Do not use the above forward zone if you want to enable [#DNSSEC validation](#DNSSEC_validation).

## Usage

### Starting Unbound

[Start/enable](/index.php/Start/enable "Start/enable") the `unbound.service` systemd service.

### Remotely control Unbound

*unbound* ships with the `unbound-control` utility which enables us to remotely administer the unbound server. It is similar to the [pdnsd-ctl](/index.php/Pdnsd#pdnsd-ctl "Pdnsd") command of [pdnsd](https://www.archlinux.org/packages/?name=pdnsd).

#### Setting up unbound-control

Before you can start using it, the following steps need to be performed:

1) Firstly, you need to run the following command

```
# unbound-control-setup

```

which will generate a self-signed certificate and private key for the server, as well as the client. These files will be created in the `/etc/unbound` directory.

2) After that, edit `/etc/unbound/unbound.conf` and put the following contents in that. The `control-enable: yes` option is necessary, the rest can be adjusted as required.

```
remote-control:
    # Enable remote control with unbound-control(8) here.
    # set up the keys and certificates with unbound-control-setup.
    control-enable: yes

    # what interfaces are listened to for remote control.
    # give 0.0.0.0 and ::0 to listen to all interfaces.
    control-interface: 127.0.0.1

    # port number for remote control operations.
    control-port: 8953

    # unbound server key file.
    server-key-file: "/etc/unbound/unbound_server.key"

    # unbound server certificate file.
    server-cert-file: "/etc/unbound/unbound_server.pem"

    # unbound-control key file.
    control-key-file: "/etc/unbound/unbound_control.key"

    # unbound-control certificate file.
    control-cert-file: "/etc/unbound/unbound_control.pem"

```

#### Using unbound-control

Some of the commands that can be used with *unbound-control* are:

*   print statistics without resetting them

```
 # unbound-control stats_noreset

```

*   dump cache to stdout

```
 # unbound-control dump_cache

```

*   flush cache and reload configuration

```
 # unbound-control reload

```

Please refer to `man 8 unbound-control` for a detailed look at the operations it supports.

## Tips and tricks

### Block advertising

You can use the following file and simply include it in your unbound configuration: [adservers](https://pgl.yoyo.org/adservers/serverlist.php?hostformat=unbound&showintro=0&startdate%5Bday%5D=&startdate%5Bmonth%5D=&startdate%5Byear%5D=&mimetype=plaintext)

 `/etc/unbound/unbound.conf` 
```
...
include: /etc/unbound/adservers

```

**Note:** In order to return some OK statuses on those hosts, you can change the 127.0.0.1 redirection to a server you control and have that server respond with empty 204 replies, see [this page](http://www.shadowandy.net/2014/04/adblocking-nginx-serving-1-pixel-gif-204-content.htm)

### Adding an authoritative DNS server

For users who wish to run both a validating, recursive, caching DNS server as well as an authoritative DNS server on a single machine then it may be useful to refer to the wiki page [nsd](/index.php/Nsd "Nsd") which gives an example of a configuration for such a system. Having one server for authoritative DNS queries and a separate DNS server for the validating, recursive, caching DNS functions gives increased security over a single DNS server providing all of these functions. Many users have used bind as a single DNS server, and some help on migration from bind to the combination of running nsd and bind is provided in the [nsd](/index.php/Nsd "Nsd") wiki page.

### WAN facing DNS

It is also possible to change the configuration files and interfaces on which the server is listening so that DNS queries from machines outside of the local network can access specific machines within the LAN. This is useful for web and mail servers which are accessible from anywhere, and the same techniques can be employed as has been achieved using bind for many years, in combination with suitable port forwarding on firewall machines to forward incoming requests to the right machine.

### Roothints systemd timer

Here is an example systemd service and timer that update `root.hints` monthly using the method in [#Root hints](#Root_hints):

 `/etc/systemd/system/roothints.service` 
```
[Unit]
Description=Update root hints for unbound
After=network.target

[Service]
ExecStart=/usr/bin/curl -o /etc/unbound/root.hints https://www.internic.net/domain/named.cache
```
 `/etc/systemd/system/roothints.timer` 
```
[Unit]
Description=Run root.hints monthly

[Timer]
OnCalendar=monthly
Persistent=true     

[Install]
WantedBy=timers.target
```

[Start/enable](/index.php/Start/enable "Start/enable") the `roothints.timer` systemd timer.

### Sandboxing

It is possible to sandbox the default `unbound.service` by restricting [capabilities](/index.php/Capabilities "Capabilities") and enforcing [Systemd#Sandboxing application environments](/index.php/Systemd#Sandboxing_application_environments "Systemd") features:

*   `CapabilityBoundingSet` defines a whitelisted set of allowed capabilities
    *   `CAP_IPC_LOCK` = Prevents paging by allowing *unbound* to lock data in memory
        *   Not a hard requirement for *unbound* but rather a personal security choice
    *   `CAP_NET_BIND_SERVICE` = Allows for socket binding to privileged ports < 1024
    *   `CAP_SETGID CAP_SETUID` = Modifies the *user* *group* to *nobody* *nobody*
    *   `CAP_SYS_CHROOT` = Allows the creation of a chroot at `/etc/unbound`
*   `ReadWritePaths` specifies paths to override from `ProtectSystem=strict`
    *   `/etc/unbound` = Allows the *ExecStartPre* command to complete
    *   `/run` = Allows access to the PID file at `/run/unbound.pid`

[Edit](/index.php/Systemd#Drop-in_files "Systemd") `unbound.service` and add the following contents (cf. [FS#52700](https://bugs.archlinux.org/task/52700)):
```
[Unit]
CapabilityBoundingSet=CAP_IPC_LOCK CAP_NET_BIND_SERVICE CAP_SETGID CAP_SETUID CAP_SYS_CHROOT
MemoryDenyWriteExecute=true
NoNewPrivileges=true
PrivateDevices=true
PrivateTmp=true
ProtectHome=true
ProtectControlGroups=true
ProtectKernelModules=true
ProtectKernelTunables=true
ProtectSystem=strict
ReadWritePaths=/etc/unbound /run
RestrictAddressFamilies=AF_INET AF_UNIX
RestrictRealtime=true
SystemCallArchitectures=native
SystemCallFilter=~@clock @cpu-emulation @debug @keyring @module mount @obsolete @resources

```

*   The *@mount* system call set includes *chroot()* which is required by unbound to build its environment
*   `mount` and `unmount2` require explicit listing if they are to be blacklisted apart from the *@mount* macro
*   The above example blacklists `CAP_SYS_ADM` which should be one of the [goals of a secure sandbox](https://lwn.net/Articles/486306/)

## Troubleshooting

### Issues concerning num-threads

The man page for `unbound.conf` mentions:

```
     outgoing-range: <number>
             Number of ports to open. This number of file  descriptors  can  be  opened  per thread.

```

and some sources suggest that the `num-threads` parameter should be set to the number of cpu cores. The sample `unbound.conf.example` file merely has:

```
       # number of threads to create. 1 disables threading.
       # num-threads: 1

```

However it is not possible to arbitrarily increase `num-threads` above `1` without causing *unbound* to start with warnings in the logs about exceeding the number of file descriptors. In reality for most users running on small networks or on a single machine it should be unnecessary to seek performance enhancement by increasing `num-threads` above `1`. If you do wish to do so then refer to [official documentation](http://www.unbound.net/documentation/howto_optimise.html) and the following rule of thumb should work:

	*Set `num-threads` equal to the number of CPU cores on the system. E.g. for 4 CPUs with 2 cores each, use 8.*

Set the `outgoing-range` to as large a value as possible, see the sections in the referred web page above on how to overcome the limit of `1024` in total. This services more clients at a time. With 1 core, try `950`. With 2 cores, try `450`. With 4 cores try `200`. The `num-queries-per-thread` is best set at half the number of the `outgoing-range`.

Because of the limit on `outgoing-range` thus also limits `num-queries-per-thread`, it is better to compile with [libevent](https://www.archlinux.org/packages/?name=libevent), so that there is no `1024` limit on `outgoing-range`. If you need to compile this way for a heavy duty DNS server then you will need to compile the programme from source instead of using the [unbound](https://www.archlinux.org/packages/?name=unbound) package.

## See also

*   [Fedora change to Unbound](https://fedoraproject.org/wiki/Changes/Default_Local_DNS_Resolver)
*   [Block hosts that contain advertisements](https://github.com/jodrell/unbound-block-hosts/)