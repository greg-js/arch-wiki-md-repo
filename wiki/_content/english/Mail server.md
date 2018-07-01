A **mail server** or [mail transfer agent](https://en.wikipedia.org/wiki/Message_transfer_agent "wikipedia:Message transfer agent") (MTA) receives and sends emails via [SMTP](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol "wikipedia:Simple Mail Transfer Protocol"). Received and accepted emails are then passed to a [mail delivery agent](https://en.wikipedia.org/wiki/Mail_delivery_agent "wikipedia:Mail delivery agent") (MDA), which stores the mail in a mailbox (usually in [mbox](https://en.wikipedia.org/wiki/mbox "wikipedia:mbox") or [Maildir](https://en.wikipedia.org/wiki/Maildir "wikipedia:Maildir") format). If you want users to be able to remotely access their mail using [email clients](/index.php/Email_client "Email client") or [mail retrieval agents](/index.php/Category:Mail_retrieval_agents "Category:Mail retrieval agents"), you need to run a [POP3](https://en.wikipedia.org/wiki/Post_Office_Protocol "wikipedia:Post Office Protocol") and/or [IMAP](https://en.wikipedia.org/wiki/IMAP "wikipedia:IMAP") server.

| Software | Package | [MTA](https://en.wikipedia.org/wiki/Message_transfer_agent "wikipedia:Message transfer agent") | [MDA](https://en.wikipedia.org/wiki/Mail_delivery_agent "wikipedia:Mail delivery agent") | [POP3](https://en.wikipedia.org/wiki/Post_Office_Protocol "wikipedia:Post Office Protocol") | [IMAP](https://en.wikipedia.org/wiki/IMAP "wikipedia:IMAP") |
| [Sendmail](/index.php/Sendmail "Sendmail") | [sendmail](https://aur.archlinux.org/packages/sendmail/) | Yes | No | No | No |
| [Exim](/index.php/Exim "Exim") | [exim](https://www.archlinux.org/packages/?name=exim) | Yes | Yes | No | No |
| [OpenSMTPD](/index.php/OpenSMTPD "OpenSMTPD") | [opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd) | Yes | Yes | No | No |
| [Postfix](/index.php/Postfix "Postfix") | [postfix](https://www.archlinux.org/packages/?name=postfix) | Yes | Yes | No | No |
| [Courier](/index.php/Courier_Mail_Server "Courier Mail Server") | [courier-mta](https://aur.archlinux.org/packages/courier-mta/) | Yes | Yes | Yes | Yes |
| [Cyrus IMAP](https://en.wikipedia.org/wiki/Cyrus_IMAP_server "wikipedia:Cyrus IMAP server") | [cyrus-imapd](https://aur.archlinux.org/packages/cyrus-imapd/) | Yes | Yes | Yes | Yes |
| [Dovecot](/index.php/Dovecot "Dovecot") | [dovecot](https://www.archlinux.org/packages/?name=dovecot) | No | Yes | Yes | Yes |
| [UW IMAP](https://en.wikipedia.org/wiki/UW_IMAP "wikipedia:UW IMAP") | [imap](https://www.archlinux.org/packages/?name=imap) | No | Yes | Yes | Yes |
| [fdm](/index.php/Fdm "Fdm") | [fdm](https://www.archlinux.org/packages/?name=fdm) | No | Yes | No | No |
| [Procmail](/index.php/Procmail "Procmail") | [procmail](https://www.archlinux.org/packages/?name=procmail) | No | Yes | No | No |

## Contents

*   [1 MX record](#MX_record)
*   [2 DKIM](#DKIM)
*   [3 Testing websites](#Testing_websites)
*   [4 Tips and tricks](#Tips_and_tricks)
*   [5 See also](#See_also)

## MX record

If you want to receive mail, you need to set an [MX record](https://en.wikipedia.org/wiki/MX_record "wikipedia:MX record") of your domain name to point to your mail server. Usually this is done from the configuration interface of your domain provider.

A mail exchanger record (MX record) is a type of resource record in the Domain Name System that specifies a mail server responsible for accepting email messages on behalf of a recipient's domain.

When an e-mail message is sent through the Internet, the sending mail transfer agent queries the Domain Name System for MX records of each recipient's domain name. This query returns a list of host names of mail exchange servers accepting incoming mail for that domain and their preferences. The sending agent then attempts to establish an SMTP connection to one of these servers, starting with the one with the smallest preference number, delivering the message to the first server with which a connection can be made.

**Note:** Some mail servers will not deliver mail to you if your MX record points to a CNAME. For best results, always point an MX record to an A record definition. For more information, see e.g. [Wikipedia's List of DNS Record Types](https://en.wikipedia.org/wiki/List_of_DNS_record_types "wikipedia:List of DNS record types").

## DKIM

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
*   [spamassasin](https://www.archlinux.org/packages/?name=spamassasin) to identify and filter spam
*   [Sieve](https://en.wikipedia.org/wiki/Sieve_(mail_filtering_language) – a mail filtering programming language
*   [webmail](https://en.wikipedia.org/wiki/Webmail "wikipedia:Webmail") like [Roundcube](/index.php/Roundcube "Roundcube") or [Squirrelmail](/index.php/Squirrelmail "Squirrelmail")

## See also

*   [Wikipedia:Comparison of e-mail servers](https://en.wikipedia.org/wiki/Comparison_of_e-mail_servers "wikipedia:Comparison of e-mail servers")