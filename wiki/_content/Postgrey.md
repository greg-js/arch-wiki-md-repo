# Postgrey

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Postfix](/index.php/Postfix "Postfix").**

**Notes:** Short enough, and [Postfix](/index.php/Postfix "Postfix") is already listing other addons. (Discuss in [Talk:Postgrey#](https://wiki.archlinux.org/index.php/Talk:Postgrey))

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** See [Help:Style](/index.php/Help:Style "Help:Style"). (Discuss in [Talk:Postgrey#](https://wiki.archlinux.org/index.php/Talk:Postgrey))

Related articles

*   [Postfix](/index.php/Postfix "Postfix")

[Postgrey](http://postgrey.schweikert.ch/) can be used to enable greylisting for a Postfix mail server.

## Installation

[Install](/index.php/Install "Install") the [postgrey](https://www.archlinux.org/packages/?name=postgrey) package. To get it running quickly edit the Postfix configuration file and add these lines:

 `/etc/postfix/main.cf` 

```
smtpd_recipient_restrictions =
  check_policy_service inet:127.0.0.1:10030

```

Then [start/enable](/index.php/Start/enable "Start/enable") the `postgrey` service. Afterwards, reload the `postfix` service. Now greylisting should be enabled.

## Configuration

Configuration is done via editing the `greylist.service` file. First copy it over to edit it.

```
# cp /usr/lib/systemd/system/postgrey.service /etc/systemd/system/

```

Now you can edit it. For example, to add automatic whitelisting (successful deliveries are whitelisted and don't have to wait any more), you could add the `--auto-whitelist-clients=N` option and replace `N` by a suitably small number (or leave it at its default of 5).

For a full documentation of possible options see `perldoc postgrey`.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Postgrey&oldid=388088](https://wiki.archlinux.org/index.php?title=Postgrey&oldid=388088)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Mail server](/index.php/Category:Mail_server "Category:Mail server")