[Shadowsocks](http://shadowsocks.org) is a lightweight socks5 proxy, written in python.

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

[Install](/index.php/Install "Install") the [shadowsocks](https://www.archlinux.org/packages/?name=shadowsocks) package.

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
    "method":"aes-256-cfb",
    "fast_open": false,
    "workers": 1
}

```

**Tip:** To specify multiple server IPs, the following syntax can be used `"server":["1.1.1.1","2.2.2.2"],`

| Name | Explanation |
| server | the address your server listens |
| server_port | server port |
| local_address | the address your local listens |
| local_port | local port |
| password | password used for encryption |
| timeout | in seconds |
| method | default: "aes-256-cfb", see [Encryption](https://github.com/shadowsocks/shadowsocks/wiki/Encryption) |
| fast_open | use [TCP-Fast-Open](https://github.com/clowwindy/shadowsocks/wiki/TCP-Fast-Open), true / false |
| workers | number of workers |

To adjust the logging level, the option `"verbose": *value*` may be added, with one of the following value:

*   2: full logging
*   1: debug
*   0: default
*   -1: warnings
*   -2: errors

### Client

#### From the command line

The client is started with the `sslocal` command. To start it using the configuration file `/etc/shadowsocks/config.json`:

```
$ sslocal -c /etc/shadowsocks/config.json

```

Alternatively, the configuration may be specified directly on the command:

```
$ sslocal -s *server_address* -p *server_port* -l *local_port* -k *password* -m *encryption_method*

```

#### Using systemd

The Shadowsocks client can be controlled with an instance of `shadowsocks@.service`.

For example, to [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the service using the configuration file `/etc/shadowsocks/config.json`, use the service `shadowsocks@config.service`.

#### GUI client

Install [shadowsocks-qt5](https://aur.archlinux.org/packages/shadowsocks-qt5/).

### Server

#### From the command line

The server is started with the `ssserver` command.

To start it in the foreground using the configuration file `/etc/shadowsocks/config.json`:

```
$ ssserver -c /etc/shadowsocks/config.json

```

To run in the background:

```
$ ssserver -c /etc/shadowsocks/config.json -d start
$ ssserver -c /etc/shadowsocks/config.json -d stop
```

#### Using systemd

The Shadowsocks server can be controlled with an instance of `shadowsocks-server@.service`.

For example, to [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the service using the configuration file `/etc/shadowsocks/config.json`, use the service `shadowsocks-server@config.service`.

To bind Shadowsocks to a privileged port (less than 1024), the server should be started as user root:

 `/etc/systemd/system/shadowsocks-server@.service.d/start-as-root.conf` 
```
[Service]
User=root

```

### Encryption

Installing the [python2-m2crypto](https://www.archlinux.org/packages/?name=python2-m2crypto) package will make encryption a little faster.

To use [Salsa20](https://en.wikipedia.org/wiki/Salsa20) or *ChaCha20* cyphers, install the [libsodium](https://www.archlinux.org/packages/?name=libsodium) package.

## See also

*   [Shadowsocks website](http://shadowsocks.org)
*   [Python package](https://pypi.python.org/pypi/shadowsocks)
*   [GitHub wiki](https://github.com/shadowsocks/shadowsocks/wiki)
*   [Backup GitHub project](https://github.com/shadowsocks-backup/shadowsocks) (the original project has been "removed according to regulations" in August 2015)