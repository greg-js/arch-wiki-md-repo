[I2P](https://geti2p.net/en/about/intro) is an anonymizing network, offering a simple layer that identity-sensitive applications can use to securely communicate. All data is wrapped with several layers of encryption, and the network is both distributed and dynamic, with no trusted parties. Many applications are available that interface with I2P, including mail, peer-peer, IRC chat, and others.

## Installation

Install the [i2pd](https://www.archlinux.org/packages/?name=i2pd) package for the daemon written in C++ which may suit hardware with limited resources or [i2pd-git](https://aur.archlinux.org/packages/i2pd-git/) for the development version.

The standard I2P suite is available with the [i2p](https://aur.archlinux.org/packages/i2p/) and [i2p-bin](https://aur.archlinux.org/packages/i2p-bin/) packages. Both require a [Java](/index.php/Java "Java") Runtime Environment (i.e. [OpenJDK](/index.php/OpenJDK "OpenJDK")). Oracle Java is recommended for the ARM platform.

The I2P homepage also provides a pre-compiled binary which includes command line (headless) option and can be installed in the user's home directory. In this case I2P will auto update itself through the i2p network.

## Usage

First, [start](/index.php/Start "Start") and optionally also enable the `i2pd.service`.

This will launch the daemon under the system user `i2p`. Next, open your browser of choice and visit the I2P welcome page at

```
127.0.0.1:7070

```

From here you can navigate to I2Ps configuration and statistics pages, and links to "Eepsites of Interest" (an [w:eepsite](https://en.wikipedia.org/wiki/eepsite "w:eepsite") being a site available only through the I2P network, similar to how `.onion` sites are only available through the Tor network). Also, be aware that eepsites are unavailable until the daemon has bootstrapped to the network, which can take several minutes.

In order to visit eepsite's configure your browser to use the local http proxy (not socks):

```
HTTP  127.0.0.1 4444
HTTPS 127.0.0.1 4445

```

## Eepsite

To make an eepsite, follow the I2P [instructions](http://127.0.0.1:7658), but keep in mind that the home directory will apply to the i2p user whose home directory is `/opt/i2p` as shown in the AUR [i2p.install](https://aur.archlinux.org/cgit/aur.git/tree/i2p.install?h=i2p) file.

## See also

*   [I2P Homepage](http://www.i2p2.de)
*   [I2P FAQ](http://www.i2p2.de/faq.html)
*   [I2P Homepage mirror](http://www.i2pproject.net)
*   [I2P on Wikipedia](https://en.wikipedia.org/wiki/I2p "wikipedia:I2p")
*   [i2pd](https://i2pd.website/) - daemon homepage