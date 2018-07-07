A **mail server** or [mail transfer agent](https://en.wikipedia.org/wiki/Message_transfer_agent "wikipedia:Message transfer agent") (MTA) receives and sends emails via [SMTP](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol "wikipedia:Simple Mail Transfer Protocol"). Received and accepted emails are then passed to a [mail delivery agent](https://en.wikipedia.org/wiki/Mail_delivery_agent "wikipedia:Mail delivery agent") (MDA), which stores the mail in a mailbox (usually in [mbox](https://en.wikipedia.org/wiki/mbox "wikipedia:mbox") or [Maildir](https://en.wikipedia.org/wiki/Maildir "wikipedia:Maildir") format). If you want users to be able to remotely access their mail using [email clients](/index.php/Email_client "Email client") or [mail retrieval agents](/index.php/Category:Mail_retrieval_agents "Category:Mail retrieval agents"), you need to run a [POP3](https://en.wikipedia.org/wiki/Post_Office_Protocol "wikipedia:Post Office Protocol") and/or [IMAP](https://en.wikipedia.org/wiki/IMAP "wikipedia:IMAP") server.

| Software | Package | [MTA](https://en.wikipedia.org/wiki/Message_transfer_agent "wikipedia:Message transfer agent") | [MDA](https://en.wikipedia.org/wiki/Mail_delivery_agent "wikipedia:Mail delivery agent") | [POP3](https://en.wikipedia.org/wiki/Post_Office_Protocol "wikipedia:Post Office Protocol") | [IMAP](https://en.wikipedia.org/wiki/IMAP "wikipedia:IMAP") | [SPF](#Sender_Policy_Framework) |
| [Sendmail](/index.php/Sendmail "Sendmail") | [sendmail](https://aur.archlinux.org/packages/sendmail/) | Yes | No | No | No | through [Milter](https://en.wikipedia.org/wiki/Milter "wikipedia:Milter") |
| [Exim](/index.php/Exim "Exim") | [exim](https://www.archlinux.org/packages/?name=exim) | Yes | Yes | No | No | experimental[[1]](https://github.com/Exim/exim/wiki/SPF) |
| [OpenSMTPD](/index.php/OpenSMTPD "OpenSMTPD") | [opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd) | Yes | Yes | No | No | No |
| [Postfix](/index.php/Postfix "Postfix") | [postfix](https://www.archlinux.org/packages/?name=postfix) | Yes | Yes | No | No | Yes |
| [Courier](/index.php/Courier_Mail_Server "Courier Mail Server") | [courier-mta](https://aur.archlinux.org/packages/courier-mta/) | Yes | Yes | Yes | Yes | Yes |
| [Cyrus IMAP](https://en.wikipedia.org/wiki/Cyrus_IMAP_server "wikipedia:Cyrus IMAP server") | [cyrus-imapd](https://aur.archlinux.org/packages/cyrus-imapd/) | Yes | Yes | Yes | Yes |  ? |
| [Dovecot](/index.php/Dovecot "Dovecot") | [dovecot](https://www.archlinux.org/packages/?name=dovecot) | No | Yes | Yes | Yes |
| [UW IMAP](https://en.wikipedia.org/wiki/UW_IMAP "wikipedia:UW IMAP") | [imap](https://www.archlinux.org/packages/?name=imap) | No | Yes | Yes | Yes |
| [fdm](/index.php/Fdm "Fdm") | [fdm](https://www.archlinux.org/packages/?name=fdm) | No | Yes | No | No |
| [Procmail](/index.php/Procmail "Procmail") | [procmail](https://www.archlinux.org/packages/?name=procmail) | No | Yes | No | No |

See also [Wikipedia:Comparison of e-mail servers](https://en.wikipedia.org/wiki/Comparison_of_e-mail_servers "wikipedia:Comparison of e-mail servers").

## Contents

*   [1 MX record](#MX_record)
*   [2 TLS](#TLS)
*   [3 Authentication](#Authentication)
    *   [3.1 Sender Policy Framework](#Sender_Policy_Framework)
    *   [3.2 Sender Rewriting Scheme](#Sender_Rewriting_Scheme)
    *   [3.3 DKIM](#DKIM)
*   [4 Testing websites](#Testing_websites)
*   [5 Tips and tricks](#Tips_and_tricks)

## MX record

If you want to receive mail, you need to set an [MX record](https://en.wikipedia.org/wiki/MX_record "wikipedia:MX record") of your domain name to point to your mail server. Usually this is done from the configuration interface of your domain provider.

A mail exchanger record (MX record) is a type of resource record in the Domain Name System that specifies a mail server responsible for accepting email messages on behalf of a recipient's domain.

When an e-mail message is sent through the Internet, the sending mail transfer agent queries the Domain Name System for MX records of each recipient's domain name. This query returns a list of host names of mail exchange servers accepting incoming mail for that domain and their preferences. The sending agent then attempts to establish an SMTP connection to one of these servers, starting with the one with the smallest preference number, delivering the message to the first server with which a connection can be made.

**Note:** Some mail servers will not deliver mail to you if your MX record points to a CNAME. For best results, always point an MX record to an A record definition. For more information, see e.g. [Wikipedia's List of DNS Record Types](https://en.wikipedia.org/wiki/List_of_DNS_record_types "wikipedia:List of DNS record types").

## TLS

**Warning:** If you deploy [TLS](https://en.wikipedia.org/wiki/TLS "wikipedia:TLS"), be sure to follow [Server-side TLS](/index.php/Server-side_TLS "Server-side TLS") to prevent vulnerabilities.

To obtain a certificate, see [OpenSSL#Certificates](/index.php/OpenSSL#Certificates "OpenSSL").

## Authentication

There are various [email authentication](https://en.wikipedia.org/wiki/Email_authentication "wikipedia:Email authentication") techniques.

### Sender Policy Framework

From [Wikipedia](https://en.wikipedia.org/wiki/Sender_Policy_Framework "wikipedia:Sender Policy Framework"):

	**Sender Policy Framework** (**SPF**) is an email validation protocol designed to detect and block email spoofing by providing a mechanism to allow receiving mail exchangers to verify that incoming mail from a domain comes from an IP Address authorized by that domain's administrators.

To allow other mail exchangers to validate mails apparently sent from your domain, you need to set a DNS TXT record as explained in the [Wikipedia article](https://en.wikipedia.org/wiki/Sender_Policy_Framework "wikipedia:Sender Policy Framework"). To validate incoming mail using SPF you need to configure your mail server to use a SPF implementation. There are several [SPF implementations](http://www.openspf.org/Implementations) available, [perl-mail-spf](https://www.archlinux.org/packages/?name=perl-mail-spf) and [perl-mail-spf-query](https://www.archlinux.org/packages/?name=perl-mail-spf-query) can be found in the official repositories.

*   For [Sendmail](/index.php/Sendmail "Sendmail") [spfmilter-acme](https://aur.archlinux.org/packages/spfmilter-acme/) can be used.
*   For [Postfix](/index.php/Postfix "Postfix"), see [Postfix#Sender Policy Framework](/index.php/Postfix#Sender_Policy_Framework "Postfix").
*   [Courier Mail Server](/index.php/Courier_Mail_Server "Courier Mail Server") natively supports SPF.

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
*   [spamassassin](https://www.archlinux.org/packages/?name=spamassassin) to identify and filter spam
*   [Sieve](https://en.wikipedia.org/wiki/Sieve_(mail_filtering_language) – a mail filtering programming language
*   [webmail](https://en.wikipedia.org/wiki/Webmail "wikipedia:Webmail") like [Roundcube](/index.php/Roundcube "Roundcube") or [Squirrelmail](/index.php/Squirrelmail "Squirrelmail")