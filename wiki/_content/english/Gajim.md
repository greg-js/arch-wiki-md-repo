[Gajim](http://gajim.org/index.php?lang=en) is a full featured and easy to use Jabber/XMPP client.

## Contents

*   [1 Installation](#Installation)
*   [2 Auto logout on suspend](#Auto_logout_on_suspend)
*   [3 Off-the-Record Messaging](#Off-the-Record_Messaging)
    *   [3.1 Configuration](#Configuration)
*   [4 OMEMO Support](#OMEMO_Support)
    *   [4.1 Configuration](#Configuration_2)

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

[OTR (off-the-record) messaging](https://en.wikipedia.org/wiki/Off-the-Record_Messaging "wikipedia:Off-the-Record Messaging") is strong end-to-end encryption protocol for instant messaging ([read more](http://www.cypherpunks.ca/otr/)). OTR hasn't any XMPP XEP, because OTR is of cross-protocol nature. Gajim does not support OTR out of the box.

Install the [gajim-plugin-otr](https://aur.archlinux.org/packages/gajim-plugin-otr/) package.

### Configuration

At first time, you also need to activate OTR plugin:

1.  Go to menu Edit => Modules;
2.  Activate the "Off-the-record encryption" plugin;
3.  Click on plugin settings button;
4.  Generate your OTR key using "Generate key";
5.  Take a look on other settings;
6.  Close dialogs to save the changes.

## OMEMO Support

[OMEMO Multi-End Message and Object Encryption](http://conversations.im/omemo/) is an XMPP Extension Protocol (XEP) for secure multi-client end-to-end encryption. It is an open standard based on Axolotl and PEP which can be freely used and implemented by anyone and recently got an experimental [plugin](https://github.com/kalkin/gajim-omemo) for Gajim.

In order to use OMEMO in Gajim, just install the [gajim-plugin-omemo](https://aur.archlinux.org/packages/gajim-plugin-omemo/) package which will also install all the required dependencies.

### Configuration

At first time, you also need to activate OMEMO plugin:

1.  Go to menu Edit => Modules;
2.  Activate the "OMEMO Multi-End Message and Object Encryption" plugin;
3.  Close dialogs to save the changes.
4.  Use the checkbox on the bottom of each chat tab to enable or disable OMEMO encryption. (if you don't see a checkbox you might have "Make message windows compact" enabled in the general settings)
5.  Click on "Get Device Keys".