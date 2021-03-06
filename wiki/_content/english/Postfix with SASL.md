Related articles

*   [Postfix](/index.php/Postfix "Postfix")
*   [Dovecot](/index.php/Dovecot "Dovecot")

SMTP protocol specifications include a possibility for user authentication, but do not provide the exact details of protocol message exchange, deferring instead to the SASL (Simple Authentication and Security Layer) standard (see [RFC4954](https://tools.ietf.org/html/rfc4954) and [RFC4422](https://tools.ietf.org/html/rfc4422)). SASL is a generic authentication framework for authentication mechanisms, of which there are many, and each of them has its own peculiar procedure that prescribes the necessary cryptographic steps to perform with the authentication data and messages to exchange over the connection. Therefore, in order to avoid imposing artificial limits on what authentication mechanisms can be used with it, Postfix, by itself, does not authenticate SMTP users with usernames and passwords, or via any other means. It offloads this task to a SASL implementation, which has to be installed separately. SASL authentication daemon is responsible both for the policy (i.e. where valid usernames and secrets such as passwords are kept) and mechanism (how exactly clients supply credentials). This is in contrast with e.g. [OpenSMTPD](/index.php/OpenSMTPD "OpenSMTPD"), which supports only PLAIN and LOGIN SASL mechanisms, but does not rely on any external library or daemon.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Introduction](#Introduction)
*   [2 Configuration with cyrus-sasl package](#Configuration_with_cyrus-sasl_package)
*   [3 Configuration with Dovecot](#Configuration_with_Dovecot)
*   [4 See also](#See_also)

## Introduction

In this article you will learn how to setup SASL authentication for [Postfix](/index.php/Postfix "Postfix").

Once Postfix is up and running you can add SASL authentication to avoid relaying. In order to prevent anonymous users from spamming, only authenticated and trusted users will be able to send emails.

Since [postfix](https://www.archlinux.org/packages/?name=postfix) package in [extra] is already compiled with SASL support, to enable SASL authentication you have two choices:

*   Use [cyrus-sasl](https://www.archlinux.org/packages/?name=cyrus-sasl) package.
*   Or enable your already configured [Dovecot](/index.php/Dovecot "Dovecot") to handle Postfix authentication (as well as its own).

From [Postfix's site](http://www.postfix.org/SASL_README.html):

	People who go to the trouble of installing Postfix may have the expectation that Postfix is more secure than some other mailers. The Cyrus SASL library contains a lot of code. With this, Postfix becomes as secure as other mail systems that use the Cyrus SASL library. Dovecot provides an alternative that may be worth considering.

## Configuration with cyrus-sasl package

[Install](/index.php/Install "Install") the [cyrus-sasl](https://www.archlinux.org/packages/?name=cyrus-sasl) package.

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

SASL can use different authentication methods. The default one is PAM (as configured in `/etc/conf.d/saslauthd`), but to set it up properly you have to create `/etc/sasl2/smtpd.conf`:

```
pwcheck_method: saslauthd
mech_list: PLAIN LOGIN
log_level: 7

```

Since pambase 20190105.1-1 and newer uses restrictive fallback for "other" PAM service, a pam configuration file is now required.[[1]](https://bugs.archlinux.org/task/61700)[[2]](https://bbs.archlinux.org/viewtopic.php?pid=1824850)

Create `/etc/pam.d/smtp`.

```
#%PAM-1.0
auth            required        pam_unix.so
account         required        pam_unix.so

```

[Start/enable](/index.php/Start/enable "Start/enable") the `saslauthd.service`.

[Restart](/index.php/Restart "Restart") the `postfix.service`.

Hopefully you should be able to telnet to your Postfix server with:

`telnet localhost 587`

You should then type:

`EHLO example.com`

This is roughly what you should see:

```
Trying 127.0.0.1...

Connected to localhost.localdomain
Escape character is '^]'

220 justin ESMTP Postfix
EHLO example.com
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
  -o smtpd_tls_security_level=encrypt
  -o smtpd_sasl_auth_enable=yes
  -o smtpd_sasl_type=dovecot
  -o smtpd_sasl_path=private/auth
  -o smtpd_sasl_security_options=noanonymous
  -o smtpd_sasl_local_domain=$myhostname
  -o smtpd_client_restrictions=permit_sasl_authenticated,reject
  -o smtpd_recipient_restrictions=reject_non_fqdn_recipient,reject_unknown_recipient_domain,permit_sasl_authenticated,reject

```

Using this configuration implies that only authenticated users can send mails. You can see this from `smtpd_client_restrictions` option.

Now add the following to Dovecot configuration file in `/etc/dovecot/conf.d/10-master.conf`:

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