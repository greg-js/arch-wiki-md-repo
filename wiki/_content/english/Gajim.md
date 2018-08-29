[Gajim](https://gajim.org/index.php?lang=en) is a full featured and easy to use XMPP client.

## Contents

*   [1 Installation](#Installation)
*   [2 D-Bus remote control](#D-Bus_remote_control)
*   [3 Show/hide roster](#Show.2Fhide_roster)
*   [4 OMEMO Support](#OMEMO_Support)
    *   [4.1 Configuration](#Configuration)
*   [5 Off-the-Record Messaging](#Off-the-Record_Messaging)
    *   [5.1 Installation / Configuration](#Installation_.2F_Configuration)
    *   [5.2 gajim-otr version confusions](#gajim-otr_version_confusions)

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

[OMEMO Multi-End Message and Object Encryption](https://conversations.im/omemo/) is an XMPP Extension Protocol (XEP) for secure multi-client end-to-end encryption. It is an open standard based on Axolotl and PEP which can be freely used and implemented by anyone and recently got an experimental [plugin](https://github.com/kalkin/gajim-omemo) for Gajim.

In order to use OMEMO in Gajim, just install the [gajim-plugin-omemo](https://aur.archlinux.org/packages/gajim-plugin-omemo/) package which will also install all the required dependencies. Alternatively, you can install it from Gajim Plugin Manager after installing the dependencies of [gajim-plugin-omemo](https://aur.archlinux.org/packages/gajim-plugin-omemo/).

### Configuration

After installing the OMEMO plugin, you have to enable it in Gajim Plugin Manager in order to use it:

1.  Go to menu Edit => Plugins;
2.  Activate the "OMEMO Multi-End Message and Object Encryption" plugin;
3.  Close dialogs to save the changes.
4.  Restart Gajim.
5.  Please refer to the official documentation for [running instructions](https://dev.gajim.org/gajim/gajim-plugins/wikis/OmemoGajimPlugin#running)

## Off-the-Record Messaging

[OTR (off-the-record) messaging](https://en.wikipedia.org/wiki/Off-the-Record_Messaging "wikipedia:Off-the-Record Messaging") is strong end-to-end encryption protocol for instant messaging ([read more](https://www.cypherpunks.ca/otr/)). OTR hasn't any XMPP XEP, because OTR is of cross-protocol nature. Gajim does not support OTR out of the box.

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