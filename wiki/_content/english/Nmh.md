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

Install [nmh](https://aur.archlinux.org/packages/nmh/) or [nmh-git](https://aur.archlinux.org/packages/nmh-git/) from the [AUR](/index.php/AUR "AUR").

Optionally install a utility to handle IMAP or POP, for example [fdm](https://www.archlinux.org/packages/?name=fdm), [offlineimap](https://www.archlinux.org/packages/?name=offlineimap) or [getmail](https://www.archlinux.org/packages/?name=getmail).

Also optionally install [msmtp](https://www.archlinux.org/packages/?name=msmtp) or another utility for sending mail.

## Configuring

*nmh* is extensively configurable in a variety of ways. The primary of these is the `~/.mh_profile` file.

The syntax for .mh_profile is unusual. For example, nmh will refuse to run if there are blank lines in the file. Read the mh_profile (5) man page for more.

By default, *nmh* uses `~/Mail` as your mail folder. To change this, set `Path`:

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

**Note:** For each *nmh* command (see list below) the user can set default flags with a line of the form `command: -flag` format in mh_profile. These work much like bash aliases.

*Nmh* is also capable of retrieving mail via POP. A basic POP setup (see inc (1) man page for more):

```
 inc: -host example.com -user username -sasl

```

## Usage

To become familiar with basic nmh usage, learn and practice the following commands:

| Command | Description |
| inc | Incorporate new mail. |
| scan | Scan the contents of the current folder. |
| folder/folders | Change the current folder or list folders and their contents. |
| show | Display messages. |
| comp | Compose a new message. |
| repl | Reply to a message. |
| refile | Move a message to another folder. |

## Frontends

While *nmh* is fully usable from the command-line, several console-based and graphical user interfaces exist. Also, some common mail tools interact smoothly with the *mh* format.

### MH-specific Frontends

*   [MH-V](http://www.hep.wisc.edu/~rader/mh-v/), a console interface to *mh/nmh* with vi- keybindings.
*   [MH-E](http://www.beedub.com/exmh/), a console interface to *mh/nmh* with Emacs keybindings.
*   [exmh](http://mh-e.sourceforge.net/), a TK-based mh GUI.

### MH-compatible Frontends

*   Popular MUA [mutt](/index.php/Mutt "Mutt") understands mh format. (Use `set mbox_type = mh` in your muttrc.)
*   Full-text mail indexer and search utility [mairix](http://www.rpcurnow.force9.co.uk/mairix/) can read and write in *mh* format. (Use `mh=path/to/mh/folder` and `mformat=mh` in .mairixrc)

## See also

*   [Nmh official site](http://www.nongnu.org/nmh/)
*   [Nmh project page on savannah](http://savannah.nongnu.org/projects/nmh/)
*   [Nmh-workers mailing list](https://lists.nongnu.org/mailman/listinfo/nmh-workers)
*   ['MH & nmh: Email for Users & Programmers' (book)](http://rand-mh.sourceforge.net/book/)