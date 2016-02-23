[Ring](https://ring.cx) is a new peer-to-peer communication solution, offering voice, video and chat in a decentralised and secure way. It is being developed by [Savoir-faire Linux](https://www.savoirfairelinux.com/), a Canadian company specialising in Free Software.

The ancestor of Ring is [SFLphone](https://projects.savoirfairelinux.com/projects/sflphone/wiki), a portable SIP/AIX software phone, also developed by Savoir-faire Linux. Ring retains most of the audio and SIP capabilities of SFLphone, while adding a Bittorrent-like DHT to completely avoid dependency on servers, and offering video and chat communication.

Additionally, Ring has a clean separation between daemon and user interface, and thus several interoperable clients are provided: [Gnome](https://ring.cx/en/documentation/gnulinux-installation), KDE, [Windows](https://ring.cx/en/documentation/windows-installation), [OS X](https://ring.cx/en/documentation/mac-osx-installation), [Android](https://ring.cx/en/documentation/android-installation).

## Installation

**Note:** Remember that as of February 2016, Ring is still in alpha stage. As such, things might break, especially when upgrading.

Ring is currently packaged in the AUR. You can choose between several versions:

*   Gnome client, weekly/monthly snapshot: [ring-gnome](https://aur.archlinux.org/packages/ring-gnome/)
*   Gnome client, latest git version: [ring-gnome-git](https://aur.archlinux.org/packages/ring-gnome-git/)
*   KDE client, latest git version: [ring-kde-git](https://aur.archlinux.org/packages/ring-kde-git/)

These packages will pull the appropriate dependencies ([ring-daemon-git](https://aur.archlinux.org/packages/ring-daemon-git/), [libringclient-git](https://aur.archlinux.org/packages/libringclient-git/) or [ring-daemon](https://aur.archlinux.org/packages/ring-daemon/), [libringclient](https://aur.archlinux.org/packages/libringclient/)).

Whether you want to use the *-git* packages or the "stable" snapshots is up to you. [ring-gnome](https://aur.archlinux.org/packages/ring-gnome/), [ring-daemon](https://aur.archlinux.org/packages/ring-daemon/) and [libringclient](https://aur.archlinux.org/packages/libringclient/) are updated weekly to monthly, and the maintainer checks that everything works fine before uploading the new version to the AUR. *-git* packages, on the other hand, may offer new features, but they may also be broken.

## Usage

You just have to use the launcher provided by your desktop environment, or run the `ring` command as user:

```
$ ring

```

It will detect which client is installed (Gnome or KDE) and run it. The daemon is launched automatically by the clients.

## Upgrading

**Important note:** to upgrade, please make sure that you upgrade **all** dependencies from the AUR at the same time! Otherwise, things will certainly break (API/ABI change).

That is, to upgrade ring-gnome-git or ring-kde-git, also upgrade libringclient-git, ring-daemon-git, and opendht-git.