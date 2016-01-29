# lariza

[lariza](https://github.com/vain/lariza/) is a simple web browser using GTK+ 2, GLib and WebKitGTK+. Its features include adblocking, keyword-based searching, a download manager and global content zoom. It provides built-in launching of suckless' [tabbed](https://www.archlinux.org/packages/?name=tabbed) to create tabs with instances of lariza. Additionally it supports the XEmbed protocol which makes it possible to embed it in another application.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Environment variables](#Environment_variables)
    *   [2.2 Adblock](#Adblock)
    *   [2.3 Keyword based searching:](#Keyword_based_searching:)
*   [3 Using lariza](#Using_lariza)
*   [4 See also](#See_also)

## Installation

lariza is available on [github](https://github.com/vain/lariza/).

To build lariza, do the following:

```
$ git clone [https://github.com/vain/lariza.git](https://github.com/vain/lariza.git)
$ cd lariza && make

```

Also make sure you install [tabbed](https://www.archlinux.org/packages/?name=tabbed) if you want to use lariza in tabs in one window. An alternative is to use a windowmanager which supports tabbing - like [i3](/index.php/I3 "I3"), [PekWM](/index.php/PekWM "PekWM") or [fluxbox](/index.php/Fluxbox "Fluxbox").

## Configuration

### Environment variables

You can customize some settings by using environment variables in your shell's rc file:

```
export LARIZA_ACCEPTED_LANGUAGE=en-US # set Accepted-Language header
export LARIZA_DOWNLOAD_DIR=/home/myUser/dump # download directory
export LARIZA_ZOOM=1.0 # default zoom level
export LARIZA_HOME_URI=[https://duckduckgo.com/](https://duckduckgo.com/) # "homepage"

```

### Adblock

Adblock can be configured by creating a file `~/.config/lariza/adblock.black` with regular expressions like this:

```
.*/ad/.*
.*/ads/.*
^https?://ad.*
^https?://advert.*
^https?://.*\.advertising\.com/

```

Lines starting with "#" are ignored.

### Keyword based searching:

Keyword based searching can be configured by creating a file `~/.config/lariza/keywordsearch` with expressions like this:

```
du [https://duckduckgo.com/?q=%s](https://duckduckgo.com/?q=%s)
wi [https://en.wikipedia.org/w/index.php?title=Special:Search&search=%s](https://en.wikipedia.org/w/index.php?title=Special:Search&search=%s)
go [https://www.google.de/?gws_rd=ssl#q=%s](https://www.google.de/?gws_rd=ssl#q=%s)
yt [http://www.youtube.com/results?search_query=%s](http://www.youtube.com/results?search_query=%s)

```

Each line consists of a keyword and a URI to be used for searching. So if you type "go archlinux" into the address box, it will use Google to search for "archlinux" by using the URI [https://www.google.de/?gws_rd=ssl#q=archlinux](https://www.google.de/?gws_rd=ssl#q=archlinux).

Lines starting with "#" are ignored.

## Using lariza

You can provide multiple URI's to open when starting lariza:

```
$ lariza [https://archlinux.org](https://archlinux.org) [http://google.com](http://google.com)

```

For the complete documentation, please have a look at the github pages.

## See also

*   [Vain's lariza github page](https://github.com/vain/lariza)
*   [page for lariza on Vain's website (german)](http://uninformativ.de/projects/?q=lariza)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lariza&oldid=387901](https://wiki.archlinux.org/index.php?title=Lariza&oldid=387901)"