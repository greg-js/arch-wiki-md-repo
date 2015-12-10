# Capi4hylafax

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Capi4hylafax#](https://wiki.archlinux.org/index.php/Talk:Capi4hylafax))

### Installation

[Install](/index.php/Install "Install") the [capi4hylafax](https://www.archlinux.org/packages/?name=capi4hylafax) package.

### Setup:

*   Please run 'faxsetup' as root user to adjust hylafax to your needs.
*   Do not even try to run faxaddmodem for capi20 devices!!!
*   c2faxaddmodem' is a nice tool for configuring your isdn card.
*   var/spool/hylafax/etc/config/config.faxCAPI to your needs, if you need more.
*   Please add 'hylafax' and 'capi4hylafax' to your daemons list in /etc/rc.conf.
*   Please be sure that your device has the right permissions 'uucp', udev users please
*   restart udev after installation.

*   Add the following two lines to /var/spool/hylafax/etc/config:

```
   SendFaxCmd: /usr/bin/c2faxsend

```

### Notes:

*   to save your config, please do not forget to add to /etc/pacman.conf

```
 NoUpgrade   = var/spool/hylafax/etc/config/config.faxCAPI

```

*   If you need more than one isdn controller please read the manual of capi4hylafax.

For comments about the package please use this thread: [https://bbs.archlinux.org/viewtopic.php?t=11089](https://bbs.archlinux.org/viewtopic.php?t=11089)

For Hints and Tips please have a look at [Hylafax](/index.php/Hylafax "Hylafax") wiki.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Capi4hylafax&oldid=382709](https://wiki.archlinux.org/index.php?title=Capi4hylafax&oldid=382709)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Modems](/index.php/Category:Modems "Category:Modems")