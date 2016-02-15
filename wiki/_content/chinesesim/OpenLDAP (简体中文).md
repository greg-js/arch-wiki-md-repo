**翻译状态：** 本文是英文页面 [openLDAP](/index.php/OpenLDAP "OpenLDAP") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-06-01，点击[这里](https://wiki.archlinux.org/index.php?title=openLDAP&diff=0&oldid=317024)可以查看翻译后英文页面的改动。

OpenLDAP 是 LDAP 协议的一个开源实现。LDAP 服务器基本上是一个为只读访问而优化的非关系型数据库。它主要用做地址簿查询（如 email 客户端）或对各种服务访问做后台认证以及用户数据权限管控。（例如，访问 Samba 时，LDAP 可以起到域控制器的作用；或者 [Linux 系统认证](/index.php/LDAP_Authentication "LDAP Authentication") 时代替 `/etc/passwd` 的作用。）

**注意:** 以 `ldap` 开头的命令（如： `ldapsearch`）是客户端工具，以 `slap` 开头的命令（如： `slapcat` `slapcat`）是服务端工具。

本页面内容仅基于一个基本的 OpenLDAP 安装做简要配置说明。

**小贴士:** 目录服务是一个庞大的主题，其配置可以非常复杂。如果你是一个完全的新手，[这里](http://www.brennan.id.au/20-Shared_Address_Book_LDAP.html)有一份详尽的介绍文档。该文档通俗易懂，即使你对 LDAP 一窍不通也完全可以引领你入门。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 服务端](#.E6.9C.8D.E5.8A.A1.E7.AB.AF)
    *   [2.2 客户端](#.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [2.3 测试安装好的系统](#.E6.B5.8B.E8.AF.95.E5.AE.89.E8.A3.85.E5.A5.BD.E7.9A.84.E7.B3.BB.E7.BB.9F)
    *   [2.4 基于TLS的OpenLDAP](#.E5.9F.BA.E4.BA.8ETLS.E7.9A.84OpenLDAP)
        *   [2.4.1 创建一个自签署的证书](#.E5.88.9B.E5.BB.BA.E4.B8.80.E4.B8.AA.E8.87.AA.E7.AD.BE.E7.BD.B2.E7.9A.84.E8.AF.81.E4.B9.A6)
        *   [2.4.2 配置基于SSL的slapd](#.E9.85.8D.E7.BD.AE.E5.9F.BA.E4.BA.8ESSL.E7.9A.84slapd)
        *   [2.4.3 启动基于SSL的slapd](#.E5.90.AF.E5.8A.A8.E5.9F.BA.E4.BA.8ESSL.E7.9A.84slapd)
*   [3 下一步](#.E4.B8.8B.E4.B8.80.E6.AD.A5)
*   [4 排错](#.E6.8E.92.E9.94.99)
    *   [4.1 检查客户端认证](#.E6.A3.80.E6.9F.A5.E5.AE.A2.E6.88.B7.E7.AB.AF.E8.AE.A4.E8.AF.81)
    *   [4.2 LDAP服务突然停止](#LDAP.E6.9C.8D.E5.8A.A1.E7.AA.81.E7.84.B6.E5.81.9C.E6.AD.A2)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 安装

OpenLDAP 软件包同时包含了服务器和客户端。可以从 [官方源](/index.php/Official_repositories "Official repositories") 安装 [openldap](https://www.archlinux.org/packages/?name=openldap)。

## 配置

### 服务端

**注意:** 系统中现有的 OpenLDAP 数据库要通过清空 `/var/lib/openldap/openldap-data/`目录的方法将其删除。

服务器的配置文件位于 `/etc/openldap/slapd.conf`。

Edit the suffix and rootdn. The suffix typically is your domain name but it does not have to be. It depends on how you use your directory. We will use _example_ for the domain name, and _com_ for the tld. The rootdn is your LDAP administrator's name (we will use _root_ here).

```
suffix     "dc=example,dc=com"
rootdn     "cn=root,dc=example,dc=com"

```

Now we delete the default root password and create a strong one:

```
# sed -i "/rootpw/ d" /etc/openldap/slapd.conf #find the line with rootpw and delete it
# echo "rootpw    $(slappasswd)" >> /etc/openldap/slapd.conf  #add a line which includes the hashed password output from slappasswd

```

You will likely want to add some typically used [schemas](http://www.openldap.org/doc/admin24/schema.html) to the top of `slapd.conf`:

```
include         /etc/openldap/schema/cosine.schema
include         /etc/openldap/schema/inetorgperson.schema
include         /etc/openldap/schema/nis.schema

```

You will likely want to add some typically used [indexes](http://www.openldap.org/doc/admin24/tuning.html#Indexes) to the bottom of `slapd.conf`:

```
index   uid             pres,eq
index   mail            pres,sub,eq
index   cn              pres,sub,eq
index   sn              pres,sub,eq
index   dc              eq

```

Now prepare the database directory. You will need to copy the default config file and set the proper ownership:

```
# cp /etc/openldap/DB_CONFIG.example /var/lib/openldap/openldap-data/DB_CONFIG
# chown ldap:ldap /var/lib/openldap/openldap-data/DB_CONFIG

```

**Note:** With OpenLDAP 2.4 the configuration of `slapd.conf` is deprecated. From this version on all configuration settings are stored in `/etc/openldap/slapd.d/`.

To store the recent changes in `slapd.conf` to the new `/etc/openldap/slapd.d/` configuration settings, we have to delete the old configuration files first, do this every time you change the configuration:

```
# rm -rf /etc/openldap/slapd.d/*

```

(if you do not have a database yet, you might need to create one by starting and stopping the `slapd.service` [using systemd](/index.php/Systemd#Using_units "Systemd") )

Then we generate the new configuration with:

```
# slaptest -f /etc/openldap/slapd.conf -F /etc/openldap/slapd.d/

```

The above command has to be run every time you change `slapd.conf`. Check if everything succeeded. Ignore message "bdb_monitor_db_open: monitoring disabled; configure monitor database to enable".

Change ownership recursively on the new files and directory in /etc/openldap/slapd.d:

```
# chown -R ldap:ldap /etc/openldap/slapd.d

```

**Note:** Index the directory after you populate it. You should stop slapd before doing this.

```
# slapindex
# chown ldap:ldap /var/lib/openldap/openldap-data/*

```

Finally, start the slapd daemon with `slapd.service` using systemd.

### 客户端

The client config file is located at `/etc/openldap/ldap.conf`.

It is quite simple: you'll only have to alter `BASE` to reflect the suffix of the server, and `URI` to reflect the address of the server, like:

 `/etc/openldap/ldap.conf` 

```
BASE            dc=example,dc=com
URI             ldap://localhost
```

If you decide to use SSL:

*   The protocol (ldap or ldaps) in the `URI` entry has to conform with the slapd configuration
*   If you decide to use self-signed certificates, add a `TLS_REQCERT allow` line to `ldap.conf`

### 测试安装好的系统

This is easy, just run the command below:

```
$ ldapsearch -x '(objectclass=*)'

```

Or authenticating as the rootdn (replacing `-x` by `-D <user> -W`), using the example configuration we had above:

```
$ ldapsearch -D "cn=root,dc=example,dc=com" -W '(objectclass=*)'

```

Now you should see some information about your database.

### 基于TLS的OpenLDAP

**Note:** [upstream documentation](http://web.archive.org/web/20130211222328/http://www.openldap.org/pub/ksoper/OpenLDAP_TLS.html#4.0) is much more useful/complete than this section

If you access the OpenLDAP server over the network and especially if you have sensitive data stored on the server you run the risk of someone sniffing your data which is sent clear-text. The next part will guide you on how to setup an SSL connection between the LDAP server and the client so the data will be sent encrypted.

In order to use TLS, you must have a certificate. For testing purposes, a _self-signed_ certificate will suffice. To learn more about certificates, see [OpenSSL](/index.php/OpenSSL "OpenSSL").

**Warning:** OpenLDAP cannot use a certificate that has a password associated to it.

#### 创建一个自签署的证书

To create a _self-signed_ certificate, type the following:

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
TLSCipherSuite HIGH:MEDIUM:-SSLv2
TLSCertificateFile /etc/openldap/ssl/slapdcert.pem
TLSCertificateKeyFile /etc/openldap/ssl/slapdkey.pem

```

The TLSCipherSuite specifies a list of OpenSSL ciphers from which slapd will choose when negotiating TLS connections, in decreasing order of preference. In addition to those specific ciphers, you can use any of the wildcards supported by OpenSSL. **NOTE:** HIGH, MEDIUM, and +SSLv2 are all wildcards.

**Note:** To see which ciphers are supported by your local OpenSSL installation, type the following: `openssl ciphers -v ALL`

Regenerate the configuration directory:

```
# rm -rf /etc/openldap/slapd.d/*                                  # erase old config settings
# slaptest -f /etc/openldap/slapd.conf -F /etc/openldap/slapd.d/  # generate new config directory from config file
# chown -R ldap:ldap /etc/openldap/slapd.d                        # Change ownership recursively to ldap on the config directory

```

#### 启动基于SSL的slapd

You will have to edit `slapd.service` to change to protocol slapd listens on.

First, disable `slapd.service` if it's enabled.

Then, copy the stock service to `/etc/systemd/system/`:

```
# cp /usr/lib/systemd/system/slapd.service /etc/systemd/system/

```

Edit it, and add change `ExecStart` to:

 `/etc/systemd/system/slapd.service`  `ExecStart=/usr/bin/slapd -u ldap -g ldap -h "ldaps:///"` 

Localhost connections don't need to use SSL. So, if you want to access the server locally you should change the `ExecStart` line to:

```
ExecStart=/usr/bin/slapd -u ldap -g ldap -h "ldap://127.0.0.1 ldaps:///"

```

Then reenable and start it:

```
# systemctl daemon-reload
# systemctl restart slapd.service

```

If `slapd` started successfully you can enable it.

**Note:** If you created a self-signed certificate above, be sure to add `TLS_REQCERT allow` to `/etc/openldap/ldap.conf` on the client, or it won't be able connect to the server.

## 下一步

You now have a basic LDAP installation. The next step is to design your directory. The design is heavily dependent on what you are using it for. If you are new to LDAP, consider starting with a directory design recommended by the specific client services that will use the directory (PAM, [Postfix](/index.php/Postfix "Postfix"), etc).

A directory for system authentication is the [LDAP Authentication](/index.php/LDAP_Authentication "LDAP Authentication") article.

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

## 参阅

*   [Official OpenLDAP Software 2.4 Administrator's Guide](http://www.openldap.org/doc/admin24/)
*   [phpLDAPadmin](/index.php/PhpLDAPadmin "PhpLDAPadmin") is a web interface tool in the style of phpMyAdmin.
*   [LDAP Authentication](/index.php/LDAP_Authentication "LDAP Authentication")
*   [apachedirectorystudio](https://aur.archlinux.org/packages/apachedirectorystudio/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") is an Eclipse-based LDAP viewer. Works perfect with OpenLDAP installations.