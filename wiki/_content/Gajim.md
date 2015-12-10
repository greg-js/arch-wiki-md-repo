# Gajim

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Gajim#](https://wiki.archlinux.org/index.php/Talk:Gajim))

[Gajim](http://gajim.org/index.php?lang=en) is a full featured and easy to use Jabber/XMPP client.

## Contents

*   [1 Installation](#Installation)
*   [2 Auto logout on suspend](#Auto_logout_on_suspend)
*   [3 Off-the-Record Messaging](#Off-the-Record_Messaging)
    *   [3.1 Configuration](#Configuration)

## Installation

[Install](/index.php/Install "Install") the [gajim](https://www.archlinux.org/packages/?name=gajim) package.

## Auto logout on suspend

If you suspend your computer gajim stays connected for about 15 minutes. To prevent message loss, it is needed to set your status offline before suspending or hibernating. The status message won't be changed.

Therefore create a new systemd unit `gajim-suspend@.service`:

 `/etc/systemd/system/gajim-suspend@.service` 

```
[Unit]
Description=Suspend Gajim
Before=sleep.target
StopWhenUnneeded=yes

[Service]
Type=oneshot
User=%I
RemainAfterExit=yes
Environment=DISPLAY=:0
ExecStart=-/usr/bin/bash -c ". /home/%I/.dbus/session-bus/$(</var/lib/dbus/machine-id)-0 && /usr/bin/gajim-remote change_status offline"
ExecStop=/usr/bin/bash -c ". /home/%I/.dbus/session-bus/$(</var/lib/dbus/machine-id)-0 && /usr/bin/gajim-remote change_status online"

[Install]
WantedBy=sleep.target
```

Then [enable](/index.php/Enable "Enable") the service.

## Off-the-Record Messaging

[OTR (off-the-record) messaging](https://en.wikipedia.org/wiki/Off-the-Record_Messaging "wikipedia:Off-the-Record Messaging") is strong end-to-end encryption protocol for instant messaging ([read more](http://www.cypherpunks.ca/otr/)). OTR hasn't any XMPP XEP, because OTR is of cross-protocol nature. Gajim doesn not support OTR out of the box.

Install the [gajim-plugin-otr](https://aur.archlinux.org/packages/gajim-plugin-otr/)<sup><small>AUR</small></sup> package.

### Configuration

At first time, you also need to activate OTR plugin:

1.  Go to menu Edit => Modules;
2.  Activate the "Off-the-record encryption" plugin;
3.  Click on plugin settings button;
4.  Generate your OTR key using "Generate key";
5.  Take a look on other settings;
6.  Close dialogs to save the changes.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Gajim&oldid=374969](https://wiki.archlinux.org/index.php?title=Gajim&oldid=374969)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet applications](/index.php/Category:Internet_applications "Category:Internet applications")