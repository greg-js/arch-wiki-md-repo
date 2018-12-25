[Gajim](https://gajim.org/index.php?lang=en) is a full featured and easy to use XMPP client.

## Contents

*   [1 Installation](#Installation)
*   [2 D-Bus remote control](#D-Bus_remote_control)
*   [3 Show/hide roster](#Show/hide_roster)
*   [4 OMEMO Support](#OMEMO_Support)
*   [5 Off-the-Record Messaging](#Off-the-Record_Messaging)
    *   [5.1 gajim-otr version confusions](#gajim-otr_version_confusions)

## Installation

[Install](/index.php/Install "Install") the [gajim](https://www.archlinux.org/packages/?name=gajim) package.

## D-Bus remote control

To enable D-Bus remote control support, go to *Preferences > Advanced > Advanced Configuration Editor*, open the 'Advanced Configuration Editor', enable *remote_control*, and then restart Gajim.

## Show/hide roster

If you would like to be able to show/hide the roster using a script or your wm, you can use the following command from the terminal.

```
$ gajim-remote toggle_roster_appearance

```

It may be necessary to restart Gajim if this doesn't work.

## OMEMO Support

[OMEMO Multi-End Message and Object Encryption](https://conversations.im/omemo/) is an XMPP Extension Protocol (XEP) for secure multi-client end-to-end encryption. It is an open standard based on Axolotl and PEP which can be freely used and implemented by anyone.

In order to use OMEMO in Gajim, follow these steps:

1.  Go to menu Edit => Plugins;
2.  Go to the available plugins window;
3.  Mark the "OMEMO Multi-End Message and Object Encryption" plugin;
4.  Back to the "Installed" plugins window;
5.  Activate the "OMEMO Multi-End Message and Object Encryption" plugin;
6.  Close dialogs to save the changes;
7.  Restart Gajim;
8.  Please refer to the official documentation for [running instructions](https://dev.gajim.org/gajim/gajim-plugins/wikis/OmemoGajimPlugin#running)

## Off-the-Record Messaging

The [OTR (off-the-record) messaging](https://en.wikipedia.org/wiki/Off-the-Record_Messaging "wikipedia:Off-the-Record Messaging") have some bugs that can lead to accidently sending plaintext. It is recommended to use PGP or [OMEMO](https://conversations.im/omemo/) instead.

The OTR plugin won't work with Gajim >= 1.0 as it was not ported to python3\. There is no port planned.

### gajim-otr version confusions

There are two differently developed/deployed versions of gajim-otr. One was developed at [github](https://github.com/python-otr/gajim-otr) but soon got merged into [gajim's own plugin-repository](https://dev.gajim.org/gajim/gajim-plugins/commits/master/gotr). [This repository](https://dev.gajim.org/gajim/gajim-plugins/wikis/home) is used for the development of many plugins, those plugins then get installed via. "Plugin Installer" from [ftp.gajim.org](ftp://ftp.gajim.org/) at the "view => plugins menu". github/gajim-otr shall not be used, due the fact it's source is outdated and [not maintained](https://github.com/python-otr/gajim-otr/wiki).