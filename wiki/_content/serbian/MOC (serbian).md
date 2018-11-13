## Contents

*   [1 Opis](#Opis)
*   [2 Instalacija](#Instalacija)
*   [3 Konfigurisanje](#Konfigurisanje)
*   [4 Korišćenje](#Korišćenje)
*   [5 Razvojna verzija](#Razvojna_verzija)
*   [6 MOC + last.fm](#MOC_+_last.fm)
*   [7 Frontends](#Frontends)

## Opis

**M**usic **O**n **C**onsole is a lightweight music player. It consists of 2 parts, a server (Moc) and the player/interface (Mocp). This is similar to [mpd](/index.php/Mpd "Mpd"), but unlike mpd, Moc comes with an interface.

## Instalacija

Sync and install with pacman:

```
# pacman -S moc

```

## Konfigurisanje

The package includes a sample configuration file at `/usr/share/doc/moc/config.example`. To configure moc, copy this file to `~/.moc/config` and edit it.

For instructions about customising the keybindings, read `/usr/share/doc/moc/keymap.example`.

If you want to use Moc with [OSS](/index.php/OSS "OSS") v4.1, see [OSS#MOC](/index.php/OSS#MOC "OSS").

## Korišćenje

To start moc:

```
$ mocp

```

This will start the server and interface. You will enter player interface. Some useful shortcuts to use mocp (case sensitive):

| Start playing a track | Enter |
| Pause track | Space or p |
| Play next track | n |
| Play previous track | b |
| Switch from playlist browsing to filesystem browsing (and vice versa) | tab |
| Add one track to the playlist | a |
| Remove track from playlist | d |
| Add a folder recursively to playlist | A |
| Clear playlist | C |
| Increase volume 5% | . (dot) |
| Decrease volume 5% | , (comma) |
| Increase volume 1% | > |
| Decrease volume 1% | < |
| Change volume to 10% | meta + 1 |
| Change volume to 20% | meta + 2 |
| etc, etc... |
| Quit player | q |

NOTE: To shut down the server, use the shift (capital) Q key or:

```
$ mocp -x

```

## Razvojna verzija

You can obtain these from the AUR. MOC 2.4.0 (stable) was released in 2006\. Features since then are in 2.5, but are not yet blessed “stable” as of writing.

*   [moc-svn](https://aur.archlinux.org/packages/moc-svn/)
*   [moc-devel](https://aur.archlinux.org/packages/moc-devel/) (alpha version for next release)

## MOC + last.fm

If you want scrobble songs to last.fm you need moc >= 2.5.0\. See [#Unstable versions](#Unstable_versions) above.

First install lastfmsubmitd. It is a daemon which is available in the "community" repository. To install it, first edit `/etc/lastfmsubmitd.conf` and add both `lastfmsubmitd` and `lastmp` to the `DAEMONS` array in `/etc/rc.conf`.

Now configure moc:

```
$ vim ~/.moc/config

```

add line:

```
OnSongChange = "/usr/lib/lastfmsubmitd/lastfmsubmit --artist %a --title %t --length %d --album %b"

```

change permission:

```
$ sudo chmod -R 777 /var/spool/lastfm

```

thats all.

## Frontends

[dmenu_mocp](https://aur.archlinux.org/packages/dmenu_mocp/) is a dmenu frontend for moc

[moc-tray](https://www.archlinux.org/packages/?name=moc-tray) is a perl gtk dock that gives you access to moc functions