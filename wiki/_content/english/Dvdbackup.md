Related articles

*   [Optical disc drive](/index.php/Optical_disc_drive "Optical disc drive")
*   [Rip Audio CDs](/index.php/Rip_Audio_CDs "Rip Audio CDs")

There are several ways to backup DVD videos. The quickest and simplest is to [copy the ISO image](/index.php/Optical_disc_drive#Creating_an_ISO_image_from_a_CD.2C_DVD.2C_or_BD "Optical disc drive") as is. Many other methods are slow, and require several steps to accomplish. [dvdbackup](http://dvdbackup.sourceforge.net/) provides one of the simpler methods to rip a DVD (with some help from [dvdauthor](http://dvdauthor.sourceforge.net/)). It is elegant because it does not demux/remux/transcode/reformat the movie. This means the backup process is done in one step. But it can be tricked into copying much more than necessary by a DVD reporting incorrect size data.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Examining the DVD](#Examining_the_DVD)
*   [3 Ripping the DVD](#Ripping_the_DVD)
    *   [3.1 A single title](#A_single_title)
    *   [3.2 The main feature](#The_main_feature)
    *   [3.3 The whole DVD](#The_whole_DVD)
*   [4 Shrinking the DVD](#Shrinking_the_DVD)
*   [5 Writing to disc](#Writing_to_disc)
    *   [5.1 Creating an ISO](#Creating_an_ISO)
    *   [5.2 Burning straight to DVD](#Burning_straight_to_DVD)

## Installation

[Install](/index.php/Install "Install") the [dvdbackup](https://www.archlinux.org/packages/?name=dvdbackup) package. [libdvdcss](https://www.archlinux.org/packages/?name=libdvdcss) is required to read encrypted DVDs. [dvdauthor](https://www.archlinux.org/packages/?name=dvdauthor) is only required if backing up specific titles or title sets.

## Examining the DVD

First, determine which title to backup. The following command retrieves information about the DVD:

```
$ dvdbackup -i /dev/dvd -I

```

After some less useful information, *dvdbackup* will display something similar to the following:

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

**Tip:** *dvdbackup* reads the name of the DVD and creates a working directory for it. If *dvdbackup* decides the name of the DVD is too generic (like "MOVIE", for instance), the user must specify a name, as it will refuse to run otherwise. Just use `-n *movie_name*` to specify.

**Note:** If you receive an error such as "`ERR: no video format specified for VMGM`" you must set the video format variable. An easy way to do this is to add `export VIDEO_FORMAT=NTSC` (for NTSC regions) to your `~/.bashrc`.

### A single title

The `-t` option allows you to extract a specific title:

```
$ dvdbackup -i /dev/dvd -o ~ -t 1

```

You will now see a number of VOB files on the hard drive (in `~/*movie_name*/VIDEO_TS`). These files can be played in [MPlayer](/index.php/MPlayer "MPlayer") or [VLC](/index.php/VLC "VLC"), but are insufficient to create a DVD copy. This is where *dvdauthor* is useful.

A title set must now be created (e.g. `VTS_01_0.IFO` and `VTS_01_0.BUP`). Be aware that the following command will make a copy of the entire movie. The original can be deleted right afterwards.

```
$ mkdir ~/dvd
$ cd ~/*movie_name*/VIDEO_TS
$ dvdauthor -t -o ~/dvd *.VOB

```

*dvdauthor* will create a copy of the movie. If it outputs anything like "SCR moves backwards, remultiplex input" there might be trouble. Before deleting any files, check the file sizes of the original VOB files compared to the copied ones. If all roughly the same size, you may be alright. You can use *mplayer* to test the affected VOB files to see if anything is missing.

Now, table of contents files must be created (e.g. `VIDEO_TS.IFO` and `VIDEO_TS.BUP`). This is much less time-consuming, and does not waste hard drive space:

```
$ cd ~/dvd/VIDEO_TS
$ dvdauthor -o ~/dvd -T

```

### The main feature

The `-F` option automatically detects the main feature (though not always correctly) and copies the entire title set:

```
$ dvdbackup -i /dev/dvd -o ~ -F

```

Now, table of contents files must be created (e.g. `VIDEO_TS.IFO` and `VIDEO_TS.BUP`):

```
$ cd ~/*movie_name*/VIDEO_TS
$ dvdauthor -o ~/*movie_name* -T

```

### The whole DVD

The `-M` option will backup the entire DVD structure, including menus, special features, etc. This requires approximately 7 GB of disk space for most DVDs:

```
$ dvdbackup -i /dev/dvd -o ~ -M

```

## Shrinking the DVD

If the movie needs to fit on a 4.7 GB single layer dvd, [vamps](https://www.archlinux.org/packages/?name=vamps) can be used to shrink it down to size. First, rip the main title and concatenate the vobs into one file.

```
$ dvdbackup -t 1 
$ cat ./movie/VIDEO_TS/*.VOB > ./movie.vob

```

Calculate the shrink factor for *vamps*. Divide the size of your vob file by the size of your writable media and round up.

```
$ du -BMB movie.vob
$ echo '5376 / 4707' | bc -l  #If your vob is 5376 MB

```

Run *vamps*, `-a` selects the audio stream. Running `ffprobe movie.vob` beforehand might help determine which stream to select.

```
$ vamps -E 1.15 -a 1 < movie.vob > movie.dvd5.vob

```

Author the dvd with [dvdauthor](https://www.archlinux.org/packages/?name=dvdauthor):

```
$ dvdauthor -t -o ./author movie.dvd5.vob
$ dvdauthor -T -o ./author

```

## Writing to disc

See [DVD Writing](/index.php/DVD_Writing "DVD Writing").

### Creating an ISO

The advantage of creating the ISO file is that you can test that everything works fine with *mplayer* before continuing. The disadvantage is that the ISO consumes hard drive space.

```
$ mkisofs -dvd-video -udf -o ~/dvd.iso ~/dvd # if a single title was extracted

```

or the following if the whole DVD was extracted:

```
$ mkisofs -dvd-video -udf -o ~/dvd.iso ~/*movie_name*

```

To test the image:

```
$ mplayer dvd:// -dvd-device ~/dvd.iso

```

If everything seems fine, burn the image:

```
$ growisofs -Z /dev/dvd=~/dvd.iso

```

**Tip:** *growisofs* is part of the [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools) package.

### Burning straight to DVD

Creating and testing an image is a waste of time and hard drive space! Basically, we can merge the *mkisofs* with the *growisofs* command:

```
$ growisofs -dvd-video -udf -Z /dev/dvd ~/dvd # if a single title was extracted

```

or

```
$ growisofs -dvd-video -udf -Z /dev/dvd ~/*movie_name*

```