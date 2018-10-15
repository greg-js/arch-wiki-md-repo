A mail server consists of multiple components. A [mail transfer agent](https://en.wikipedia.org/wiki/Message_transfer_agent "wikipedia:Message transfer agent") (MTA) receives and sends emails via [SMTP](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol "wikipedia:Simple Mail Transfer Protocol"). Received and accepted emails are then passed to a [mail delivery agent](https://en.wikipedia.org/wiki/Mail_delivery_agent "wikipedia:Mail delivery agent") (MDA), which stores the mail in a mailbox (usually in [mbox](https://en.wikipedia.org/wiki/mbox "wikipedia:mbox") or [Maildir](https://en.wikipedia.org/wiki/Maildir "wikipedia:Maildir") format). If you want users to be able to remotely access their mail using [email clients](/index.php/Email_client "Email client") (MUA), you need to run a [POP3](https://en.wikipedia.org/wiki/Post_Office_Protocol "wikipedia:Post Office Protocol") and/or [IMAP](https://en.wikipedia.org/wiki/IMAP "wikipedia:IMAP") server.

```
+---------+  SMTP  +---+   +---+               +----------------+
|Other MTA| <----> |MTA| --|MDA|-> Storage <-- |POP3/IMAP server|
+---------+        +---+   +---+               +----------------+
                     ^                                 ^
                     |     SMTP    +---+               |
                     +-------------|MUA|---------------+
                                   +---+

```

## Contents

*   [1 Software](#Software)
    *   [1.1 POP3/IMAP servers](#POP3.2FIMAP_servers)
    *   [1.2 Standalone MDAs](#Standalone_MDAs)
*   [2 Ports](#Ports)
*   [3 MX record](#MX_record)
*   [4 TLS](#TLS)
*   [5 Authentication](#Authentication)
    *   [5.1 Sender Policy Framework](#Sender_Policy_Framework)
    *   [5.2 Sender Rewriting Scheme](#Sender_Rewriting_Scheme)
    *   [5.3 DKIM](#DKIM)
*   [6 Testing websites](#Testing_websites)
*   [7 Tips and tricks](#Tips_and_tricks)

## Software

All of these software except Sendmail include a mail delivery agent.

*   **[Exim](/index.php/Exim "Exim")** — A highly configurable mail transfer agent.

	[https://exim.org/](https://exim.org/) || [exim](https://www.archlinux.org/packages/?name=exim)

*   **[OpenSMTPD](/index.php/OpenSMTPD "OpenSMTPD")** — A mail transfer agent, part of the OpenBSD project.

	[https://opensmtpd.org/](https://opensmtpd.org/) || [opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd)

*   **[Postfix](/index.php/Postfix "Postfix")** — A mail transfer agent, meant to be fast, easy to administer, and secure.

	[http://www.postfix.org/](http://www.postfix.org/) || [postfix](https://www.archlinux.org/packages/?name=postfix)

*   **[Sendmail](/index.php/Sendmail "Sendmail")** — A well-known mail transfer agent.

	[http://www.sendmail.org/](http://www.sendmail.org/) || [sendmail](https://aur.archlinux.org/packages/sendmail/)

### POP3/IMAP servers

*   **[Courier](/index.php/Courier "Courier")** — A mail transfer agent, providing POP3, IMAP, webmail and mailing list services as individual components.

	[https://www.courier-mta.org/](https://www.courier-mta.org/) || [courier-mta](https://aur.archlinux.org/packages/courier-mta/)

*   **[Cyrus IMAP](https://en.wikipedia.org/wiki/Cyrus_IMAP_server "wikipedia:Cyrus IMAP server")** — A mail transfer agent with a custom mail spool format, provides POP3 and IMAP services.

	[https://www.cyrusimap.org/](https://www.cyrusimap.org/) || [cyrus-imapd](https://aur.archlinux.org/packages/cyrus-imapd/)

*   **[Dovecot](/index.php/Dovecot "Dovecot")** — An IMAP and POP3 server written to be secure, fast and simple to set up.

	[https://dovecot.org/](https://dovecot.org/) || [dovecot](https://www.archlinux.org/packages/?name=dovecot)

*   **[UW IMAP](https://en.wikipedia.org/wiki/UW_IMAP "wikipedia:UW IMAP")** — An IMAP/POP server.

	[https://www.washington.edu/imap/](https://www.washington.edu/imap/) || [imap](https://www.archlinux.org/packages/?name=imap)

### Standalone MDAs

*   **[fdm](/index.php/Fdm "Fdm")** — A simple program for delivering and filtering mail.

	[https://github.com/nicm/fdm](https://github.com/nicm/fdm) || [fdm](https://www.archlinux.org/packages/?name=fdm)

*   **[Procmail](/index.php/Procmail "Procmail")** — A program for filtering, sorting and storing email (unmaintained).

	[http://www.procmail.org/](http://www.procmail.org/) || [procmail](https://www.archlinux.org/packages/?name=procmail)

See also [Wikipedia:Comparison of e-mail servers](https://en.wikipedia.org/wiki/Comparison_of_e-mail_servers "wikipedia:Comparison of e-mail servers").

## Ports

| Purpose | Port | Protocol | Encryption |
| Accept mail from other MTAs. | 25 | SMTP | STARTTLS |
| Accept submissions from MUAs. | 587 | SMTP | STARTTLS |
| 465 | [SMTPS](https://en.wikipedia.org/wiki/SMTPS "wikipedia:SMTPS") | implicit TLS |
| Let MUAs access mail. | 110 | POP3 | STARTTLS |
| 995 | POP3S | implicit TLS |
| 143 | IMAP | STARTTLS |
| 993 | IMAPS | implicit TLS |

Note that implicit TLS is more secure than [STARTTLS](https://en.wikipedia.org/wiki/Opportunistic_TLS "wikipedia:Opportunistic TLS") because the latter is vulnerable to [man-in-the-middle attacks](https://en.wikipedia.org/wiki/Man-in-the-middle_attack "wikipedia:Man-in-the-middle attack"), for more information see [[1]](https://serverfault.com/questions/523804/is-starttls-less-safe-than-tls-ssl) and [RFC:8314](https://tools.ietf.org/html/rfc8314 "rfc:8314").

## MX record

Hosting a mail server requires a [domain name](https://en.wikipedia.org/wiki/Domain_name "wikipedia:Domain name") with an [MX record](https://en.wikipedia.org/wiki/MX_record "wikipedia:MX record") pointing to the domain name of your mail transfer agent. The domain name used as the value of the MX record must map to at least one [address record](https://en.wikipedia.org/wiki/A_record "wikipedia:A record") (A, AAAA) and must not have a [CNAME record](https://en.wikipedia.org/wiki/CNAME_record "wikipedia:CNAME record"), otherwise you are breaking [RFC 2181](https://tools.ietf.org/html/rfc2181#section-10.3 "rfc:2181") and may not get mail from some mail servers. Configuring DNS records is usually done from the configuration interface of your [domain name registrar](https://en.wikipedia.org/wiki/Domain_name_registrar "wikipedia:Domain name registrar").

## TLS

**Warning:** If you deploy [TLS](https://en.wikipedia.org/wiki/TLS "wikipedia:TLS"), be sure to follow [Server-side TLS](/index.php/Server-side_TLS "Server-side TLS") to prevent vulnerabilities.

To obtain a certificate, see [OpenSSL#Certificates](/index.php/OpenSSL#Certificates "OpenSSL").

## Authentication

There are various [email authentication](https://en.wikipedia.org/wiki/Email_authentication "wikipedia:Email authentication") techniques.

### Sender Policy Framework

From [Wikipedia](https://en.wikipedia.org/wiki/Sender_Policy_Framework "wikipedia:Sender Policy Framework"):

	**Sender Policy Framework** (**SPF**) is an email validation protocol designed to detect and block email spoofing by providing a mechanism to allow receiving mail exchangers to verify that incoming mail from a domain comes from an IP Address authorized by that domain's administrators.

To allow other mail exchangers to validate mails apparently sent from your domain, you need to set a DNS TXT record as explained in the [Wikipedia article](https://en.wikipedia.org/wiki/Sender_Policy_Framework "wikipedia:Sender Policy Framework"). To validate incoming mail using SPF you need to configure your mail transfer agent to use a SPF implementation. There are several [SPF implementations](http://www.openspf.org/Implementations) available, [libspf2](https://www.archlinux.org/packages/?name=libspf2), [perl-mail-spf](https://www.archlinux.org/packages/?name=perl-mail-spf) and [perl-mail-spf-query](https://www.archlinux.org/packages/?name=perl-mail-spf-query) can be found in the official repositories.

<caption>SPF validation support</caption>
| [Courier](/index.php/Courier "Courier") | Yes, built-in |
| [Postfix](/index.php/Postfix "Postfix") | [Yes](/index.php/Postfix#Sender_Policy_Framework "Postfix") |
| [Sendmail](/index.php/Sendmail "Sendmail") | through [Milter](https://en.wikipedia.org/wiki/Milter "wikipedia:Milter") and [spfmilter-acme](https://aur.archlinux.org/packages/spfmilter-acme/) |
| [Exim](/index.php/Exim "Exim") | [experimental](https://github.com/Exim/exim/wiki/SPF), requires [libspf2](https://www.archlinux.org/packages/?name=libspf2) |
| [OpenSMTPD](/index.php/OpenSMTPD "OpenSMTPD") | No |
| [Cyrus IMAP](https://en.wikipedia.org/wiki/Cyrus_IMAP_server "wikipedia:Cyrus IMAP server") | ? |

The following websites let you validate your SPF record:

*   [SPF Record Checker](http://www.kitterman.com/spf/validate.html)
*   [SPF Email test](http://www.appmaildev.com/en/spf)

**Tip:** SPF can even be helpful for domains not used to send email. Publishing a policy like `v=spf1 -all` makes any mail server enforcing SPF reject emails from your domain name, thus preventing misuse.

### Sender Rewriting Scheme

The [Sender Rewriting Scheme](https://en.wikipedia.org/wiki/Sender_Rewriting_Scheme "wikipedia:Sender Rewriting Scheme") (SRS) is a secure scheme to allow forwardable bounces for server-side forwarded emails without breaking the [Sender Policy Framework](#Sender_Policy_Framework).

For [Postfix](/index.php/Postfix "Postfix"), see [Postfix#Sender Rewriting Scheme](/index.php/Postfix#Sender_Rewriting_Scheme "Postfix").

### DKIM

[DomainKeys Identified Mail](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail "wikipedia:DomainKeys Identified Mail") (DKIM) is a domain-level email authentication method designed to detect email spoofing.

Available DKIM implementations are [OpenDKIM](/index.php/OpenDKIM "OpenDKIM") and [dkimproxy](https://www.archlinux.org/packages/?name=dkimproxy).

## Testing websites

There are several handy web sites that can help you test DNS records, deliverability, and encryption support.

*   [https://mxtoolbox.com/](https://mxtoolbox.com/)
*   [http://ismyemailworking.com/](http://ismyemailworking.com/)
*   [https://www.mail-tester.com/](https://www.mail-tester.com/)
*   [https://www.checktls.com/](https://www.checktls.com/)
*   [https://pingability.com/zoneinfo.jsp](https://pingability.com/zoneinfo.jsp)

## Tips and tricks

Most mail servers can be configured to strip users' IP addresses and [user agents](https://en.wikipedia.org/wiki/User_agent "wikipedia:User agent") from outgoing mail.

Available extras that can usually be integrated are:

*   [ClamAV](/index.php/ClamAV "ClamAV") for virus checking emails
*   [SpamAssassin](/index.php/SpamAssassin "SpamAssassin") to identify and filter spam
*   [Sieve](https://en.wikipedia.org/wiki/Sieve_(mail_filtering_language) – a mail filtering programming language
*   [webmail](https://en.wikipedia.org/wiki/Webmail "wikipedia:Webmail") like [Roundcube](/index.php/Roundcube "Roundcube") or [Squirrelmail](/index.php/Squirrelmail "Squirrelmail")