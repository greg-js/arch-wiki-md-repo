[WiFi Radar](http://wifi-radar.tuxfamily.org/) is a nifty little GUI program that lets you switch wireless networks with ease.

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