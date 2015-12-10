# Moc

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**M**usic **O**n **C**onsole is a lightweight music player which consists of 2 parts, a server (Moc) and a player/interface (Mocp). This is similar to [mpd](/index.php/Mpd "Mpd"), but unlike _mpd_, Moc comes with an interface. Its server does not support remote access.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
*   [4 Last.fm scrobbling](#Last.fm_scrobbling)
    *   [4.1 mocp-scrobbler](#mocp-scrobbler)
*   [5 Front-ends](#Front-ends)
*   [6 systemd service file](#systemd_service_file)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 MOC fails to start](#MOC_fails_to_start)
    *   [7.2 Strange characters](#Strange_characters)
    *   [7.3 FATAL_ERROR: Layout1 is malformed](#FATAL_ERROR:_Layout1_is_malformed)
*   [8 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [moc](https://www.archlinux.org/packages/?name=moc) package. The latest development version is available as [moc-svn](https://aur.archlinux.org/packages/moc-svn/)<sup><small>AUR</small></sup>.

## Configuration

The package includes a sample configuration file at `/usr/share/doc/moc/config.example`. To configure _moc_, copy this file to `~/.moc/config` and edit it.

For instructions about customizing the keybindings, read `/usr/share/doc/moc/keymap.example`.

If you want to use Moc with [OSS](/index.php/OSS "OSS") v4.1, see [OSS#MOC](/index.php/OSS#MOC "OSS").

## Usage

Start _moc_:

```
$ mocp

```

This will start the server and interface. Some useful shortcuts (case sensitive):

<table class="wikitable">

<tbody>

<tr>

<td>Start playing a track</td>

<td>`Enter`</td>

</tr>

<tr>

<td>Pause track</td>

<td>`Space` or `p`</td>

</tr>

<tr>

<td>Play next track</td>

<td>`n`</td>

</tr>

<tr>

<td>Play previous track</td>

<td>`b`</td>

</tr>

<tr>

<td>Switch from playlist browsing to  
filesystem browsing (and vice versa)</td>

<td>`Tab`</td>

</tr>

<tr>

<td>Add one track to the playlist</td>

<td>`a`</td>

</tr>

<tr>

<td>Remove track from playlist</td>

<td>`d`</td>

</tr>

<tr>

<td>Add a folder recursively to playlist</td>

<td>`Shift+a`</td>

</tr>

<tr>

<td>Clear playlist</td>

<td>`Shift+c`</td>

</tr>

<tr>

<td>Increase volume 5%</td>

<td>`.` (dot)</td>

</tr>

<tr>

<td>Decrease volume 5%</td>

<td>`,` (comma)</td>

</tr>

<tr>

<td>Increase volume 1%</td>

<td>`>`</td>

</tr>

<tr>

<td>Decrease volume 1%</td>

<td>`<`</td>

</tr>

<tr>

<td>Change volume to 10%</td>

<td>`meta+1`</td>

</tr>

<tr>

<td>Change volume to 20%</td>

<td>`meta+2`</td>

</tr>

<tr>

<td>Quit player</td>

<td>`q`</td>

</tr>

</tbody>

</table>

**Note:** To shut down the server, use `Shift+q` or:

```
$ mocp -x

```

## Last.fm scrobbling

### mocp-scrobbler

[mocp-scrobbler](https://aur.archlinux.org/packages/mocp-scrobbler/)<sup><small>AUR</small></sup> is a Last.fm/Libre.fm scrobbler for MOC with support for now-playing notifications, daemonization and cache. It only depends on [Python](/index.php/Python "Python") 3.

Copy the example file to your user config directory:

```
mkdir ~/.mocpscrob/
cp /usr/share/doc/mocp-scrobbler/config.example  ~/.mocpscrob/config

```

Edit `~/.mocpscrob/config` to add your login and password. The password variable will be replaced with `password_md5` on the first run. Its value will be the original value hashed using MD5 algorithm. If you want to change password, just add again password with you new password, and `password_md5` will be replaced.

To scrobble tracks, start _mocp-scrobbler_ as daemon before _mocp_. You can also use an [alias](/index.php/Alias "Alias"):

```
alias mocp='/usr/bin/mocp-scrobbler.py -d; mocp'

```

## Front-ends

*   **dmenu_mocp** — Dmenu frontend to MOC

[https://github.com/mutantturkey/mocicon](https://github.com/mutantturkey/mocicon) || [dmenu_mocp](https://aur.archlinux.org/packages/dmenu_mocp/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/dmenu_mocp)]</sup>

*   **mocicon** — GTK panel applet to control MOC

[http://mocicon.sourceforge.net/](http://mocicon.sourceforge.net/) || [mocicon](https://aur.archlinux.org/packages/mocicon/)<sup><small>AUR</small></sup>

*   **moc-tray** — Quick and easy access to mocp basic functions

[https://code.google.com/p/moc-tray/](https://code.google.com/p/moc-tray/) || [moc-tray](https://www.archlinux.org/packages/?name=moc-tray)

*   **eXo** — Qt frontend to MOC, supports scrobbling

[https://bitbucket.org/blaze/exo/](https://bitbucket.org/blaze/exo/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=exo)</small>

## systemd service file

 `/etc/systemd/system/moc@.service` 

```
[Unit]
Description=MOC server
ConditionPathExists=/usr/bin/mocp
After=network.target sound.target

[Service]
RemainAfterExit=yes
User=%I
ExecStart=/usr/bin/mocp -S
ExecStop=/usr/bin/mocp -x
WorkingDirectory=/home/%I/

[Install]
WantedBy=multi-user.target

```

[Enable](/index.php/Enable "Enable") this service for the respective user.

## Troubleshooting

### MOC fails to start

If MOC fails to start, it is most probably because of something wrong in `~/.moc/`. You can try to fix it, or simply delete the whole folder.

### Strange characters

If you see strange-like characters displayed in _moc_ instead of the normal lines (vertical lines to separate space, etc.), you may have a font set incompatible to MOC. Either change the respective font, or edit `.moc/config` to use ASCII for drawing lines:

```
ASCIILines = no

```

### FATAL_ERROR: Layout1 is malformed

If MOC crashes with this error, try adding either line to `.moc/config`:

```
Layout1 = directory(0,0,50%,100%): playlist(50%,0,100%,100%)

```

or

```
Layout1 = directory(0,0,50%,100%): playlist(50%,0,FILL,100%)

```

See [original report](http://moc.daper.net/node/262) and [Debian bugs](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=485059).

## See also

*   [Official documentation](http://moc.daper.net/documentation)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Moc&oldid=407557](https://wiki.archlinux.org/index.php?title=Moc&oldid=407557)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia players](/index.php/Category:Multimedia_players "Category:Multimedia players")