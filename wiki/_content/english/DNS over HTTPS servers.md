Related articles

*   [DNS over HTTPS](/index.php/DNS_over_HTTPS "DNS over HTTPS")

DNS, since its inception, has been unencrypted on UDP/53, and later TCP/53, making it susceptible to snooping attacks. For additional information on the available protocols that can be used to address this vulnerability, see [Domain name resolution#Privacy and security](/index.php/Domain_name_resolution#Privacy_and_security "Domain name resolution"). This article covers two of the three available protocols for DNS servers with the necessary proxy configuration to provide both DNS over HTTPS (DoH) and DNS over TLS (DoT). Multiple DoH utilities are available in the AUR including [coredns](https://aur.archlinux.org/packages/coredns/), [dns-over-https](https://www.archlinux.org/packages/?name=dns-over-https), [doh-proxy](https://aur.archlinux.org/packages/doh-proxy/), and [python-doh-proxy](https://aur.archlinux.org/packages/python-doh-proxy/). Which of the available solutions is appropriate, depends on the needs of your network.

[coredns](https://aur.archlinux.org/packages/coredns/) provides both a caching, non-authoritative DNS server, and DoH services (citation needed).

[dns-over-https](https://www.archlinux.org/packages/?name=dns-over-https), [doh-proxy](https://aur.archlinux.org/packages/doh-proxy/), and [python-doh-proxy](https://aur.archlinux.org/packages/python-doh-proxy/) all provide an HTTP listener for proxying behind your existing HTTPS server, and a stub resolver to forward regular queries on UDP/53 to a secure DNS server. Additionally, both [doh-proxy](https://aur.archlinux.org/packages/doh-proxy/) and [python-doh-proxy](https://aur.archlinux.org/packages/python-doh-proxy/) provide a standalone HTTPS/2 server.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 DoH server/proxy software configuration](#DoH_server/proxy_software_configuration)
    *   [1.1 coreDNS](#coreDNS)
    *   [1.2 dns-over-https](#dns-over-https)
    *   [1.3 doh-proxy](#doh-proxy)
    *   [1.4 python-doh-proxy](#python-doh-proxy)
        *   [1.4.1 Stub resolver](#Stub_resolver)
        *   [1.4.2 DoH proxy](#DoH_proxy)
        *   [1.4.3 DoH proxy](#DoH_proxy_2)
*   [2 Standalone DNS server configuration](#Standalone_DNS_server_configuration)
    *   [2.1 Bind](#Bind)
    *   [2.2 Unbound](#Unbound)
*   [3 Web server configuration](#Web_server_configuration)
    *   [3.1 Apache httpd proxy configuration](#Apache_httpd_proxy_configuration)
    *   [3.2 nginx proxy configuration](#nginx_proxy_configuration)
*   [4 DNS over TLS configuration via stunnel](#DNS_over_TLS_configuration_via_stunnel)

## DoH server/proxy software configuration

### coreDNS

### dns-over-https

### doh-proxy

### python-doh-proxy

Install the following AUR packages (and their dependencies from the official repos): [python-aioh2](https://aur.archlinux.org/packages/python-aioh2/); [python-requests_download](https://aur.archlinux.org/packages/python-requests_download/); [install-wheel-scripts](https://aur.archlinux.org/packages/install-wheel-scripts/); [flit](https://aur.archlinux.org/packages/flit/); [python-aiohttp_remotes](https://aur.archlinux.org/packages/python-aiohttp_remotes/); and [python-doh-proxy](https://aur.archlinux.org/packages/python-doh-proxy/).

#### Stub resolver

If you intend to provide encrypted queries to your local network for legacy applications, configure the stub resolver:

 `/etc/conf.d/doh-stub` 
```
LISTENPORT=5353
ADDR=127.0.0.1
DOMAIN=mydomain.tld
NS=127.0.0.1
PORT=443
```

If you do not have a way to provide a secure forward DNS lookoup to your real DNS server, you should configure both DOMAIN and NS to use one of the upstream providers (CloudFlare, OpenDNS, etc., instead of localhost). If you only need to provide lookups to localhost, this is fine. If you need to provide them for the entire network, the you could listen on 53 directly if you do not have a local caching or authoritative DNS server - you would also want to use the real IP address instead of the loopback adapter in this case.

#### DoH proxy

If you have an existing HTTP server and wish to proxy DNS lookups with it, setup the HTTP proxy to listen on port 8080:

 `/etc/conf.d/doh-httpproxy` 
```
NS=127.0.0.1
PORT=8080
ADDR=127.0.0.1
```

Optionally, you can utilize either the doh-proxy service or an upstream DoH provider to forward queries.

#### DoH proxy

If you do not have an existing http server, you can configure the HTTPS/2 lisener:

 `/etc/conf.d/doh-proxy` 
```
NS=127.0.0.1
UPSTREAMPORT=5353
ADDR=127.0.0.1
LISTENPORT=443
CERT=/etc/ssl/private/fullchain.pem
KEY=/etc/ssl/private/privkey.pem
```

Again, adjust as necessary, but be certain that the upstream server has a way to perform secure queries, or you will be creating a loop.

## Standalone DNS server configuration

### Bind

Typical: If using ISC bind as the current DNS provider, and you will be providing both forwarding services for legacy clients and DoH to modern clients, you will likely want to configure named to forward all non-local queries to your stub resolver, comment out any forwarding lines an forward to the stub resolver (omit forward only if you would like to fall back to roots):

 `/etc/named.conf` 
```
options {
...
    //forwarders { 8.8.8.8; 8.8.4.4; };
    forwarders { 127.0.0.1 port 5353; };
    forward only;
...
};
...
```

If you want to forward to an external TLS proxy (via [stunnel](https://www.archlinux.org/packages/?name=stunnel)), do the same but use only TCP/54 (see stunnel configuration below):

 `/etc/named.conf` 
```
options {
...
    //forwarders { 8.8.8.8; 8.8.4.4; };
    forwarders { 127.0.0.1 port 54; };
    forward only;
...
};
...
server 127.0.0.1 {
    tcp-only yes;
};
...
```

Optional: If using ISC bind as the the current DNS provider, and you will be providing both forwarding services for legacy clients and DoH to modern clients, you might want to configure named to listen on an alternate port, for example TCP|UDP/54, rather than the default of 53 so that your stub resolver will listen on the standard port. Comment out any existing 'listen' lines and add the following (omit the v6 line if not needed):

 `/etc/named.conf` 
```
...
    //listen-on { any; };
    listen-on port 54 { any; };
    listen-on-v6 port 54 { any; };
...
```

### Unbound

## Web server configuration

### Apache httpd proxy configuration

Configure a proxy in your primary httpd.conf or appropriate vhost listening on 443:

 `/etc/httpd/conf/vhosts/**yourhost**.conf` 
```
...
    ProxyPass /dns-query http://[127.0.0.1]:8080/dns-query
    ProxyPassReverse /dns-query http://[127.0.0.1]:8080/dns-query
...

```

### nginx proxy configuration

Configure a proxy in your primary nginx.conf (or appropriate vhost configuration) listening on 443:

 `/etc/nginx.conf` 
```
...
        location /dns-query {
            proxy_pass http://localhost:8080/dns-query;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
...
```

## DNS over TLS configuration via stunnel

Configure stunnel to listen on TCP/853 for TLS connections, and forward to your local DNS provider:

 `/etc/stunnel/conf.d/DoT.conf` 
```
[dns]
accept = 853
connect = 127.0.0.1:53
cert = /etc/ssl/private/fullchain.pem
key = /etc/ssl/private/privkey.pem
```

Configure stunnel to listen on TCP/54 and forward to an upstream secure provider:

 `/etc/stunnel/conf.d/DoT-Remote.conf` 
```
[dnsovertls]
client = yes
accept = 54
connect = 10.10.10.1:853
verifyChain = yes
CAPath = /etc/ssl/certs
checkHost = <your_host_name>
```