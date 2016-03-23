**Mutt** is a text-based mail client renowned for its powerful features. Though over 2 decades old, Mutt remains the mail client of choice for a great number of power-users. Unfortunately, a default Mutt install is plagued by complex keybindings along with a daunting amount of documentation. This guide will help the average user get Mutt up and running, and begin customizing it to their particular needs.

## Contents

*   [1 Overview](#Overview)
*   [2 Installing](#Installing)
*   [3 Configuring](#Configuring)
    *   [3.1 IMAP](#IMAP)
        *   [3.1.1 Native IMAP support](#Native_IMAP_support)
            *   [3.1.1.1 imap_user](#imap_user)
            *   [3.1.1.2 imap_pass](#imap_pass)
            *   [3.1.1.3 folder](#folder)
            *   [3.1.1.4 spoolfile](#spoolfile)
            *   [3.1.1.5 mailboxes](#mailboxes)
            *   [3.1.1.6 Summary](#Summary)
        *   [3.1.2 External IMAP support](#External_IMAP_support)
    *   [3.2 POP3](#POP3)
    *   [3.3 Maildir](#Maildir)
    *   [3.4 SMTP](#SMTP)
        *   [3.4.1 Folders](#Folders)
        *   [3.4.2 Native SMTP support](#Native_SMTP_support)
        *   [3.4.3 External SMTP support](#External_SMTP_support)
        *   [3.4.4 Sending mails from Mutt](#Sending_mails_from_Mutt)
    *   [3.5 Multiple accounts](#Multiple_accounts)
    *   [3.6 Passwords management](#Passwords_management)
        *   [3.6.1 Security concern](#Security_concern)
*   [4 Advanced features](#Advanced_features)
    *   [4.1 Key bindings](#Key_bindings)
    *   [4.2 E-mail character encoding](#E-mail_character_encoding)
    *   [4.3 Printing](#Printing)
    *   [4.4 Custom mail headers](#Custom_mail_headers)
    *   [4.5 Signature block](#Signature_block)
        *   [4.5.1 Random signature](#Random_signature)
    *   [4.6 Viewing URLs & opening your favorite web browser](#Viewing_URLs_.26_opening_your_favorite_web_browser)
    *   [4.7 Viewing HTML](#Viewing_HTML)
    *   [4.8 Mutt and Vim](#Mutt_and_Vim)
    *   [4.9 Mutt and GNU nano](#Mutt_and_GNU_nano)
    *   [4.10 Mutt and Emacs](#Mutt_and_Emacs)
    *   [4.11 Colors](#Colors)
    *   [4.12 Index Format](#Index_Format)
        *   [4.12.1 Display recipient instead of sender in "Sent" folder view](#Display_recipient_instead_of_sender_in_.22Sent.22_folder_view)
        *   [4.12.2 Variable column width](#Variable_column_width)
    *   [4.13 Contact management](#Contact_management)
        *   [4.13.1 Address aliases](#Address_aliases)
        *   [4.13.2 Abook](#Abook)
        *   [4.13.3 Goobook](#Goobook)
    *   [4.14 Manage multiple sender accounts](#Manage_multiple_sender_accounts)
    *   [4.15 Request IMAP mail retrieval manually](#Request_IMAP_mail_retrieval_manually)
    *   [4.16 Avoiding slow index on large (IMAP) folders due to coloring](#Avoiding_slow_index_on_large_.28IMAP.29_folders_due_to_coloring)
    *   [4.17 Speed up folders switch](#Speed_up_folders_switch)
    *   [4.18 Use Mutt to send mail from command line](#Use_Mutt_to_send_mail_from_command_line)
    *   [4.19 Composing HTML e-mails](#Composing_HTML_e-mails)
    *   [4.20 How to display another email while composing](#How_to_display_another_email_while_composing)
    *   [4.21 Archive treated e-mails](#Archive_treated_e-mails)
    *   [4.22 Mutt-Sidebar](#Mutt-Sidebar)
    *   [4.23 Migrating mails from one computer to another](#Migrating_mails_from_one_computer_to_another)
    *   [4.24 Filtering the message view](#Filtering_the_message_view)
    *   [4.25 Display the index above the pager view](#Display_the_index_above_the_pager_view)
    *   [4.26 Default folder for saving attachments](#Default_folder_for_saving_attachments)
    *   [4.27 PGP signed/encrypted mail](#PGP_signed.2Fencrypted_mail)
    *   [4.28 Pager behavior](#Pager_behavior)
    *   [4.29 Fast reply](#Fast_reply)
    *   [4.30 Ignore own e-mail addresses from group-reply](#Ignore_own_e-mail_addresses_from_group-reply)
    *   [4.31 Conversation grouping](#Conversation_grouping)
    *   [4.32 IMAP message cache](#IMAP_message_cache)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Backspace does not work in Mutt](#Backspace_does_not_work_in_Mutt)
    *   [5.2 The *change-folder* function always prompt for the same mailbox](#The_change-folder_function_always_prompt_for_the_same_mailbox)
    *   [5.3 I cannot change folder when using Mutt read-only (Mutt -R)](#I_cannot_change_folder_when_using_Mutt_read-only_.28Mutt_-R.29)
    *   [5.4 Error sending message, child exited 127 (Exec error.).](#Error_sending_message.2C_child_exited_127_.28Exec_error..29.)
    *   [5.5 Character encoding problems](#Character_encoding_problems)
*   [6 Documentation](#Documentation)
*   [7 See also](#See_also)

## Overview

Mutt focuses primarily on being a Mail User Agent (MUA), and was originally written to view mail. Later implementations (added for retrieval, sending, and filtering mail) are simplistic compared to other mail applications and, as such, users may wish to use external applications to extend Mutt's capabilities.

Nevertheless, the Arch Linux [mutt](https://www.archlinux.org/packages/?name=mutt) package is compiled with IMAP, POP3 and SMTP support, removing the necessity for external applications.

This article covers using both native IMAP sending and retrieval, and a setup depending on [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP") or [getmail](/index.php/Getmail "Getmail") (POP3) to retrieve mail, [procmail](/index.php/Procmail "Procmail") to filter it in the case of POP3, and [msmtp](/index.php/Msmtp "Msmtp") to send it.

## Installing

[Install](/index.php/Install "Install") the [mutt](https://www.archlinux.org/packages/?name=mutt) package.

Optionally install external helper applications for an IMAP setup, such as [isync](/index.php/Isync "Isync"), [OfflineIMAP](/index.php/OfflineIMAP "OfflineIMAP"), or [msmtp](/index.php/Msmtp "Msmtp").

Or (if using POP3) [getmail](https://www.archlinux.org/packages/?name=getmail), [fetchmail](https://www.archlinux.org/packages/?name=fetchmail) or [fdm](https://www.archlinux.org/packages/?name=fdm) and [procmail](https://www.archlinux.org/packages/?name=procmail).

**Note:**

*   If you just need the authentication methods LOGIN and PLAIN, these are satisfied with the dependency [libsasl](https://www.archlinux.org/packages/?name=libsasl)
*   If you want to (or have to) use CRAM-MD5, GSSAPI or DIGEST-MD5, install the package [cyrus-sasl-gssapi](https://www.archlinux.org/packages/?name=cyrus-sasl-gssapi)
*   If you are using Gmail as your SMTP server, you may need to install the package [cyrus-sasl](https://www.archlinux.org/packages/?name=cyrus-sasl)

## Configuring

This section covers [#IMAP](#IMAP), [#POP3](#POP3), [#Maildir](#Maildir) and [#SMTP](#SMTP) configuration.

Note that Mutt will recognize by default two locations for its configuration file; `~/.muttrc` and `~/.mutt/muttrc`. Either location will work. In case you decide to put the initialization file somewhere else, use `$ mutt -F /path/to/.muttrc`. You should also know some prerequisite for Mutt configuration. Its syntax is very close to the Bourne Shell. For example, you can get the content of another config file:

```
source /path/to/other/config/file

```

You can use variables and assign the result of shell commands to them.

```
set editor=`echo \$EDITOR`

```

Here the `$` gets escaped so that it does not get substituted by Mutt before being passed to the shell. Also note the use of the backquotes, as bash syntax `$(...)` does not work. Mutt has a lot of predefined variables, but you can also set your own. User variable **must begin with "my"!**

```
set my_name = "John Doe"

```

### IMAP

#### Native IMAP support

The [mutt](https://www.archlinux.org/packages/?name=mutt) package is compiled with IMAP support. At the very least you need to have 4 lines in your muttrc file to be able to access your mail.

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

The spoolfile is the folder where your (unfiltered) e-mail arrives. Most e-mail services conventionally names it *INBOX*. You can now use '=' or '+' as a substitution for the full `folder` path that was configured above. For example:

```
set spoolfile=+INBOX

```

##### mailboxes

Any imap folders that should be checked regularly for new mail should be listed here:

```
mailboxes =INBOX =family
mailboxes imaps://imap.gmail.com/INBOX imaps://imap.gmail.com/family

```

Alternatively, check for all subscribed IMAP folders (as if all were added with a `mailboxes` line):

```
set imap_check_subscribed

```

These two versions are equivalent if you want to subscribe to all folders. So the second method is much more convenient, but the first one gives you more flexibility. Also, newer Mutt versions are configured by default to include a macro bound to the 'y' key which will allow you to change to any of the folders listed under mailboxes.

If you do not set this variable, the *spoolfile* will be used by default. This variable is also important for the [sidebar](#Mutt-Sidebar).

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

# Allow Mutt to open new imap connection automatically.
unset imap_passive

# Keep IMAP connection alive by polling intermittently (time in seconds).
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
set folder=$HOME/mail
set spoolfile=+/
set header_cache=~/.cache/mutt
```

This is a minimal Configuration that enables you to access your Maildir and checks for new local Mails in INBOX. This configuration also caches the headers of the eMails to speed up directory-listings. It might not be enabled in your build (but it sure is in the Arch-Package). Note that this does not affect OfflineIMAP in any way. It always syncs the all directories on a Server. `spoolfile` tells Mutt which local directories to poll for new Mail. You might want to add more Spoolfiles (for example the Directories of Mailing-Lists) and maybe other things. But this is subject to the Mutt manual and beyond the scope of this document.

### SMTP

Whether you use POP or IMAP to receive mail you will probably still send mail using SMTP.

#### Folders

There is basically only one important folder here: the one where all your sent e-mails will be saved.

```
set record = +Sent

```

Gmail saves automatically sent e-mail to `+[Gmail]/Sent`, so we do not want duplicates.

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

See `man 5 muttrc` for more information.

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

Well all you need is to write account-specific parameters to their respective files and source them. All the IMAP/POP3/SMTP config for each account should go to its respective folder.

**Warning:** When one account is setting a variable that is not specified for other accounts, you **must unset** it for them, otherwise configuration will overlap and you will most certainly experience unexpected behaviour.

Mutt can handle this thanks to one of its most powerful features: hooks. Basically a hook is a command that gets executed before a specific action. There are several hooks available. For multiple accounts, you must use account-hooks *and* folder-hooks.

*   Folder-hooks will run a command before switching folders. This is mostly useful to set the appropriate SMTP parameters when you are in a specific folder. For instance when you are in your work mailbox and you send a e-mail, it will automatically use your work account as sender.
*   Account-hooks will run a command everytime Mutt calls a function related to an account, like IMAP syncing. It does not require you to switch to any folder.

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

Now all your accounts are set, start Mutt. To switch from one account to another, just change the folder (`c` key). Alternatively you can use the [sidebar](#Mutt-Sidebar).

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

Keep in mind that writing your password in `.muttrc` is a security risk, and it might be of your concern. The trivial way to keep your passwords safe is not writing them in the config file. Mutt will then prompt for it when needed. However, this is quite cumbersome in the long run, especiallly if you have several accounts.

Here follows a smart and convenient solution: all your passwords are encrypted into one file and Mutt will prompt for a passphrase on startup only. You can opt for a keyring tool (e.g. GPG, [pwsafe](https://www.archlinux.org/packages/?name=pwsafe)) or an encryption tool like [ccrypt](https://www.archlinux.org/packages/?name=ccrypt), which may be more simple and straightforward to use. Since GPG is a Mutt dependency, we will use it here.

First create a pair of public/private keys:

```
gpg --gen-key

```

If you do not understand this process have a look at [Wikipedia:Asymmetric cryptography](https://en.wikipedia.org/wiki/Asymmetric_cryptography "wikipedia:Asymmetric cryptography").

Create a file **in a secure environment** since it will contain your passwords for a couple of seconds:

 `~/.my-pwds` 
```
set my_pw_personal = "*first password*"
set my_pw_work = "*second password*"
```

**Note:** Remember that user defined variables **must** start with `my_`.

Now encrypt the file:

```
gpg -e -r 'your-name' ~/.my-pwds

```

Note that 'your-name' must match the one you provided at the `gpg --gen-key` step. Now you can wipe your file containing your passwords in clear:

```
shred -xu ~/.my-pwds

```

Back to your account dedicated files, e.g. `.mutt/muttrc`:

```
set imap_pass=$my_pw_personal
# Every time the password is needed, use $my_pw_personal variable.
```

And in your `.muttrc`, **before** you source any account dedicated file:

```
source "gpg2 -dq $HOME/.my-pwds.gpg |"

```

**Note:**

*   At the end of the line above, there is no space between the pipe and the double quote.
*   Make sure that you use single quotes instead of double quotes when using your password variable inside of a string. For example: The line `account-hook $folder "set imap_user=user@gmail.com imap_pass=$my_pw_personal"` will **not** work.

*   The `-q` parameter makes gpg2 quiet which prevents gpg2 output messing with Mutt interface.
*   The pipe `|` at the end of a string is the Mutt syntax to tell that you want the result of what is preceeding.

Explanation: when Mutt starts, it will first source the result of the password decryption, that's why it will prompt for a passphrase. Then all passwords will be stored in memory in specific variables for the time Mutt runs. Then, when a folder-hook is called, it sets the imap_pass variable to the variable holding the appropriate password. When switching accounts, the imap_pass variable will be set to another variable holding another password, etc.

If you use external tools like OfflineIMAP and msmtp, you need to set up an agent (e.g. gpg-agent, see [GnuPG#gpg-agent](/index.php/GnuPG#gpg-agent "GnuPG")) to keep the passphrase into cache and thus avoiding those tools always prompting for it.

#### Security concern

If `enter-command` is available from the UI, it is possible to see the password unencrypted, which my be undesired if anybody else than you has access to your session while Mutt is running. You may want to disable it for this reason. As a consequence, every command that the user intends to use must be bound to a key in advance, otherwise it will never be accessible.

 `.muttrc` 
```
 bind generic,alias,attach,browser,editor,index,compose,pager,pgp,postpone ':' noop

```

## Advanced features

Guides to get you started with using & customizing Mutt :

*   [My first Mutt](http://mutt.blackfish.org.uk/) (maintained by Bruno Postle)
*   [The Woodnotes Guide to the Mutt Email Client](http://www.therandymon.com/woodnotes/mutt/using-mutt.html) (maintained by Randall Wood)
*   [The Homely Mutt](http://stevelosh.com/blog/2012/10/the-homely-mutt) (by Steve Losh)
*   [Everything You Need To Know To Start Using GnuPG with Mutt](http://codesorcery.net/old/mutt/mutt-gnupg-howto) (by Justin R. Miller)

If you have any Mutt specific questions, feel free to ask in [the irc channel](/index.php/ArchChannel "ArchChannel").

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

### E-mail character encoding

You may be concerned with sending e-mail in a decent character set (charset for short) like UTF-8\. Nowadays UTF-8 is highly recommended to almost everyone.

When using Mutt there are two levels where the charset must be specified:

*   The text editor used to write the e-mail must save it in the desired encoding.
*   Mutt will then check the e-mail and determine which encoding is the more apropriate according to the priority you specified in the `send_charset` variable. Default: "us-ascii:iso-8859-1:utf-8".

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

### Printing

You can install [muttprint](https://aur.archlinux.org/packages/muttprint/) for fancier printing quality. In your muttrc file, insert:

```
set print_command="/usr/bin/muttprint %s -p {PrinterName}"

```

### Custom mail headers

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

### Signature block

Create a .signature in your home directory. Your signature will be appended at the end of your email. Alternatively you can specify a file in your Mutt configuration:

```
set signature="path/to/sig/file"

```

#### Random signature

You can use *fortune* (package [fortune-mod](https://www.archlinux.org/packages/?name=fortune-mod)) to add a random signature to Mutt.

Create a fortune file and then add the following line to your .muttrc:

 `set signature="fortune pathtofortunefile|"` 

Note the pipe at the end. It tells Mutt that the specified string is not a file, but a command.

### Viewing URLs & opening your favorite web browser

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

### Viewing HTML

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

Edit muttrc and add the following,

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

### Mutt and Vim

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

### Mutt and GNU nano

[nano](/index.php/Nano "Nano") is another nice console editor to use with Mutt.

To limit the width of text to 72 characters, edit your .nanorc file and add:

```
 set fill 72

```

Also, in muttrc file, you can specify the line to start editing so that you will skip the mail header:

```
 set editor="nano +7"

```

### Mutt and Emacs

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

### Colors

Append sample color definitions to your .muttrc file:

```
$ cat /usr/share/doc/mutt/samples/colors.linux >> ~/.muttrc

```

Then adjust to your liking. The actual color each of these settings will produce depends on the colors set in your [~/.Xresources](/index.php/Xresources "Xresources") file.

Alternatively, you can source any file you want containing colors (and thus act as a theme file):

```
source ~/.mutt/colors.zenburn

```

A nice theme example:

```
## Theme kindly inspired from
## http://nongeekshandbook.blogspot.ie/2009/03/mutt-color-configuration.html

## Colours for items in the index
color index brightcyan black ~N
color index brightred black ~O
color index brightyellow black ~F
color index black green ~T
color index brightred black ~D
mono index bold ~N
mono index bold ~F
mono index bold ~T
mono index bold ~D

## Highlights inside the body of a message.

## URLs
color body brightgreen black "(http|ftp|news|telnet|finger)://[^ \"\t\r
]*"
color body brightgreen black "mailto:[-a-z_0-9.]+@[-a-z_0-9.]+"
mono body bold "(http|ftp|news|telnet|finger)://[^ \"\t\r
]*"
mono body bold "mailto:[-a-z_0-9.]+@[-a-z_0-9.]+"

## Email addresses.
color body brightgreen black "[-a-z_0-9.%$]+@[-a-z_0-9.]+\\.[-a-z][-a-z]+"

## Header
color header green black "^from:"
color header green black "^to:"
color header green black "^cc:"
color header green black "^date:"
color header yellow black "^newsgroups:"
color header yellow black "^reply-to:"
color header brightcyan black "^subject:"
color header red black "^x-spam-rule:"
color header green black "^x-mailer:"
color header yellow black "^message-id:"
color header yellow black "^Organization:"
color header yellow black "^Organisation:"
color header yellow black "^User-Agent:"
color header yellow black "^message-id: .*pine"
color header yellow black "^X-Fnord:"
color header yellow black "^X-WebTV-Stationery:"

color header red black "^x-spam-rule:"
color header green black "^x-mailer:"
color header yellow black "^message-id:"
color header yellow black "^Organization:"
color header yellow black "^Organisation:"
color header yellow black "^User-Agent:"
color header yellow black "^message-id: .*pine"
color header yellow black "^X-Fnord:"
color header yellow black "^X-WebTV-Stationery:"
color header yellow black "^X-Message-Flag:"
color header yellow black "^X-Spam-Status:"
color header yellow black "^X-SpamProbe:"
color header red black "^X-SpamProbe: SPAM"

## Coloring quoted text - coloring the first 7 levels:
color quoted cyan black
color quoted1 yellow black
color quoted2 red black
color quoted3 green black
color quoted4 cyan black
color quoted5 yellow black
color quoted6 red black
color quoted7 green black

## Default color definitions
#color hdrdefault white green
color signature brightmagenta black
color indicator black cyan
color attachment black green
color error red black
color message white black
color search brightwhite magenta
color status brightyellow blue
color tree brightblue black
color normal white black
color tilde green black
color bold brightyellow black
#color underline magenta black
color markers brightcyan black

## Colour definitions when on a mono screen
mono bold bold
mono underline underline
mono indicator reverse

```

### Index Format

Here follows a quick example to put in your `.muttrc` to customize the Index Format, i.e. the columns displayed in the folder view.

```
set date_format="%y-%m-%d %T"
set index_format="%2C | %Z [%d] %-30.30F (%-4.4c) %s"

```

See the [Mutt Reference](http://www.mutt.org/doc/manual/manual-6.html), `man 3 strftime` and `man 3 printf` for more details.

#### Display recipient instead of sender in "Sent" folder view

By default Mutt will display the sender in the index view. It is fine for most folders, but rather useless for the one were you store a copy of your sent e-mails since it will always display your name.

The "columns" of the index can be configured through the `index_format` variable. Its syntax is documented in the `muttrc` man page. The values of our concern are `%t` (recipient) and `%F` (sender).

To change the columns according to the current folder, we need to use a hook:

 `muttrc` 
```
folder-hook   *[sS]ent* 'set index_format="%2C | %Z [%d] %-30.30t (%-4.4c) %?M?<%M> ?%s"'
folder-hook ! *[sS]ent* 'set index_format="%2C | %Z [%d] %-30.30F (%-4.4c) %?M?<%M> ?%s"'

```

The exclamation mark means *everything that does not match the following regex*. Of course you can change the index_format following your taste, and the regular expression if the folder does not have *Sent* not *sent* in its name.

Let's centralize the settings, it will simplify future tweaking.

 `muttrc` 
```
set my_index_format_pre='set index_format="%2C | %Z [%d] %-30.30'
set my_index_format_post=' (%-4.4c) %?M?<%M> ?%s"'

folder-hook .*[sS]ent.* "$my_index_format_pre"t"$my_index_format_post"
folder-hook ! .*[sS]ent.* "$my_index_format_pre"F"$my_index_format_post"

```

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
*   `reverse_alias` sorts in reverse order if set to yes.
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

### Manage multiple sender accounts

If you use multiple sender accounts, you can automatically associate a specific sender account with a recipient. [mutt-vid](https://aur.archlinux.org/packages/mutt-vid/) scans sent emails for the most recent "From" details associated with specific recipients, saving these in a file for mutt to source. The next time you email this recipient, mutt will automatically invoke a send-hook with the same email address and real name that you used previously. See mutt-vid's [homepage](https://github.com/protist/mutt-vid) for more details.

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

### Use Mutt to send mail from command line

Man pages will show all available commands and how to use them, but here are a couple of examples. You could use Mutt to send alerts, logs or some other system information, triggered by login through .bash_profile, or as a regular cron job.

Send a message:

```
mutt -s "Subject" somejoeorjane@someserver.com < /var/log/somelog

```

Send a message with attachment:

```
mutt -s "Subject" somejoeorjane@someserver.com -a somefile < /tmp/sometext.txt

```

### Composing HTML e-mails

Since Mutt has nothing of a WYSIWIG client, HTML is quite straightforward, and you can do much more than with all WYSIWIG mail clients around since you edit the source code directly. Simply write your mail using HTML syntax. For example:

```
This is normal text<br>
<b>This is bold text</b>

```

Now before sending the mail, use the `edit-type` command (default shortcut `Ctrl+t`), and replace `text/plain` by `text/html`.

**Note:** HTML e-mails are regarded by many people as useless, cumbersome, and subject to reading issues. Mutt can read HTML mails with a text browser like w3m or lynx, but it has clearly no advantage over a plain-text e-mail. You should avoid writing HTML e-mails when possible.

### How to display another email while composing

A common complaint with Mutt is that when composing a new mail (or reply), you cannot open another mail (i.e. for checking with another correspondent) without closing the current mail (postponing). The following describes a solution:

First, fire up Mutt as usual. Then, launch another terminal window. Now start a new Mutt with

```
mutt -R

```

This starts Mutt in read-only mode, and you can browse other emails at your convenience. It is strongly recommended to always launch a second Mutt in read-only mode, as conflicts will easily arise otherwise.

**Note:** When changing folders (with `c` or `y`) the read-only mode is not preserved. Instead `Esc c` has to be used.

**Tip:** This solution calls for a bit of typing, so it is suitable to bind the following command to a keyboard shortcut (see [Extra Keyboard Keys](/index.php/Extra_Keyboard_Keys "Extra Keyboard Keys") for details):
```
$TERMINAL -e mutt -R

```
where `$TERMINAL` is your terminal.

### Archive treated e-mails

When you read an e-mail, you have four choices: Answer it, Flag it, Archive it or Delete it. If you have this in mind, you can keep your inbox slim and fit with this macro (set up for Gmail):

```
macro index \' "<tag-pattern>~R !~D !~F<enter>\
<tag-prefix><save-message>+[Gmail]/All <enter>" \
"Archive"

```

### Mutt-Sidebar

The vanilla Mutt does not feature a sidebar unlike most MUAs. If you miss it, you can install [mutt-sidebar](https://aur.archlinux.org/packages/mutt-sidebar/) or [mutt-sidebar-hg](https://aur.archlinux.org/packages/mutt-sidebar-hg/) which add a list of folders on the left side of the Mutt window.

For a while there has been several different patches for the sidebar. Since the late 2000's, it seems like the main patch is maintained at [Lunar Linux](http://www.lunar-linux.org/mutt-sidebar/). See the documentation there. Note that the patch also updates the `muttrc` man page, so have a look at the `sidebar_*` sections.

You can choose to display the sidebar on startup, or to prompt it manually with a key:

```
set sidebar_visible = yes
macro index b '<enter-command>toggle sidebar_visible<enter><refresh>'
macro pager b '<enter-command>toggle sidebar_visible<enter><redraw-screen>'

```

You also probabaly need some shortcuts to navigate in the bar:

```
# Ctrl-n, Ctrl-p to select next, previous folder.
# Ctrl-o to open selected folder.
bind index,pager \CP sidebar-prev
bind index,pager \CN sidebar-next
bind index,pager \CO sidebar-open

```

**Note:** You *must* set the `mailboxes` variables or the `imap_check_subscribed` to tell the sidebar which folder should be displayed. See the [mailboxes](#mailboxes) section.

If you use the `imap_check_subscribed` option to list all your folders, they will appear in an uncontrollable order in the sidebar. Fix it with

```
set sidebar_sort = yes

```

Note that with the `mailboxes` option, folders appear in the order they were set to `mailboxes` if you do not use the `sidebar_sort` option.

If you have trouble with truncated names, set the option

```
set sidebar_shortpath = yes

```

Finally, you may want to add a separator between different mailboxes. The sidebar patch does not currently provide any kind of separator option. A simple (and dirty) workaround is to add a fake folder to the list of folders:

```
mailboxes "+-- My mailbox -----------"

```

The dashes are not required, they are here just for fancy output. It will also work if you used the `imap_check_subscribed` option. If you chose to sort the folders, the separator will not appear in the correct place, so an even more dirty workaround is to add an 'A' in front of the name. Note that punctuation is ignored during sorting.

```
mailboxes "+A-- My mailbox -----------"

```

### Migrating mails from one computer to another

In case you are transfering your mails to a new machine (copy&paste), you probably need to delete the header cache (a file or folder like `~/.cache/mutt` if you followed the above configuration) to make Mutt able to read your migrated E-Mails. Otherwise Mutt may freeze.

Note that if you had a folder created for you header cache, all mailboxes will have their own cache file, so you can delete caches individually without having to remove everything.

### Filtering the message view

You can restrict the view to e-mails matching a pattern and specific properties with the `limit` command (default shortcut: `l`).

To view all e-mails containing "foo" in the header, simply write "foo" and you are done. To remove the filter, use the "all" keyword.

To view all flagged messages, use

```
~F

```

To view all unread messages that are either of size ≥1MB or from johndoe, use

```
~U (~z 1- | ~f johndoe)

```

All possible patterns are listed in the [official manual](http://www.mutt.org/doc/manual/manual-4.html#ss4.2).

### Display the index above the pager view

Set the following variable in your `muttrc`:

```
set pager_index_lines=10

```

### Default folder for saving attachments

By default Mutt will save attachments to the folder it was started from. If you want to always set the default destination to `~/attachments`, you can create the following alias, which launches Mutt in this folder:

```
alias mutt='cd ~/attachments && mutt'

```

### PGP signed/encrypted mail

The official Mutt package is compiled with GPGME support. If you have a pair of keys in your [GnuPG](/index.php/GnuPG "GnuPG") keyring, then it suffices to add this:

 `.muttrc` 
```
set crypt_use_gpgme=yes

```

For convenience, you can set further PGP settings:

 `.muttrc` 
```
set crypt_replysign=yes
set crypt_replysignencrypted=yes
set pgp_timeout=3600

```

See the `pgp_*` and `crypt_*` options in `muttrc(5)`.

To be able to view the encrypted message to others, add either `encrypt-to` or `hidden-encrypt-to` in your `~/.gnupg/gpg.conf`.

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

### Conversation grouping

The default sort order is by date. Use the `sort-mailbox` command (default key: `o`) to change the sorting option. You can group e-mails by conversation/thread, in which case you can define how to sort threads and how to sort within a thread.

In the following example, threads are sorted according to the date of their last e-mail.

 `muttrc` 
```
set sort=threads
set sort_aux=last-date-received

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

This macro tells Mutt to sync (which is a write operation) before switching. Either use the [sidebar](#Mutt-Sidebar) or set another macro:

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

If you're having problems with character encoding, first read [this section](http://dev.mutt.org/trac/wiki/MuttFaq/Charset) in the Mutt wiki.

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

## Documentation

Newcomers may find it quite hard to find help for Mutt. Actually most of the topics are covered in the official documentation. We urge you to read it.

*   [The official manual](http://www.mutt.org/doc/manual/). The stock [mutt](https://www.archlinux.org/packages/?name=mutt) package for Arch Linux also installs the HTML and plain text manual at `/usr/share/doc/mutt/`.
*   The `mutt` and `muttrc` man pages.

## See also

*   [The official Mutt website](http://www.mutt.org/)
*   [Official Manual](http://www.mutt.org/doc/devel/manual.html)
*   [The Mutt wiki](http://wiki.mutt.org/)
*   [Brisbin's great guide on how to setup different IMAP accounts with Mutt, offlineimap, msmtp](http://pbrisbin.com/posts/two_accounts_in_mutt/)
*   [A Quick Guide to Mutt](http://srobb.net/mutt.html)
*   [Steve Losh on Mutt, offlineimap, msmtp, notmuch (focused on Gmail)](http://stevelosh.com/blog/2012/10/the-homely-mutt/)
*   [muttrc builder](http://www.muttrcbuilder.org/)