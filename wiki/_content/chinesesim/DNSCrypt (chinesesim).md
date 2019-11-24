**翻译状态：** 本文是英文页面 [DNSCrypt](/index.php/DNSCrypt "DNSCrypt") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-06-30，点击[这里](https://wiki.archlinux.org/index.php?title=DNSCrypt&diff=0&oldid=525116)可以查看翻译后英文页面的改动。

[dnscrypt-proxy](https://github.com/jedisct1/dnscrypt-proxy) 可以加密和认证用户和 DNS 解析服务器之间的数据传输，支持 [DNS over HTTPS](https://en.wikipedia.org/wiki/DNS_over_HTTPS "wikipedia:DNS over HTTPS") 和 [DNSCrypt](https://dnscrypt.info/)，可以避免中间人攻击和窃听。*dnscrypt-proxy* 兼容 [DNSSEC](/index.php/DNSSEC "DNSSEC")。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 启动](#启动)
    *   [2.2 选择解析服务器](#选择解析服务器)
    *   [2.3 禁用其他占用53端口的服务](#禁用其他占用53端口的服务)
    *   [2.4 修改 resolv.conf](#修改_resolv.conf)
    *   [2.5 启动 systemd 服务](#启动_systemd_服务)
*   [3 技巧](#技巧)
    *   [3.1 本地 DNS 缓存配置](#本地_DNS_缓存配置)
        *   [3.1.1 修改端口](#修改端口)
        *   [3.1.2 本地 DNS 缓存配置举例](#本地_DNS_缓存配置举例)
            *   [3.1.2.1 Unbound](#Unbound)
            *   [3.1.2.2 dnsmasq](#dnsmasq)
            *   [3.1.2.3 pdnsd](#pdnsd)
    *   [3.2 沙盒隔离](#沙盒隔离)
    *   [3.3 启用 EDNS0](#启用_EDNS0)
        *   [3.3.1 测试 EDNS0](#测试_EDNS0)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [dnscrypt-proxy](https://www.archlinux.org/packages/?name=dnscrypt-proxy)。

## 配置

### 启动

服务有两种启动方式，但是只能二选一：

*   启用 `.service`

**注意:** 必须指定 `listen_addresses` (即在配置文件中写好 `listen_addresses = ['127.0.0.1:53', '[::1]:53']`)

*   启用 `.socket`

**注意:** 必须留空 `listen_addresses` (即 `listen_addresses = [ ]`)，systemd 会自己配置好 socket

### 选择解析服务器

By leaving `server_names` commented out in the configuration file `/etc/dnscrypt-proxy/dnscrypt-proxy.toml`, *dnscrypt-proxy* will choose the fastest server from the sources already configured under `[sources]` [[1]](https://github.com/jedisct1/dnscrypt-proxy/wiki/Configuration#an-example-static-server-entry). The lists will be downloaded, verified, and automatically updated. [[2]](https://github.com/jedisct1/dnscrypt-proxy/wiki/Configuration-Sources#what-is-the-point-of-these-lists). Thus, configuring a specific set of servers is optional.

To manually set which server is used, edit `/etc/dnscrypt-proxy/dnscrypt-proxy.toml` and uncomment the `server_names` variable, selecting one or more of the servers. For example, to use Cloudflare's servers:

```
server_names = ['cloudflare', 'cloudflare-ipv6']

```

A full list of resolvers is located at the [upstream page](https://download.dnscrypt.info/resolvers-list/v2/public-resolvers.md) or [Github](https://raw.githubusercontent.com/DNSCrypt/dnscrypt-resolvers/master/v2/public-resolvers.md). If *dnscrypt-proxy* has run successfully on the system before, `/var/cache/dnscrypt-proxy/public-resolvers.md` will also contain a list. Look at the description for servers note which validate [DNSSEC](/index.php/DNSSEC "DNSSEC"), do not log, and are uncensored. These requirements can be configured globally with the `require_dnssec`, `require_nolog`, `require_nofilter` options.

### 禁用其他占用53端口的服务

**提示：** 如果使用 [#Unbound](#Unbound) 提供本地 DNS 缓存，请跳过这一节，因为 *unbound* 默认监听 53。

查看占用 53 端口的服务：

```
 $ ss -lp 'sport = :domain'

```

如果输出除了表头还有其他内容，你就需要禁用占用53端口的那些服务，比如 `systemd-resolved.service` 和其他网络管理器包含的类似服务。把它们全部干掉，直到上面的命令的输出只剩这个样子：

```
 Netid               State                 Recv-Q                Send-Q                     Local Address:Port                                   Peer Address:Port

```

### 修改 resolv.conf

修改 [resolv.conf](/index.php/Resolv.conf "Resolv.conf")，把现有的`nameserver`全部清掉，添一行指向 *localhost* 的地址（一般是 127.0.0.1）的`nameserver`；并增添一行 *options* [[3]](https://github.com/jedisct1/dnscrypt-proxy/wiki/Installation-linux#step-4-change-the-system-dns-settings)。示例如下：

```
nameserver 127.0.0.1
options edns0 single-request-reopen

```

其他程序可能会修改 resolv.conf，详见：[resolv.conf#Overwriting of /etc/resolv.conf](/index.php/Resolv.conf#Overwriting_of_/etc/resolv.conf "Resolv.conf")。

### 启动 systemd 服务

根据上面你选择的[配置](#启动)来 [start/enable](/index.php/Start/enable "Start/enable") `dnscrypt-proxy.service` 或者 `dnscrypt-proxy.socket`

## 技巧

### 本地 DNS 缓存配置

**Tip:** *dnscrypt* can cache entries without relying on another program. This feature is enabled by default with the line `cache = true` in your dnscrypt configuration file

It is recommended to run DNSCrypt as a forwarder for a local DNS cache if not using *dnscrypt's* cache feature; otherwise, every single query will make a round-trip to the upstream resolver. Any local DNS caching program should work. In addition to setting up *dnscrypt-proxy*, you must setup your local DNS cache program.

#### 修改端口

In order to forward queries from a local DNS cache, *dnscrypt-proxy* should listen on a port different from the default `53`, since the DNS cache itself needs to listen on `53` and query *dnscrypt-proxy* on a different port. Port number `53000` is used as an example in this section. In this example, the port number is larger than 1024 so *dnscrypt-proxy* is not required to be run by root.

There are two methods for changing the default port:

**Socket method**

[Edit](/index.php/Edit "Edit") `dnscrypt-proxy.socket` with the following contents:

```
[Socket]
ListenStream=
ListenDatagram=
ListenStream=127.0.0.1:53000
ListenDatagram=127.0.0.1:53000

```

When queries are forwarded from the local DNS cache to `53000`, `dnscrypt-proxy.socket` will start `dnscrypt-proxy.service`.

**Service method**

Edit the `listen_addresses` option in `/etc/dnscrypt-proxy/dnscrypt-proxy.toml` with the following:

```
listen_addresses = ['127.0.0.1:53000', '[::1]:53000']

```

#### 本地 DNS 缓存配置举例

The following configurations should work with *dnscrypt-proxy* and assume that it is listening on port `53000`.

##### Unbound

Configure [Unbound](/index.php/Unbound "Unbound") to your liking (in particular, see [Unbound#Local DNS server](/index.php/Unbound#Local_DNS_server "Unbound")) and add the following lines to the end of the `server` section in `/etc/unbound/unbound.conf`:

```
  do-not-query-localhost: no
forward-zone:
  name: "."
  forward-addr: 127.0.0.1@53000

```

**Tip:** If you are setting up a server, add `interface: 0.0.0.0@53` and `access-control: *your-network*/*subnet-mask* allow` inside the `server:` section so that the other computers can connect to the server. A client must be configured with `nameserver *address-of-your-server*` in `/etc/resolv.conf`.

[Restart](/index.php/Restart "Restart") `unbound.service` to apply the changes.

##### dnsmasq

Configure dnsmasq as a [local DNS cache](/index.php/Dnsmasq#DNS_cache_setup "Dnsmasq"). The basic configuration to work with DNSCrypt:

 `/etc/dnsmasq.conf` 
```
no-resolv
server=127.0.0.1#53000
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

### 沙盒隔离

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

### 启用 EDNS0

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

#### 测试 EDNS0

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