# I2P

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

From the I2P homepage:

_I2P is an anonymizing network, offering a simple layer that identity-sensitive applications can use to securely communicate. All data is wrapped with several layers of encryption, and the network is both distributed and dynamic, with no trusted parties._

_Many applications are available that interface with I2P, including mail, peer-peer, IRC chat, and others._

## Installation

I2P is available in the [AUR](/index.php/AUR "AUR"), with [i2p](https://aur.archlinux.org/packages/i2p/)<sup><small>AUR</small></sup> providing compilation from source, and [i2p-bin](https://aur.archlinux.org/packages/i2p-bin/)<sup><small>AUR</small></sup> providing a precompiled binary.

## Usage

First, [start](/index.php/Start "Start") and optionally also enable the `i2prouter.service`.

This will launch the daemon under the system user `i2p`. Next, open your browser of choice and visit the I2P welcome page at

```
127.0.0.1:7657/home

```

From here you can navigate to I2Ps configuration and statistics pages, and links to "Eepsites of Interest" (eepsites being sites available only through the I2P network, similar to how .onion sites are only available through the Tor network). Also, be aware that eepsites are unavailable until the daemon has bootstrapped to the network, which can take several minutes.

To enable the use of outproxies, use the following browser settings:

```
HTTP  127.0.0.1 4444
HTTPS 127.0.0.1 4445

```

## External Links

*   [I2P Homepage](http://www.i2p2.de)
*   [I2P FAQ](http://www.i2p2.de/faq.html)
*   [Homepage mirror](http://www.i2pproject.net)
*   [I2P Wikipedia entry](http://en.wikipedia.org/wiki/I2p)

Retrieved from "[https://wiki.archlinux.org/index.php?title=I2P&oldid=409364](https://wiki.archlinux.org/index.php?title=I2P&oldid=409364)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Networking](/index.php/Category:Networking "Category:Networking")