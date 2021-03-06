Related articles

*   [Dovecot](/index.php/Dovecot "Dovecot")
*   [Postfix](/index.php/Postfix "Postfix")
*   [Exim](/index.php/Exim "Exim")

[OpenSMTPD](https://www.opensmtpd.org/) is a free [mail transfer agent](/index.php/Mail_transfer_agent "Mail transfer agent"), developed as part of the OpenBSD project. This article builds upon [Mail server](/index.php/Mail_server "Mail server").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Local mail](#Local_mail)
        *   [2.1.1 Local mail only](#Local_mail_only)
        *   [2.1.2 Hybrid : local mail and relay](#Hybrid_:_local_mail_and_relay)
        *   [2.1.3 Relay only](#Relay_only)
    *   [2.2 Simple OpenSMTPD/mbox configuration](#Simple_OpenSMTPD/mbox_configuration)
        *   [2.2.1 TLS](#TLS)
        *   [2.2.2 Create user accounts](#Create_user_accounts)
        *   [2.2.3 Craft a simple smtpd.conf setup](#Craft_a_simple_smtpd.conf_setup)
        *   [2.2.4 Create tables](#Create_tables)
    *   [2.3 Test the configuration](#Test_the_configuration)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Console debugging](#Console_debugging)
    *   [3.2 Subsystem tracing](#Subsystem_tracing)
    *   [3.3 Manual Submission port authentication](#Manual_Submission_port_authentication)
    *   [3.4 "Helo command rejected: need fully-qualified hostname"](#"Helo_command_rejected:_need_fully-qualified_hostname")
    *   [3.5 System users authentication failure](#System_users_authentication_failure)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd) package.

## Configuration

OpenSMTPD is configured in `/etc/smtpd/`.

**Note:** Starting with OpenSMTPD [version 6.4.0](https://www.opensmtpd.org/announces/release-6.4.0.txt) the configuration file syntax has been completely reworked, breaking compatibility with previous configuration files. For instruction on migrating the configuration to the new syntax see [https://poolp.org/posts/2018-05-21/switching-to-opensmtpd-new-config/](https://poolp.org/posts/2018-05-21/switching-to-opensmtpd-new-config/).

### Local mail

To have local mail working, for example for [cron](/index.php/Cron "Cron") mails, it is enough to simply [start](/index.php/Start "Start") `smtpd.service`.

The default configuration of OpenSMTPD is to do local retrieval and delivery of mail, and also relay outgoing mail. See [smtpd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/smtpd.conf.5).

#### Local mail only

To do only local mail, the following is enough:

 `/etc/smtpd/smtpd.conf` 
```
listen on localhost
action "local" mbox alias <aliases>
match for local action "local"

```

#### Hybrid : local mail and relay

These two lines in `/etc/smtpd/smtpd.conf` :

```
action "local" mbox alias <aliases>
action "relay" relay host "smtp://smtp.foo.bar" mail-from "@foo.bar"
match for local action "local"
match for any action "relay"

```

configure OpenSMTPD to :

*   send local email *locally*, without going through a relay (useful for cron & at mail notifications)

*   use a relay to send a mail outside of localhost

Simply replace *smtp.foo.bar* by your ISP mail server, or another server at your convenience.

#### Relay only

To send all local emails through a relay invoke [procmail](/index.php/Procmail "Procmail"):

 `/etc/smtpd/smtpd.conf` 
```
action "local" mda "procmail -f -" virtual <aliases>
action "relay" relay host "smtps://label@smtp.foo.bar" auth <secrets> mail-from "@foo.bar"
match for local action "local"
match for any action "relay"

```

The aliases option is used for the local user mapping, for a simplified mapping you can use virtual aliases with a catch all:

 `/etc/smtpd/aliases` 
```
@ foo@bar

```

### Simple OpenSMTPD/mbox configuration

#### TLS

To obtain a certificate, see [OpenSSL#Usage](/index.php/OpenSSL#Usage "OpenSSL").

**Note:** OpenSMTPD has solid defaults, SSLv3 is always disabled and the default `ciphers` are not known to be insecure. You might still want to test the server as described in [Server-side TLS](/index.php/Server-side_TLS "Server-side TLS").

#### Create user accounts

*   Create a user account on the mail server for each desired mailbox.

```
# useradd -m -s /bin/bash roger
# useradd -m -s /bin/bash shirley

```

*   OpenSMTPD will deliver messages to the user account's mbox file at `/var/spool/mail/*<username>*`
*   Multiple SMTP email addresses can be routed to a given mbox if desired.

#### Craft a simple smtpd.conf setup

*   A working configuration can be had in as little as nine lines!

 `/etc/smtpd/smtpd.conf` 
```
pki mx.domain.tld cert         "/etc/smtpd/tls/smtpd.crt"
pki mx.domain.tld key          "/etc/smtpd/tls/smtpd.key"

table creds                    "/etc/smtpd/creds"
table vdoms                    "/etc/smtpd/vdoms"
table vusers                   "/etc/smtpd/vusers"

listen on eth0 tls pki mx.domain.tld
listen on eth0 port 465 smtps pki mx.domain.tld auth <creds>
listen on eth0 port 587 tls-require pki mx.domain.tld auth <creds>

action receive	mbox virtual <vusers>
action send relay

match from any for domain <vdoms> action receive
match for any action send

```

#### Create tables

*   For the domain table file; simply put one domain per line

 `/etc/smtpd/vdoms` 
```
personaldomain.org
businessname.com

```

*   For the user table file; list one inbound SMTP email address per line and then map it to an mbox user account name, SMTP email address, or any combination of the two on the right, separated by commas.

 `/etc/smtpd/vusers` 
```
roger@personaldomain.org          roger
newsletters@personaldomain.org    roger,roger.rulz@gmail.com

roger@businessname.com            roger
shirley@businessname.com          shirley
info@businessname.com             roger,shirley
contact@businessname.com          info@businessname.com

```

*   For the creds table file; put the user name in the 1st column and the password hash in the 2nd column

 `/etc/smtpd/creds` 
```
roger                              <password hash created using 'smtpctl encrypt' command>
shirley                            <password hash created using 'smtpctl encrypt' command>

```

### Test the configuration

```
# smtpd -n

```

If you get a message that says 'configuration OK' - you're ready to [rock and roll](/index.php/Systemd "Systemd"). If not, work on any configuration errors and try again.

## Troubleshooting

### Console debugging

If you're having problems with mail delivery, try [stopping](/index.php/Stop "Stop") the `smtpd.service` and launching the daemon manually with the 'do not daemonize' and 'verbose output' options. Then watch the console for errors.

```
# smtpd -dv

```

### Subsystem tracing

Add the `-T` flag to get real-time subsystem tracing

```
# smtpd -dv -T smtp

```

Alternately, use the `smtpctl trace *<subsystem>*` command if the daemon is already running. The trace output will appear in the console output above as well as the journalctl output for the smtpd.service. For example:

```
# smtpctl trace expand && smtpctl trace lookup

```

...will trace both aliases/virtual/forward expansion and user/credentials lookups

### Manual Submission port authentication

*   Encode username and password in base64

```
# printf '\0username\0password' | base64  

```

*   Connect to submission port using `openssl s_client` command

```
# openssl s_client -host mx.domain.tld -port 587 -starttls smtp

```

*   enter `ehlo myhostname` followed by `AUTH PLAIN`. Paste in the base64 string from step above after `334` response.

```
250 HELP
ehlo test.domain.tld
250-mx.hostname.tld Hello test.domain.tld [5.5.5.5], pleased to meet you
250-8BITMIME
250-ENHANCEDSTATUSCODES
250-SIZE 36700160
250-DSN
250-AUTH PLAIN LOGIN
250 HELP
AUTH PLAIN
334 
dXNlcm5hbWUAdXNlcm5hbWUAcGFzc3dvcmQ=
235 2.0.0: Authentication succeeded

```

### "Helo command rejected: need fully-qualified hostname"

When sending email, if you get this kind of messages, set your FQDN in the file `/etc/smtpd/mailname`. Otherwise, the server name is derived from the local [hostname](/index.php/Hostname "Hostname") returned by [gethostname(3p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gethostname.3p), either directly if it is a fully qualified domain name, or by retrieving the associated canonical name through [getaddrinfo(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/getaddrinfo.3).

### System users authentication failure

If you are using the system users and the authentication with valid credentials fails, you have to configure [PAM](/index.php/PAM "PAM"):

 `/etc/pam.d/smtpd` 
```
auth required pam_unix.so
account required pam_unix.so
password required pam_unix.so
session required pam_unix.so

```

## See also

*   [Wikipedia:OpenSMTPD](https://en.wikipedia.org/wiki/OpenSMTPD "wikipedia:OpenSMTPD")
*   OpenSMTPD pairs well with [Dovecot](/index.php/Dovecot "Dovecot"). Combine the two for a nice minimalist mailserver
*   [OpenSMTPD project page](http://opensmtpd.org/)
*   [Simple SMTP server with OpenSMTPD](https://coderwall.com/p/eejzja)