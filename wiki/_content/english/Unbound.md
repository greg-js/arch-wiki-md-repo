[Unbound](https://unbound.net/) is a validating, recursive, and caching DNS resolver.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Access control](#Access_control)
    *   [2.2 Root hints](#Root_hints)
    *   [2.3 Set /etc/resolv.conf to use the local DNS server](#Set_.2Fetc.2Fresolv.conf_to_use_the_local_DNS_server)
    *   [2.4 Logging](#Logging)
    *   [2.5 DNSSEC validation](#DNSSEC_validation)
    *   [2.6 Forwarding queries](#Forwarding_queries)
*   [3 Usage](#Usage)
    *   [3.1 Starting Unbound](#Starting_Unbound)
    *   [3.2 Remotely control Unbound](#Remotely_control_Unbound)
        *   [3.2.1 Setting up unbound-control](#Setting_up_unbound-control)
        *   [3.2.2 Using unbound-control](#Using_unbound-control)
*   [4 Adding an authoritative DNS server](#Adding_an_authoritative_DNS_server)
*   [5 WAN facing DNS](#WAN_facing_DNS)
*   [6 Issues concerning num-threads](#Issues_concerning_num-threads)
*   [7 Block advertising](#Block_advertising)
    *   [7.1 See also](#See_also)

## Installation

Install the [unbound](https://www.archlinux.org/packages/?name=unbound) package from [official repositories](/index.php/Official_repositories "Official repositories").

Additionally, [expat](https://www.archlinux.org/packages/?name=expat) is required for [DNSSEC](/index.php/DNSSEC "DNSSEC") validation.

## Configuration

_unbound_ is easy to configure. There is a sample config file `/etc/unbound/unbound.conf.example`, which can be copied to `/etc/unbound/unbound.conf` and with the adjustments to the file for your own needs it is enough to run on both IPv4 and IPv6 without access restrictions.

### Access control

You can specify the interfaces to answer queries from by IP address. To listen on _localhost_, use:

```
interface: 127.0.0.1

```

To listen on all interfaces, use:

```
interface: 0.0.0.0

```

Access can be further configured via the `access-control` option:

```
access-control: _subnet_ _action_

```

For example:

```
access-control: 192.168.1.0/24 allow

```

_action_ can be one of `deny` (drop message), `refuse` (polite error reply), `allow` (recursive ok), or `allow_snoop` (recursive and nonrecursive ok). By default everything is refused except for localhost.

### Root hints

For querying a host that is not cached as an address the resolver needs to start at the top of the server tree and query the root servers to know where to go for the top level domain for the address being queried. Therefore it is necessary to put a _root hints_ file into the _unbound_ config directory. The simplest way to do this is to run the command:

 `# curl -o /etc/unbound/root.hints https://www.internic.net/domain/named.cache` 

It is a good idea to run this every six months or so in order to make sure the list of root servers is up to date. This can be done manually or by setting up a [cron](/index.php/Cron "Cron") job for the task.

Point _unbound_ to the `root.hints` file:

```
root-hints: "/etc/unbound/root.hints"

```

### Set /etc/resolv.conf to use the local DNS server

Edit `/etc/resolv.conf` (See also [resolv.conf](/index.php/Resolv.conf "Resolv.conf")):

```
nameserver 127.0.0.1

```

Also if you want to be able to use the hostname of local machine names without the fully qualified domain names, then add a line with the local domain such as:

```
domain localdomain.com
nameserver 127.0.0.1

```

That way you can refer to local hosts such as mainmachine1.localdomain.com as simply mainmachine1 when using the ssh command, but the drill command below still requires the fully qualified domain names in order to perform lookups.

Testing the server before making it default can be done using the drill command from the [ldns](https://www.archlinux.org/packages/?name=ldns) package with examples from internal and external forward and reverse addresses:

```
$ drill @127.0.0.1 www.cnn.com
$ drill @127.0.0.1 localmachine.localdomain.com
$ drill @127.0.0.1 -x w.x.y.z 

```

where `w.x.y.z` can be a local or external IP address and the `-x` option requests a reverse lookup. Once all is working, and you have `/etc/resolv.conf` set to use `127.0.0.1` as the nameserver then you no longer need the `@127.0.0.1` in the _drill_ command, and you can test again that it uses the default DNS server - check that the server used as listed at the bottom of the output from each of these commands shows it is `127.0.0.1` being queried.

### Logging

If you will want logging for _unbound_, then create a log file which can also be in the same directory, but you can choose any location. One way is then to do as root:

```
# touch /etc/unbound/unbound.log
# chown unbound:unbound /etc/unbound/unbound.log

```

Then you can include the logging parameter when you set up the main `unbound.conf` file as below.

### DNSSEC validation

You will need the root server trust key anchor file. It is provided by the [dnssec-anchors](https://www.archlinux.org/packages/?name=dnssec-anchors) package (already installed as a dependency), however, _unbound_ needs read and write access to the file. The `unbound.service` service accomplishes this by copying the `/etc/trusted-key.key` file to `/etc/unbound/trusted-key.key`. You just need to point _unbound_ to this file:

 `/etc/unbound/unbound.conf` 

```
server:
  ...
  trust-anchor-file: trusted-key.key
  ...

```

Also make sure that if a general [forward](#Forwarding_queries) to the Google servers had been in place, then comment them out otherwise DNS queries will fail. DNSSEC validation will be done if the DNS server being queried supports it.

**Note:** Including DNSSEC checking significantly increases DNS lookup times for initial lookups. Once an address is cached locally, then the lookup is virtually instantaneous.

You can now test if DNSSEC is working, using _drill_ in [ldns](https://www.archlinux.org/packages/?name=ldns) (installed as dependency):

```
drill sigfail.verteiltesysteme.net # should return rcode: SERVFAIL
drill sigok.verteiltesysteme.net   # should return rcode: NOERROR

```

### Forwarding queries

If you have a local network which you wish to have DNS queries for and there is a local DNS server that you would like to forward queries to then you should include this line:

```
private-address: _local_subnet/subnet_mask_

```

for example:

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
forward-addr: 10.0.0.1        # Home DNS

```

```
forward-zone:
name: "10.in-addr.arpa."
forward-addr: 10.0.0.1

```

**Note:** There is a difference between forward zones and stub zones - stub zones will only work when connected to an authoritative DNS server directly. This would work for lookups from a [BIND](/index.php/BIND "BIND") DNS server if it is providing authoritative DNS - but if you are referring queries to an _unbound_ server in which internal lookups are forwarded on to another DNS server, then defining the referral as a stub zone in the machine here will not work. In that case it is necessary to define a forward zone as above, since forward zones can have daisy chain lookups onward to other DNS servers. i.e. forward zones can refer queries to recursive DNS servers. This distinction is important as you do not get any error messages indicating what the problem is if you use a stub zone inappropriately.

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

This will make _unbound_ use Google and OpenDNS servers as the forward zone for external lookups.

**Note:** OpenDNS strips DNSSEC records from responses. Do not use the above forward zone if you want to enable [#DNSSEC validation](#DNSSEC_validation).

## Usage

### Starting Unbound

The _unbound_ package provides `unbound.service`, just [start](/index.php/Start "Start") it. You may want to _enable_ it so that it starts at boot.

### Remotely control Unbound

_unbound_ ships with the `unbound-control` utility which enables us to remotely administer the unbound server. It is similar to the [pdnsd-ctl](/index.php/Pdnsd#pdnsd-ctl "Pdnsd") command of [pdnsd](https://www.archlinux.org/packages/?name=pdnsd).

#### Setting up unbound-control

Before you can start using it, the following steps need to be performed:

1) Firstly, you need to run the following command

```
# unbound-control-setup

```

which will generate a self-signed certificate and private key for the server, as well as the client. These files will be created in the `/etc/unbound` directory.

2) After that, edit `/etc/unbound/unbound.conf` and put the following contents in that. The **control-enable: yes** option is necessary, the rest can be adjusted as required.

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

Some of the commands that can be used with _unbound-control_ are:

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

## Adding an authoritative DNS server

For users who wish to run both a validating, recursive, caching DNS server as well as an authoritative DNS server on a single machine then it may be useful to refer to the wiki page [nsd](/index.php/Nsd "Nsd") which gives an example of a configuration for such a system. Having one server for authoritative DNS queries and a separate DNS server for the validating, recursive, caching DNS functions gives increased security over a single DNS server providing all of these functions. Many users have used bind as a single DNS server, and some help on migration from bind to the combination of running nsd and bind is provided in the [nsd](/index.php/Nsd "Nsd") wiki page.

## WAN facing DNS

It is also possible to change the configuration files and interfaces on which the server is listening so that DNS queries from machines outside of the local network can access specific machines within the LAN. This is useful for web and mail servers which are accessible from anywhere, and the same techniques can be employed as has been achieved using bind for many years, in combination with suitable port forwarding on firewall machines to forward incoming requests to the right machine.

## Issues concerning num-threads

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

However it is not possible to arbitrarily increase `num-threads` above `1` without causing _unbound_ to start with warnings in the logs about exceeding the number of file descriptors. In reality for most users running on small networks or on a single machine it should be unnecessary to seek performance enhancement by increasing `num-threads` above `1`. If you do wish to do so then refer to [official documentation](http://www.unbound.net/documentation/howto_optimise.html) and the following rule of thumb should work:

	_Set `num-threads` equal to the number of CPU cores on the system. E.g. for 4 CPUs with 2 cores each, use 8._

Set the `outgoing-range` to as large a value as possible, see the sections in the referred web page above on how to overcome the limit of `1024` in total. This services more clients at a time. With 1 core, try `950`. With 2 cores, try `450`. With 4 cores try `200`. The `num-queries-per-thread` is best set at half the number of the `outgoing-range`.

Because of the limit on `outgoing-range` thus also limits `num-queries-per-thread`, it is better to compile with [libevent](https://www.archlinux.org/packages/?name=libevent), so that there is no `1024` limit on `outgoing-range`. If you need to compile this way for a heavy duty DNS server then you will need to compile the programme from source instead of using the [unbound](https://www.archlinux.org/packages/?name=unbound) package.

## Block advertising

You can use the following file and simply include it in your unbound configuration: [adservers](https://pgl.yoyo.org/adservers/serverlist.php?hostformat=unbound&showintro=0&startdate%5Bday%5D=&startdate%5Bmonth%5D=&startdate%5Byear%5D=&mimetype=plaintext)

 `/etc/unbound/unbound.conf` 

```
...
include: /etc/unbound/adservers

```

**Note:** In order to return some OK statuses on those hosts, you can change the 127.0.0.1 redirection to a server you control and have that server respond with empty 204 replies, see [this page](http://www.shadowandy.net/2014/04/adblocking-nginx-serving-1-pixel-gif-204-content.htm)

### See also

*   [Block hosts that contain advertisements](https://github.com/jodrell/unbound-block-hosts/)