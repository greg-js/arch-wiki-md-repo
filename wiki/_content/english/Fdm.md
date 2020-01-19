Related articles

*   [Alpine](/index.php/Alpine "Alpine")
*   [msmtp](/index.php/Msmtp "Msmtp")
*   [Mutt](/index.php/Mutt "Mutt")
*   [Postfix](/index.php/Postfix "Postfix")
*   [SSMTP](/index.php/SSMTP "SSMTP")

**fdm** (*fetch and deliver mail*), is a simple program for delivering and filtering mail. Comparing it to other same-purposed applications shows that it has similarities with [Mutt](/index.php/Mutt "Mutt")'s very focused design principles.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installing](#Installing)
*   [2 Configuring](#Configuring)
    *   [2.1 mbox](#mbox)
    *   [2.2 maildir](#maildir)
    *   [2.3 Final setup](#Final_setup)
*   [3 Testing](#Testing)
*   [4 Extended usage](#Extended_usage)
    *   [4.1 Additional filtering](#Additional_filtering)
    *   [4.2 Automation](#Automation)
        *   [4.2.1 Cron](#Cron)
        *   [4.2.2 Systemd Timer](#Systemd_Timer)
*   [5 See also](#See_also)

## Installing

[Install](/index.php/Install "Install") the [fdm](https://www.archlinux.org/packages/?name=fdm) package.

## Configuring

*fdm* supports the tried and tested mbox format along with the newer maildir specification.

### mbox

Alpine uses the mbox format, so we need to set up some files that we will be editing:

```
$ cd
$ mkdir mail
$ touch mail/INBOX .fdm.conf 
$ chmod 600 .fdm.conf mail/INBOX

```

### maildir

Mutt prefers a capitized mail directory, and is able to use the maildir format. If you plan on using Mutt do the following setup:

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

This will collect the mail from the listed accounts and deliver it to the INBOX folder that we made. Refer to the [fdm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fdm.1) man page for specifics on how to connect to other types of mail servers (POP3 for example).

**Tip:** You can also specify your login name and/or password in the `.netrc` file.

## Testing

Once you have this setup to your satisfaction, attempt to collect your mail by manually running fdm.

```
$ fdm -kv fetch

```

This will keep your mail untouched on the server incase there are errors. Look over the output to make sure everything worked as planned. Open your favorite mail reader (MUA) and make sure that you can read the mail that was just delivered.

## Extended usage

### Additional filtering

If you want to have mail from a certain account go to a specific mailbox, you could add the following lines to your fdm.conf file. From the config file above, if you wanted to filter the mail from `*bar@gmail.com*` into it's own folder `*bar-mail*`, you would add this below the existing "action" line:

```
action *bar-deliver* mbox "%h/mail/*bar-mail*"

```

Change the `mbox` to `maildir` if needed, also make sure the path is correct.

To activate the new action, add this before the existing "match" line:

```
match account *bar* action *bar-deliver*

```

Then all mail to `*bar@gmail.com*` will be put into the `*bar-mail*` mail folder.

### Automation

Since *fdm* does not run as a daemon, timed mail fetching is left to job schedulers like [cron](/index.php/Cron "Cron") or [systemd timers](/index.php/Systemd/Timers "Systemd/Timers"). This section will show implementations for both.

#### Cron

Fetch and sort mail from all accounts every 15 minutes, appending a log all matches to a local file:

 `$ crontab -e` 
```
...
*/15 * * * * fdm fetch >> $HOME/[Mm]ail/fdm.log

```

#### Systemd Timer

Setup the fdm service for the local user to fetch and sort mail from all accounts:

 `${XDG_CONFIG_HOME:-$HOME/.config}/systemd/user/fdm.service` 
```
[Unit]

Description=Fetch mail using fdm
After=network.target network-online.target dbus.socket
Documentation=man:fdm(1)

[Service]
Type=oneshot
ExecStart=/usr/bin/fdm fetch

```

Then setup the timer to run the service every 15 minutes:

 `${XDG_CONFIG_HOME:-$HOME/.config}/systemd/user/fdm.timer` 
```
[Unit]
Description=Fetch mail using fdm

[Timer]
# Uncomment to run the service two minutes after booting
# OnBootSec=2m
OnUnitActiveSec=15m
Persistent=true

[Install]
WantedBy=timers.target

```

Finally:

```
$ systemctl --user daemon-reload
$ systemctl --user start fdm.timer

```

## See also

*   [fdm's official site (github)](https://github.com/nicm/fdm)
*   [fdm-users mailing list](https://lists.sourceforge.net/lists/listinfo/fdm-users)