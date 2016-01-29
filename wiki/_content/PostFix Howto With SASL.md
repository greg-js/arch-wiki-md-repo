# PostFix Howto With SASL

Related articles

*   [Postfix](/index.php/Postfix "Postfix")
*   [Dovecot](/index.php/Dovecot "Dovecot")

From [Postfix's site](http://www.postfix.org/SASL_README.html):

NaN

## Contents

*   [1 Introduction](#Introduction)
*   [2 Configuration with cyrus-sasl package](#Configuration_with_cyrus-sasl_package)
*   [3 Configuration with Dovecot](#Configuration_with_Dovecot)
*   [4 See also](#See_also)

## Introduction

In this article you will learn how to setup SASL authentication for [Postfix](/index.php/Postfix "Postfix").

Once Postfix is up and running you can add SASL authentication to avoid relaying. Only authenticated and trusted users will be able to send emails. This will avoid anonymous users to make spamming.

Since [postfix](https://www.archlinux.org/packages/?name=postfix) package in [extra] is already compiled with SASL support, to enable SASL authentication you have two choices:

*   Use [cyrus-sasl](https://www.archlinux.org/packages/?name=cyrus-sasl) package.
*   Or enable your already configured [Dovecot](/index.php/Dovecot "Dovecot") to handle Postfix authentication (as well as its own).

## Configuration with cyrus-sasl package

[Install](/index.php/Install "Install") [cyrus-sasl](https://www.archlinux.org/packages/?name=cyrus-sasl) from the [official repositories](/index.php/Official_repositories "Official repositories").

To enable SASL for accepting mail from other users, open the ["Message submission"](http://tools.ietf.org/html/rfc6409) port (TCP 587) in `/etc/postfix/master.cf`, by uncommenting these lines (which are there by default, just commented):

```
submission inet n       -       n       -       -       smtpd
  -o syslog_name=postfix/submission
  -o smtpd_tls_security_level=encrypt
  -o smtpd_sasl_auth_enable=yes
  -o smtpd_reject_unlisted_recipient=no
#  -o smtpd_client_restrictions=$mua_client_restrictions
#  -o smtpd_helo_restrictions=$mua_helo_restrictions
#  -o smtpd_sender_restrictions=$mua_sender_restrictions
  -o smtpd_recipient_restrictions=permit_sasl_authenticated,reject
  -o milter_macro_daemon_name=ORIGINATING

```

Note that this also enables SSL, so if you do not have a SSL certificate, keep the "smtpd_tls_security_level" option commented out.

The three restriction options (client, helo, sender) can also be left commented out, since smtpd_recipient_restrictions already handles SASL users.

Setup Postfix as you normally would and [start](/index.php/Daemons#Starting_manually "Daemons") it. If you want to start it at boot time see [Daemons#Starting on boot](/index.php/Daemons#Starting_on_boot "Daemons").

SASL can use different authentication methods. The default one is PAM (as configured in `/etc/conf.d/saslauthd`), but to set it up properly you have to create `/usr/lib/sasl2/smtpd.conf`:

```
pwcheck_method: saslauthd
mech_list: plain
log_level: 7

```

Now [restart](/index.php/Restart "Restart") postfix and saslauthd services.

Hopefully you should be able to telnet to your Postfix server with:

`telnet localhost 587`

You should then type:

`EHLO test.com`

This is roughly what you should see:

```
Trying 127.0.0.1...

Connected to localhost.localdomain
Escape character is '^]'

220 justin ESMTP Postfix
EHLO test.com
250-justin
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250-AUTH PLAIN OTP DIGEST-MD5 CRAM-MD5
250 8BITMIME

```

## Configuration with Dovecot

If you are using [Dovecot](/index.php/Dovecot "Dovecot") as your IMAP or POP mail server and your users already authenticate (with PAM maybe), then there is no need to configure another package.

Simply edit `/etc/postfix/master.cf` and add the following lines under the `submission` or `smtp` section (depending on what you are using):

```
  # SASL authentication with dovecot
  -o smtpd_sasl_auth_enable=yes
  -o smtpd_sasl_type=dovecot
  -o smtpd_sasl_path=private/auth
  -o smtpd_sasl_security_options=noanonymous
  -o smtpd_sasl_local_domain=$myhostname
  -o smtpd_client_restrictions=permit_sasl_authenticated,reject
  -o smtpd_recipient_restrictions=reject_non_fqdn_recipient,reject_unknown_recipient_domain,permit_sasl_authenticated,reject

```

Using this configuration implies that only authenticated users can send mails. You can see this from `smtpd_client_restrictions` option.

Now add the following to Dovecot configuration file in `/etc/dovecot/dovecot.conf`:

```
service auth {
  unix_listener /var/spool/postfix/private/auth {
    group = postfix
    mode = 0660
    user = postfix
  }
  user = root
}

```

As you can see a unix socket is created in `/var/spool/postfix/private/auth`, the same specified in `smtpd_sasl_path` option of `master.cf`

Finally [restart](/index.php/Restart "Restart") both postfix and dovecot services.

## See also

*   [Postfix SASL readme](http://www.postfix.org/SASL_README.html) in Postfix official documentation.

*   [SASL authentication with Dovecot](http://wiki2.dovecot.org/HowTo/PostfixAndDovecotSASL) in Dovecot official documentation.

*   [Centos Howto Postfix SASL](http://wiki.centos.org/HowTos/postfix_sasl)

Retrieved from "[https://wiki.archlinux.org/index.php?title=PostFix_Howto_With_SASL&oldid=409824](https://wiki.archlinux.org/index.php?title=PostFix_Howto_With_SASL&oldid=409824)"