# quvi

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