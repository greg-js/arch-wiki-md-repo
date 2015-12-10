# HTTP tunneling

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

In networking, tunneling is using a protocol of higher level (in our case HTTP) to transport a lower level protocol (in our case TCP).

## Contents

*   [1 Creating the tunnel](#Creating_the_tunnel)
    *   [1.1 Using corscrew and HTTP CONNECT](#Using_corscrew_and_HTTP_CONNECT)
        *   [1.1.1 Tunneling Git](#Tunneling_Git)
    *   [1.2 Using httptunnel](#Using_httptunnel)
    *   [1.3 Using proxytunnel](#Using_proxytunnel)
    *   [1.4 Using openbsd-netcat](#Using_openbsd-netcat)
*   [2 Using the tunnel](#Using_the_tunnel)

## Creating the tunnel

### Using corscrew and HTTP CONNECT

To open the connection to the server running the SSH daemon we will use the HTTP CONNECT method which allows a client to connect to a server through an HTTP proxy by sending an HTTP CONNECT request to this proxy.

**Note:** If your proxy does not support the HTTP Connect method, see the other methods below.

For this we will use [corkscrew](http://www.agroman.net/corkscrew/), a tool for tunneling SSH through HTTP proxies available in the [official repositories](/index.php/Official_repositories "Official repositories") as [corkscrew](https://www.archlinux.org/packages/?name=corkscrew).

Opening an SSH connection is pretty simple:

```
ssh user@server -o "ProxyCommand corkscrew `$proxy_ip_or_domain_name $proxy_port $destination_ip_or_domain_name $destination_port`"

```

but that just opens a shell yet what we want is a SOCKS tunnel, so we do this:

```
ssh -ND `$port` user@server -o "ProxyCommand corkscrew `$proxy_ip_or_domain_name $proxy_port $destination_ip_or_domain_name $destination_port`"

```

which creates a [SOCKS](https://en.wikipedia.org/wiki/SOCKS "wikipedia:SOCKS") proxy on `localhost:$port`.

#### Tunneling Git

Restrictive corporate firewalls typically block the port that [git](/index.php/Git "Git") uses. However, git can be made to tunnel through HTTP proxies using utilities such as corkscrew. When git sees the environment variable `GIT_PROXY_COMMAND` set, it will run the command in `$GIT_PROXY_COMMAND` and use that program's stdin and stdout, instead of a network socket.

Create a script file `corkscrewtunnel.sh`

```
#! /bin/bash

corkscrew _proxyhost_ _proxyport_ $*

```

Set `GIT_PROXY_COMMAND`

```
export GIT_PROXY_COMMAND=_path-to-corkscrewtunnel.sh_

```

Now, git should be able to tunnel successfully through the HTTP proxy.

### Using httptunnel

[httptunnel](http://www.nocrew.org/software/httptunnel.html), available in the [official repositories](/index.php/Official_repositories "Official repositories") as [httptunnel](https://www.archlinux.org/packages/?name=httptunnel), creates a bidirectional virtual data connection tunneled in HTTP requests. The HTTP requests can be sent via an HTTP proxy if so desired. This can be useful for users behind restrictive firewalls. If WWW access is allowed through a HTTP proxy, it's possible to use httptunnel and, say, telnet or PPP to connect to a computer outside the firewall.

If you already have a web server listening on port 80 you are probably going to want to create a virtual host and tell your web server to proxy request to the hts server. This is not covered here.

If you do not have any web server listening on port 80 you can do:

*   on the server:

```
hts --forward-port localhost:22 80

```

*   on the client:

```
htc --forward-port 8888 example.net:80
ssh -ND user@localhost -p 8888

```

**Note:** As SSH thinks it is connecting to localhost it will not recognize the fingerprint and display a warning.

You can now use `localhost:8888` as a [SOCKS](http://en.wikipedia.org/wiki/SOCKS) proxy.

### Using proxytunnel

[Install](/index.php/Install "Install") the [proxytunnel](https://www.archlinux.org/packages/?name=proxytunnel) package from the [official repositories](/index.php/Official_repositories "Official repositories").

```
$ ProxyCommand /usr/bin/proxytunnel -p some-proxy:8080 -d www.muppetzone.com:443

```

### Using openbsd-netcat

[Install](/index.php/Install "Install") the [openbsd-netcat](https://www.archlinux.org/packages/?name=openbsd-netcat) package from the [official repositories](/index.php/Official_repositories "Official repositories").

To open a connection using the openbsd netcat version:

```
$ ssh user@final_server -o "ProxyCommand=nc -X connect -x some-proxy:$proxy_port %h %p"

```

## Using the tunnel

See [Using a SOCKS proxy](/index.php/Using_a_SOCKS_proxy "Using a SOCKS proxy").

Retrieved from "[https://wiki.archlinux.org/index.php?title=HTTP_tunneling&oldid=408506](https://wiki.archlinux.org/index.php?title=HTTP_tunneling&oldid=408506)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Networking](/index.php/Category:Networking "Category:Networking")
*   [Secure Shell](/index.php/Category:Secure_Shell "Category:Secure Shell")