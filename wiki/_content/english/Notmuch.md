Related articles

*   [mutt](/index.php/Mutt "Mutt")

[Notmuch](http://notmuchmail.org/) is a mail indexer. Essentially, is a very thin front end on top of *xapian*. Much like [Sup](/index.php/Sup "Sup"), it focuses on one thing: indexing your email messages. Notmuch can be used as an email reader, or simply as an indexer and search tool for other MUAs, like [mutt](/index.php/Mutt "Mutt").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Overview](#Overview)
*   [2 First time Usage](#First_time_Usage)
*   [3 Frontends](#Frontends)
    *   [3.1 Emacs](#Emacs)
    *   [3.2 Vim](#Vim)
    *   [3.3 alot](#alot)
    *   [3.4 bower](#bower)
    *   [3.5 Neomutt](#Neomutt)
    *   [3.6 astroid](#astroid)
*   [4 Integrating with mutt](#Integrating_with_mutt)
*   [5 Integrating with NeoMutt](#Integrating_with_NeoMutt)
*   [6 Permanently delete emails](#Permanently_delete_emails)

## Overview

Notmuch is written in C and an order of magnitude faster than sup-mail. Notmuch can be terminated during the indexing process, on the next run it will continue where it left off. Also like sup-mail, it does not provide a way to permanently delete unwanted email messages (however, see [#Permanently delete emails](#Permanently_delete_emails)). It doesn't fetch or send mails, nor does it store your email addresses, you'll need to use programs like [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP"), [msmtp](/index.php/Msmtp "Msmtp") and *abook* for those tasks.

Install the [notmuch](https://www.archlinux.org/packages/?name=notmuch) package. It provides [python](/index.php/Python "Python"), [vim](/index.php/Vim "Vim"), and [emacs](/index.php/Emacs "Emacs") bindings.

## First time Usage

After installation, you enter an interactive setup by running:

```
 notmuch setup

```

The program prompts you for the location of your maildir and your primary and secondary email addresses. You can also edit the config file directly which is created by default at `$HOME/.notmuch-config`.

Subsequent re-indexing of the mail directories is done with:

```
 notmuch new

```

## Frontends

There are [a range of ways to use notmuch](http://notmuchmail.org/frontends/), including cli, or with one of the Unix $EDITORS:

### Emacs

The default frontend for notmuch is Emacs. It is developed by the same people that develop notmuch.

### Vim

There is a vim interface available and included in the [notmuch-vim](https://www.archlinux.org/packages/?name=notmuch-vim) package. To start it, type:

```
vim -c NotMuch

```

### alot

alot is a standalone CLI interface for notmuch, written in python. It is available as [alot](https://www.archlinux.org/packages/?name=alot) and [alot-git](https://aur.archlinux.org/packages/alot-git/).

Alot uses [mailcap](https://en.wikipedia.org/wiki/Mailcap "wikipedia:Mailcap") for handling different kinds of files. This currently includes html mails, which means that you need to configure a `~/.mailcap` file in order to view html mails. As minimum, put this line into your `~/.mailcap`:

```
 text/html; w3m -dump -o -document_charset=%{charset} %s; nametemplate=%s.html; copiousoutput

```

This uses [w3m](https://www.archlinux.org/packages/?name=w3m), some other text based clients such as [links](https://www.archlinux.org/packages/?name=links) or [lynx](https://www.archlinux.org/packages/?name=lynx) can be used instead, although their arguments might differ.

More file handlers can be configured of course.

### bower

[bower](https://github.com/wangp/bower) is another CLI interface, this one is written in [Mercury](https://mercurylang.org/). It is available as [bower-mail](https://aur.archlinux.org/packages/bower-mail/).

### Neomutt

[Neomutt](https://www.neomutt.org/) - Another mutt fork which includes many feature patches, among them the [Notmuch](http://www.neomutt.org/feature/notmuch) integration patch. Install the [neomutt](https://www.archlinux.org/packages/?name=neomutt) or the [neomutt-git](https://aur.archlinux.org/packages/neomutt-git/) package.

### astroid

[Astroid](https://github.com/astroidmail/astroid) is a graphical MUA and interface to notmuch written using C++ and GTK. [astroid](https://aur.archlinux.org/packages/astroid/) (stable) and [astroid-git](https://aur.archlinux.org/packages/astroid-git/) (VCS) packages are available. The GUI is designed to be very fast, preview HTML and attachments, be navigable by keyboard. It is extensively configurable and you use your favorite editor either embedded or launch it externally. Check out the [Tour](https://github.com/astroidmail/astroid/wiki) to see how astroid can be used and for a description of the complete setup, or check out the [README](https://github.com/astroidmail/astroid) for more information.

## Integrating with mutt

If you use [mutt](/index.php/Mutt "Mutt") as your MUA, then notmuch is an excellent complementary tool to index and search your mail. The [notmuch-mutt](https://www.archlinux.org/packages/?name=notmuch-mutt) package provides a script to integrate notmuch with mutt.

After installing the [notmuch-mutt](https://www.archlinux.org/packages/?name=notmuch-mutt) package and configuring notmuch, the only thing left before using notmuch to search from mutt is adding keybindings to call the `notmuch-mutt` perl script from mutt. Adding the following to your `.muttrc` is what is recommended in notmuch contrib source:

```
macro index <F8> \
"<enter-command>set my_old_pipe_decode=\$pipe_decode my_old_wait_key=\$wait_key nopipe_decode nowait_key<enter>\
<shell-escape>notmuch-mutt -r --prompt search<enter>\
<change-folder-readonly>`echo ${XDG_CACHE_HOME:-$HOME/.cache}/notmuch/mutt/results`<enter>\
<enter-command>set pipe_decode=\$my_old_pipe_decode wait_key=\$my_old_wait_key<enter>" \
"notmuch: search mail"

macro index <F9> \
"<enter-command>set my_old_pipe_decode=\$pipe_decode my_old_wait_key=\$wait_key nopipe_decode nowait_key<enter>\
<pipe-message>notmuch-mutt -r thread<enter>\
<change-folder-readonly>`echo ${XDG_CACHE_HOME:-$HOME/.cache}/notmuch/mutt/results`<enter>\
<enter-command>set pipe_decode=\$my_old_pipe_decode wait_key=\$my_old_wait_key<enter>" \
"notmuch: reconstruct thread"

macro index <F6> \
"<enter-command>set my_old_pipe_decode=\$pipe_decode my_old_wait_key=\$wait_key nopipe_decode nowait_key<enter>\
<pipe-message>notmuch-mutt tag -- -inbox<enter>\
<enter-command>set pipe_decode=\$my_old_pipe_decode wait_key=\$my_old_wait_key<enter>" \
"notmuch: remove message from inbox"

```

The above uses `F8` to search your inbox using notmuch, `F9` to create threads from search results, and `F6` to tag search results.

## Integrating with NeoMutt

If you use [neomutt](https://www.archlinux.org/packages/?name=neomutt), the [notmuch-mutt](https://www.archlinux.org/packages/?name=notmuch-mutt) package is not required. Instead, create a `~/.mailboxes` with some basic (virtual) mailboxes. A virtual mailbox is not an actual folder, but the result of a notmuch query for a specific tag:

 `~/.mailboxes` 
```
virtual-mailboxes "inbox" "notmuch://?query=tag:inbox"
virtual-mailboxes "archive" "notmuch://?query=tag:archive"
virtual-mailboxes "sent" "notmuch://?query=tag:sent"
virtual-mailboxes "newsletters" "notmuch://?query=tag:newsletters"
```

Next, make mutt aware of your virtual mailboxes by enabling virtual spoolfile and sourcing the latter:

 `~/.muttrc` 
```
set virtual_spoolfile=yes
set folder=*notmuch-root-folder*
source ~/.mailboxes
```

At this point, mutt will still list your mailboxes as empty, because your mails are not yet tagged and thus, notmuch querys are empty. To fill your virtual mailboxes, you need to initially tag the messages in your maildir. A very simple approach is to create a shell script like the following:

 `~/.scripts/notmuch-hook.sh` 
```
#!/bin/sh
notmuch new
# retag all "new" messages "inbox" and "unread"
notmuch tag +inbox +unread -new -- tag:new
# tag all messages from "me" as sent and remove tags inbox and unread
notmuch tag -new -inbox +sent -- from:me@example.org or from:me@myself.com
# tag newsletters, but dont show them in inbox
notmuch tag +newsletters +unread -new -- from:newsletter@example.org or subject:'newsletter*'
```

Make the shell script executable and run it:

```
 chmod +x ~/.scripts/notmuch-hook.sh
 ~/.scripts/notmuch-hook.sh

```

For the above example to work, make sure that notmuch tags new messages as 'new':

 `~/.notmuch-config` 
```
[new]
tags=new
```

Finally, your hook script needs to rerun on new mail arrival. If you use [offlineimap](https://www.archlinux.org/packages/?name=offlineimap) to sync IMAP to a local maildir, create a post sync hook:

 `~/.offlineimaprc` 
```
[Account myaccount]
postsynchook = ~/.scripts/notmuch-hook.sh
```

Some useful key bindings:

 `~/.muttrc` 
```
macro index A "<modify-labels>+archive -unread -inbox\
" "Archive message"
macro index c "<change-vfolder>?" "Change to vfolder overview"
macro index \\\\ "<vfolder-from-query>" "Search mailbox"
```

## Permanently delete emails

One choice is to maintain a tag of emails you wish to remove from your disk, for example, "killed". Then, you can combine the search for the tags with `xargs` to delete them permanently:

```
 notmuch search --output=files --format=text0 tag:killed | xargs -r0 rm
 notmuch new

```

By placing this into the `pre-new` hook for notmuch you can make sure you delete files before updating the database.