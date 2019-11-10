[Retroshare](https://retroshare.cc/) is a free software, cross-platform [Friend-to-Friend](https://en.wikipedia.org/wiki/Friend-to-friend "wikipedia:Friend-to-friend") application that offers secure chat and file sharing features.

## Installation

Retroshare is available in the [AUR](/index.php/AUR "AUR") as [retroshare](https://aur.archlinux.org/packages/retroshare/) and [retroshare-git](https://aur.archlinux.org/packages/retroshare-git/).

## Usage

First, you have to create new profile. Then you need to explicitly add friends to be able to connect to them. In order to connect to your friends you need to exchange your certificates.

It is strongly recommended to use Retroshare with Tor for privacy reasons when connecting to people you don't know and trust IRL.

*   Retroshare over Tor: Use [this](http://ruv6gkdi2p42juij.onion/) onion chat server with the [TBB](https://en.wikipedia.org/wiki/Tor_(anonymity_network)#Tor_Browser to find new friends.
*   No Tor (not recommended): Use [this](https://retroshare.ch/) chat server to find new friends.

### Retro-Tor

Since version 0.6.0, Retroshare is able to run over the Tor network, using a Tor hidden service to create a so-called “Hidden node” which IP is not visible even to friends of this node.

To do this install [Tor](/index.php/Tor "Tor") and edit `/etc/tor/torrc` as per the [manual](https://retroshare.readthedocs.io/en/latest/tutorial/tor-hidden-rs-node/#configure-your-hidden-service). Then start the [systemd](/index.php/Systemd "Systemd") service and use `journalctl` to see if it bootstrapped successfully.

There is currently no way to migrate an existing non-Tor identity to Retro-Tor. If you already created a user before installing Tor you can re/move the `~/.retroshare/` directory.

## See also

*   [RetroShare on Wikipedia](https://en.wikipedia.org/wiki/RetroShare "wikipedia:RetroShare")
*   [Release notes about Tor](https://retroshareteam.wordpress.com/2018/03/13/release-notes-for-v0-6-4/)