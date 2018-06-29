A mail server consists generally of:

*   a [mail transfer agent](https://en.wikipedia.org/wiki/Message_transfer_agent "wikipedia:Message transfer agent") (MTA) that receives and sends emails via [SMTP](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol "wikipedia:Simple Mail Transfer Protocol")
*   a [mail delivery agent](https://en.wikipedia.org/wiki/Mail_delivery_agent "wikipedia:Mail delivery agent") (MDA) that stores mail it receives from the MTA in a mailbox ([mbox](https://en.wikipedia.org/wiki/mbox "wikipedia:mbox") / [Maildir](https://en.wikipedia.org/wiki/Maildir "wikipedia:Maildir")).
*   a [POP3](https://en.wikipedia.org/wiki/Post_Office_Protocol "wikipedia:Post Office Protocol") and/or [IMAP](https://en.wikipedia.org/wiki/IMAP "wikipedia:IMAP") server to access the mail

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

Available extras that can usually be integrated are:

*   [ClamAV](/index.php/ClamAV "ClamAV") for virus checking emails
*   [spamassasin](https://www.archlinux.org/packages/?name=spamassasin) to identify and filter spam
*   [Sieve](https://en.wikipedia.org/wiki/Sieve_(mail_filtering_language) – a mail filtering programming language

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

## See also

*   [Wikipedia:Comparison of e-mail servers](https://en.wikipedia.org/wiki/Comparison_of_e-mail_servers "wikipedia:Comparison of e-mail servers")