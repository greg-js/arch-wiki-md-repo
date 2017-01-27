**翻译状态：** 本文是英文页面 [openLDAP](/index.php/OpenLDAP "OpenLDAP") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-01-27，点击[这里](https://wiki.archlinux.org/index.php?title=openLDAP&diff=0&oldid=464607)可以查看翻译后英文页面的改动。

OpenLDAP 是 LDAP 协议的一个开源实现。LDAP 服务器本质上是一个为只读访问而优化的非关系型数据库。它主要用做地址簿查询（如 email 客户端）或对各种服务访问做后台认证以及用户数据权限管控。（例如，访问 Samba 时，LDAP 可以起到域控制器的作用；或者 [Linux 系统认证](/index.php/LDAP_authentication "LDAP authentication") 时代替 `/etc/passwd` 的作用。）

**注意:** 以 `ldap` 开头的命令（如： `ldapsearch`）是客户端工具，以 `slap` 开头的命令（如： `slapcat` `slapcat`）是服务端工具。

本页面内容仅基于一个基本的 OpenLDAP 安装做简要配置说明。

**提示：** 目录服务是一个庞大的主题，其配置可以非常复杂。如果你是一个完全的新手，[这里](http://www.brennan.id.au/20-Shared_Address_Book_LDAP.html)有一份详尽的介绍文档。该文档通俗易懂，即使你对 LDAP 一窍不通也完全可以引领你入门。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 服务端](#.E6.9C.8D.E5.8A.A1.E7.AB.AF)
    *   [2.2 客户端](#.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [2.3 创建初始项](#.E5.88.9B.E5.BB.BA.E5.88.9D.E5.A7.8B.E9.A1.B9)
    *   [2.4 测试安装好的系统](#.E6.B5.8B.E8.AF.95.E5.AE.89.E8.A3.85.E5.A5.BD.E7.9A.84.E7.B3.BB.E7.BB.9F)
    *   [2.5 基于 TLS 的 OpenLDAP](#.E5.9F.BA.E4.BA.8E_TLS_.E7.9A.84_OpenLDAP)
        *   [2.5.1 创建一个自签署的证书](#.E5.88.9B.E5.BB.BA.E4.B8.80.E4.B8.AA.E8.87.AA.E7.AD.BE.E7.BD.B2.E7.9A.84.E8.AF.81.E4.B9.A6)
        *   [2.5.2 配置基于SSL的slapd](#.E9.85.8D.E7.BD.AE.E5.9F.BA.E4.BA.8ESSL.E7.9A.84slapd)
        *   [2.5.3 启动基于SSL的slapd](#.E5.90.AF.E5.8A.A8.E5.9F.BA.E4.BA.8ESSL.E7.9A.84slapd)
*   [3 下一步](#.E4.B8.8B.E4.B8.80.E6.AD.A5)
*   [4 排错](#.E6.8E.92.E9.94.99)
    *   [4.1 检查客户端认证](#.E6.A3.80.E6.9F.A5.E5.AE.A2.E6.88.B7.E7.AB.AF.E8.AE.A4.E8.AF.81)
    *   [4.2 LDAP服务突然停止](#LDAP.E6.9C.8D.E5.8A.A1.E7.AA.81.E7.84.B6.E5.81.9C.E6.AD.A2)
    *   [4.3 LDAP Server Doesn't Start](#LDAP_Server_Doesn.27t_Start)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 安装

OpenLDAP 软件包同时包含了服务器和客户端。请[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")软件包 [openldap](https://www.archlinux.org/packages/?name=openldap)。

## 配置

### 服务端

**注意:** 需要先清空系统中现有 OpenLDAP 数据库，请删除 `/var/lib/openldap/openldap-data/`目录下的所有文件。

服务器的配置文件位于 `/etc/openldap/slapd.conf`。

需要编辑后缀和 rootdn。典型的后缀通常是你所用的域名，但这并非强制要求，而是依赖于你如何使用你的目录。下例中以 *example* 做为域名，tld 为 *com*，rootdn 则是 LDAP 管理员的名字（这里用 *root*）。

```
suffix     "dc=example,dc=com"
rootdn     "cn=root,dc=example,dc=com"

```

现在删除默认 root 口令并创建一个强口令：

```
# sed -i "/rootpw/ d" /etc/openldap/slapd.conf #find the line with rootpw and delete it
# echo "rootpw    $(slappasswd)" >> /etc/openldap/slapd.conf  # 添加一行包含经由 slappasswd 哈希化的口令行

```

在 `slapd.conf` 头部添加一些 [schemas](http://www.openldap.org/doc/admin24/schema.html):

**注意:** currently missing: cp /usr/share/doc/samba/examples/LDAP/samba.schema /etc/openldap/schema

```
include         /etc/openldap/schema/cosine.schema
include         /etc/openldap/schema/inetorgperson.schema
include         /etc/openldap/schema/nis.schema
#include         /etc/openldap/schema/samba.schema

```

可能需要在 `slapd.conf` 底部加入一些常用的 [indexes](http://www.openldap.org/doc/admin24/tuning.html#Indexes):

```
index   uid             pres,eq
index   mail            pres,sub,eq
index   cn              pres,sub,eq
index   sn              pres,sub,eq
index   dc              eq

```

现在准备数据目录，需要重命名配置文件：

```
# mv /var/lib/openldap/openldap-data/DB_CONFIG.example /var/lib/openldap/openldap-data/DB_CONFIG

```

**注意:** 从 OpenLDAP 2.4 版本开始所有配置数据都保存在 `/etc/openldap/slapd.d/`中，建议不再使用 `slapd.conf` 作为配置文件。

将 `slapd.conf` 中的改动应用到 `/etc/openldap/slapd.d/`，需要先删除老配置：

```
# rm -rf /etc/openldap/slapd.d/*

```

如果还没有数据库，用 [using systemd](/index.php/Systemd#Using_units "Systemd") 启动然后停止 `slapd.service` 服务。

用下面命令生成配置文件:

```
# slaptest -f /etc/openldap/slapd.conf -F /etc/openldap/slapd.d/

```

每次修改 `slapd.conf` 后，都需要执行上面命令。检查有没有问题，可以忽略 "bdb_monitor_db_open: monitoring disabled; configure monitor database to enable".

修改 /etc/openldap/slapd.d 中所有文件的权限:

```
# chown -R ldap:ldap /etc/openldap/slapd.d

```

**注意:** 增加文件后，请建立索引，建立前请停止 slapd 服务.
```
# slapindex
# chown ldap:ldap /var/lib/openldap/openldap-data/*

```

或者

```
$ sudo -u ldap slapindex

```

最后，启动 `slapd.service` 服务。

### 客户端

客户的配置文件位于 `/etc/openldap/ldap.conf`.

这个配置很简单，只需要将`BASE` 设置为服务器的前缀，将 `URI` 设置为服务器的地址:

 `/etc/openldap/ldap.conf` 
```
BASE            dc=example,dc=com
URI             ldap://localhost
```

要使用 SSL 的话:

*   `URI` 的协议 (ldap 或 ldaps) 要和 slapd 配置一致
*   要使用自签名的证书，在 `ldap.conf` 中添加 `TLS_REQCERT allow` 行
*   要从认证机构获取自签名证书，在 `ldap.conf` 中添加`TLS_CACERTDIR /usr/share/ca-certificates/trust-source`行.

### 创建初始项

配置好客户端后，创建根项和 root 角色项：

```
$ ldapadd -x -D 'cn=root,dc=example,dc=com' -W
dn: dc=example,dc=com
objectClass: dcObject	
objectClass: organization
dc: example
o: Example
description: Example directory
dn: cn=root,dc=example,dc=com
objectClass: organizationalRole
cn: root
description: Directory Manager
^D

```

第一行后的内容是在 stdin 输入的，或者用 -f 选项从文件或重定向读入.

### 测试安装好的系统

运行下面命令:

```
$ ldapsearch -x '(objectclass=*)'

```

或认证为 rootdn (将 `-x` 替换为 `-D <user> -W`), 用上面配置的例子的话：

```
$ ldapsearch -D "cn=root,dc=example,dc=com" -W '(objectclass=*)'

```

应该能看到数据库中的信息.

### 基于 TLS 的 OpenLDAP

**注意:** [官方文档](http://www.openldap.org/doc/admin24/)比本节内容更加完整实用。

如果通过网络访问 OpenLDAP 服务器，尤其是当你的服务器上保存有敏感数据时，明文传输这些数据存在被他人嗅探的风险。If you access the OpenLDAP server over the network and especially if you have sensitive data stored on the server you run the risk of someone sniffing your data which is sent clear-text. 下面章节将指导你如何设置 LDAP 服务器与客户端之间的 SSL 连接以加密传输数据。The next part will guide you on how to setup an SSL connection between the LDAP server and the client so the data will be sent encrypted.

要使用 TLS，你必须获得一个证书。In order to use TLS, you must have a certificate. 测试时可以使用*自签署*证书。证书的详细信息请参阅 [OpenSSL](/index.php/OpenSSL "OpenSSL")。For testing purposes, a *self-signed* certificate will suffice. To learn more about certificates, see [OpenSSL](/index.php/OpenSSL "OpenSSL").

**警告:** OpenLDAP 不能使用关联了口令的证书。cannot use a certificate that has a password associated to it.

#### 创建一个自签署的证书

输入下列命令创建一个自签署证书： To create a *self-signed* certificate, type the following:

```
$ openssl req -new -x509 -nodes -out slapdcert.pem -keyout slapdkey.pem -days 365

```

You will be prompted for information about your LDAP server. Much of the information can be left blank. The most important information is the common name. This must be set to the DNS name of your LDAP server. If your LDAP server's IP address resolves to example.org but its server certificate shows a CN of bad.example.org, LDAP clients will reject the certificate and will be unable to negotiate TLS connections (apparently the results are wholly unpredictable).

Now that the certificate files have been created copy them to `/etc/openldap/ssl/` (create this directory if it doesn't exist) and secure them. `slapdcert.pem` must be world readable because it contains the public key. `slapdkey.pem` on the other hand should only be readable for the ldap user for security reasons:

```
# mv slapdcert.pem slapdkey.pem /etc/openldap/ssl/
# chmod -R 755 /etc/openldap/ssl/
# chmod 400 /etc/openldap/ssl/slapdkey.pem
# chmod 444 /etc/openldap/ssl/slapdcert.pem
# chown ldap /etc/openldap/ssl/slapdkey.pem

```

#### 配置基于SSL的slapd

Edit the daemon configuration file (`/etc/openldap/slapd.conf`) to tell LDAP where the certificate files reside by adding the following lines:

```
# Certificate/SSL Section
TLSCipherSuite DEFAULT
TLSCertificateFile /etc/openldap/ssl/slapdcert.pem
TLSCertificateKeyFile /etc/openldap/ssl/slapdkey.pem

```

If you are using a signed SSL Certificate from a certification authority such as [Let’s Encrypt](/index.php/Let%E2%80%99s_Encrypt "Let’s Encrypt"), you will also need to specify the path to the root certificates database and your intermediary certificate. You will also need to change ownership of the `.pem` files and intermediary directories to make them readable to the user `ldap`:

```
# Certificate/SSL Section
TLSCipherSuite DEFAULT
TLSCertificateFile /etc/letsencrypt/live/ldap.my-domain.com/cert.pem
TLSCertificateKeyFile /etc/letsencrypt/live/ldap.my-domain.com/privkey.pem	
TLSCACertificateFile /etc/letsencrypt/live/ldap.my-domain.com/chain.pem
TLSCACertificatePath /usr/share/ca-certificates/trust-source

```

The TLSCipherSuite specifies a list of OpenSSL ciphers from which slapd will choose when negotiating TLS connections, in decreasing order of preference. In addition to those specific ciphers, you can use any of the wildcards supported by OpenSSL. DEFAULT is a wildcard. See `man ciphers` for description of ciphers, wildcards and options supported.

**Note:** To see which ciphers are supported by your local OpenSSL installation, type the following: `openssl ciphers -v ALL:COMPLEMENTOFALL`. Always test which ciphers will actually be enabled by TLSCipherSuite by providing it to OpenSSL command, like this: `openssl ciphers -v 'DEFAULT'`

Regenerate the configuration directory:

```
# rm -rf /etc/openldap/slapd.d/*                                  # erase old config settings
# slaptest -f /etc/openldap/slapd.conf -F /etc/openldap/slapd.d/  # generate new config directory from config file
# chown -R ldap:ldap /etc/openldap/slapd.d                        # Change ownership recursively to ldap on the config directory

```

#### 启动基于SSL的slapd

You will have to edit `slapd.service` to change to protocol slapd listens on.

Create the override unit:

 `systemctl edit slapd.service` 
```
[Service]
ExecStart=/usr/bin/slapd -u ldap -g ldap -h "ldaps:///"
```

Localhost connections don't need to use SSL. So, if you want to access the server locally you should change the `ExecStart` line to:

```
ExecStart=/usr/bin/slapd -u ldap -g ldap -h "ldap://127.0.0.1 ldaps:///"

```

Then [restart](/index.php/Restart "Restart") `slapd.service`. If it was enabled before, reenable it now.

If `slapd` started successfully you can enable it.

**Note:** If you created a self-signed certificate above, be sure to add `TLS_REQCERT allow` to `/etc/openldap/ldap.conf` on the client, or it won't be able connect to the server.

## 下一步

You now have a basic LDAP installation. The next step is to design your directory. The design is heavily dependent on what you are using it for. If you are new to LDAP, consider starting with a directory design recommended by the specific client services that will use the directory (PAM, [Postfix](/index.php/Postfix "Postfix"), etc).

A directory for system authentication is the [LDAP authentication](/index.php/LDAP_authentication "LDAP authentication") article.

A nice web frontend is [phpLDAPadmin](/index.php/PhpLDAPadmin "PhpLDAPadmin").

## 排错

### 检查客户端认证

If you can't connect to your server for non-secure authentication

```
$ ldapsearch -x -H ldap://ldaservername:389 -D cn=Manager,dc=example,dc=exampledomain

```

and for TLS secured authentication with:

```
$ ldapsearch -x -H ldaps://ldaservername:636 -D cn=Manager,dc=example,dc=exampledomain

```

### LDAP服务突然停止

If you notice that slapd seems to start but then stops, try running:

```
# chown ldap:ldap /var/lib/openldap/openldap-data/*

```

to allow slapd write access to its data directory as the user "ldap".

### LDAP Server Doesn't Start

Try starting the server from the command line with debugging output enabled:

```
# slapd -u ldap -g ldap -h ldaps://ldaservername:636 -d Config,Stats

```

## 参阅

*   [Official OpenLDAP Software 2.4 Administrator's Guide](http://www.openldap.org/doc/admin24/)
*   [phpLDAPadmin](/index.php/PhpLDAPadmin "PhpLDAPadmin") is a web interface tool in the style of phpMyAdmin.
*   [LDAP authentication](/index.php/LDAP_authentication "LDAP authentication")
*   [apachedirectorystudio](https://aur.archlinux.org/packages/apachedirectorystudio/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") is an Eclipse-based LDAP viewer. Works perfect with OpenLDAP installations.