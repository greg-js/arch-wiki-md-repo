# dvdbackup

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Optical disc drive](/index.php/Optical_disc_drive "Optical disc drive")

There are several ways to backup DVD videos; see [DVD Ripping](/index.php/DVD_Ripping "DVD Ripping"). Many methods are slow, and require several steps to accomplish. [dvdbackup](https://www.archlinux.org/packages/?name=dvdbackup) provides a simpler method (with some help from [dvdauthor](https://www.archlinux.org/packages/?name=dvdauthor)). The `dvdbackup` program is elegant because it does not demux/remux/transcode/reformat the movie. This means the backup process is done in one step.

## Contents

*   [1 Installation](#Installation)
*   [2 Examining the DVD](#Examining_the_DVD)
*   [3 Ripping the DVD](#Ripping_the_DVD)
    *   [3.1 A single title](#A_single_title)
    *   [3.2 The main feature](#The_main_feature)
    *   [3.3 The whole DVD](#The_whole_DVD)
*   [4 Writing to disc](#Writing_to_disc)
    *   [4.1 Creating an ISO](#Creating_an_ISO)
    *   [4.2 Burning straight to DVD](#Burning_straight_to_DVD)

## Installation

[Install](/index.php/Install "Install") [dvdbackup](https://www.archlinux.org/packages/?name=dvdbackup) from the [official repositories](/index.php/Official_repositories "Official repositories").

[dvdauthor](https://www.archlinux.org/packages/?name=dvdauthor) is available in the official repositories, but it is only required if backing up specific titles or title sets.

[libdvdcss](https://www.archlinux.org/packages/?name=libdvdcss) is available in the official repositories and is required to read encrypted DVDs.

## Examining the DVD

First, determine which title to backup. The following command retrieves information about the DVD:

```
$ dvdbackup -i /dev/dvd -I

```

After some less useful information, `dvdbackup` will display something similar to the following:

```
$ dvdbackup -i /dev/sr0 -I

```

```
[...]

Main feature:
	Title set containing the main feature is  1
	The aspect ratio of the main feature is 16:9
	The main feature has 1 angle(s)
	The main feature has 1 audio_track(s)
	The main feature has 2 subpicture channel(s)
	The main feature has a maximum of 28 chapter(s) in on of it's titles
	The main feature has a maximum of 6 audio channel(s) in on of it's titles

```

This indicates that the main feature is in title set 1\. Next a list of title sets is displayed:

```
$ dvdbackup -i /dev/sr0 -I

```

```
[...]

Title Sets:

	Title set 1
		The aspect ratio of title set 1 is 16:9
		Title set 1 has 1 angle(s)
		Title set 1 has 1 audio_track(s)
		Title set 1 has 2 subpicture channel(s)

		Titles included in title set 1 is/are
			Title 1:
				Title 1 has 28 chapter(s)
				Title 1 has 6 audio channle(s)

```

The main feature in this example is title 1\. Sometimes a title set will include more than one title, sometimes not. Title sets can also include menus, which will no longer work if not backing up the entire DVD.

## Ripping the DVD

**Tip:** `dvdbackup` reads the name of the DVD and creates a working directory for it. If `dvdbackup` decides the name of the DVD is too generic (like "MOVIE", for instance), the user must specify a name, as it will refuse to run otherwise. Just use `-n _movie_name_` to specify.

**Note:** If you receive an error such as "`ERR: no video format specified for VMGM`" you must set the video format variable. An easy way to do this is to add `export VIDEO_FORMAT=NTSC` (for NTSC regions) to your `~/.bashrc`.

### A single title

The `-t` option allows you to extract a specific title:

```
$ dvdbackup -i /dev/dvd -o ~ -t 1

```

You will now see a number of VOB files on the hard drive (in `~/_movie_name_/VIDEO_TS`). These files can be played in [MPlayer](/index.php/MPlayer "MPlayer") or [VLC](/index.php/VLC "VLC"), but are insufficient to create a DVD copy. This is where `dvdauthor` is useful.

A title set must now be created (e.g. `VTS_01_0.IFO` and `VTS_01_0.BUP`). Be aware that the following command will make a copy of the entire movie. The original can be deleted right afterwards.

```
$ mkdir ~/dvd
$ cd ~/_movie_name_/VIDEO_TS
$ dvdauthor -t -o ~/dvd *.VOB

```

`dvdauthor` will create a copy of the movie. If it outputs anything like "SCR moves backwards, remultiplex input" there might be trouble. Before deleting any files, check the file sizes of the original VOB files compared to the copied ones. If all roughly the same size, you may be alright. You can use [MPlayer](/index.php/MPlayer "MPlayer") to test the affected VOB files to see if anything is missing.

Now, table of contents files must be created (e.g. `VIDEO_TS.IFO` and `VIDEO_TS.BUP`). This is much less time-consuming, and does not waste hard drive space:

```
$ cd ~/dvd/VIDEO_TS
$ dvdauthor -o ~/dvd -T

```

### The main feature

The `-F` option automatically detects the main feature, though not always correctly, and copies the entire title set:

```
$ dvdbackup -i /dev/dvd -o ~ -F

```

Now, table of contents files must be created (e.g. `VIDEO_TS.IFO` and `VIDEO_TS.BUP`):

```
$ cd ~/_movie_name_/VIDEO_TS
$ dvdauthor -o ~/_movie_name_ -T

```

### The whole DVD

The `-M` option will backup the entire DVD structure, including menus, special features, etc. This requires approximately 7 GB of disk space for most DVDs:

```
$ dvdbackup -i /dev/dvd -o ~ -M

```

## Writing to disc

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Optical Disc Drive](/index.php/Optical_Disc_Drive "Optical Disc Drive").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Dvdbackup#](https://wiki.archlinux.org/index.php/Talk:Dvdbackup))

See [DVD Writing](/index.php/DVD_Writing "DVD Writing").

### Creating an ISO

The advantage of creating the ISO file is that you can test that everything works fine with [MPlayer](/index.php/MPlayer "MPlayer") before continuing. The disadvantage is that the ISO consumes hard drive space.

```
$ mkisofs -dvd-video -udf -o ~/dvd.iso ~/dvd # if a single title was extracted

```

or the following if the whole DVD was extracted:

```
$ mkisofs -dvd-video -udf -o ~/dvd.iso ~/_movie_name_

```

To test the image with [MPlayer](/index.php/MPlayer "MPlayer"), simply:

```
$ mplayer dvd:// -dvd-device ~/dvd.iso

```

If everything seems fine, burn the image:

```
$ growisofs -Z /dev/dvd=~/dvd.iso

```

**Tip:** `growisofs` is part of the [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools) package.

### Burning straight to DVD

If confident in our skills, creating and testing an image is a waste of time and hard drive space! Basically, one can merge the mkisofs with the growisofs command listed above:

```
$ growisofs -dvd-video -udf -Z /dev/dvd ~/dvd # if a single title was extracted

```

or:

```
$ growisofs -dvd-video -udf -Z /dev/dvd ~/_movie_name_

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dvdbackup&oldid=414793](https://wiki.archlinux.org/index.php?title=Dvdbackup&oldid=414793)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia](/index.php/Category:Multimedia "Category:Multimedia")

Hidden category:

*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")