[sdcv](https://www.archlinux.org/packages/?name=sdcv) is the console version of the StarDict program that provides console access to dictionaries in StarDict's format

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

There are various places on the web where you can download StarDict dictionaries. Here are some links to get you started:

*   [http://abloz.com/huzheng/stardict-dic/dict.org](http://abloz.com/huzheng/stardict-dic/dict.org)
*   [http://abloz.com/huzheng/stardict-dic/freedict.de](http://abloz.com/huzheng/stardict-dic/freedict.de)
*   [http://abloz.com/huzheng/stardict-dic/mova.org](http://abloz.com/huzheng/stardict-dic/mova.org)
*   [http://abloz.com/huzheng/stardict-dic](http://abloz.com/huzheng/stardict-dic)

Then you can extract the files into `/usr/share/stardict/dic`.

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