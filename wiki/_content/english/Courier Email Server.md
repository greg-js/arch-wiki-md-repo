This is a small howto on how to install an imap-Server with Courier-Imap, SSL-Encryption and grabbing all the other mail-accounts with fetchmail. Procmail is responsible for delivering the Mails to the different Users.

You can fetch your Mail from this IMAP-Server with every Mail-Client capable of communicating with IMAP.

For testing purposes you should create an own email-account, e.g. www.gmx.de.

For more complex setup see [Creating a Linux Mail Server (Postfix, Procmail, Fetchmail, SpamBayes, Courier-imap, Mutt, SquirrelMail)](http://www.hypexr.org/linux_mail_server.php)

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Using fetchmail](#Using_fetchmail)
    *   [1.2 Using procmail](#Using_procmail)
    *   [1.3 First Try with procmail and fetchmail working together](#First_Try_with_procmail_and_fetchmail_working_together)
    *   [1.4 Configuring Courier Imap](#Configuring_Courier_Imap)
    *   [1.5 Doing some cron-jobs](#Doing_some_cron-jobs)

## Installation

[Install](/index.php/Install "Install") [fetchmail](https://www.archlinux.org/packages/?name=fetchmail), [procmail](https://www.archlinux.org/packages/?name=procmail), and [courier-imap](https://aur.archlinux.org/packages/courier-imap/).

### Using fetchmail

Just make .fetchmailrc in your home-directory and add the following lines:

```
poll pop.gmx.de with proto POP3
 user "username" there with password "passwd" is "morphus" here
mda "/usr/bin/procmail -d %s"

```

*   username - Your username on the pop3-server
*   passwd - Your password on the pop3-server
*   morphus - Your local account where the mail belongs to

### Using procmail

Create and edit .procmailrc in your home-directory

```
PATH=$HOME/bin:/usr/bin:/bin:/usr/local/bin:.
MAILDIR=$HOME/Maildir/
DEFAULT=$HOME/Maildir/
LOGFILE=$MAILDIR/procmail.log

```

Now secure your .fetchmailrc since they contain passwords

```
chmod 600 .fetchmailrc

```

### First Try with procmail and fetchmail working together

Send some bulk-mails to your test-account. Then run

```
fetchmail -av

```

Fetchmail echos the communication with the pop-Server and after the run finished you should find some files in your Mail-Folder with the Mails.

### Configuring Courier Imap

Run the command

```
maildirmake Maildir

```

with each user you want to have an imap-account

[Start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `courier-imapd.service`.

You should be able to connect from your console with telnet like this:

 `[morphus@spielemorph ~]$ telnet 192.168.6.1 143` 
```
Trying 192.168.6.1...
Connected to 192.168.6.1.
Escape character is '^]'.
* OK [CAPABILITY IMAP4rev1 UIDPLUS CHILDREN NAMESPACE THREAD=ORDEREDSUBJECT
 THREAD<code>REFERENCES SORT QUOTA IDLE ACL ACL2</code>UNION STARTTLS] Courier-IMAP ready.
Copyright 1998-2004 Double Precision, Inc.  See COPYING for distribution information.
1 login morphus passwd
1 OK LOGIN Ok.

```

This means everything is okay and you can connect. Your mail should be delivered to this Maildirectory and you should be able to connect with any imap-capable program.

### Doing some cron-jobs

Just add the fetchmail -av command to the [users cron-list](/index.php/Cron "Cron"), e.g. every 10 minutes he should grep the emails

```
'/10 ' ' ' * /usr/bin/fetchmail -av

```