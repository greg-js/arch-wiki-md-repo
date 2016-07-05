This article explains how to install and configure a simple [OpenSMTPD](https://www.opensmtpd.org/) server.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Local mail](#Local_mail)
        *   [2.1.1 Local-only](#Local-only)
    *   [2.2 Simple OpenSMTPD/mbox configuration](#Simple_OpenSMTPD.2Fmbox_configuration)
        *   [2.2.1 Create encryption keys](#Create_encryption_keys)
        *   [2.2.2 Create user accounts](#Create_user_accounts)
        *   [2.2.3 Craft a simple smtpd.conf setup](#Craft_a_simple_smtpd.conf_setup)
        *   [2.2.4 Create tables](#Create_tables)
    *   [2.3 Test the configuration](#Test_the_configuration)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Console debugging](#Console_debugging)
    *   [3.2 Subsystem tracing](#Subsystem_tracing)
    *   [3.3 Manual Submission port authentication](#Manual_Submission_port_authentication)
    *   [3.4 Resources](#Resources)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

[opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd) is configured in `/etc/smtpd`.

### Local mail

To have local mail working, for example for [cron](/index.php/Cron "Cron") mails, it is enough to simply [start](/index.php/Start "Start") `smtpd.service`.

[The default configuration](http://man.openbsd.org/smtpd.conf#EXAMPLES) of OpenSMTPD is to do local retrieval and delivery of mail, and also relay outgoing mail.

#### Local-only

To do local-only mail, the following is enough:

 `/etc/smtpd/smtpd.conf` 
```
listen on localhost
accept for local alias <aliases> deliver to mbox

```

### Simple OpenSMTPD/mbox configuration

#### Create encryption keys

[openssl](https://www.archlinux.org/packages/?name=openssl) provides TLS support and is installed by default on Arch installations.

Create a private key and self-signed certificate. This is adequate for most installations that do not require a [CSR](https://en.wikipedia.org/wiki/Certificate_signing_request "wikipedia:Certificate signing request"):

```
# mkdir -m 700 /etc/smtpd/tls; cd /etc/smtpd/tls
# openssl req -new -x509 -nodes -newkey rsa:4096 -keyout smtpd.key -out smtpd.crt -days 1095
# chmod 400 smtpd.key; chmod 444 smtpd.crt

```

#### Create user accounts

*   Create a user account on the mail server for each desired mailbox.

```
# useradd -m -s /bin/bash roger
# useradd -m -s /bin/bash shirley

```

*   OpenSMTPD will deliver messages to the user account's mbox file at `/var/spool/mail/<username>`
*   Multiple SMTP email addresses can be routed to a given mbox if desired.

#### Craft a simple smtpd.conf setup

*   A working configuration can be had in as little as nine lines!

 `/etc/smtpd/smtpd.conf` 
```
pki mx.domain.tld certificate  "/etc/smtpd/tls/smtpd.crt"
pki mx.domain.tld key          "/etc/smtpd/tls/smtpd.key"

table creds                    "/etc/smtpd/creds"
table vdoms                    "/etc/smtpd/vdoms"
table vusers                   "/etc/smtpd/vusers"

listen on eth0 tls pki mx.domain.tld
listen on eth0 port 587 tls-require pki mx.domain.tld auth <creds>

accept from any for domain <vdoms> virtual <vusers> deliver to mbox
accept for any relay

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

If you're having problems with mail delivery, try stopping the smtpd.service and launching the daemon manually with the 'do not daemonize' and 'verbose output' options. Then watch the console for errors.

```
# systemctl stop smtpd.service
# smtpd -dv

```

### Subsystem tracing

Add the '-T' flag to get real-time subsystem tracing

```
# smtpd -dv -T smtp

```

Alternately, use the 'smtpctl trace <subsystem>' command if the daemon is already running. The trace output will appear in the console output above as well as the journalctl output for the smtpd.service. For example:

```
# smtpctl trace expand && smtpctl trace lookup

```

...will trace both aliases/virtual/forward expansion and user/credentials lookups

### Manual Submission port authentication

*   Encode username and password in base64

```
# printf 'username\0username\0password' | base64  

```

*   Connect to submission port using 'openssl s_client' command

```
# openssl s_client -host mx.domain.tld -port 587 -starttls smtp

```

*   enter 'ehlo myhostname' followed by 'AUTH PLAIN'. Paste in the base64 string from step above after '334' response.

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

### Resources

There are also several handy web sites that can help you test DNS records, deliverability, and encryption support

*   [MXToolBox](http://mxtoolbox.com/)
*   [IsMyEmailWorking.com](http://ismyemailworking.com/)
*   [MailTester](http://www.mail-tester.com/)
*   [TLS tests and tools](https://checktls.com/)
*   [STARTTLS.info](https://starttls.info/)
*   [Pingability Quick DNS Check](https://pingability.com/zoneinfo.jsp)

## See also

*   OpenSMTPD pairs well with [Dovecot](/index.php/Dovecot "Dovecot"). Combine the two for a nice minimalist mailserver
*   [OpenSMTPD project page](http://opensmtpd.org/)
*   [Simple SMTP server with OpenSMTPD](https://coderwall.com/p/eejzja)