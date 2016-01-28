# DNSCrypt

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[DNSCrypt](http://dnscrypt.org/) encrypts and authenticates DNS traffic between user and DNS resolver. While IP traffic itself is unchanged, it prevents local spoofing of DNS queries, ensuring DNS responses are sent by the server of choice. [[1]](https://www.reddit.com/r/sysadmin/comments/2hn435/dnssec_vs_dnscrypt/ckuhcbu)

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 DNSCrypt as a forwarder for local DNS cache](#DNSCrypt_as_a_forwarder_for_local_DNS_cache)
        *   [3.1.1 Example: configuration for Unbound](#Example:_configuration_for_Unbound)
        *   [3.1.2 Example: configuration for dnsmasq](#Example:_configuration_for_dnsmasq)
        *   [3.1.3 Example: configuration for pdnsd](#Example:_configuration_for_pdnsd)
    *   [3.2 Enable EDNS0](#Enable_EDNS0)
        *   [3.2.1 Test EDNS0](#Test_EDNS0)
    *   [3.3 Redundant DNSCrypt providers](#Redundant_DNSCrypt_providers)

## Installation

[Install](/index.php/Install "Install") the [dnscrypt-proxy](https://www.archlinux.org/packages/?name=dnscrypt-proxy) package.

## Configuration

When `dnscrypt-proxy.socket` is [enabled](/index.php/Enable "Enable"), _dnscrypt-proxy_ accepts incoming requests on `127.0.0.1:53` to a DNS resolver. The default DNS resolver for `dnscrypt-proxy.service` is _dnscrypt.eu-nl_. Compatible resolver names are visible in the first column of `/usr/share/dnscrypt-proxy/dnscrypt-resolvers.csv` (a potentially more up-to-date list is available directly on the [upstream page](https://github.com/jedisct1/dnscrypt-proxy/blob/master/dnscrypt-resolvers.csv)).

To change the default, [edit](/index.php/Systemd#Editing_provided_units "Systemd") `dnscrypt-proxy.service`. It is recommended to choose a provider close to your location.

Modify the [resolv.conf](/index.php/Resolv.conf "Resolv.conf") file and replace the current set of resolver addresses with _localhost_:

```
nameserver 127.0.0.1

```

Other programs may overwrite this setting; see [resolv.conf#Preserve DNS settings](/index.php/Resolv.conf#Preserve_DNS_settings "Resolv.conf") for details.

## Tips and tricks

### DNSCrypt as a forwarder for local DNS cache

It is recommended to run DNSCrypt as a forwarder for a local DNS cache, otherwise every single query will make a round-trip to the upstream resolver. Any local DNS caching program should work, examples below show configuration for [Unbound](/index.php/Unbound "Unbound"), [dnsmasq](/index.php/Dnsmasq "Dnsmasq"), and [pdnsd](/index.php/Pdnsd "Pdnsd").

First configure _dnscrypt-proxy_ to listen on a port different from the default `53`, since the DNS cache needs to listen on `53` and query _dnscrypt-proxy_ on a different port. Port number `40` is used as an example in this section:

 `# systemctl edit dnscrypt-proxy.socket` 

```
[Socket]
ListenStream=
ListenDatagram=
ListenStream=127.0.0.1:40
ListenDatagram=127.0.0.1:40
```

**Note:** The `ListenStream` and `ListenDatagram` options need to be cleared with empty assignment before overriding, otherwise the new address would be _added_ to the list of sockets. See [systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd") for details.

Then restart `dnscrypt-proxy.socket` and _stop_ `dnscrypt-proxy.service` if already running to let it be started by the _.socket_ unit.

#### Example: configuration for Unbound

Configure [Unbound](/index.php/Unbound "Unbound") to your liking (remember to [set /etc/resolv.conf to use the local DNS server](/index.php/Unbound#Set_.2Fetc.2Fresolv.conf_to_use_the_local_DNS_server "Unbound")) and add the following lines to the end of the `server` section in `/etc/unbound/unbound.conf`:

```
do-not-query-localhost: no
forward-zone:
  name: "."
  forward-addr: 127.0.0.1@40

```

**Tip:** If you are setting up a server, add `interface: 0.0.0.0@53` and `access-control: _your-network_/_subnet-mask_ allow` inside the `server:` section so that the other computers can connect to the server. A client must be configured with `nameserver _address-of-your-server_` in `/etc/resolv.conf`.

Restart `unbound.service` to apply the changes.

#### Example: configuration for dnsmasq

Configure dnsmasq as a [local DNS cache](/index.php/Dnsmasq#DNS_Cache_Setup "Dnsmasq"). The basic configuration to work with DNSCrypt:

 `/etc/dnsmasq.conf` 

```
no-resolv
server=127.0.0.1#40
listen-address=127.0.0.1
```

If you configured DNSCrypt to use a resolver with enabled DNSSEC validation, make sure to enable it also in dnsmasq:

 `/etc/dnsmasq.conf`  `proxy-dnssec` 

Restart `dnsmasq.service` to apply the changes.

#### Example: configuration for pdnsd

Install [pdnsd](/index.php/Pdnsd "Pdnsd"). A basic configuration to work with DNSCrypt is:

 `/etc/pdnsd.conf` 

```
global {
    perm_cache = 1024;
    cache_dir = "/var/cache/pdnsd";
    run_as = "pdnsd";
    server_ip = 127.0.0.1;
    status_ctl = on;
    query_method = udp_tcp;
    min_ttl = 15m;       # Retain cached entries at least 15 minutes.
    max_ttl = 1w;        # One week.
    timeout = 10;        # Global timeout option (10 seconds).
    neg_domain_pol = on;
    udpbufsize = 1024;   # Upper limit on the size of UDP messages.
}

server {
    label = "dnscrypt-proxy";
    ip = 127.0.0.1;
    port = 40;
    timeout = 4;
    proxy_only = on;
}

source {
    owner = localhost;
    file = "/etc/hosts";
}
```

Restart `pdnsd.service` to apply the changes.

### Enable EDNS0

[Extension Mechanisms for DNS](https://en.wikipedia.org/wiki/Extension_mechanisms_for_DNS "wikipedia:Extension mechanisms for DNS") that, among other things, allows a client to specify how large a reply over UDP can be.

Add the following line to your `/etc/resolv.conf`:

```
options edns0

```

You may also wish to add the following argument to _dnscrypt-proxy_:

```
--edns-payload-size=<bytes>

```

The default size being **1252** bytes, with values up to **4096** bytes being purportedly safe. A value below or equal to **512** bytes will disable this mechanism, unless a client sends a packet with an OPT section providing a payload size.

#### Test EDNS0

Make use of the [DNS Reply Size Test Server](https://www.dns-oarc.net/oarc/services/replysizetest), use the _dig_ command line tool from the [bind-tools](https://www.archlinux.org/packages/?name=bind-tools) package to issue a TXT query for the name _rs.dns-oarc.net_:

```
$ dig +short rs.dns-oarc.net txt

```

With **EDNS0** supported, the output should look similar to this:

```
rst.x3827.rs.dns-oarc.net.
rst.x4049.x3827.rs.dns-oarc.net.
rst.x4055.x4049.x3827.rs.dns-oarc.net.
"2a00:d880:3:1::a6c1:2e89 DNS reply size limit is at least 4055 bytes"
"2a00:d880:3:1::a6c1:2e89 sent EDNS buffer size 4096"

```

### Redundant DNSCrypt providers

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Needs some tweaks to comply with [Help:Style](/index.php/Help:Style "Help:Style"), e.g avoid writing in first person and link to [enable](/index.php/Enable "Enable"), [start](/index.php/Start "Start") and similar instead of explicit systemctl commands. (Discuss in [Talk:DNSCrypt#](https://wiki.archlinux.org/index.php/Talk:DNSCrypt))

Obtaining redundancy requires a simple edit to the above Unbound example and the addition of a second instance of the dnscrypt-proxy and service. Please be sure that the above Unbound example is working prior to proceeding, as this tip extends the previous example.

Extend the above [Unbound](/index.php/Unbound "Unbound") configuration in `/etc/unbound/unbound.conf` to include an additional forward address that uses a different port. Port 41 is used in the below example:

```
do-not-query-localhost: no
forward-zone:
  name: "."
  forward-addr: 127.0.0.1@40
  forward-addr: 127.0.0.1@41

```

We will use an instanced systemd service to accomplish this. This will use one dnscrypt-proxy@.service systemd service to handle as many distinct DNSCrypt resolves as we want.

First, we need /etc/systemd/system/dnscrypt-proxy@.service, containing:

```
[Unit]
Description=DNSCrypt client proxy
Documentation=man:dnscrypt-proxy(8)
Requires=dnscrypt-proxy@%i.socket

[Service]
Type=notify
NonBlocking=true
ExecStart=/usr/sbin/dnscrypt-proxy \
    --resolver-name=%i
Restart=always

```

This specifies an instanced systemd service that starts a dnscrypt-proxy using the service name specified after the @ symbol of a corresponding .socket file.

You can now create two (or more!) socket files, specifying different DNSCrypt providers.

For the first proxy, listening on 127.0.0.1@40 and connecting to the default dnscrypt.eu-nl provider, copy /lib/systemd/system/dnscrypt-proxy.socket to /etc/systemd/system/dnscrypt-proxy@dnscrypt.eu-nl.socket.

For the second proxy, copy /lib/systemd/system/dnscrypt-proxy.socket /etc/systemd/system/dnscrypt-proxy@cloudns-syd.socket (you can replace **cloudns-syd** with any of the provider names in /usr/share/dnscrypt-proxy/dnscrypt-resolvers.csv; choosing a provider geographically close is generally a good idea) and edit it to specify port 41 instead of port 40:

```
[Unit]
Description=dnscrypt-proxy-secondary listening socket

[Socket]
ListenStream=127.0.0.1:41
ListenDatagram=127.0.0.1:41

[Install]
WantedBy=sockets.target

```

Now we need to reload the systemd configuration.

```
systemctl daemon-reload

```

Since we are replacing the default service with a different name, we need to explicitly stop and disable the default service:

```
systemctl disable dnscrypt-proxy dnscrypt-proxy.socket
systemctl stop dnscrypt-proxy dnscrypt-proxy.socket

```

Now we enable and start the sockets:

```
systemctl enable dnscrypt-proxy@dnscrypt.eu-nl.socket dnscrypt-proxy@cloudns-syd.socket
systemctl start dnscrypt-proxy@dnscrypt.eu-nl.socket dnscrypt-proxy@cloudns-syd.socket

```

Finally Restart Unbound:

```
systemctl restart unbound

```

If successful, your two selected dns providers should be the only ones found when using one of the dns leak test websites.

Retrieved from "[https://wiki.archlinux.org/index.php?title=DNSCrypt&oldid=412765](https://wiki.archlinux.org/index.php?title=DNSCrypt&oldid=412765)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Domain Name System](/index.php/Category:Domain_Name_System "Category:Domain Name System")
*   [Encryption](/index.php/Category:Encryption "Category:Encryption")

Hidden category:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")