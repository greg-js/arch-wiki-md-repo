Related articles

*   [Audiobook](/index.php/Audiobook "Audiobook")
*   [iPhone tethering](/index.php/IPhone_tethering "IPhone tethering")

The purpose of this article is to demonstrate the use of an **iPad**, **iPod** or **iPhone** with Arch Linux.

## Contents

*   [1 Connecting to a device](#Connecting_to_a_device)
    *   [1.1 Manual mounting](#Manual_mounting)
*   [2 Changing iPod mountpoint](#Changing_iPod_mountpoint)
*   [3 Importing videos and pictures](#Importing_videos_and_pictures)
    *   [3.1 HTML5 videos](#HTML5_videos)
    *   [3.2 Importing pictures and deleting them](#Importing_pictures_and_deleting_them)
*   [4 Converting video for devices](#Converting_video_for_devices)
    *   [4.1 Handbrake](#Handbrake)
    *   [4.2 Avidemux](#Avidemux)
    *   [4.3 Mencoder](#Mencoder)
    *   [4.4 FFmpeg](#FFmpeg)
*   [5 Device specific](#Device_specific)
    *   [5.1 iPhone/iPod Touch](#iPhone.2FiPod_Touch)
        *   [5.1.1 The iFuse Way](#The_iFuse_Way)
        *   [5.1.2 Generating HashInfo file](#Generating_HashInfo_file)
        *   [5.1.3 Unobfuscating the Database](#Unobfuscating_the_Database)
    *   [5.2 iPod Classic/Nano (3rd generation)](#iPod_Classic.2FNano_.283rd_generation.29)
    *   [5.3 iPod Nano 5th generation](#iPod_Nano_5th_generation)
    *   [5.4 iPod Shuffle 1st and 2nd generation](#iPod_Shuffle_1st_and_2nd_generation)
    *   [5.5 iPod Shuffle 4th generation](#iPod_Shuffle_4th_generation)
*   [6 iPod management apps](#iPod_management_apps)
*   [7 See also](#See_also)

## Connecting to a device

Applications which use GVFS, such as some file managers (GNOME Files, Thunar) or media players (Rhythmbox) can interact with iOS devices after [installing](/index.php/Install "Install") the [gvfs-afc](https://www.archlinux.org/packages/?name=gvfs-afc) package. Restarting the file manager or application might be needed. Also confirm that usbmuxd is running in the background if the device is still not being recognized by the file manager or application.

#### Manual mounting

[Install](/index.php/Install "Install") the [ifuse](https://www.archlinux.org/packages/?name=ifuse), [libimobiledevice](https://www.archlinux.org/packages/?name=libimobiledevice) and [ideviceinstaller-git](https://aur.archlinux.org/packages/ideviceinstaller-git/) packages.

Make sure that you have the fuse module loaded by doing `modprobe fuse`, assuming that you do not have it in `/etc/modules-load.d/` already.

**Note:** If your device has a screen password, unlock the device first

Plug in the device and follow the following steps

```
#usbmuxd -f -v
idevice_id -l
ideviceinfo
ideviceinstaller -l

```

The last command will provide the information regarding mounting with Fuse. For example to mount VLC installed on the device one can use the command:

```
#ifuse --documents org.videolan.vlc-ios <mountpoint>

```

The mountpoint field is where you want to have it mounted.

And you are done! You should be able to transfer files.

To unmount:

```
# umount <mountpoint>

```

**Note:** If an error is encountered during mounting, rebooting the device and repeating the steps can be helpful

## Changing iPod mountpoint

Traditional iPods are accessed just like a normal USB storage device containing a vfat file system (in rare cases `hfsplus`), and can be [accessed as such](/index.php/USB_storage_devices "USB storage devices"). See the [USB storage devices](/index.php/USB_storage_devices "USB storage devices") article for detailed instructions.

**Tip:** If you cannot see the vfat file system, it is likely that your iPod is `hfsplus` formatted. For convenience, as Arch kernel is built with no support for that filesystem, you might want to restore your iPod using iTunes on Windows. This will erase all data on your iPod, and format it as a vfat filesystem

If udisks2 is running, it will mount an attached iPod to `/run/media/*$USER*/*iPod_name*`.

If the volume label of your iPod is long, or contains a mixture of spaces, and/or lower-case and capital letters, it may present an inconvenience. You may easily change the volume label for more expedient access using `dosfslabel` from the [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) package:

*   Get and confirm the current volume label:

```
# dosfslabel /dev/sd*XY*

```

*   Set the new volume label:

```
# dosfslabel /dev/sd*XY* ArchPod

```

*   Unmount the device:

```
$ udisksctl unmount -b /dev/sd*XY*

```

*   Mount it again:

```
$ udisksctl mount -b /dev/sd*XY*

```

where `/dev/sdxx` is the current device node of your iPod.

## Importing videos and pictures

Both videos and photos can be found in typically in `*<mountpoint>*/DCIM/100APPLE`.

### HTML5 videos

Typically you want to convert MOV files to a HTML5 video format like OGV using [ffmpeg2theora](https://www.archlinux.org/packages/?name=ffmpeg2theora). Note that the creation date metadata is not in the converted video, so you need to use a script like:

```
#!/usr/bin/sh

find -name "*.MOV" | while read mov
do
    d=$(gst-discoverer-1.0 -v $mov | awk '/datetime:/{print $2}' | tr -d \")
    base=${mov%.*}
    if test -f $base.ogv
    then
        touch -d${d} $base.ogv
        ls -l $base.ogv
    else
        echo $base.ogv missing
    fi
done

```

And use `cp -a` or `rsync -t` in order to preserve the file's date & time.

### Importing pictures and deleting them

You can move photos and videos out of `*<mountpoint>*/DCIM/100APPLE`, however you need to trigger a rebuild of the "Camera Roll" database by deleting the old databases.

```
# rm Photos* com.apple.photos.caches_metadata.plist

```

## Converting video for devices

### Handbrake

[Handbrake](http://handbrake.fr/) is a nifty tool with presets for a variety of iPod versions. CLI and GTK versions are available with the [handbrake-cli](https://www.archlinux.org/packages/?name=handbrake-cli) and [handbrake](https://www.archlinux.org/packages/?name=handbrake) packages respectively.

If you do decide to take the CLI way, a good guide is available at [http://trac.handbrake.fr/wiki/CLIGuide](http://trac.handbrake.fr/wiki/CLIGuide).

### Avidemux

[Install](/index.php/Install "Install") the [avidemux-qt](https://www.archlinux.org/packages/?name=avidemux-qt) package.

This can convert to mp4 files. If you enforce a hard max of bit rate @ 700ish and keep the video size to 720x480 or 320x240 than it works fine for video file exporting.

### Mencoder

[Install](/index.php/Install "Install") the [mplayer](https://www.archlinux.org/packages/?name=mplayer) package.

Has *extremely* comprehensive configuration support, which will be able to spit out iPod-compatible video files. Check out [mencoder(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mencoder.1); a lot of MPlayer opts will also affect encoding.

A basic guide is also available at [MEncoder](/index.php/MEncoder "MEncoder").

An example command to encode iPhone/iPod Touch-compatible video:

```
mencoder INPUT -o output.mp4 \
-vf scale=480:-10,harddup \
-oac faac -faacopts mpeg=4:object=2:raw:br=128 \
-of lavf -lavfopts format=mp4 \
-ovc x264 -x264encopts nocabac:level_idc=30:bframes=0

```

### FFmpeg

[Install](/index.php/Install "Install") the [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) package.

Another encoder with comprehensive configuration support. Example command to encode for 5G iPod:

```
$ ffmpeg -vcodec xvid -b 300 -qmin 3 -qmax 5 -bufsize 4096 \
-g 300 -acodec aac -ab 96 -i INPUT -s 320x240 \
-aspect 4:3 output.mp4

```

or iPod Touch/iPhone compatible video output:

```
$ ffmpeg -f mp4 -vcodec mpeg4 -maxrate 1000 -b 700 -qmin 3 -qmax 5\
-bufsize 4096 -g 300 -acodec aac -ab 192 -s 480×320 -aspect 4:3 -i INPUT output.mp4

```

## Device specific

### iPhone/iPod Touch

By default, neither the iPhone nor the iPod Touch present mass storage capability over USB, though there is a solution for accessing your files.

The proposed solution is to use a FUSE file system called [ifuse](https://www.archlinux.org/packages/?name=ifuse), which allows you to mount your device through USB, as you normally would. After installing ifuse, for instance, you should see your iPhone appear in the left navigation of Gnome Files and other supporting file managers.

**Tip:** You can also use other [#iPod management apps](#iPod_management_apps) to transfer pictures and music.

Refer to this page:[[1]](https://help.ubuntu.com/community/PortableDevices/iPhone)

#### The iFuse Way

**Note:** If your device has a screen password, one must unlock the device to gain access through the USB interface.

[Install](/index.php/Install "Install") the [ifuse](https://www.archlinux.org/packages/?name=ifuse) package.

Now make sure that you have the fuse module loaded by doing `modprobe fuse`, assuming that you do not have it in `/etc/modules-load.d/` already.

You can now mount your device. Make sure it is unlocked before you plug it in, or it will not be recognized.

```
# ifuse <mountpoint>

```

The mountpoint field is where you want to have it mounted.

And you are done! You should be able to point your syncing software of choice to the mount point and be able to transfer files.

To unmount your device:

```
# umount <mountpoint>

```

#### Generating HashInfo file

If you have not previously synced your device using iTunes specifically, you will get error messages telling you that the HashInfo file is missing. This can be fixed by making an iTunes installation on MacOS or Windows create it (by plugging in the iPod there). Alternatively you can create this file yourself, instructions can be found on [this website](http://ihash.marcansoft.com/).

#### Unobfuscating the Database

Since firmware version 2.0, Apple has obfuscated the music database. If you are using recent firmware, the file `/System/Library/Lockdown/Checkpoint.xml` can be modified to enable use of the older, non-obfuscated database. If that file doesn't exist then try to copy from `/System/Library/CoreServices/Checkpoint.xml` to `/System/Library/Lockdown/Checkpoint.xml` then replace:

```
<key>DBVersion</key>
<integer>4</integer>

```

with:

```
<key>DBVersion</key>
<integer>2</integer>

```

Then reboot your device.

If syncing fails with "ERROR: Unsupported checksum type '0' in cbk file generation!", you may need to leave this at 4\. libgpod seems to [expect a hashed database.](http://gitorious.org/libgpod/libgpod/blobs/b9b83dc8b6c3d1f0c53ed32f05279ca838d54e02/src/itdb_sqlite.c#line2064)

### iPod Classic/Nano (3rd generation)

You need to set up the iPod to make libgpod able to find its Firewire ID. For this, you will need to get your FireWire ID manually

1) Mount the iPod as a rw mount point. In the following example, I will use `/mnt/ipod`.

2 ) Find the serial number by typing

```
# lsusb -v | grep -i Serial 

```

this should print a 16 character long string like 00A1234567891231 (it will have no colons or hyphens)

3) Once you have that number, create or edit `/mnt/ipod/iPod_Control/Device/SysInfo`. Add to that file the line below:

```
  FirewireGuid: 0xffffffffffffffff

```

(replace ffffffffffffffff with the 16 digit string you obtained at the previous step and do not forget the leading 0x before the string)

Your iPod can now be managed with Amarok or gtkpod.

### iPod Nano 5th generation

Follow the instructions below in order to set up the FirewireID then go to following URL – [http://ihash.marcansoft.com/](http://ihash.marcansoft.com/) – and enter the serial number (the one used in the previous step) on the website. It will generate a file (named *HashInfo*) which you will place under the iPod_Control/Device/ directory. Unplug the iPod device and plug it back.

All credits go to [https://wired-news.blogspot.it/2012/09/ipod-nano-5g-synchronization-issues-in.html](https://wired-news.blogspot.it/2012/09/ipod-nano-5g-synchronization-issues-in.html)

**Note:** I tried to follow the above 3rd generation instructions but they were not enough. I don't know if this further step is needed also for the above mentioned iPod.

### iPod Shuffle 1st and 2nd generation

Due to the simple structure of the Shuffle (compared to the "big" iPods), it is possible to use the player almost like any other USB flash MP3 player. What is necessary is [rebuild_db.py](http://sourceforge.net/projects/shuffle-db/files/latest/download) file stored in the iPod's root directory. Simply copy MP3 files onto the iPod Shuffle (sub-folders are allowed too) and run:

```
$ python2 /path/to/rebuild_db.py

```

[Source](http://shuffle-db.sourceforge.net/)

### iPod Shuffle 4th generation

In order to use this version of the iPod Shuffle under linux, you can use the python based command line tool [ipod-shuffle-4g](https://aur.archlinux.org/packages/ipod-shuffle-4g/). It also provides advanced voiceover and (auto)playlist generation support.

## iPod management apps

*   [Rhythmbox](http://wiki.gnome.org/Apps/Rhythmbox)
    *   GTK interface ([GNOME](/index.php/GNOME "GNOME"))
    *   Is part of the official GNOME projects.
    *   Fast, light interface.
    *   Manage music on your computer and iPod
    *   Download or stream podcasts and video podcasts
    *   Queue up songs and podcasts
    *   Last.fm integration
    *   Live radio stations
    *   Jamendo and Magnatune support
    *   Audio CD burning
    *   Album cover display
    *   Song lyrics display
    *   DAAP sharing

*   [Banshee](http://banshee.fm)
    *   GTK interface (GNOME)
    *   Uses Mono so it is slower and more resource hogging than rhythmbox
    *   Device Sync: Sync your music and videos to your Android, iPod, or other device - or import its media
    *   Podcasts: Download or stream podcasts and video podcasts
    *   Play Queue: Queue up songs, videos, and podcasts, or let the Auto DJ take over
    *   Shuffle Modes: Shuffle (or Auto DJ) by artist, album, rating, or even songs' acoustic similarity
    *   Album Art: Artwork is automatically fetched as you listen
    *   Powerful Search, Smart Playlists: Find exactly what you want, fast
    *   Video Support: All the power of Banshee, now for your videos

*   [Yamipod](http://www.yamipod.com)
    *   GTK interface (GNOME)
    *   super lightweight application for managing ONLY music on your iPod (not on your computer)
    *   easy ratings edit
    *   PC to iPod synchronization
    *   News RSS and podcasts to iPod upload
    *   Last.fm support
    *   playlist support

*   [GTKPod](http://www.gtkpod.org/libgpod/)
    *   GTK interface (GNOME)
    *   Read your existing iTunesDB (i.e. import the existing contents of your iPod including play counts, ratings and on-the-go playlists).
    *   Add MP3, WAV, M4A (non-protected AAC), M4B (audio book), podcasts, and various video files (single files, directories or existing playlists) to the **iPod. You need a third party product to download podcasts, like 'bashpodder' or 'gpodder'
    *   View, add and modify Cover Art
    *   Browse the contents of your local hard disk by album/artist/genre by adding all your songs to the 'local' database. From there the tracks can be **dragged over to the iPod/Shuffle easily.
    *   Create and modify playlists, including smart playlists.
    *   You can choose the charset the ID3 tags are encoded in from within gtkpod. The default is the charset currently used by your locale setting.
    *   Extract tag information (artist, album, title...) from the filename if you supply a template.
    *   Detect duplicates when adding songs (optional).
    *   Remove and export tracks from your iPod.
    *   Modify ID3 tags -- changes are also updated in the original file (optional).
    *   Refresh ID3 tags from file (if you have changed the tags in the original file).
    *   Sync directories.
    *   Normalize the volume of your tracks (uses mp3gain or the replay-gain tag)
    *   Write the updated iTunesDB and added songs to your iPod.
    *   Work offline and synchronize your new playlists / songs with the iPod at a later time.
    *   Export your korganizer/kaddressbook/Thunderbird/evocalendar/evolution/webcalendar... data to the iPod (scripts for other programs can be added).

*   [Floola](http://www.floola.com)
    *   GTK interface (GNOME)

*   [Amarok](http://amarok.kde.org/)
    *   KDE/qt interface

*   [qPod](http://qpod.sourceforge.net)
    *   KDE/qt interface
    *   front-end for GNUpod

*   [GNUpod](http://www.gnu.org/software/gnupod/)
    *   command-line only

*   [jakpod](http://www.jakpod.de/)
    *   JakPod is based on Java and allows you to copy music and video files to your iPod.
    *   iPod Nano 6th support
    *   [jakpod](https://aur.archlinux.org/packages/jakpod/)

## See also

*   [More information about iPhone/iPod Touch support](http://help.ubuntu.com/community/PortableDevices/iPhone)
*   [Apple trailers downloader script](http://wiki.gotux.net/code/perl/atget)