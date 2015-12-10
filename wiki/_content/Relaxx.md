# Relaxx

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

From [RelaXXPlayer - Home of the easy listening mpd client](http://relaxx.dirk-hoeschen.de/):

_AJAX-based web-frontend for the Music Player Daemon (MPD). RelaXX includes features like keyboard-control, drag and drop, context-menus, sortable tracklists and more using JavaScript. Can be used as a public jukebox for MP3 or OGG. The server uses PHP._

## Installation

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** As of PHP 5.2.0, the JSON extension is bundled and compiled into PHP [by default](http://php.net/manual/en/json.installation.php). (Discuss in [Talk:Relaxx#](https://wiki.archlinux.org/index.php/Talk:Relaxx))

RelaXX requires the JSON extension:

```
# pecl install json

```

Edit `/etc/php/php.ini` and add or uncomment the following line to enable the extension:

```
extension=json.so

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Relaxx&oldid=389773](https://wiki.archlinux.org/index.php?title=Relaxx&oldid=389773)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia players](/index.php/Category:Multimedia_players "Category:Multimedia players")