This article describes how to set up a mail server suitable for personal or small office use.

[Dovecot](http://www.dovecot.org/) is an open source [IMAP](https://en.wikipedia.org/wiki/IMAP "wikipedia:IMAP") and [POP3](https://en.wikipedia.org/wiki/POP3 "wikipedia:POP3") server for Linux/UNIX-like systems, written primarily with security in mind. Developed by Timo Sirainen, Dovecot was first released in July 2002\. Dovecot primarily aims to be a lightweight, fast and easy to set up open source mailserver. For more detailed information, please see the official [Dovecot Wiki](http://wiki2.dovecot.org/).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Assumptions](#Assumptions)
    *   [2.2 Create the SSL certificate](#Create_the_SSL_certificate)
    *   [2.3 Dovecot configuration](#Dovecot_configuration)
    *   [2.4 PAM Authentication](#PAM_Authentication)
    *   [2.5 PAM Authentication with LDAP](#PAM_Authentication_with_LDAP)
    *   [2.6 Sieve](#Sieve)
*   [3 Starting the server](#Starting_the_server)
*   [4 Tricks](#Tricks)

## Installation

[Install](/index.php/Install "Install") the [dovecot](https://www.archlinux.org/packages/?name=dovecot) package.

## Configuration

### Assumptions

*   Each mail account served by Dovecot, has a local user account defined on the server.
*   The server uses [PAM](/index.php/PAM "PAM") to authenticate the user against the local user database (/etc/passwd).
*   [SSL](https://en.wikipedia.org/wiki/Transport_Layer_Security "wikipedia:Transport Layer Security") is used to encrypt the authentication password.
*   The common [Maildir](https://en.wikipedia.org/wiki/Maildir "wikipedia:Maildir") format is used to store the mail in the user's home directory.
*   A [MDA](https://en.wikipedia.org/wiki/Mail_delivery_agent "wikipedia:Mail delivery agent") has already been set up to deliver mail to the local users.

### Create the SSL certificate

The [dovecot](https://www.archlinux.org/packages/?name=dovecot) package contains a script to generate the server SSL certificate.

*   Copy the configuration file from the sample file: `# cp /etc/ssl/dovecot-openssl.cnf{.sample,}` .
*   Edit `/etc/ssl/dovecot-openssl.cnf` to configure the certificate.

*   Execute `# /usr/lib/dovecot/mkcert.sh` to generate the certificate.

The certificate/key pair is created as `/etc/ssl/certs/dovecot.pem` and `/etc/ssl/private/dovecot.pem`.

Run `cp /etc/ssl/certs/dovecot.pem /etc/ca-certificates/trust-source/anchors/dovecot.crt` and then `# trust extract-compat` whenever you have changed your certificate.

**Warning:** If you plan on implementing SSL/TLS, please respond safely to [POODLE](http://disablessl3.com/) and [FREAK/Logjam](https://weakdh.org/sysadmin.html) by adding the following to your [configuration](#Dovecot_configuration):
```
ssl_protocols = !SSLv2 !SSLv3
ssl_cipher_list = ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA
ssl_prefer_server_ciphers = yes
ssl_dh_parameters_length = 2048
```

### Dovecot configuration

*   Copy the `dovecot.conf` and `conf.d/*` configuration files from `/usr/share/doc/dovecot/example-config` to `/etc/dovecot`:

```
# cp /usr/share/doc/dovecot/example-config/dovecot.conf /etc/dovecot
# cp -r /usr/share/doc/dovecot/example-config/conf.d /etc/dovecot

```

The default configuration is ok for most systems, but make sure to read through the configuration files to see what options are available. See the [quick configuration guide](http://wiki2.dovecot.org/QuickConfiguration) and [dovecot configuration](http://wiki2.dovecot.org/#Dovecot_configuration) for more instructions.

By default dovecot will try to detect what mail storage system is in use on the system. To use the Maildir format edit `/etc/dovecot/conf.d/10-mail.conf` to set `mail_location = maildir:~/Maildir`.

### PAM Authentication

*   To configure PAM for dovecot, create `/etc/pam.d/dovecot` with the following content:

 `/etc/pam.d/dovecot` 
```
auth    required        pam_unix.so nullok
account required        pam_unix.so 

```

### PAM Authentication with LDAP

*   If you are using an [OpenLDAP](/index.php/OpenLDAP "OpenLDAP") server for authentication instead, be sure to be able to login with your LDAP users first, as described in [LDAP authentication](/index.php/LDAP_authentication "LDAP authentication").

You can then write the following in `/etc/pam.d/dovecot` remembering that the entries order is very important:

 `/etc/pam.d/dovecot` 
```
auth    sufficient      pam_ldap.so
auth    required        pam_unix.so     nullok
account sufficient      pam_ldap.so
account required        pam_unix.so
session required        pam_mkhomedir.so skel=/etc/skel umask=0022
session sufficient      pam_ldap.so
```

In this way both LDAP and system users have their mailbox.

*   Change the name of the following file so it can be read by dovecot:

```
# mv /etc/dovecot/conf.d/auth-system.conf{.ext,}

```

*   Edit `/etc/dovecot/conf.d/auth-system.conf` by changing the `passdb` directive, like this:

```
passdb {
  driver = pam
  args = session=yes dovecot
}

```

By using the `pam_mkhomedir.so` module and by adding the `session` part in the `passdb` directive, if an LDAP user logs in for the first time the corresponding home directory will be automatically created.

### Sieve

[Sieve](https://en.wikipedia.org/wiki/Sieve_(mail_filtering_language) is a programming language that can be used to create filters for email on mail server.

*   Install [pigeonhole](https://www.archlinux.org/packages/?name=pigeonhole).
*   Add "sieve" to "protocols" in dovecot.conf (and the lines from the next points)

```
protocols = imap pop3 sieve

```

*   Add minimal 80-sieve.conf in `/etc/dovecot/conf.d/`

```
service managesieve-login {
  inet_listener sieve {
    port = 4190
  }
}

service managesieve {
}

protocol sieve {
}

```

*   Add "sieve" as "mail_plugins" in "protocol lda" section of `/etc/dovecot/conf.d/15-lda.conf`

```
protocol lda {
  mail_plugins = sieve
}

```

*   Specify sieve storage location in "plugin" section of `/etc/dovecot/conf.d/90-plugin.conf`:

```
plugin {
  sieve=/var/mail/%u/dovecot.sieve
  sieve_dir=/var/mail/%u/sieve
}

```

**Note:** Nowadays it is recommended to use LMTP instead of LDA. Nevertheless the Dovecot LDA can still be used for small mailservers. More information can be found in the [Dovecot Wiki](http://wiki2.dovecot.org/LMTP)

*   Ensure that your MTA uses dovecot for delivery. For example: postfix's main.cf and dovecot-lda:

```
 mailbox_command = /usr/lib/dovecot/dovecot-lda -f "$SENDER" -a "$RECIPIENT"

```

## Starting the server

Use the standard [systemd](/index.php/Systemd "Systemd") syntax to control the `dovecot.service` [daemon](/index.php/Daemon "Daemon").

## Tricks

Generate hashes with non-default hash functions.

```
doveadm pw -s SHA512-CRYPT -p "superpassword"

```

Remember to make sure that the column in the database is large enough(you might not get a warning..)

Remember to set the password scheme in your dovecot-sql.conf file

```
default_pass_scheme = SHA512-CRYPT

```