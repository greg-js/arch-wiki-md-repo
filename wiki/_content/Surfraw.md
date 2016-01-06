# Surfraw

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[surfraw](http://surfraw.alioth.debian.org/) provides a fast UNIX command line interface to a variety of popular WWW search engines. Surfraw was originally created by Julian Assange.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 /usr/bin/surfraw: line 487: <url>: No such file or directory](#.2Fusr.2Fbin.2Fsurfraw:_line_487:_.3Curl.3E:_No_such_file_or_directory)

## Installation

[Install](/index.php/Install "Install") the [surfraw](https://www.archlinux.org/packages/?name=surfraw) package.

## Configuration

Surfraw uses the default browser to open the result. The behaviour can be customized via `~/.surfraw.conf`

```
SURFRAW_graphical_browser=/usr/bin/chromium
#SURFRAW_text_browser=/usr/bin/elinks
SURFRAW_graphical=yes

```

## Usage

Surfraw consists of a collection of shell scripts, called elvi, each of which searches a specific web site.

To see the list of elvi type:

```
$ surfraw -elvi

```

You can call surfraw in full, or the shortened form:

```
$ sr duckduckgo _topic_name_

```

You can also add surfraw to your `$PATH` to call the elvi directly.

There are over 100 elvi available for searching the web, e.g. from amazon:

```
$ surfraw amazon -search=books -country=en -q Stanislaw Lem 

```

To search the [AUR](/index.php/AUR "AUR"):

```
sr aur _package_name_

```

To search this wiki:

```
sr archwiki _article_name_

```

For a full list of web site search scripts see: [List of Elvi](http://surfraw.alioth.debian.org/#elvilist)

## Troubleshooting

### /usr/bin/surfraw: line 487: <url>: No such file or directory

If you get a error message like this:

```
$ sr google foo
/usr/bin/surfraw: line 487: http://www.google.com/search?q=foo&num=30: No such file or directory

```

That happens because you haven't specified a browser, and you haven't got Firefox (the default) installed. You can configure your browser in the conf file:

 `~/.config/surfraw/conf`  `SURFRAW_graphical_browser /usr/bin/chromium` 

Retrieved from "[https://wiki.archlinux.org/index.php?title=Surfraw&oldid=414499](https://wiki.archlinux.org/index.php?title=Surfraw&oldid=414499)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Internet applications](/index.php/Category:Internet_applications "Category:Internet applications")
*   [Search](/index.php/Category:Search "Category:Search")