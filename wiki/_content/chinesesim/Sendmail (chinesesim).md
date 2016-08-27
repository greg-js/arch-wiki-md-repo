**翻译状态：** 本文是英文页面 [Sendmail](/index.php/Sendmail "Sendmail") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-26，点击[这里](https://wiki.archlinux.org/index.php?title=Sendmail&diff=0&oldid=435685)可以查看翻译后英文页面的改动。

Sendmail 是来自 UNIX 世界的经典 SMTP 服务器。Arch Linux 还提供了 [Postfix](/index.php/Postfix "Postfix")。

本文的目的是为本地用户账户设置 Sendmail，**不使用 mysql 或者其它数据库**，同时允许建立所谓 *mail-only 账户*。

本文仅描述了配置 Sendmail 的必需步骤；要添加 IMAP 与 POP3 服务，您可以考虑阅读 [Dovecot](/index.php/Dovecot "Dovecot") 的内容。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 DNS 记录](#DNS_.E8.AE.B0.E5.BD.95)
*   [3 添加用户](#.E6.B7.BB.E5.8A.A0.E7.94.A8.E6.88.B7)
*   [4 配置](#.E9.85.8D.E7.BD.AE)
    *   [4.1 创建 SSL 证书](#.E5.88.9B.E5.BB.BA_SSL_.E8.AF.81.E4.B9.A6)
    *   [4.2 sendmail.cf](#sendmail.cf)
    *   [4.3 sendmail.conf](#sendmail.conf)
    *   [4.4 local-host-names](#local-host-names)
    *   [4.5 access.db](#access.db)
    *   [4.6 aliases.db](#aliases.db)
    *   [4.7 virtusertable.db](#virtusertable.db)
    *   [4.8 开机自动启动](#.E5.BC.80.E6.9C.BA.E8.87.AA.E5.8A.A8.E5.90.AF.E5.8A.A8)
    *   [4.9 SASL 验证](#SASL_.E9.AA.8C.E8.AF.81)
*   [5 小窍门](#.E5.B0.8F.E7.AA.8D.E9.97.A8)
    *   [5.1 将某个域名的全部邮件转发至特定邮箱](#.E5.B0.86.E6.9F.90.E4.B8.AA.E5.9F.9F.E5.90.8D.E7.9A.84.E5.85.A8.E9.83.A8.E9.82.AE.E4.BB.B6.E8.BD.AC.E5.8F.91.E8.87.B3.E7.89.B9.E5.AE.9A.E9.82.AE.E7.AE.B1)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [sendmail](https://aur.archlinux.org/packages/sendmail/), [procmail](https://www.archlinux.org/packages/?name=procmail) 和 [m4](https://www.archlinux.org/packages/?name=m4)

## DNS 记录

您应当拥有一个域名，并且编辑所拥有域名的 MX 记录指向你的服务器。请注意一些服务器在处理指向 CNAMEs 的 MX 记录时会出现问题，所以你应当考虑将 MX 记录指向一个 A 记录。

## 添加用户

为每个需要接收邮件的用户创建 [[Users and groups|Linux 用户，每个用户会拥有类似 username@your-domain.com 的电子邮件地址。但是如果你想要添加 *mail-only 账户*，即仅能处理电子邮件，但不能使用 shell 或 X 进行登录的账户，您可以按如下步骤添加该类账户：

```
# useradd -m -s /usr/bin/nologin *username*

```

注：在此之后，您可以随时通过修改 `/etc/passwd` 等方式更改账户类型与属性。

## 配置

### 创建 SSL 证书

**Warning:** If you plan on implementing SSL/TLS, know that some variations and implementations are [still](https://weakdh.org/#affected) [vulnerable to attack](https://en.wikipedia.org/wiki/Transport_Layer_Security#Attacks_against_TLS.2FSSL "wikipedia:Transport Layer Security"). For details on these current vulnerabilities within SSL/TLS and how to apply appropriate changes to Sendmail, visit [http://disablessl3.com/](http://disablessl3.com/) and [https://weakdh.org/sysadmin.html](https://weakdh.org/sysadmin.html)

生成一个 key 并对其签名，请阅读 [OpenSSL](/index.php/OpenSSL#Generating_keys "OpenSSL") 以了解更多信息，[Let's Encrypt](/index.php/Let%27s_Encrypt "Let's Encrypt") 提供了免费认证。

**Warning:** 使用经过口令加密（具有 passphrase）的服务器的密钥文件可能导致 Sendmail 启用 TLS 失败。如果出现问题，请参考 [这里](https://mnx.io/blog/removing-a-passphrase-from-an-ssl-key/) 移除已有密钥文件的口令。

**Note:** 建议将服务器密钥与证书统一放在 `/etc/mail/certs/` 目录下，并移除服务器密钥文件的组可读与其它可读权限。之后 `sendmailconfig` 工具可能会自动更改该文件夹下文件的属主、属组与权限。

### sendmail.cf

创建文件 `/etc/mail/sendmail.mc`，并以此为基础使用 [m4](https://zh.wikipedia.org/wiki/M4_(程式語言)) 工具生成 `sendmail.cf` 文件。

您可以由 `/usr/share/sendmail-cf/README` 文件了解配置 sendmail 的全部选项。

**Warning:** 无论是从头创建自己的 `sendmail.mc` 文件，还是在已有的 `sendmail.mc` 文件基础上进行修改，请时刻牢记，在**非 TLS** 情况下使用明文验证是十分危险的行为。除非您明确了解自己行为的意义，请使用以下示例中的方法强制进行 TLS 验证以确保安全性。

下面是在 [TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security "wikipedia:Transport Layer Security") 之上进行身份验证的配置文件示例。例子包含了解释工作原理的注释，这些注释以 `dnl` 这个单词起始。

 `/etc/mail/sendmail.mc` 
```
include(`/usr/share/sendmail-cf/m4/cf.m4')
define(`confDOMAIN_NAME', `your-domain.com')dnl
FEATURE(use_cw_file)
dnl  The following allows relaying if the user authenticates,
dnl  and disallows plaintext authentication (PLAIN/LOGIN) on
dnl  non-TLS links:
define(`confAUTH_OPTIONS', `A p y')dnl
dnl
dnl  Accept PLAIN and LOGIN authentications:
TRUST_AUTH_MECH(`LOGIN PLAIN')dnl
define(`confAUTH_MECHANISMS', `LOGIN PLAIN')dnl
dnl
dnl Make sure this paths correctly point to your SSL cert files:
define(`confCACERT_PATH',`/etc/ssl/certs')
define(`confCACERT',`/etc/ssl/cacert.pem')
define(`confSERVER_CERT',`/etc/ssl/certs/server.crt')
define(`confSERVER_KEY',`/etc/ssl/private/server.key')
dnl
FEATURE(`virtusertable', `hash /etc/mail/virtusertable.db')dnl
OSTYPE(linux)dnl
MAILER(local)dnl
MAILER(smtp)dnl

```

然后使用使用

```
# m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf

```

命令生成 `sendmail.cf` 文件。

**Note:** 如果您对 `sendmail.cf` 语法感兴趣，请参阅 [这篇文章](http://www.sendmail.org/~ca/email/doc8.12/op-sh-5.html) 了解详情。

### sendmail.conf

`sendmail.conf` 文件，如果存在，则也是配置 Sendmail 并最终生成 `sendmail.cf` 的一个配置文件。请阅读文件内含的注释了解详细信息。

### local-host-names

请将您的域名写入 `local-host-names` 文件:

 `/etc/mail/local-host-names` 
```
localhost
your-domain.com
mail.your-domain.com
localhost.localdomain

```

请确保您的域名可以被 `/etc/hosts` 文件解析。

### access.db

创建文件 `/etc/mail/access` 然后写入规则以配置邮件转发、允许收信与拒信。假设你在 `10.5.0.0/24` 有一个 VPN，而且你希望转发来自该 IP 段的所有邮件：

 `/etc/mail/access` 
```
10.5.0 RELAY
127.0.0 RELAY

```

然后使用

```
# makemap hash /etc/mail/access.db < /etc/mail/access

```

命令处理生成 sendmail 可以使用的配置数据库。

### aliases.db

编辑文件 `/etc/mail/aliases` ，反注释这一行： `#root: human being here` 并将其修改如下：

 `root:         your-username` 

你可以在此添加用户的别名。例如：

```
coolguy:      your-username
somedude:     your-username
```

然后使用

```
# newaliases

```

命令进行处理。

### virtusertable.db

创建 `virtusertable` 文件并在其中写入含有域名的别名：（这项功能在您的服务器绑定多域名时十分有用）

 `/etc/mail/virtusertable` 
```
your-username@your-domain.com         your-username
joe@my-other.tk                       joenobody

```

然后使用

```
# makemap hash /etc/mail/virtusertable.db < /etc/mail/virtusertable

```

命令进行处理。

### 开机自动启动

启用并启动下列服务。请阅读 [守护进程](/index.php/Daemon_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Daemon (简体中文)") 了解详情。

*   `saslauthd.service`
*   `sendmail.service`
*   `sm-client.service`

### SASL 验证

将用户添加至 SASL 数据库并设置用于 SMTP 身份验证的密码。

```
# saslpasswd2 -c your-username

```

注：您可以设置使用异于 SASL 的身份验证途径。这需要进一步修改配置文件，这里不赘述。

## 小窍门

### 将某个域名的全部邮件转发至特定邮箱

若需将 **my-other.tk** 域名下所有用户的电子邮件转发到 **your-username@your-domain.com**，请在 `/etc/mail/virtusertable` 文件中添加以下一行：

 `@my-other.tk        your-username@your-domain.com` 

不要忘记再次使用如下命令更新配置数据库：

```
# makemap hash /etc/mail/virtusertable.db < /etc/mail/virtusertable

```