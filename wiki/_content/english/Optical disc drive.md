Related articles

*   [Codecs](/index.php/Codecs "Codecs")
*   [MPlayer](/index.php/MPlayer "MPlayer")
*   [dvdbackup](/index.php/Dvdbackup "Dvdbackup")
*   [MEncoder](/index.php/MEncoder "MEncoder")
*   [Blu-ray](/index.php/Blu-ray "Blu-ray")

From [Wikipedia](https://en.wikipedia.org/wiki/Optical_disc_drive "wikipedia:Optical disc drive"):

	In computing, an optical disc drive (ODD) is a disk drive that uses laser light or electromagnetic waves within or near the visible light spectrum as part of the process of reading or writing data to or from optical discs. Some drives can only read from discs, but recent drives are commonly both readers and recorders, also called burners or writers. Compact discs, DVDs, and Blu-ray discs are common types of optical media which can be read and recorded by such drives. Optical drive is the generic name; drives are usually described as "CD" "DVD", or "Blu-ray", followed by "drive", "writer", etc.

## Contents

*   [1 Burning](#Burning)
    *   [1.1 Install burning utilities](#Install_burning_utilities)
    *   [1.2 Making an ISO image from existing files on hard disk](#Making_an_ISO_image_from_existing_files_on_hard_disk)
        *   [1.2.1 Basic options](#Basic_options)
        *   [1.2.2 graft-points](#graft-points)
    *   [1.3 Mounting an ISO image](#Mounting_an_ISO_image)
    *   [1.4 Converting img/ccd to an ISO image](#Converting_img.2Fccd_to_an_ISO_image)
    *   [1.5 Learning the name of your optical drive](#Learning_the_name_of_your_optical_drive)
    *   [1.6 Reading the volume label of a CD or DVD](#Reading_the_volume_label_of_a_CD_or_DVD)
    *   [1.7 Creating an ISO image from a CD, DVD, or BD](#Creating_an_ISO_image_from_a_CD.2C_DVD.2C_or_BD)
    *   [1.8 Erasing CD-RW and DVD-RW](#Erasing_CD-RW_and_DVD-RW)
    *   [1.9 Formatting DVD-RW](#Formatting_DVD-RW)
    *   [1.10 Formatting BD-RE and BD-R](#Formatting_BD-RE_and_BD-R)
    *   [1.11 Burning an ISO image to CD, DVD, or BD](#Burning_an_ISO_image_to_CD.2C_DVD.2C_or_BD)
    *   [1.12 Verifying the burnt ISO image](#Verifying_the_burnt_ISO_image)
    *   [1.13 ISO 9660 and burning on-the-fly](#ISO_9660_and_burning_on-the-fly)
    *   [1.14 Multi-session](#Multi-session)
        *   [1.14.1 Multi-session by cdrecord](#Multi-session_by_cdrecord)
        *   [1.14.2 Multi-session by growisofs](#Multi-session_by_growisofs)
        *   [1.14.3 Multi-session by xorriso](#Multi-session_by_xorriso)
    *   [1.15 BD Defect Management](#BD_Defect_Management)
    *   [1.16 Burning an audio CD](#Burning_an_audio_CD)
    *   [1.17 Burning a BIN/CUE](#Burning_a_BIN.2FCUE)
        *   [1.17.1 TOC/CUE/BIN for mixed-mode disks](#TOC.2FCUE.2FBIN_for_mixed-mode_disks)
    *   [1.18 Burn backend problems](#Burn_backend_problems)
    *   [1.19 Burning CD/DVD/BD with a GUI](#Burning_CD.2FDVD.2FBD_with_a_GUI)
*   [2 Playback](#Playback)
    *   [2.1 CD](#CD)
    *   [2.2 DVD](#DVD)
*   [3 Ripping](#Ripping)
    *   [3.1 CD](#CD_2)
    *   [3.2 DVD-Video](#DVD-Video)
        *   [3.2.1 dvd::rip](#dvd::rip)
    *   [3.3 DVD-Audio](#DVD-Audio)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Brasero fails to normalize audio CD](#Brasero_fails_to_normalize_audio_CD)
    *   [4.2 VLC: Error "... could not open the disc /dev/dvd"](#VLC:_Error_.22..._could_not_open_the_disc_.2Fdev.2Fdvd.22)
    *   [4.3 DVD drive is noisy](#DVD_drive_is_noisy)
    *   [4.4 Playback does not work with new computer (new DVD-Drive)](#Playback_does_not_work_with_new_computer_.28new_DVD-Drive.29)
    *   [4.5 None of the above programs are able to rip/encode a DVD to my hard disk!](#None_of_the_above_programs_are_able_to_rip.2Fencode_a_DVD_to_my_hard_disk.21)
    *   [4.6 GUI program log indicates problems with backend program](#GUI_program_log_indicates_problems_with_backend_program)
        *   [4.6.1 Special case: medium error / write error](#Special_case:_medium_error_.2F_write_error)
    *   [4.7 AHCI](#AHCI)
    *   [4.8 BD-R DL 50GB errors on trying to burn second layer](#BD-R_DL_50GB_errors_on_trying_to_burn_second_layer)
    *   [4.9 Disc tray autocloses](#Disc_tray_autocloses)
*   [5 See also](#See_also)

## Burning

**Warning:** The quality of optical drives and the discs themselves varies greatly. Generally, using a slow burn speed is recommended for reliable burns. If you are experiencing unexpected behaviour from the disc, try burning at the lowest speed supported by your burner.

The burning process of optical disc drives consists of creating or obtaining an image and writing it to an optical medium. The image may in principle be any data file. If you want to mount the resulting medium, then it is usually an ISO 9660 file system image file. Audio and multi-media CDs are often burned from a *.bin* file, under control of a *.toc* file or a *.cue* file which tell the desired track layout.

### Install burning utilities

If you want to use programs with graphical user interface, then follow [#Burning CD/DVD/BD with a GUI](#Burning_CD.2FDVD.2FBD_with_a_GUI).

The programs listed here are command line oriented. They are the back ends which are used by most free GUI programs for CD, DVD, and BD. GUI users might get to them when it comes to troubleshooting or to scripting of burn activities.

You need at least one program for creation of file system images and one program that is able to burn data onto your desired media type.

Available programs for ISO 9660 image creation are:

*   *mkisofs* from [cdrtools](https://www.archlinux.org/packages/?name=cdrtools)
*   *xorriso* and *xorrisofs* from [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

The traditional choice is *mkisofs*.

Available programs for burning to media are:

*   *cdrdao* from [cdrdao](https://www.archlinux.org/packages/?name=cdrdao) (CD only, TOC/CUE/BIN only)
*   *cdrecord* from [cdrtools](https://www.archlinux.org/packages/?name=cdrtools)
*   *cdrskin* from [libburn](https://www.archlinux.org/packages/?name=libburn)
*   *growisofs* from [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools) (DVD and BD only)
*   *xorriso* and *xorrecord* from [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

The traditional choices are *cdrecord* for CD and *growisofs* for DVD and Blu-ray Disk. For writing TOC/CUE/BIN files to CD, install [cdrdao](https://www.archlinux.org/packages/?name=cdrdao).

The free GUI programs for CD, DVD, and BD burning depend on at least one of the above packages.

*xorrisofs* supports the *mkisofs* options which are shown in this document.

*cdrskin* supports the shown *cdrecord* options; *xorrecord* also supports those which do not deal with audio CD.

### Making an ISO image from existing files on hard disk

The simplest way to create an ISO image is to first copy the needed files to one directory, for example: `./for_iso`.

Then generate the image file with *mkisofs*:

```
$ mkisofs -V "*ARCHIVE_2013_07_27*" -J -r -o *isoimage.iso* *./for_iso*

```

Each of those options are explained in the following sections.

#### Basic options

	`-V`

	Specifies the name (that is assigned to) of the file system. The ISO 9660 standard specs impose the limitations of 32-character string length, as well as limiting the characters allowed to sets of: "A" to "Z", "0" to "9", and "_". This volume label will probably show up as mount point if the medium is mounted automatically.

	`-J`

	Enables [Joliet](https://en.wikipedia.org/wiki/Joliet_(file_system) extension, which allocates special space to store file names in Unicode (up to 64 UTF-16 characters for each file).

	`-joliet-long`

	Increases maximum length of file names from 64 to 103 UTF-16 characters in Joliet table. Non-compliant to Joliet specs and not commonly supported.

	`-r`

	Enables [Rock Ridge](https://en.wikipedia.org/wiki/Rock_Ridge "wikipedia:Rock Ridge") extension, which adds POSIX file system semantics to an image, including support of long 255-character filenames and Unix-style file permissions.

	`-o`

	Sets the file path for the resulting ISO image.

#### graft-points

It is also possible to let *mkisofs* to collect files and directories from various paths

```
$ mkisofs -V "*BACKUP_2013_07_27*" -J -r -o *backup_2013_07_27.iso* \
  -graft-points \
  */photos=/home/user/photos \*
  /mail=/home/user/mail \
  /photos/holidays=/home/user/holidays/photos

```

	`-graft-points`

	Enables the recognition of *pathspecs* which consist of a target address in the ISO file system (e.g. `/photos`) and a source address on hard disk (e.g. `/home/user/photos`). Both are separated by a "=" character.

So this example puts the disk directory `/home/user/photos`, `/home/user/mail` and `/home/user/holidays/photos`, respectively in the ISO image as `/photos`, `/mail` and `/photos/holidays`.

Programs *mkisofs* and *xorrisofs* accept the same options. For secure backups, consider using *xorrisofs* with option `--for_backup`, which records eventual ACLs and stores an MD5 checksum for each data file.

See the manuals of the ISO 9660 programs for more info about their options:

*   [mkisofs](http://cdrtools.sourceforge.net/private/man/cdrecord/index.html)
*   [xorrisofs](https://www.gnu.org/software/xorriso/man_1_xorrisofs.html)

### Mounting an ISO image

You can mount an ISO image if you want to browse its files. To mount the ISO image, we can use:

```
# mount -t iso9660 -o ro,loop */path/to/file.iso* */mount-point*

```

Do not forget to unmount the image when your inspection of the image is done:

```
# umount /mount-point

```

See also [Mounting images as user](/index.php/Mounting_images_as_user "Mounting images as user") for mounting without root privileges.

### Converting img/ccd to an ISO image

To convert an `img`/`ccd` image, you can use [ccd2iso](https://www.archlinux.org/packages/?name=ccd2iso):

```
$ ccd2iso *~/image.img* *~/image.iso*

```

### Learning the name of your optical drive

For the remainder of this section the name of your recording device is assumed to be `/dev/sr0`.

Check this by

```
$ cdrecord dev=*/dev/sr0* -checkdrive

```

which should report `Vendor_info` and `Identification` fields of the drive.

If no drive is found, check whether any `/dev/sr*` exist and whether they offer read/write permission (`wr-`) to you or your group. If no `/dev/sr*` exists then try [loading](/index.php/Kernel_modules "Kernel modules") module `sr_mod` manually.

### Reading the volume label of a CD or DVD

If you want to get the name/label of the media, use *dd*:

```
$ dd if=*/dev/sr0* bs=1 skip=32808 count=32

```

### Creating an ISO image from a CD, DVD, or BD

You should determine the size of the ISO file system before copying it to hard disk. Most media types deliver more data than was written to them with the most recent burn run.

Use program *isosize* out of package [util-linux](https://www.archlinux.org/packages/?name=util-linux) to obtain the count of blocks to read:

```
$ blocks=$(isosize -d 2048 */dev/sr0*)

```

Have a look whether the obtained number of blocks is plausible

 `$ echo "That would be $(expr $blocks / 512) MB"` 
```
That would be 589 MB

```

Then copy the determined amount of data from medium to hard disk:

```
$ dd if=*/dev/sr0* of=*isoimage.iso* bs=2048 count=$blocks status=progress

```

Omit `count=$blocks` if you did not determine the size. You will probably get more data than needed. The resulting file will nevertheless be mountable. It should still fit onto a medium of the same type as the medium from which the image was copied.

If the original medium was bootable, then the copy will be a bootable image. You may use it as pseudo CD for a virtual machine or burn it onto optical media which should then become bootable.

### Erasing CD-RW and DVD-RW

Used CD-RW media need to be erased before you can write over the previously recorded data. This is done by

```
$ cdrecord -v dev=*/dev/sr0* blank=fast

```

There are two options for blanking: `blank=fast` and `blank=full`. Full blanking lasts as long as a full write run. It overwrites the payload data on the CD. Nevertheless this should not be considered as securely making those data unreadable. For that purpose, several full write runs with random data are advised.

Alternative commands are:

```
$ cdrskin -v dev=*/dev/sr0* blank=fast
$ xorriso -outdev */dev/sr0* -blank as_needed

```

To erase the DVD-RW use the *dvd+rw-format* utility from [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools):

```
$ dvd+rw-format -blank=fast */dev/sr0*

```

Alternative commands are:

```
$ cdrecord -v dev=*/dev/sr0* blank=fast
$ cdrskin -v dev=*/dev/sr0* blank=deformat_sequential_quickest
$ xorriso -outdev */dev/sr0* -blank deformat_quickest

```

Such fastly blanked DVD-RW are not suitable for multi-session and cannot take input streams of unpredicted length. For that purpose one has to use one of:

```
$ cdrecord -v dev=*/dev/sr0* blank=all
$ dvd+rw-format -blank=full */dev/sr0*
$ cdrskin -v dev=*/dev/sr0* blank=as_needed
$ xorriso -outdev */dev/sr0* -blank as_needed

```

The other media types are either write-once (CD-R, DVD-R, DVD+R, BD-R) or are overwritable without the need for erasing (DVD-RAM, DVD+RW, BD-RE).

### Formatting DVD-RW

Formatted DVD-RW media can be overwritten without previous erasure. So consider to apply once in their life time

```
$ dvd+rw-format -force */dev/sr0*
$ cdrskin -v dev=*/dev/sr0* blank=format_if_needed
$ xorriso -outdev */dev/sr0* -format as_needed

```

Unlike DVD-RAM, DVD+RW, and BD-RE, formatted DVD-RW cannot be used as (slow) hard disk directly, but rather need the mediation of driver pktcdvd. See man pktsetup.

### Formatting BD-RE and BD-R

BD-RE need formatting before first use. This is done automatically by the burn programs when they detect the unformatted state. Nevertheless the size of the payload area can be influenced by expert versions of the format commands shown above for DVD-RW.

BD-R can be used unformatted or formatted. Unformatted they are written with full nominal speed and offer maximum storage capacity. Formatted they get checkread during write operations and bad blocks get replaced by blocks from the Spare Area. This reduces write speed to a half or less of nominal speed. The default sized Spare Area reduces the storage capacity by 768 MiB.

growisofs formats BD-R by default. The others do not. growisofs can be kept from formatting. cdrskin and xorriso can write with full nominal speed on formatted BD-RE or BD-R:

```
 $ growisofs -use-the-force-luke=spare:none ...growisofs.or.mkisofs.options...
 $ cdrskin stream_recording=on ...cdrecord.options...
 $ xorriso -stream_recording on ...xorriso.commands...

```

### Burning an ISO image to CD, DVD, or BD

To burn a readily prepared ISO image file `isoimage.iso` onto an optical medium, run for CD:

```
$ cdrecord -v -sao dev=*/dev/sr0* *isoimage.iso*

```

and for DVD or BD:

```
$ growisofs -dvd-compat -Z */dev/sr0*=*isoimage.iso*

```

**Note:**

*   Make sure that the medium is not mounted when you begin to write to it. Mounting may happen automatically if the medium contains a readable file system. In the best case, it will prevent the burn programs from using the burner device. In the worst case, there will be misburns because read operations disturbed the drive. So if in doubt, do: `# umount /dev/sr0` 
*   *growisofs* has a [small bug](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=713016) with blank BD-R media. It issues an error message after the burning is complete. Programs like *k3b* then believe the whole burn run failed. To prevent this, either
    *   format the blank BD-R by `dvd+rw-format */dev/sr0*` before submitting it to *growisofs*
    *   or use *growisofs* option `-use-the-force-luke=spare:none`

### Verifying the burnt ISO image

You can verify the integrity of the burnt medium to make sure it contains no errors. Always eject the medium and reinsert it before verifying. It will guarantee that not any kernel cache will be used to read the data.

First calculate the MD5 checksum of the original ISO image:

 `$ md5sum isoimage.iso` 
```
 e5643e18e05f5646046bb2e4236986d8 isoimage.iso

```

Next calculate the MD5 checksum of the ISO file system on the medium. Although some media types deliver exactly the same amount of data as have been submitted to the burn program, many others append trailing garbage when being read. So you should restrict reading to the size of the ISO image file.

```
$ blocks=$(expr $(du -b isoimage.iso | awk '{print $1}') / 2048)

```
 `$ dd if=/dev/sr0 bs=2048 count=$blocks | md5sum` 
```
 43992+0 records in
 43992+0 records out
 90095616 bytes (90 MB) copied, 0.359539 s, 251 MB/s
 e5643e18e05f5646046bb2e4236986d8  -

```

Both runs should yield the same MD5 checksum (here: `e5643e18e05f5646046bb2e4236986d8`). If they do not, you will probably also get an I/O error message from the `dd` run. `dmesg` might then tell about SCSI errors and block numbers, if you are interested.

### ISO 9660 and burning on-the-fly

It is not necessary to store an emerging ISO file system on hard disk before writing it to optical media. Only very old CD drives at very old computers could suffer failed burns due to empty drive buffer.

If you omit option `-o` from *mkisofs* then it writes the ISO image to standard output. This can be piped into the standard input of burn programs.

```
$ mkisofs -V "ARCHIVE_2013_07_27" -J -r ./for_iso | \
  cdrecord -v dev=/dev/sr0 -waiti -

```

Option `-waiti` is not really needed here. It prevents *cdrecord* from writing to the medium before *mkisofs* starts its output. This would allow *mkisofs* to read the medium without disturbing an already started burn run. See next section about multi-session.

On DVD and BD, you may let *growisofs* operate *mkisofs* for you and burn its output on-the-fly

```
$ growisofs -Z */dev/sr0* -V "*ARCHIVE_2013_07_27*" -r -J *./for_iso*

```

### Multi-session

ISO 9660 multi-session means that a medium with readable file system is still writable at its first unused block address, and that a new ISO directory tree gets written to this unused part. The new tree is accompanied by the content blocks of newly added or overwritten data files. The blocks of data files, which shall stay as in the old ISO tree, will not be written again.

Linux and many other operating systems will mount the directory tree in the last session on the medium. This youngest tree will normally show the files of the older sessions, too.

#### Multi-session by cdrecord

CD-R and CD-RW stay writable (aka "appendable") if cdrecord option `-multi` was used

```
$ cdrecord -v -multi dev=*/dev/sr0* *isoimage.iso*

```

Then the medium can be inquired for the parameters of the next session

```
$ m=$(cdrecord dev=*/dev/sr0* -msinfo)

```

By help of these parameters and of the readable medium in the drive you can produce the add-on ISO session

```
$ mkisofs -M */dev/sr0* -C "$m" \
   -V "*ARCHIVE_2013_07_28*" -J -r -o *session2.iso* *./more_for_iso*

```

Finally append the session to the medium and keep it appendable again

```
$ cdrecord -v -multi dev=*/dev/sr0* *session2.iso*

```

Programs *cdrskin* and *xorrecord* do this too with DVD-R, DVD+R, BD-R and unformatted DVD-RW. Program *cdrecord* does multi-session with at least DVD-R and DVD-RW. They all do with CD-R and CD-RW, of course.

Most re-usable media types do not record a session history that would be recognizable for a mounting kernel. But with ISO 9660 it is possible to achieve the multi-session effect even on those media.

*growisofs* and *xorriso* can do this and hide most of the complexity.

#### Multi-session by growisofs

By default, *growisofs* uses *mkisofs* as a backend for creating ISO images forwards most of its program arguments to . See above examples of *mkisofs*. It bans option `-o` and deprecates option `-C`. By default it uses the *mkisofs*. You may specify to use one of the others compatible backend program by setting environment variable `MKISOFS`:

```
$ export MKISOFS="xorrisofs"

```

The wish to begin with a new ISO file system on the optical medium is expressed by option `-Z`

```
$ growisofs -Z */dev/sr0* -V "*ARCHIVE_2013_07_27*" -r -J *./for_iso*

```

The wish to append more files as new session to an existing ISO file system is expressed by option `-M`

```
$ growisofs -M */dev/sr0* -V "*ARCHIVE_2013_07_28*" -r -J *./more_for_iso*

```

For details see the [growisofs(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/growisofs.1) manual and the manuals of *mkisofs* and *xorrisofs*.

#### Multi-session by xorriso

*xorriso* learns the wish to begin with a new ISO file system from the blank state of the medium. So it is appropriate to blank it if it contains data. The command `-blank as_needed` applies to all kinds of re-usable media and even to ISO images in data files on hard disk. It does not cause error if applied to a blank write-once medium.

```
$ xorriso -outdev */dev/sr0* -blank as_needed \
          -volid "*ARCHIVE_2013_07_27*" -joliet on -add *./for_iso* --

```

On non-blank writable media *xorriso* appends the newly given disk files if command `-dev` is used rather than `-outdev`. Of course, no command `-blank` should be given here

```
$ xorriso -dev */dev/sr0* \
          -volid "*ARCHIVE_2013_07_28*" -joliet on -add *./more_for_iso* --

```

For details see the [manual page](https://www.gnu.org/software/xorriso/man_1_xorriso.html) and especially its [examples](https://www.gnu.org/software/xorriso/man_1_xorriso.html#EXAMPLES)

### BD Defect Management

BD-RE and formatted BD-R media are normally written with enabled Defect Management. This feature reads the written blocks while they are still stored in the drive buffer. In case of poor read quality the blocks get written again or redirected to the *Spare Area* where the data get stored in replacement blocks.

This checkreading reduces write speed to at most half of the nominal speed of drive and BD medium. Sometimes it is even worse. Heavy use of the Spare Area causes long delays during read operations. So Defect Management is not always desirable.

*cdrecord* does not format BD-R. It has no means to prevent Defect Management on BD-RE media, though.

*growisofs* formats BD-R by default. The Defect Management can be prevented by option `-use-the-force-luke=spare:none`. It has no means to prevent Defect Management on BD-RE media, though.

*cdrskin*, *xorriso* and *xorrecord* do not format BD-R by default. They do with `cdrskin blank=format_if_needed`, resp. `xorriso -format as_needed`, resp. `xorrecord blank=format_overwrite`. These three programs can disable Defect Management with BD-RE and already formatted BD-R by `cdrskin stream_recording=on`, resp. `xorriso -stream_recording on`, resp. `xorrecord stream_recording=on`.

### Burning an audio CD

Create your audio tracks and store them as uncompressed, 16-bit, stereo WAV files. To convert MP3 to WAV, ensure [lame](https://www.archlinux.org/packages/?name=lame) is installed, *cd* to the directory with your MP3 files, and run:

```
$ for i in *.mp3; do lame --decode "$i" "$(basename "$i" .mp3)".wav; done

```

In case you get an error when trying to burn WAV files converted with LAME, try decoding with [mpg123](https://www.archlinux.org/packages/?name=mpg123):

```
$ for i in *.mp3; do mpg123 --rate 44100 --stereo --buffer 3072 --resync -w $(basename $i .mp3).wav $i; done

```

To convert AAC to WAV ensure [faad2](https://www.archlinux.org/packages/?name=faad2) is installed and run:

```
$ for i in *.m4a; do faad $i; done

```

Name the audio files in a manner that will cause them to be listed in the desired track order when listed alphabetically, such as `01.wav`, `02.wav`, `03.wav`, etc. Use the following command to simulate burning the WAV files as an audio CD:

```
$ cdrecord **-dummy** -v -pad speed=1 dev=*/dev/sr0* -dao -swab *.wav

```

If everything worked, you can remove the `dummy` flag to actually burn the CD.

To test the new audio CD, use [MPlayer](/index.php/MPlayer "MPlayer"):

```
$ mplayer cdda://

```

### Burning a BIN/CUE

To burn a BIN/CUE image run:

```
$ cdrdao write --device */dev/sr0* *image.cue*

```

#### TOC/CUE/BIN for mixed-mode disks

ISO images only store a single data track. If you want to create an image of a mixed-mode disk (data track with multiple audio tracks) then you need to make a TOC/BIN pair:

```
$ cdrdao read-cd --read-raw --datafile *image.bin* --driver generic-mmc:0x20000 --device */dev/cdrom* *image.toc*

```

Some software only likes CUE/BIN pair, you can make a CUE sheet with *toc2cue* (part of [cdrdao](https://www.archlinux.org/packages/?name=cdrdao)):

```
$ toc2cue *image.toc* *image.cue*

```

### Burn backend problems

If you're experiencing problems, you may ask for advise at mailing list [cdwrite@other.debian.org](mailto:cdwrite@other.debian.org), or try to write to the one of support mail addresses if some are listed near the end of the program's man page.

Tell the command lines you tried, the medium type (e.g. CD-R, DVD+RW, ...), and the symptoms of failure (program messages, disappointed user expectation, ...). You will possibly get asked to obtain the newest release or development version of the affected program and to make test runs. But the answer might as well be, that your drive dislikes the particular medium.

### Burning CD/DVD/BD with a GUI

There are several applications available to burn CDs in a graphical environment.

See also [Wikipedia:Comparison of disc authoring software](https://en.wikipedia.org/wiki/Comparison_of_disc_authoring_software "wikipedia:Comparison of disc authoring software").

*   **[AcetoneISO](https://en.wikipedia.org/wiki/AcetoneISO "wikipedia:AcetoneISO")** — All-in-one ISO tool (supports BIN, MDF, NRG, IMG, DAA, DMG, CDI, B5I, BWI, PDI and ISO).

	[http://sourceforge.net/projects/acetoneiso](http://sourceforge.net/projects/acetoneiso) || [acetoneiso2](https://www.archlinux.org/packages/?name=acetoneiso2)

*   **BashBurn** — Lightweight terminal based menu frontend for CD/DVD burning tools.

	[http://bashburn.dose.se/](http://bashburn.dose.se/) || [bashburn](https://www.archlinux.org/packages/?name=bashburn)

*   **[Brasero](https://en.wikipedia.org/wiki/Brasero_(software) "wikipedia:Brasero (software)")** — Disc burning application for the GNOME desktop that is designed to be as simple as possible. Part of [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

	[https://wiki.gnome.org/Apps/Brasero](https://wiki.gnome.org/Apps/Brasero) || [brasero](https://www.archlinux.org/packages/?name=brasero)

*   **cdw** — Ncurses frontend to *cdrecord*, *mkisofs*, *growisofs*, *dvd+rw-mediainfo*, *dvd+rw-format* and *xorriso*.

	[http://cdw.sourceforge.net/](http://cdw.sourceforge.net/) || [cdw](https://aur.archlinux.org/packages/cdw/)

*   **[GnomeBaker](https://en.wikipedia.org/wiki/GnomeBaker "wikipedia:GnomeBaker")** — Full featured CD/DVD burning application for the GNOME desktop.

	[http://gnomebaker.sourceforge.net/](http://gnomebaker.sourceforge.net/) || [gnomebaker](https://aur.archlinux.org/packages/gnomebaker/)

*   **Graveman** — GTK-based CD/DVD burning application. It requires configuration to point to correct devices.

	[http://graveman.tuxfamily.org/](http://graveman.tuxfamily.org/) || [graveman](https://aur.archlinux.org/packages/graveman/)

*   **[isomaster](https://en.wikipedia.org/wiki/ISO_Master "wikipedia:ISO Master")** — ISO image editor.

	[http://littlesvr.ca/isomaster](http://littlesvr.ca/isomaster) || [isomaster](https://aur.archlinux.org/packages/isomaster/)

*   **[K3b](https://en.wikipedia.org/wiki/K3b "wikipedia:K3b")** — Feature-rich and easy to handle CD burning and ripping application based on KDElibs.

	[http://www.k3b.org/](http://www.k3b.org/) || [k3b](https://www.archlinux.org/packages/?name=k3b)

*   **[X-CD-Roast](https://en.wikipedia.org/wiki/X-CD-Roast "wikipedia:X-CD-Roast")** — Lightweight *cdrtools* front-end for CD and DVD writing.

	[http://www.xcdroast.org/](http://www.xcdroast.org/) || [xcdroast](https://aur.archlinux.org/packages/xcdroast/)

*   **[Xfburn](https://en.wikipedia.org/wiki/Xfce#Xfburn "wikipedia:Xfce")** — Simple front-end to the libburnia libraries with support for CD/DVD(-RW), ISO images, and BurnFree.

	[http://goodies.xfce.org/projects/applications/xfburn](http://goodies.xfce.org/projects/applications/xfburn) || [xfburn](https://www.archlinux.org/packages/?name=xfburn)

*   **xorriso-tcltk** — Graphical front-end to ISO and CD/DVD/BD burn tool xorriso

	[https://www.gnu.org/software/xorriso/xorriso-tcltk-screen.gif](https://www.gnu.org/software/xorriso/xorriso-tcltk-screen.gif) || [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

## Playback

### CD

Playback of audio CDs requires the [libcdio](https://www.archlinux.org/packages/?name=libcdio) package.

### DVD

If you wish to play encrypted DVDs, you must install the libdvd* packages:

*   [libdvdread](https://www.archlinux.org/packages/?name=libdvdread)
*   [libdvdcss](https://www.archlinux.org/packages/?name=libdvdcss)
*   [libdvdnav](https://www.archlinux.org/packages/?name=libdvdnav)

Additionally, you must install player software. Popular DVD players are [MPlayer](/index.php/MPlayer "MPlayer"), [xine](https://en.wikipedia.org/wiki/Xine "wikipedia:Xine") and [VLC](/index.php/VLC "VLC"). See the [video players](/index.php/List_of_applications/Multimedia#Video_players "List of applications/Multimedia") list and the specific instructions for [MPlayer](/index.php/MPlayer#DVD_playing "MPlayer").

## Ripping

[Ripping](https://en.wikipedia.org/wiki/Ripping "wikipedia:Ripping") is the process of copying audio or video content to a hard disk, typically from removable media or media streams.

### CD

*   **[Abcde](https://en.wikipedia.org/wiki/ABCDE "wikipedia:ABCDE")** — Comprehensive command-line tool for ripping audio CDs.

	[https://abcde.einval.com/](https://abcde.einval.com/) || [abcde](https://www.archlinux.org/packages/?name=abcde)

*   **[Asunder](https://en.wikipedia.org/wiki/Asunder "wikipedia:Asunder")** — GTK+-based CD ripping program.

	[http://littlesvr.ca/asunder/](http://littlesvr.ca/asunder/) || [asunder](https://www.archlinux.org/packages/?name=asunder)

*   **[cdparanoia](https://en.wikipedia.org/wiki/cdparanoia "wikipedia:cdparanoia")** — Compact Disc Digital Audio (CDDA) Digital Audio Extraction (DAE) tool.

	[https://xiph.org/paranoia/index.html](https://xiph.org/paranoia/index.html) || [cdparanoia](https://www.archlinux.org/packages/?name=cdparanoia)

*   **Goobox** — CD player and ripper for GNOME.

	[https://people.gnome.org/~paobac/goobox/](https://people.gnome.org/~paobac/goobox/) || [goobox](https://www.archlinux.org/packages/?name=goobox)

*   **[Grip](https://en.wikipedia.org/wiki/Grip_(software) "wikipedia:Grip (software)")** — Fast and light CD ripper within the GNOME project that resembles [Audiograbber](https://en.wikipedia.org/wiki/Audiograbber "wikipedia:Audiograbber").

	[https://sourceforge.net/projects/grip/](https://sourceforge.net/projects/grip/) || [grip](https://aur.archlinux.org/packages/grip/).

*   **[K3b](https://en.wikipedia.org/wiki/K3b "wikipedia:K3b")** — Feature-rich and easy to handle CD/DVD burning and ripping application based on KDElibs.

	[http://www.k3b.org/](http://www.k3b.org/) || [k3b](https://www.archlinux.org/packages/?name=k3b)

*   **ripperX** — GTK+ program to rip CD audio tracks and encode them to the Ogg, MP3, or FLAC formats.

	[https://sourceforge.net/projects/ripperx/](https://sourceforge.net/projects/ripperx/) || [ripperx](https://aur.archlinux.org/packages/ripperx/)

*   **ripright** — Minimal CD ripper modeled on autorip.

	[http://www.mcternan.me.uk/ripright/](http://www.mcternan.me.uk/ripright/) || [ripright](https://aur.archlinux.org/packages/ripright/)

*   **ripit** — Command-line ripper that supports MusicBrainz, freeddb and various codecs.

	[http://www.suwald.com/ripit/news.php](http://www.suwald.com/ripit/news.php) || [ripit](https://aur.archlinux.org/packages/ripit/)

*   **rubyripper** — Audiodisk ripper that tries to deliver a secure rip through multiple rippings of the same track and corrections of any differences.

	[https://code.google.com/archive/p/rubyripper/](https://code.google.com/archive/p/rubyripper/) || [rubyripper](https://aur.archlinux.org/packages/rubyripper/)

*   **shnsplit** — Splits .wav and .flac files according to a CUE sheet and encodes the resulting pieces. A useful companion to ABCDE.

	[http://www.etree.org/shnutils/shntool/](http://www.etree.org/shnutils/shntool/) || [shntool](https://www.archlinux.org/packages/?name=shntool)

*   **[Sound Juicer](https://en.wikipedia.org/wiki/Sound_Juicer "wikipedia:Sound Juicer")** — CD ripper for GNOME.

	[https://wiki.gnome.org/Apps/SoundJuicer](https://wiki.gnome.org/Apps/SoundJuicer) || [sound-juicer](https://www.archlinux.org/packages/?name=sound-juicer)

*   **soundKonverter** — Front-end to various audio converters.

	[https://www.linux-apps.com/content/show.php?content=29024](https://www.linux-apps.com/content/show.php?content=29024) || [soundkonverter](https://www.archlinux.org/packages/?name=soundkonverter)

*   **whipper** — CD ripper aiming for accuracy over speed. Uses cdparanoia, MusicBrainz, AccurateRip.

	[https://github.com/JoeLametta/whipper](https://github.com/JoeLametta/whipper) || [whipper](https://www.archlinux.org/packages/?name=whipper)

### DVD-Video

Often, the process of ripping a DVD can be broken down into two subtasks:

1.  **Data extraction** — Copying the audio and/or video data to a hard disk,
2.  [Transcoding](https://en.wikipedia.org/wiki/Transcode "wikipedia:Transcode") — Converting the extracted data into a suitable format.

Some utilities perform both tasks, whilst others focus on one aspect or the other:

*   **Avidemux** — Multithreaded video transcoder, which offers both a graphical and command-line interface with many preset configurations. Influenced by Handbrake.

	[http://fixounet.free.fr/avidemux/](http://fixounet.free.fr/avidemux/) || [avidemux-qt-git](https://aur.archlinux.org/packages/avidemux-qt-git/)

*   **[dvdbackup](/index.php/Dvdbackup "Dvdbackup")** — Tool for pure data extraction which does not transcode. It is useful for creating *exact* copies of encrypted DVDs in conjunction with **libdvdcss** or for decrypting video for other utilities unable to read encrypted DVDs.

	[http://dvdbackup.sourceforge.net/](http://dvdbackup.sourceforge.net/) || [dvdbackup](https://www.archlinux.org/packages/?name=dvdbackup)

*   **[FFmpeg](/index.php/FFmpeg "FFmpeg")** — Complete and free Internet live audio and video broadcasting solution for Linux/Unix, capable to do a direct rip in any format (audio/video) from a DVD-Video ISO image, just select the input as the ISO image and proceed with the desired options. It also allows to downmixing, shrinking, spliting, selecting streams among other features.

	[http://ffmpeg.org/](http://ffmpeg.org/) || See [article](/index.php/FFmpeg#Package_installation "FFmpeg")

*   **HandBrake** — Multithreaded video transcoder, which offers both a graphical and command-line interface with many preset configurations.

	[https://handbrake.fr/](https://handbrake.fr/) || [handbrake](https://www.archlinux.org/packages/?name=handbrake)

*   **Hybrid** — Multi platform Qt based frontend for a bunch of other tools which can convert nearly every input to x264/Xvid/VP8 + ac3/ogg/mp3/aac/flac inside an mp4/m2ts/mkv/webm/mov/avi container, a Blu-ray or an AVCHD structure.

	[http://www.selur.de/](http://www.selur.de/) || [hybrid-encoder](https://aur.archlinux.org/packages/hybrid-encoder/)

*   **[MEncoder](/index.php/MEncoder "MEncoder")** — Free command line video decoding, encoding and filtering tool released under the GNU GPL. It is a close sibling to MPlayer and can convert all the formats that MPlayer understands into a variety of compressed and uncompressed formats using different codecs. Wrapper programs like [h264enc](https://aur.archlinux.org/packages/h264enc/) can provide an assistive interface. Many [GUI frontends](/index.php/MEncoder#GUI_frontends "MEncoder") are available.

	[http://www.mplayerhq.hu/](http://www.mplayerhq.hu/) || [mencoder](https://www.archlinux.org/packages/?name=mencoder)

*   **Transcode** — Video/DVD ripper and encoder with the CLI.

	[http://transcoding.org/](http://transcoding.org/) || [transcode](https://www.archlinux.org/packages/?name=transcode)

#### dvd::rip

dvd::rip is a front-end to [transcode](https://www.archlinux.org/packages/?name=transcode), used to extract DVD's to the hard disk and transcode or extract and transcode on-the-fly.

The following packages should be installed:

*   [dvdrip](https://aur.archlinux.org/packages/dvdrip/): GTK front-end for [transcode](https://www.archlinux.org/packages/?name=transcode), which performs the ripping and encoding
*   [libdv](https://www.archlinux.org/packages/?name=libdv): Software codec for DV video
*   [xvidcore](https://www.archlinux.org/packages/?name=xvidcore): If you want to encode your ripped files as XviD, an open source MPEG-4 video codec (free alternative to DivX).
*   [subtitleripper](https://aur.archlinux.org/packages/subtitleripper/): If you want to read and process subtitles.

The dvd::rip preferences are mostly well-documented/self-explanatory. If you need help with something, see [http://www.exit1.org/dvdrip/doc/gui-gui_pref.cipp](http://www.exit1.org/dvdrip/doc/gui-gui_pref.cipp).

Ripping a DVD is often a simple matter of selecting the preferred codec(s), selecting the desired titles, then clicking the "Rip" button.

### DVD-Audio

*   **Python Audio Tools** — Includes dvda2track, which is easy to use command line tool to extract DVD-Audio tracks to uncompressed wav files.

	[http://audiotools.sourceforge.net/](http://audiotools.sourceforge.net/) || [audiotools-git](https://aur.archlinux.org/packages/audiotools-git/)

## Troubleshooting

### Brasero fails to normalize audio CD

If you try to burn it may stop at the first step called Normalization.

As a workaround you can disable the normalization plugin using the *Edit > Plugins* menu

### VLC: Error "... could not open the disc /dev/dvd"

If you get an error like

```
vlc dvdread could not open the disc "/dev/dvd"

```

it may be because there is no device node `/dev/dvd` on your system. Udev no longer creates `/dev/dvd` and instead uses `/dev/sr0`. To fix this, edit the VLC configuration file (`~/.config/vlc/vlcrc`):

```
# DVD device (string)
dvd=/dev/sr0

```

### DVD drive is noisy

If playing DVD videos causes the system to be very loud, it may be because the disk is spinning faster than it needs to. To temporarily change the speed of the drive, run:

```
# eject -x 12 /dev/dvd

```

Sometimes:

```
# hdparm -E12 /dev/dvd

```

Any speed that is supported by the drive can be used, or 0 for the maximum speed.

[Setting CD-ROM and DVD-ROM drive speed](http://michal.kosmulski.org/computing/tips/cd-rom-speed.html)

### Playback does not work with new computer (new DVD-Drive)

If playback does not work and you have a new computer (new DVD-Drive) the reason might be that the [region code](https://en.wikipedia.org/wiki/DVD_region_code "wikipedia:DVD region code") is not set. You can read and set the region code with the [regionset](https://aur.archlinux.org/packages/regionset/) package.

### None of the above programs are able to rip/encode a DVD to my hard disk!

Make sure the region of your DVD reader is set correctly; otherwise, you will get loads of inexplicable [CSS](https://en.wikipedia.org/wiki/Content_Scramble_System "wikipedia:Content Scramble System")-related errors. Use the [regionset](https://aur.archlinux.org/packages/regionset/) package to do so.

### GUI program log indicates problems with backend program

If you use a GUI program and experience problems which the program's log blames on some backend program, then try to reproduce the problem by the logged backend program arguments. Whether you succeed with reproducing or not, you may report the logged lines and your own findings to the places mentioned in [#Burn backend problems](#Burn_backend_problems) section.

#### Special case: medium error / write error

Here are some typical messages about the drive disliking the medium. This can only be solved by using a different drive or a different medium. A different program will hardly help.

Brasero with backend growisofs:

```
BraseroGrowisofs stderr: :-[ WRITE@LBA=0h failed with SK=3h/ASC=0Ch/ACQ=00h]: Input/output error

```

Brasero with backend libburn:

```
BraseroLibburn Libburn reported an error SCSI error on write(16976,16): [3 0C 00] Write error

```

### AHCI

If your new DVD drive is detected but you can't mount disks, check wether your BIOS uses [AHCI](/index.php/AHCI "AHCI") and add the module to the kernel image.

Edit `/etc/mkinitcpio.conf` and add `ahci` to the `MODULES` variable (see [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") for details):

```
MODULES="ahci"

```

Rebuild the kernel image so that it includes the newly added module:

```
# mkinitcpio -p linux

```

### BD-R DL 50GB errors on trying to burn second layer

Using *growisofs* from [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools) for burning 50GB BD-R DL discs might result in a fatal error and damaged media, such as:

 `$ growisofs -Z /dev/sr0 -J -R -V "label" files` 
```
Executing 'mkisofs -J -R -V label files | builtin_dd of=/dev/sr0 obs=32k seek=0'
I: -input-charset not specified, using utf-8 (detected in locale settings)
  0.03% done, estimate finish Fri Jan 29 19:50:36 2016
  0.05% done, estimate finish Fri Jan 29 19:50:36 2016
  0.08% done, estimate finish Fri Jan 29 19:50:36 2016
/dev/sr0: pre-formatting blank BD-R for 49.8GB...
/dev/sr0: "Current Write Speed" is 8.2x4390KBps.
  0.11% done, estimate finish Sat Jan 30 03:29:13 2016
  0.13% done, estimate finish Sat Jan 30 02:10:01 2016
...
 63.20% done, estimate finish Fri Jan 29 20:43:45 2016
:-[ WRITE@LBA=b6d820h failed with SK=3h/WRITE ERROR]: Input/output error
:-( write failed: Input/output error
/dev/sr0: flushing cache
/dev/sr0: closing track
/dev/sr0: closing session
:-[ CLOSE SESSION failed with SK=5h/INVALID FIELD IN CDB]: Input/output error
/dev/sr0: reloading tray

```

This happened at the 25GB boundary when starting to write the second layer. Using *cdrecord* from [cdrtools](https://www.archlinux.org/packages/?name=cdrtools) works with no problems. Tested with a 'HL-DT-ST BD-RE WH16NS40' LG burner, and Verbatim BD-R DL 6x discs (#96911). [FS#47797](https://bugs.archlinux.org/task/47797)

### Disc tray autocloses

If after ejecting a cd, either by using the `eject` command, or pushing the drive button, the drive disc tray autocloses before being able to remove the disc, try the following command:

```
# sysctl -w dev.cdrom.autoclose=0

```

If that solves the problem, make the change permanent:

 `/etc/sysctl.d/60-cdrom-autoclose.conf`  `dev.cdrom.autoclose = 0` 

## See also

*   In the United States, backup of physically obtained media is allowed under these conditions: [About Piracy - RIAA](https://www.riaa.com/resources-learning/about-piracy/).
*   [Convert any Movie to DVD Video](/index.php/Convert_any_Movie_to_DVD_Video "Convert any Movie to DVD Video")
*   [Main page of the project Libburnia](http://libburnia-project.org/)