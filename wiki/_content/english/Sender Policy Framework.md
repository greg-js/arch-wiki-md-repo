From [Wikipedia](https://en.wikipedia.org/wiki/Sender_Policy_Framework "wikipedia:Sender Policy Framework"):

	**Sender Policy Framework** (**SPF**) is an email validation protocol designed to detect and block email spoofing by providing a mechanism to allow receiving mail exchangers to verify that incoming mail from a domain comes from an IP Address authorized by that domain's administrators.

To allow other mail exchangers to validate mails apparently sent from your domain, you need to set a DNS TXT record as explained in the [Wikipedia article](https://en.wikipedia.org/wiki/Sender_Policy_Framework "wikipedia:Sender Policy Framework"). To validate incoming mail using SPF you need to configure your mail server to use a [SPF implementation](#Validator).

## Contents

*   [1 Validator](#Validator)
    *   [1.1 Installation](#Installation)
    *   [1.2 Configuration](#Configuration)
    *   [1.3 Postfix integration](#Postfix_integration)
    *   [1.4 Testing](#Testing)
*   [2 Sender Rewriting Scheme](#Sender_Rewriting_Scheme)
*   [3 Remarks](#Remarks)
*   [4 Known problems](#Known_problems)
*   [5 See also](#See_also)

## Validator

This is shown for [Postfix](/index.php/Postfix "Postfix") only.

### Installation

There are several SPF validators available [[1]](http://www.openspf.org/Implementations), [perl-mail-spf](https://www.archlinux.org/packages/?name=perl-mail-spf) and [perl-mail-spf-query](https://www.archlinux.org/packages/?name=perl-mail-spf-query) can be found in the official Repositories. Below [python-postfix-policyd-spf](https://aur.archlinux.org/packages/python-postfix-policyd-spf/) is combined with the [postfix](https://www.archlinux.org/packages/?name=postfix) mail server.

### Configuration

Edit `/etc/python-policyd-spf/policyd-spf.conf` to your needs. An extensively commented version can be found at `/etc/python-policyd-spf/policyd-spf.conf.commented`. Pay some extra attention to the HELO check policy, as standard settings strictly reject HELO failures.

### Postfix integration

In the main.cf add a timeout for the policyd:

 `/etc/postfix/main.cf`  `policy-spf_time_limit = 3600s` 

Then add a transport

 `/etc/postfix/master.cf` 
```
policy-spf  unix  -       n       n       -       0       spawn
     user=nobody argv=/usr/bin/policyd-spf
```

Lastly you need to add the policyd to the `smtpd_recipient_restrictions`. To minimize load put it to the end of the restrictions:

 `/etc/postfix/main.cf` 
```
smtpd_recipient_restrictions=
     ...
     permit_sasl_authenticated
     permit_mynetworks
     reject_unauth_destination
     check_policy_service unix:private/policy-spf

```

### Testing

You can test your Setup with the following:

 `/etc/python-policyd-spf/policyd-spf.conf`  `defaultSeedOnly = 0` 

## Sender Rewriting Scheme

The [Sender Rewriting Scheme](https://en.wikipedia.org/wiki/Sender_Rewriting_Scheme "wikipedia:Sender Rewriting Scheme") (SRS) is a solution to allow email forwarding by the server (like mailing lists need) without breaking the SPF.

SRS rewrites the ENVELOPE-FROM field to your own domain, thus passing the SPF test at the recipient server. To prevent creating open relays and still catch and backwrite bounces, this often contains a hash of the original address combined with a secret only known to the server, providing authenticity of bounce email.

For [postfix](https://www.archlinux.org/packages/?name=postfix) install [postsrsd](https://aur.archlinux.org/packages/postsrsd/) and adjust the settings:

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

## Remarks

SPF can even be helpful for domains not supposed to send email. Publishing a policy like `v=spfv -all` prevents anyone from sending in this domains name thus preventing misuse.

## Known problems

Some contact form providers send mails impersonating the sender using its email address in FROM-field. This is bad practice but still used, and leads to rejected emails with strict SPF policies (such as `v=spf1 a -all`).

## See also

*   [SPF Record Checker](http://www.kitterman.com/spf/validate.html)
*   [SPF Email test](http://www.appmaildev.com/en/spf)