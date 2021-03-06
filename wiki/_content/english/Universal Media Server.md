[Universal Media Server](http://www.universalmediaserver.com/) is a DLNA-compliant UPnP Media Server. It is based on PS3 Media Server by shagrath. It is actually an evolution of the "SubJunk Build" of PMS. UMS was started by SubJunk, an official developer of PMS, in order to ensure greater stability and file-compatibility.

Because it is written in Java, Universal Media Server supports all major operating systems, with versions for Windows, Linux and Mac OS X. The program streams or transcodes many different media formats with little or no configuration. It is powered by MEncoder, FFmpeg, tsMuxeR, AviSynth, MediaInfo and more, which combine to offer support for a wide range of media formats.

## Installation

Universal Media Server is available in the [AUR](/index.php/AUR "AUR") via [ums](https://aur.archlinux.org/packages/ums/).

## Configuration

UMS can be run on a per-user basis. Run the executable at `/opt/ums/UMS.sh` once, then copy the config file at `/opt/ums/UMS.conf` to `~/.config/UMS/UMS.conf` and edit it. The `port`, `folders`, and `minimized` options in `UMS.conf` are especially noteworthy.

## Running

To start the daemon as a particular user, [start/enable](/index.php/Start/enable "Start/enable") the template unit `ums@*user*.service`