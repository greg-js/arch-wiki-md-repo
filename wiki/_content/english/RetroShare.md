**RetroShare** – A free software, cross-platform [Friend-to-Friend](https://en.wikipedia.org/wiki/Friend-to-friend "wikipedia:Friend-to-friend") application that offers secure chat and file sharing features.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Retroshare over Tor via hidden service](#Retroshare_over_Tor_via_hidden_service)
        *   [1.1.1 Migrating existing profile to Retroshare-Tor](#Migrating_existing_profile_to_Retroshare-Tor)
*   [2 Usage](#Usage)
    *   [2.1 No friends to add?](#No_friends_to_add.3F)
*   [3 External Links](#External_Links)

## Installation

RetroShare is available in [AUR](/index.php/AUR "AUR") as [retroshare](https://aur.archlinux.org/packages/retroshare/) and [retroshare-git](https://aur.archlinux.org/packages/retroshare-git/).

### Retroshare over Tor via hidden service

1\. [Install](/index.php/Install "Install") [tor](https://www.archlinux.org/packages/?name=tor), enable and start it via [systemctl](/index.php/Systemctl "Systemctl"). Then check it is working correctly ("Bootstrapped 100%: Done"):

```
$ journalctl -f -u tor

```

2\. Edit `/etc/tor/torrc` according to [the Retroshare-Tor generic *nix manual](https://retroshare.readthedocs.io/en/latest/tutorial/tor-hidden-rs-node/#configure-your-hidden-service)

3\. Create the dir for the hidden service according to the manual

4\. Restart tor with systemctl.

5\. Find your onion.address according to the manual

6\. Start Retroshare and follow the [Retroshare-Tor Setup](https://retroshare.readthedocs.io/en/latest/tutorial/tor-hidden-rs-node/#retroshare-tor-setup)

#### Migrating existing profile to Retroshare-Tor

There is currently no way to migrate an existing non-tor-hidden-identity to Retroshare-Tor. If you already created a user before installing tor you can clean the dot-directory of retroshare with

```
$ rm ~/.retroshare

```

## Usage

First, you have to create new profile. Then you need to explicitly add friends to be able to connect to them. In order to connect to your friends you need to exchange your certificates.

### No friends to add?

**Warning:** It is [stongly recommended](https://retroshareteam.wordpress.com/2018/03/13/release-notes-for-v0-6-4/) to use Retroshare-Tor for privacy reasons when connecting to people you don't know and trust IRL.

*   Retroshare-Tor: Use [this onion chatserver](http://ruv6gkdi2p42juij.onion/) with [tor-browser](https://www.archlinux.org/packages/?name=tor-browser) to find new friends
*   Non-Tor (not recommended): Use [this clearnet chatserver](https://retroshare.ch/) to find new friends

## External Links

*   [RetroShare Homepage](http://retroshare.net//)
*   [RetroShare Wikipedia entry](https://en.wikipedia.org/wiki/RetroShare "wikipedia:RetroShare")