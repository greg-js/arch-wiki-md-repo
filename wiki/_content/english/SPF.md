Sender Policy Framework (SPF) is a protocol to indentify qualified servers, which are allowed to send emails on behalf of a domain. It consists of two parts, a DNS TXT record explained in [record](#Record) and a validating mail filter explained in [validator](#Validator). SPF can lead to problems when forwarding mail. For a solution for this see the Sender Rewrite Scheme (SRS) section below.

## Contents

*   [1 Record](#Record)
*   [2 Validator](#Validator)
    *   [2.1 Installation](#Installation)
    *   [2.2 Configuration](#Configuration)
    *   [2.3 Postfix integration](#Postfix_integration)
    *   [2.4 Testing](#Testing)
*   [3 Sender Rewrite Scheme (SRS)](#Sender_Rewrite_Scheme_.28SRS.29)
*   [4 Remarks](#Remarks)
*   [5 Known problems](#Known_problems)
*   [6 See also](#See_also)

## Record

An example record could look like this `v=spf1 ip4:192.0.2.0/24 ip4:198.51.100.123 a -all` and is entered as TXT record of the email sending domain.

The following mechanisms are supported:

| Tag Name | Explanation |
| ALL | Matches always; used for a default result like -all for all IPs not matched by prior mechanisms. |
| A | Matches domains A and AAAA record |
| IP4 | Matches given IPv4 address or address range |
| IP6 | Matches given IPv6 address or address range |
| MX | Matches domains mx record |
| PTR | Matches PTR record. This mechanism is deprecated and should no longer be used. |
| EXISTS | Matches if domain exists, regardless of the address. This is rarely used. Along with the SPF macro language it offers more complex matches like DNSBL-queries. |
| INCLUDE | Includes the SPF record of a given domain |

where you can use the following quantifiers:

| Qantifier | Explanation |
| + | PASS result. This can be omitted; e.g., +mx is the same as mx. |
| ? | NEUTRAL result interpreted like NONE (no policy). |
| ~ | SOFTFAIL, a debugging aid between NEUTRAL and FAIL. Typically, messages that return a SOFTFAIL are accepted but tagged. |
| - | FAIL, the mail should be rejected (see below). |

## Validator

This is shown for [Postfix](/index.php/Postfix "Postfix") only.

### Installation

There are several SPF validators available [[1]](http://www.openspf.org/Implementations), [perl-mail-spf](https://www.archlinux.org/packages/?name=perl-mail-spf) and [perl-mail-spf-query](https://www.archlinux.org/packages/?name=perl-mail-spf-query) can be found in the official Repositories. Below [python-postfix-policyd-spf](https://aur.archlinux.org/packages/python-postfix-policyd-spf/) is combined with the [postfix](https://www.archlinux.org/packages/?name=postfix) mailserver.

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

## Sender Rewrite Scheme (SRS)

To prevent future SPF checks from failing when forwarding mails, SRS provides a scheme to rewrite the ENVELOPE-FROM field to your own domain, thus passing the SPF test at the recipient server. To prevent creating open relays and still catch and backwrite bounces, this often contains a hash of the original adress combined with a secret only known to the server, providing validability of bounce email. For [postfix](https://www.archlinux.org/packages/?name=postfix) install [postsrsd](https://aur.archlinux.org/packages/postsrsd/) and adjust the settings:

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

Some contact form providers send mails impersonating the sender using its email address in FROM-field. This is bad practice but still used, and leads to rejected emails with strict SPF policies (such als `v=spf1 a -all`).

## See also

*   [SPF Record Checker](http://www.kitterman.com/spf/validate.html)