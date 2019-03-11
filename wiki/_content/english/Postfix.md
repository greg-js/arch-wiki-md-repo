Related articles

*   [Postfix with SASL](/index.php/Postfix_with_SASL "Postfix with SASL")
*   [Virtual user mail system](/index.php/Virtual_user_mail_system "Virtual user mail system")
*   [OpenDMARC](/index.php/OpenDMARC "OpenDMARC")
*   [OpenDKIM](/index.php/OpenDKIM "OpenDKIM")

[Postfix](https://en.wikipedia.org/wiki/Postfix_(software) is a [mail transfer agent](/index.php/Mail_transfer_agent "Mail transfer agent") that according to [its website](http://www.postfix.org/):

	attempts to be fast, easy to administer, and secure, while at the same time being sendmail compatible enough to not upset existing users. Thus, the outside has a sendmail-ish flavor, but the inside is completely different.

This article builds upon [Mail server](/index.php/Mail_server "Mail server"). The goal of this article is to setup Postfix and explain what the basic configuration files do. There are instructions for setting up local system user-only delivery and a link to a guide for virtual user delivery.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Aliases](#Aliases)
    *   [2.2 Local mail](#Local_mail)
    *   [2.3 Virtual mail](#Virtual_mail)
    *   [2.4 Check configuration](#Check_configuration)
*   [3 Start Postfix](#Start_Postfix)
*   [4 TLS](#TLS)
    *   [4.1 Secure SMTP (sending)](#Secure_SMTP_(sending))
    *   [4.2 Secure SMTP (receiving)](#Secure_SMTP_(receiving))
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Blacklist incoming emails](#Blacklist_incoming_emails)
    *   [5.2 Hide the sender's IP and user agent in the Received header](#Hide_the_sender's_IP_and_user_agent_in_the_Received_header)
    *   [5.3 Postfix in a chroot jail](#Postfix_in_a_chroot_jail)
    *   [5.4 DANE (DNSSEC)](#DANE_(DNSSEC))
        *   [5.4.1 Resource Record](#Resource_Record)
        *   [5.4.2 Configuration](#Configuration_2)
*   [6 Extras](#Extras)
    *   [6.1 Postgrey](#Postgrey)
        *   [6.1.1 Installation](#Installation_2)
        *   [6.1.2 Configuration](#Configuration_3)
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

## Installation

[Install](/index.php/Install "Install") the [postfix](https://www.archlinux.org/packages/?name=postfix) package.

## Configuration

See [Postfix Basic Configuration](http://www.postfix.org/BASIC_CONFIGURATION_README.html). Configuration files are in `/etc/postfix` by default. The two most important files are:

*   `master.cf`, defines what Postfix services are enabled an what how clients connect to them, see [master(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/master.5)
*   `main.cf`, the main configuration file, see [postconf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/postconf.5)

Configuration changes need a `postfix.service` [reload](/index.php/Reload "Reload") in order to take effect.

### Aliases

See [aliases(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/postfix/aliases.5.en).

You can specify aliases (also known as forwarders) in `/etc/postfix/aliases`.

You need to map all mail addressed to *root* to another account since it is not a good idea to read mail as root.

Uncomment the following line, and change `you` to a real account.

```
root: you

```

Once you have finished editing `/etc/postfix/aliases` you must run the postalias command:

```
postalias /etc/postfix/aliases

```

For later changes you can use:

```
newaliases

```

**Tip:** Alternatively you can create the file `~/.forward`, e.g. `/root/.forward` for root. Specify the user to whom root mail should be forwarded, e.g. *user@localhost*. `/root/.forward` 
```
user@localhost

```

### Local mail

To only deliver mail to local system users (that are in `/etc/passwd`) update `/etc/postfix/main.cf` to reflect the following configuration. Uncomment, change, or add the following lines:

```
myhostname = localhost
mydomain = localdomain
mydestination = $myhostname, localhost.$mydomain, localhost
inet_interfaces = $myhostname, localhost
mynetworks_style = host
default_transport = error: outside mail is not deliverable

```

All other settings may remain unchanged. After setting up the above configuration file, you may wish to set up some [#Aliases](#Aliases) and then [#Start Postfix](#Start_Postfix).

### Virtual mail

Virtual mail is mail that does not map to a user account (`/etc/passwd`).

See [Virtual user mail system with Postfix, Dovecot and Roundcube](/index.php/Virtual_user_mail_system_with_Postfix,_Dovecot_and_Roundcube "Virtual user mail system with Postfix, Dovecot and Roundcube") for a comprehensive guide how to set it up.

### Check configuration

Run the `postfix check` command. It should output anything that you might have done wrong in a config file.

To see all of your configs, type `postconf`. To see how you differ from the defaults, try `postconf -n`.

## Start Postfix

**Note:** You must run `newaliases` at least once for Postfix to run, even if you did not set up any [#Aliases](#Aliases).

[Start/enable](/index.php/Start/enable "Start/enable") the `postfix.service`.

## TLS

For more information, see [Postfix TLS Support](http://www.postfix.org/TLS_README.html).

### Secure SMTP (sending)

By default, Postfix/sendmail will not send email encrypted to other SMTP servers. To use TLS when available, add the following line to `main.cf`:

 `/etc/postfix/main.cf`  `smtp_tls_security_level = may` 

To *enforce* TLS (and fail when the remote server does not support it), change `may` to `encrypt`. Note, however, that this violates [RFC:2487](https://tools.ietf.org/html/rfc2487 "rfc:2487") if the SMTP server is publicly referenced.

### Secure SMTP (receiving)

**Warning:** If you deploy [TLS](https://en.wikipedia.org/wiki/TLS "wikipedia:TLS"), be sure to follow [weakdh.org's guide](https://weakdh.org/sysadmin.html) to prevent FREAK/Logjam. Since mid-2015, the default settings have been safe against [POODLE](https://en.wikipedia.org/wiki/POODLE "wikipedia:POODLE"). For more information see [Server-side TLS](/index.php/Server-side_TLS "Server-side TLS").

By default, Postfix will not accept secure mail.

You need to [obtain a certificate](/index.php/Obtain_a_certificate "Obtain a certificate"). Point Postfix to your TLS certificates by adding the following lines to `main.cf`:

 `/etc/postfix/main.cf` 
```
smtpd_tls_security_level = may
smtpd_tls_cert_file = **/path/to/cert.pem**
smtpd_tls_key_file = **/path/to/key.pem**
```

There are two ways to accept secure mail. STARTTLS over SMTP (port 587) and SMTPS (port 465). The latter was previously deprecated but was reinstated by [RFC:8314](https://tools.ietf.org/html/rfc8314 "rfc:8314").

To enable STARTTLS over SMTP (port 587), uncomment the following lines in `master.cf`:

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

To enable SMTPS (port 465), uncomment the following lines in `master.cf`:

 `/etc/postfix/master.cf` 
```
**smtps**     inet  n       -       n       -       -       smtpd
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

And in the first line, replace `**smtps**` with `submissions`. (this is the official service name according to [IANA](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.txt); Postfix still references the old name)

The rationale surrounding the `$smtpd_*_restrictions` lines is the same as above.

**Note:** If you get an error message like `postfix/master[5309]: fatal: 0.0.0.0:smtps: Servname not supported for ai_socktype`, make sure that you have the following line in `postfix/master.cf`:
```
submissions inet n       -       n       -       -       smtpd

```

Also make sure that `/etc/services` is up to date and includes the following line:

```
submissions 465/tcp

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

And don't forget to [reload](/index.php/Reload "Reload") Postfix.

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

With policy services one can easily finetune Postfix' behaviour of mail delivery. [postfwd](https://www.archlinux.org/packages/?name=postfwd) and policyd ([policyd-mysql](https://aur.archlinux.org/packages/policyd-mysql/), [policyd-pgsql](https://aur.archlinux.org/packages/policyd-pgsql/) or [policyd-sqlite](https://aur.archlinux.org/packages/policyd-sqlite/)) provide services to do so. This allows you to e.g. implement time-aware grey- and blacklisting of senders and receivers as well as [SPF](/index.php/SPF "SPF") policy checking.

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

In `main.cf` file, add a timeout for the policyd:

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

If you get one or both warnings with `journalctl`:

```
warning: database /etc/postfix/virtual.db is older than source file /etc/postfix/virtual
warning: database /etc/postfix/transport.db is older than source file /etc/postfix/transport

```

Then you can fix it by using these commands, depending on the messages you get:

```
postmap /etc/postfix/transport
postmap /etc/postfix/virtual

```

And [restart](/index.php/Restart "Restart") `postfix.service`.

## See also

*   [Official documentation](http://www.postfix.org/documentation.html)
*   [Postfix Ubuntu documentation](https://help.ubuntu.com/community/Postfix)
*   [Out of Office](http://linox.be/index.php/2005/07/13/44/) for Squirrelmail