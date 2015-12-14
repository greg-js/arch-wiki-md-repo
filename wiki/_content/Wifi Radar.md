# Wifi Radar

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[WiFi Radar](http://wifi-radar.tuxfamily.org/) is a nifty little GUI program that lets you switch wireless networks with ease.

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Wifi Radar#](https://wiki.archlinux.org/index.php/Talk:Wifi_Radar))

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Tips and tricks](#Tips_and_tricks)
*   [4 Additional Resources](#Additional_Resources)

## Installation

[Install](/index.php/Install "Install") [wifi-radar](https://www.archlinux.org/packages/?name=wifi-radar) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

Edit `/etc/sudoers` using `visudo` command and add:

```
yourusername     ALL=(ALL) NOPASSWD: /usr/sbin/wifi-radar

```

Run `wifi-radar` from your application menu. If you want to view the available networks or to configure your setup, simply run `wifi-radar` as root.

## Tips and tricks

1.  You might need to edit `/etc/conf.d/wifi-radar` to set the particular network interface that you want to use.

1.  Some users have had to set `ifup required` to `ON` in order for WiFi Radar to work properly.

## Additional Resources

[Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") -- The wireless setup wiki page

Retrieved from "[https://wiki.archlinux.org/index.php?title=Wifi_Radar&oldid=412212](https://wiki.archlinux.org/index.php?title=Wifi_Radar&oldid=412212)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Wireless networking](/index.php/Category:Wireless_networking "Category:Wireless networking")