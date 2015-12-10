# nmh

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [S-nail](/index.php/S-nail "S-nail")
*   [msmtp](/index.php/Msmtp "Msmtp")
*   [Mutt](/index.php/Mutt "Mutt")
*   [Postfix](/index.php/Postfix "Postfix")
*   [Notmuch](/index.php/Notmuch "Notmuch")

**nmh** (new message handler), is a powerful electronic mail handling system. Following the Unix Philosophy, nmh is made up by a collection of simple programs each of which has a single purpose. This architecture allows the user to intersperse nmh with other commands at the shell prompt and to write scripts tailored to their needs.

## Contents

*   [1 Installing](#Installing)
*   [2 Configuring](#Configuring)
*   [3 Usage](#Usage)
*   [4 Frontends](#Frontends)
    *   [4.1 MH-specific Frontends](#MH-specific_Frontends)
    *   [4.2 MH-compatible Frontends](#MH-compatible_Frontends)
*   [5 See also](#See_also)

## Installing

Install [nmh](https://aur.archlinux.org/packages/nmh/)<sup><small>AUR</small></sup> or [nmh-git](https://aur.archlinux.org/packages/nmh-git/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

Optionally install a utility to handle IMAP or POP, for example [fdm](https://www.archlinux.org/packages/?name=fdm), [offlineimap](https://www.archlinux.org/packages/?name=offlineimap) or [getmail](https://www.archlinux.org/packages/?name=getmail).

Also optionally install [msmtp](https://www.archlinux.org/packages/?name=msmtp) or another utility for sending mail.

## Configuring

_nmh_ is extensively configurable in a variety of ways. The primary of these is the `~/.mh_profile` file.

The syntax for .mh_profile is unusual. For example, nmh will refuse to run if there are blank lines in the file. Read the mh_profile (5) man page for more.

By default, _nmh_ uses `~/Mail` as your mail folder. To change this, set `Path`:

```
 Path: path/to/mail/folder

```

**Note:**

*   Path can be either full (if prefixed with `/`) or relative to $HOME.
*   Nmh uses the mh mail format, which is different from the maildir and mbox. Setting your Path to a preexisting maildir folder, for example, will not work.

Set inbox (relative to Path):

```
 Inbox: inbox

```

Also by default, nmh populates the mail folder with the `inc` command, which incorporates mail from the user's mail drop (`/var/mail/user`).

If you have a non-standard mail drop path, you can set an [environment variable](/index.php/Environment_variable "Environment variable") `$MAILDROP`, or set MailDrop in `mh_profile`:

```
 MailDrop: /path/to/mail-drop

```

or set inc:

```
 inc: -file /path/to/mail-drop

```

**Note:** For each _nmh_ command (see list below) the user can set default flags with a line of the form `command: -flag` format in mh_profile. These work much like bash aliases.

_Nmh_ is also capable of retrieving mail via POP. A basic POP setup (see inc (1) man page for more):

```
 inc: -host example.com -user username -sasl

```

## Usage

To become familiar with basic nmh usage, learn and practice the following commands:

<table class="wikitable">

<tbody>

<tr>

<th width="75">Command</th>

<th>Description</th>

</tr>

<tr>

<td>inc</td>

<td>Incorporate new mail.</td>

</tr>

<tr>

<td>scan</td>

<td>Scan the contents of the current folder.</td>

</tr>

<tr>

<td>folder/folders</td>

<td>Change the current folder or list folders and their contents.</td>

</tr>

<tr>

<td>show</td>

<td>Display messages.</td>

</tr>

<tr>

<td>comp</td>

<td>Compose a new message.</td>

</tr>

<tr>

<td>repl</td>

<td>Reply to a message.</td>

</tr>

<tr>

<td>refile</td>

<td>Move a message to another folder.</td>

</tr>

</tbody>

</table>

## Frontends

While _nmh_ is fully usable from the command-line, several console-based and graphical user interfaces exist. Also, some common mail tools interact smoothly with the _mh_ format.

### MH-specific Frontends

*   [MH-V](http://www.hep.wisc.edu/~rader/mh-v/), a console interface to _mh/nmh_ with vi- keybindings.
*   [MH-E](http://www.beedub.com/exmh/), a console interface to _mh/nmh_ with Emacs keybindings.
*   [exmh](http://mh-e.sourceforge.net/), a TK-based mh GUI.

### MH-compatible Frontends

*   Popular MUA [mutt](/index.php/Mutt "Mutt") understands mh format. (Use `set mbox_type = mh` in your muttrc.)
*   Full-text mail indexer and search utility [mairix](http://www.rpcurnow.force9.co.uk/mairix/) can read and write in _mh_ format. (Use `mh=path/to/mh/folder` and `mformat=mh` in .mairixrc)

## See also

*   [Nmh official site](http://www.nongnu.org/nmh/)
*   [Nmh project page on savannah](http://savannah.nongnu.org/projects/nmh/)
*   [Nmh-workers mailing list](https://lists.nongnu.org/mailman/listinfo/nmh-workers)
*   ['MH & nmh: Email for Users & Programmers' (book)](http://rand-mh.sourceforge.net/book/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Nmh&oldid=376938](https://wiki.archlinux.org/index.php?title=Nmh&oldid=376938)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Email clients](/index.php/Category:Email_clients "Category:Email clients")