Related articles

*   [Postfix with SASL](/index.php/Postfix_with_SASL "Postfix with SASL")
*   [Amavis](/index.php/Amavis "Amavis")
*   [Virtual user mail system](/index.php/Virtual_user_mail_system "Virtual user mail system")
*   [Courier MTA](/index.php/Courier_MTA "Courier MTA")
*   [Exim](/index.php/Exim "Exim")
*   [OpenSMTPD](/index.php/OpenSMTPD "OpenSMTPD")
*   [OpenDMARC](/index.php/OpenDMARC "OpenDMARC")
*   [OpenDKIM](/index.php/OpenDKIM "OpenDKIM")
*   [SOGo](/index.php/SOGo "SOGo")

From [Postfix's site](http://www.postfix.org/):

	Postfix attempts to be fast, easy to administer, and secure, while at the same time being sendmail compatible enough to not upset existing users. Thus, the outside has a sendmail-ish flavor, but the inside is completely different.

The goal of this article is to setup Postfix and explain what the basic configuration files do. There are instructions for setting up local system user-only delivery and a link to a guide for virtual user delivery.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 master.cf](#master.cf)
    *   [2.2 main.cf](#main.cf)
        *   [2.2.1 Default message and mailbox size limits](#Default_message_and_mailbox_size_limits)
    *   [2.3 Aliases](#Aliases)
    *   [2.4 Local mail](#Local_mail)
    *   [2.5 Virtual mail](#Virtual_mail)
    *   [2.6 DNS records](#DNS_records)
    *   [2.7 Check configuration](#Check_configuration)
*   [3 Start Postfix](#Start_Postfix)
*   [4 TLS](#TLS)
    *   [4.1 Secure SMTP (sending)](#Secure_SMTP_.28sending.29)
    *   [4.2 Secure SMTP (receiving)](#Secure_SMTP_.28receiving.29)
        *   [4.2.1 SMTPS (port 465)](#SMTPS_.28port_465.29)
*   [5 Extra](#Extra)
    *   [5.1 PostfixAdmin](#PostfixAdmin)
    *   [5.2 Blacklist incoming emails](#Blacklist_incoming_emails)
    *   [5.3 Postgrey](#Postgrey)
        *   [5.3.1 Installation](#Installation_2)
        *   [5.3.2 Configuration](#Configuration_2)
        *   [5.3.3 Whitelisting](#Whitelisting)
        *   [5.3.4 Troubleshooting](#Troubleshooting)
    *   [5.4 SpamAssassin](#SpamAssassin)
        *   [5.4.1 Spam Assassin rule update](#Spam_Assassin_rule_update)
        *   [5.4.2 SpamAssassin stand-alone generic setup](#SpamAssassin_stand-alone_generic_setup)
        *   [5.4.3 SpamAssassin combined with Dovecot LDA / Sieve (Mailfiltering)](#SpamAssassin_combined_with_Dovecot_LDA_.2F_Sieve_.28Mailfiltering.29)
        *   [5.4.4 SpamAssassin combined with Dovecot LMTP / Sieve](#SpamAssassin_combined_with_Dovecot_LMTP_.2F_Sieve)
        *   [5.4.5 Call ClamAV from SpamAssassin](#Call_ClamAV_from_SpamAssassin)
    *   [5.5 Using Razor](#Using_Razor)
    *   [5.6 Hide the sender's IP and user agent in the Received header](#Hide_the_sender.27s_IP_and_user_agent_in_the_Received_header)
    *   [5.7 Postfix in a chroot jail](#Postfix_in_a_chroot_jail)
    *   [5.8 Rule-based mail processing](#Rule-based_mail_processing)
    *   [5.9 DANE (DNSSEC)](#DANE_.28DNSSEC.29)
        *   [5.9.1 Resource Record](#Resource_Record)
        *   [5.9.2 Configuration](#Configuration_3)
    *   [5.10 Sender Policy Framework](#Sender_Policy_Framework)
    *   [5.11 Sender Rewriting Scheme](#Sender_Rewriting_Scheme)
*   [6 Troubleshooting](#Troubleshooting_2)
    *   [6.1 Warning: "database /etc/postfix/*.db is older than source file .."](#Warning:_.22database_.2Fetc.2Fpostfix.2F.2A.db_is_older_than_source_file_...22)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [postfix](https://www.archlinux.org/packages/?name=postfix) package.

## Configuration

### master.cf

`/etc/postfix/master.cf` is the master configuration file where you can specify which protocols will be served. It is also the place where you can put your new pipes e.g. to check for Spam!

It is recommended to enable secure SMTP as described in [#Secure SMTP (sending)](#Secure_SMTP_.28sending.29) and [#Secure SMTP (receiving)](#Secure_SMTP_.28receiving.29).

See [this page](http://www.postfix.org/TLS_README.html) for more information about encrypting outgoing and incoming email.

### main.cf

`/etc/postfix/main.cf` is the main configuration file where everything is configured. The settings below are recommended for virtual local-only delivery.

*   `myhostname` should be set if your mail server has multiple domains, and you do not want the primary domain to be the mail host. You should have both a DNS A record and an MX record point to this hostname.

	 `myhostname = mail.nospam.net` 

*   `mydomain` is usually the value of `myhostname`, minus the first part. If your domain is wonky, then just set it manually.

	 `mydomain = nospam.net` 

*   `myorigin` is where the email will be seen as being sent from. I usually set this to the value of `mydomain`. For simple servers, this works fine. This is for mail originating from a local account. Since we are not doing local delivery (except sending), then this is not really as important as it normally would be.

	 `myorigin = $mydomain` 

*   `mydestination` is the lookup for local users.

	 `mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain` 

*   `mynetworks` and `mynetworks_style` control relaying, and whom is allowed to. We do not want any relaying.

	For our sakes, we will simply set `mynetwork_style` to host, as we are trying to make a standalone Postfix host, that people will use webmail on. No relaying, no other MTA's. Just webmail.

	 `mynetworks_style = host` 

*   `relaydomains` controls the destinations that Postfix will relay TO. The default value is empty. This should be fine for now.

	 `relay_domains =` 

*   `home_mailbox` or `mail_spool_directory` control how mail is delivered/stored for the users.

	If set, `mail_spool_directory` specifies an absolute path where mail gets delivered. By default Postfix stores mails in `/var/spool/mail`.

	 `mail_spool_directory = /home/vmailer` 

	Alternatively, if set, `home_mailbox` specifies a mailbox relative to the user's home directory where mail gets delivered (eg: /home/vmailer).

	Courier-IMAP requires "Maildir" format, so you **must** set it like the following example with trailing slash:

	 `home_mailbox = Maildir/` 

#### Default message and mailbox size limits

Postfix imposes both message and mailbox size limits by default. The message_size_limit controls the maximum size in bytes of a message, including envelope information. (default 10240000) The mailbox_size_limit controls the maximum size of any local individual mailbox or maildir file. This limits the size of **any** file that is written to upon local delivery, **including files written by external commands** (i.e. procmail) that are executed by the local delivery agent. (default is 51200000, set to 0 for no limit) If bounced message notifications are generated, check the size of the local mailbox under `/var/spool/mail` and use postconf to check these size limits:

```
# postconf mailbox_size_limit
mailbox_size_limit = 51200000
# postconf message_size_limit
message_size_limit = 10240000

```

### Aliases

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

See [Virtual user mail system](/index.php/Virtual_user_mail_system "Virtual user mail system") for a comprehensive guide how to set it up.

### DNS records

See [Mail server#MX record](/index.php/Mail_server#MX_record "Mail server").

### Check configuration

Run the `postfix check` command. It should output anything that you might have done wrong in a config file.

To see all of your configs, type `postconf`. To see how you differ from the defaults, try `postconf -n`.

## Start Postfix

**Note:** You must run `newaliases` at least once for postfix to run, even if you did not set up any [#Aliases](#Aliases).

[Start/enable](/index.php/Start/enable "Start/enable") the `postfix.service`.

## TLS

**Warning:** If you deploy [TLS](https://en.wikipedia.org/wiki/TLS "wikipedia:TLS"), be sure to follow [weakdh.org's guide](https://weakdh.org/sysadmin.html) to prevent FREAK/Logjam. Since mid-2015, the default settings have been safe against [POODLE](https://en.wikipedia.org/wiki/POODLE "wikipedia:POODLE"). For more information see [Server-side TLS](/index.php/Server-side_TLS "Server-side TLS").

To obtain a certificate, see [OpenSSL#Certificates](/index.php/OpenSSL#Certificates "OpenSSL").

For more information, see [Postfix TLS Support](http://www.postfix.org/TLS_README.html).

### Secure SMTP (sending)

By default, Postfix/sendmail will not send email encrypted to other SMTP servers. To use TLS when available, add the following line to `main.cf`:

 `/etc/postfix/main.cf`  `smtp_tls_security_level = may` 

To *enforce* TLS (and fail when the remote server does not support it), change `may` to `encrypt`. Note, however, that this violates RFC 2487 if the SMTP server is publicly referenced.

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

## Extra

### PostfixAdmin

[PostfixAdmin](http://postfixadmin.sourceforge.net/) is a web interface for Postfix used to manage mailboxes, virtual domains and aliases.

To use PostfixAdmin, you need a working Apache/MySQL/PHP setup as described in [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server").

For IMAP functionality, you will need to install [php-imap](https://www.archlinux.org/packages/?name=php-imap) and uncomment `extension=imap` in `/etc/php/php.ini`.

Next, [install](/index.php/Install "Install") [postfixadmin](https://www.archlinux.org/packages/?name=postfixadmin).

Edit the PostfixAdmin configuration file:

 `/etc/webapps/postfixadmin/config.inc.php` 
```
$CONF['configured'] = true;
// correspond to dovecot maildir path /home/vmail/%d/%u 
$CONF['domain_path'] = 'YES';
$CONF['domain_in_mailbox'] = 'NO';
$CONF['database_type'] = 'mysqli';
$CONF['database_host'] = 'localhost';
$CONF['database_user'] = 'postfix_user';
$CONF['database_password'] = 'hunter2';
$CONF['database_name'] = 'postfix_db';

// globally change all instances of ''change-this-to-your.domain.tld'' 
// to an appropriate value

```

If installing dovecot and you changed the password scheme in dovecot (to SHA512-CRYPT for example), reflect that with postfix

 `/etc/webapps/postfixadmin/config.inc.php` 
```
$CONF['encrypt'] = 'dovecot:SHA512-CRYPT';

```

As of dovecot 2, dovecotpw has been deprecated. You will also want to ensure that your config reflects the new binary name.

 `/etc/webapps/postfixadmin/config.inc.php` 
```
$CONF['dovecotpw'] = "/usr/sbin/doveadm pw";

```

**Note:** For this to work it does not suffice to have dovecot installed, it also needs to be configured. See [Dovecot#Dovecot configuration](/index.php/Dovecot#Dovecot_configuration "Dovecot").

Create the Apache configuration file:

 `/etc/httpd/conf/extra/httpd-postfixadmin.conf` 
```
Alias /postfixadmin "/usr/share/webapps/postfixAdmin/public"
<Directory "/usr/share/webapps/postfixAdmin/public">
    DirectoryIndex index.html index.php
    AllowOverride All
    Options FollowSymlinks
    Require all granted
</Directory>

```

To only allow localhost access to postfixadmin (for heightened security), add this to the previous <Directory> directive:

```
   Order Deny,Allow
   Deny from all
   Allow from 127.0.0.1

```

Now, include httpd-postfixadmin.conf to `/etc/httpd/conf/httpd.conf`:

```
# PostfixAdmin configuration
Include conf/extra/httpd-postfixadmin.conf

```

Finally, navigate to [http://127.0.0.1:80/postfixadmin/setup.php](http://127.0.0.1:80/postfixadmin/setup.php) to finish the setup. Generate your setup password hash at the bottom of the page once it is done. Write the hash to the config file

 `/etc/webapps/postfixadmin/config.inc.php` 
```
$CONF['setup_password'] = 'yourhashhere';

```

Now you can create a superadmin account at [http://127.0.0.1:80/postfixadmin/setup.php](http://127.0.0.1:80/postfixadmin/setup.php)

**Note:** If you go to yourdomain/postfixadmin/setup.php and it says do not find config.inc.php, add `/etc/webapps/postfixadmin` to the `open_basedir` line in `/etc/php/php.ini`.

**Note:** If you get a blank page check the syntax of the file with `php -l /etc/webapps/postfixadmin/config.inc.php`.

### Blacklist incoming emails

Manually blacklisting incoming emails by sender address can easily be done with Postfix.

Create and open `/etc/postfix/blacklist_incoming` file and append sender email address:

```
user@blacklistdomain.com REJECT

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

### Postgrey

[Postgrey](http://postgrey.schweikert.ch/) can be used to enable greylisting for a Postfix mail server.

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

If you specify --unix=/path/to/socket and the socket file is not created ensure you have removed the default --inet=127.0.0.1:10030 from the service file.

For a full documentation of possible options see `perldoc postgrey`.

### SpamAssassin

Install the [spamassassin](https://www.archlinux.org/packages/?name=spamassassin) package.

Go over `/etc/mail/spamassassin/local.cf` and configure it to your needs.

#### Spam Assassin rule update

Update the SpamAssassin matching patterns and compile them:

```
# sa-update && sa-compile

```

You will want to run this periodically, the best way to do so is by setting up a [Systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers").

Create the following service, which will run these commands:

 `/etc/systemd/system/spamassassin-update.service` 
```
[Unit]
Description=spamassassin housekeeping stuff

[Service]
#User=spamd
#Group=spamd
Type=oneshot

# remove --allowplugins, if you do not want plugin updates from SA.
ExecStart=/bin/sh -c '/usr/bin/vendor_perl/sa-update --allowplugins && {\
 /usr/bin/vendor_perl/sa-compile --quiet;\
 /usr/bin/systemctl -q --no-block try-restart spamassassin.service; }'
SuccessExitStatus=1

# uncomment the following ExecStart line to train SA's bayes filter
# and specify the path to the mailbox that contains spam email(s)
#ExecStart=/usr/bin/vendor_perl/sa-learn --spam <path_to_your_spam_mailbox>
```

Then create the timer, which will execute the previous service daily:

 `/etc/systemd/system/spamassassin-update.timer` 
```
[Unit]
Description=spamassassin house keeping

[Timer]
OnCalendar=daily
Persistent=true

[Install]
WantedBy=timers.target
```

Now you can [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `spamassassin-update.timer`.

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

#### Call ClamAV from SpamAssassin

Install and setup clamd as described in [ClamAV](/index.php/ClamAV "ClamAV").

Follow one of the above instructions to call SpamAssassin from within your mail system.

[Install](/index.php/Install "Install") the [perl-cpanplus-dist-arch](https://www.archlinux.org/packages/?name=perl-cpanplus-dist-arch) package. Then install the ClamAV perl library as follows:

```
 # /usr/bin/vendor_perl/cpanp -i File::Scan::ClamAV

```

Add the 2 files from [http://wiki.apache.org/spamassassin/ClamAVPlugin](http://wiki.apache.org/spamassassin/ClamAVPlugin) into `/etc/mail/spamassassin/`. Edit `/etc/mail/spamassassin/clamav.pm` and update `$CLAM_SOCK` to point to your Clamd socket location (default is `/var/lib/clamav/clamd.sock`).

Finally, [restart](/index.php/Restart "Restart") `spamassassin.service`.

### Using Razor

Make sure you have installed SpamAssassin first, then:

[Install](/index.php/Install "Install") the [razor](https://www.archlinux.org/packages/?name=razor) package.

Register with Razor.

```
 # mkdir /etc/mail/spamassassin/razor
 # chown spamd:spamd /etc/mail/spamassassin/razor
 # sudo -u spamd -s
 $ cd /etc/mail/spamassassin/razor
 $ razor-admin -home=/etc/mail/spamassassin/razor -register
 $ razor-admin -home=/etc/mail/spamassassin/razor -create
 $ razor-admin -home=/etc/mail/spamassassin/razor -discover

```

Tell SpamAssassin about Razor, add

```
 razor_config /etc/mail/spamassassin/razor/razor-agent.conf

```

to `/etc/mail/spamassassin/local.cf`.

Tell Razor about itself, add

```
 razorhome = /etc/mail/spamassassin/razor/

```

to `/etc/mail/spamassassin/razor/razor-agent.conf`

Finally, [restart](/index.php/Restart "Restart") `spamassassin.service`.

### Hide the sender's IP and user agent in the Received header

This is a privacy concern mostly, if you use Thunderbird and send an email. The received header will contain your LAN and WAN IP and info about the email client you used. (Original source: [AskUbuntu](http://askubuntu.com/questions/78163/when-sending-email-with-postfix-how-can-i-hide-the-senders-ip-and-username-in)) What we want to do is remove the Received header from outgoing emails. This can be done by the following steps:

Add this line to main.cf

```
smtp_header_checks = regexp:/etc/postfix/smtp_header_checks

```

Create /etc/postfix/smtp_header_checks with this content:

```
/^Received: .*/     IGNORE
/^User-Agent: .*/   IGNORE

```

Finally, restart postfix.service

### Postfix in a chroot jail

Postfix is not put in a chroot jail by default. The Postfix documentation [[1]](http://www.postfix.org/BASIC_CONFIGURATION_README.html#chroot_setup) provides details about how to accomplish such a jail. The steps are outlined below and are based on the chroot-setup script provided in the postfix source code.

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

And don't forget to reload postfix.

### Rule-based mail processing

With policy services one can easily finetune postfix' behaviour of mail delivery. [postfwd](https://www.archlinux.org/packages/?name=postfwd) and [policyd](https://aur.archlinux.org/pkgbase/policyd) provide services to do so. This allows you to e.g. implement time-aware grey- and blacklisting of senders and receivers as well as [SPF](/index.php/SPF "SPF") policy checking.

Policy services are standalone services and connected to Postfix like this:

 `/etc/postfix/main.cf` 
```
smtpd_recipient_restrictions =
  ...
  check_policy_service unix:/run/policyd.sock
  check_policy_service inet:127.0.0.1:10040

```

Placing policy services at the end of the queue reduces load, as only legitimate mails are processed. Be sure to place it before the first permit statement to catch all incoming messages.

### DANE (DNSSEC)

#### Resource Record

**Warning:** This is not a trivial section. Be aware that you make sure you know what you are doing. You better read [Common Mistakes](https://dane.sys4.de/common_mistakes) before.

[DANE](/index.php/DANE "DANE") supports several types of records, however not all of them are suitable in postfix.

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

**Note:** For global mandatory DANE, change `smtp_tls_security_level` to `dane-only`. Be aware that this makes postfix tempfail on all delivieres that do not use DANE at all!

Full documentation is found [here](http://www.postfix.org/TLS_README.html#client_tls_dane).

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

Enable and start the daemon, making sure it runs after reboot as well. Then configure postfix accordingly by tweaking the following lines:

 `/etc/postfix/main.cf` 
```
sender_canonical_maps = tcp:localhost:10001
sender_canonical_classes = envelope_sender
recipient_canonical_maps = tcp:localhost:10002
recipient_canonical_classes= envelope_recipient,header_recipient
```

Restart postfix and start forwarding mail.

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

*   [Out of Office](http://linox.be/index.php/2005/07/13/44/) for Squirrelmail 
*   [Postfix Ubuntu documentation](https://help.ubuntu.com/community/Postfix)