[PyTVShows](https://sourceforge.net/projects/pytvshows/) is a Python script for downloading .torrent files from trvrss.net or eztv.it. The configuration is very easy and PyTVShows remembers the series you already watched.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Running pytvshows](#Running_pytvshows)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [pytvshows](https://aur.archlinux.org/packages/pytvshows/) from the [AUR](/index.php/AUR "AUR").

## Configuration

Create a file named `.pytvshows.cfg` in your home directory.

In this file you are going to fill in your series in this syntax for example south park:

```
#[South+Park]
 episode = x
 season = y

 [Dirty+Jobs]
 episode = 5
 season = 5

```

note that x and y are variables, you can fill in the season and episode number you already have watched like x = 14 & y = 12 also note that + means a whitespace, you must always add this symbol for a whitespace if you do not do that the script will not work.

## Running pytvshows

Now you can start running pytvshows by default the output directory is your ~/ you can change that:

```
# pytvshows --output_dir=/home/<user>/torrents/

```

For more options run:

```
# pytvshows --help

```

Let your bittorent client watch the directory where you download your torrents so they are automatically added.

If you want to run pytvshows in the background, first make a bash script:

```
#!/bin/bash
echo -n “tvshows.sh - “; date # log current date & time 
pytvshows  --output_dir=/home/<user>/torrents/ --verbose >> ~/scripts/pytvshows.log

```

As you can see, log the output of pytvshows.

Then add this script to cron:

```
#crontab -e (as normal user, using pytvshows as root is not recommended)
#30 * * * * /home/<user>/scripts/tvshows.sh 

```

Please use a other time otherwise it will get to many hits at the same time.

## See also

[http://sourceforge.net/projects/pytvshows/](http://sourceforge.net/projects/pytvshows/)