Related articles

*   [fdm](/index.php/Fdm "Fdm")
*   [msmtp](/index.php/Msmtp "Msmtp")
*   [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP")
*   [isync](/index.php/Isync "Isync")

[Mutt](http://www.mutt.org/) is a text-based mail client renowned for its powerful features. Though over 2 decades old, Mutt remains the mail client of choice for a great number of power-users.

Mutt focuses primarily on being a Mail User Agent (MUA), and was originally written to view mail. Later implementations (added for retrieval, sending, and filtering mail) are simplistic compared to other mail applications and, as such, users may wish to use external applications to extend Mutt's capabilities.

Nevertheless, the Arch Linux [mutt](https://www.archlinux.org/packages/?name=mutt) package is compiled with IMAP, POP3 and SMTP support, removing the necessity for external applications.

This article covers using both native IMAP sending and retrieval, and a setup depending on [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP") or [getmail](/index.php/Getmail "Getmail") (POP3) to retrieve mail, [procmail](/index.php/Procmail "Procmail") to filter it in the case of POP3, and [msmtp](/index.php/Msmtp "Msmtp") to send it.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 NeoMutt](#NeoMutt)
*   [2 Configuration](#Configuration)
    *   [2.1 IMAP](#IMAP)
        *   [2.1.1 Native IMAP support](#Native_IMAP_support)
            *   [2.1.1.1 imap_user](#imap_user)
            *   [2.1.1.2 imap_pass](#imap_pass)
            *   [2.1.1.3 folder](#folder)
            *   [2.1.1.4 spoolfile](#spoolfile)
            *   [2.1.1.5 mailboxes](#mailboxes)
            *   [2.1.1.6 Summary](#Summary)
        *   [2.1.2 External IMAP support](#External_IMAP_support)
    *   [2.2 POP3](#POP3)
    *   [2.3 Maildir](#Maildir)
    *   [2.4 SMTP](#SMTP)
        *   [2.4.1 Folders](#Folders)
        *   [2.4.2 Native SMTP support](#Native_SMTP_support)
        *   [2.4.3 External SMTP support](#External_SMTP_support)
        *   [2.4.4 Sending mails from Mutt](#Sending_mails_from_Mutt)
    *   [2.5 Multiple accounts](#Multiple_accounts)
    *   [2.6 Passwords management](#Passwords_management)
        *   [2.6.1 Security concern](#Security_concern)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Key bindings](#Key_bindings)
    *   [3.2 Composition](#Composition)
        *   [3.2.1 Encrypt and sign mail (GnuPG)](#Encrypt_and_sign_mail_(GnuPG))
        *   [3.2.2 E-mail character encoding](#E-mail_character_encoding)
        *   [3.2.3 Custom mail headers](#Custom_mail_headers)
        *   [3.2.4 Signature block](#Signature_block)
            *   [3.2.4.1 Random signature](#Random_signature)
        *   [3.2.5 Compose and send from command line](#Compose_and_send_from_command_line)
        *   [3.2.6 Compose HTML e-mails](#Compose_HTML_e-mails)
        *   [3.2.7 Display another email while composing](#Display_another_email_while_composing)
    *   [3.3 Printing](#Printing)
    *   [3.4 Viewing content](#Viewing_content)
        *   [3.4.1 Viewing URLs in a web browser](#Viewing_URLs_in_a_web_browser)
        *   [3.4.2 Viewing HTML](#Viewing_HTML)
        *   [3.4.3 Filtering the message view](#Filtering_the_message_view)
        *   [3.4.4 Conversation grouping](#Conversation_grouping)
    *   [3.5 Configuring editors to work with mutt](#Configuring_editors_to_work_with_mutt)
        *   [3.5.1 vim](#vim)
        *   [3.5.2 GNU nano](#GNU_nano)
        *   [3.5.3 Emacs](#Emacs)
    *   [3.6 Display settings](#Display_settings)
        *   [3.6.1 Colors](#Colors)
        *   [3.6.2 Index Format](#Index_Format)
        *   [3.6.3 Display recipient instead of sender in "Sent" folder view](#Display_recipient_instead_of_sender_in_"Sent"_folder_view)
        *   [3.6.4 Variable column width](#Variable_column_width)
        *   [3.6.5 Sidebar](#Sidebar)
        *   [3.6.6 Display the index above the pager view](#Display_the_index_above_the_pager_view)
    *   [3.7 Contact management](#Contact_management)
        *   [3.7.1 Address aliases](#Address_aliases)
        *   [3.7.2 Abook](#Abook)
        *   [3.7.3 Goobook](#Goobook)
        *   [3.7.4 Khard](#Khard)
    *   [3.8 Manage multiple sender accounts](#Manage_multiple_sender_accounts)
    *   [3.9 Request IMAP mail retrieval manually](#Request_IMAP_mail_retrieval_manually)
    *   [3.10 Avoiding slow index on large (IMAP) folders due to coloring](#Avoiding_slow_index_on_large_(IMAP)_folders_due_to_coloring)
    *   [3.11 Speed up folders switch](#Speed_up_folders_switch)
    *   [3.12 Archive treated e-mails](#Archive_treated_e-mails)
    *   [3.13 Migrating mails from one computer to another](#Migrating_mails_from_one_computer_to_another)
    *   [3.14 Default folder for saving attachments](#Default_folder_for_saving_attachments)
    *   [3.15 Pager behavior](#Pager_behavior)
    *   [3.16 Fast reply](#Fast_reply)
    *   [3.17 Ignore own e-mail addresses from group-reply](#Ignore_own_e-mail_addresses_from_group-reply)
    *   [3.18 IMAP message cache](#IMAP_message_cache)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Backspace does not work in Mutt](#Backspace_does_not_work_in_Mutt)
    *   [4.2 The *change-folder* function always prompt for the same mailbox](#The_change-folder_function_always_prompt_for_the_same_mailbox)
    *   [4.3 I cannot change folder when using Mutt read-only (Mutt -R)](#I_cannot_change_folder_when_using_Mutt_read-only_(Mutt_-R))
    *   [4.4 Error sending message, child exited 127 (Exec error.).](#Error_sending_message,_child_exited_127_(Exec_error.).)
    *   [4.5 Character encoding problems](#Character_encoding_problems)
    *   [4.6 Unable to login with GMail](#Unable_to_login_with_GMail)
    *   [4.7 Not possible to open too long URLs with urlview](#Not_possible_to_open_too_long_URLs_with_urlview)
*   [5 Documentation](#Documentation)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [mutt](https://www.archlinux.org/packages/?name=mutt) package. Alternatively consider using the [#NeoMutt](#NeoMutt) package.

Optionally install external helper applications for an IMAP setup, such as [isync](/index.php/Isync "Isync"), [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP"), or [msmtp](/index.php/Msmtp "Msmtp").

Or (if using POP3) [getmail](https://www.archlinux.org/packages/?name=getmail), [fetchmail](https://www.archlinux.org/packages/?name=fetchmail) or [fdm](https://www.archlinux.org/packages/?name=fdm) and [procmail](https://www.archlinux.org/packages/?name=procmail).

**Note:**

*   If you just need the authentication methods LOGIN and PLAIN, these are satisfied with the dependency [libsasl](https://www.archlinux.org/packages/?name=libsasl)
*   If you want to (or have to) use CRAM-MD5, GSSAPI or DIGEST-MD5, install the package [cyrus-sasl-gssapi](https://www.archlinux.org/packages/?name=cyrus-sasl-gssapi)
*   If you are using Gmail as your SMTP server, you may need to install the package [cyrus-sasl](https://www.archlinux.org/packages/?name=cyrus-sasl)

### NeoMutt

The [NeoMutt](http://www.neomutt.org/) project aims to bring together all the patches for Mutt. It adds a large set of [features](http://www.neomutt.org/feature.html). Lots of old Mutt patches have been brought up-to-date, tidied and documented.

While there are many different packages of mutt in the AUR, each of them providing another set of patches, NeoMutt aims to replace them in the future by implementing appropriate compile options.

NeoMutt can be installed with the [neomutt](https://www.archlinux.org/packages/?name=neomutt) package or alternatively from the AUR at [neomutt-git](https://aur.archlinux.org/packages/neomutt-git/) for the development version.

## Configuration

This section covers [#IMAP](#IMAP), [#POP3](#POP3), [#Maildir](#Maildir) and [#SMTP](#SMTP) configuration.

Mutt will, by default, search six locations for its configuration file; `~/.muttrc`, `~/.mutt/muttrc`, and `$XDG_CONFIG_HOME/mutt/muttrc`, first with `-MUTT_VERSION` appended, then without. Any of these locations will work. In case you decide to put the initialization file somewhere else, use `$ mutt -F /path/to/.muttrc`. You should also know some prerequisite for Mutt configuration. Its syntax is very close to the Bourne Shell. For example, you can get the content of another configuration file:

```
source /path/to/other/config/file

```

You can use variables and assign the result of shell commands to them.

```
set editor=`echo \$EDITOR`

```

Here the `$` gets escaped so that it does not get substituted by Mutt before being passed to the shell. Also note the use of the backquotes, as bash syntax `$(...)` does not work. Mutt has a lot of predefined variables, but you can also set your own. User variables **must begin with "my"!**

```
set my_name = "John Doe"

```

### IMAP

#### Native IMAP support

The [mutt](https://www.archlinux.org/packages/?name=mutt) package is compiled with IMAP support. At the very least you need to have four lines in your muttrc file to be able to access your mail.

##### imap_user

```
set imap_user=USERNAME

```

**Tip:** Continuing with the previous example, remember that Gmail requires your full email address (this is not standard): `set imap_user=your.username@gmail.com` 

##### imap_pass

If unset, the password will be prompted for.

```
set imap_pass=SECRET

```

**Tip:** If you have enabled two-factor authentication in Gmail and you have added an application specific password for Mutt, you will want to use that password here rather than your regular Gmail password.

##### folder

Instead of a local directory which contains all your mail (and directories), use your server (and the highest folder in the hierarchy, if needed).

```
set folder=imap[s]://imap.server.domain[:port]/[folder/]

```

You do not have to use a folder, but it might be convenient if you have all your other folders inside your INBOX, for example. Whatever you set here as your folder can be accessed later in Mutt with just an equal sign (=) or a plus sign (+). Example:

```
set folder=imaps://imap.gmail.com/

```

It should be noted that for several accounts, it is best practice to use different folders -- e.g. for *account-hook*. If you have several Gmail account, use

```
set folder=imaps://username@imap.gmail.com/

```

instead, where your account is *username@gmail.com*. This way it will be possible to distinguish the different folders. Otherwise it would lead to authentication errors.

##### spoolfile

The spoolfile is the folder where your (unfiltered) e-mail arrives. Most e-mail services conventionally name it *INBOX*. You can now use '=' or '+' as a substitution for the full `folder` path that was configured above. For example:

```
set spoolfile=+INBOX

```

##### mailboxes

Any IMAP folders that should be checked regularly for new mail should be listed here:

```
mailboxes =INBOX =family
mailboxes imaps://imap.gmail.com/INBOX imaps://imap.gmail.com/family

```

Alternatively, check for all subscribed IMAP folders (as if all were added with a `mailboxes` line):

```
set imap_check_subscribed

```

These two versions are equivalent if you want to subscribe to all folders. So the second method is much more convenient, but the first one gives you more flexibility. Also, newer Mutt versions are configured by default to include a macro bound to the 'y' key which will allow you to change to any of the folders listed under mailboxes.

If you do not set this variable, the *spoolfile* will be used by default. This variable is also important for the [#Sidebar](#Sidebar).

##### Summary

Using these options, you will be able to start Mutt, enter your IMAP password, and start reading your mail. Here is a muttrc snippet (for Gmail) with some other lines you might consider adding for better IMAP support.

```
set folder      = imaps://imap.gmail.com/
set imap_user   = your.username@gmail.com
set imap_pass   = your-imap-password
set spoolfile   = +INBOX
mailboxes       = +INBOX

# Store message headers locally to speed things up.
# If hcache is a folder, Mutt will create sub cache folders for each account which may speeds things up even more.
set header_cache = ~/.cache/mutt

# Store messages locally to speed things up, like searching message bodies.
# Can be the same folder as header_cache.
# This will cost important disk usage according to your e-mail amount.
set message_cachedir = "~/.cache/mutt"

# Specify where to save and/or look for postponed messages.
set postponed = +[Gmail]/Drafts

# Allow Mutt to open a new IMAP connection automatically.
unset imap_passive

# Keep the IMAP connection alive by polling intermittently (time in seconds).
set imap_keepalive = 300

# How often to check for new mail (time in seconds).
set mail_check = 120
```

#### External IMAP support

While IMAP support is built into Mutt, it does not download mail for offline use. It is possible to use an external application such as [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP") or [isync](/index.php/Isync "Isync") to download your emails to a local folder which can then be processed by Mutt.

Consider using applications such as [spamassassin](https://www.archlinux.org/packages/?name=spamassassin) or [imapfilter](https://aur.archlinux.org/packages/imapfilter/) to sort mail.

### POP3

The [mutt](https://www.archlinux.org/packages/?name=mutt) package is compiled with POP3 support, which is configured via the `pop_*` variables as described in `muttrc(5)`.

Alternatively, it is possible to use external programs to fetch mail using POP3\. One popular option is to use [getmail](/index.php/Getmail "Getmail") for retrieving and [procmail](/index.php/Procmail "Procmail") for filtering the mail.

### Maildir

Maildir is a generic and standardized format. Almost every MUA is able to handle Maildirs and Mutt's support is excellent. There are just a few simple things that you need to do to get Mutt to use them. Open your muttrc and add the following lines:

```
set mbox_type=Maildir
set folder=~/mail
set spoolfile=+/
set header_cache=~/.cache/mutt
```

This is a minimal Configuration that enables you to access your Maildir and checks for new local Mails in INBOX. This configuration also caches the headers of the eMails to speed up directory-listings. It might not be enabled in your build (but it sure is in the Arch-Package). Note that this does not affect OfflineIMAP in any way. It always syncs all of the directories on a Server. `spoolfile` tells Mutt which local directories to poll for new Mail. You might want to add more Spoolfiles (for example the Directories of Mailing-Lists) and maybe other things. But this is subject to the Mutt manual and beyond the scope of this document.

### SMTP

Whether you use POP or IMAP to receive mail you will probably still send mail using SMTP.

#### Folders

There is basically only one important folder here: the one where all your sent e-mails will be saved.

```
set record = +Sent

```

Gmail automatically saves sent e-mail to `+[Gmail]/Sent`, so we do not want duplicates.

```
unset record

```

#### Native SMTP support

The [mutt](https://www.archlinux.org/packages/?name=mutt) package is compiled with SMTP support.

For example:

```
set my_pass='mysecretpass'
set my_user=myname

set realname = 'Your Real Name'
set from = your-email-address
set use_from = yes

set smtp_url=smtps://$my_user:$my_pass@smtp.domain.tld
set ssl_force_tls = yes
```

Note that if your SMTP credentials are the same as your IMAP credentials, then you can use those variables:

 `set smtp_url=smtps://$imap_user:$imap_pass@smtp.domain.tld` 

You may need to tweak the security parameters. If you get an error like `SSL routines:SSL23_GET_SERVER_HELLO:unknown protocol`, then your server probably uses the SMTP instead of SMTPS.

 `set smtp_url=smtp://$imap_user:$imap_pass@smtp.domain.tld` 

There are other variables that you may need to set. For example for use of STARTTLS:

 `set ssl_starttls = yes` 

If your server uses the LOGIN authentication method you might need to specify this explicitly, despite the manual's claim that all methods are tried by default:

 `set smtp_authenticators = "login"` 

See [muttrc(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/muttrc.5) for more information.

#### External SMTP support

An external SMTP agent such as [msmtp](/index.php/Msmtp "Msmtp"), [SSMTP](/index.php/SSMTP "SSMTP") or [opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd) can also be used.

The `sendmail` variable in your `muttrc` determines the program and arguments used to deliver mail in mutt. Any additional arguments must be interpreted by the program as recipient addresses.

For example, if using [msmtp](/index.php/Msmtp "Msmtp"):

 `muttrc` 
```
set realname='Disgruntled Kangaroo'

set sendmail="/usr/bin/msmtp"

set edit_headers=yes
set folder=~/mail
set mbox=+mbox
set spoolfile=+inbox
set record=+sent
set postponed=+drafts
set mbox_type=Maildir

mailboxes +inbox +lovey-dovey +happy-kangaroos
```

#### Sending mails from Mutt

Now, startup `mutt`:

You should see all the mail in `~/mail/inbox`. Press `m` to compose mail; it will use the editor defined by your `EDITOR` environment variable. If this variable is not set, you can fix it before starting Mutt:

```
$ export EDITOR=your-favorite-editor
$ mutt

```

You should store the EDITOR value into your shell resource configuration file (such as [bashrc](/index.php/Bashrc "Bashrc")). You can also set the editor from Mutt's configuration file:

 `.muttrc`  `set editor=your-favorite-editor` 

For testing purposes, address the letter to yourself. After you have written the letter, save and exit the editor. You will return to Mutt, which will now show information about your e-mail. Press `y` to send it.

**Warning:** If at this point you press `q` by accident, Mutt will ask you `Postpone this message? ([yes]/no)`. This is really asking whether you want to save the message you just wrote. If you press "n" (perhaps because you want to edit the message again) the message will be permanently deleted. When using Mutt, always remember that "Postpone this message?" really means "Save this message?".

### Multiple accounts

Now you should have a working configuration for one account at least. You might wonder how to use several accounts, since we put everything into a single file.

Well all you need is to write account-specific parameters to their respective files and source them. All the IMAP/POP3/SMTP configuration for each account should go to its respective folder.

**Warning:** When one account is setting a variable that is not specified for other accounts, you **must unset** it for them, otherwise configuration will overlap and you will most certainly experience unexpected behaviour.

Mutt can handle this thanks to one of its most powerful features: hooks. Basically a hook is a command that gets executed before a specific action. There are several hooks available. For multiple accounts, you must use account-hooks *and* folder-hooks.

*   Folder-hooks will run a command before switching folders. This is mostly useful to set the appropriate SMTP parameters when you are in a specific folder. For instance when you are in your work mailbox and you send a e-mail, it will automatically use your work account as sender.
*   Account-hooks will run a command every time Mutt calls a function related to an account, like IMAP syncing. It does not require you to switch to any folder.

Hooks take two parameters:

```
account-hook [!]regex command
folder-hook [!]regex command

```

The regex is the folder to be matched (or not if preceded by the !). The command tells what to do.

Let us give a full example:

 `.muttrc` 
```
## General options
set header_cache = "~/.cache/mutt"
set imap_check_subscribed
set imap_keepalive = 300
unset imap_passive
set mail_check = 60
set mbox_type=Maildir

## ACCOUNT1
source "~/.mutt/work"
# Here we use the $folder variable that has just been set in the sourced file.
# We must set it right now otherwise the 'folder' variable will change in the next sourced file.
folder-hook $folder 'source ~/.mutt/work'

## ACCOUNT2
source "~/.mutt/personal"
folder-hook *user@gmail.com/ 'source ~/.mutt/personal'
folder-hook *user@gmail.com/Family 'set realname="Bob"'

```
 `.mutt/work` 
```
## Receive options.
set imap_user=user@gmail.com
set imap_pass=****
set folder = imaps://user@imap.gmail.com/
set spoolfile = +INBOX
set postponed = +Drafts
set record = +Sent

## Send options.
set smtp_url=smtps://user:****@smtp.gmail.com
set realname='User X'
set from=user@gmail.com
set hostname="gmail.com"
set signature="John Doe"
# Connection options
set ssl_force_tls = yes
unset ssl_starttls

## Hook -- IMPORTANT!
account-hook $folder "set imap_user=user@gmail.com imap_pass=****"

```

Finally `.mutt/personal` should be similar to `.mutt/work`.

Now all your accounts are set, start Mutt. To switch from one account to another, just change the folder (`c` key). Alternatively you can use the [sidebar](#Sidebar).

To change folder for different mailboxes you have to type the complete address -- for IMAP/POP3 folders, this may be quite inconvenient -- let us bind some key to it.

```
## Shortcuts
macro index,pager <f2> '<sync-mailbox><enter-command>source ~/.mutt/personal<enter><change-folder>!<enter>'
macro index,pager <f3> '<sync-mailbox><enter-command>source ~/.mutt/work<enter><change-folder>!<enter>'

```

With the above shortcuts (or with the sidebar) you will find that changing folders (with `c` by default) is not contextual, *i.e.* it will not list the folders of the current mailbox, but of the one used the last time you changed folders. To make the behaviour more contextual, the trick is to press *=* or *+* for current mailbox. You can automate this with the following macro:

```
macro index 'c' '<change-folder>?<change-dir><home>^K=<enter>'

```

### Passwords management

Keep in mind that writing your password in `.muttrc` is a security risk. One solution is to always enter the password manually, but this becomes cumbersome.

An alternative solution is to encrypt your password with [GnuPG](/index.php/GnuPG "GnuPG") in an encrypted file. [Setup your own keypair](/index.php/GnuPG#Create_a_key_pair "GnuPG") if you have not done so already. [Create](/index.php/Create "Create") a file in a [tmpfs](/index.php/Tmpfs "Tmpfs") with the following contents:

```
set my_pass = " *password*"

```

**Note:** Remember that user defined variables **must** start with `my_`.

Then [encrypt](/index.php/Encrypt "Encrypt") this file, setting yourself as the recipient and move it into an accessible location. In this example the encrypted file resides at $HOME/.my-pwds.gpg.

In your mutt configuration file add the following before any account:

```
source "gpg -dq $HOME/.my-pwds.gpg |"

```

**Note:** At the end of the line above, there is no space between the pipe and the double quote.

This decrypts the file quietly and sets the variable `my_pass` in this example. This can be used in any variable after it has been source. For example:

 `set imap_pass=$my_pass` 

If you use external tools like OfflineIMAP and msmtp, you need to set up an agent (e.g. gpg-agent, see [GnuPG#gpg-agent](/index.php/GnuPG#gpg-agent "GnuPG")) to keep the passphrase into cache and thus avoiding those tools always prompting for it.

#### Security concern

If `enter-command` is available from the UI, it is possible to see the password unencrypted, which may be undesired if anybody else than you has access to your session while Mutt is running. You may want to disable it for this reason. As a consequence, every command that the user intends to use must be bound to a key in advance, otherwise it will never be accessible.

 `.muttrc` 
```
 bind generic,alias,attach,browser,editor,index,compose,pager,pgp,postpone ':' noop

```

## Tips and tricks

Guides to get you started with using & customizing Mutt :

*   [My first Mutt](http://mutt.postle.net/) (maintained by Bruno Postle)
*   [The Woodnotes Guide to the Mutt Email Client](http://www.therandymon.com/woodnotes/mutt/using-mutt.html) (maintained by Randall Wood)
*   [The Homely Mutt](http://stevelosh.com/blog/2012/10/the-homely-mutt) (by Steve Losh)
*   [Everything You Need To Know To Start Using GnuPG with Mutt](http://codesorcery.net/old/mutt/mutt-gnupg-howto) (by Justin R. Miller)
*   [A List of useful programs that often are used in combination with neomutt](https://neomutt.org/contrib/useful-programs)

If you have any Mutt specific questions, feel free to ask in the [IRC channel](/index.php/IRC_channel "IRC channel").

### Key bindings

The default key bindings are quite far from the more common Emacs-like or Vi-like bindings. You can customize them to your preference. Mutt has a different set of bindings for the pager, the index, the attachment view, etc. Thus you need to specify which *map* you want to modify when you bind a key. You can review the list of commands and key bindings from Mutt's help page (default key: `?`). Example of Vi-like bindings:

 `muttrc` 
```
bind pager j next-line
bind pager k previous-line
bind attach,index,pager \CD next-page
bind attach,index,pager \CU previous-page
bind pager g top
bind pager G bottom
bind attach,index g first-entry
bind attach,index G last-entry

```

### Composition

#### Encrypt and sign mail (GnuPG)

To start encrypting mail in mutt using [GnuPG](/index.php/GnuPG "GnuPG") copy `/usr/share/doc/mutt/samples/gpg.rc` to your mutt configuration folder (e.g. to `~/.mutt/gpg.rc`). Then [append](/index.php/Append "Append") the following to your mutt configuration file (e.g. `~/.mutt/mutrrc`):

```
source ~/.mutt/gpg.rc

```

Most encryption options are then available by pressing `p` in the compose view.

See the `pgp_*` and `crypt_*` options in [muttrc(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/muttrc.5).

#### E-mail character encoding

When using Mutt there are two levels where the character sets that must be specified:

*   The text editor used to write the e-mail must save it in the desired encoding.
*   Mutt will then check the e-mail and determine which encoding is the more appropriate according to the priority you specified in the `send_charset` variable. Default: "us-ascii:iso-8859-1:utf-8".

So if you write an e-mail with characters allowed in ISO-8859-1 (like 'résumé'), but without characters specific to Unicode, then Mutt will set the encoding to ISO-8859-1.

To avoid this behaviour, set the variable in your `muttrc`:

```
set send_charset="us-ascii:utf-8"

```

or even

```
set send_charset="utf-8"

```

The first compatible charset starting from the left will be used. Since UTF-8 is a superset of US-ASCII it does not harm to leave it in front of UTF-8, it may ensure old MUA will not get confused when seeing the charset in the e-mail header.

#### Custom mail headers

One of the greatest thing in Mutt is that you can have full control over your mail header.

First, make your headers editable when you write e-mails:

```
set edit_headers=yes

```

Mutt also features a special function `my_hdr` for customizing your header. Yes, it is named just like a variable, but in fact it is a function.

You can clear it completely, which you *should* do when switching accounts with different headers, otherwise they will overlap:

```
unmy_hdr *

```

Other variables have also an impact on the headers, so it is wise to clear them before using `my_hdr`:

```
unset use_from
unset use_domain
unset user_agent

```

Now, you can add any field you want -- even non-standard one -- to your header using the following syntax:

```
my_hdr <FIELD>: <VALUE>

```

Note that <VALUE> can be the result of a command.

Example:

```
## Extra info.
my_hdr X-Info: Keep It Simple, Stupid.

## OS Info.
my_hdr X-Operating-System: `uname -s`, kernel `uname -r`

## This header only appears to MS Outlook users
my_hdr X-Message-Flag: WARNING!! Outlook sucks

## Custom Mail-User-Agent ID.
my_hdr User-Agent: Every email client sucks, this one just sucks less.

```

#### Signature block

Create a .signature in your home directory. Your signature will be appended at the end of your email. Alternatively you can specify a file in your Mutt configuration:

```
set signature="path/to/sig/file"

```

##### Random signature

You can use *fortune* (package [fortune-mod](https://www.archlinux.org/packages/?name=fortune-mod)) to add a random signature to Mutt.

Create a fortune file and then add the following line to your .muttrc:

 `set signature="fortune pathtofortunefile|"` 

Note the pipe at the end. It tells Mutt that the specified string is not a file, but a command.

#### Compose and send from command line

Man pages will show all available commands and how to use them, but here are a couple of examples. You could use Mutt to send alerts, logs or some other system information, triggered by login through `.bash_profile`, or as a regular [cron](/index.php/Cron "Cron") job.

Send a message:

```
mutt -s "Subject" somejoeorjane@someserver.com < /var/log/somelog

```

Send a message with attachment:

```
mutt -s "Subject" somejoeorjane@someserver.com -a somefile < /tmp/sometext.txt

```

#### Compose HTML e-mails

Since Mutt has nothing of a WYSIWIG client, HTML is quite straightforward, and you can do much more than with all WYSIWIG mail clients around since you edit the source code directly. Simply write your mail using HTML syntax. For example:

```
This is normal text<br>
<b>This is bold text</b>

```

Now before sending the mail, use the `edit-type` command (default shortcut `Ctrl+t`), and replace `text/plain` by `text/html`.

**Note:** HTML e-mails are regarded by many people as useless, cumbersome, and subject to reading issues. Mutt can read HTML mails with a text browser like w3m or lynx, but it has clearly no advantage over a plain-text e-mail. You should avoid writing HTML e-mails when possible.

#### Display another email while composing

A common complaint with Mutt is that when composing a new mail (or reply), you cannot open another mail (i.e. for checking with another correspondent) without closing the current mail (postponing). The following describes a solution:

First, fire up Mutt as usual. Then, launch another terminal window. Now start a new Mutt with

```
mutt -R

```

This starts Mutt in read-only mode, and you can browse other emails at your convenience. It is strongly recommended to always launch a second Mutt in read-only mode, as conflicts will easily arise otherwise.

**Note:** When changing folders (with `c` or `y`) the read-only mode is not preserved. Instead `Esc c` has to be used.

**Tip:** This solution calls for a bit of typing, so it is suitable to bind the following command to a [keyboard shortcut](/index.php/Keyboard_shortcut "Keyboard shortcut"):
```
$TERMINAL -e mutt -R

```
where `$TERMINAL` is your terminal.

### Printing

You can install [muttprint](https://aur.archlinux.org/packages/muttprint/) for fancier printing quality. In your muttrc file, insert:

```
set print_command="/usr/bin/muttprint %s -p {PrinterName}"

```

### Viewing content

#### Viewing URLs in a web browser

Your should start by creating a .mutt directory in $HOME if not done yet. There, create a file named macros. Insert the following:

```
 macro pager \cb <pipe-entry>'urlview'<enter> 'Follow links with urlview'

```

Then install the [urlview](https://aur.archlinux.org/packages/urlview/) package.

Create a .urlview in $HOME and insert the following:

```
REGEXP (((http|https|ftp|gopher)|mailto)[.:][^ >"\t]*|www\.[-a-z0-9.]+)[^ .,;\t>">\):]
COMMAND <your-browser> %s

```

When you read an email on the pager, hitting ctrl+b will list all the urls from the email. Navigate up or down with arrow keys and hit enter on the desired url. Your browser will start and go to the selected site.

Some browser will require additional arguments to work properly. For example, [Luakit](/index.php/Luakit "Luakit") will close on Mutt exit. You need to fork it to background, using the `-n` parameter:

```
COMMAND luakit -n %s 2>/dev/null

```

The `2>/dev/null` is to make it quiet, i.e. to prevent useless message printing where you do not want them to.

**Note:** urlview has a few deficiencies (e.g. the inability to handle certain email encodings) and is fairly feature-bare (e.g. it does not provide context for links it finds). There are a couple alternatives that do better. One, which can handle all email encodings and provides link context, is [extract_url.pl](http://www.memoryhole.net/~kyle/extract_url/). Another, which can also provide link context but cannot handle all email encodings, is [urlscan-git](https://aur.archlinux.org/packages/urlscan-git/). Both are drop-in replacements for urlview, though extract_url has features which benefit from additional configuration changes.

#### Viewing HTML

It is possible to pass the html body to an external HTML program and then dump it, keeping email viewing uniform and unobtrusive. Three programs are described here: [lynx](https://www.archlinux.org/packages/?name=lynx), [w3m](https://www.archlinux.org/packages/?name=w3m) and [elinks](https://www.archlinux.org/packages/?name=elinks) (make sure the selected package is [installed](/index.php/Pacman "Pacman")).

If `~/.mutt/mailcap` does not exist you will need to create it and save the following to it.

```
text/html; lynx -assume_charset=%{charset} -display_charset=utf-8 -dump %s; nametemplate=%s.html; copiousoutput

```

or, in case of w3m,

```
text/html; w3m -I %{charset} -T text/html; copiousoutput;

```

or, in case of elinks,

```
text/html; elinks -dump ; copiousoutput;

```

Edit `~/.muttrc` and add the following,

```
set mailcap_path 	= ~/.mutt/mailcap

```

To automatically open HTML messages in lynx, w3m or elinks add this additional line to the muttrc:

```
auto_view text/html

```

The beauty of this is, instead of seeing an html body as source or being opened by a separate program, in this case lynx, you see the formatted content directly, and any url links within the email can be displayed with `Ctrl+b`, assuming you have [urlview](https://aur.archlinux.org/packages/urlview/) installed.

If you receive many emails with multiple or alternate encodings Mutt may default to treating every email as html. To avoid this, add the following variable to your ~/.muttrc to have Mutt default to text when available and use w3m/lynx only when no text version is availble in the email:

```
alternative_order text/plain text/html

```

Some HTML mails may not display correctly in a text-based web browser. As a fallback solution, you can bind a key to open a graphical browser in such cases. The following macro will open the HTML mail selected from the attachment view in the web browser defined in the environment. (Feel free to adapt the `~/.cache/mutt/` folder).

```
macro attach 'V' "<pipe-entry>cat >~/.cache/mutt/mail.html && $BROWSER ~/.cache/mutt/mail.html && rm ~/.cache/mutt/mail.html<enter>"

```

#### Filtering the message view

You can restrict the view to e-mails matching a pattern and specific properties with the `limit` command (default shortcut: `l`).

To view all e-mails containing "foo" in the header, simply write "foo" and you are done. To remove the filter, use the "all" keyword.

To view all flagged messages, use

```
~F

```

To view all unread messages that are either of size ≥1MB or from johndoe, use

```
~U (~z 1M- | ~f johndoe)

```

All possible patterns are listed in the [official manual](http://www.mutt.org/doc/manual/#patterns).

#### Conversation grouping

The default sort order is by date. Use the `sort-mailbox` command (default key: `o`) to change the sorting option. You can group e-mails by conversation/thread, in which case you can define how to sort threads and how to sort within a thread.

In the following example, threads are sorted according to the date of their last e-mail.

 `muttrc` 
```
set sort=threads
set sort_aux=last-date-received

```

### Configuring editors to work with mutt

#### vim

*   To limit the width of text to 72 characters, edit your .[vimrc](/index.php/Vim "Vim") file and add:

```
au BufRead /tmp/mutt-* set tw=72

```

*   Another choice is to use Vim's mail filetype plugin to enable other mail-centric options besides 72 character width. Edit `~/.vim/filetype.vim`, creating it if unpresent, and add:

```
augroup filetypedetect
  " Mail
  autocmd BufRead,BufNewFile *mutt-*              setfiletype mail
augroup END

```

*   To set a different tmp directory, e.g. ~/.tmp, add a line to your muttrc as follows:

```
set tmpdir="~/.tmp"

```

*   To reformat a modified text see the Vim context help

```
:h 10.7

```

#### GNU nano

[nano](/index.php/Nano "Nano") is another nice console editor to use with Mutt.

To limit the width of text to 72 characters, edit your .nanorc file and add:

```
 set fill 72

```

If you do not want to limit the width of text globally, you can pass the column number as an argument to the hard-wrap option in your muttrc file, e.g.:

```
 set editor="nano -r 72"

```

Also, in muttrc file, you can specify the line to start editing so that you will skip the mail header:

```
 set editor="nano +7"

```

#### Emacs

Emacs has a *mail* and a *message* major mode. To switch to mail-mode automatically when Emacs is called from Mutt, you can add the following to your `.emacs`:

 `.emacs` 
```
;; Mutt support.
(setq auto-mode-alist (append '(("/tmp/mutt.*" . mail-mode)) auto-mode-alist))

```

If you usually run Emacs daemon, you may want Mutt to connect to it. Add this to your `.muttrc`:

 `.muttrc` 
```
set editor="emacsclient -a \"\" -t"

```

### Display settings

#### Colors

[Append](/index.php/Append "Append") the contents of `/usr/share/doc/mutt/samples/colors.linux` to your .muttrc file, or copy and source it. Then adjust to your liking.

The actual color each of these settings will produce depends on the colors set in your [~/.Xresources](/index.php/Xresources "Xresources") file.

Alternatively, you can source any file you want containing colors (and thus act as a theme file). See [[1]](http://nongeekshandbook.blogspot.be/2009/03/mutt-color-configuration.html) for a theme example.

#### Index Format

Here follows a quick example to put in your `.muttrc` to customize the Index Format, i.e. the columns displayed in the folder view.

```
set date_format="%y-%m-%d %T"
set index_format="%2C | %Z [%d] %-30.30F (%-4.4c) %s"

```

See the [Mutt Reference](http://www.mutt.org/doc/manual/#index-format), [strftime(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/strftime.3) and [printf(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/printf.3) for more details.

#### Display recipient instead of sender in "Sent" folder view

By default Mutt uses the `%L` format string in the `index_format` variable, which will display:

*   "To <list-name>", if an address in the "To:" or "Cc:" header field matches an address defined by the user's `subscribe` command.
*   Otherwise it displays the author name, or recipient name if the message is from you.

If you use multiple email addresses in the same mailbox, make sure to configure the [alternates variable](https://dev.mutt.org/trac/wiki/UseCases/MultiAccounts#Settinguptheaddresses:alternates), so that Mutt knows which messages were from you.

#### Variable column width

If you resize the window, the subject might get truncated while there is still unused space left for some fields, like for the sender. You can get the maximum number of columns supported by your terminal (i.e. the width) using a shell call to `tput cols`. With this value, you can set a percentage of the width to fields like Sender and Subject.

Example using the above folder-hook and a sidebar width of 24:

 `muttrc` 
```
## From field gets 30% of remaining space, Subject gets 70%.
## Remaining space is the total width minus the other fields (35), minus the sidebar (24)
set my_index_format_pre='set my_col_from = `echo $((30 * ($(tput cols)-35-24) / 100))`; set my_col_subject = `echo $((70 * ($(tput cols)-35-24) / 100))`; set index_format="%2C | %Z [%d] %-$my_col_from.${my_col_from}'
set my_index_format_post=' (%-4.4c) %?M?<%M> ?%-$my_col_subject.${my_col_subject}s"'

folder-hook .*[sS]ent.* "$my_index_format_pre"t"$my_index_format_post"
folder-hook ! .*[sS]ent.* "$my_index_format_pre"F"$my_index_format_post"

```

We *must* set the variables `my_col_from` and `my_col_from` from within the hooks. Otherwise, the column values will not get re-computed.

We can add a binding to force re-computing the index format without changing folder:

 `muttrc` 
```
macro index,pager \CL "<enter-command>$my_index_format_pre"F"$my_index_format_post<enter><redraw-screen>"

```

#### Sidebar

Example settings for a sidebar are in `/usr/share/doc/mutt/samples/sample.muttrc-sidebar`, including keybindings. Copy, edit, and source that file in your mutt configuration file. Be sure to change `set sidebar_visible = yes`.

[Append](/index.php/Append "Append") the following in order to toggle the sidebar visibility:

```
bind index,pager B sidebar-toggle-visible

```

**Note:** You *must* set the `mailboxes` variables or the `imap_check_subscribed` to tell the sidebar which folder should be displayed. See the [mailboxes](#mailboxes) section.

Note that with the `mailboxes` option, folders appear in the order they were set to `mailboxes` if you do not use the `sidebar_sort_method` option.

**Tip:** To add a separator between different mailboxes, add a fake folder to the list of folders For example add: mailboxes "+-- My mailbox -----------"

#### Display the index above the pager view

Set the following variable in your `muttrc`:

```
set pager_index_lines=10

```

### Contact management

#### Address aliases

*Aliases* is the way Mutt manages contacts. An alias is **nickname [longname] <address>**.

*   The **nickname** is what you will type in Mutt to get your contact address. One word only, and should be easy to remember.
*   The **longname** is optional. It may be several words.
*   An **<address>** must be in a valid form (i.e. with an `@`).

It is quite simple indeed. Add this to `.muttrc`:

```
set alias_file = "~/.mutt/aliases"
set sort_alias = alias
set reverse_alias = yes
source $alias_file
```

Explanation:

*   `alias_file` is the file where the information is getting stored when you add an alias from within Mutt.
*   `sort_alias` specifies which field to use to sort the alias list when displayed in Mutt. Possible values: alias, address.
*   `reverse_alias` if set to yes mutt will display the "personal" name from your aliases in the index menu if it finds an alias that matches the message's sender.
*   `source $alias_file` tells Mutt to read aliases on startup. Needed for auto-completion.

Now all you have to do when prompted `To:` is writing the alias instead of the full address. The beauty of it is that you can auto-complete the alias using `Tab`. Autocompleting a wrong or an empty string will display the full list. You can select the alias as usual, or by typing its index number.

There are two ways to create aliases:

*   From Mutt, press `a` when an e-mail of the targetted person if selected.
*   Edit the alias_file manually. The syntax is really simple:

```
alias nickname Long Name <my-friend@domain.tld>

```

#### Abook

[abook](https://www.archlinux.org/packages/?name=abook) is a stand-alone program dedicated to contact management. It uses a very simple text-based interface and contacts are stored in a plain text, human-readable database. Besides the desired contact properties are extensible (birthday, address, fax, and so on).

Abook is specifically designed to be interfaced with Mutt, so that it can serve as a full, more featured replacement of Mutt internal aliases. If you want to use Abook instead of aliases, remove the aliases configuration in `.muttrc` and add this:

 `muttrc` 
```
## Abook
set query_command= "abook --mutt-query '%s'"
macro index,pager  a "<pipe-message>abook --add-email-quiet<return>" "Add this sender to Abook"
bind editor        <Tab> complete-query

```

See the man pages `abook` and `abookrc` for more details and a full configuration sample.

#### Goobook

Goobook allows you to search your Google contacts from the command line or from within Mutt and can be installed with the [goobook-git](https://aur.archlinux.org/packages/goobook-git/) package.

Before using goobook you must configure `~/.goobookrc`. To generate the default template:

```
$ goobook config-template > ~/.goobookrc

```

See `~/.goobookrc` for configuration options. At a minimum, you will need to enter your **email** and **password**.

**Note:** If you have two-step verification enabled with the Google account, you may need to generate an application password.

If you want to use Goobook instead of aliases, remove any alias configuration in `.muttrc` and add:

 `muttrc` 
```
## GooBook
set query_command="goobook query '%s'"
macro index,pager a "<pipe-message>goobook add<return>" "add sender to google contacts"
bind editor <Tab> complete-query

```

When composing an email message within mutt, `Tab` will now search your Google contacts. While viewing messages `a` will add the sender to Google contacts.

#### Khard

[khard](https://www.archlinux.org/packages/?name=khard) is a command-line addressbook that is able to sync with CardDAV-servers.

### Manage multiple sender accounts

If you use multiple sender accounts, you can automatically associate a specific sender account with a recipient. [mutt-vid](https://aur.archlinux.org/packages/mutt-vid/) scans sent emails for the most recent "From" details associated with specific recipients, saving these in a file for mutt to source. The next time you email this recipient, mutt will automatically invoke a send-hook with the same email address and real name that you used previously. See mutt-vid's [homepage](https://gitlab.com/protist/mutt-vid) for more details.

### Request IMAP mail retrieval manually

If you do not want to wait for the next automatic IMAP fetching (or if you did not enable it), you might want to fetch mails manually. There is a mutt command `imap-fetch-mail` for that. Alternatively, you could bind it to a key:

```
bind index "^" imap-fetch-mail

```

### Avoiding slow index on large (IMAP) folders due to coloring

Index highlighting by regex is nice, but can lead to slow folder viewing if your regex checks the body of the message.

Use folder-hook for only highlighting in for example the inbox (if you manage to empty your mailbox effiently):

```
folder-hook . 'uncolor index "~b \"Hi Joe\" ~R !~T !~F !~p !~P"'
folder-hook ""!"" 'color index brightyellow black "~b \"Hi Joe\" ~N !~T !~F !~p !~P"'

```

### Speed up folders switch

Add this to your `.muttrc`:

 `set sleep_time = 0` 

### Archive treated e-mails

When you read an e-mail, you have four choices: Answer it, Flag it, Archive it or Delete it. If you have this in mind, you can keep your inbox slim and fit with this macro (set up for Gmail):

```
macro index \' "<tag-pattern>~R !~D !~F<enter>\
<tag-prefix><save-message>+[Gmail]/All <enter>" \
"Archive"

```

### Migrating mails from one computer to another

In case you are transfering your mails to a new machine (copy&paste), you probably need to delete the header cache (a file or folder like `~/.cache/mutt` if you followed the above configuration) to make Mutt able to read your migrated E-Mails. Otherwise Mutt may freeze.

Note that if you had a folder created for you header cache, all mailboxes will have their own cache file, so you can delete caches individually without having to remove everything.

### Default folder for saving attachments

By default Mutt will save attachments to the folder it was started from. If you want to always set the default destination to `~/attachments`, you can create the following alias, which launches Mutt in this folder:

```
alias mutt='cd ~/attachments && mutt'

```

### Pager behavior

Show context lines when going to next page:

```
set pager_context=3

```

Stop at the end instead of displaying next mail:

```
set pager_stop=yes

```

### Fast reply

By default Mutt will ask to confirm the recipient and the subject when you reply to an e-mail. It will also ask if you want to include the original mail in your answer. If you assume you will always stick to the default values, you can set up Mutt to skip these questions:

 `muttrc` 
```
set fast_reply=yes
set include=yes

```

You can still edit the recipient and the subject before sending.

### Ignore own e-mail addresses from group-reply

Mutt will include your e-mail address(es) in the recipient list when you group-reply to a mail you were CC'ed. You can ask Mutt to ignore some addresses with:

```
alternates mail1@server1|mail2@server2|...

```

### IMAP message cache

When using the built-in IMAP support, e-mails are fetched in memory by default. Retrieving a big e-mail several times will download it from your IMAP server that many times.

Alternatively, you can ask Mutt to store all fetched messages on disk:

 `muttrc` 
```
set message_cachedir=~/.cache/mutt/messages

```

(The folder must exist.) This will make any future retrieval instantaneous, even with big attachments.

If you want to purge the cache from its oldest e-mails exceeding a limit of, say, 50MB, you can use a script like the following:

 `~/.mutt/purgecache.sh` 
```
#!/bin/sh

## In KB.
CACHE_LIMIT=51200

cd "$1" 2>/dev/null
[ $? -ne 0 ] && exit

[ $(du -s . | cut -f1 -d'	') -lt $CACHE_LIMIT ] && exit
while IFS= read -r i; do
	rm "$i"
	[ $(du -s . | cut -f1 -d'	') -lt $CACHE_LIMIT ] && exit
done <<EOF
$(find . -type f -exec ls -rt1 {} +)
EOF

```

and call it on startup:

 `muttrc` 
```
set message_cachedir=~/.cache/mutt/messages
source "~/.mutt/purgecache.sh '$message_cachedir'|"

```

## Troubleshooting

### Backspace does not work in Mutt

This is a common problem with some xterm-like terminals. Two solutions:

*   Either rebind the key in `.muttrc`

```
bind index,pager ^? previous-line

```

Note that `^?` is one single character representing backspace in [caret notation](https://en.wikipedia.org/wiki/Caret_notation "wikipedia:Caret notation"). To type in Emacs, use `Ctrl+q Backspace`, in Vim `Ctrl+v Backspace`.

*   Or fix your terminal:

```
$ infocmp > termbs.src

```

Edit `termbs.src` and change `kbs=^H` to `kbs=\177`, then:

```
$ tic -x termbs.src

```

### The *change-folder* function always prompt for the same mailbox

This is not a bug, this is actually an intended behaviour. See the [multiple accounts section](#Multiple_accounts) for a workaround.

### I cannot change folder when using Mutt read-only (Mutt -R)

This is certainly because you are using macros like this one:

```
macro index,pager <f2> '<sync-mailbox><enter-command>source ~/.mutt/personal<enter><change-folder>!<enter>'

```

This macro tells Mutt to sync (which is a write operation) before switching.

Either use the [sidebar](#Sidebar) or set another macro:

```
macro index,pager <f3> '<enter-command>source ~/.mutt/personal<enter><change-folder>!<enter>'

```

### Error sending message, child exited 127 (Exec error.).

This is an SMTP error. It means that mutt does not know how to send the message. You can either try installing sendmail and see if that solves your issue, or you can set the smtp_url variable. If you use gmail, you can add the following to your muttrc to tell mutt to use gmails smtp server.

```
set smtp_url=smtps://$imap_user:$imap_pass@smtp.gmail.com

```

Take note of the smtps protocol, it is important. This should solve the problem.

### Character encoding problems

If you are having problems with character encoding, first read [this section](http://dev.mutt.org/trac/wiki/MuttFaq/Charset) in the Mutt wiki.

If Chinese text is still garbled, it may help to decode with GBK even when GB2312 is specified in the header. You can do this with `iconv` by adding the following to your `mailcap` file:

```
text/plain; iconv -f gbk -t utf-8 %s; test=echo "%{charset}" | grep -ic "gb2312"; copiousoutput;

```

and enabling it by adding a line to your `.muttrc`:

```
auto_view text/plain

```

For HTML emails, you can edit the relevant line of your mailcap by replacing `%{charset}` with `$(echo %{charset} | sed s/gb2312/gbk/I)`, for example:

```
text/html; w3m -dump -I $(echo %{charset} | sed s/gb2312/gbk/I) %s; nametemplate=%s.html; copiousoutput

```

### Unable to login with GMail

Gmail disables access from apps it considers less secure, including `mutt`. You can enable access by following the instructions [here](https://support.google.com/accounts/answer/6010255)

### Not possible to open too long URLs with urlview

Too long URLs are not parsed correctly, because urlview does not decode text (see [[2]](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=127090)). You can let mutt decode the e-mails instead. Replace the line for opening urlview with the following code:

```
macro index \cb "\
:set my_tmp_pipe_decode=\$pipe_decode
\
:set pipe_decode
\
|urlview
\
:set pipe_decode=\$my_tmp_pipe_decode
\
:unset my_tmp_pipe_decode
" \
'call urlview to extract URLs out of a message'

```

## Documentation

Newcomers may find it quite hard to find help for Mutt. Actually most of the topics are covered in the official documentation. We urge you to read it.

*   [The official manual](http://www.mutt.org/doc/manual/). The stock [mutt](https://www.archlinux.org/packages/?name=mutt) package for Arch Linux also installs the HTML and plain text manual at `/usr/share/doc/mutt/`.
*   The `mutt` and `muttrc` man pages.

## See also

*   [The official Mutt website](http://www.mutt.org/)
*   [Official Manual](http://www.mutt.org/doc/manual/)
*   [The Mutt wiki](https://gitlab.com/muttmua/mutt/wikis/home/)
*   [Brisbin's great guide on how to setup different IMAP accounts with Mutt, offlineimap, msmtp](http://pbrisbin.com/posts/two_accounts_in_mutt/)
*   [A Quick Guide to Mutt](http://srobb.net/mutt.html)
*   [Steve Losh on Mutt, offlineimap, msmtp, notmuch (focused on Gmail)](http://stevelosh.com/blog/2012/10/the-homely-mutt/)
*   [muttrc builder](http://www.muttrcbuilder.org/)