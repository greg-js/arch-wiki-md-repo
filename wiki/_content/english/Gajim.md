[Gajim](https://gajim.org/index.php?lang=en) is a full featured and easy to use XMPP client.

## Contents

*   [1 Installation](#Installation)
*   [2 D-Bus remote control](#D-Bus_remote_control)
*   [3 Show/hide roster](#Show/hide_roster)
*   [4 OMEMO Support](#OMEMO_Support)
*   [5 Minimize / Close to tray](#Minimize_/_Close_to_tray)

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

1.  [Install](/index.php/Install "Install") the [python-axolotl](https://www.archlinux.org/packages/?name=python-axolotl) and [python-qrcode](https://www.archlinux.org/packages/?name=python-qrcode) packages.
2.  Open Gajim and go to menu *Gajim* => *Plugins*;
3.  Go to the *Available* tab;
4.  Mark the "OMEMO" plugin and click the *Install/Update Plugin* button;
5.  Go back to the *Installed* tab;
6.  Activate the "OMEMO" plugin;
7.  Close dialogs to save the changes;
8.  Restart Gajim;
9.  Please refer to the official documentation for [running instructions](https://dev.gajim.org/gajim/gajim-plugins/wikis/OmemoGajimPlugin#running)

## Minimize / Close to tray

By default Gajim remains in the taskbar (for Docks) instead of minimizing to tray when closing it. If you would like to disable this behavior, go to *Preferences > Advanced > Advanced Configuration Editor* and change **hide_on_roster_x_button** to **Activated**.