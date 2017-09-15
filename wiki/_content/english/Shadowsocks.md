[Shadowsocks](http://shadowsocks.org) is a lightweight socks5 proxy, Originally written in Python.

## Contents

*   [1 Installation](#Installation)
*   [2 Setup](#Setup)
    *   [2.1 Client](#Client)
        *   [2.1.1 From the command line](#From_the_command_line)
        *   [2.1.2 Using systemd](#Using_systemd)
        *   [2.1.3 GUI client](#GUI_client)
    *   [2.2 Server](#Server)
        *   [2.2.1 From the command line](#From_the_command_line_2)
        *   [2.2.2 Using systemd](#Using_systemd_2)
    *   [2.3 Encryption](#Encryption)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the package [shadowsocks-libev](https://www.archlinux.org/packages/?name=shadowsocks-libev) or [shadowsocks](https://www.archlinux.org/packages/?name=shadowsocks).

## Setup

Shadowsocks configuration may be done with a JSON formatted file. The following example configuration is included in the package:

 `/etc/shadowsocks/example.json` 
```
{
    "server":"my_server_ip",
    "server_port":8388,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"mypassword",
    "timeout":300,
    "method":"chacha20-ietf-poly1305",
    "fast_open": false,
    "workers": 1
}

```

**Tip:** To specify multiple server IPs, the following syntax can be used `"server":["1.1.1.1","2.2.2.2"],`

**Tip:** To find out the fastest method running on your machine, you can benchmark with the script[[1]](https://github.com/shadowsocks/shadowsocks-libev/blob/0437e05aa8ec7f36f1eeb8c366dfd2b2b3b0288b/scripts/iperf.sh)

| Name | Explanation |
| server | the address your server listens |
| server_port | server port |
| local_address | the address your local listens |
| local_port | local port |
| password | password used for encryption |
| timeout | in seconds |
| method | see [Encryption](https://github.com/shadowsocks/shadowsocks/wiki/Encryption) |
| fast_open | use [TCP-Fast-Open](https://github.com/clowwindy/shadowsocks/wiki/TCP-Fast-Open), true / false |
| workers | number of workers |

### Client

**Warning:** The [udns](https://www.archlinux.org/packages/?name=udns) package is used as a stub resolver for DNS. In order to prevent DNS request leaking of client applications (like browsers), further applications must be employed. For example, [privoxy](/index.php/Privoxy "Privoxy") or a full DNS resolver on the client.[[2]](https://github.com/shadowsocks/shadowsocks-libev/issues/1542) [[3]](https://github.com/shadowsocks/shadowsocks-libev/issues/1641)

#### From the command line

The client is started with the `ss-local` command. To start it using the configuration file `/etc/shadowsocks/config.json`:

```
$ ss-local -c /etc/shadowsocks/config.json

```

Alternatively, the configuration may be specified directly on the command:

```
$ ss-local -s *server_address* -p *server_port* -l *local_port* -k *password* -m *encryption_method*

```

To use verbose log, add `-v` to the command:

```
$ ss-local -s *server_address* -p *server_port* -l *local_port* -k *password* -m *encryption_method* -v

```

#### Using systemd

The Shadowsocks client can be controlled with an instance of `shadowsocks@.service`.

For example, to [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the service using the configuration file `/etc/shadowsocks/config.json`, use the service `shadowsocks-libev@config.service`.

#### GUI client

Install [shadowsocks-qt5](https://www.archlinux.org/packages/?name=shadowsocks-qt5).

### Server

#### From the command line

The server is started with the `ss-server`(shadowsocks-libev) or `ssserver`(shadowsocks) command.

To start it in the foreground using the configuration file `/etc/shadowsocks/config.json`:

shadowsocks-libev

```
$ ss-server -c /etc/shadowsocks/config.json

```

shadowsocks

```
$ ssserver -c /etc/shadowsocks/config.json

```

To run in the background:

shadowsocks-libev

```
$ ss-server -c /etc/shadowsocks/config.json -d start
$ ss-server -c /etc/shadowsocks/config.json -d stop

```

shadowsocks

```
$ ssserver -c /etc/shadowsocks/config.json -d start
$ ssserver -c /etc/shadowsocks/config.json -d stop

```

#### Using systemd

The Shadowsocks server can be controlled with an instance of `shadowsocks-server@.service`.

For example, to [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the service using the configuration file `/etc/shadowsocks/config.json`, use the service `shadowsocks-libev-server@config.service`(shadowsocks-libev) or `shadowsocks-server@config.service`(shadowsocks).

To bind Shadowsocks to a privileged port (less than 1024), the server should be started as user root:

 `/etc/systemd/system/shadowsocks-server@.service.d/start-as-root.conf` 
```
[Service]
User=root

```

### Encryption

Installing the [python2-m2crypto](https://www.archlinux.org/packages/?name=python2-m2crypto) package will make encryption a little faster.

To use [Salsa20](https://en.wikipedia.org/wiki/Salsa20 "wikipedia:Salsa20") or *ChaCha20* cyphers, install the [libsodium](https://www.archlinux.org/packages/?name=libsodium) package.

## See also

*   [Shadowsocks website](http://shadowsocks.org)
*   [Python package](https://pypi.python.org/pypi/shadowsocks)
*   [GitHub wiki](https://github.com/shadowsocks/shadowsocks/wiki)
*   [Backup GitHub project](https://github.com/shadowsocks-backup/shadowsocks) (the original project has been "removed according to regulations" in August 2015)