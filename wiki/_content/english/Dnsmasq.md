**dnsmasq** provides services as a DNS cacher and a DHCP server. As a Domain Name Server (DNS) it can cache DNS queries to improve connection speeds to previously visited sites, and as a DHCP server [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) can be used to provide internal IP addresses and routes to computers on a LAN. Either or both of these services can be implemented. dnsmasq is considered to be lightweight and easy to configure; it is designed for personal computer use or for use on a network with less than 50 computers. It also comes with a [PXE](/index.php/PXE "PXE") server.

## Contents

*   [1 Installation](#Installation)
*   [2 DNS Cache Setup](#DNS_Cache_Setup)
    *   [2.1 DNS Addresses File](#DNS_Addresses_File)
        *   [2.1.1 resolv.conf](#resolv.conf)
            *   [2.1.1.1 More than three nameservers](#More_than_three_nameservers)
        *   [2.1.2 dhcpcd](#dhcpcd)
        *   [2.1.3 dhclient](#dhclient)
    *   [2.2 NetworkManager](#NetworkManager)
        *   [2.2.1 Custom Configuration](#Custom_Configuration)
        *   [2.2.2 IPv6](#IPv6)
        *   [2.2.3 Other methods](#Other_methods)
*   [3 DHCP server setup](#DHCP_server_setup)
*   [4 Start the daemon](#Start_the_daemon)
*   [5 Test](#Test)
    *   [5.1 DNS Caching](#DNS_Caching)
    *   [5.2 DHCP Server](#DHCP_Server)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Prevent OpenDNS Redirecting Google Queries](#Prevent_OpenDNS_Redirecting_Google_Queries)
    *   [6.2 View leases](#View_leases)
    *   [6.3 Adding a custom domain](#Adding_a_custom_domain)
    *   [6.4 Override addresses](#Override_addresses)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq).

## DNS Cache Setup

To set up dnsmasq as a DNS caching daemon on a single computer edit `/etc/dnsmasq.conf` and uncomment the `listen-address` directive, adding in the localhost IP address:

```
listen-address=127.0.0.1

```

To use this computer to listen on its LAN IP address for other computers on the network:

```
listen-address=192.168.1.1    # Example IP

```

It is recommended that you use a static LAN IP in this case.

Multiple ip address settings:

```
listen-address=127.0.0.1,192.168.1.1 

```

### DNS Addresses File

After configuring dnsmasq, the DHCP client will need to prepend the localhost address to the known DNS addresses in `/etc/resolv.conf`. This causes all queries to be sent to dnsmasq before trying to resolve them with an external DNS. After the DHCP client is configured, the network will need to be restarted for changes to take effect.

#### resolv.conf

One option is a pure `resolv.conf` configuration. To do this, just make the first nameserver in `/etc/resolv.conf` point to localhost:

 `/etc/resolv.conf` 
```
nameserver 127.0.0.1
# External nameservers
...

```

Now DNS queries will be resolved first with dnsmasq, only checking external servers if dnsmasq cannot resolve the query. [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd), unfortunately, tends to overwrite `/etc/resolv.conf` by default, so if you use DHCP it is a good idea to protect `/etc/resolv.conf`. To do this, append `nohook resolv.conf` to the dhcpcd config file:

 `/etc/dhcpcd.conf` 
```
...
nohook resolv.conf
```

It is also possible to write protect your resolv.conf:

```
# chattr +i /etc/resolv.conf

```

##### More than three nameservers

A limitation in the way Linux handles DNS queries is that there can only be a maximum of three nameservers used in `resolv.conf`. As a workaround, you can make localhost the only nameserver in `resolv.conf`, and then create a separate `resolv-file` for your external nameservers. First, create a new resolv file for dnsmasq:

 `/etc/resolv.dnsmasq.conf` 
```
# Google's nameservers, for example
nameserver 8.8.8.8
nameserver 8.8.4.4

```

And then edit `/etc/dnsmasq.conf` to use your new resolv file:

 `/etc/dnsmasq.conf` 
```
...
resolv-file=/etc/resolv.dnsmasq.conf
...

```

#### dhcpcd

[dhcpcd](/index.php/Dhcpcd "Dhcpcd") has the ability to prepend or append nameservers to `/etc/resolv.conf` by creating (or editing) the `/etc/resolv.conf.head` and `/etc/resolv.conf.tail` files respectively:

```
echo "nameserver 127.0.0.1" > /etc/resolv.conf.head

```

#### dhclient

For [dhclient](https://www.archlinux.org/packages/?name=dhclient), uncomment in `/etc/dhclient.conf`:

```
prepend domain-name-servers 127.0.0.1;

```

### NetworkManager

DNS requests can be sped up by caching previous requests locally for subsequent lookup. [NetworkManager](/index.php/NetworkManager "NetworkManager") has a plugin to enable DNS caching using dnsmasq, but it is not enabled in the default configuration.

Make sure [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) has been installed, but has been disabled. Then, edit `/etc/NetworkManager/NetworkManager.conf` and change the `dns` in the `[main]` section:

 `/etc/NetworkManager/NetworkManager.conf` 
```
[main]
plugins=keyfile
dhcp=dhclient
dns=dnsmasq

```

Now restart NetworkManager or reboot. NetworkManager will automatically start dnsmasq and add 127.0.0.1 to `/etc/resolv.conf`. The actual DNS servers can be found in `/var/run/NetworkManager/dnsmasq.conf`. You can verify dnsmasq is being used by doing the same DNS lookup twice with `$ dig example.com` that can be installed with [bind-tools](https://www.archlinux.org/packages/?name=bind-tools) and verifying the server and query times.

#### Custom Configuration

Custom configurations can be created for *dnsmasq* by creating configuration files in `/etc/NetworkManager/dnsmasq.d/`. For example, to change the size of the DNS cache (which is stored in RAM):

 `/etc/NetworkManager/dnsmasq.d/cache`  `cache-size=1000` 

#### IPv6

Enabling `dnsmasq` in NetworkManager may break IPv6-only DNS lookups (i.e. `dig -6 [hostname]`) which would otherwise work. In order to resolve this, creating the following file will configure *dnsmasq* to also listen to the IPv6 loopback:

 `/etc/NetworkManager/dnsmasq.d/ipv6_listen.conf`  `listen-address=::1` 

In addition, `dnsmasq` also does not prioritize upstream IPv6 DNS. Unfortunately NetworkManager does not do this ([Ubuntu Bug](https://bugs.launchpad.net/ubuntu/+source/network-manager/+bug/936712)). A workaround would be to disable IPv4 DNS in the NetworkManager config, assuming one exists

#### Other methods

Another option is in NetworkManagers' settings (usually by right-clicking the applet) and entering settings manually. Setting up will depending on the type of front-end used; the process usually involves right-clicking on the applet, editing (or creating) a profile, and then choosing DHCP type as 'Automatic (specify addresses).' The DNS addresses will need to be entered and are usually in this form: `127.0.0.1, DNS-server-one, ...`.

## DHCP server setup

By default dnsmasq has the DHCP functionality turned off, if you want to use it you must turn it on in (`/etc/dnsmasq.conf`). Here are the important settings:

```
# Only listen to routers' LAN NIC.  Doing so opens up tcp/udp port 53 to
# localhost and udp port 67 to world:
interface=<LAN-NIC>

# dnsmasq will open tcp/udp port 53 and udp port 67 to world to help with
# dynamic interfaces (assigning dynamic ips). Dnsmasq will discard world
# requests to them, but the paranoid might like to close them and let the 
# kernel handle them:
bind-interfaces

# Dynamic range of IPs to make available to LAN pc
dhcp-range=192.168.111.50,192.168.111.100,12h

# If you’d like to have dnsmasq assign static IPs, bind the LAN computer's
# NIC MAC address:
dhcp-host=aa:bb:cc:dd:ee:ff,192.168.111.50

```

## Start the daemon

To have dnsmasq load upon startup:

 `# systemctl enable dnsmasq` 

To start dnsmasq immediately:

 `# systemctl start dnsmasq` 

To see if dnsmasq started properly, check the system's journal:

 `$ journalctl -u dnsmasq` 

The network will also need to be restarted so the DHCP client can create a new `/etc/resolv.conf`.

## Test

### DNS Caching

To do a lookup speed test choose a website that has not been visited since dnsmasq has been started (*dig* is part of the [bind-tools](https://www.archlinux.org/packages/?name=bind-tools) package):

```
$ dig archlinux.org | grep "Query time"

```

Running the command again will use the cached DNS IP and result in a faster lookup time if dnsmasq is setup correctly:

 `$ dig archlinux.org | grep "Query time"` 
```
;; Query time: 18 msec

```
 `$ dig archlinux.org | grep "Query time"` 
```
;; Query time: 2 msec

```

### DHCP Server

From a computer that is connected to the one with dnsmasq on it, configure it to use DHCP for automatic IP address assignment, then attempt to log into the network normally.

## Tips and tricks

### Prevent OpenDNS Redirecting Google Queries

To prevent OpenDNS from redirecting all Google queries to their own search server, add to `/etc/dnsmasq.conf`:

 `server=/www.google.com/<ISP DNS IP>` 

### View leases

 `$ cat /var/lib/misc/dnsmasq.leases` 

### Adding a custom domain

It is possible to add a custom domain to hosts in your (local) network:

```
local=/home.lan/
domain=home.lan

```

In this example it is possible to ping a host/device (e.g. defined in your hosts file) as `hostname.home.lan`.

Uncomment `expand-hosts` to add the custom domain to hosts entries:

```
expand-hosts

```

Without this setting, you'll have to add the domain to entries of /etc/hosts.

### Override addresses

In some cases, such as when operating a captive portal, it can be useful to resolve specific domains names to a hard-coded set of addresses. This is done with the `address` config:

```
address=/example.com/1.2.3.4

```

Furthermore, it's possible to return a specific address for all domain names that are not answered from `/etc/hosts` or DHCP by using a special wildcard:

```
address=/#/1.2.3.4

```

## See also

*   [Caching Nameserver using dnsmasq, and a few other tips and tricks.](http://www.g-loaded.eu/2010/09/18/caching-nameserver-using-dnsmasq/)