Procmail is a program for filtering, sorting and storing email. It can be used both on mail clients and mail servers. It can be used to filter out spam, checking for viruses, to send automatic replies, etc.

The goal of this article is to teach the configuration of procmail. This article assumes you already have either a email client ([mutt](/index.php/Mutt "Mutt"), [nmh](/index.php/Nmh "Nmh"), etc) or a mail server ([sendmail](/index.php/Sendmail "Sendmail"), [postfix](/index.php/Postfix "Postfix"), etc) working, that can use (or requires) procmail. It also assumes you have at least basic knowledge on regular expressions. This article will give only a minimal explanation, for a complete manual, check the `man procmailrc`

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Assignments](#Assignments)
    *   [2.2 Recipes](#Recipes)
        *   [2.2.1 Flags and lockfile](#Flags_and_lockfile)
        *   [2.2.2 Conditions](#Conditions)
        *   [2.2.3 Action](#Action)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Spamassassin](#Spamassassin)
    *   [3.2 ClamAV](#ClamAV)
    *   [3.3 Filtering mail to a different mailbox](#Filtering_mail_to_a_different_mailbox)
    *   [3.4 Postfix Piping](#Postfix_Piping)
    *   [3.5 Sending to Dovecot](#Sending_to_Dovecot)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the package [procmail](https://www.archlinux.org/packages/?name=procmail) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

The configuration is going to be saved on `~/.procmailrc` if this is the configuration for an email client, or on `/etc/procmailrc` if is going to be used by an email server.

**Note:** Be careful when testing your procmail configuration on sample messages you have received, as messages can be automatically bounced back to sender if there is an error in your configuration file. To avoid this potentially embarrassing situation, turn off bounces by passing `-t` to `procmail`, or setting the `DELIVERED` environment variable (`man procmailrc`).

The configuration is composed of two sections; **assignments** and **recipes**.

### Assignments

The assignments section provides variables for procmail

```
PATH=/bin:/usr/bin
MAILDIR=$HOME/Mail
DEFAULT=$HOME/Mail/inbox
LOGFILE=/dev/null
SHELL=/bin/sh

```

### Recipes

Recipes are the main section, they are the actual filters that do the actions. Recipes have the following format:

```
:0 [flags] [ : [locallockfile] ]
<zero or more conditions (one per line)>
<exactly one action line>

```

The conditions are extended regular expressions, with some few extra options. Conditions always start with an asterisk.

The action can be only a mailbox name, or an external program.

#### Flags and lockfile

For basic recipes, you do not need any flags. But they can be necessary if your script calls an external command. Here is a list of some of the most used flags:

*   **f** Consider the pipe as a filter.
*   **w** Wait for the filter or program to finish and check its exitcode (normally ignored); if the filter is unsuccessful, then the text will not have been filtered.

Using a `:` after the `:0` is to use a lockfile. A lockfile is necessary to prevent problems if 2 or more instances of procmail are working at the same time (that may happen if 2 or more email arrive almost at the same moment).

You can set the name of the lockfile after the `:`

#### Conditions

A condition starts with an asterisk, following an extended regexp, like this one:

 `* ^From.* someperson@\w+.com` 

#### Action

An action can be something as simple as

 `work` 

in that case, the mail that complies with the condition will be saved in the `work` inbox.

An action can also start with a pipe, which means the message is going to be passed to the standard input of the command following the pipe. For example:

```
| /usr/bin/vendor_perl/spamc 

```

By default, once a recipe's action is done, the processing is over.

If the **f** flag was used, the command can alter the message and keep reading recipes. In this example, the spamassassin command will add headers to the mail, with its spam status level, which later can be used by **another recipe** to block it, or store it on a different mailbox.

## Tips and tricks

### Spamassassin

Here is an example using spamassassin to block spam. You should already have spamassassin installed and working.

```
# By using the f and w flags and no condition, spamassassin is going add the X-Spam headers to every single mail, and then process other recipes.
# No lockfile is used.
:0fw
| /usr/bin/vendor_perl/spamc

# Messages with a 5 stars or higher spam level are going to be deleted right away
# And since we never touch any inbox, no lockfile is needed.
:0
* ^X-Spam-Level: \*\*\*\*\*
/dev/null

# If a mail with spam-status:yes was not deleted by previous line, it could be a false positive. So its going to be sent to an spam mailbox instead.
# Since we do not want the possibility of one procmail instance messing with another procmail instance, we use a lockfile
:0:
* ^X-Spam-Status: Yes
$HOME/mail/Spam

```

### ClamAV

An example using the [ClamAV](/index.php/ClamAV "ClamAV") antivirus.

```
# We make sure its going to use the sh shell. Mostly needed for mail-only account that have /sbin/nologin as shell
SHELL=/bin/sh

# We will scan the mail with clam using the standard input, and saving the result on the AV_REPORT variable
AV_REPORT=`clamdscan --stdout --no-summary - |sed 's/^stream: //'`

# We check if the word FOUND was in the result and save "Yes" or "No" according to that
VIRUS=`echo $AV_REPORT|sed '/FOUND/ { s/.*/Yes/; q  };  /FOUND/  !s/.*/No/'`

# formail is a filter that can alter a mail message, while keeping the correct format. We use it here to add/alter a header called 
# X-Virus with either value Yes or No
:0fw
| formail -i "X-Virus: $VIRUS"

# And if we just added "X-Virus: Yes", we will also add another header with the scan result, and alter the subject, again, with the scan result.
# Since we are using the f flag, the mail is going to be delivered anyway.
:0fw
* ^X-Virus: Yes
| formail -i "X-Virus-Report: $AV_REPORT" -i "Subject: [Virus] $AV_REPORT"

```

### Filtering mail to a different mailbox

If a coworker keeps using *forward* to send you jokes and other non serious stuff, but at the same time, writes you work related mails, you could save the forwarded mails (most likely not-work-related mails) on a different mailbox.

```
:0:
* ^From.*coworker@domain.com
* ^Subject.*FW:
$HOME/mail/jokes

```

### Postfix Piping

To pipe from [postfix](/index.php/Postfix "Postfix") open `/etc/postfix/main.cf` then add

```
mailbox_command = /usr/bin/procmail -a "$EXTENSION"

```

After [reloading](/index.php/Reload "Reload") `postfix.service`, email will be send to procmail for filtering and delivery.

### Sending to Dovecot

To forward to [dovecot](/index.php/Dovecot "Dovecot") change the following assignments

The deliver will be the first attempt then Default will be the back up.

```
DELIVER="/usr/lib/dovecot/deliver -d $LOGNAME"
DEFAULT="$HOME/Maildir/"
MAILDIR="$HOME/Maildir/"

```

The advantage is the dovecot will have its databases up to date at all times.

Then to spam mail and deliver for example

```
# deliver spam to spam folder
:0 w
* ^X-Spam-Status: Yes
| $DELIVER -m Spam

# deliver to INBOX and stop
:0 w
| $DELIVER

```

Further information can be found here [http://wiki2.dovecot.org/procmail](http://wiki2.dovecot.org/procmail)

## See also

*   [Procmail Homepage](http://www.procmail.org/)