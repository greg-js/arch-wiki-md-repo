[HAProxy](http://www.haproxy.org/) is a free, very fast and reliable solution offering high availability, load balancing, and proxying for TCP and HTTP-based applications. It is particularly suited for very high traffic web sites and powers quite a number of the world's most visited ones. Over the years it has become the de-facto standard opensource load balancer, is now shipped with most mainstream Linux distributions, and is often deployed by default in cloud platforms.

## Contents

*   [1 Installation](#Installation)
*   [2 Running](#Running)
*   [3 Configuration](#Configuration)
    *   [3.1 General configuration](#General_configuration)
        *   [3.1.1 ACLs](#ACLs)
        *   [3.1.2 Backends](#Backends)
        *   [3.1.3 Frontends](#Frontends)
        *   [3.1.4 Health checks](#Health_checks)
*   [4 See also](#See_also)

## Installation

Install the [haproxy](https://www.archlinux.org/packages/?name=haproxy) package from repositories.

## Running

Enable `haproxy.service` [using systemd](/index.php/Systemd#Using_units "Systemd"). HAProxy's configuration can be reloaded live using `# systemctl reload haproxy.service`.

## Configuration

An example configuration is available in `/etc/haproxy/haproxy.cfg`. Edit it to suit your needs, and then start `haproxy.service`.

### General configuration

#### ACLs

HAProxy supports ACLs, which can be used to test conditions and perform a given action based on the results of those tests. A typical ACL would be written as follows:

 `/etc/haproxy/haproxy.cfg` 
```
acl photo_page path_beg /photos

```

In this case, the ACL is matched if the user's request path begins with `/photos`.

#### Backends

In HAProxy terminology, **backends** are a server or set of servers that will receive forwarded requests. Backends can balance load based on several [load balancing algorithms](http://cbonte.github.io/haproxy-dconv/configuration-1.4.html#4.2-balance), including:

*   Round-robin
*   Static round-robin (also known as weighted round-robin)
*   Least connections

An example backend may be written as follows:

 `/etc/haproxy/haproxy.cfg` 
```
backend http-in
   balance roundrobin
   server s1 web1.example.com:80 check
   server s2 web2.example.com:80 check

```

#### Frontends

**Frontends** are used to define how requests should be forwarded to backends. They consist of the following:

*   IP addresses and ports
*   ACLs
*   *use_backend* rules

#### Health checks

When a backend is declared with the `check` option, HAProxy will check on startup and on scheduled intervals if the backend is available to process forwarded requests. If a backend fails the health check, it will be removed from rotation until it is deemed to be healthy again, i.e. it passes the health check.

By default, HAProxy will attempt to establish a TCP connection to the backend to determine healthiness.

If a large number of backends are declared with the `check` option, HAProxy will query all of them on startup, which may delay startup time.

## See also

*   [The official HAProxy website](http://www.haproxy.org/)
*   [Configuration guide](http://cbonte.github.io/haproxy-dconv/configuration-1.7.html)