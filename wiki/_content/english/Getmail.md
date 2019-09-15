[getmail](https://en.wikipedia.org/wiki/getmail "wikipedia:getmail") is a mail retriever designed to allow you to get your mail from one or more mail accounts on various mail servers to your local machine for reading with a minimum of fuss. *getmail* is designed to be secure, flexible, reliable, and easy-to-use. *getmail* is designed to replace other mail retrievers such as [fetchmail](https://en.wikipedia.org/wiki/Fetchmail "wikipedia:Fetchmail").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Retrieving mail](#Retrieving_mail)
        *   [2.1.1 Password management](#Password_management)
        *   [2.1.2 Other options](#Other_options)
        *   [2.1.3 More than one Email account with getmail](#More_than_one_Email_account_with_getmail)
    *   [2.2 Sorting mail with procmail](#Sorting_mail_with_procmail)
    *   [2.3 Fetching mail automatically with systemd](#Fetching_mail_automatically_with_systemd)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [getmail](https://www.archlinux.org/packages/?name=getmail) package.

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

#### Password management

It is possible, rather than storing your password in the config, to call an external program to read the password. In which case, you would use the `password_command` parameter:

```
  password_command = ("/path/to/password-retriever", "-p", "myaccount@example.org")

```

Note that the password parameter (in the example config above) overrides this parameter; specify one or the other, not both.

To store the password in a keyring instead of in plain text in the configuration file, setup [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring"), and install the [python2-gnomekeyring](https://aur.archlinux.org/packages/python2-gnomekeyring/) package. Then, delete the `password` entry from `getmailrc`, and run

```
 getmail --store-password-in-gnome-keyring

```

type the password when prompted to have it saved into the keyring.

#### Other options

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

### Fetching mail automatically with systemd

You can run `getmail` every n hours/minutes with [Systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers"). Create a unit file for the timer:

 `~/.config/systemd/user/get_mail.timer` 
```
[Unit]
Description=Run getmail every 15 minutes

[Timer]
OnActiveSec=15min
OnUnitActiveSec=15min

[Install]
WantedBy=timers.target

```

Now create the service file:

 `~/.config/systemd/user/get_mail.service` 
```
[Unit]
Description=Run getmail

[Service]
ExecStart=/usr/bin/getmail --quiet

[Install]
WantedBy=default.target

```

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `get_mail.timer` using the `--user` flag.

## See also

*   [getmail documentation](http://pyropus.ca/software/getmail/)
*   [Documentation on Configuring Getmail with rcfiles](http://pyropus.ca/software/getmail/configuration.html#running)
*   How to [Backup Gmail with getmail](/index.php/Backup_Gmail_with_getmail "Backup Gmail with getmail").