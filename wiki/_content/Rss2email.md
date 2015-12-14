# Rss2email

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**rss2email** is a free tool for retrieving content from RSS feeds and mailing it. It is useful for those who do not want yet another program with which to keep up and for people who have a system for e-mail management that they would like to apply to their RSS feeds as well. People with lots of e-mail often have highly customized systems that let them process their mail efficiently; rss2email allows them to easily apply this system to their feeds as well.

## Contents

*   [1 Installation](#Installation)
*   [2 Adding feeds](#Adding_feeds)
*   [3 Getting RSS feeds](#Getting_RSS_feeds)
*   [4 Managing rss2email](#Managing_rss2email)
*   [5 Advanced configuration](#Advanced_configuration)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [rss2email-wking](https://aur.archlinux.org/packages/rss2email-wking/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

## Adding feeds

First, tell _rss2email_ where it should send feeds by running the command:

```
$ r2e new _user@example.com_

```

Next, subscribe to an RSS feed. For example, to subscribe to the Arch Linux package updates feed, run:

```
$ r2e add https://www.archlinux.org/feeds/packages/ ''e-mail address''

```

Note that an e-mail address only has to be given if the feed is to be delivered to an address other than the default one; otherwise, leaving off the e-mail address is acceptable.

After a new feed is added, _rss2email_ will e-mail every post it hasn't previously e-mailed. The first time it is run, therefore, it will e-mail every post. To avoid this behavior, after adding a new feed, run:

```
$ r2e run --no-send

```

## Getting RSS feeds

To get new stories, execute the command:

```
$ r2e run

```

To automate this process and have _rss2email_ check for new feeds every 30 minutes, users should add the following to their `[crontab](/index.php/Crontab "Crontab")` by running the command `crontab -e` and appending to the file:

```
*/30 * * * * /usr/bin/r2e run

```

## Managing rss2email

To view feeds previously added to rss2email, run:

```
r2e list

```

This will output a numbered list of feeds. To delete a feed, run:

```
r2e delete _number_

```

where _number_ is the number of the feed to be deleted.

To change the default e-mail address, run:

```
r2e email _new_address@example.net_

```

## Advanced configuration

The following configuration changes should be made in `config.py`, which should be located at `~/.rss2email/config.py`.

To have RSS entries sent as HTML e-mails instead of as plain text, set:

```
HTML_MAIL = 1

```

To receive new e-mails when RSS posts are updated, set:

```
TRUST_GUID = 0

```

To set the date header of e-mails to when the RSS post was written, rather than when the e-mail is actually sent, set:

```
DATE_HEADER = 1

```

To fix the error message "sender domain must exist" or to change the address from which e-mails are sent, set:

```
DEFAULT_FROM = user@example.com

```

To force all feeds to use this address, even if they have their own address set, use:

```
FORCE_FROM = 1

```

To have rss2email automatically wrap long lines, set:

```
BODY_WIDTH = 72

```

Where 72 is the number of characters after which rss2email should start a new line.

To send mail using an SMTP server rather than the local machine, use:

```
SMTP_SEND = 1
SMTP_SERVER = _smtp.example.com:25_

```

If the SMTP server requires authentication, set:

```
AUTHREQUIRED = 1
SMTP_USER = _user@example.com_
SMTP_PASS = _password_

```

## See also

*   [http://www.allthingsrss.com/rss2email/?page_id=31#unix](http://www.allthingsrss.com/rss2email/?page_id=31#unix) - Official getting started page
*   [http://www.linux.com/archive/feed/50469](http://www.linux.com/archive/feed/50469) - linux.com article.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Rss2email&oldid=412168](https://wiki.archlinux.org/index.php?title=Rss2email&oldid=412168)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Email clients](/index.php/Category:Email_clients "Category:Email clients")