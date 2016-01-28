# Backup Gmail with getmail

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [getmail](/index.php/Getmail "Getmail").**

**Notes:** Only [#Troubleshooting](#Troubleshooting) is specific to Gmail. (Discuss in [Talk:Backup Gmail with getmail#](https://wiki.archlinux.org/index.php/Talk:Backup_Gmail_with_getmail))

We can use getmail to fully backup email messages from a Gmail account.

Emails will be backed-up in Maildir format, meaning that each email will be a separate text file, readable with any email client, or even with a text editor.

## Contents

*   [1 Installing getmail](#Installing_getmail)
*   [2 Creating required files and folders](#Creating_required_files_and_folders)
*   [3 Configuring getmail](#Configuring_getmail)
*   [4 Running getmail and adding a cron job](#Running_getmail_and_adding_a_cron_job)
*   [5 Migrating emails, importing old emails](#Migrating_emails.2C_importing_old_emails)
*   [6 Troubleshooting](#Troubleshooting)

## Installing getmail

```
# pacman -S getmail

```

## Creating required files and folders

Getmail reads its configuration from ~/.getmail/getmailrc by default. Unfortunately this directory and file do not exist by default, so we need to create them.

```
$ mkdir ~/.getmail
$ touch ~/.getmail/getmailrc
$ chmod 700 ~/.getmail

```

We also need to create the folder where the emails will be backed-up:

```
$ mkdir -p ~/bak/mail
$ cd ~/bak/mail
$ mkdir cur new tmp

```

For this example ~/bak/mail was chosen , but it could just as well be ~/mail. The cur, new and tmp folders are required by the Maildir format and by getmail.

## Configuring getmail

Open the ~/.getmail/getmailrc file and add the entries below. The complete file can also be found here [http://archlinux.pastebin.com/0GH5vtSn](http://archlinux.pastebin.com/0GH5vtSn)

```
# More configuration options here:
# [http://pyropus.ca/software/getmail/configuration.html](http://pyropus.ca/software/getmail/configuration.html)
[retriever]
type = SimpleIMAPSSLRetriever
server = imap.gmail.com
mailboxes = ("Inbox", "[Gmail]/Sent Mail") # optional - leave this line out to just grab inbox
username = USER
password = PASS

```

The retriever section tells getmail where to connect. It uses IMAP to connect to the server. For POP3 we can use the type SimplePOP3SSLRetriever, but we'll also have to modify the server field. The mailbox which we backup will be All Mail.

Note that Gmail was called Google Mail in some countries like Germany. Even if all GMail accounts are migrated to the new name, the IMAP-Server still assumes Google Mail as the mail box directory. The mailboxes variable must be set to [Google Mail] in those cases. Also, you might need to replace box labels by whatever GMail calls that directory in the language of your Google account.

The username and password fields need to be changed to your own.

```
[destination]
type = Maildir
path = ~/bak/mail/

```

The path field is the destination folder (which we created earlier) where the emails will be backed-up. All emails will be placed in 'new', and the cur and tmp folders will be left empty. This is normal, do not delete cur and tmp.

The options section is a bit longer:

```
[options]
verbose = 2
message_log = ~/.getmail/log

```

This tells getmail to be very verbose and tell us the status of each message (whether it was backed-up successfully, total number of messages, etc). Also, everything will be logged to ~/.getmail/log.

```
# retrieve only new messages
# if set to true it will re-download ALL messages every time!
read_all = false

```

```
# do not alter messages
delivered_to = false
received = false

```

Setting delivered_to and received fields to false will prevent emails from being altered by getmail.

## Running getmail and adding a cron job

Now if we run getmail it will backup all Gmail emails to ~/bak/mail, outputting its status along the way.

We want to periodically run getmail to backup our Gmail account, so we'll add a cron job:

```
* * * * *   ID=getmail FREQ=1d getmail -q

```

The -q parameter will run getmail in quiet mode and only report errors.

## Migrating emails, importing old emails

Backing-up emails will suffice for most people, but if we want to migrate our emails to another account it gets a bit tricky. The appendmail script from [http://bitbucket.org/wooptoo/appendmail](http://bitbucket.org/wooptoo/appendmail) can help us import emails to another account, be it Gmail or not. It can also be used to import old emails in our existing Gmail account.

Basically it reads every email file from its 'import' folder and puts it on Gmail or another account.

A direct link to download is [http://bitbucket.org/wooptoo/appendmail/get/tip.zip](http://bitbucket.org/wooptoo/appendmail/get/tip.zip) It needs PHP to run, and you need to modify the username and password to yours.

## Troubleshooting

Depending on your Gmail security, you may be left with this error when running getmail:

```
getmailrc: credential/login error ([ALERT] Please log in via your web browser: [http://support.google.com/mail/accounts/bin/answer.py?answer=78754](http://support.google.com/mail/accounts/bin/answer.py?answer=78754) (Failure))
  0 messages (0 bytes) retrieved, 0 skipped
```

To bypass this Gmail security feature, one must [enable access for less secure apps](https://www.google.com/settings/security/lesssecureapps)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Backup_Gmail_with_getmail&oldid=377542](https://wiki.archlinux.org/index.php?title=Backup_Gmail_with_getmail&oldid=377542)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Email clients](/index.php/Category:Email_clients "Category:Email clients")

Hidden category:

*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")