Related articles

*   [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution")

[dnscrypt-proxy](https://github.com/jedisct1/dnscrypt-proxy) is a DNS proxy with support for the encrypted DNS protocols [DNS over HTTPS](/index.php/DNS_over_HTTPS "DNS over HTTPS") and [DNSCrypt](https://dnscrypt.info/), which can be used to prevent man-in-the-middle attacks and eavesdropping. *dnscrypt-proxy* is also compatible with [DNSSEC](/index.php/DNSSEC "DNSSEC").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Startup](#Startup)
    *   [2.2 Select resolver](#Select_resolver)
    *   [2.3 Disable any services bound to port 53](#Disable_any_services_bound_to_port_53)
    *   [2.4 Modify resolv.conf](#Modify_resolv.conf)
    *   [2.5 Start systemd service](#Start_systemd_service)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Local DNS cache configuration](#Local_DNS_cache_configuration)
        *   [3.1.1 Change port](#Change_port)
        *   [3.1.2 Example local DNS cache configurations](#Example_local_DNS_cache_configurations)
            *   [3.1.2.1 Unbound](#Unbound)
            *   [3.1.2.2 dnsmasq](#dnsmasq)
            *   [3.1.2.3 pdnsd](#pdnsd)
    *   [3.2 Sandboxing](#Sandboxing)
    *   [3.3 Enable EDNS0](#Enable_EDNS0)
        *   [3.3.1 Test EDNS0](#Test_EDNS0)

## Installation

[Install](/index.php/Install "Install") the [dnscrypt-proxy](https://www.archlinux.org/packages/?name=dnscrypt-proxy) package.

## Configuration

### Startup

The service can be started in two mutually exclusive ways (i.e. only one of the two may be enabled):

*   With the `.service` file.

**Note:** The `listen_addresses` option must be configured (e.g. `listen_addresses = ['127.0.0.1:53', '[::1]:53']`) in the configuration file when using the `.service` file.

*   Through the `.socket` activation.

**Note:** When using socket activation the `listen_addresses` option must be set to empty (i.e. `listen_addresses = [ ]`) in the configuration file, since systemd is taking care of the socket configuration.

### Select resolver

By leaving `server_names` commented out in the configuration file `/etc/dnscrypt-proxy/dnscrypt-proxy.toml`, *dnscrypt-proxy* will choose the fastest server from the sources already configured under `[sources]` [[1]](https://github.com/jedisct1/dnscrypt-proxy/wiki/Configuration#an-example-static-server-entry). The lists will be downloaded, verified, and automatically updated [[2]](https://github.com/jedisct1/dnscrypt-proxy/wiki/Configuration-Sources#what-is-the-point-of-these-lists). Thus, configuring a specific set of servers is optional.

To manually set which server is used, edit `/etc/dnscrypt-proxy/dnscrypt-proxy.toml` and uncomment the `server_names` variable, selecting one or more of the servers. For example, to use Cloudflare's servers:

```
server_names = ['cloudflare', 'cloudflare-ipv6']

```

A full list of resolvers is located at the [upstream page](https://download.dnscrypt.info/resolvers-list/v2/public-resolvers.md) or [Github](https://raw.githubusercontent.com/DNSCrypt/dnscrypt-resolvers/master/v2/public-resolvers.md). If *dnscrypt-proxy* has run successfully on the system before, `/var/cache/dnscrypt-proxy/public-resolvers.md` will also contain a list. Look at the description for servers note which validate [DNSSEC](/index.php/DNSSEC "DNSSEC"), do not log, and are uncensored. These requirements can be configured globally with the `require_dnssec`, `require_nolog`, `require_nofilter` options.

### Disable any services bound to port 53

**Tip:** If using [#Unbound](#Unbound) as your local DNS cache this section can be ignored, as *unbound* runs on port 53 by default.

To see if any programs are using port 53, run:

```
 $ ss -lp 'sport = :domain'

```

If the output contains more than the first line of column names, you need to disable whatever service is using port 53\. One common culprit is `systemd-resolved.service`([NetworkManager#Unit dbus-org.freedesktop.resolve1.service not found](/index.php/NetworkManager#Unit_dbus-org.freedesktop.resolve1.service_not_found "NetworkManager")), but other network managers may have analogous components. You are ready to proceed once the above command outputs nothing more than the following line:

```
 Netid               State                 Recv-Q                Send-Q                                 Local Address:Port                                   Peer Address:Port

```

### Modify resolv.conf

Modify the [resolv.conf](/index.php/Resolv.conf "Resolv.conf") file and replace the current set of resolver addresses with the address for *localhost* and options [[3]](https://github.com/jedisct1/dnscrypt-proxy/wiki/Installation-linux#step-4-change-the-system-dns-settings):

```
nameserver ::1
nameserver 127.0.0.1
options edns0 single-request-reopen

```

Other programs may overwrite this setting; see [resolv.conf#Overwriting of /etc/resolv.conf](/index.php/Resolv.conf#Overwriting_of_/etc/resolv.conf "Resolv.conf") for details.

### Start systemd service

Finally, [start/enable](/index.php/Start/enable "Start/enable") the `dnscrypt-proxy.service` unit or `dnscrypt-proxy.socket`, depending on which method you chose above.

## Tips and tricks

### Local DNS cache configuration

**Tip:** *dnscrypt-proxy* can cache entries without relying on another program. This feature is enabled by default with the line `cache = true` in your *dnscrypt-proxy* configuration file

It is recommended to run *dnscrypt-proxy* as a forwarder for a local DNS cache if not using *dnscrypt-proxy's* cache feature; otherwise, every single query will make a round-trip to the upstream resolver. Any local DNS caching program should work. In addition to setting up *dnscrypt-proxy*, you must setup your local DNS cache program.

#### Change port

In order to forward queries from a local DNS cache, *dnscrypt-proxy* should listen on a port different from the default `53`, since the DNS cache itself needs to listen on `53` and query *dnscrypt-proxy* on a different port. Port number `53000` is used as an example in this section. In this example, the port number is larger than 1024 so *dnscrypt-proxy* is not required to be run by root.

There are two methods for changing the default port:

**Socket method**

[Edit](/index.php/Edit "Edit") `dnscrypt-proxy.socket` with the following contents:

```
[Socket]
ListenStream=
ListenDatagram=
ListenStream=127.0.0.1:53000
ListenStream=[::1]:53000
ListenDatagram=127.0.0.1:53000
ListenDatagram=[::1]:53000

```

When queries are forwarded from the local DNS cache to `53000`, `dnscrypt-proxy.socket` will start `dnscrypt-proxy.service`.

**Service method**

Edit the `listen_addresses` option in `/etc/dnscrypt-proxy/dnscrypt-proxy.toml` with the following:

```
listen_addresses = ['127.0.0.1:53000', '[::1]:53000']

```

#### Example local DNS cache configurations

The following configurations should work with *dnscrypt-proxy* and assume that it is listening on port `53000`.

##### Unbound

Configure [Unbound](/index.php/Unbound "Unbound") to your liking (in particular, see [Unbound#Local DNS server](/index.php/Unbound#Local_DNS_server "Unbound")) and add the following lines to the end of the `server` section in `/etc/unbound/unbound.conf`:

```
  do-not-query-localhost: no
forward-zone:
  name: "."
  forward-addr: ::1@53000
  forward-addr: 127.0.0.1@53000

```

**Tip:** If you are setting up a server, add `interface: 0.0.0.0@53` and `access-control: *your-network*/*subnet-mask* allow` inside the `server:` section so that the other computers can connect to the server. A client must be configured with `nameserver *address-of-your-server*` in `/etc/resolv.conf`.

[Restart](/index.php/Restart "Restart") `unbound.service` to apply the changes.

##### dnsmasq

Configure dnsmasq as a [local DNS cache](/index.php/Dnsmasq#DNS_server "Dnsmasq"). The basic configuration to work with *dnscrypt-proxy*:

 `/etc/dnsmasq.conf` 
```
no-resolv
server=::1#53000
server=127.0.0.1#53000
listen-address=::1,127.0.0.1
```

If you configured *dnscrypt-proxy* to use a resolver with enabled [DNSSEC](/index.php/DNSSEC "DNSSEC") validation, make sure to enable it also in dnsmasq:

 `/etc/dnsmasq.conf` 
```
conf-file=/usr/share/dnsmasq/trust-anchors.conf
dnssec
```

Restart `dnsmasq.service` to apply the changes.

##### pdnsd

Install [pdnsd](/index.php/Pdnsd "Pdnsd"). A basic configuration to work with *dnscrypt-proxy* is:

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
    port = 53000;
    timeout = 4;
    proxy_only = on;
}

source {
    owner = localhost;
    file = "/etc/hosts";
}
```

Restart `pdnsd.service` to apply the changes.

### Sandboxing

[Edit](/index.php/Edit "Edit") `dnscrypt-proxy.service` to include the following lines:

```
[Service]
CapabilityBoundingSet=CAP_IPC_LOCK CAP_SETGID CAP_SETUID CAP_NET_BIND_SERVICE
ProtectSystem=strict
ProtectHome=true
ProtectKernelTunables=true
ProtectKernelModules=true
ProtectControlGroups=true
PrivateTmp=true
PrivateDevices=true
MemoryDenyWriteExecute=true
NoNewPrivileges=true
RestrictRealtime=true
RestrictAddressFamilies=AF_INET AF_INET6
SystemCallArchitectures=native
SystemCallFilter=~@clock @cpu-emulation @debug @keyring @ipc @module @mount @obsolete @raw-io

```

See [systemd.exec(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.exec.5) and [Systemd#Sandboxing application environments](/index.php/Systemd#Sandboxing_application_environments "Systemd") for more information. Additionally see [upstream comments](https://github.com/jedisct1/dnscrypt-proxy/pull/601#issuecomment-284171727).

### Enable EDNS0

[Extension Mechanisms for DNS](https://en.wikipedia.org/wiki/Extension_mechanisms_for_DNS "wikipedia:Extension mechanisms for DNS") that, among other things, allows a client to specify how large a reply over UDP can be.

Add the following line to your `/etc/resolv.conf`:

```
options edns0

```

You may also wish to append the following to `/etc/dnscrypt-proxy.conf`:

```
EDNSPayloadSize *<bytes>*

```

Where *<bytes>* is a number, the default size being **1252**, with values up to **4096** bytes being purportedly safe. A value below or equal to **512** bytes will disable this mechanism, unless a client sends a packet with an OPT section providing a payload size.

#### Test EDNS0

Make use of the [DNS Reply Size Test Server](https://www.dns-oarc.net/oarc/services/replysizetest), use the *drill* command line tool to issue a TXT query for the name *rs.dns-oarc.net*:

```
$ drill rs.dns-oarc.net TXT

```

With **EDNS0** supported, the "answer section" of the output should look similar to this:

```
rst.x3827.rs.dns-oarc.net.
rst.x4049.x3827.rs.dns-oarc.net.
rst.x4055.x4049.x3827.rs.dns-oarc.net.
"2a00:d880:3:1::a6c1:2e89 DNS reply size limit is at least 4055 bytes"
"2a00:d880:3:1::a6c1:2e89 sent EDNS buffer size 4096"

```