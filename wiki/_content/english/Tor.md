Related articles

*   [GNUnet](/index.php/GNUnet "GNUnet")
*   [I2P](/index.php/I2P "I2P")
*   [Freenet](/index.php/Freenet "Freenet")

[Tor](https://www.torproject.org) is an open source implementation of 2nd generation [onion routing](https://en.wikipedia.org/wiki/Onion_routing "wikipedia:Onion routing") that provides free access to an anonymous proxy network. Its primary goal is to enable [online anonymity](https://en.wikipedia.org/wiki/Internet_anonymity "wikipedia:Internet anonymity") by protecting against [traffic analysis](https://en.wikipedia.org/wiki/Traffic_analysis "wikipedia:Traffic analysis") attacks.

## Contents

*   [1 Introduction](#Introduction)
*   [2 Installation](#Installation)
*   [3 Configuration](#Configuration)
    *   [3.1 Relay Configuration](#Relay_Configuration)
*   [4 Running Tor in a Chroot](#Running_Tor_in_a_Chroot)
*   [5 Running Tor in a systemd-nspawn container with a virtual network interface](#Running_Tor_in_a_systemd-nspawn_container_with_a_virtual_network_interface)
    *   [5.1 Host installation and configuration](#Host_installation_and_configuration)
        *   [5.1.1 Virtual network interface](#Virtual_network_interface)
        *   [5.1.2 Start and enable systemd-nspawn](#Start_and_enable_systemd-nspawn)
    *   [5.2 Container configuration](#Container_configuration)
        *   [5.2.1 Start and enable systemd-networkd](#Start_and_enable_systemd-networkd)
    *   [5.3 Configure Tor](#Configure_Tor)
*   [6 Usage](#Usage)
*   [7 Web browsing](#Web_browsing)
    *   [7.1 Firefox](#Firefox)
    *   [7.2 Chromium](#Chromium)
        *   [7.2.1 Debug](#Debug)
        *   [7.2.2 Extension](#Extension)
    *   [7.3 Luakit](#Luakit)
*   [8 HTTP proxy](#HTTP_proxy)
    *   [8.1 Firefox](#Firefox_2)
    *   [8.2 Polipo](#Polipo)
    *   [8.3 Privoxy](#Privoxy)
*   [9 Instant messaging](#Instant_messaging)
    *   [9.1 Pidgin](#Pidgin)
*   [10 Irssi](#Irssi)
*   [11 Pacman](#Pacman)
*   [12 Running a Tor server](#Running_a_Tor_server)
    *   [12.1 Running a Tor bridge](#Running_a_Tor_bridge)
        *   [12.1.1 Configuration](#Configuration_2)
        *   [12.1.2 Troubleshooting](#Troubleshooting)
    *   [12.2 Running a Tor relay](#Running_a_Tor_relay)
        *   [12.2.1 Configuration](#Configuration_3)
    *   [12.3 Running a Tor exit node](#Running_a_Tor_exit_node)
        *   [12.3.1 Configuration](#Configuration_4)
        *   [12.3.2 +100Mbps Exit Relay configuration example](#.2B100Mbps_Exit_Relay_configuration_example)
            *   [12.3.2.1 Tor](#Tor)
                *   [12.3.2.1.1 Raise maximum number of open file descriptors](#Raise_maximum_number_of_open_file_descriptors)
                *   [12.3.2.1.2 Start tor.service as root to bind Tor to privileged ports](#Start_tor.service_as_root_to_bind_Tor_to_privileged_ports)
                *   [12.3.2.1.3 Tor configuration](#Tor_configuration)
            *   [12.3.2.2 arm](#arm)
            *   [12.3.2.3 iptables](#iptables)
            *   [12.3.2.4 Haveged](#Haveged)
            *   [12.3.2.5 pdnsd](#pdnsd)
                *   [12.3.2.5.1 Uncensored DNS](#Uncensored_DNS)
*   [13 TorDNS](#TorDNS)
    *   [13.1 Using TorDNS for all DNS queries](#Using_TorDNS_for_all_DNS_queries)
*   [14 Torsocks](#Torsocks)
*   [15 Transparent Torification](#Transparent_Torification)
*   [16 Troubleshooting](#Troubleshooting_2)
    *   [16.1 Problem with user value](#Problem_with_user_value)
*   [17 See also](#See_also)

## Introduction

Users of the Tor network run an onion proxy on their machine. This software connects out to Tor, periodically negotiating a virtual circuit through the Tor network. Tor employs cryptography in a layered manner (hence the 'onion' analogy), ensuring perfect forward secrecy between routers. At the same time, the onion proxy software presents a SOCKS interface to its clients. SOCKS-aware applications may be pointed at Tor, which then multiplexes the traffic through a Tor virtual circuit.

**Warning:** Tor by itself is *not* all you need to maintain your anonymity. There are several major pitfalls to watch out for (see: [Want Tor to really work?](https://www.torproject.org/download/download.html#warning)).

Through this process the onion proxy manages networking traffic for end-user anonymity. It keeps a user anonymous by encrypting traffic, sending it through other nodes of the Tor network, and decrypting it at the last node to receive your traffic before forwarding it to the server you specified. One trade off that has to be made for the anonymity Tor provides is that it can be considerably slower than a regular direct connection, due to the large amount of traffic re-routing. Additionally, although Tor provides protection against traffic analysis it cannot prevent traffic confirmation at the boundaries of the Tor network (i.e. the traffic entering and exiting the network).

See [Wikipedia:Tor (anonymity network)](https://en.wikipedia.org/wiki/Tor_(anonymity_network) for more information.

## Installation

[Install](/index.php/Install "Install") the [tor](https://www.archlinux.org/packages/?name=tor) package.

The [arm](https://www.archlinux.org/packages/?name=arm) (Anonymizing Relay Monitor) package provides a terminal status monitor for bandwidth usage, connection details and more.

For a GUI, you can use [vidalia](https://aur.archlinux.org/packages/vidalia/).

**Warning:** Vidalia is discontinued and no longer supported by the Tor Project. Please see [https://blog.torproject.org/blog/plain-vidalia-bundles-be-discontinued-dont-panic](https://blog.torproject.org/blog/plain-vidalia-bundles-be-discontinued-dont-panic)

## Configuration

By default Tor reads configurations from the file `/etc/tor/torrc`. The configuration options are explained in [tor(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/tor.1) and the [Tor website](https://torproject.org/docs/tor-manual.html.en). The default configuration should work fine for most Tor users.

There are potential conflicts between configurations in `torrc` and those in `tor.service`.

*   In `torrc`, `RunAsDaemon` should, as by default, be set to `0`, since `Type=simple` is set in the `[Service]` section in `tor.service`.
*   In `torrc`, `User` should not be set unless `User=` is set to `root` in the `[Service]` section in `tor.service`.

### Relay Configuration

The maximum file descriptor number that can be opened by Tor can be set with `LimitNOFILE` in `tor.service`. Fast relays may want to increase this value.

If your computer is not running a webserver, and you have not set `AccountingMax`, consider changing your `ORPort` to `443` and/or your `DirPort` to `80`. Many Tor users are stuck behind firewalls that only let them browse the web, and this change will let them reach your Tor relay. If you are already using ports `80` and `443`, other useful ports are `22`, `110`, and `143`.[[1]](https://www.torproject.org/docs/tor-relay-debian) But since these are privileged ports, to do so Tor must be run as root, by setting `User=root` in `tor.service` and `User tor` in `torrc`.

You may wish to review [Lifecycle of a New Relay](https://blog.torproject.org/blog/lifecycle-of-a-new-relay) Tor documentation.

## Running Tor in a Chroot

**Warning:** Connecting with telnet to the local ControlPort seems to be broken while running Tor in a chroot

For security purposes, it may be desirable to run Tor in a [chroot](/index.php/Chroot "Chroot"). The following script will create an appropriate chroot in `/opt/torchroot`:

 `~/torchroot-setup.sh` 
```
#!/bin/bash
export TORCHROOT=/opt/torchroot

mkdir -p $TORCHROOT
mkdir -p $TORCHROOT/etc/tor
mkdir -p $TORCHROOT/dev
mkdir -p $TORCHROOT/usr/bin
mkdir -p $TORCHROOT/usr/lib
mkdir -p $TORCHROOT/usr/share/tor
mkdir -p $TORCHROOT/var/lib

ln -s /usr/lib  $TORCHROOT/lib
cp /etc/hosts           $TORCHROOT/etc/
cp /etc/host.conf       $TORCHROOT/etc/
cp /etc/localtime       $TORCHROOT/etc/
cp /etc/nsswitch.conf   $TORCHROOT/etc/
cp /etc/resolv.conf     $TORCHROOT/etc/
cp /etc/tor/torrc       $TORCHROOT/etc/tor/

cp /usr/bin/tor         $TORCHROOT/usr/bin/
cp /usr/share/tor/geoip* $TORCHROOT/usr/share/tor/
cp /lib/libnss* /lib/libnsl* /lib/ld-linux-*.so* /lib/libresolv* /lib/libgcc_s.so* $TORCHROOT/usr/lib/
cp $(ldd /usr/bin/tor | awk '{print $3}'|grep --color=never "^/") $TORCHROOT/usr/lib/
cp -r /var/lib/tor      $TORCHROOT/var/lib/
chown -R tor:tor $TORCHROOT/var/lib/tor

sh -c "grep --color=never ^tor /etc/passwd > $TORCHROOT/etc/passwd"
sh -c "grep --color=never ^tor /etc/group > $TORCHROOT/etc/group"

mknod -m 644 $TORCHROOT/dev/random c 1 8
mknod -m 644 $TORCHROOT/dev/urandom c 1 9
mknod -m 666 $TORCHROOT/dev/null c 1 3

if [[ "$(uname -m)" == "x86_64" ]]; then
  cp /usr/lib/ld-linux-x86-64.so* $TORCHROOT/usr/lib/.
  ln -sr /usr/lib64 $TORCHROOT/lib64
  ln -s $TORCHROOT/usr/lib ${TORCHROOT}/usr/lib64
fi

```

After running the script as root, Tor can be launched in the [chroot](/index.php/Chroot "Chroot") with the command:

```
# chroot --userspec=tor:tor /opt/torchroot /usr/bin/tor

```

or if you use systemd overload the service:

 `/etc/systemd/system/tor.service.d/chroot.conf` 
```
[Service]
User=root
ExecStart=
ExecStart=/usr/bin/sh -c "chroot --userspec=tor:tor /opt/torchroot /usr/bin/tor -f /etc/tor/torrc"
KillSignal=SIGINT

```

## Running Tor in a systemd-nspawn container with a virtual network interface

In this example we will create a [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") container named `tor-exit` with a virtual macvlan network interface.

See [Systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") and [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") for full documentation.

### Host installation and configuration

In this example the container will reside in `/srv/container`:

```
# mkdir /srv/container/tor-exit

```

[Install](/index.php/Install "Install") the [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts).

Install [base](https://www.archlinux.org/groups/x86_64/base/), [tor](https://www.archlinux.org/packages/?name=tor) and [arm](https://www.archlinux.org/packages/?name=arm) and deselect [linux](https://www.archlinux.org/packages/?name=linux) as per [Systemd-nspawn#Create and boot a minimal Arch Linux distribution in a container](/index.php/Systemd-nspawn#Create_and_boot_a_minimal_Arch_Linux_distribution_in_a_container "Systemd-nspawn"):

```
# pacstrap -i -c -d /srv/container/tor-exit base tor arm

```

Create directory if it does not exist:

```
# mkdir /var/lib/container

```

**Note:** Symlinks for `nspawn` are currently broken (as of 2016-02-04; see [https://github.com/systemd/systemd/issues/2001](https://github.com/systemd/systemd/issues/2001)), and will give you a "too many levels of symlinks" error. As a (possibly insecure) workaround, simply pacstrap your install to the container directory instead.

Symlink to register the container on the host, as per [Systemd-nspawn#Enable container on boot](/index.php/Systemd-nspawn#Enable_container_on_boot "Systemd-nspawn"):

```
# ln -s /srv/container/tor-exit /var/lib/container/tor-exit

```

#### Virtual network interface

Create a Dropin directory for the container service:

```
# mkdir /etc/systemd/system/systemd-nspawn@tor-exit.service.d

```
 `/etc/systemd/system/systemd-nspawn@tor-exit.service.d/tor-exit.conf` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/systemd-nspawn --quiet --keep-unit --boot --link-journal=guest --network-macvlan=$INTERFACE --private-network --directory=/var/lib/container/%i
LimitNOFILE=32768

```

`--network-macvlan=$INTERFACE --private-network` automagically creates a macvlan named `mv-$INTERFACE` inside the container, which is not visible from the host. `--private-network` is implied by `--network-macvlan=` according to [systemd-nspawn(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-nspawn.1). This is advisable for security as it will allow you to give a private IP to the container, and it won't know what your machine's IP is. This can help obscure DNS requests.

`LimitNOFILE=32768` per [#Raise maximum number of open file descriptors](#Raise_maximum_number_of_open_file_descriptors).

Setup [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") according to your network in `/srv/container/tor-exit/etc/systemd/network/mv-$INTERFACE.network`.

#### Start and enable systemd-nspawn

[Start](/index.php/Start "Start") and enable `systemd-nspawn@tor-exit.service`.

### Container configuration

`# machinectl login tor-exit` login to the container, see [Systemd-nspawn#machinectl](/index.php/Systemd-nspawn#machinectl "Systemd-nspawn").

`# mv /srv/container/tor-exit/etc/securetty /srv/container/tor-exit/etc/securetty.bak` if you get the error described in [Systemd-nspawn#Troubleshooting](/index.php/Systemd-nspawn#Troubleshooting "Systemd-nspawn").

#### Start and enable systemd-networkd

[Start](/index.php/Start "Start") and enable `systemd-networkd.service`. `networkctl` displays if `systemd-networkd` is correctly configured.

### Configure Tor

See [#Running a Tor server](#Running_a_Tor_server).

**Tip:** It is easier to edit files in the container from the host with your normal editor.

## Usage

Start/enable `tor.service` [using systemd](/index.php/Systemd#Using_units "Systemd"). Alternatively, launch it with `sudo -u tor /usr/bin/tor`.

To use a program over tor, configure it to use `127.0.0.1` or localhost as a SOCKS5 proxy, with port `9050` (plain tor with standard settings). To check if Tor is functioning properly visit the [Tor](https://check.torproject.org/), [Harvard](http://serifos.eecs.harvard.edu/cgi-bin/ipaddr.pl?tor=1) or [Xenobite.eu](https://torcheck.xenobite.eu/) websites.

## Web browsing

The Tor Project currently only supports web browsing with tor through the [Tor Browser Bundle](https://aur.archlinux.org/packages/?K=tor-browser), which can be downloaded from the AUR. It is built with a patched version of the Firefox extended support releases. Tor can also be used with regular [Firefox](/index.php/Firefox "Firefox"), [Chromium](/index.php/Chromium "Chromium") and other browsers, but this is [not recommended](https://www.torproject.org/docs/faq.html.en#TBBOtherBrowser) by the Tor Project.

**Tip:** For makepkg to verify the signature on the AUR source tarball download for TBB, import the [signing keys from the Tor Project](https://www.torproject.org/docs/signing-keys.html.en) (currently 2E1AC68ED40814E0) as explained in [GnuPG#Import a public key](/index.php/GnuPG#Import_a_public_key "GnuPG").

### Firefox

In *Preferences > Advanced > Network tab > Settings* manually set Firefox to use the SOCKS proxy `localhost` with port `9050`. Then you must type `about:config` into the address bar and "void your warranty". Change `network.proxy.socks_remote_dns` to `true` and restart the browser. This channels all DNS requests through TOR's socks proxy.

### Chromium

You can simply run:

```
$ chromium --proxy-server="socks5://myproxy:8080" --host-resolver-rules="MAP * ~NOTFOUND , EXCLUDE myproxy"

```

The `--proxy-server="socks5://myproxy:8080"` flag tells Chrome to send all `http://` and `https://` URL requests through the SOCKS proxy server `"myproxy:8080"`, using version 5 of the SOCKS protocol. The hostname for these URLs will be resolved by the proxy server, and not locally by Chrome.

**Warning:** Proxying of `ftp://` URLs through a SOCKS proxy is not yet implemented[[2]](https://www.chromium.org/developers/design-documents/network-stack/socks-proxy).

The `--proxy-server` flag applies to URL loads only. There are other components of Chrome which may issue DNS resolves directly and hence bypass this proxy server. The most notable such component is the "DNS prefetcher". Hence if DNS prefetching is not disabled in Chrome then you will still see local DNS requests being issued by Chrome despite having specified a SOCKS v5 proxy server. Disabling DNS prefetching would solve this problem, however it is a fragile solution since once needs to be aware of all the areas in Chrome which issue raw DNS requests. To address this, the next flag, `--host-resolver-rules="MAP * ~NOTFOUND , EXCLUDE myproxy"`, is a catch-all to prevent Chrome from sending any DNS requests over the network. It says that all DNS resolves are to be simply mapped to the (invalid) address `~NOTFOUND` (think of it as `0.0.0.0`). The `"EXCLUDE"` clause make an exception for `"myproxy"`, because otherwise Chrome would be unable to resolve the address of the SOCKS proxy server itself, and all requests would necessarily fail with `PROXY_CONNECTION_FAILED`.

#### Debug

The first thing to check when debugging is look at the Proxy tab on about:net-internals, and verify what the effective proxy settings are: `chrome://net-internals/#proxy`

Next, take a look at the DNS tab of `about:net-internals` to make sure Chrome isn't issuing local DNS resolves: `chrome://net-internals/#dns`

#### Extension

Just as with Firefox, you can setup a fast switch for example through [Proxy SwitchySharp](https://chrome.google.com/webstore/detail/dpplabbmogkhghncfbfdeeokoefdjegm).

Once installed enter in its configuration page. Under the tab *Proxy Profiles* add a new profile *Tor*, if ticked untick the option *Use the same proxy server for all protocols*, then add *localhost* as SOCKS Host, *9050* to the respective port and select *SOCKS v5*.

Optionally you can enable the quick switch under the *General* tab to be able to switch beetween normal navigation and Tor network just by left-clicking on the Proxy SwitchySharp's icon.

### Luakit

**Warning:** It will not be hard for an observer to identify you by the rare user-agent string, and there may be further issues with Flash, JavaScript or similar.

You can simply run:

```
$ torsocks luakit

```

## HTTP proxy

Tor can be used with an HTTP proxy like [Polipo](/index.php/Polipo "Polipo") or [Privoxy](/index.php/Privoxy "Privoxy"), however the Tor dev team recommends using the SOCKS5 library since browsers directly support it.

### Firefox

The [FoxyProxy](https://addons.mozilla.org/en-us/firefox/addon/foxyproxy-standard/) add-on allows you to specify multiple proxies for different URLs or for all your browsing. After restarting Firefox manually set Firefox to port `8118` on `localhost`, which is where [Polipo](/index.php/Polipo "Polipo") or [Privoxy](/index.php/Privoxy "Privoxy") are running. These settings can be access under *Add > Standard proxy type*. Select a proxy label (e.g Tor) and enter the port and host into the *HTTP Proxy* and *SSL Proxy* fields. To check if Tor is functioning properly visit the [Tor Check](https://check.torproject.org/) website and toggle Tor.

### Polipo

The Tor Project has created a custom [Polipo configuration file](https://gitweb.torproject.org/torbrowser.git/plain/build-scripts/config/polipo.conf?id=1ffcd9dafb9dd76c3a29dd686e05a71a95599fb5) to prevent potential problems with Polipo as well to provide better anonymity.

Keep in mind that Polipo is not required if you can use a SOCKS 5 proxy, which Tor starts automatically on port 9050\. If you want to use [Chromium](/index.php/Chromium "Chromium") with Tor, you do not need the Polipo package (see: [#Chromium](#Chromium)).

### Privoxy

You can also use this setup in other applications like messaging (e.g. Jabber, IRC). Applications that support HTTP proxies you can connect to Privoxy (i.e. `127.0.0.1:8118`). To use SOCKS proxy directly, you can point your application at Tor (i.e. `127.0.0.1:9050`). A problem with this method though is that applications doing DNS resolves by themselves may leak information. Consider using Socks4A (e.g. with Privoxy) instead.

## Instant messaging

In order to use an IM client with tor, we do not need an http proxy like [polipo](/index.php/Polipo "Polipo")/[privoxy](/index.php/Privoxy "Privoxy"). We will be using tor's daemon directly which listens to port 9050 by default.

### Pidgin

You can set up Pidgin to use Tor globally, or per account. To use Tor globally, go to Tools -> Preferences -> Proxy. To use Tor for specific accounts, go to *Accounts > Manage Accounts*, select the desired account, click Modify, then go to the Proxy tab. The proxy settings are as follows:

```
Proxy type SOCKS5
Host 127.0.0.1
Port 9150

```

Note that [some time in 2013](https://trac.torproject.org/projects/tor/ticket/8135) the Port has changed from 9050 to 9150 if you use the Tor Browser Bundle. Try the other value if you receive a "Connection refused" message.

## Irssi

Freenode recommends connecting to `.onion` directly. It also requires charybdis and ircd-seven's SASL mechanism for identifying to nickserv during connection; see [Irssi#Authenticating with SASL](/index.php/Irssi#Authenticating_with_SASL "Irssi"). Start irssi:

```
$ torsocks irssi

```

Set your identification to nickserv, which will be read when connecting. Supported mechanisms are ECDSA-NIST256P-CHALLENGE (see [ecdsatool](https://github.com/atheme/ecdsatool/blob/master/cap_sasl.pl)) and PLAIN. DH-BLOWFISH is [no longer supported](https://freenode.net/sasl/sasl-irssi.shtml).

```
/sasl set *network* *username* *password* *mechanism*

```

Disable CTCP and DCC and set a different hostname to prevent information disclosure: [[3]](https://encrypteverything.ca/IRC_Anonymity_Guide)

```
/ignore * CTCPS
/ignore * DCC
/set hostname *fake_host*

```

Connect to Freenode:

```
/connect -network *network* frxleqtzgvwkv7oz.onion

```

For more information check [Accessing freenode Via Tor](http://freenode.net/irc_servers.shtml#tor), [SASL README](http://freenode.net/sasl/README.txt) or [IRC/SILC Wiki article](https://trac.torproject.org/projects/tor/wiki/doc/TorifyHOWTO/IrcSilc).

## Pacman

Pacman download operations (repository DBs, packages, and public keys) can be done using the Tor network.

Advantages:

*   Attackers that can monitor your Internet connection and that specifically targets your machine cannot watch the updates anymore and, because of that, they cannot deduce the packages you have installed, how up to date they are, when or how frequently you update them. An attacker can still learn what software and the versions you use by other means, for instance watching the packets from your http server or probing the machine will show that you have an http server installed and its version.
*   If the mirror is not an onion, a malicious exit nodes you are going through can watch the updates, and may decide to attack you, however they probably cannot know who they are attacking.
*   Attackers trying to make your machine believe that there are no new updates to prevent it from getting security fixes will have a harder time doing it since they cannot target your machine specifically.

Disadvantages:

*   Longer updates times due to Longer latency and lower throughput. This can be a big security risk if/when the updates needs to be done as fast as possible, especially on machines directly connected to the Internet. That is the case when there is a huge security flaw, and that the flaws are fast to probe, easy to exploit, and that attackers have already started targeting as many systems as they can before the systems are updated.

Reliability with Tor:

*   You don't need a working DNS anymore.
*   You depend on the Tor network and the exit nodes not blocking the updates.
*   You depend on the Tor daemon to work properly. The Tor daemon may not work if there is no more disk space available to it. "Reserved blocks gid:" in ext4, quotas, or other means can fix that.
*   If you are in a country where Tor is blocked, or that there are almost or no Tor users at all, you should use bridges.

Note on gpg:

On stock arch, pacman only trust keys which are either signed by you (That can be done with pacman-key --lsign-key) or signed by 2 of 5 Arch master keys. If a malicious exit node replaces packages with ones signed by its key, pacman will not let the user install the package.
**Warning:** This might not be true for other distributions derived from ARCH, for non-official repositories and for AUR
 `/etc/pacman.conf` 
```
...
XferCommand = /usr/bin/curl --socks5-hostname localhost:9050 -C - -f %u > %o
...
```

## Running a Tor server

The Tor network is reliant on people contributing bandwidth and setting up services. There are several ways to contribute to the network.

### Running a Tor bridge

A Tor bridge is a Tor relay that is not listed in the public Tor directory, thus making it possible for people to connect to the Tor network when governments or ISPs block all public Tor relays.

#### Configuration

According to [https://www.torproject.org/docs/bridges](https://www.torproject.org/docs/bridges) , make your `torrc` be just these four lines (Default: `/etc/tor/torrc`, or `$HOME/.torrc` if that file is not found)

```
   SocksPort 0
   ORPort 443
   BridgeRelay 1
   Exitpolicy reject *:*

```

#### Troubleshooting

If you get "Could not bind to 0.0.0.0:443: Permission denied" errors on startup, you will need to pick a higher ORPort (e.g. 8080), or perhaps [forward the port](http://www.portforward.com/) in your router.

### Running a Tor relay

This means that your machine will act as an entry node or forwarding relay and, unlike a bridge, it will be listed in the public Tor directory. Your IP address will be publicly visible in the Tor directory but the relay will only forward to other relays or Tor exit nodes, not directly to the internet.

#### Configuration

You should at least share 20KiB/s:

```
Nickname *tornickname*
ORPort 9001                    # This TCP-Port has to be opened/forwarded in your Firewall
BandwidthRate 20 KB            # Throttle traffic to 20KB/s
BandwidthBurst 50 KB           # But allow bursts up to 50KB/s

```

Disallow exits from your relay:

```
ExitPolicy reject *:*

```

### Running a Tor exit node

Any requests from a Tor user to the regular internet obviously need to exit the network somewhere, and exit nodes provide this vital service. To the accessed host, the request will appear as having originated from your machine. This means that running an exit node is generally considered more legally onerous than running other forms of Tor relays. Before becoming an exit relay, you may want to read [Tips for Running an Exit Node With Minimal Harassment](https://blog.torproject.org/running-exit-node).

#### Configuration

Using the torrc, you can configure which services you wish to allow through your exit node. Allow all traffic:

```
ExitPolicy accept *:*

```

Allow only irc ports 6660-6667 to exit from node:

```
ExitPolicy accept *:6660-6667,reject *:* # Allow irc ports but no more

```

By default, Tor will block certain ports. You can use the torrc to overide this.

```
ExitPolicy accept *:119        # Accept nntp as well as default exit policy

```

#### +100Mbps Exit Relay configuration example

If you run a fast exit relay (+100Mbps) with `ORPort 443` and `DirPort 80` (as recommended in [Configuring a Tor relay on Debian/Ubuntu](http://www.torproject.org/docs/tor-relay-debian.html.en#after)) the following configuration changes might serve as inspiration to setup Tor alongside [iptables](/index.php/Iptables "Iptables") firewall, [Haveged](/index.php/Haveged "Haveged") to increase system entropy and [pdnsd](/index.php/Pdnsd "Pdnsd") as DNS cache. It is important to *first* read [Configuring a Tor relay on Debian/Ubuntu](http://www.torproject.org/docs/tor-relay-debian.html.en#after).

**Note:** See [#Running Tor in a systemd-nspawn container with a virtual network interface](#Running_Tor_in_a_systemd-nspawn_container_with_a_virtual_network_interface) for instructions to install Tor in a `systemd-nspawn` container. [Haveged](/index.php/Haveged "Haveged") should be installed on the container host.

##### Tor

###### Raise maximum number of open file descriptors

To handle more than 8192 connections `LimitNOFILE` can be raised to 32768 as per [Tor FAQ](https://www.torproject.org/docs/faq.html.en#PackagedTor).

 `/etc/systemd/system/tor.service.d/increase-file-limits.conf` 
```
[Service]
LimitNOFILE=32768

```

To succesfully raise `nofile` limit, you may also have to append the following:

 `/etc/security/limits.conf` 
```
...
tor     soft    nofile    32768
tor     hard    nofile    32768
@tor    soft    nofile    32768
@tor    hard    nofile    32768

```

Check if the `nofile` (filedescriptor) limit is successfully raised with `# sudo -u tor 'ulimit -Hn'` or `# sudo -u tor bash` and `# ulimit -Hn`.

###### Start tor.service as root to bind Tor to privileged ports

To bind Tor to privileged ports the service must be started as root. Please specify `User tor` option in `/etc/tor/torrc`.

 `/etc/systemd/system/tor.service.d/start-as-root.conf` 
```
[Service]
User=root

```

###### Tor configuration

To listen on Port 80 and 443 the service need to be started as `root` as described in [#Start tor.service as root to bind Tor to privileged ports](#Start_tor.service_as_root_to_bind_Tor_to_privileged_ports). Use the `User tor` option in `/etc/tor/torrc` to properly reduce Tor’s privileges.

 `/etc/tor/torrc` 
```
SocksPort 0                                       ## Pure relay configuration without local socks proxy

Log notice stdout                                 ## Default Tor behavior

ControlPort 9051                                  ## For arm connection
CookieAuthentication 1                            ## For arm connection

ORPort 443                                        ## Service must be started as root

Address $IP                                       ## IP or FQDN
Nickname $NICKNAME                                ## Nickname displayed in [Onionoo](https://onionoo.torproject.org/)

RelayBandwidthRate 500 Mbits                      ## bytes|KBytes|MBytes|GBytes|KBits|MBits|GBits
RelayBandwidthBurst 1000 MBits                    ## bytes|KBytes|MBytes|GBytes|KBits|MBits|GBits

ContactInfo $E-MAIL - $BTC-ADDRESS                ## See [OnionTip](https://oniontip.com/)

DirPort 80                                        ## Service must be started as root
DirPortFrontPage /etc/tor/tor-exit-notice.html    ## Original: [https://gitweb.torproject.org/tor.git/plain/contrib/operator-tools/tor-exit-notice.html](https://gitweb.torproject.org/tor.git/plain/contrib/operator-tools/tor-exit-notice.html)

MyFamily $($KEYID),$($KEYID)...                   ## Remember $ in front of keyid(s) ;)

ExitPolicy reject XXX.XXX.XXX.XXX/XX:*            ## Block domain of public IP in addition to std. exit policy

User tor                                          ## Return to tor user after service started as root to listen on privileged ports

DisableDebuggerAttachment 0                       ## For arm connection

### Performance related options ###
AvoidDiskWrites 1                                 ## Reduce wear on SSD
DisableAllSwap 1                                  ## Service must be started as root
HardwareAccel 1                                   ## Look for OpenSSL hardware cryptographic support
NumCPUs 2                                         ## Only start two threads

```

This configuration is based on the [Tor Manual](https://www.torproject.org/docs/tor-manual.html.en).

Tor opens a socks proxy on port 9050 by default -- even if you do not configure one. Set `SocksPort 0` if you plan to run Tor only as a relay, and not make any local application connections yourself.

`Log notice stdout` changes logging to stdout, which is also the Tor default. `ControlPort 9051`, `CookieAuthentication 1` and `DisableDebuggerAttachment 0` enables [arm](https://www.archlinux.org/packages/?name=arm) to connect to Tor and display connections.

`ORPort 443` and `DirPort 80` lets Tor listen on port 443 and 80 and `DirPortFrontPage` displays the [tor-exit-notice.html](https://gitweb.torproject.org/tor.git/plain/contrib/operator-tools/tor-exit-notice.html) on port 80.

`ExitPolicy reject XXX.XXX.XXX.XXX/XX:*` should reflect your public IP and netmask, which can be obtained with the command `# ip addr`, so exit connections cannot connect to the host or neighboring machines public IP and circumvent firewalls.

`AvoidDiskWrites 1` reduces disk writes and wear on SSD. `DisableAllSwap 1` "will attempt to lock all current and future memory pages, so that memory cannot be paged out".

If `# cat /proc/cpuinfo | grep aes` returns that your CPU supports AES instructions and `# lsmod | grep aes` returns that the module is loaded, you can specify `HardwareAccel 1` which tries "to use built-in (static) crypto hardware acceleration when available", see [http://www.torservers.net/wiki/setup/server#aes-ni_crypto_acceleration](http://www.torservers.net/wiki/setup/server#aes-ni_crypto_acceleration).

`ORPort 443`, `DirPort 80` and `DisableAllSwap 1` require that you start the Tor service as `root` as described in [#Start tor.service as root to bind Tor to privileged ports](#Start_tor.service_as_root_to_bind_Tor_to_privileged_ports). Use the `User tor` option to properly reduce Tor’s privileges.

##### arm

If `ControlPort 9051` and `CookieAuthentication 1` is specified in `/etc/tor/torrc`, [arm](https://www.archlinux.org/packages/?name=arm) can be started with `sudo -u tor arm`. If you want to watch Tor connections in [arm](https://www.archlinux.org/packages/?name=arm) `DisableDebuggerAttachment 0` must also be specified.

##### iptables

Setup and learn to use [iptables](/index.php/Iptables "Iptables"). Instead of being a [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall") where connection tracking would have to track thousands of connections on a tor exit relay this firewall configuration is stateless.

 `/etc/iptables/iptables.rules` 
```
*raw
-A PREROUTING -j NOTRACK
-A OUTPUT -j NOTRACK
COMMIT

*filter
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -p tcp ! --syn -j ACCEPT
-A INPUT -p udp -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -p tcp --dport 443 -j ACCEPT
-A INPUT -p tcp --dport 80 -j ACCEPT
-A INPUT -i lo -j ACCEPT
COMMIT

```

`-A PREROUTING -j NOTRACK` and `-A OUTPUT -j NOTRACK` disables connection tracking in the `raw` table.

`:INPUT DROP [0:0]` is the default `INPUT` target and drops input traffic we do not specifically `ACCEPT`.

`:FORWARD DROP [0:0]` is the default `FORWARD` target and only relevant if the host is a normal router, not when the host is an onion router.

`:OUTPUT ACCEPT [0:0]` is the default `OUTPUT` target and allows all outgoing connections.

`-A INPUT -p tcp ! --syn -j ACCEPT` allow already established incoming TCP connections per the rules below and TCP connections established from the exit node.

`-A INPUT -p udp -j ACCEPT` allow all incoming UDP connections because we do not use connection tracking.

`-A INPUT -p icmp -j ACCEPT` allow [ICMP](https://en.wikipedia.org/wiki/Internet_Control_Message_Protocol "wikipedia:Internet Control Message Protocol").

`-A INPUT -p tcp --dport 443 -j ACCEPT` allow incoming connections to the `ORPort`.

`-A INPUT -p tcp --dport 80 -j ACCEPT` allow incoming connections to the `DirPort`.

`-A INPUT -i lo -j ACCEPT` allows all connections on the loopback interface.

##### Haveged

See [Haveged](/index.php/Haveged "Haveged") to decide if your system generates enough entropy to handle a lot of OpenSSL connections, see [haveged - A simple entropy daemon](http://www.issihosts.com/haveged/) and [how-to-setup-additional-entropy-for-cloud-servers-using-haveged](http://www.digitalocean.com/community/tutorials/how-to-setup-additional-entropy-for-cloud-servers-using-haveged) for documentation.

##### pdnsd

**Warning:** This configuration assumes your network DNS resolver is trusted (uncensored).

You can use [pdnsd](/index.php/Pdnsd "Pdnsd") to cache DNS queries locally, so the exit relay can resolve DNS faster and the exit relay does not forward all DNS queries to an external DNS recursor.

 `/etc/pdnsd.conf` 
```
...
perm_cache=102400                       ## (Default value)*100 = 1MB * 100 = 100MB
...
server {
    label= "resolvconf";
    file = "/etc/pdnsd-resolv.conf";    ## Preferably do not use /etc/resolv.conf
    timeout=4;                          ## Server timeout, this may be much shorter than the global timeout option.
    uptest=query;                       ## Test availability using empty DNS queries. 
    query_test_name=".";                ## To be used if remote servers ignore empty queries.
    interval=10m;                       ## Test every 10 minutes.
    purge_cache=off;                    ## Ignore TTL.
    edns_query=yes;                     ## Use EDNS for outgoing queries to allow UDP messages larger than 512 bytes. May cause trouble with some legacy systems.
    preset=off;                         ## Assume server is down before uptest.
 }
...

```

This configuration stub shows how to cache queries to your normal DNS recursor locally and increase pdnsd cache size to 100MB.

###### Uncensored DNS

If your local DNS recursor is in some way censored or interferes with DNS queries, see [Resolv.conf#Alternative DNS servers](/index.php/Resolv.conf#Alternative_DNS_servers "Resolv.conf") for alternatives and add them in a seperate server-section in `/etc/pdnsd.conf` as per [Pdnsd#DNS servers](/index.php/Pdnsd#DNS_servers "Pdnsd").

## TorDNS

The Tor 0.2.x series provides a built-in DNS forwarder. To enable it add the following lines to the Tor configuration file and restart the daemon:

 `/etc/tor/torrc` 
```
DNSPort 9053
AutomapHostsOnResolve 1
AutomapHostsSuffixes .exit,.onion

```

This will allow Tor to accept DNS requests (listening on port 9053 in this example) like a regular DNS server, and resolve the domain via the Tor network. A downside is that it is only able to resolve DNS queries for A-records; MX and NS queries are never answered. For more information see this [Debian-based introduction](https://techstdout.boum.org/TorDns/).

DNS queries can also be performed through a command line interface by using `tor-resolve`. For example:

```
$ tor-resolve archlinux.org
66.211.214.131

```

### Using TorDNS for all DNS queries

It is possible to configure your system, if so desired, to use TorDNS for *all* queries your system makes, regardless of whether or not you eventually use Tor to connect to your final destination. To do this, configure your system to use 127.0.0.1 as its DNS server and edit the 'DNSPort' line in `/etc/tor/torrc` to show:

```
DNSPort 53

```

Alternatively, you can use a local caching DNS server, such as [dnsmasq](/index.php/Dnsmasq "Dnsmasq") or [pdnsd](/index.php/Pdnsd "Pdnsd"), which will also compensate for TorDNS being a little slower than traditional DNS servers. The following instructions will show how to set up *dnsmasq* for this purpose.

Change the tor setting to listen for the DNS request in port 9053 and install [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq).

Modify its configuration file so that it contains:

 `/etc/dnsmasq.conf` 
```
no-resolv
port=9053
server=127.0.0.1#9053
listen-address=127.0.0.1

```

These configurations set dnsmasq to listen only for requests from the local computer, and to use TorDNS at its sole upstream provider. It is now neccessary to edit `/etc/resolv.conf` so that your system will query only the dnsmasq server.

 `/etc/resolv.conf` 
```
nameserver 127.0.0.1

```

Start the **dnsmasq** daemon.

Finally if you use *dhcpd* you would need to change its settings to that it does not alter the resolv configuration file. Just add this line in the configuration file:

 `/etc/dhcpcd.conf` 
```
nohook resolv.conf

```

If you already have an *nohook* line, just add **resolv.conf** separated with a comma.

## Torsocks

**torsocks** will allow you use an application via the Tor network without the need to make configuration changes to the application involved. From the man page:

*torsocks is a wrapper between the torsocks library and the application in order to make every Internet communication go through the Tor network.*

Usage example:

```
$ torsocks elinks checkip.dyndns.org
$ torsocks wget -qO- https://check.torproject.org/ | grep -i congratulations

```

## Transparent Torification

In some cases it is more secure and often easier to transparently torify an entire system instead of configuring individual applications to use Tor's socks port, not to mention preventing DNS leaks. Transparent torification can be done with [iptables](/index.php/Iptables "Iptables") in such a way that all outbound packets are redirected through Tor's *TransPort*, except the Tor traffic itself. Once in place, applications do not need to be configured to use Tor, though Tor's *SocksPort* will still work. This also works for DNS via Tor's *DNSPort*, but realize that Tor only supports TCP, thus UDP packets other than DNS cannot be sent through Tor and therefore must be blocked entirely to prevent leaks. Using iptables to transparently torify a system affords comparatively strong leak protection, but it is not a substitute for virtualized torification applications such as Whonix, or TorVM [[4]](https://www.whonix.org/wiki/Comparison_with_Others). Transparent torification also will not protect against fingerprinting attacks on its own, so it is recommended to use it in conjunction with the Tor Browser (search the AUR for the version you want: [https://aur.archlinux.org/packages/?K=tor-browser](https://aur.archlinux.org/packages/?K=tor-browser)) or to use an amnesic solution like [Tails](http://tails.boum.org/) instead. Applications can still learn your computer's hostname, MAC address, serial number, timezone, etc. and those with root privileges can disable the firewall entirely. In other words, transparent torification with iptables protects against accidental connections and DNS leaks by misconfigured software, it is not sufficient to protect against malware or software with serious security vulnerabilities.

To enable transparent torification, use the following file for `iptables-restore` and `ip6tables-restore` (internally used by [systemd](/index.php/Systemd "Systemd")'s `iptables.service` and `ip6tables.service`).

**Note:**

This file uses the nat table to force outgoing connections through the TransPort or DNSPort, and blocks anything it cannot torrify.

*   Now using `--ipv6` and `--ipv4` for protocol specific changes. `iptables-restore` and `ip6tables-restore` can now use the same file.
*   Where --ipv6 or --ipv4 is explicitly defined, `ip*tables-restore` will ignore the rule if it is not for the correct protocol.
*   `ip6tables` does not support `--reject-with`. Make sure your torrc contains the following lines:

```
SocksPort 9050
DNSPort 5353
TransPort 9040

```

See [iptables(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/iptables.8).

**Note:**

iptables-restore: unable to initialize table 'nat'

Requires:

```
modprobe ip_tables
modprobe iptable_nat
modprobe ip_conntrack
modprobe iptable-filter
modprobe ipt_state

```

 `/etc/iptables/iptables.rules` 
```

*nat
:PREROUTING ACCEPT [6:2126]
:INPUT ACCEPT [0:0]
:OUTPUT ACCEPT [17:6239]
:POSTROUTING ACCEPT [6:408]

-A PREROUTING ! -i lo -p udp -m udp --dport 53 -j REDIRECT --to-ports 5353
-A PREROUTING ! -i lo -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -j REDIRECT --to-ports 9040
-A OUTPUT -o lo -j RETURN
--ipv4 -A OUTPUT -d 192.168.0.0/16 -j RETURN
-A OUTPUT -m owner --uid-owner "tor" -j RETURN
-A OUTPUT -p udp -m udp --dport 53 -j REDIRECT --to-ports 5353
-A OUTPUT -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -j REDIRECT --to-ports 9040
COMMIT

*filter
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
:OUTPUT DROP [0:0]

-A INPUT -i lo -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
--ipv4 -A INPUT -p tcp -j REJECT --reject-with tcp-reset
--ipv4 -A INPUT -p udp -j REJECT --reject-with icmp-port-unreachable
--ipv4 -A INPUT -j REJECT --reject-with icmp-proto-unreachable
--ipv6 -A INPUT -j REJECT
--ipv4 -A OUTPUT -d 127.0.0.0/8 -j ACCEPT
--ipv4 -A OUTPUT -d 192.168.0.0/16 -j ACCEPT
--ipv6 -A OUTPUT -d ::1/8 -j ACCEPT
-A OUTPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A OUTPUT -m owner --uid-owner "tor" -j ACCEPT
--ipv4 -A OUTPUT -j REJECT --reject-with icmp-port-unreachable
--ipv6 -A OUTPUT -j REJECT
COMMIT

```

This file also works for ip6tables-restore, so you may symlink it:

```
ln -s /etc/iptables/iptables.rules /etc/iptables/ip6tables.rules

```

Then make sure Tor is running, and [start/enable](/index.php/Start/enable "Start/enable") the `iptables` and `ip6tables` systemd units.

You may want to add `Requires=iptables.service` and `Requires=ip6tables.service` to whatever systemd unit logs your user in (most likely a [display manager](/index.php/Display_manager "Display manager")), to prevent any user processes from being started before the firewall up. See [systemd](/index.php/Systemd "Systemd").

## Troubleshooting

### Problem with user value

If the **tor** daemon failed to start, then run the following command as root (or use sudo)

```
# tor

```

If you get the following error

```
May 23 00:27:24.624 [warn] Error setting groups to gid 43: "Operation not permitted".
May 23 00:27:24.624 [warn] If you set the "User" option, you must start Tor as root.
May 23 00:27:24.624 [warn] Failed to parse/validate config: Problem with User value. See logs for details.
May 23 00:27:24.624 [err] Reading config failed--see warnings above.

```

Then it means that the problem is with the User value, which likely means that one or more files or directories in your `/var/lib/tor` directory is not owned by tor. This can be determined by using the following find command:

```
find /var/lib/tor/ ! -user tor

```

Any files or directories listed in the output from this command needs to have its ownership changed. This can be done individually for each file like so:

```
chown tor:tor /var/lib/tor/filename

```

Or to change everything listed by the above find example, modify the command to this:

```
find /var/lib/tor/ ! -user tor -exec chown tor:tor {} \;

```

Tor should now start up correctly.

Still if you cannot start the tor service, run the service using root (this will switch back to the tor user). To do this, change the user name in the `/etc/tor/torrc` file:

```
User tor

```

Now modify the systemd's tor service file `/usr/lib/systemd/system/tor.service` as follows

```
[Service]
User=root
Group=root
Type=simple

```

The process will be run as tor user. For this purpose change user and group ID to tor and also make it writable:

```
# chown -R tor:tor /var/lib/tor/
# chmod -R 755 /var/lib/tor

```

Now save changes:

```
# systemctl --system daemon-reload

```

Then [start](/index.php/Start "Start") `tor.service`.

## See also

*   [Running the Tor client on Linux/BSD/Unix](https://www.torproject.org/docs/tor-doc-unix.html.en)
*   [Unix-based Tor Articles](https://trac.torproject.org/projects/tor/wiki#Unixish)
*   [Software commonly integrated with Tor](https://trac.torproject.org/projects/tor/wiki/doc/SupportPrograms)
*   [How to set up a Tor *Hidden Service*](https://www.torproject.org/docs/tor-hidden-service.html.en)
*   [List of tor pluggable transports for obfuscating tor's traffic](https://trac.torproject.org/projects/tor/wiki/doc/PluggableTransports)