# DNSCrypt (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**翻译状态：** 本文是英文页面 [DNSCrypt](/index.php/DNSCrypt "DNSCrypt") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-09-10，点击[这里](https://wiki.archlinux.org/index.php?title=DNSCrypt&diff=0&oldid=397827)可以查看翻译后英文页面的改动。

[DNSCrypt](http://dnscrypt.org/) encrypts and authenticates DNS traffic between user and DNS resolver. While IP traffic itself is unchanged, it prevents local spoofing of DNS queries, ensuring DNS responses are sent by the server of choice. [[1]](https://www.reddit.com/r/sysadmin/comments/2hn435/dnssec_vs_dnscrypt/ckuhcbu)

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
*   [3 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [3.1 DNSCrypt 作为转发的本地DNS缓存](#DNSCrypt_.E4.BD.9C.E4.B8.BA.E8.BD.AC.E5.8F.91.E7.9A.84.E6.9C.AC.E5.9C.B0DNS.E7.BC.93.E5.AD.98)
        *   [3.1.1 示例: 配置 Unbound](#.E7.A4.BA.E4.BE.8B:_.E9.85.8D.E7.BD.AE_Unbound)
        *   [3.1.2 示例: 配置 dnsmasq](#.E7.A4.BA.E4.BE.8B:_.E9.85.8D.E7.BD.AE_dnsmasq)
        *   [3.1.3 示例: 配置 pdnsd](#.E7.A4.BA.E4.BE.8B:_.E9.85.8D.E7.BD.AE_pdnsd)
    *   [3.2 启用EDNS0](#.E5.90.AF.E7.94.A8EDNS0)
        *   [3.2.1 测试 EDNS0](#.E6.B5.8B.E8.AF.95_EDNS0)
    *   [3.3 Redundant DNSCrypt providers](#Redundant_DNSCrypt_providers)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [dnscrypt-proxy](https://www.archlinux.org/packages/?name=dnscrypt-proxy) 软件包。

## 配置

When `dnscrypt-proxy.socket` is [enabled](/index.php/Enable "Enable"), _dnscrypt-proxy_ accepts incoming requests on `127.0.0.1:53` to a DNS resolver. The default DNS resolver for `dnscrypt-proxy.service` is _dnscrypt.eu-nl_. Compatible resolver names are visible in the first column of `/usr/share/dnscrypt-proxy/dnscrypt-resolvers.csv`.

To change the default, [edit](/index.php/Systemd#Editing_provided_unit_files "Systemd") `dnscrypt-proxy.service`. It is recommended to choose a provider close to your location.

Modify the [resolv.conf](/index.php/Resolv.conf "Resolv.conf") file and replace the current set of resolver addresses with _localhost_:

```
nameserver 127.0.0.1

```

Other programs may overwrite this setting; 参阅 [resolv.conf#Preserve DNS settings](/index.php/Resolv.conf#Preserve_DNS_settings "Resolv.conf") for details.

## 提示和技巧

### DNSCrypt 作为转发的本地DNS缓存

It is recommended to run DNSCrypt as a forwarder for a local DNS cache, otherwise every single query will make a round-trip to the upstream resolver. Any local DNS caching program should work, examples below show configuration for [Unbound](/index.php/Unbound "Unbound"), [dnsmasq](/index.php/Dnsmasq "Dnsmasq"), and [pdnsd](/index.php/Pdnsd "Pdnsd").

First configure _dnscrypt-proxy_ to listen on a port different from the default `53`, since the DNS cache needs to listen on `53` and query _dnscrypt-proxy_ on a different port. Port number `40` is used as an example in this section:

 `# systemctl edit dnscrypt-proxy.socket` 

```
[Socket]
ListenStream=
ListenDatagram=
ListenStream=127.0.0.1:40
ListenDatagram=127.0.0.1:40
```

**Note:** The `ListenStream` and `ListenDatagram` options need to be cleared with empty assignment before overriding, otherwise the new address would be _added_ to the list of sockets. See [systemd#Editing provided unit files](/index.php/Systemd#Editing_provided_unit_files "Systemd") for details.

Then restart `dnscrypt-proxy.socket` and _stop_ `dnscrypt-proxy.service` if already running to let it be started by the _.socket_ unit.

#### 示例: 配置 Unbound

配置 [Unbound_(简体中文)](/index.php/Unbound_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Unbound (简体中文)") to your liking (remember to [set /etc/resolv.conf to use the local DNS server](/index.php/Unbound#Set_.2Fetc.2Fresolv.conf_to_use_the_local_DNS_server "Unbound")) and add the following lines to the end of the `server` section in `/etc/unbound/unbound.conf`:

```
do-not-query-localhost: no
forward-zone:
  name: "."
  forward-addr: 127.0.0.1@40

```

**Tip:** If you are setting up a server, add `interface: 0.0.0.0@53` and `access-control: _your-network_/_subnet-mask_ allow` inside the `server:` section so that the other computers can connect to the server. A client must be configured with `nameserver _address-of-your-server_` in `/etc/resolv.conf`.

重启 `unbound.service` 以应用更改。

#### 示例: 配置 dnsmasq

配置 dnsmasq作为 [本地DNS缓存](/index.php/Dnsmasq#DNS_Cache_Setup "Dnsmasq"), 基本配置工作在DNSCrypt:

 `/etc/dnsmasq.conf` 

```
no-resolv
server=127.0.0.1#40
listen-address=127.0.0.1
```

如果你配置DNSCrypt并使用 resolver和启用DNSSEC 验证，要确保并启用dnsmasq：

 `/etc/dnsmasq.conf`  `proxy-dnssec` 

重启 `dnsmasq.service` 以应用更改。

#### 示例: 配置 pdnsd

安装[pdnsd](/index.php/Pdnsd "Pdnsd"). 基本配置工作在DNSCrypt:

 `/etc/pdnsd.conf` 

```
global {
	perm_cache=16384;
	cache_dir="/var/cache/pdnsd";
	run_as="pdnsd";
 	server_ip = 127.0.0.1;
	status_ctl = on;
	query_method=udp_tcp;
	min_ttl=15m;       # Retain cached entries at least 15 minutes.
	max_ttl=1w;        # One week.
	timeout=10;        # Global timeout option (10 seconds).
	neg_domain_pol=on;
	udpbufsize=1024;   # Upper limit on the size of UDP messages.
}

server {
	label = "dnscrypt-proxy";
	ip = 127.0.0.1;
	port = 40;
	timeout = 4;
	interface = any;
	uptest = if;
	interval = 15m;
	proxy_only=on;
}

source {
	owner=localhost;
	file="/etc/hosts";
}

rr {
	name=localhost;
	reverse=on;
	a=127.0.0.1;
	owner=localhost;
	soa=localhost,root.localhost,42,86400,900,86400,86400;
}
```

重启 `pdnsd.service` 以应用更改。

### 启用EDNS0

[Extension Mechanisms for DNS](https://en.wikipedia.org/wiki/Extension_mechanisms_for_DNS "wikipedia:Extension mechanisms for DNS") that, among other things, allows a client to specify how large a reply over UDP can be.

Add the following line to your `/etc/resolv.conf`:

```
options edns0

```

You may also wish to add the following argument to _dnscrypt-proxy_:

```
--edns-payload-size=<bytes>

```

The default size being **1252** bytes, with values up to **4096** bytes being purportedly safe. A value below or equal to **512** bytes will disable this mechanism, unless a client sends a packet with an OPT section providing a payload size.

#### 测试 EDNS0

Make use of the [DNS Reply Size Test Server](https://www.dns-oarc.net/oarc/services/replysizetest), use the _dig_ command line tool from the [bind-tools](https://www.archlinux.org/packages/?name=bind-tools) package to issue a TXT query for the name _rs.dns-oarc.net_:

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

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Needs some tweaks to comply with [Help:Style](/index.php/Help:Style "Help:Style"), e.g avoid writing in first person and link to [enable](/index.php/Enable "Enable"), [start](/index.php/Start "Start") and similar instead of explicit systemctl commands. (Discuss in [Talk:DNSCrypt (简体中文)#](https://wiki.archlinux.org/index.php/Talk:DNSCrypt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)))

Creating redundancy is easy. Obtaining redundancy requires a simple edit to the above Unbound example and the addition of a second instance of the dnscrypt-proxy and service. Please be sure that you have the above Unbound example working prior to proceeding, as this tip extends the previous example.

Extend the above [Unbound](/index.php/Unbound "Unbound") configuration in `/etc/unbound/unbound.conf` to include an additional forward address that uses a different port. I use port 41 in the below example:

```
do-not-query-localhost: no
forward-zone:
  name: "."
  forward-addr: 127.0.0.1@40
  forward-addr: 127.0.0.1@41

```

Create a copy of the dnscrypt-proxy.service and dnscrypt-proxy.socket in the /etc/systemd/system folder. I used the names dnscrypt-proxy-backup.service and dnscrypt-proxy-backup.socket. The names don't really matter, but they must be unique and the socket must use the same prefix as the service. Edit **dnscrypt-proxy-backup.socket** and change the port to 41, as follows:

```
[Unit]
Description=dnscrypt-proxy listening socket

[Socket]
ListenStream=127.0.0.1:41
ListenDatagram=127.0.0.1:41

[Install]
WantedBy=sockets.target

```

Edit **dnscrypt-proxy-backup.service** , as follows indicating a different dnscrypt server name and listening on the the port entered above, 41:

```
[Unit]
Description=DNSCrypt client proxy
Requires=dnscrypt-proxy.socket

[Install]
Also=dnscrypt-proxy.socket
WantedBy=multi-user.target

[Service]
Type=simple
NonBlocking=true
ExecStart=/usr/bin/dnscrypt-proxy -R cloudns-can

```

You must force systemd to read the new service and socket files:

```
systemctl daemon-reload

```

Then enable the service and socket:

```
systemctl enable dnscrypt-proxy-backup.service dnscrypt-proxy-backup.socket

```

Start the service and socket. It's not really necessary to start the service as the socket will automatically launch it, but it does no harm.:

```
systemctl start dnscrypt-proxy-backup.service dnscrypt-proxy-backup.socket

```

Finally Restart Unbound:

```
systemctl restart unbound

```

If successful, your two selected dns providers should be the only ones found when using one of the dns leak test websites.

I really wanted to accomplish this with only a single .service and .socket files. Though the systemd documentation seems to indicate that it should be possible, I could not make it work. Here in lies a challenge to the more educated systemd folks out there. I'd love to see this further simplified.

Retrieved from "[https://wiki.archlinux.org/index.php?title=DNSCrypt_(简体中文)&oldid=415111](https://wiki.archlinux.org/index.php?title=DNSCrypt_(简体中文)&oldid=415111)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Domain Name System (简体中文)](/index.php/Category:Domain_Name_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Domain Name System (简体中文)")
*   [Encryption (简体中文)](/index.php/Category:Encryption_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Encryption (简体中文)")

Hidden category:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")