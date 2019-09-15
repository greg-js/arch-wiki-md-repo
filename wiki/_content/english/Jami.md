[Jami](https://jami.net) (formerly **GNU Ring**) is a peer-to-peer communication solution, offering voice, video and chat in a decentralised and secure way. It is being developed by [Savoir-faire Linux](https://www.savoirfairelinux.com/), a Canadian company specialising in Free Software.

The ancestor of Jami is [SFLphone](https://en.wikipedia.org/wiki/Jami_(software)#History "wikipedia:Jami (software)"), a portable SIP/AIX software phone, also developed by Savoir-faire Linux. Jami retains most of the audio and SIP capabilities of SFLphone, while adding a Bittorrent-like DHT to completely avoid dependency on servers, and offering video and chat communication.

Additionally, Jami has a clean separation between daemon and user interface. The supported platforms are GNU/Linux, Windows, Mac OSX and Android.

## Installation

Jami is currently packaged in [community], with some third-party clients in AUR. You can choose between several versions:

*   official Gnome client, weekly/monthly snapshot: [jami-gnome](https://www.archlinux.org/packages/?name=jami-gnome)
*   unofficial KDE client, stable version: [ring-kde](https://aur.archlinux.org/packages/ring-kde/)
*   Gnome client, latest git version: [ring-gnome-git](https://aur.archlinux.org/packages/ring-gnome-git/)
*   KDE client, latest git version: [ring-kde-git](https://aur.archlinux.org/packages/ring-kde-git/)

## Usage

You can use the `jami` command as user:

```
$ jami

```

It will detect which client is installed (Gnome or KDE) and run it. The daemon is launched automatically by clients.