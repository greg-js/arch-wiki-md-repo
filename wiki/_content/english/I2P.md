From the [I2P](https://geti2p.net/en/) homepage:

	I2P is an anonymizing network, offering a simple layer that identity-sensitive applications can use to securely communicate. All data is wrapped with several layers of encryption, and the network is both distributed and dynamic, with no trusted parties.

	Many applications are available that interface with I2P, including mail, peer-peer, IRC chat, and others.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Eepsite](#Eepsite)
*   [4 See also](#See_also)

## Installation

I2P is available with the [i2p](https://aur.archlinux.org/packages/i2p/) package providing compilation from source, and the [i2p-bin](https://aur.archlinux.org/packages/i2p-bin/) package providing a precompiled binary.

The I2P homepage also provides a precompiled binary package for command line (headless) install in the users home directory. In case of this installation type I2P will auto update itself through the i2p network.

A [Java](/index.php/Java "Java") Runtime Environment is required, OpenJDK is fine, for arm platform Oracle Java is recommended.

## Usage

First, [start](/index.php/Start "Start") and optionally also enable the `i2prouter.service`.

This will launch the daemon under the system user `i2p`. Next, open your browser of choice and visit the I2P welcome page at

```
127.0.0.1:7657/home

```

From here you can navigate to I2Ps configuration and statistics pages, and links to "Eepsites of Interest" (an [w:eepsite](https://en.wikipedia.org/wiki/eepsite "w:eepsite") being a site available only through the I2P network, similar to how .onion sites are only available through the Tor network). Also, be aware that eepsites are unavailable until the daemon has bootstrapped to the network, which can take several minutes.

In order to visit eepsite's configure your browser to use the local http proxy (not socks):

```
HTTP  127.0.0.1 4444
HTTPS 127.0.0.1 4445

```

## Eepsite

If you make an eepsite, follow the I2P instructions, but keep in mind that the home directory will apply to the i2p user whose home directory is `/opt/i2p` as shown in the AUR [i2p.install](https://aur.archlinux.org/cgit/aur.git/tree/i2p.install?h=i2p) file.

## See also

*   [I2P Homepage](http://www.i2p2.de)
*   [I2P FAQ](http://www.i2p2.de/faq.html)
*   [Homepage mirror](http://www.i2pproject.net)
*   [I2P Wikipedia entry](https://en.wikipedia.org/wiki/I2p "wikipedia:I2p")