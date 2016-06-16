[Notmuch](http://notmuchmail.org/) is a mail indexer. Essentially, is a very thin front end on top of *xapian*. Much like [Sup](/index.php/Sup "Sup"), it focuses on one thing: indexing your email messages. Notmuch can be used as an email reader, or simply as an indexer and search tool for other MUAs, like [mutt](/index.php/Mutt "Mutt").

## Contents

*   [1 Overview](#Overview)
*   [2 First time Usage](#First_time_Usage)
*   [3 Frontends](#Frontends)
    *   [3.1 Emacs](#Emacs)
    *   [3.2 Vim](#Vim)
    *   [3.3 alot](#alot)
    *   [3.4 bower](#bower)
    *   [3.5 mutt-kz](#mutt-kz)
    *   [3.6 ner](#ner)
*   [4 Integrating with mutt](#Integrating_with_mutt)
    *   [4.1 notmuch-mutt problems](#notmuch-mutt_problems)

## Overview

Notmuch is written in C and an order of magnitude faster than sup-mail. Notmuch can be terminated during the indexing process, on the next run it will continue where it left off. Also like sup-mail, it does not provide a way to permanently delete unwanted email messages. It doesn't fetch or send mails, nor does it store your email addresses, you'll need to use programs like [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP"), [msmtp](/index.php/Msmtp "Msmtp") and *abook* for those tasks.

Notmuch is available in the [official repositories](/index.php/Official_repositories "Official repositories"): [notmuch](https://www.archlinux.org/packages/?name=notmuch) or [notmuch-git](https://aur.archlinux.org/packages/notmuch-git/) from the [AUR](/index.php/AUR "AUR")

It provides [python](/index.php/Python "Python"), [vim](/index.php/Vim "Vim"), and [emacs](/index.php/Emacs "Emacs") bindings.

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

There's a vim interface available and included in notmuch. To start it, type:

```
vim -c NotMuch

```

### alot

alot is a standalone CLI interface for notmuch, written in python. It is available from [AUR](/index.php/AUR "AUR") as [alot](https://aur.archlinux.org/packages/alot/) or [alot-git](https://aur.archlinux.org/packages/alot-git/).

Alot uses [mailcap](https://en.wikipedia.org/wiki/Mailcap "wikipedia:Mailcap") for handling different kinds of files. This currently includes html mails, which means that you need to configure a `~/.mailcap` file in order to view html mails. As minimum, put this line into your `~/.mailcap`:

```
 text/html; w3m -dump -o -document_charset=%{charset} %s; nametemplate=%s.html; copiousoutput

```

This uses [w3m](https://www.archlinux.org/packages/?name=w3m), some other text based clients such as [links](https://www.archlinux.org/packages/?name=links) or [lynx](https://www.archlinux.org/packages/?name=lynx) can be used instead, although their arguments might differ.

More file handlers can be configured of course.

### bower

[bower](https://github.com/wangp/bower) is another CLI interface, this one is written in [Mercury](https://mercurylang.org/).

### mutt-kz

[mutt-kz](http://kzak.redcrew.org/doku.php?id=mutt:start) - A fork of mutt with integrated notmuch. It has a virtual folder support and talks directly to libnotmuch, avoiding hacks with symbolic links. It is available from [AUR](/index.php/AUR "AUR") as [mutt-kz](https://aur.archlinux.org/packages/mutt-kz/) or [mutt-kz-git](https://aur.archlinux.org/packages/mutt-kz-git/).

### ner

[ner](http://the-ner.org/) - notmuch email reader - is yet another CLI interface, apparently written in C++.

[ner-git](https://aur.archlinux.org/packages/ner-git/) is available from the [AUR](/index.php/AUR "AUR").

## Integrating with mutt

If you use [mutt](/index.php/Mutt "Mutt") as your MUA, then notmuch is an excellent complementary tool to index and search your mail. The [notmuch-mutt](https://www.archlinux.org/packages/?name=notmuch-mutt) package provides a script to integrate notmuch with mutt.

After installing the [notmuch-mutt](https://www.archlinux.org/packages/?name=notmuch-mutt) package and configuring notmuch, the only thing left before using notmuch to search from mutt is adding keybindings to call the `notmuch-mutt` perl script from mutt. Adding the following to your `.muttrc` is what is recommended in notmuch contrib source:

```
macro index <F8> \
     "<enter-command>unset wait_key<enter><shell-escape>notmuch-mutt --prompt search<enter><change-folder-readonly>`echo ${XDG_CACHE_HOME:-$HOME/.cache}/notmuch/mutt/results`<enter>" \
     "notmuch: search mail"
macro index <F9> \
     "<enter-command>unset wait_key<enter><pipe-message>notmuch-mutt thread<enter><change-folder-readonly>`echo ${XDG_CACHE_HOME:-$HOME/.cache}/notmuch/mutt/results`<enter><enter-command>set wait_key<enter>" \
     "notmuch: reconstruct thread"
macro index <F6> \
     "<enter-command>unset wait_key<enter><pipe-message>notmuch-mutt tag -inbox<enter>" \
     "notmuch: remove message from inbox"

```

The above uses `F8` to search your inbox using notmuch, `F9` to create threads from search results, and `F6` to tag search results.

### notmuch-mutt problems

There can sometimes be disagreement between pacman-installed and managed perl modules and perl modules installed via cpan/cpanm. An error message of the format:

```
Gnu.c: loadable library and perl binaries are mismatched (got handshake key 0xdb00080, needed 0xdb80080)

```

can indicate that some of the notmuch-mutt dependencies are installed via cpan while some are installed and managed via pacman, and that you should install all dependencies via one or the other method.