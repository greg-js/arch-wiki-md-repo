[Sdcv](https://dushistov.github.io/sdcv/) is a command line dictionary. It provides access to dictionaries in StarDict's format.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Adding dictionaries](#Adding_dictionaries)
*   [4 Tips](#Tips)
    *   [4.1 Alias sdcv](#Alias_sdcv)
*   [5 See Also](#See_Also)

## Installation

[sdcv](https://www.archlinux.org/packages/?name=sdcv) is available from the official repositories

## Usage

[sdcv](https://www.archlinux.org/packages/?name=sdcv) can be started from the command line:

```
sdcv

```

This gives you a 'shell-like' command-line from which you can query the database.

## Adding dictionaries

(You can find a comprehensive post here [[1]](https://askubuntu.com/questions/191125/is-there-an-offline-command-line-dictionary))

Download the dictionary files according to your requirements from the following sources:

- The Collaborative International Dictionary of English (GPL, 35MB, 174222 words) [[2]](https://web.archive.org/web/20140917131745/http://abloz.com/huzheng/stardict-dic/dict.org/stardict-dictd_www.dict.org_gcide-2.4.2.tar.bz2)

- [https://web.archive.org/web/20140428004049/http://abloz.com/huzheng/stardict-dic/misc/](https://web.archive.org/web/20140428004049/http://abloz.com/huzheng/stardict-dic/misc/)

- Free On-Line Dictionary of Computing [[3]](http://foldoc.org/)

- Jargon File - A comprehensive compendium of hacker slang illuminating many aspects of hackish tradition, folklore, and humor[[4]](http://catb.org/jargon/html/online-preface.html)

- GNU Linux English-English Dictionary [[5]](http://abloz.com/huzheng/stardict-dic/misc/stardict-xfardic-gnu-linux-2.4.2.tar.bz2)

Make the directory where sdcv looks for the dictionary:

```
sudo mkdir -p /usr/share/stardict/dic/

```

Then you can extract the files into `/usr/share/stardict/dic`.

If it is a .bz2 file:

```
sudo tar -xvjf downloaded.tar.bz2 -C /usr/share/stardict/dic

```

If it is a .gz file:

```
sudo tar -xvzf downlaoded.tar.gz -C /usr/share/stardict/dic

```

* * *

If you don't have root permissions, you can set the `STARDICT_DATA_DIR` environment variable. A good choice might be:

```
export STARDICT_DATA_DIR=$XDG_DATA_HOME

```

sdcv will look in the `dic` subdirectory so make sure that is created and place your dictionaries inside it

After that, you should be set

## Tips

### Alias sdcv

sdcv isn't a very good name for a terminal command you are likely to use a lot. A good name might be:

```
alias def="/usr/bin/sdcv"

```

## See Also

*   [Official web site](http://sdcv.sourceforge.net/)