[ObexFTP](http://dev.zuckschwerdt.org/openobex/wiki/ObexFtp) implements the [OBEX](https://en.wikipedia.org/wiki/OBEX "wikipedia:OBEX") protocol, used to transfer files. OBEX was adopted by [Bluetooth](/index.php/Bluetooth "Bluetooth") and [Android](/index.php/Android "Android") supports it since version 2.1.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Obex Object Push](#Obex_Object_Push)
    *   [2.2 ObexFTP](#ObexFTP)
    *   [2.3 ObexFS](#ObexFS)

## Installation

[Install](/index.php/Install "Install") the [obexftp](https://aur.archlinux.org/packages/obexftp/) package.

For a Tcl/Tk front-end [install](/index.php/Install "Install") [obextool](https://aur.archlinux.org/packages/obextool/).

For a [GVFS](/index.php/GVFS "GVFS") client [install](/index.php/Install "Install") [gnome-vfs-obexftp](https://aur.archlinux.org/packages/gnome-vfs-obexftp/).

## Usage

### Obex Object Push

To send a file, find out the channel of the OBEX Push service:

```
$ sdptool search --bdaddr *MAC_address* OPUSH

```

Then send the file to that channel using the following command from [[1]](http://dev.zuckschwerdt.org/openobex/wiki/ObexFtpExamples/#Obex-PUSH-over-Bluetooth):

```
$ obexftp --nopath --noconn --uuid none --bluetooth *MAC_address* --channel *channel* --put *file*

```

Alternatively you could use [ussp-push](https://aur.archlinux.org/packages/ussp-push/). To receive OBEX Pushes, there's [ObexPushD](https://gitlab.com/obexpushd/mainline), which however is no longer packaged for Arch.

### ObexFTP

If your device supports the Obex FTP service but you do not wish to mount the device you can transfer files to and from the device using the obexftp command.

To send a file to a device run the command:

```
$ obexftp -b *MAC_address* -p /path/to/file

```

To retrieve a file from a device run the command:

```
$ obexftp -b *MAC_address* -g filename

```

**Note:** Ensure that the file you are retrieving is in the device's *exchange folder*. If the file is in a subfolder of the exchange folder then provide the correct path in the command.

### ObexFS

Another option, rather than using KDE or Gnome Bluetooth packages, is ObexFS which allows for the mounting of phones which are treated like any other filesystem.

**Note:** To use ObexFS, one needs a device that provides an ObexFTP service.

Mount supported phones by running:

```
$ obexfs -b *MAC_address* *mountpoint*

```

Once you have finished, to unmount the device use the command:

```
$ fusermount -u *mountpoint*

```

For more mounting options see [http://dev.zuckschwerdt.org/openobex/wiki/ObexFs](http://dev.zuckschwerdt.org/openobex/wiki/ObexFs)

**Note:** Ensure that the bluetooth device you are mounting is **not** set to mount *read-only*. You should be able to do this from the device's settings. If the device is mounted *read-only* you may encounter a permissions error when trying to transfer files to the device.