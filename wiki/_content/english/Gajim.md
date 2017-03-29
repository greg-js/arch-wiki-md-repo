[Gajim](http://gajim.org/index.php?lang=en) is a full featured and easy to use Jabber/XMPP client.

## Contents

*   [1 Installation](#Installation)
*   [2 Enabling DBus remote control Support](#Enabling_DBus_remote_control_Support)
*   [3 Enabling OpenPGP](#Enabling_OpenPGP)
*   [4 Show/hide roster](#Show.2Fhide_roster)
*   [5 Auto logout on suspend](#Auto_logout_on_suspend)
*   [6 Off-the-Record Messaging](#Off-the-Record_Messaging)
    *   [6.1 Installation / Configuration](#Installation_.2F_Configuration)
    *   [6.2 gajim-otr version confusions](#gajim-otr_version_confusions)
*   [7 OMEMO Support](#OMEMO_Support)
    *   [7.1 Configuration](#Configuration)

## Installation

[Install](/index.php/Install "Install") the [gajim](https://www.archlinux.org/packages/?name=gajim) package. Then, restart Gajim.

## Enabling DBus remote control Support

As of version 0.16.6, DBus support is disabled, in order to activate it, enable *remote_control* in the 'Advanced Configuration Editor' (Preferences -> Advanced -> 'Advanced Configuration Editor'), then restart Gajim.

## Enabling OpenPGP

Needs the packages python2-gnupg python2-gnupginterface. The python3 packages won’t suffice as of 0.16.7-1.

## Show/hide roster

If you would like to be able to show/hide the roster using a script or your wm, you can use the following command from the terminal.

```
$ gajim-remote toggle_roster_appearance

```

It may be necessary to restart Gajim if this doesn't work.

## Auto logout on suspend

If you suspend your computer gajim stays connected for about 15 minutes. To prevent message loss, it is needed to set your status offline before suspending or hibernating. The status message won't be changed.

This can be achieved by creating a new systemd unit `gajim-suspend@.service` that uses Gajim's [D-Bus](/index.php/D-Bus "D-Bus") interface:

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

The D-Bus remote control feature must be enabled for the systemd unit to work. It can be tested using

```
$ gajim-remote check_gajim_running

```

In case it returns "False" while Gajim is running, enable DBus Support, restart Gajim, then [enable](/index.php/Enable "Enable") the service.

## Off-the-Record Messaging

[OTR (off-the-record) messaging](https://en.wikipedia.org/wiki/Off-the-Record_Messaging "wikipedia:Off-the-Record Messaging") is strong end-to-end encryption protocol for instant messaging ([read more](http://www.cypherpunks.ca/otr/)). OTR hasn't any XMPP XEP, because OTR is of cross-protocol nature. Gajim does not support OTR out of the box.

### Installation / Configuration

1.  Go to "contact-window" menu "Edit => Plugins";
2.  If not activated out of the box, activate the "Plugin Installer";
3.  Restart Gajim.
4.  In "plugins-window", switch to the "Available" tab;
5.  Activate the "Off-the-record encryption" plugin;
6.  Restart Gajim.
7.  Click on plugin settings button;
8.  Generate your OTR key using "Generate key";
9.  Take a look on other settings;
10.  Close dialogs to save the changes.
11.  Restart Gajim.

### gajim-otr version confusions

There are two differently developed/deployed versions of gajim-otr. One was developed at [github](https://github.com/python-otr/gajim-otr) but soon got merged into [gajim's own plugin-repository](https://dev.gajim.org/gajim/gajim-plugins/commits/master/gotr). [This repository](https://dev.gajim.org/gajim/gajim-plugins/wikis/home) is used for the development of many plugins, those plugins then get installed via. "Plugin Installer" from [ftp.gajim.org](ftp://ftp.gajim.org/) at the "view => plugins menu". github/gajim-otr shall not be used, due the fact it's source is outdated and [not maintained](https://github.com/python-otr/gajim-otr/wiki).

## OMEMO Support

[OMEMO Multi-End Message and Object Encryption](http://conversations.im/omemo/) is an XMPP Extension Protocol (XEP) for secure multi-client end-to-end encryption. It is an open standard based on Axolotl and PEP which can be freely used and implemented by anyone and recently got an experimental [plugin](https://github.com/kalkin/gajim-omemo) for Gajim.

In order to use OMEMO in Gajim, just install the [gajim-plugin-omemo](https://aur.archlinux.org/packages/gajim-plugin-omemo/) package which will also install all the required dependencies.

### Configuration

After installing the OMEMO plugin, you have to enable it in Gajim Plugin Manager in order to use it:

1.  Go to menu Edit => Plugins;
2.  Activate the "OMEMO Multi-End Message and Object Encryption" plugin;
3.  Close dialogs to save the changes.
4.  Restart Gajim.
5.  Please refer to the official documentation for [running instructions](https://dev.gajim.org/gajim/gajim-plugins/wikis/OmemoGajimPlugin#running)