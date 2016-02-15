[Cjdns](https://github.com/cjdelisle/cjdns) implements an encrypted IPv6 network using public-key cryptography for address allocation and a distributed hash table for routing. This provides near-zero-configuration networking, and prevents many of the security and scalability issues that plague existing networks.

## Install and configure

Install [cjdns](https://www.archlinux.org/packages/?name=cjdns) from community or [cjdns-git](https://aur.archlinux.org/packages/cjdns-git/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). The package includes a systemd service file, but sysvinit scripts are available too in [cjdns-git-sysvinit](https://aur.archlinux.org/packages/cjdns-git-sysvinit/).

_If you do not already have one_, generate a new `cjdroute.conf` in the `/etc` directory by becoming root and running:

```
# cjdroute --genconf > /etc/cjdroute.conf

```

**Note:** For added security, you should limit access to `/etc/cjdroute.conf` as it contains the private key capable of encrypting and decrypting all your communications; you can do so by becoming root and running:

```
# chmod 600 /etc/cjdroute.conf

```

Become root again and open `/etc/cjdroute.conf`, then add at least one peer to the "connectTo" section (Peers can be anyone else running cjdns who gives you credentials to connect to them with, and can be found in #cjdns and #projectmeshnet on [EFnet](http://www.efnet.org) among many other places).

## Starting

Start and enable the `cjdns` [systemd](/index.php/Systemd "Systemd") service. This will also start the `cjdnsadmin` service.

If _cjdns_ did not start, you should check for errors and edit `/etc/cjdroute.conf` if needed:

```
# systemctl status cjdns
# journalctl -u cjdns

```

## See also

*   [Wikipedia:Cjdns](https://en.wikipedia.org/wiki/Cjdns "wikipedia:Cjdns")