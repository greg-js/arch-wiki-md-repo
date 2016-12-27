[WiFi Radar](http://wifi-radar.tuxfamily.org/) is a nifty little GUI program that lets you switch wireless networks with ease.

## Installation

[Install](/index.php/Install "Install") [wifi-radar](https://www.archlinux.org/packages/?name=wifi-radar) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

The project's [documention](http://wifi-radar.tuxfamily.org/support/user-manual.html) gives a good overview for the user interface.

*wifi-radar* needs to be run with administrative privileges. Edit `/etc/sudoers` using the *visudo* command and add:

```
*yourusername*     ALL=(ALL) NOPASSWD: /usr/sbin/wifi-radar

```

Then, run *wifi-radar* from your application menu to view the available networks or to configure your setup.

For configuration file options, see the project's [manual](http://wifi-radar.tuxfamily.org/support/user-manual.html).

**Tip:**

*   You may edit `/etc/conf.d/wifi-radar` to set a particular network interface that you want to use.
*   Some users have had to set `ifup required` to `ON` in order for WiFi Radar to work properly.