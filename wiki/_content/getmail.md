# getmail

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** cron ([cronie](https://www.archlinux.org/packages/?name=cronie)) is not included in [base](https://www.archlinux.org/groups/x86_64/base/) anymore and has to be installed manually, or use [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers") instead (Discuss in [Talk:Getmail#](https://wiki.archlinux.org/index.php/Talk:Getmail))

[getmail](https://en.wikipedia.org/wiki/getmail "wikipedia:getmail") is a mail retriever designed to allow you to get your mail from one or more mail accounts on various mail servers to your local machine for reading with a minimum of fuss. _getmail_ is designed to be secure, flexible, reliable, and easy-to-use. _getmail_ is designed to replace other mail retrievers such as [fetchmail](https://en.wikipedia.org/wiki/Fetchmail "wikipedia:Fetchmail").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Retrieving mail](#Retrieving_mail)
        *   [2.1.1 More than one Email account with getmail](#More_than_one_Email_account_with_getmail)
    *   [2.2 Sorting mail with procmail](#Sorting_mail_with_procmail)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the package [getmail](https://www.archlinux.org/packages/?name=getmail) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

*   Create a configuration directory, and set the right permissions by executing: `$ mkdir -m 0700 ~/.getmail`. The main configuration file often contains sensitive information, namely passwords in plain text.
*   Create a configuration file, the default being: `~/.getmail/getmailrc`. A separate configuration file is needed for each mailserver to pick up mail from. Configuration files other than the default, will have to be explicitly passed as arguments to the getmail command.

### Retrieving mail

Here is an example `getmailrc` used with a gmail account.

```
[retriever]
type = SimplePOP3SSLRetriever
server = pop.gmail.com
username = username@gmail.com
port = 995
password = password

[destination]
type = Maildir
path = ~/mail/
```

You can tweak this to your POP3 service's specification.

Most people will like to add the following section to their `getmailrc` to prevent all the mail on the server being downloaded every time getmail is ran.

```
[options]
read_all = False
```

For this guide we will be storing our mail in the `maildir` format. The two main mailbox formats are `mbox` and `maildir`. The main difference between the two is that `mbox` is one file, with all of your mails and their headers stored in it, whereas a `maildir` is a directory tree. Each mail is its own file, which will often speed things up.

A `maildir` is just a folder with the folders `cur`, `new` and `tmp` in it.

```
$ mkdir -p ~/mail/{cur,new,tmp}

```

Now, run getmail. If it works fine, you can create a cronjob for getmail to run every n hours/minutes. Type `crontab -e` to edit cronjobs, and enter the following:

```
 */10 * * * * /usr/bin/getmail

```

That will run `getmail` every 10 minutes.

Also, to quiet getmail down, we can reduce its verbosity to zero by adding the following to `getmailrc`.

```
[options]
verbose = 0
```

#### More than one Email account with getmail

By default, when you run `getmail` the program searches for the file getmailrc created as seen above. If you have more than one mail account you would like to get mail from, then you can create such a file for each email address, and then tell getmail to run using both of them. Obviously if you have two accounts and two files you cannot have both of them called getmailrc. What you do is give them two different names, using myself as an example: I call one personal, and one university. These two files contain content relevant to my personal mail, and my university work mail respectively. Then to get getmail to work on these two files, instead of searching for getmailrc(default), I use the --rcfile switch like so: `getmail --rcfile university --rcfile personal` This can work with more files if you have more email accounts, just make sure each file is in the .getmail directory and make sure to alter the cronjob to run the command with the --rcfile switches. E.g.

```
 */30 * * * * /usr/bin/getmail --rcfile university --rcfile personal

```

Obviously you can call your files whatever you want, providing you include them in the cronjob or shell command, and they are in the .getmail/ directory, getmail will fetch mail from those two accounts.

### Sorting mail with procmail

Edit your getmailrc to pass retrieved mail to procmail:

```
[destination]
type = MDA_external
path = /usr/bin/procmail
```

Then configure [procmail](/index.php/Procmail "Procmail") to filter your mail.

## See also

*   [getmail documentation](http://pyropus.ca/software/getmail/)
*   [Documentation on Configuring Getmail with rcfiles](http://pyropus.ca/software/getmail/configuration.html#running)
*   How to [Backup Gmail with getmail](/index.php/Backup_Gmail_with_getmail "Backup Gmail with getmail").

Retrieved from "[https://wiki.archlinux.org/index.php?title=Getmail&oldid=412089](https://wiki.archlinux.org/index.php?title=Getmail&oldid=412089)"