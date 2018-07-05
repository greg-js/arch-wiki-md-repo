[Trojan](https://trojan-gfw.github.io/trojan/) is an unidentifiable mechanism that helps you bypass GFW. It consists of a proxy client and a [proxy server](https://en.wikipedia.org/wiki/Proxy_server "wikipedia:Proxy server").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Client](#Client)
    *   [2.2 Server](#Server)
        *   [2.2.1 TLS Certificate](#TLS_Certificate)
        *   [2.2.2 TCP Fast Open](#TCP_Fast_Open)
        *   [2.2.3 Disguise](#Disguise)
*   [3 Running](#Running)
    *   [3.1 Systemd Service](#Systemd_Service)
    *   [3.2 Manually](#Manually)
*   [4 See also](#See_also)

## Installation

Trojan can be [installed](/index.php/Install "Install") with the [trojan](https://www.archlinux.org/packages/?name=trojan) package.

## Configuration

Trojan cannot run without proper configuration. It uses [JSON](https://en.wikipedia.org/wiki/JSON "wikipedia:JSON") as its config format. All configuration work is done in `/etc/trojan/`. Detailed explanations of each field of the config file can be found [here](https://trojan-gfw.github.io/trojan/config). A convenient config generator is right [here](https://trojan-gfw.github.io/trojan-config-gen/).

### Client

An example of client config:

 `/etc/trojan/config.json` 
```
{
    "run_type": "client",
    "local_addr": "127.0.0.1",
    "local_port": 1080,
    "remote_addr": "example.com",
    "remote_port": 443,
    "password": ["password1"],
    "append_payload": true,
    "log_level": 1,
    "ssl": {
        "verify": true,
        "verify_hostname": true,
        "cert": "",
        "cipher": "ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES128-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA:AES128-SHA:AES256-SHA:DES-CBC3-SHA",
        "sni": "example.com",
        "alpn": [
            "h2",
            "http/1.1"
        ],
        "reuse_session": true,
        "curves": "",
        "sigalgs": ""
    },
    "tcp": {
        "keep_alive": true,
        "no_delay": true,
        "fast_open": true,
        "fast_open_qlen": 5
    }
}

```

### Server

An example of server config:

 `/etc/trojan/config.json` 
```
{
    "run_type": "server",
    "local_addr": "0.0.0.0",
    "local_port": 443,
    "remote_addr": "127.0.0.1",
    "remote_port": 80,
    "password": [
        "password1",
        "password2"
    ],
    "log_level": 1,
    "ssl": {
        "cert": "/path/to/certificate.crt",
        "key": "/path/to/private.key",
        "key_password": "",
        "cipher": "ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES256-SHA:ECDHE-ECDSA-DES-CBC3-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:DES-CBC3-SHA:!DSS",
        "prefer_server_cipher": true,
        "alpn": [
            "http/1.1"
        ],
        "reuse_session": true,
        "session_timeout": 300,
        "curves": "",
        "sigalgs": "",
        "dhparam": ""
    },
    "tcp": {
        "keep_alive": true,
        "no_delay": true,
        "fast_open": true,
        "fast_open_qlen": 5
    }
}

```

#### TLS Certificate

You'll need to provide a [TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security "wikipedia:Transport Layer Security") certificate and private key for trojan to work. You can either apply for a free certificate with [Let's Encrypt](https://letsencrypt.org/) or generate a self-signed one **(NOT RECOMMENDED)** in [this](https://www.ibm.com/support/knowledgecenter/en/SSWHYP_4.0.0/com.ibm.apimgmt.cmc.doc/task_apionprem_gernerate_self_signed_openSSL.html) way. Then, set the `cert`, `key`, and `key_password` fields in the config accordingly.

#### TCP Fast Open

For [TCP Fast Open](https://en.wikipedia.org/wiki/TCP_Fast_Open "wikipedia:TCP Fast Open") on servers to work, you'll need to turn it on in your OS:

```
# echo 3 > /proc/sys/net/ipv4/tcp_fastopen

```

#### Disguise

Trojan servers can be disguised as other services over TLS to prevent active probing. This can be done by, for example, running a [web server](https://en.wikipedia.org/wiki/Web_server "wikipedia:Web server") with [nginx](/index.php/Nginx "Nginx") and pointing `remote_addr` and `remote_port` fields to the server address and port.

## Running

### Systemd Service

Trojan can be controlled with `trojan.service` and `trojan@.service`. For example, to [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") trojan with config file `/etc/trojan/xxx.json`, you can run:

```
# systemctl start trojan@xxx
# systemctl enable trojan@xxx

```

Running

```
# systemctl start trojan
# systemctl enable trojan

```

will [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") trojan with `/etc/trojan/config.json`.

### Manually

Trojan can also start in a shell, by running:

```
$ trojan /etc/trojan/config.json

```

You can replace `/etc/trojan/config.json` with any other config files. Note that trojan outputs its log to [stderr](https://en.wikipedia.org/wiki/Standard_streams#Standard_error_.28stderr.29 "wikipedia:Standard streams"), so you'll have to redirect it to a file if you want to keep the log.

## See also

[GitHub Project](https://github.com/trojan-gfw/trojan)