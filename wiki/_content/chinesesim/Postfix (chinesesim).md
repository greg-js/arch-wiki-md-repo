Related articles

*   [Postfix with SASL](/index.php/Postfix_with_SASL "Postfix with SASL")
*   [Virtual user mail system](/index.php/Virtual_user_mail_system "Virtual user mail system")
*   [OpenDMARC](/index.php/OpenDMARC "OpenDMARC")
*   [OpenDKIM](/index.php/OpenDKIM "OpenDKIM")

**翻译状态：** 本文是英文页面 [Postfix](/index.php/Postfix "Postfix") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-12-06，点击[这里](https://wiki.archlinux.org/index.php?title=Postfix&diff=0&oldid=558391)可以查看翻译后英文页面的改动。

[Postfix](https://en.wikipedia.org/wiki/Postfix_(software) 是[邮件传输代理软件](/index.php/Mail_transfer_agent "Mail transfer agent")。按照其 [官方网站](http://www.postfix.org/)的说法:

	attempts to be fast, easy to administer, and secure, while at the same time being sendmail compatible enough to not upset existing users. Thus, the outside has a sendmail-ish flavor, but the inside is completely different.

	快速、管理简单、安全， 同时足够兼容[Sendmail (简体中文)](/index.php/Sendmail_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Sendmail (简体中文)")，从而不会影响现有用户。 因此，从外面看是sendmail-ish风格，但内部是完全不同的。

本文基于 [邮件服务器](/index.php/Mail_server "Mail server")。 本文的目标是设置Postfix并解释基本配置文件的功能。 这里有两种交付方式的设置说明：本地系统用户方式 和 虚拟用户方式。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 别名 Aliases](#别名_Aliases)
    *   [2.2 系统本地用户邮件(Local mail)](#系统本地用户邮件(Local_mail))
    *   [2.3 虚拟用户邮件(Virtual mail)](#虚拟用户邮件(Virtual_mail))
    *   [2.4 检查配置 Check configuration](#检查配置_Check_configuration)
*   [3 启动 Postfix](#启动_Postfix)
*   [4 TLS](#TLS)
    *   [4.1 Secure SMTP (sending)](#Secure_SMTP_(sending))
    *   [4.2 Secure SMTP (receiving)](#Secure_SMTP_(receiving))
        *   [4.2.1 SMTPS (port 465)](#SMTPS_(port_465))
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Blacklist incoming emails](#Blacklist_incoming_emails)
    *   [5.2 Hide the sender's IP and user agent in the Received header](#Hide_the_sender's_IP_and_user_agent_in_the_Received_header)
    *   [5.3 Postfix in a chroot jail](#Postfix_in_a_chroot_jail)
    *   [5.4 DANE (DNSSEC)](#DANE_(DNSSEC))
        *   [5.4.1 Resource Record](#Resource_Record)
        *   [5.4.2 Configuration](#Configuration)
*   [6 Extras](#Extras)
    *   [6.1 Postgrey](#Postgrey)
        *   [6.1.1 Installation](#Installation)
        *   [6.1.2 Configuration](#Configuration_2)
        *   [6.1.3 Whitelisting](#Whitelisting)
        *   [6.1.4 Troubleshooting](#Troubleshooting)
    *   [6.2 SpamAssassin](#SpamAssassin)
        *   [6.2.1 SpamAssassin stand-alone generic setup](#SpamAssassin_stand-alone_generic_setup)
        *   [6.2.2 SpamAssassin combined with Dovecot LDA / Sieve (Mailfiltering)](#SpamAssassin_combined_with_Dovecot_LDA_/_Sieve_(Mailfiltering))
        *   [6.2.3 SpamAssassin combined with Dovecot LMTP / Sieve](#SpamAssassin_combined_with_Dovecot_LMTP_/_Sieve)
    *   [6.3 Rule-based mail processing](#Rule-based_mail_processing)
    *   [6.4 Sender Policy Framework](#Sender_Policy_Framework)
    *   [6.5 Sender Rewriting Scheme](#Sender_Rewriting_Scheme)
*   [7 Troubleshooting](#Troubleshooting_2)
    *   [7.1 Warning: "database /etc/postfix/*.db is older than source file .."](#Warning:_"database_/etc/postfix/*.db_is_older_than_source_file_..")
*   [8 See also](#See_also)

## 安装

[安装](/index.php/Install "Install") 软件包 [postfix](https://www.archlinux.org/packages/?name=postfix)。

## 配置

请参照软件开发者提供的： [Postfix Basic Configuration 基础配置项](http://www.postfix.org/BASIC_CONFIGURATION_README.html). 默认的配置文件位于`/etc/postfix` 。 其中两个非常重要的文件是:

*   `master.cf`, 定义了启用哪些Postfix服务以及客户端如何连接它们, 请参照 [master(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/master.5)
*   `main.cf`, 主配置文件，请参照 [postconf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/postconf.5)（英文）

配置文件更改过后需要 [重新加载](/index.php/Reload "Reload") 主服务 `postfix.service`。

### 别名 Aliases

请参照在线 man 文件： [aliases(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/postfix/aliases.5.en)。

别名配置文件： `/etc/postfix/aliases`。你可以在这个文件里指定别名 (有时候也被称为 forwarders ) 。

您需要将发往“root”的所有邮件映射到另一个帐户，因为以root身份阅读邮件不是一个好主意。

将下面这行取消注释，并且把 `you` 替换成你要使用的真实账户。

```
root: you

```

一旦你完成了对 `/etc/postfix/aliases` 的编辑， 你就需要运行下面的 postalias 命令:

```
postalias /etc/postfix/aliases

```

对于以后的更改，您可以使用:

```
newaliases

```

**提示：** 或者，你也可以为 root 用户创建这个文件 `~/.forward`, 例如 `/root/.forward`。 指定将root的邮件转发到哪个用户, 例如 *user@localhost*。 `/root/.forward` 
```
user@localhost

```

### 系统本地用户邮件(Local mail)

要仅向本地系统用户（也就是`/etc/passwd`中存在的用户）发送邮件，请更新配置文件：`/etc/postfix/main.cf`中的以下配置行（取消注释，更改或添加）:

```
myhostname = localhost
mydomain = localdomain
mydestination = $myhostname, localhost.$mydomain, $mydomain
inet_interfaces = $myhostname, localhost
mynetworks_style = host
default_transport = error: outside mail is not deliverable

```

所有其他设置维持不变。 完成上面这个配置后，你可能还想配置一些[#别名 Aliases](#别名_Aliases)参数，然后[#启动 Postfix](#启动_Postfix)。

### 虚拟用户邮件(Virtual mail)

虚拟用户邮件的邮件账户不存储在本地系统的(`/etc/passwd`文件中。可以配合数据库完成对用户账户的存储。

请参见 [Virtual user mail system with Postfix, Dovecot and Roundcube (简体中文)](/index.php/Virtual_user_mail_system_with_Postfix,_Dovecot_and_Roundcube_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Virtual user mail system with Postfix, Dovecot and Roundcube (简体中文)") 那是一个如何设置的详细介绍。

### 检查配置 Check configuration

运行`postfix check` 命令来完成配置检查。它会输出所有你在配置文件中可能写错的东西。

运行`postconf`命令可以查看所有的配置。运行`postconf -n`命令可以查看与默认配置的区别。

## 启动 Postfix

**注意:** 即使你没有设置任何[#别名 Aliases](#别名_Aliases)，也需要至少运行一次`newaliases`命令才能让 Postfix 正常运行。

[启动](/index.php/Start/enable "Start/enable") `postfix.service` 服务。

## TLS

**Warning:** If you deploy [TLS](https://en.wikipedia.org/wiki/TLS "wikipedia:TLS"), be sure to follow [weakdh.org's guide](https://weakdh.org/sysadmin.html) to prevent FREAK/Logjam. Since mid-2015, the default settings have been safe against [POODLE](https://en.wikipedia.org/wiki/POODLE "wikipedia:POODLE"). For more information see [Server-side TLS](/index.php/Server-side_TLS "Server-side TLS").

You need to [obtain a certificate](/index.php/Obtain_a_certificate "Obtain a certificate").

For more information, see [Postfix TLS Support](http://www.postfix.org/TLS_README.html).

### Secure SMTP (sending)

By default, Postfix/sendmail will not send email encrypted to other SMTP servers. To use TLS when available, add the following line to `main.cf`:

 `/etc/postfix/main.cf`  `smtp_tls_security_level = may` 

To *enforce* TLS (and fail when the remote server does not support it), change `may` to `encrypt`. Note, however, that this violates [RFC:2487](https://tools.ietf.org/html/rfc2487 "rfc:2487") if the SMTP server is publicly referenced.

### Secure SMTP (receiving)

By default, Postfix will not accept secure mail.

To enable STARTTLS over SMTP (port 587, the proper way of securing SMTP), add the following lines to `main.cf`

 `/etc/postfix/main.cf` 
```
smtpd_tls_security_level = may
smtpd_tls_cert_file = **/path/to/cert.pem**
smtpd_tls_key_file = **/path/to/key.pem**
```

In `master.cf`, find and uncomment the following lines to enable the service on that port with the correct settings:

 `/etc/postfix/master.cf` 
```
submission inet n       -       n       -       -       smtpd
  -o syslog_name=postfix/submission
  -o smtpd_tls_security_level=encrypt
  -o smtpd_sasl_auth_enable=yes
  -o smtpd_tls_auth_only=yes
  -o smtpd_reject_unlisted_recipient=no
#  -o smtpd_client_restrictions=$mua_client_restrictions
#  -o smtpd_helo_restrictions=$mua_helo_restrictions
#  -o smtpd_sender_restrictions=$mua_sender_restrictions
  -o smtpd_recipient_restrictions=
  -o smtpd_relay_restrictions=permit_sasl_authenticated,reject
  -o milter_macro_daemon_name=ORIGINATING
```

The `smtpd_*_restrictions` options remain commented because `$mua_*_restrictions` are not defined in main.cf by default. If you do decide to set any of `$mua_*_restrictions`, uncomment those lines too.

If you need support for the deprecated SMTPS port 465, also follow the next section.

#### SMTPS (port 465)

The deprecated method of securing SMTP is using the **wrapper mode** which uses the system service **smtps** as a non-standard service and runs on port 465.

To enable it, uncomment the following lines in `master.cf`:

 `/etc/postfix/master.cf` 
```
smtps     inet  n       -       n       -       -       smtpd
  -o syslog_name=postfix/smtps
  -o smtpd_tls_wrappermode=yes
  -o smtpd_sasl_auth_enable=yes
  -o smtpd_reject_unlisted_recipient=no
#  -o smtpd_client_restrictions=$mua_client_restrictions
#  -o smtpd_helo_restrictions=$mua_helo_restrictions
#  -o smtpd_sender_restrictions=$mua_sender_restrictions
  -o smtpd_recipient_restrictions=
  -o smtpd_relay_restrictions=permit_sasl_authenticated,reject
  -o milter_macro_daemon_name=ORIGINATING

```

The rationale surrounding the `$smtpd_*_restrictions` lines is the same as above.

After this, verify that these lines are in `/etc/services`:

```
smtps 465/tcp # Secure SMTP
smtps 465/udp # Secure SMTP

```

If they are not there, go ahead and add them (replace the other listing for port 465). Otherwise Postfix will not start and you will get the following error:

```
*postfix/master[5309]: fatal: 0.0.0.0:smtps: Servname not supported for ai_socktype*

```

## Tips and tricks

### Blacklist incoming emails

Manually blacklisting incoming emails by sender address can easily be done with Postfix.

Create and open `/etc/postfix/blacklist_incoming` file and append sender email address:

```
user@example.com REJECT

```

Then use the `postmap` command to create a database:

```
# postmap hash:blacklist_incoming

```

Add the following code before the first permit rule in `main.cf`:

```
smtpd_recipient_restrictions = check_sender_access hash:/etc/postfix/blacklist_incoming

```

Finally [restart](/index.php/Restart "Restart") `postfix.service`.

### Hide the sender's IP and user agent in the Received header

This is a privacy concern mostly, if you use Thunderbird and send an email. The received header will contain your LAN and WAN IP and info about the email client you used. (Original source: [AskUbuntu](http://askubuntu.com/questions/78163/when-sending-email-with-postfix-how-can-i-hide-the-senders-ip-and-username-in)) What we want to do is remove the Received header from outgoing emails. This can be done by the following steps:

Add the following line to `main.cf`:

```
smtp_header_checks = regexp:/etc/postfix/smtp_header_checks

```

Create `/etc/postfix/smtp_header_checks` with this content:

```
/^Received: .*/     IGNORE
/^User-Agent: .*/   IGNORE

```

Finally, [restart](/index.php/Restart "Restart") `postfix.service`.

### Postfix in a chroot jail

Postfix is not put in a chroot jail by default. The Postfix documentation [[1]](http://www.postfix.org/BASIC_CONFIGURATION_README.html#chroot_setup) provides details about how to accomplish such a jail. The steps are outlined below and are based on the chroot-setup script provided in the Postfix source code.

First, go into the `master.cf` file in the directory `/etc/postfix` and change all the chroot entries to 'yes' (y) except for the services `qmgr`, `proxymap`, `proxywrite`, `local`, and `virtual`

Second, create two functions that will help us later with copying files over into the chroot jail (see last step)

```
CP="cp -p"

```

```
cond_copy() {
  # find files as per pattern in $1
  # if any, copy to directory $2
  dir=`dirname "$1"`
  pat=`basename "$1"`
  lr=`find "$dir" -maxdepth 1 -name "$pat"`
  if test ! -d "$2" ; then exit 1 ; fi
  if test "x$lr" != "x" ; then $CP $1 "$2" ; fi
}

```

Next, make the new directories for the jail:

```
set -e
umask 022

```

```
POSTFIX_DIR=${POSTFIX_DIR-/var/spool/postfix}
cd ${POSTFIX_DIR}

```

```
mkdir -p etc lib usr/lib/zoneinfo
test -d /lib64 && mkdir -p lib64

```

Find the localtime file

```
lt=/etc/localtime
if test ! -f $lt ; then lt=/usr/lib/zoneinfo/localtime ; fi
if test ! -f $lt ; then lt=/usr/share/zoneinfo/localtime ; fi
if test ! -f $lt ; then echo "cannot find localtime" ; exit 1 ; fi
rm -f etc/localtime

```

Copy localtime and some other system files into the chroot's etc

```
$CP -f $lt /etc/services /etc/resolv.conf /etc/nsswitch.conf etc
$CP -f /etc/host.conf /etc/hosts /etc/passwd etc
ln -s -f /etc/localtime usr/lib/zoneinfo

```

Copy required libraries into the chroot using the previously created function `cond_copy`

```
cond_copy '/usr/lib/libnss_*.so*' lib
cond_copy '/usr/lib/libresolv.so*' lib
cond_copy '/usr/lib/libdb.so*' lib

```

And don't forget to reload Postfix.

### DANE (DNSSEC)

#### Resource Record

**Warning:** This is not a trivial section. Be aware that you make sure you know what you are doing. You better read [Common Mistakes](https://dane.sys4.de/common_mistakes) before.

[DANE](/index.php/DANE "DANE") supports several types of records, however not all of them are suitable in Postfix.

Certificate usage 0 is unsupported, 1 is mapped to 3 and 2 is optional, thus it is recommendet to publish a "3" record. More on [Resource Records](/index.php/DANE#Resource_Record "DANE").

#### Configuration

Opportunistic DANE is configured this way:

 `/etc/postfix/main.cf` 
```
smtpd_use_tls = yes
smtp_dns_support_level = dnssec
smtp_tls_security_level = dane

```
 `/etc/postfix/master.cf` 
```
dane       unix  -       -       n       -       -       smtp
  -o smtp_dns_support_level=dnssec
  -o smtp_tls_security_level=dane

```

To use per-domain policies, e.g. opportunistic DANE for example.org and mandatory DANE for example.com, use something like this:

 `/etc/postfix/main.cf` 
```
indexed = ${default_database_type}:${config_directory}/

# Per-destination TLS policy
#
smtp_tls_policy_maps = ${indexed}tls_policy

# default_transport = smtp, but some destinations are special:
#
transport_maps = ${indexed}transport

```
 `transport` 
```
example.com dane
example.org dane

```
 `tls_policy` 
```
example.com dane-only

```

**Note:** For global mandatory DANE, change `smtp_tls_security_level` to `dane-only`. Be aware that this makes Postfix tempfail (respond with a `4.X.X` error code) on all deliveries that do not use DANE at all!

Full documentation is found [here](http://www.postfix.org/TLS_README.html#client_tls_dane).

## Extras

*   **[PostfixAdmin](/index.php/PostfixAdmin "PostfixAdmin")** — A web-based administrative interface for Postfix.

	[http://postfixadmin.sourceforge.net/](http://postfixadmin.sourceforge.net/) || [postfixadmin](https://www.archlinux.org/packages/?name=postfixadmin)

### Postgrey

[Postgrey](http://postgrey.schweikert.ch/) can be used to enable [greylisting](https://en.wikipedia.org/wiki/Greylisting "wikipedia:Greylisting") for a Postfix mail server.

#### Installation

[Install](/index.php/Install "Install") the [postgrey](https://www.archlinux.org/packages/?name=postgrey) package. To get it running quickly edit the Postfix configuration file and add these lines:

 `/etc/postfix/main.cf` 
```
smtpd_recipient_restrictions =
  check_policy_service inet:127.0.0.1:10030

```

Then [start/enable](/index.php/Start/enable "Start/enable") the `postgrey` service. Afterwards, reload the `postfix` service. Now greylisting should be enabled.

#### Configuration

Configuration is done via editing the `postgrey.service` file. First copy it over to edit it.

```
# cp /usr/lib/systemd/system/postgrey.service /etc/systemd/system/

```

#### Whitelisting

To add automatic whitelisting (successful deliveries are whitelisted and don't have to wait any more), you could add the `--auto-whitelist-clients=N` option and replace `N` by a suitably small number (or leave it at its default of 5).

...actually, the preferred method should be the override:

```
cat /etc/systemd/system/postgrey.service.d/override.conf

```

```
[Service]
ExecStart=
ExecStart=/usr/bin/postgrey --inet=127.0.0.1:10030 \
       --pidfile=/run/postgrey/postgrey.pid \
       --group=postgrey --user=postgrey \
       --daemonize \
       --greylist-text="Greylisted for %%s seconds" \
       --auto-whitelist-clients

```

To add your own list of whitelisted clients in addition to the default ones, create the file `/etc/postfix/whitelist_clients.local` and enter one host or domain per line, then restart `postgrey.service` so the changes take effect.

#### Troubleshooting

If you specify `--unix=/path/to/socket` and the socket file is not created ensure you have removed the default `--inet=127.0.0.1:10030` from the service file.

For a full documentation of possible options see `perldoc postgrey`.

### SpamAssassin

This section describes how to integrate [SpamAssassin](/index.php/SpamAssassin "SpamAssassin").

#### SpamAssassin stand-alone generic setup

**Note:** If you want to combine SpamAssassin and Dovecot Mail Filtering, ignore the next two lines and continue further down instead.

Edit `/etc/postfix/master.cf` and add the content filter under smtp.

```
smtp      inet  n       -       n       -       -       smtpd
  -o content_filter=spamassassin
```

Also add the following service entry for SpamAssassin

```
spamassassin unix -     n       n       -       -       pipe
  flags=R user=spamd argv=/usr/bin/vendor_perl/spamc -e /usr/bin/sendmail -oi -f ${sender} ${recipient}
```

Now you can [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `spamassassin.service`.

#### SpamAssassin combined with Dovecot LDA / Sieve (Mailfiltering)

Set up LDA and the Sieve-Plugin as described in [Dovecot#Sieve](/index.php/Dovecot#Sieve "Dovecot"). But ignore the last line `mailbox_command...` .

Instead add a pipe in `/etc/postfix/master.cf`:

```
 dovecot   unix  -       n       n       -       -       pipe
       flags=DRhu user=vmail:vmail argv=/usr/bin/vendor_perl/spamc -u spamd -e /usr/lib/dovecot/dovecot-lda -f ${sender} -d ${recipient}

```

And activate it in `/etc/postfix/main.cf`:

```
 virtual_transport = dovecot

```

#### SpamAssassin combined with Dovecot LMTP / Sieve

Set up the LMTP and Sieve as described in [Dovecot#Sieve](/index.php/Dovecot#Sieve "Dovecot").

Edit `/etc/dovecot/conf.d/90-plugins.conf` and add:

```
 sieve_before = /etc/dovecot/sieve.before.d/
 sieve_extensions = +vnd.dovecot.filter
 sieve_plugins = sieve_extprograms
 sieve_filter_bin_dir = /etc/dovecot/sieve-filter
 sieve_filter_exec_timeout = 120s #this is often needed for the long running spamassassin scans, default is otherwise 10s

```

Create the directory and put spamassassin in as a binary that can be ran by dovecot:

```
 # mkdir /etc/dovecot/sieve-filter
 # ln -s /usr/bin/vendor_perl/spamc /etc/dovecot/sieve-filter/spamc

```

Create a new file, `/etc/dovecot/sieve.before.d/spamassassin.sieve` which contains:

```
 require [ "vnd.dovecot.filter" ];
 filter "spamc" [ "-d", "127.0.0.1", "--no-safe-fallback" ];

```

Compile the sieve rules `spamassassin.svbin`:

```
 # cd /etc/dovecot/sieve.before.d
 # sievec spamassassin.sieve

```

Finally, [restart](/index.php/Restart "Restart") `dovecot.service`.

### Rule-based mail processing

With policy services one can easily finetune Postfix' behaviour of mail delivery. [postfwd](https://www.archlinux.org/packages/?name=postfwd) and [policyd](https://aur.archlinux.org/pkgbase/policyd) provide services to do so. This allows you to e.g. implement time-aware grey- and blacklisting of senders and receivers as well as [SPF](/index.php/SPF "SPF") policy checking.

Policy services are standalone services and connected to Postfix like this:

 `/etc/postfix/main.cf` 
```
smtpd_recipient_restrictions =
  ...
  check_policy_service unix:/run/policyd.sock
  check_policy_service inet:127.0.0.1:10040

```

Placing policy services at the end of the queue reduces load, as only legitimate mails are processed. Be sure to place it before the first permit statement to catch all incoming messages.

### Sender Policy Framework

To use the [Sender Policy Framework](/index.php/Sender_Policy_Framework "Sender Policy Framework") with Postfix, [install](/index.php/Install "Install") [python-postfix-policyd-spf](https://aur.archlinux.org/packages/python-postfix-policyd-spf/).

Edit `/etc/python-policyd-spf/policyd-spf.conf` to your needs. An extensively commented version can be found at `/etc/python-policyd-spf/policyd-spf.conf.commented`. Pay some extra attention to the HELO check policy, as standard settings strictly reject HELO failures.

In the main.cf add a timeout for the policyd:

 `/etc/postfix/main.cf`  `policy-spf_time_limit = 3600s` 

Then add a transport

 `/etc/postfix/master.cf` 
```
policy-spf  unix  -       n       n       -       0       spawn
     user=nobody argv=/usr/bin/policyd-spf
```

Lastly you need to add the policyd to the `smtpd_recipient_restrictions`. To minimize load put it to the end of the restrictions but above any `reject_rbl_client` DNSBL line:

 `/etc/postfix/main.cf` 
```
smtpd_recipient_restrictions=
     ...
     permit_sasl_authenticated
     permit_mynetworks
     reject_unauth_destination
     check_policy_service unix:private/policy-spf
```

You can test your Setup with the following:

 `/etc/python-policyd-spf/policyd-spf.conf`  `defaultSeedOnly = 0` 

### Sender Rewriting Scheme

To use the [Sender Rewriting Scheme](/index.php/Sender_Rewriting_Scheme "Sender Rewriting Scheme") with Postfix, [install](/index.php/Install "Install") [postsrsd](https://aur.archlinux.org/packages/postsrsd/) and adjust the settings:

 `/etc/postsrsd/postsrsd` 
```
SRS_DOMAIN=yourdomain.tld
SRS_EXCLUDE_DOMAINS=yourotherdomain.tld,yet.anotherdomain.tld
SRS_SEPARATOR==
SRS_SECRET=/etc/postsrsd/postsrsd.secret
SRS_FORWARD_PORT=10001
SRS_REVERSE_PORT=10002
RUN_AS=postsrsd
CHROOT=/usr/lib/postsrsd
```

Enable and start the daemon, making sure it runs after reboot as well. Then configure Postfix accordingly by tweaking the following lines:

 `/etc/postfix/main.cf` 
```
sender_canonical_maps = tcp:localhost:10001
sender_canonical_classes = envelope_sender
recipient_canonical_maps = tcp:localhost:10002
recipient_canonical_classes= envelope_recipient,header_recipient
```

Restart Postfix and start forwarding mail.

## Troubleshooting

### Warning: "database /etc/postfix/*.db is older than source file .."

If you get one or both warnings with `journalctl`

```
warning: database /etc/postfix/virtual.db is older than source file /etc/postfix/virtual
warning: database /etc/postfix/transport.db is older than source file /etc/postfix/transport

```

then you can fix it by using these commands depending on the messages you get

```
postmap /etc/postfix/transport
postmap /etc/postfix/virtual

```

and restart `postfix.service`

## See also

*   [Official documentation](http://www.postfix.org/documentation.html)
*   [Postfix Ubuntu documentation](https://help.ubuntu.com/community/Postfix)
*   [Out of Office](http://linox.be/index.php/2005/07/13/44/) for Squirrelmail