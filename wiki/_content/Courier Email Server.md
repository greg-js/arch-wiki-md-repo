# Courier Email Server

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** rc.d references. Needs update to [Systemd](/index.php/Systemd "Systemd"). (Discuss in [Talk:Courier Email Server#](https://wiki.archlinux.org/index.php/Talk:Courier_Email_Server))

This is a small howto on how to install an imap-Server with Courier-Imap, SSL-Encryption and grabbing all the other mail-accounts with fetchmail. Procmail is responsible for delivering the Mails to the different Users.

You can fetch your Mail from this IMAP-Server with every Mail-Client capable of communicating with IMAP.

For testing purposes you should create an own email-account, e.g. www.gmx.de.

For more complex setup see [Creating a Linux Mail Server (Postfix, Procmail, Fetchmail, SpamBayes, Courier-imap, Mutt, SquirrelMail)](http://www.hypexr.org/linux_mail_server.php)

## Contents

*   [1 Installing Packages](#Installing_Packages)
*   [2 Using fetchmail](#Using_fetchmail)
*   [3 Using procmail](#Using_procmail)
*   [4 First Try with procmail and fetchmail working together](#First_Try_with_procmail_and_fetchmail_working_together)
*   [5 Configuring Courier Imap](#Configuring_Courier_Imap)
*   [6 Doing some cron-jobs](#Doing_some_cron-jobs)

#### Installing Packages

[Install](/index.php/Install "Install") [fetchmail](https://www.archlinux.org/packages/?name=fetchmail), [procmail](https://www.archlinux.org/packages/?name=procmail), and [courier-imap](https://aur.archlinux.org/packages/courier-imap/)<sup><small>AUR</small></sup>.

#### Using fetchmail

Just make .fetchmailrc in your home-directory and add the following lines:

```
poll pop.gmx.de with proto POP3
 user "username" there with password "passwd" is "morphus" here
mda "/usr/bin/procmail -d %s"

```

*   username - Your username on the pop3-server
*   passwd - Your password on the pop3-server
*   morphus - Your local account where the mail belongs to

#### Using procmail

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

#### First Try with procmail and fetchmail working together

Send some bulk-mails to your test-account. Then run

```
fetchmail -av

```

Fetchmail echos the communication with the pop-Server and after the run finished you should find some files in your Mail-Folder with the Mails.

#### Configuring Courier Imap

Run the command

```
maildirmake Maildir

```

with each user you want to have an imap-account

And now just start courier imap with

```
/etc/rc.d/courier-imap start

```

You should be able to connect from your console with telnet like this:

```
[morphus@spielemorph ~]$ telnet 192.168.6.1 143
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

#### Doing some cron-jobs

Just add the fetchmail -av command to the [users cron-list](/index.php/Cron "Cron"), e.g. every 10 minutes he should grep the emails

```
'/10 ' ' ' * /usr/bin/fetchmail -av

```

Add /etc/rc.d/courier-imap to your rc.conf in the DAEMONS section.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Courier_Email_Server&oldid=388074](https://wiki.archlinux.org/index.php?title=Courier_Email_Server&oldid=388074)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Mail server](/index.php/Category:Mail_server "Category:Mail server")