[DNSCrypt](http://dnscrypt.info/) encrypts and authenticates DNS traffic between user and DNS resolver. While IP traffic itself is unchanged, it prevents local spoofing of DNS queries, ensuring DNS responses are sent by the server of choice. [[1]](https://www.reddit.com/r/sysadmin/comments/2hn435/dnssec_vs_dnscrypt/ckuhcbu)

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Select resolver](#Select_resolver)
    *   [2.2 Modify resolv.conf](#Modify_resolv.conf)
    *   [2.3 Start systemd service](#Start_systemd_service)
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
    *   [3.4 Redundant DNSCrypt providers](#Redundant_DNSCrypt_providers)
        *   [3.4.1 Create instanced systemd service](#Create_instanced_systemd_service)
            *   [3.4.1.1 Create systemd file](#Create_systemd_file)
            *   [3.4.1.2 Add dnscrypt-sockets](#Add_dnscrypt-sockets)
            *   [3.4.1.3 Apply new systemd configuration](#Apply_new_systemd_configuration)

## Installation

[Install](/index.php/Install "Install") the [dnscrypt-proxy](https://www.archlinux.org/packages/?name=dnscrypt-proxy) package.

**Tip:** [dnscrypt-proxy-gui](https://aur.archlinux.org/packages/dnscrypt-proxy-gui/) provides a GUI written in Qt to set the DNS server used by DNSCrypt.

## Configuration

**Tip:** An example configuration file, `/etc/dnscrypt-proxy.conf.example` is provided, but note that systemd overrides the `LocalAddress` option with a [socket file](#Change_port).

To configure *dnscrypt-proxy*, perform the following steps:

### Select resolver

Select a resolver from `/usr/share/dnscrypt-proxy/dnscrypt-resolvers.csv` and edit `/etc/dnscrypt-proxy.conf`, using a short name from the csv file's first column, `Name`. For example, to select *dnscrypt.eu-nl* as the resolver:

```
ResolverName dnscrypt.eu-nl

```

**Tip:**

*   A potentially more up-to-date list is available directly on the [upstream page](https://github.com/dyne/dnscrypt-proxy/blob/master/dnscrypt-resolvers.csv).
*   At this stage you may also wish to add an unprivileged user to run dnscrypt. See [#dnscrypt runs with root privileges](#dnscrypt_runs_with_root_privileges).

### Modify resolv.conf

After selecting a dnscrypt resolver, modify the [resolv.conf](/index.php/Resolv.conf "Resolv.conf") file and replace the current set of resolver addresses with address for *localhost*:

```
nameserver 127.0.0.1

```

Other programs may overwrite this setting; see [resolv.conf#Preserve DNS settings](/index.php/Resolv.conf#Preserve_DNS_settings "Resolv.conf") for details.

### Start systemd service

Finally, [start and enable](/index.php/Enable "Enable") the `dnscrypt-proxy.service`.

## Tips and tricks

### Local DNS cache configuration

**Note:** *dnscrypt* can cache entries without relying on another program. Ensure that `LocalCache on` is in your dnscrypt configuration file to enable this feature.

It is recommended to run DNSCrypt as a forwarder for a local DNS cache if not using *dnscrypt's* cache feature; otherwise, every single query will make a round-trip to the upstream resolver. Any local DNS caching program should work. In addition to setting up *dnscrypt-proxy*, you must setup your local DNS cache program.

#### Change port

**Note:** Changing the IP address or port in `/etc/dnscrypt-proxy.conf` [does not work](https://web.archive.org/web/20171215112100/https://github.com/jedisct1/dnscrypt-proxy/issues/528) when using the provided systemd unit and must be changed in the provided systemd socket as follows.

In order to forward to a local DNS cache, *dnscrypt-proxy* should listen on a port different from the default `53`, since the DNS cache itself needs to listen on `53` and query *dnscrypt-proxy* on a different port. Port number `5353` is used as an example in this section. In this example, the port number is larger than 1024 so *dnscrypt-proxy* is not required to be run by root. [Edit](/index.php/Edit "Edit") `dnscrypt-proxy.socket` with the following contents:

```
[Socket]
ListenStream=
ListenDatagram=
ListenStream=127.0.0.1:5353
ListenDatagram=127.0.0.1:5353

```

**Note:** UDP Port `5353` is used by [Avahi](/index.php/Avahi#Firewall "Avahi") (if installed and running) and can cause warnings in the journal and [Avahi](/index.php/Avahi "Avahi")'s mDNS unreliable.

#### Example local DNS cache configurations

The following configurations should work with *dnscrypt-proxy* and assume that it is listening on port `5353`.

##### Unbound

Configure [Unbound](/index.php/Unbound "Unbound") to your liking (in particular, see [Unbound#Local DNS server](/index.php/Unbound#Local_DNS_server "Unbound")) and add the following lines to the end of the `server` section in `/etc/unbound/unbound.conf`:

```
do-not-query-localhost: no
forward-zone:
  name: "."
  forward-addr: 127.0.0.1@5353

```

**Tip:** If you are setting up a server, add `interface: 0.0.0.0@53` and `access-control: *your-network*/*subnet-mask* allow` inside the `server:` section so that the other computers can connect to the server. A client must be configured with `nameserver *address-of-your-server*` in `/etc/resolv.conf`.

[Restart](/index.php/Restart "Restart") `unbound.service` to apply the changes.

##### dnsmasq

Configure dnsmasq as a [local DNS cache](/index.php/Dnsmasq#DNS_cache_setup "Dnsmasq"). The basic configuration to work with DNSCrypt:

 `/etc/dnsmasq.conf` 
```
no-resolv
server=127.0.0.1#5353
listen-address=127.0.0.1
```

If you configured DNSCrypt to use a resolver with enabled DNSSEC validation, make sure to enable it also in dnsmasq:

 `/etc/dnsmasq.conf`  `proxy-dnssec` 

Restart `dnsmasq.service` to apply the changes.

##### pdnsd

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
    port = 5353;
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
CapabilityBoundingSet=CAP_IPC_LOCK CAP_SETGID CAP_SETUID
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

This can be combined with the additions in [#dnscrypt runs with root privileges](#dnscrypt_runs_with_root_privileges).

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

### Redundant DNSCrypt providers

To use several different dnscrypt providers, you may simply copy the original `dnscrypt-proxy.service` and `dnscrypt-proxy.socket`. Then in your new copy of the service change the command line parameters, either pointing to a new configuration file or naming a different resolver directly. From there change the port in the new copy of the socket. Lastly, update your local DNS cache program to point to new service's port. For example, with [unbound](/index.php/Unbound "Unbound") the configuration file would look like if using ports `5353` for the original socket and `5354` for the new socket.

 `/etc/unbound/unbound.conf` 
```
 do-not-query-localhost: no
 forward-zone:
   name: "."
   forward-addr: 127.0.0.1@5353
   forward-addr: 127.0.0.1@5354
```

#### Create instanced systemd service

An alternative option to copying the systemd service is to used an instanced service.

##### Create systemd file

First, create `/etc/systemd/system/dnscrypt-proxy@.service` containing:

```
[Unit]
Description=DNSCrypt client proxy
Documentation=man:dnscrypt-proxy(8)
Requires=dnscrypt-proxy@%i.socket

[Service]
Type=notify
NonBlocking=true
ExecStart=/usr/bin/dnscrypt-proxy \
    --resolver-name=%i
Restart=always

```

This specifies an instanced systemd service that starts a dnscrypt-proxy using the service name specified after the @ symbol of a corresponding .socket file.

##### Add dnscrypt-sockets

To create multiple dnscrypt-proxy sockets, copy `/usr/lib/systemd/system/dnscrypt-proxy.socket` to a new file, `/etc/systemd/system/dnscrypt-proxy@*short-name.here*.socket`, replacing the socket instance name with one of the short names listed in [`dnscrypt-resolvers.csv`](#Select_resolver) and [change the port](#Change_port). Use a different port for each instance (5353, 5354, and so forth).

##### Apply new systemd configuration

Now we need to reload the systemd configuration.

```
# systemctl daemon-reload

```

Since we are replacing the default service with a different name, we need to explicitly [stop](/index.php/Stop "Stop") and [disable](/index.php/Disable "Disable") `dnscrypt-proxy.service` and `dnscrypt-proxy.socket`.

Now [start/enable](/index.php/Start/enable "Start/enable") the new service(s), e.g., `dnscrypt-proxy@dnscrypt.eu-nl`, etc.

Finally [restart](/index.php/Restart "Restart") `unbound.service`.