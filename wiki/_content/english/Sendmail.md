Sendmail is the classic SMTP server from the unix world. Arch Linux provides the alternative [Postfix](/index.php/Postfix "Postfix") in the [official repositories](/index.php/Official_repositories "Official repositories").

The goal of this article is to setup Sendmail for local users accounts, **without using mysql or other database**, and allowing also the creation of *mail-only accounts*.

This article only explains the required steps configuring Sendmail; after that, you probably want to add IMAP and POP3 access, so you could follow the [Dovecot](/index.php/Dovecot "Dovecot") article.

## Contents

*   [1 Installation](#Installation)
*   [2 DNS Records](#DNS_Records)
*   [3 Adding users](#Adding_users)
*   [4 Configuration](#Configuration)
    *   [4.1 Create SSL certs](#Create_SSL_certs)
    *   [4.2 sendmail.cf](#sendmail.cf)
    *   [4.3 local-host-names](#local-host-names)
    *   [4.4 access.db](#access.db)
    *   [4.5 aliases.db](#aliases.db)
    *   [4.6 virtusertable.db](#virtusertable.db)
    *   [4.7 Start on boot](#Start_on_boot)
    *   [4.8 SASL authentication](#SASL_authentication)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Forward all the mail of one domain to certain user](#Forward_all_the_mail_of_one_domain_to_certain_user)

## Installation

[Install](/index.php/Install "Install") the [sendmail](https://aur.archlinux.org/packages/sendmail/), [procmail](https://www.archlinux.org/packages/?name=procmail) and [m4](https://www.archlinux.org/packages/?name=m4) packages.

## DNS Records

You should have a domain, and edit your MX records to point your server. Remember some servers have problems with MX records pointing to CNAMEs, so your MX should point to an A record instead.

## Adding users

Create a [Linux user](/index.php/Users_and_groups "Users and groups") for each user that wants to receive email at *username@your-domain.com*. To add *mail-only accounts*, that is, users who can get email, but can't have shell access or login on X, you can add them like this:

```
# useradd -m -s /usr/bin/nologin *username*

```

## Configuration

### Create SSL certs

**Warning:** If you plan on implementing SSL/TLS, know that some variations and implementations are [still](https://weakdh.org/#affected) [vulnerable to attack](https://en.wikipedia.org/wiki/Transport_Layer_Security#Attacks_against_TLS.2FSSL "wikipedia:Transport Layer Security"). For details on these current vulnerabilities within SSL/TLS and how to apply appropriate changes to Sendmail, visit [http://disablessl3.com/](http://disablessl3.com/) and [https://weakdh.org/sysadmin.html](https://weakdh.org/sysadmin.html)

Generate a key and obtain a certificate. See [OpenSSL#Self-signed certificate](/index.php/OpenSSL#Self-signed_certificate "OpenSSL") for private use or [Let's Encrypt](/index.php/Let%27s_Encrypt "Let's Encrypt") for a free publicly-trusted certificate.

### sendmail.cf

Create the file `/etc/mail/sendmail.mc`. You can read all the options for configuring sendmail on the file `/usr/share/sendmail-cf/README`.

**Warning:** If you create your own sendmail.mc file, remember that plaintext auth over **non-TLS** is very risky. Using the following example forces TLS and is therefore more safe unless you know what are you doing

Here is an example using auth over [TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security "wikipedia:Transport Layer Security"). The example has comments explaing how it works. The comments start with `dnl` .

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

Then process it with

```
# m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf

```

### local-host-names

Put your domains on the `local-host-names` file:

 `/etc/mail/local-host-names` 
```
localhost
your-domain.com
mail.your-domain.com
localhost.localdomain

```

Make sure the domains are also resolved by your `/etc/hosts` file.

### access.db

Create the file `/etc/mail/access` and put there the base addresses where you want to be able to relay mail. Lets suppose you have a vpn on `10.5.0.0/24`, and you want to relay mails from any ip in that range:

 `/etc/mail/access` 
```
10.5.0 RELAY
127.0.0 RELAY

```

Then process it with

```
# makemap hash /etc/mail/access.db < /etc/mail/access

```

### aliases.db

Edit the file `/etc/mail/aliases` and uncomment the line `#root: human being here` and change it to be like this:

 `root:         your-username` 

You can add aliases for your usernames there, like:

```
coolguy:      your-username
somedude:     your-username
```

Then process it with

```
# newaliases

```

### virtusertable.db

Create your `virtusertable` file and put there aliases that includes domains (useful if your server is hosting several domains)

 `/etc/mail/virtusertable` 
```
your-username@your-domain.com         your-username
joe@my-other.tk                       joenobody

```

Then process it with

```
# makemap hash /etc/mail/virtusertable.db < /etc/mail/virtusertable

```

### Start on boot

Enable and start the following services. Read [Daemons](/index.php/Daemons "Daemons") for more datails.

*   `saslauthd.service`
*   `sendmail.service`
*   `sm-client.service`

### SASL authentication

Add a user to the SASL database for SMTP authentication.

```
# saslpasswd2 -c your-username

```

## Tips and tricks

### Forward all the mail of one domain to certain user

To forward all mail addressed to any user in the **my-other.tk** domain to **your-username@your-domain.com**, add to the `/etc/mail/virtusertable` file:

 `@my-other.tk        your-username@your-domain.com` 

Do not forget to process it again with

```
# makemap hash /etc/mail/virtusertable.db < /etc/mail/virtusertable

```