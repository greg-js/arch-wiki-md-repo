[Trojan](https://trojan-gfw.github.io/trojan/) is an unidentifiable mechanism that helps you bypass the Great Firewall of China. It consists of a proxy client and a [proxy server](https://en.wikipedia.org/wiki/Proxy_server "wikipedia:Proxy server").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 TLS Certificate](#TLS_Certificate)
    *   [2.2 TCP Fast Open](#TCP_Fast_Open)
    *   [2.3 Disguise](#Disguise)
*   [3 Running](#Running)
    *   [3.1 Systemd Service](#Systemd_Service)
    *   [3.2 Manually](#Manually)
*   [4 See also](#See_also)

## Installation

Trojan can be [installed](/index.php/Install "Install") with the [trojan](https://www.archlinux.org/packages/?name=trojan) or [trojan-git](https://aur.archlinux.org/packages/trojan-git/) package.

## Configuration

Trojan cannot run without proper configuration. It uses [JSON](https://en.wikipedia.org/wiki/JSON "wikipedia:JSON") as its config format. All configuration work is done in `/etc/trojan/`. Detailed explanations of each field of the config file can be found [here](https://trojan-gfw.github.io/trojan/config). A convenient config generator is right [here](https://trojan-gfw.github.io/trojan-config-gen/).

Examples of client and server configuration are at `/usr/share/doc/trojan/examples/client.json-example` and `/usr/share/doc/trojan/examples/server.json-example`.

### TLS Certificate

You'll need to provide a [TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security "wikipedia:Transport Layer Security") certificate and private key for trojan servers to work. You can either apply for a free certificate with [Let's Encrypt](https://letsencrypt.org/) or generate a self-signed one in [this](https://www.ibm.com/support/knowledgecenter/en/SSWHYP_4.0.0/com.ibm.apimgmt.cmc.doc/task_apionprem_gernerate_self_signed_openSSL.html) way. Then, set the `cert`, `key`, and `key_password` fields in the config accordingly. Note that you should pin the certificate by setting `cert` on the client if you generate a self-signed certificate.

### TCP Fast Open

For [TCP Fast Open](https://en.wikipedia.org/wiki/TCP_Fast_Open "wikipedia:TCP Fast Open") on servers to work, you'll need to turn it on in your OS:

```
# echo 3 > /proc/sys/net/ipv4/tcp_fastopen

```

### Disguise

Trojan servers can be disguised as other services over TLS to prevent active probing. This can be done by, for example, running a [web server](/index.php/Web_server "Web server") with [nginx](/index.php/Nginx "Nginx") and pointing `remote_addr` and `remote_port` fields to the server address and port.

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