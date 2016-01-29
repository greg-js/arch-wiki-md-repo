# fdm

Related articles

*   [Alpine](/index.php/Alpine "Alpine")
*   [msmtp](/index.php/Msmtp "Msmtp")
*   [Mutt](/index.php/Mutt "Mutt")
*   [Postfix](/index.php/Postfix "Postfix")
*   [SSMTP](/index.php/SSMTP "SSMTP")

**fdm** (_fetch and deliver mail_), is a simple program for delivering and filtering mail. Comparing it to other same-purposed applications shows that it has similarities with [Mutt](/index.php/Mutt "Mutt")'s very focused design principles.

## Contents

*   [1 Installing](#Installing)
*   [2 Configuring](#Configuring)
    *   [2.1 mbox](#mbox)
    *   [2.2 maildir](#maildir)
    *   [2.3 Final setup](#Final_setup)
*   [3 Testing](#Testing)
*   [4 Extended usage](#Extended_usage)
    *   [4.1 Additional filtering](#Additional_filtering)
    *   [4.2 Automation with cron](#Automation_with_cron)
*   [5 See also](#See_also)

## Installing

[Install](/index.php/Install "Install") the [fdm](https://www.archlinux.org/packages/?name=fdm) package.

## Configuring

_fdm_ supports the tried and tested mbox format along with the newer maildir specification.

### mbox

Alpine uses the mbox format, so we need to set up some files that we will be editing.

```
$ cd
$ mkdir mail
$ touch mail/INBOX .fdm.conf 
$ chmod 600 .fdm.conf mail/INBOX

```

### maildir

Mutt prefers a capitized mail directory, and is able to use the maildir format. If you plan on using Mutt do the following setup.

```
$ cd
$ touch .fdm.conf; chmod 600 .fdm.conf
$ mkdir -p Mail/INBOX/{new,cur,tmp}

```

### Final setup

Edit `.fdm.conf`, and add your email accounts and basic filter rules. Use mbox or maildir, but not both.

```
## .fdm.conf
## Accounts and rules for:
#> foo@example.com
#> bar@gmail.com
## Last edit 21-Dec-09

# Catch-all action (mbox):
action "inbox" mbox "%h/mail/INBOX"
# Catch-all action (maildir):
# action "inbox" maildir "%h/Mail/INBOX"

account "foo" imaps server "imap.example.com"
	user "foo@example.com" pass "supersecret"

account "bar" imaps server "imap.gmail.com"
        user "bar@gmail.com" pass "evenmoresecret"

# Match all mail and deliver using the 'inbox' action.
match all action "inbox"

```

This will collect the mail from the listed accounts and deliver it to the INBOX folder that we made. Refer to the `fdm(1)` man page for specifics on how to connect to other types of mail servers (POP3 for example).

**Tip:** You can also specify your login name and/or password in the `.netrc` file.

## Testing

Once you have this setup to your satisfaction, attempt to collect your mail by manually running fdm.

```
$ fdm -kv fetch

```

This will keep your mail untouched on the server incase there are errors. Look over the output to make sure everything worked as planned. Open your favorite mail reader (MUA) and make sure that you can read the mail that was just delivered.

## Extended usage

_Non-essential features that add to_ fdm'_s usability_

### Additional filtering

If you want to have mail from a certain account go to a specific mailbox, you could add the following lines to your fdm.conf file. From the config file above, if you wanted to filter the mail from `_bar@gmail.com_` into it's own folder `_bar-mail_`, you would add this below the existing "action" line:

```
action _bar-deliver_ mbox "%h/mail/_bar-mail_"

```

Change the `mbox` to `maildir` if needed, also make sure the path is correct.

To activate the new action, add this before the existing "match" line:

```
match account _bar_ action _bar-deliver_

```

Then all mail to `_bar@gmail.com_` will be put into the `_bar-mail_` mail folder.

### Automation with cron

If all went well, set up a [cron](/index.php/Cron "Cron") job to check your mail regularly.

```
$ crontab -e
*/15 * * * * fdm fetch >> $HOME/[Mm]ail/fdm.log

```

## See also

*   [fdm's official site (github)](https://github.com/nicm/fdm)
*   [fdm-users mailing list](https://lists.sourceforge.net/lists/listinfo/fdm-users)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Fdm&oldid=411264](https://wiki.archlinux.org/index.php?title=Fdm&oldid=411264)"