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
        *   [3.3.1 Add new forward address](#Add_new_forward_address)
        *   [3.3.2 Create instanced systemd service](#Create_instanced_systemd_service)
        *   [3.3.3 Add first dnscrypt-socket](#Add_first_dnscrypt-socket)
        *   [3.3.4 Add additional dyscrypt-sockets](#Add_additional_dyscrypt-sockets)
        *   [3.3.5 Apply new systemd configuration](#Apply_new_systemd_configuration)
*   [4 Known issues](#Known_issues)
    *   [4.1 dnscrypt runs with root privileges](#dnscrypt_runs_with_root_privileges)

## Installation

[Install](/index.php/Install "Install") the [dnscrypt-proxy](https://www.archlinux.org/packages/?name=dnscrypt-proxy) package.

## Configuration

Select a resolver from `/usr/share/dnscrypt-proxy/dnscrypt-resolvers.csv` and [edit](/index.php/Systemd#Editing_provided_units "Systemd") `dnscrypt-proxy.service`, using the first column as the name of the resolver with the `-R` flag. For example, to select *dnscrypt.eu-nl* as the resolver, the drop-in file would look like this:

```
[Service]
ExecStart=
ExecStart=/usr/bin/dnscrypt-proxy -R dnscrypt.eu-nl

```

**Tip:** A potentially more up-to-date list is available directly on the [upstream page](https://github.com/jedisct1/dnscrypt-proxy/blob/master/dnscrypt-resolvers.csv).

After selecting a dnscrypt resolver, modify the [resolv.conf](/index.php/Resolv.conf "Resolv.conf") file and replace the current set of resolver addresses with address for *localhost*:

```
nameserver 127.0.0.1

```

Other programs may overwrite this setting; see [resolv.conf#Preserve DNS settings](/index.php/Resolv.conf#Preserve_DNS_settings "Resolv.conf") for details.

Finally, [start and enable](/index.php/Enable "Enable") the `dnscrypt-proxy.service`.

## Tips and tricks

### DNSCrypt as a forwarder for local DNS cache

It is recommended to run DNSCrypt as a forwarder for a local DNS cache, otherwise every single query will make a round-trip to the upstream resolver. Any local DNS caching program should work, examples below show configuration for [Unbound](/index.php/Unbound "Unbound"), [dnsmasq](/index.php/Dnsmasq "Dnsmasq"), and [pdnsd](/index.php/Pdnsd "Pdnsd").

First configure *dnscrypt-proxy* to listen on a port different from the default `53`, since the DNS cache needs to listen on `53` and query *dnscrypt-proxy* on a different port. Port number `40` is used as an example in this section:

 `# systemctl edit dnscrypt-proxy.socket` 
```
[Socket]
ListenStream=
ListenDatagram=
ListenStream=127.0.0.1:40
ListenDatagram=127.0.0.1:40
```

**Note:** The `ListenStream` and `ListenDatagram` options need to be cleared with empty assignment before overriding, otherwise the new address would be *added* to the list of sockets. See [systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd") for details.

Then restart `dnscrypt-proxy.socket` and *stop* `dnscrypt-proxy.service` if already running to let it be started by the *.socket* unit.

#### Example: configuration for Unbound

Configure [Unbound](/index.php/Unbound "Unbound") to your liking (in particular, see [Unbound#Local DNS server](/index.php/Unbound#Local_DNS_server "Unbound")) and add the following lines to the end of the `server` section in `/etc/unbound/unbound.conf`:

```
do-not-query-localhost: no
forward-zone:
  name: "."
  forward-addr: 127.0.0.1@40

```

**Tip:** If you are setting up a server, add `interface: 0.0.0.0@53` and `access-control: *your-network*/*subnet-mask* allow` inside the `server:` section so that the other computers can connect to the server. A client must be configured with `nameserver *address-of-your-server*` in `/etc/resolv.conf`.

[Restart](/index.php/Restart "Restart") `unbound.service` to apply the changes.

#### Example: configuration for dnsmasq

Configure dnsmasq as a [local DNS cache](/index.php/Dnsmasq#DNS_cache_setup "Dnsmasq"). The basic configuration to work with DNSCrypt:

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

You may also wish to add the following argument to *dnscrypt-proxy*:

```
--edns-payload-size=<bytes>

```

The default size being **1252** bytes, with values up to **4096** bytes being purportedly safe. A value below or equal to **512** bytes will disable this mechanism, unless a client sends a packet with an OPT section providing a payload size.

#### Test EDNS0

Make use of the [DNS Reply Size Test Server](https://www.dns-oarc.net/oarc/services/replysizetest), use the *dig* command line tool from the [bind-tools](https://www.archlinux.org/packages/?name=bind-tools) package to issue a TXT query for the name *rs.dns-oarc.net*:

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

#### Add new forward address

**Note:** Obtaining redundancy requires a simple edit to the above Unbound example and the addition of a second instance of the dnscrypt-proxy and service. Please be sure that the above Unbound example is working prior to proceeding, as this tip extends the previous example.

Extend the previous [Unbound](/index.php/Unbound "Unbound") configuration in `/etc/unbound/unbound.conf` to include an additional forward address that uses a different port. Port 41 is used in the below example:

```
do-not-query-localhost: no
forward-zone:
  name: "."
  forward-addr: 127.0.0.1@40
  forward-addr: 127.0.0.1@41

```

#### Create instanced systemd service

We will use an instanced systemd service to accomplish this. This will use one `dnscrypt-proxy@.service` systemd service to handle as many distinct DNSCrypt resolves as we want.

First, we need `/etc/systemd/system/dnscrypt-proxy@.service` containing:

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

#### Add first dnscrypt-socket

You can now create two (or more!) socket files, specifying different DNSCrypt providers.

For the first dnscrypt-proxy socket, listening on 127.0.0.1@40 and connecting to the example dnscrypt.eu-nl provider, copy `/lib/systemd/system/dnscrypt-proxy.socket` to `/etc/systemd/system/dnscrypt-proxy@dnscrypt.eu-nl.socket`.

#### Add additional dyscrypt-sockets

For the second (or more) dnscrypt-proxy socket, copy `/lib/systemd/system/dnscrypt-proxy.socket` to eg. `/etc/systemd/system/dnscrypt-proxy@cloudns-syd.socket`

Here you can replace the socket instance name to eg. **cloudns-syd** as one of those listed in `providers name` column in `/usr/share/dnscrypt-proxy/dnscrypt-resolvers.csv` and edit it to eg. port 41 and so forth.

```
 [Unit]
 Description=dnscrypt-proxy-secondary listening socket

 [Socket]
 ListenStream=127.0.0.1:41
 ListenDatagram=127.0.0.1:41

 [Install]
 WantedBy=sockets.target

```

#### Apply new systemd configuration

Now we need to reload the systemd configuration.

```
# systemctl daemon-reload

```

Since we are replacing the default service with a different name, we need to explicitly [stop](/index.php/Stop "Stop") and [disable](/index.php/Disable "Disable") `dnscrypt-proxy` and `dnscrypt-proxy.socket`.

Now [start/enable](/index.php/Start/enable "Start/enable") the new sockets, `dnscrypt-proxy@dnscrypt.eu-nl.socket` and `dnscrypt-proxy@cloudns-syd.socket`.

Finally [restart](/index.php/Restart "Restart") `unbound.service`

## Known issues

### dnscrypt runs with root privileges

See [FS#49881](https://bugs.archlinux.org/task/49881). To work around this, create an unprivileged user manually.

[Create the user](/index.php/Users_and_groups#User_management "Users and groups") as follows:

```
# useradd -r -d /var/dnscrypt -m -s /sbin/nologin dnscrypt

```

[Edit](/index.php/Systemd#Editing_provided_units "Systemd") `dnscrypt-proxy.service`, pointing `--user` to the new user:

```
[Service]
ExecStart=
ExecStart=/usr/bin/dnscrypt-proxy -R dnscrypt.eu-nl --user=dnscrypt

```