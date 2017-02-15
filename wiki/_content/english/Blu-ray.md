This article is designed to help Linux users to play the Blu-ray discs they have legally purchased on their computers. Since no official Blu-ray player software is available on their system, Linux users have to use open-source libraries capable of handling the DRM schemes that protect these disc contents. This is legal in most countries where interoperability allows this.

## Contents

*   [1 How it works](#How_it_works)
    *   [1.1 Blu-ray DRM](#Blu-ray_DRM)
        *   [1.1.1 AACS](#AACS)
            *   [1.1.1.1 AACS decryption process](#AACS_decryption_process)
        *   [1.1.2 BD+](#BD.2B)
*   [2 Playback](#Playback)
    *   [2.1 Preparation](#Preparation)
    *   [2.2 Decryption process](#Decryption_process)
        *   [2.2.1 Decrypting using VUK (step 3.1 or 3.2.1)](#Decrypting_using_VUK_.28step_3.1_or_3.2.1.29)
        *   [2.2.2 Decrypting using PK and Host K/C (step 3.2.2)](#Decrypting_using_PK_and_Host_K.2FC_.28step_3.2.2.29)
        *   [2.2.3 BD+ support](#BD.2B_support)
    *   [2.3 Media players](#Media_players)
        *   [2.3.1 mplayer](#mplayer)
            *   [2.3.1.1 Stuttering video](#Stuttering_video)
            *   [2.3.1.2 Incorrect audio language](#Incorrect_audio_language)
            *   [2.3.1.3 Out-of-sync audio](#Out-of-sync_audio)
        *   [2.3.2 VLC](#VLC)
        *   [2.3.3 xine](#xine)
    *   [2.4 Troubleshooting](#Troubleshooting)
        *   [2.4.1 Absent KEYDB.cfg file](#Absent_KEYDB.cfg_file)
        *   [2.4.2 Revoked Host key/certificate](#Revoked_Host_key.2Fcertificate)
        *   [2.4.3 Using aacskeys](#Using_aacskeys)
            *   [2.4.3.1 If aacskeys is not able to generate the key](#If_aacskeys_is_not_able_to_generate_the_key)
*   [3 See also](#See_also)

## How it works

### Blu-ray DRM

Contrary to the DVD CSS, which was definitely compromised once the unique encryption key had been discovered, Blu-ray uses stronger DRM mechanisms, which makes it a lot more difficult to manage. Firstly, the AACS standard uses a lot more complicated cryptographic process to protect the disc content, but also allows the industry to revoke compromised keys and distribute new keys through new discs. Secondly, Blu-ray may also use another layer of protection: BD+. Although most of commercial discs use AACS, a few of them additionally use BD+. In 2007, the AACS system was compromised and decryption keys were published on the Internet. Many decryption programs were made available, but the interest to Linux users was the capability of playing their discs - legally purchased - on their computers. Although the industry was able to revoke the first leaked decryption keys, new keys are regularly published in a cat and mouse play.

#### AACS

The AACS specification and decryption process are publicly available at [[1]](http://www.aacsla.com/specifications/). Many articles and research papers describe it in detail at [[2]](http://forum.doom9.org/showthread.php?t=122363), [[3]](http://cacr.uwaterloo.ca/~dstinson/papers/AACS-journal.pdf) or [[4]](http://www.iis.sinica.edu.tw/papers/lcs/5007-F.pdf).

[libaacs](https://www.archlinux.org/packages/?name=libaacs) is a research project from the VideoLAN developer team to implement the Advanced Access Content System specification, and distributed as an open-source library [[5]](http://www.videolan.org/developers/libaacs.html). This project does not offer any key or certificate that could be used to decode encrypted copyrighted material. However, combined with a key database file, it is possible to use it to play Blu-ray discs that use the AACS standard. This file is called `KEYDB.cfg` and is accessed by libaacs in `~/.config/aacs`. The format of this file is available at [[6]](http://git.videolan.org/?p=libaacs.git;a=blob_plain;f=KEYDB.cfg;hb=HEAD).

##### AACS decryption process

The AACS decryption process for a protected disc by a licensed player goes through four stages:

1.  The software/embedded player's Device Keys, together with the disc's Media Key Block (MKB) data are used to retrieve a "Processing Key", and with that (plus another datum from the MKB) to compute the Media Key.
2.  That Media Key, together with the disc's Volume ID (VID) obtained by the player presenting a valid Host Certificate to the drive is used to compute the Volume Unique Key (VUK).
3.  This VUK is used to unscramble the disc's scrambled Title Keys.
4.  Finally those Title Keys unscramble the disc's protected media content.

Note that it is the disc that contains the MKB. MKBs have been renewed since the first commercial Blu-ray release in 2006\. The latest MKB is version 64, but many MKB actually share the same key. The software player provides the Host key and certificate, whereas the drive contains a list of the Host key/certificates that have been revoked. Host key/certification revocation occurs when a newer disc (containing a higher MKB than the previous played disc) is decrypted, or played, or attempted to decrypt or play (the mere insertion of a disc does not update the drive). When this happens, the drive forever loses its capability to use older Host key/certificates.

Using [libaacs](https://www.archlinux.org/packages/?name=libaacs), the decryption process can skip some of these stages to reach the last step, which allows the media player to play the disc. This is either by providing in the `KEYDB.cfg` file either (or both):

*   a valid (corresponding to the MKB version of the disc) Processing key and a valid (i.e. non revoked by the drive) Host key/certificate
*   a valid VUK for the specific disc.

If libaacs finds a valid processing key for the disc MKB version as well as a valid Host key and certificates, it can start the decryption process from step 2\. However, the Host key/certificates are regularly revoked through the propagation of new Blu-ray discs. Once revoked, a drive is not able to read both new and older discs. This is usually irreversible and can only be fixed by providing a more recent Host key/certificate (for Windows users, this corresponds to updating their software player). The advantage of this method is that until the Host key/certificate is revoked, and as long as the disc uses an MKB version for which the Processing key is known, libaacs is able to compute the VUK of any disc. As of today, the Processing keys for MKB version up to 61 have been computed and made available on the Internet. Thus, this method is slightly outdated.

Thankfully, in case no valid Processing key is available and/or the Host certificate has been revoked, libaacs has an alternative way to decrypt a disc: by providing a valid VUK in the `KEYDB.cfg` file. This allows libaacs to skip directly to step 3\. Contrary to the Processing keys, VUKs are disc specific. Therefore this is less efficient as the user will have to get the VUK from a third party. But the great advantage is that VUKs cannot be revoked. Note that if libaacs is able to perform step 2 (with a valid Host key/certificate), then it stores the VUK calculated in step 3 in `~/.cache/aacs/vuk`. At subsequent viewings of the same disc, libaacs can reuse the stored VUK. Thus it may be a good idea to backup these VUKs, or even better, to upload them to [[7]](http://www.labdv.com/aacs/).

There have been several efforts to compile VUKs from various sources. Early attempts include forum threads, such as available at [[8]](http://forum.doom9.org/attachment.php?attachmentid=11170&d=1276615904) or [[9]](http://forum.doom9.org/showthread.php?p=1525922#post1525922). Recently, a centralised VUK database has been made available at [[10]](http://www.labdv.com/aacs/), with nearly 21,000 published VUKs. This is the most comprehensive source of public VUKs available.

#### BD+

BD+ is an additional but optional component of the Blu-ray DRM. In December 2013, VideoLAN released the long awaited [libbdplus](https://aur.archlinux.org/packages/libbdplus/) which provides experimental support for BD+ decryption. The library does not provide keys or certificates required for BD+ decryption, you need to retrieve and install them separately, as explained at [[11]](http://www.labdv.com/aacs/) and [[12]](http://www.labdv.com/aacs/advanced-users.php).

**Note:** The download provided by LabDV is a *.tar.bz2* archive, but is named `bdplus-vm0.bz2`. You want to put a folder named `vm0` in `~/.config/bdplus`, **not** a file named `bdplus-vm0`. You may have to rename the file to end with *.tar.bz2* if you are using a GUI archiving tool.

## Playback

### Preparation

1.  [Install](/index.php/Install "Install") [libbluray](https://www.archlinux.org/packages/?name=libbluray) and [libaacs](https://www.archlinux.org/packages/?name=libaacs) from the [official repositories](/index.php/Official_repositories "Official repositories").
2.  Download the [`KEYDB.cfg`](http://www.labdv.com/aacs/KEYDB.cfg) file from [[13]](http://www.labdv.com/aacs/) and copy it in the directory `~/.config/aacs`. This file contains PK, HC and VUK data required for attempting the decryption process described below for nearly 21,000 discs.
3.  If necessary (*i.e.* if volumes are not mounted automatically on your system), mount the disc to a directory, *e.g.*: `# mount /dev/sr0 /media/blurays` 

### Decryption process

Launch a Blu-ray software player, such as VLC, and try to play the disc (on VLC, select Media -> Open Disc, then in the Disc tab, chose Blu-ray. Be sure "No disc Menus" is checked.). The software player will then apply the decryption process described below:

1.  The user starts playing a Blu-ray with a video player having libbluray and libaacs support.
2.  If the BR disc is not scrambled with AACS, go to 4.1.
3.  If the BR disc is scrambled with AACS, libaacs will:
    1.  Check if a valid VUK for the disc is already available in `~/.cache/aacs/vuk/`. If yes, go to step 4.1, if not continue to next step.
    2.  Read `~/.config/aacs/KEYDB.cfg`:
        1.  If a valid VUK is available, go to 4.1, if not continue to next step.
        2.  If a valid PK (*i.e.* corresponding to the disc MKB version) and a valid (non-revoked by drive) Host key/certificate is available, libaacs will attempt to compute the VUK. The VUK is then stored in `~/.cache/aacs/vuk` for future use. Go to step 4.1\. If no valid PK/HKC are available, go to step 4.2.
4.  Result
    1.  The software player is able to play the disc content.
    2.  The software player fails to read the disc content.

#### Decrypting using VUK (step 3.1 or 3.2.1)

Using the VUK specific to your disc will always work, and cannot be revoked by the industry, as it is the most downstream decryption key for a Blu-ray disc. However, there is one unique VUK per disc, corresponding to one VID, making this method rely on VUK lists or databases. The VUK will be known if either of these are true:

*   decrypting using PK and Host K/C described below has worked once, and the generated VUK for your disc has been stored in `~/.cache/aacs/vuk`, or
*   the valid VUK for your disc has been obtained from a third party (*i.e.* is available in `KEYDB.cfg`). This allows you to read a disc, even if the PK and host key/certificate have been revoked for your disc MKB version.

If none of these are true, then the software player will attempt decrypting the disc using the second method.

#### Decrypting using PK and Host K/C (step 3.2.2)

The advantage of this method is that - when it works - it can decrypt any disc (up to a certain MBK version) and compute the VUK required to play it. Once the VUK is known, it is then stored for future usage.

**Note:** As of December 2016, latest commercial Blu-ray discs come with MKB v64\. Since no PK beyond MKB v61 has been made publicly available, this decryption method may be obsolete for most recent discs. It is presented for information purpose, but has little chance to be used with recent discs until newer PKs are made available. Therefore, decrypting using VUK lists is now privileged, since it is irrevocable by the movie industry. However, this implies Linux users rely on discovery by third parties since there is no more any open source tool on Linux that can generate VUKs for discs with MKB v62 and above.

This method uses the Processing keys and a Host key/certificate present at the beginning of the `KEYDB.cfg` file. Currently, they will work for a disc up to MKB v61 but have been revoked in MKB v62 and above discs) in `~/.config/aacs/`. Further, this method will only work if your drive has not revoked the host key/certificate that is in this `KEYDB.cfg` file (*i.e.* if you have not tried to play a disc with MKB v30 and above).

If this method is successful, after you play the disc, libaacs will store the VUK in `~/.cache/aacs/vuk`. The filename is the disc ID and its content is the VUK itself. VLC will reuse this VUK even if it does not find a valid `KEYDB.cfg` file, so it could be a good idea to backup this directory for the future.

#### BD+ support

These pages [[14]](http://www.labdv.com/aacs/) and [[15]](http://www.labdv.com/aacs/advanced-users.php) provide you with further instructions on how to play Blu-ray discs encrypted with BD+. [libbdplus](https://aur.archlinux.org/packages/libbdplus/) provides experimental support for BD+ decryption, but if this fails, users will have to use commercial solutions, such as [makemkv](https://aur.archlinux.org/packages/makemkv/) or [DVDFab](#See_also) (under Wine).

BD+ mainly works by adding errors to the video stream, not enough to make it unwatchable but enough to make it unpleasant to watch due to near constant artifacting. These are fixed in official players by using "fixup tables", which are downloaded from the internet and provide a mapping to convert the broken video stream into the correct video stream. libbdplus stopped working a long time ago, and for right now there's no open source method of playing discs with BD+ protection.

### Media players

These are media players capable of using libbluray and libaacs to play AACS-scrambled Blu-ray discs.

#### mplayer

To play Blu-ray discs in mplayer the basic playback command is:

```
$ mplayer br:///</bluray/mount/dir>

```

or:

```
$ mplayer br://<title number> -bluray-device </bluray/mount/dir>

```

##### Stuttering video

It is likely that you will need to enable hardware acceleration and multi core CPU support for the Blu-ray to play smoothly.

For nvidia cards, enable hardware acceleration by installing libvdpau and using the option '-vo vdpau' with mplayer. e.g:

```
$ mplayer -vo vdpau br:///</bluray/mount/dir>

```

For multi core CPU support use the options '-lavdopts threads=N', where 'N' is the number of cores, e.g:

```
$ mplayer -lavdopts threads=2 br:///</bluray/mount/dir>

```

##### Incorrect audio language

You can scroll through the playback languages using the '#' key.

##### Out-of-sync audio

From your first mplayer output, you must find the codec used for the Blu-ray. It will be at the end of the line "Selected video codec".

For H.264 discs use the option '-vc ffh264vdpau'. e.g:

```
$ mplayer -vc ffh264vdpau br:///</bluray/mount/dir>

```

For VC-1 discs use '-vc ffvc1vdpau'. e.g:

```
$ mplayer -vc ffvc1vdpau br:///</bluray/mount/dir>

```

For MPEG discs use '-vc ffmpeg12vdpau'. e.g:

```
$ mplayer -vc ffmpeg12vdpau br:///</bluray/mount/dir>

```

#### VLC

Since version 2.0.0, vlc has had experimental Blu-ray playback support. Blu-ray menus can be used if you install [libbluray-git](https://aur.archlinux.org/packages/libbluray-git/) instead of [libbluray](https://www.archlinux.org/packages/?name=libbluray).

Start playback with:

```
$ vlc bluray://</bluray/mount/dir>

```

#### xine

Start playback with:

```
$ xine bluray://</bluray/mount/dir>

```

### Troubleshooting

#### Absent `KEYDB.cfg` file

If a valid VUK is found in `~/.cache/aacs/vuk`, then libaacs does not need to use `KEYDB.cfg` to decrypt the content. However, a `KEYDB.cfg` file in `~/.config/aacs/` is still required (even if that file is empty).

#### Revoked Host key/certificate

Unfortunately, what may happen when trying to play a newer Blu-ray disc is the revocation of host key/certificates (which are keys of licensed software players) by your drive. When this happens, [aacskeys](https://aur.archlinux.org/packages/aacskeys/) will return this message:

```
 The given Host Certficate / Private Key has been revoked by your drive.

```

This is part of the AACS protection scheme: editors are able to revoke old software player host keys that have leaked on the Internet and distribute the lists on newer commercial disc releases. This is irreversible and does cannot be fixed even after reflashing the drive. The only two ways to correct this would be:

*   to update the host key/certificate part in `KEYDB.cfg` to ones that have not been revoked (yet)
*   to add in `KEYDB.cfg` the VUK of each specific disc instead, [as explained above](#Decrypting_using_VUK_.28step_3.1_or_3.2.1.29). VUKs cannot be revoked by the industry.

When a disc (using mplayer or vlc) is succesfully decrypted, libaacs will store the VUK in `~/.cache/aacs/vuk`. If the host key/certificate in `KEYDB.cfg` is subsequently revoked, VLC will still be able to use the stored VUK, so it could be a good idea to backup the `~/.cache/aacs` directory for the future.

#### Using aacskeys

Install [aacskeys](https://aur.archlinux.org/packages/aacskeys/). You need to run [aacskeys](https://aur.archlinux.org/packages/aacskeys/) from a directory that contains valid host key/certificate and processing keys:

 `cd /usr/share/aacskeys` and run: `aacskeys </bluray/mount/dir>` eg: `cd /usr/share/aacskeys && aacskeys /media/blurays` 

If you wish, you may add the Blu-ray to the key database: edit `~/.config/aacs/KEYDB.cfg` and add the information output by aacskeys using this syntax:

 `0x<unit key file hash> = Film Title    | V | 0x<volume unique key>` 

##### If aacskeys is not able to generate the key

Try to generate the VolumeID with [DumpVID](http://forum.doom9.org/showthread.php?p=993782) using wine. The VolumeID can now be used to generate the Blu-ray VUK with aacskeys with the VolumeID option

 `Usage: aacskeys [options] <mountpath> [volume id / binding nonce]` 

## See also

For DVD, the [libdvdcss](https://www.archlinux.org/packages/?name=libdvdcss) package supplies the needed decryption libs. Below are some options for Blu-ray/HD-DVD decryption. Users can employ to backup a commercial Blu-ray movie under Fair Use guidelines:

*   [aacskeys](https://aur.archlinux.org/packages/aacskeys/) - Opensource
*   [dumphd](https://aur.archlinux.org/packages/dumphd/) - Opensource
*   [makemkv](https://aur.archlinux.org/packages/makemkv/) - Closed source/limited free beta

*   [anydvdhd](http://www.slysoft.com/en/anydvdhd.html) - Commercial software requiring users to run it on an Microsoft OS in a VM.
*   [DVDFab HD Decrypter](https://appdb.winehq.org/objectManager.php?sClass=application&iId=2377) - Commercial software for Windows, but works fine using [Wine](/index.php/Wine "Wine").