# msmtp

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [mutt](/index.php/Mutt "Mutt")
*   [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP")

[msmtp](http://msmtp.sourceforge.net/) is a very simple and easy to use SMTP client with fairly complete [sendmail](https://en.wikipedia.org/wiki/sendmail "wikipedia:sendmail") compatibility.

## Contents

*   [1 Installing](#Installing)
*   [2 Basic setup](#Basic_setup)
*   [3 Using the mail command](#Using_the_mail_command)
*   [4 Test functionality](#Test_functionality)
*   [5 Cronie default email client](#Cronie_default_email_client)
*   [6 Miscellaneous](#Miscellaneous)
    *   [6.1 Practical password management](#Practical_password_management)
    *   [6.2 Using msmtp offline](#Using_msmtp_offline)
    *   [6.3 Vim syntax highlighting](#Vim_syntax_highlighting)
    *   [6.4 Send mail with PHP using msmtp](#Send_mail_with_PHP_using_msmtp)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Issues with TLS](#Issues_with_TLS)
    *   [7.2 Server sent empty reply](#Server_sent_empty_reply)
    *   [7.3 Issues with GSSAPI](#Issues_with_GSSAPI)

## Installing

msmtp can be [installed](/index.php/Installed "Installed") with the package [msmtp](https://www.archlinux.org/packages/?name=msmtp). Additionally install [msmtp-mta](https://www.archlinux.org/packages/?name=msmtp-mta) that creates a sendmail alias to msmtp.

## Basic setup

The following is an example of a msmtp configuration (the file is based on the packaged, regular-user, example located at `/usr/share/doc/msmtp/msmtprc-user.example`; the system configuration file belongs at `/etc/msmtprc` and it's example is located at `/usr/share/doc/msmtp/msmtprc-system.example`):

 `~/.msmtprc` 

```
# Set default values for all following accounts.
defaults
auth           on
tls            on
tls_trust_file /etc/ssl/certs/ca-certificates.crt
logfile        ~/.msmtp.log

# Gmail
account        gmail
host           smtp.gmail.com
port           587
from           _username_@gmail.com
user           _username_
password       _plain-text-password_

# A freemail service
account        freemail
host           smtp.freemail.example
from           joe_smith@freemail.example
...

# Set a default account
account default : gmail

```

**Note:** If you are using SSL/TLS and receive a "Server sent empty reply" error message, see [#Server sent empty reply](#Server_sent_empty_reply).

The _user_ configuration file must be explicitly readable/writeable to only it's owner or msmtp will fail:

```
$ chmod 600 ~/.msmtprc

```

To avoid saving the password in plain text in the configuration file, use _passwordeval_ to launch an external program. This example using Gnu PG is commonly used to perform decryption of a password:

```
 echo -e "password\n" | gpg --encrypt -o .msmtp-gmail.gpg # enter id (email...)

```

**Warning:** Most shells save command history(e.g. .bash_history .zhistory). To avoid this use gpg with shell stdin: `gpg --encrypt -o .msmtp-gmail.gpg -r <email> -`. The ending dash is not a typo, rather it causes gpg to use stdin. After running that snippet of code, type in your password, press enter, and press Control-d so gpg can encrypt your password.

 `~/.msmtprc` 

```
passwordeval    "gpg --quiet --for-your-eyes-only --no-tty --decrypt ~/.msmtp-gmail.gpg"

```

## Using the mail command

To send mails using the `mail` command you must install the package [s-nail](https://www.archlinux.org/packages/?name=s-nail). Either install [msmtp-mta](https://www.archlinux.org/packages/?name=msmtp-mta) or edit `/etc/mail.rc` to set sendmail client:

 `/etc/mail.rc`  `set sendmail=/usr/bin/msmtp` 

A `.msmtprc` file will need to be in the home of every user who want to send mail or alternatively the system wide `/etc/msmtprc` can be used.

msmtp also understands aliases. Add the following line to the defaults section of msmtprc or your local configuration file:

 `/etc/msmtprc`  `aliases               /etc/aliases` 

and create an aliases file in `/etc`

 `/etc/aliases` 

```
# Example aliases file

# Send root to Joe and Jane
root: joe_smith@example.com, jane_chang@example.com

# Send everything else to admin
default: admin@domain.example
```

## Test functionality

The account option (`--account=,-a` tells which account to use as sender:

```
$ echo "hello there username." | msmtp -a default _username_@domain.com

```

Or, with the addresses in a file:

```
To: _username_@domain.com
From: _username_@gmail.com
Subject: A test

Hello there.

```

```
$ cat test.mail | msmtp -a default <username>@domain.com

```

**Tip:** If using Gmail you'll need to allow "Less Secure Apps" in _Settings_ > _Security_. Make sure to sign out of your other Gmail accounts first because the security settings part of Google Accounts can not manage concurrent sessions of more than one account.

## Cronie default email client

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Arch uses [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers") instead of cronie (Discuss in [Talk:Msmtp#](https://wiki.archlinux.org/index.php/Talk:Msmtp))

To make [cronie](https://www.archlinux.org/packages/?name=cronie) use msmtp rather than sendmail, make sure [msmtp-mta](https://www.archlinux.org/packages/?name=msmtp-mta) is installed, or edit the `cronie.service` systemd unit:

 `/etc/systemd/system/cronie.service.d/msmtp.conf` 

```
[Service]
ExecStart=
ExecStart=/usr/bin/crond -n -m '/usr/bin/msmtp -t'
```

Then you must tell cronie or msmtp what your email address is, either by:

1.  Add to `/etc/msmtprc`: `aliases /etc/aliases` and create `/etc/aliases`: `your_username: email@address.com` — OR —.

*   Add a `MAILTO` line to the crontab: `MAILTO=email@address.com` 

## Miscellaneous

Other details.

### Practical password management

The `password` directive may be omitted. In that case, if the account in question has `auth` set to a legitimate value other than `off`, invoking msmtp from an interactive shell will ask for the password before sending mail. msmtp will not prompt if it has been called by another type of application, such as [Mutt](/index.php/Mutt "Mutt"). There is a solution for such cases: the `--passwordeval` parameter. You can call msmtp to use an external keyring tool like gpg:

 `msmtp --passwordeval 'gpg -d mypwfile.gpg'` 

If gpg prompt for the passphrase cannot be issued (e.g. when called from Mutt) then start the [gpg-agent](/index.php/GPG#gpg-agent "GPG") before.

A simple hack to start the agent is to execute a external command in your muttrc.

**Note:** Mutt uses the backtick `` command `` syntax to execute external commands

For example, you can put something like the following in your muttrc

 `muttrc`  `set my_msmtp_pass=`gpg -d mypwfile.gpg`` 

Mutt will execute this when it starts, gpg-agent will cache your password, msmtp will be happy and you can send mail.

**Note:** If you do this, you will have to restart mutt after gpg-agent clears the password to start sending emails again

If you cannot use a keyring tool for any reason, you may want to use the password directly. There is a patched version [msmtp-pwpatched](https://aur.archlinux.org/packages/msmtp-pwpatched/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/msmtp-pwpatched)]</sup> in the AUR that provides the `--password` parameter. Note that it is a **huge security flaw**, since any user connected to you machine can see the parameter of any command (in the /proc filesystem for example).

If this is not desired, an alternative is to place passwords in `~/.netrc`, a file that can act as a common pool for msmtp, [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP"), and associated tools.

### Using msmtp offline

Although msmtp is great, it requires that you be online to use it. This isn't ideal for people on laptops with intermittent connections to the Internet or dialup users. Several scripts have been written to remedy this fact, collectively called msmtpqueue.

The scripts are installed under `/usr/share/doc/msmtp/msmtpqueue`. You might want to copy the scripts to a convenient location on your computer, (`/usr/local/bin` is a good choice).

Finally, change your MUA to use msmtp-enqueue.sh instead of msmtp when sending e-mail. By default, queued messages will be stored in `~/.msmtpqueue`. To change this location, change the `QUEUEDIR=$HOME/.msmtpqueue` line in the scripts (or delete the line, and export the QUEUEDIR variable in `.bash_profile` like so: `export QUEUEDIR="$XDG_DATA_HOME/msmtpqueue"`).

When you want to send any mail that you've created and queued up run:

```
$ /usr/local/bin/msmtp-runqueue.sh

```

Adding `/usr/local/bin` to your PATH can save you some keystrokes if you're doing it manually. The README file that comes with the scripts has some handy information, reading it is recommended.

### Vim syntax highlighting

The msmtp source distribution includes a `msmtprc` highlighting script for [Vim](/index.php/Vim "Vim"). Install it from `./scripts/vim/msmtp.vim`.

### Send mail with PHP using msmtp

Look for _sendmail_path_ option in your `php.ini` and edit like this:

 `sendmail_path = "/usr/bin/msmtp -C /path/to/your/config -t"` 

Note that you **can not** use a user configuration file (ie: one under ~/) if you plan on using msmtp as a sendmail replacement with php or something similar. In that case just create /etc/msmtprc, and remove your user configuration (or not if you plan on using it for something else). Also make sure it's readable by whatever you're using it with (php, django, etc...)

From the msmtp manual: _Accounts defined in the user configuration file override accounts from the system configuration file. The user configuration file must have no more permissions than user read/write_

So it's impossible to have a conf file under ~/ and have it still be readable by the php user.

To test it place this file in your php enabled server or using php-cli.

```
<?php
mail("your@email.com", "Test email from PHP", "msmtp as sendmail for PHP");
?>

```

## Troubleshooting

### Issues with TLS

If you see the following message:

```
 msmtp: TLS certificate verification failed: the certificate hasn't got a known issuer

```

it probably means your tls_trust_file is not right.

Just follow the [fine manual](http://msmtp.sourceforge.net/doc/msmtp.html#Transport-Layer-Security). It explains you how to find out the server certificate issuer of a given smtp server. Then you can explore the `/usr/share/ca-certificates/` directory to find out if by any chance, the certificate you need is there. If not, you will have to get the certificate on your own. If you are using your own certificate, you can make msmtp trust it by adding the following to your **~/.msmtprc**:

```
 tls_fingerprint <SHA1 (recommended) or MD5 fingerprint of the certificate>

```

If you are trying to send mail through GMail and are receiving this error, have a look at [this](http://www.mail-archive.com/msmtp-users@lists.sourceforge.net/msg00141.html) thread or just use the second GMail example above.

If you are completely desperate, but are 100% sure you are communicating with the right server, you can always temporarily disable the cert check:

```
$ msmtp --tls-certcheck off

```

If you see the following message:

```
 msmtp: TLS handshake failed: the operation timed out

```

You may be affected by this [bug](https://bugs.archlinux.org/task/44994). Recompile with "--with-ssl=openssl" (msmtp is compiled with GnuTLS by default).

### Server sent empty reply

If you get a "server sent empty reply" error, add the following line to **~/.msmtprc**:

```
tls_starttls off

```

This allows msmtp to use SSL/TLS (port 465) in place of STARTTLS (port 587) [[1]](https://www.fastmail.com/help/technical/ssltlsstarttls.html).

### Issues with GSSAPI

If you get the following error

```
GNU SASL: GSSAPI error in client while negotiating security context in gss_init_sec_context() in SASL library.  This is most likely due insufficient credentials or malicious interactions.

```

Try changing your auth setting to plain, instead of gssapi in your .msmtprc file [[2]](https://bbs.archlinux.org/viewtopic.php?id=138727):

```
auth plain

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Msmtp&oldid=412701](https://wiki.archlinux.org/index.php?title=Msmtp&oldid=412701)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Email clients](/index.php/Category:Email_clients "Category:Email clients")
*   [Mail server](/index.php/Category:Mail_server "Category:Mail server")