# Subsonic

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**Subsonic** is a music server that lets you store your music on one machine and play it from other machines, cell phones, via a web interface, or various other applications. It can be installed using the [subsonic](https://aur.archlinux.org/packages/subsonic/)<sup><small>AUR</small></sup> package on [AUR](/index.php/AUR "AUR").

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Install transcoders](#Install_transcoders)
    *   [1.2 HTTPS Setup](#HTTPS_Setup)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 FLAC playback](#FLAC_playback)
    *   [2.2 UTF-8 file names not added to the database](#UTF-8_file_names_not_added_to_the_database)
*   [3 Madsonic](#Madsonic)
*   [4 External links](#External_links)

## Configuration

After performing any configuration, remember to [restart](/index.php/Restart "Restart") `subsonic.service`.

### Install transcoders

By default, Subsonic uses FFmpeg to transcode videos and songs to an appropriate format and bitrate on-the-fly. After installation, you can change these defaults so that, for example, Subsonic will transcode FLAC files using FLAC and LAME instead of FFmpeg. You should therefore [Install](/index.php/Install "Install") the [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg), and you may also want to install [flac](https://www.archlinux.org/packages/?name=flac) and [lame](https://www.archlinux.org/packages/?name=lame).

For security reasons, Subsonic will not search the system for any transcoders. Instead, the user must create symlinks to the transcoders in the `/var/lib/subsonic/transcode` folder. Create the symlinks like so:

```
$ cd /var/lib/subsonic/transcode
# for transcoder in ffmpeg flac lame; do ln -s "$(which $transcoder)"; done

```

### HTTPS Setup

To enable HTTPS browsing and streaming, edit `/var/lib/subsonic/subsonic.sh` and change this line:

```
SUBSONIC_HTTPS_PORT=0

```

To this:

```
SUBSONIC_HTTPS_PORT=8443

```

**Note:** port 8443 seems hard-coded somewhere. When attempting to change it to port 8080 it will automatically redirect the browser to port 8443 after manually accepting the invalid HTTPS certificate. You will still be able to re-navigate to port 8080 after the warning page and have it work on that port.

## Troubleshooting

### FLAC playback

The FFmpeg transcoder doesn't handle FLAC files well, and clients will often fail to play the resultant streams. (at least, on [my](/index.php?title=User:Ichimonji10&action=edit&redlink=1 "User:Ichimonji10 (page does not exist)") machine) Using FLAC and LAME instead of FFmpeg solves this issue. This workaround requires that the FLAC and LAME transcoders have been installed, as explained in [#Install transcoders](#Install_transcoders).

Start Subsonic and go to `settings > transcoding`. Ensure that the default FFmpeg transcoder does not get used on files with a "flac" extension, then add a new entry. You'll end up with something like this:

<table class="wikitable">

<tbody>

<tr>

<th>Name</th>

<th>Convert from</th>

<th>Convert to</th>

<th>Step 1</th>

<th>Step 2</th>

</tr>

<tr>

<td>mp3 default</td>

<td>... NOT flac ...</td>

<td>mp3</td>

<td>ffmpeg ...</td>

</tr>

<tr>

<td>mp3 flac</td>

<td>flac</td>

<td>mp3</td>

<td>flac --silent --decode --stdout %s</td>

<td>lame --silent -h -b %b -</td>

</tr>

</tbody>

</table>

### UTF-8 file names not added to the database

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** The default init system under Arch is now Systemd, not SysV. (Discuss in [Talk:Subsonic#](https://wiki.archlinux.org/index.php/Talk:Subsonic))

You must have at least one UTF-8 [locale](/index.php/Locale "Locale") installed.

If you start subsonic using `/etc/rc.d/subsonic`, and your /etc/[rc.conf](/index.php/Rc.conf "Rc.conf") has `DAEMON_LOCALE="no"`, then the subsonic daemon will be started with the C locale, and Java will skip any folders with "international characters" (e.g. ßðþøæå etc.). Either set `DAEMON_LOCALE` to `"yes"` (but this will affect **all** rc.daemons), or add a line to the beginning of `/var/subsonic/subsonic.sh` which sets `LANG` to an installed UTF-8 locale, e.g. `LANG=nn_NO.utf8`.

## Madsonic

Madsonic is a fork of Subsonic with extra features, does not require a registration fee (read completely free) and is available in AUR.

Once you start the server, pay close attention to the Transcoding options, as you will probably have to change the command from "Audioffmpeg" to "ffmpeg".

## External links

*   [Official web site](http://www.subsonic.org)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Subsonic&oldid=412181](https://wiki.archlinux.org/index.php?title=Subsonic&oldid=412181)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia](/index.php/Category:Multimedia "Category:Multimedia")