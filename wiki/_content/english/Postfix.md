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
*   [4 Testing](#Testing)
    *   [4.1 Error response](#Error_response)
    *   [4.2 See that you have received a email](#See_that_you_have_received_a_email)
*   [5 Extra](#Extra)
    *   [5.1 PostfixAdmin](#PostfixAdmin)
    *   [5.2 Secure SMTP (sending)](#Secure_SMTP_.28sending.29)
    *   [5.3 Secure SMTP (receiving)](#Secure_SMTP_.28receiving.29)
        *   [5.3.1 STARTTLS over SMTP (port 587)](#STARTTLS_over_SMTP_.28port_587.29)
        *   [5.3.2 SMTPS (port 465)](#SMTPS_.28port_465.29)
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
        *   [5.9.2 Configuration](#Configuration_2)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [postfix](https://www.archlinux.org/packages/?name=postfix) package.

**Note:** A logging package like [syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng) must be set up before logs will appear in /var/log/mail.log

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

**Warning:** If you plan on implementing SSL/TLS, please respond safely to [FREAK/Logjam](https://weakdh.org/sysadmin.html) by adding the following to your configuration: `smtpd_tls_exclude_ciphers = aNULL, eNULL, EXPORT, DES, RC4, MD5, PSK, aECDH, EDH-DSS-DES-CBC3-SHA, EDH-RSA-DES-CBC3-SHA, KRB5-DES, CBC3-SHA` 

Then, generate a [dhparam file](https://www.openssl.org/docs/man1.0.2/apps/dhparam.html) by following [these instructions](https://weakdh.org/sysadmin.html) and then adding the following to your configuration:

 `smtpd_tls_dh1024_param_file = ${config_directory}/dhparams.pem` 

Since mid-2015, the default settings have been safe against [POODLE](http://disablessl3.com/).

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

An MX record should point to the mail host. Usually this is done from configuration interface of your domain provider.

A mail exchanger record (MX record) is a type of resource record in the Domain Name System that specifies a mail server responsible for accepting email messages on behalf of a recipient's domain.

When an e-mail message is sent through the Internet, the sending mail transfer agent queries the Domain Name System for MX records of each recipient's domain name. This query returns a list of host names of mail exchange servers accepting incoming mail for that domain and their preferences. The sending agent then attempts to establish an SMTP connection to one of these servers, starting with the one with the smallest preference number, delivering the message to the first server with which a connection can be made.

**Note:** Some mail servers will not deliver mail to you if your MX record points to a CNAME. For best results, always point an MX record to an A record definition. For more information, see e.g. [Wikipedia's List of DNS Record Types](https://en.wikipedia.org/wiki/List_of_DNS_record_types "wikipedia:List of DNS record types").

### Check configuration

Run the `postfix check` command. It should output anything that you might have done wrong in a config file.

To see all of your configs, type `postconf`. To see how you differ from the defaults, try `postconf -n`.

## Start Postfix

**Note:** You must run `newaliases` at least once for postfix to run, even if you did not set up any [#Aliases](#Aliases).

[Start/enable](/index.php/Start/enable "Start/enable") the `postfix.service`.

## Testing

Now lets see if Postfix is going to deliver mail for our test user.

```
nc servername 25
helo testmail.org
mail from:<test@testmail.org>
rcpt to:<cactus@virtualdomain.tld>
data
This is a test email.
.
quit

```

### Error response

```
451 4.3.0 <lisi@test.com>:Temporary lookup failure

```

Maybe you have entered the wrong user/password for MySQL or the MySQL socket is not in the right place.

This error will also occur if you neglect to run newaliases at least once before starting postfix. MySQL is not required for local only usage of postfix.

```
550 5.1.1 <email@spam.me>: Recipient address rejected: User unknown in virtual mailbox table.

```

Double check content of mysql_virtual_mailboxes.cf and check the main.cf for mydestination

### See that you have received a email

Now type `$ find /home/vmailer`.

You should see something like the following:

```
/home/vmailer/virtualdomain.tld/cactus@virtualdomain.tld
/home/vmailer/virtualdomain.tld/cactus@virtualdomain.tld/tmp
/home/vmailer/virtualdomain.tld/cactus@virtualdomain.tld/cur
/home/vmailer/virtualdomain.tld/cactus@virtualdomain.tld/new
/home/vmailer/virtualdomain.tld/cactus@virtualdomain.tld/new/1102974226.2704_0.bonk.testmail.org

```

The key is the last entry. This is an actual email, if you see that, it is working.

## Extra

### PostfixAdmin

To use PostfixAdmin, you need a working Apache/MySQL/PHP setup as described in [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server").

For IMAP functionality, you will need to install [php-imap](https://www.archlinux.org/packages/?name=php-imap) and uncomment imap.so in /etc/php/php.ini

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

Create the Apache configuration file:

 `/etc/httpd/conf/extra/httpd-postfixadmin.conf` 
```
Alias /postfixadmin "/usr/share/webapps/postfixAdmin"
<Directory "/usr/share/webapps/postfixAdmin">
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

**Note:** If you go to yourdomain/postfixadmin/setup.php and it says do not find config.inc.php, add `/etc/webapps/postfixadmin` to the `open_basedir` line in `/etc/php/php.ini`.

**Note:** If you get a blank page check the syntax of the file with `php -l /etc/webapps/postfixadmin/config.inc.php`.

### Secure SMTP (sending)

By default, Postfix/sendmail will not send email encrypted to other SMTP servers. To use TLS when available, add the following line to `main.cf`:

 `/etc/postfix/main.cf`  `smtp_tls_security_level = may` 

To *enforce* TLS (and fail when the remote server does not support it), change `may` to `encrypt`.

### Secure SMTP (receiving)

For more information, see [Postfix TLS Support](http://www.postfix.org/TLS_README.html).

#### STARTTLS over SMTP (port 587)

To enable STARTTLS over SMTP (port 587, the proper way of securing SMTP), add the following lines to `main.cf`

 `/etc/postfix/main.cf` 
```
smtpd_tls_security_level = may
smtpd_tls_cert_file = **/path/to/cert.pem**
smtpd_tls_key_file = **/path/to/key.pem**
```

Also in `master.cf` find and remove the comment from the following line to enable the service on that port:

 `/etc/postfix/master.cf`  `submission inet n       -       n       -       -       smtpd` 

If you need support for the deprecated SMTPS port 465, read the next section.

#### SMTPS (port 465)

The deprecated method of securing SMTP is using the **wrapper mode** which uses the system service **smtps** as a non-standard service and runs on port 465.

To enable it uncomment the following lines in

 `/etc/postfix/master.cf` 
```
smtps     inet  n       -       n       -       -       smtpd
  -o smtpd_tls_wrappermode=yes
  -o smtpd_sasl_auth_enable=yes

```

And verify that these lines are in `/etc/services`:

```
smtps 465/tcp # Secure SMTP
smtps 465/udp # Secure SMTP

```

If they are not there, go ahead and add them (replace the other listing for port 465). Otherwise Postfix will not start and you will get the following error:

```
*postfix/master[5309]: fatal: 0.0.0.0:smtps: Servname not supported for ai_socktype*

```

### SpamAssassin

Install the [spamassassin](https://www.archlinux.org/packages/?name=spamassassin) package.

Go over `/etc/mail/spamassassin/local.cf` and configure it to your needs.

#### Spam Assassin rule update

Update the SpamAssassin matching patterns and compile them:

```
# sa-update
# sa-compile

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
ExecStart=/usr/bin/vendor_perl/sa-update --allowplugins #You can remove the allowplugins options if you do not want direct plugin updates from SA.
SuccessExitStatus=0 1 #0 = updated, 1 = no updates available
ExecStart=/usr/bin/vendor_perl/sa-compile
SuccessExitStatus=0
# You can automatically train SA's bayes filter by uncommenting this line and specifying the path to a mailbox where you store email that is spam (for ex this could be yours or your users manually reported spam)
#ExecStart=/usr/bin/vendor_perl/sa-learn --spam <path to your spam>
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

Finally, you'll need to modify your Spamassassin systemd service file so that it knows to restart itself to read the new rules. Copy the bundled service file to a custom service file:

 `# cp /usr/lib/systemd/system/spamassassin.service /etc/systemd/system` 

And edit the newly created `/etc/systemd/system/spamassassin.service` to include:

```
[Unit]
PartOf=spamassassin-update.service
```

This will ensure that Spamassassin's spamd is restarted just before the timer runs. This means the rules will be available the next day if your timer runs daily. This is so that there is no long service interruption while `sa.service` runs as it takes a while to compile rules.

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

DANE supports several types of records, however not all of them are suitable in postfix.

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

## See also

*   [Out of Office](http://linox.be/index.php/2005/07/13/44/) for Squirrelmail
*   [Postfix Ubuntu documentation](https://help.ubuntu.com/community/Postfix)
*   [Use Gmail as an SMTP relay](http://sherlock.heroku.com/blog/2012/02/03/setting-up-postfix-to-use-gmail-as-an-smtp-relay-host-in-archlinux/)