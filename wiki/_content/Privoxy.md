# Privoxy

[Privoxy](http://www.privoxy.org/) is a filtering proxy for the HTTP protocol, frequently used in combination with [Tor](/index.php/Tor "Tor"). Privoxy is a web proxy with advanced filtering capabilities for protecting privacy, filtering web page content, managing cookies, controlling access, and removing ads, banners, pop-ups, etc. It supports both stand-alone systems and multi-user networks.

Using Privoxy is necessary when they use a [SOCKS](https://en.wikipedia.org/wiki/SOCKS "wikipedia:SOCKS") proxy directly because browsers leak your DNS requests, which reduces your anonymity.

## Contents

*   [1 Installation and setup](#Installation_and_setup)
*   [2 i2p](#i2p)
*   [3 Forwarding through tor](#Forwarding_through_tor)
*   [4 Tips](#Tips)
    *   [4.1 Privoxy and Polipo](#Privoxy_and_Polipo)
*   [5 Ad Blocking with Privoxy](#Ad_Blocking_with_Privoxy)
*   [6 Usage](#Usage)
*   [7 See also](#See_also)

## Installation and setup

[Install](/index.php/Install "Install") the [privoxy](https://www.archlinux.org/packages/?name=privoxy) package from the [official repositories](/index.php/Official_repositories "Official repositories").

When Privoxy is used in conjunction with [Tor](/index.php/Tor "Tor") the two applications need to exchange information through a chain, which requires the specification of forwarding rules.

Finally, if you plan to make Privoxy available to other computers in your network, just add:

```
listen-address [SERVER-IP]:[PORT]

```

For example:

```
listen-address 192.168.1.1:8118

```

## i2p

To forward .i2p sites through the [I2P](/index.php/I2P "I2P") router, add the following to `/etc/privoxy/config`:

```
forward .i2p localhost:4444

```

## Forwarding through tor

Edit your `/etc/privoxy/config` file and add this line at the end (be sure to include the . at the end

```
forward-socks5 / localhost:9050 .

```

This example uses the default port used by Tor. If you changed the port number modify the example accordingly. The same basic example is valid for other targets. If you plan on chaining to another proxy specify the method (here [SOCKS5](https://en.wikipedia.org/wiki/SOCKS#SOCKS5 "wikipedia:SOCKS")) and the port to suit your needs. Refer to section 5 of the manual inside `/etc/privoxy/config` for a complete list of options and examples.

The above will forward all browser traffic through Tor. To only forward .onion sites through Tor, use this instead:

```
forward-socks4a .onion localhost:9050 .

```

## Tips

### Privoxy and Polipo

**Warning:** Using persistent caching like this will reduce the anonymity of tor (or another proxy), since detecting caching due to lack of certain requests is possible.

If you like to use a small and fast caching web proxy with Privoxy, you can use [Polipo](/index.php/Polipo "Polipo"). Then you have to forward Privoxy's traffic to Polipo by forwarding all traffic to Polipo's port 8123:

```
forward / localhost:8123 .

```

## Ad Blocking with Privoxy

**Warning:** Blocking advertisements can reduce anonymity, since it creates a unique browser signature. This should not be done when using tor or another proxy for anonymity.

Using an ad blocking extension in a web browser can increase page load time. Additionally, extensions like AdBlock Plus are not supported by all browsers. A useful alternative is to install system-wide ad blocking by setting a proxy address in your preferred browser.

Once Privoxy has been installed download and install the Opera urlfilter importer from [AUR](/index.php/AUR "AUR") (i.e. [blocklist-to-privoxy](https://aur.archlinux.org/packages/blocklist-to-privoxy/?ID=63431)). You can optionally use an [AUR Helper](/index.php/AUR_Helper "AUR Helper") to do so.

You can use adblock plus filters instead of the above "opera-fanboy" filters (fanboy filters haven't been updated in a long time anyway). The script here ([https://github.com/Andrwe/privoxy-blocklist](https://github.com/Andrwe/privoxy-blocklist)) automatically downloads adblock plus filters, converts them to a privoxy friendly format, and edits privoxy's config file to include those filters. 1) Run this script once to create /etc/conf.d/privoxy-blacklist 2) edit /etc/conf.d/privoxy-blacklist, and uncomment the line that says "PRIVOXY_USER=" and the two lines below it. 3) Run the script again to download and install the blocklists. 4) restart privoxy.

To block tracking via embedded Facebook "Like" button, Twitter "follow", and Google Plus "+1", edit `/etc/privoxy/user.action` and add these lines to the end:

```
{+block-as-image{Facebook "like" and similar tracking URLs.}}
www.facebook.com/(extern|plugins)/(login_status|like(box)?|activity|fan)\.php
platform.twitter.com/widgets/follow_button?
plusone.google.com

```

## Usage

[Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the Privoxy service (`privoxy.service`).

Configure your program to use Privoxy. The default address is:

```
localhost:8118

```

For Firefox, go to:

```
Preferences > Advanced > Network > Settings

```

For Chromium you can use:

```
$ chromium --proxy-server="localhost:8118"

```

Alternatively you can set `http_proxy` environment variable, which is respected by Firefox, Chromium and other applications:

```
http_proxy="http://localhost:8118"

```

## See also

*   [Privoxy Official Website](http://www.privoxy.org/)
*   [Tor Official Website](https://www.torproject.org/index.html.en)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Privoxy&oldid=412159](https://wiki.archlinux.org/index.php?title=Privoxy&oldid=412159)"