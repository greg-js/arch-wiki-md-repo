# quvi

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [List of Applications](/index.php/List_of_Applications "List of Applications").**

**Notes:** Doesn't add more information than an entry in the list; usage instructions are documented in the man page and other upstream sources. (Discuss in [Talk:Quvi#](https://wiki.archlinux.org/index.php/Talk:Quvi))

**quvi** parses media stream URLs for Internet applications that would otherwise have to use adobe flash multimedia platform to access the media streams. The typical examples of this are the different media hosts, such as YouTube, for videos that use this "multimedia platform" to deliver their content.

Source: [project home](http://quvi.sourceforge.net/)

## Installation

Install [quvi](https://www.archlinux.org/packages/?name=quvi) from [community](/index.php/Official_repositories "Official repositories").

## Usage

The simplest way to play a video from a URL is to issue

```
 $ quvi "<url>" --exec "mplayer %u"

```

This can be configured as a default behavior by creating

 `~/.quvirc`  `exec = "mplayer %u"` 

## Related links

*   [Quvi homepage](http://quvi.sourceforge.net/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Quvi&oldid=389771](https://wiki.archlinux.org/index.php?title=Quvi&oldid=389771)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia players](/index.php/Category:Multimedia_players "Category:Multimedia players")