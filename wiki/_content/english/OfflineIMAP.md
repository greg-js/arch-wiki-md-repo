Related articles

*   [isync](/index.php/Isync "Isync")
*   [notmuch](/index.php/Notmuch "Notmuch")
*   [msmtp](/index.php/Msmtp "Msmtp")

[OfflineIMAP](http://offlineimap.org/) is a Python utility to sync mail from IMAP servers. It does not work with the POP3 protocol or mbox, and is usually paired with a MUA such as [Mutt](/index.php/Mutt "Mutt").

**Note:** [imapfw](http://www.offlineimap.org/development/2015/10/08/imapfw-is-made-public.html) is intened to replace offlineimap in the future.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Minimal](#Minimal)
    *   [2.2 Selective folder synchronization](#Selective_folder_synchronization)
*   [3 Usage](#Usage)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Running offlineimap in the background](#Running_offlineimap_in_the_background)
        *   [4.1.1 systemd service](#systemd_service)
    *   [4.2 Automatic mailbox generation for mutt](#Automatic_mailbox_generation_for_mutt)
    *   [4.3 Gmail configuration](#Gmail_configuration)
    *   [4.4 Password management](#Password_management)
        *   [4.4.1 .netrc](#.netrc)
        *   [4.4.2 Using GPG](#Using_GPG)
        *   [4.4.3 Using pass](#Using_pass)
        *   [4.4.4 Gnome keyring](#Gnome_keyring)
            *   [4.4.4.1 Option 1: using gnomekeyring Python module](#Option_1:_using_gnomekeyring_Python_module)
            *   [4.4.4.2 Option 2: using gnome-keyring-query tool](#Option_2:_using_gnome-keyring-queryAUR_tool)
        *   [4.4.5 python2-keyring](#python2-keyring)
        *   [4.4.6 Emacs EasyPG](#Emacs_EasyPG)
        *   [4.4.7 KeePass / KeePassX](#KeePass_.2F_KeePassX)
            *   [4.4.7.1 Old kdb format](#Old_kdb_format)
    *   [4.5 Kerberos authentication](#Kerberos_authentication)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Overriding UI and autorefresh settings](#Overriding_UI_and_autorefresh_settings)
    *   [5.2 Folder could not be created](#Folder_could_not_be_created)
    *   [5.3 SSL fingerprint does not match](#SSL_fingerprint_does_not_match)
    *   [5.4 Copying message, connection closed](#Copying_message.2C_connection_closed)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [offlineimap](https://www.archlinux.org/packages/?name=offlineimap) package or [offlineimap-git](https://aur.archlinux.org/packages/offlineimap-git/) for the development version.

## Configuration

Offlineimap is distributed with two default configuration files, which are both located in `/usr/share/offlineimap/`. `offlineimap.conf` contains every setting and is thorougly documented. Alternatively, `offlineimap.conf.minimal` is not commented and only contains a small number of settings (see: [Minimal](#Minimal)).

Copy one of the default configuration files to `~/.offlineimaprc`.

**Note:** Writing a comment after an option/value on the same line is invalid syntax, hence take care that comments are placed on their own separate line.

### Minimal

The following file is a commented version of `offlineimap.conf.minimal`.

 `~/.offlineimaprc` 
```
[general]
# List of accounts to be synced, separated by a comma.
accounts = main

[Account main]
# Identifier for the local repository; e.g. the maildir to be synced via IMAP.
localrepository = main-local
# Identifier for the remote repository; i.e. the actual IMAP, usually non-local.
remoterepository = main-remote

[Repository main-local]
# OfflineIMAP supports Maildir, GmailMaildir, and IMAP for local repositories.
type = Maildir
# Where should the mail be placed?
localfolders = ~/mail

[Repository main-remote]
# Remote repos can be IMAP or Gmail, the latter being a preconfigured IMAP.
type = IMAP
remotehost = host.domain.tld
remoteuser = username

```

### Selective folder synchronization

For synchronizing only certain folders, you can use a [folderfilter](http://offlineimap.org/doc/nametrans.html#folderfilter) in the **remote** section of the account in `~/.offlineimaprc`. For example, the following configuration will only synchronize the folders `Inbox` and `Sent`:

 `~/.offlineimaprc` 
```
[Repository main-remote]
# Synchronize only the folders Inbox and Sent:
folderfilter = lambda foldername: foldername in ["Inbox", "Sent"]
...
```

For more options, see the [official documentation](http://offlineimap.org/doc/nametrans.html#folderfilter).

## Usage

Before running offlineimap, create any parent directories that were allocated to local repositories:

```
$ mkdir ~/mail

```

Now, run the program:

```
$ offlineimap

```

Mail accounts will now be synced. If anything goes wrong, take a closer look at the error messages. OfflineIMAP is usually very verbose about problems; partly because the developers did not bother with taking away tracebacks from the final product.

## Tips and tricks

### Running offlineimap in the background

Most other mail transfer agents assume that the user will be using the tool as a [daemon](/index.php/Daemon "Daemon") by making the program sync periodically by default. In offlineimap, there are a few settings that control backgrounded tasks.

Confusingly, they are spread thin all-over the configuration file:

 `~/.offlineimaprc` 
```
# In the general section
[general]
# Controls how many accounts may be synced simultaneously
maxsyncaccounts = 1

# In the account identifier
[Account main]
# Minutes between syncs
autorefresh = 0.5
# Quick-syncs do not update if the only changes were to IMAP flags.
# autorefresh=0.5 together with quick=10 yields
# 10 quick refreshes between each full refresh, with 0.5 minutes between every 
# refresh, regardless of type.
quick = 10

# In the remote repository identifier
[Repository main-remote]
# Instead of closing the connection once a sync is complete, offlineimap will
# send empty data to the server to hold the connection open. A value of 60
# attempts to hold the connection for a minute between syncs (both quick and
# autorefresh).This setting has no effect if autorefresh and holdconnectionopen
# are not both set.
keepalive = 60
# OfflineIMAP normally closes IMAP server connections between refreshes if
# the global option autorefresh is specified.  If you wish it to keep the
# connection open, set this to true. This setting has no effect if autorefresh
# is not set.
holdconnectionopen = yes

```

#### systemd service

Instead of setting OfflineIMAP as a daemon, it can be managed with the packages's provided [systemd/User](/index.php/Systemd/User "Systemd/User") timer. To use it, [start/enable](/index.php/Start/enable "Start/enable") the user timer `offlineimap.timer` using the `--user` flag.

This timer by default runs OfflineIMAP every 15 minutes. This can be easily changed by creating a [drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet"). For example, the following modifies the timer to check every 5 minutes:

 `~/.config/systemd/user/offlineimap.timer.d/timer.conf` 
```
[Timer]
OnUnitInactiveSec=5m

```

For more robust solution it is possible to set a watchdog which will kill OfflineIMAP in case of freeze:

 `~/.config/systemd/user/offlineimap.service.d/service.conf` 
```
[Service]
WatchdogSec=300

```

### Automatic mailbox generation for mutt

[Mutt](/index.php/Mutt "Mutt") cannot be simply pointed to an IMAP or maildir directory and be expected to guess which subdirectories happen to be the mailboxes, yet offlineimap can generate a muttrc fragment containing the mailboxes that it syncs.

 `~/.offlineimaprc` 
```
[mbnames]
enabled = yes
filename = ~/.mutt/mailboxes
header = "mailboxes "
peritem = "+%(accountname)s/%(foldername)s"
sep = " "
footer = "
"

```

Then add the following lines to `~/.mutt/muttrc`.

 `~/.mutt/muttrc` 
```
# IMAP: offlineimap
set folder = "~/mail"
source ~/.mutt/mailboxes
set spoolfile = "+account/INBOX"
set record = "+account/Sent\ Items"
set postponed = "+account/Drafts"

```

`account` is the name you have given to your IMAP account in `~/.offlineimaprc`.

### Gmail configuration

This remote repository is configured specifically for Gmail support, substituting folder names in uppercase for lowercase, among other small additions. Keep in mind that this configuration does not sync the *All Mail* folder, since it is usually unnecessary and skipping it prevents bandwidth costs:

 `~/.offlineimaprc` 
```
[Repository gmail-remote]
type = Gmail
remoteuser = user@gmail.com
remotepass = password
nametrans = lambda foldername: re.sub ('^\[gmail\]', 'bak',
                               re.sub ('sent_mail', 'sent',
                               re.sub ('starred', 'flagged',
                               re.sub (' ', '_', foldername.lower()))))
folderfilter = lambda foldername: foldername not in ['[Gmail]/All Mail']
# Necessary as of OfflineIMAP 6.5.4
sslcacertfile = /etc/ssl/certs/ca-certificates.crt

```

**Note:**

*   If you have Gmail set to another language, the folder names may appear translated too, e.g. "verzonden_berichten" instead of "sent_mail".
*   After version 6.3.5, offlineimap also creates remote folders to match your local ones. Thus you may need a nametrans rule for your local repository too that reverses the effects of this nametrans rule. If you don't want to make a reverse nametrans rule, you can disable remote folder creation by putting this in your remote configuration: `createfolders = False`
*   As of 1 October 2012 gmail SSL certificate fingerprint is not always the same. This prevents from using `cert_fingerprint` and makes the `sslcacertfile` way a better solution for the SSL verification (see [#SSL fingerprint does not match](#SSL_fingerprint_does_not_match)).

### Password management

#### .netrc

Add the following lines to your `~/.netrc`:

```
machine hostname.tld
    login [your username]
    password [your password]

```

Do not forget to give the file appropriate rights like 600 or 700:

```
$ chmod 600 ~/.netrc

```

#### Using GPG

GNU Privacy Guard can be used for storing a password in an encrypted file. First set up [GnuPG](/index.php/GnuPG "GnuPG") and then follow the steps in this section. It is assumed that you can use your GPG private key [without entering a password](/index.php/GnuPG#gpg-agent "GnuPG") all the time.

First type in the password for the email account in a plain text file. Do this in a secure directory with `700` permissions located on a [tmpfs](/index.php/Tmpfs "Tmpfs") to avoid writing the unencrypted password to the disk. Then [encrypt](/index.php/Encrypt "Encrypt") the file with GnuPG setting yourself as the recipient.

Remove the plain text file since it is no longer needed. Move the encrypted file to the final location, e.g. `~/.offlineimappass.gpg`.

Now create a python function that will decrypt the password:

 `~/.offlineimap.py` 
```
#! /usr/bin/env python2
from subprocess import check_output

def get_pass():
    return check_output("gpg -dq ~/.offlineimappass.gpg", shell=True).strip("
")
```

Load this file from `~/.offlineimaprc` and specify the defined function:

 `~/.offlineimaprc` 
```
[general]
# Path to file with arbitrary Python code to be loaded
pythonfile = ~/.offlineimap.py
...

[Repository *example*]
# Decrypt and read the encrypted password
remotepasseval = get_pass()
...
```

#### Using pass

[pass](/index.php/Pass "Pass") is a simple password manager from the command line based on GPG.

First create a password for your email account(s):

```
$ pass insert Mail/*account*

```

Now create a python function that will decrypt the password:

 `~/.offlineimap.py` 
```
#! /usr/bin/env python2
from subprocess import check_output

def get_pass(account):
    return check_output("pass Mail/" + account, shell=True).splitlines()[0]
```

This is an example for a multi-account setup. You can customize the argument to *pass* as defined previously.

Load this file from `~/.offlineimaprc` and specify the defined function:

 `~/.offlineimaprc` 
```
[general]
# Path to file with arbitrary Python code to be loaded
pythonfile = ~/.offlineimap.py
...

[Repository Gmail]
# Decrypt and read the encrypted password
remotepasseval = get_pass("Gmail")
...
```

#### Gnome keyring

In configuration for remote repositories the remoteusereval/remotepasseval fields can be set to custom python code that evaluates to the username/password. The code can be a call to a function defined in a Python script pointed to by 'pythonfile' config field. Create `~/.offlineimap.py` according to either of the two options below and use it in the configuration:

```
[general]
pythonfile = ~/.offlineimap.py

[Repository examplerepo]
type = IMAP
remotehost = mail.example.com
remoteusereval = get_username("examplerepo")
remotepasseval = get_password("examplerepo")

```

##### Option 1: using gnomekeyring Python module

Install [python2-gnomekeyring](https://www.archlinux.org/packages/?name=python2-gnomekeyring). Then:

 `~/.offlineimap.py` 
```
#! /usr/bin/env python2

import gnomekeyring as gkey

def set_credentials(repo, user, pw):
    KEYRING_NAME = "offlineimap"
    attrs = { "repo": repo, "user": user }
    keyring = gkey.get_default_keyring_sync()
    gkey.item_create_sync(keyring, gkey.ITEM_NETWORK_PASSWORD,
        KEYRING_NAME, attrs, pw, True)

def get_credentials(repo):
    keyring = gkey.get_default_keyring_sync()
    attrs = {"repo": repo}
    items = gkey.find_items_sync(gkey.ITEM_NETWORK_PASSWORD, attrs)
    return (items[0].attributes["user"], items[0].secret)

def get_username(repo):
    return get_credentials(repo)[0]
def get_password(repo):
    return get_credentials(repo)[1]

if __name__ == "__main__":
    import sys
    import os
    import getpass
    if len(sys.argv) != 3:
        print "Usage: %s <repository> <username>" \
            % (os.path.basename(sys.argv[0]))
        sys.exit(0)
    repo, username = sys.argv[1:]
    password = getpass.getpass("Enter password for user '%s': " % username)
    password_confirmation = getpass.getpass("Confirm password: ")
    if password != password_confirmation:
        print "Error: password confirmation does not match"
        sys.exit(1)
    set_credentials(repo, username, password)

```

To set the credentials, run this script from a shell.

##### Option 2: using [gnome-keyring-query](https://aur.archlinux.org/packages/gnome-keyring-query/) tool

 `~/.offlineimap.py` 
```
#! /usr/bin/env python2
# executes gnome-keyring-query get passwd
# and returns the output

import locale
from subprocess import Popen, PIPE

encoding = locale.getdefaultlocale()[1]

def get_password(p):
    (out, err) = Popen(["gnome-keyring-query", "get", p], stdout=PIPE).communicate()
    return out.decode(encoding).strip()

```

#### python2-keyring

There is a general solution that should work for any keyring. Install [python2-keyring](http://pypi.python.org/pypi/keyring) from [AUR](/index.php/AUR "AUR"), then change your ~/.offlineimaprc to say something like:

```
[general]
pythonfile = /home/user/offlineimap.py
...
[Repository RemoteEmail]
remoteuser = username@host.net
remotepasseval = keyring.get_password("offlineimap","username@host.net")
...

```

and somewhere in ~/offlineimap.py add `import keyring`. Now all you have to do is set your password, like so:

```
$ python2 
>>> import keyring
>>> keyring.set_password("offlineimap","username@host.net", "MYPASSWORD")
```

and it will grab the password from your (kwallet/gnome-) keyring instead of having to keep it in plaintext or enter it each time.

#### Emacs EasyPG

See [http://www.emacswiki.org/emacs/OfflineIMAP#toc2](http://www.emacswiki.org/emacs/OfflineIMAP#toc2)

#### KeePass / KeePassX

Install [python2-libkeepass](https://aur.archlinux.org/packages/python2-libkeepass/) from the AUR, then add the following to your offlineimap.py file:

```
#! /usr/bin/env python2
import os, getpass
import libkeepass

def get_keepass_pw(dbpath, title="", username=""):
    if os.path.isfile(dbpath):
        with libkeepass.open(
                os.path.expanduser(dbpath),
                password=getpass.getpass("Master password for '" + dbpath +    "': ")) as kdb:
            entry = kdb.tree.xpath(
                './/Entry'
                '/String/Key[.="Title"]/../Value[.="{title}"]/../..'
                '/String/Key[.="UserName"]/../Value[.="{username}"]/../..'
                '/String/Key[.="Password"]/../Value'.format(
                    title=title,
                    username=username
                )
            )[0]
            return entry.text
    else:
        print "Error: '" + dbpath + "' does not exist."
        return

```

Next, edit your ~/.offlineimaprc:

```
[general]
# VVV Set this path correctly VVV
pythonfile = /home/user/offlineimap.py
...
[Repository RemoteEmail]
remoteuser = username@host.net
# Set the DB path as well as the title and username of the specific entry you'd like to use.
# This will prompt you on STDIN at runtime for the kdb master password.
remotepasseval = get_keepass_pw("/path/to/database.kdb", title="<entry title>", username="<entry username>")
...

```

Note that as-is, this does not support KDBs with keyfiles, only KDBs with password-only auth.

##### Old kdb format

If your key database is stored in an old format, you the xpath strings may not be correct. This method should work in that case, but it's not compatible with the current default format (v4)

Install [python2-keepass-git](https://aur.archlinux.org/packages/python2-keepass-git/) from the AUR, then add the following to your offlineimap.py file:

```
#! /usr/bin/env python2
import os, getpass
from keepass import kpdb

def get_keepass_pw(dbpath, title="", username=""):
    if os.path.isfile(dbpath):
        db = kpdb.Database(dbpath, getpass.getpass("Master password for '" + dbpath +    "': "))
        for entry in db.entries:
            if (entry.title == title) and (entry.username == username):
                return entry.password
    else:
        print "Error: '" + dbpath + "' does not exist."
        return

```

### Kerberos authentication

Install [python2-kerberos](https://aur.archlinux.org/packages/python2-kerberos/) from [AUR](/index.php/AUR "AUR") and do not specify remotepass in your .offlineimaprc. OfflineImap figure out the reset all if have a valid Kerberos TGT. If you have 'maxconnections', it will fail for some connection. Comment 'maxconnections' out will solve this problem.

## Troubleshooting

### Overriding UI and autorefresh settings

For the sake of troubleshooting, it is sometimes convenient to launch offlineimap with a more verbose UI, no background syncs and perhaps even a debug level:

```
$ offlineimap [ -o ] [ -d <debug_type> ] [ -u <ui> ]

```

	-o

	Disable autorefresh, keepalive, etc.

	-d <debug_type>

	Where *<debug_type>* is one of `imap`, `maildir` or `thread`. Debugging imap and maildir are, by far, the most useful.

	-u <ui>

	Where *<ui>* is one of `CURSES.BLINKENLIGHTS`, `TTY.TTYUI`, `NONINTERACTIVE.BASIC`, `NONINTERACTIVE.QUIET` or `MACHINE.MACHINEUI`. TTY.TTYUI is sufficient for debugging purposes.

**Note:** More recent versions use the following for <ui>: `blinkenlights`, `ttyui`, `basic`, `quiet` or `machineui`.

### Folder could not be created

In version 6.5.3, offlineimap gained the ability to create folders in the remote repository, as described [here](http://comments.gmane.org/gmane.mail.imap.offlineimap.general/4784).

This can lead to errors of the following form when using `nametrans` on the remote repository:

```
ERROR: Creating folder bar on repository foo-remote
  Folder 'bar'[foo-remote] could not be created. Server responded: ('NO', ['[ALREADYEXISTS] Duplicate folder name bar (Failure)'])

```

The solution is to provide an inverse `nametrans` lambda for the local repository, e.g.

 `~/.offlineimaprc` 
```
[Repository foo-local]
nametrans = lambda foldername: foldername.replace('bar', 'BAR')

[Repository foo-remote]
nametrans = lambda foldername: foldername.replace('BAR', 'bar')

```

*   For working out the correct inverse mapping. the output of `offlineimap --info` should help.
*   After updating the mapping, it may be necessary to remove all of the folders under `$HOME/.offlineimap/` for the affected accounts.

### SSL fingerprint does not match

```
ERROR: Server SSL fingerprint 'keykeykey' for hostname 'example.com' does not match configured fingerprint. Please verify and set 'cert_fingerprint' accordingly if not set yet.

```

To solve this, add to `~/.offlineimaprc` (in the same section as `ssl = yes`) one of the following:

*   either add `cert_fingerprint`, with the certificate fingerprint of the remote server. This checks whether the remote server certificate matches the given fingerprint.

```
cert_fingerprint = keykeykey

```

*   or add `sslcacertfile` with the path to the system CA certificates file. Needs [ca-certificates](https://www.archlinux.org/packages/?name=ca-certificates) installed. This validates the remote ssl certificate chain against the Certification Authorities in that file.

```
sslcacertfile = /etc/ssl/certs/ca-certificates.crt

```

### Copying message, connection closed

```
ERROR: Copying message -2 [acc: email] connection closed
Folder sent [acc: email]: ERROR: while syncing sent [account email] connection closed

```

Cause of this can be creation of same message both locally and on server. This happens if your email provider automatically saves sent mails to same folder as your local client. If you encounter this, disable save of sent messages in your local client.

## See also

*   [Official OfflineIMAP mailing list](https://lists.alioth.debian.org/mailman/listinfo/offlineimap-project)
*   [Mutt + Gmail + Offlineimap](https://pbrisbin.com/posts/mutt_gmail_offlineimap/) - An outline of brisbin's simple gmail/mutt setup using cron to keep offlineimap syncing.