[FireHOL](http://firehol.org) is a language (and a program to run it) to build secure, stateful firewalls from easy to understand, human-readable configuration files. The configuration stays readable even for very complex setups. In the background it interfaces with [iptables](/index.php/Iptables "Iptables") (IPv4/IPv6).

## Installation

[Install](/index.php/Install "Install") [firehol](https://aur.archlinux.org/packages/firehol/) or [firehol-git](https://aur.archlinux.org/packages/firehol-git/).

## Configuration

The configuration file is `/etc/firehol/firehol.conf`.

A good way to start learning its scripting declarations is by copying an [Firehol example configuration](http://firehol.org/#firehol).

The configuration file is bash file and has 3 parts:

*   helper
*   interface
*   router

## Try, Run and Enable

You can test the configuration file's correctness by issuing:

```
# firehol try

```

or

```
# firehol nofast try

```

If the configuration is working, [start/enable](/index.php/Start/enable "Start/enable") the `firehol.service`.

**Tip:**

*   The package also includes [FireQOS](http://firehol.org/#fireqos), a helper for [Advanced traffic control](/index.php/Advanced_traffic_control "Advanced traffic control"). It is packaged with its own `fireqos.service`.
*   The [netdata](https://www.archlinux.org/packages/?name=netdata) (or [netdata-git](https://aur.archlinux.org/packages/netdata-git/)) application for traffic monitoring, created by the same project authors, also is available. See [Netdata](https://github.com/firehol/netdata) for more information.