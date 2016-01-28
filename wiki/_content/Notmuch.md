# Notmuch

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [mutt](/index.php/Mutt "Mutt")

[Notmuch](http://notmuchmail.org/) is a mail indexer. Essentially, is a very thin front end on top of _xapian_. Much like [Sup](/index.php/Sup "Sup"), it focuses on one thing: indexing your email messages. Notmuch can be used as an email reader, or simply as an indexer and search tool for other MUAs, like [mutt](/index.php/Mutt "Mutt").

## Contents

*   [1 Overview](#Overview)
*   [2 First time Usage](#First_time_Usage)
*   [3 Frontends](#Frontends)
    *   [3.1 Emacs](#Emacs)
    *   [3.2 Vim](#Vim)
    *   [3.3 alot](#alot)
    *   [3.4 bower](#bower)
    *   [3.5 ner](#ner)
*   [4 Integrating with mutt](#Integrating_with_mutt)

## Overview

Notmuch is written in C and an order of magnitude faster than sup-mail. Notmuch can be terminated during the indexing process, on the next run it will continue where it left off. Also like sup-mail, it does not provide a way to permanently delete unwanted email messages. It doesn't fetch or send mails, nor does it store your email addresses, you'll need to use programs like [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP"), [msmtp](/index.php/Msmtp "Msmtp") and _abook_ for those tasks.

Notmuch is available in the [official repositories](/index.php/Official_repositories "Official repositories"): [notmuch](https://www.archlinux.org/packages/?name=notmuch) or [notmuch-git](https://aur.archlinux.org/packages/notmuch-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/notmuch-git)]</sup> from the [AUR](/index.php/AUR "AUR")

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

alot is a standalone CLI interface for notmuch, written in python. It is available from [AUR](/index.php/AUR "AUR") as [alot](https://aur.archlinux.org/packages/alot/)<sup><small>AUR</small></sup> or [alot-git](https://aur.archlinux.org/packages/alot-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/alot-git)]</sup>.

Alot uses [mailcap](https://en.wikipedia.org/wiki/Mailcap) for handling different kinds of files. This currently includes html mails, which means that you need to configure a `~/.mailcap` file in order to view html mails. As minimum, put this line into your `~/.mailcap`:

```
 text/html; w3m -dump %s; nametemplate=%s.html; copiousoutput

```

More file handlers can be configured of course.

### bower

[bower](https://github.com/wangp/bower) is another CLI interface, this one is written in [Mercury](https://mercurylang.org/).

### ner

[ner](http://the-ner.org/) - notmuch email reader - is yet another CLI interface, apparently written in C++.

[ner-git](https://aur.archlinux.org/packages/ner-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ner-git)]</sup> is available from the [AUR](/index.php/AUR "AUR").

## Integrating with mutt

If you use [mutt](/index.php/Mutt "Mutt") as your MUA, then notmuch is an excellent complementary tool to index and search your mail. The [notmuch-mutt](https://www.archlinux.org/packages/?name=notmuch-mutt) package provides a script to integrate notmuch with mutt.

Refer to the [notmuch-mutt](https://www.archlinux.org/packages/?name=notmuch-mutt) man page for configuration information. This [blogpost](http://jasonwryan.com/blog/2012/05/23/notmuch/) steps through how to setup notmuch with mutt, but the information is a little outdated.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Notmuch&oldid=413712](https://wiki.archlinux.org/index.php?title=Notmuch&oldid=413712)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Email clients](/index.php/Category:Email_clients "Category:Email clients")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")