DomainKeys Identified Mail is a digital email signing/verification technology, which is already supported by some common mail providers (for example yahoo, google, etc).

## Contents

*   [1 The idea](#The_idea)
*   [2 Installation](#Installation)
*   [3 Basic configuration](#Basic_configuration)
*   [4 Postfix integration](#Postfix_integration)
*   [5 Sendmail integration](#Sendmail_integration)
*   [6 Multiple Domains](#Multiple_Domains)
*   [7 Security](#Security)
*   [8 Notes](#Notes)

## The idea

Basically DKIM means digitally signing all messages on the server to verify the message actually was sent from the domain in question and is not spam or pishing (and has not been modified).

*   The sender's mail server signs outgoing email with the private key.

*   When the message arrives, the receiver (or his server) requests the public key from the domain's DNS and verifies the signature.

This ensures the message was sent from a server who's private key matches the domain's public key.

For more info see [RFC 6376](http://tools.ietf.org/html/rfc6376)

## Installation

[Install](/index.php/Install "Install") the package [opendkim](https://www.archlinux.org/packages/?name=opendkim) from the [Official repositories](/index.php/Official_repositories "Official repositories").

## Basic configuration

Main configuration file is `/etc/opendkim.conf`

*   Copy/move the sample configuration file `/etc/opendkim/opendkim.conf.sample` to `/etc/opendkim/opendkim.conf` and change the following options:

 `/etc/opendkim/opendkim.conf` 
```
Domain                  example.com
KeyFile                 /path/to/keys/server1.private
Selector                myselector
Socket                  inet:8891@localhost
UserID                  opendkim

```

*   To generate a secret signing key, you need to specify the domain used to send mails and a selector which is used to refer to the key. You may choose anything you like, see the RFC for details, but alpha-numeric strings should be OK:

```
opendkim-genkey -r -s myselector -d example.com

```

*   Add a **DNS TXT** record with your selector and public key. The correct record is generated with the private key and can be found in `myselector.txt` in the same location as the private key. Example:

```
myselector._domainkey   IN	 TXT	"v=DKIM1; k=rsa; s=email; p=...................."

```

Check that your DNS record has been correctly updated:

```
host -t TXT myselector._domainkey.example.com

```

You may also check that your DKIM DNS record is properly formated using one of the [DKIM Key checker](http://dkimcore.org/tools/) available on the web.

*   Enable and start the `opendkim.service`. Read [Daemons](/index.php/Daemons "Daemons") for more information.

## Postfix integration

Either add the following lines to `main.cf`:

```
 non_smtpd_milters=inet:127.0.0.1:8891
 smtpd_milters=inet:127.0.0.1:8891

```

Or change smtpd options in `master.cf`:

```
smtp      inet  n       -       n       -       -       smtpd
  -o smtpd_client_connection_count_limit=10
  -o smtpd_milters=inet:127.0.0.1:8891

submission inet n       -       n       -       -       smtpd
  -o smtpd_enforce_tls=no
  -o smtpd_sasl_auth_enable=yes
  -o smtpd_client_restrictions=permit_sasl_authenticated,reject
  -o smtpd_sasl_path=smtpd
  -o cyrus_sasl_config_path=/etc/sasl2
  -o smtpd_milters=inet:127.0.0.1:8891

```

## Sendmail integration

Edit the `sendmail.mc` file and add the following line, **after the last line** starting with `FEATURE`:

 `/etc/mail/sendmail.mc` 
```

INPUT_MAIL_FILTER(`opendkim', `S=inet:8891@localhost')

```

Rebuild the `sendmail.cf` file with:

 `# m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf` 

And then restart the sendmail.service. Read [Daemons](/index.php/Daemons "Daemons") for more details.

## Multiple Domains

If you're providing mail server service to multiple virtual domains on the same server, you'll need to modify the basic configuration as below:

Provide these directives in /etc/opendkim/opendkim.conf

```
KeyTable                refile:/etc/opendkim/KeyTable
SigningTable            refile:/etc/opendkim/SigningTable
ExternalIgnoreList      refile:/etc/opendkim/TrustedHosts
InternalHosts           refile:/etc/opendkim/TrustedHosts

```

Create these 2 files to tell opendkim where to find the correct keys. You can use the same key for all the domains or generate a key for each domain. Make changes to match your settings. Add more lines as needed. /etc/opendkim/KeyTable

```
myselector._domainkey.example1.com example1.com:myselector:/etc/opendkim/myselector.private
myselector._domainkey.example2.com example2.com:myselector:/etc/opendkim/myselector.private
...

```

/etc/opendkim/SigningTable

```
*@example1.com myselector._domainkey.example1.com
*@example2.com myselector._domainkey.example2.com
...

```

Create file /etc/opendkim/TrustedHosts tells opendkim who to let use your keys. This is referenced by the ExternalIgnoreList directive in your conf file. Opendkim will ignore this list of hosts when verifying incoming mail. And, because it’s also referenced by the InternalHosts directive, this same list of hosts will be considered “internal,” and opendkim will sign their outgoing mail.

```
127.0.0.1
::1
hostname.example1.com
example1.com
hostname.example2.com
example2.com
...

```

Change ownership of all files to opendkim:

```
chown -R opendkim:mail /etc/opendkim

```

Add a DNS TXT record with your selector and public key for each of the domains.

You can now restart opendkim.

## Security

The default configuration for the OpenDKIM daemon is less than ideal from a security point of view (all those are minor security issues):

*   The OpenDKIM daemon does not need to run as `root` at all (the configuration suggested earlier will have OpenDKIM drop `root` privileges by himself but `systemd` can do this too and much earlier).
*   If your mail daemon is on the same host as the OpenDKIM daemon, there is no need for localhost tcp sockets and unix sockets may be used instead, allowing classic user/group access controls.
*   OpenDKIM is using the `/tmp` folder by default whereas it could use its own folder with additional access restrictions.

The following configurations files will fix most of those issues (assuming you're using Postfix) and drop some unnecessary options in the systemd service unit:

 `/etc/tmpfiles.d/opendkim.conf` 
```
D /run/opendkim 0750 opendkim postfix

```
 `/etc/opendkim/opendkim.conf` 
```
BaseDirectory           /var/lib/opendkim
Domain                  example.com
KeyFile                 /etc/opendkim/myselector.private
Selector                myselector
Socket                  local:/run/opendkim/opendkim.sock
Syslog                  Yes
TemporaryDirectory      /run/opendkim
UMask                   002

```
 `/etc/systemd/system/opendkim.service` 
```
[Unit]
Description=OpenDKIM daemon
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
User=opendkim
Group=postfix
ExecStart=/usr/bin/opendkim -x /etc/opendkim/opendkim.conf

[Install]
WantedBy=multi-user.target

```

Edit `/etc/postfix/main.cf` accordingly to make Postfix listen to this unix socket:

 `/etc/postfix/main.cf` 
```
smtpd_milters = unix:/run/opendkim/opendkim.sock
non_smtpd_milters = unix:/run/opendkim/opendkim.sock

```

## Notes

While you're about to fight spam and increase people's trust in your server, you might want to take a look at [Sender Policy Framework](https://en.wikipedia.org/wiki/Sender_Policy_Framework "wikipedia:Sender Policy Framework"), which basically means adding a DNS Record stating which servers are authorized to send email for your domain.