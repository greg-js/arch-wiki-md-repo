This article outlines the additional software packages necessary to expand the features and functionality of file managers, particularly where using a [window manager](/index.php/Window_manager "Window manager") such as [Openbox](/index.php/Openbox "Openbox"). The ability to access partitions and removable media without a password - if affected - has also been provided.

## Contents

*   [1 Overview](#Overview)
*   [2 Additional features](#Additional_features)
    *   [2.1 Mounting](#Mounting)
        *   [2.1.1 File manager daemon](#File_manager_daemon)
        *   [2.1.2 Standalone](#Standalone)
    *   [2.2 Networks](#Networks)
        *   [2.2.1 Windows access](#Windows_access)
        *   [2.2.2 Apple access](#Apple_access)
    *   [2.3 Thumbnail previews](#Thumbnail_previews)
        *   [2.3.1 File managers other than Dolphin and Konqueror](#File_managers_other_than_Dolphin_and_Konqueror)
        *   [2.3.2 Dolphin and Konqueror (KDE)](#Dolphin_and_Konqueror_.28KDE.29)
    *   [2.4 Archive files](#Archive_files)
    *   [2.5 NTFS read/write support](#NTFS_read.2Fwrite_support)
    *   [2.6 Desktop notifications](#Desktop_notifications)
    *   [2.7 Enable Trash functionality on different filesystems (external drives)](#Enable_Trash_functionality_on_different_filesystems_.28external_drives.29)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 "Not Authorized" when attempting to mount drives](#.22Not_Authorized.22_when_attempting_to_mount_drives)
    *   [3.2 Password required to access partitions](#Password_required_to_access_partitions)
    *   [3.3 Directories are not opened in the file manager](#Directories_are_not_opened_in_the_file_manager)

## Overview

**Note:** When installed, the software packages listed below will automatically be sourced by all installed - and capable - file managers, and within all desktop environments and/or window managers.

A file manager alone will not provide the features and functionality that users of full desktop environments such as [Xfce](/index.php/Xfce "Xfce") or [KDE](/index.php/KDE "KDE") will be accustomed to. This is because additional software packages will be required to enable a given file manager to:

*   Display and access other partitions
*   Display, mount, and access removable media (e.g. USB sticks, optical discs, and digital cameras)
*   Enable networking / shared networks with other installed operating systems
*   Enable thumbnailing
*   Archive and extract compressed files
*   Automatically mount removable media

When a file manager has been installed as part of a full desktop environment, most of these packages will usually have been installed automatically. Consequently, where a file manager has been installed for a standalone window manager then - as is the case with the window manager itself - only a basic foundation will be provided. The user must then determine the nature and extent of the features and functionality to be added.

## Additional features

Particularly where using - or intending to use - a lightweight environment, it should be noted that more file manager features and functions will usually mean the use of more memory. See also [udisks](/index.php/Udisks "Udisks").

### Mounting

*   [gvfs](https://www.archlinux.org/packages/?name=gvfs): The **G**nome **V**irtual **F**ile **S**ystem provides mounting and trash functionality. GVFS uses [udisks2](https://www.archlinux.org/packages/?name=udisks2) for mounting functionality and is the recommended solution for most file managers.

**Tip:** For some file managers it may be useful to have the package [gamin](https://www.archlinux.org/packages/?name=gamin) installed. [Gamin](/index.php/Gamin "Gamin") is a file and directory monitoring system.

Folders used by GVFS:

*   `/usr/lib/gvfs/` contains `gvfsd-*` files, where `*` refers to the various supported file system types.
*   `/usr/share/gvfs/mounts/` contains mount rules for GVFS. To use one's own rules, create `~/.gvfs/mounts`.

Additional packages for installation usually follows the [gvfs-* pattern](https://www.archlinux.org/packages/?q=gvfs-), for example:

*   [gvfs-mtp](https://www.archlinux.org/packages/?name=gvfs-mtp): media players and mobile devices that use [MTP](/index.php/MTP "MTP")
*   [gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2): digital cameras and mobile devices that use [PTP](https://en.wikipedia.org/wiki/Picture_Transfer_Protocol "wikipedia:Picture Transfer Protocol")
*   [gvfs-afc](https://www.archlinux.org/packages/?name=gvfs-afc): Apple mobile devices

#### File manager daemon

The first is to simply autostart or run the installed file manager in [daemon](/index.php/Daemon "Daemon") mode (i.e. as a background process). For example, when using [PCManFM](/index.php/PCManFM "PCManFM") in [Openbox](/index.php/Openbox "Openbox"), the following command would be added to the `~/.config/openbox/autostart` file:

```
pcmanfm -d &

```

It will also be necessary to configure the file manager itself in respect to volume management (e.g. what it will do and what applications will be launched when certain file types are detected upon mounting).

**Tip:** Most desktop environments will start the file manager in daemon mode by default so manual intervention will not be required in these use cases.

#### Standalone

Another option is to install a separate [mount application](/index.php/List_of_applications#Mount_tools "List of applications"). The advantages of using this are:

*   Less memory may be required to run as a background / [daemon](/index.php/Daemon "Daemon") process than a file manager
*   It is not file manager specific, allowing them to be freely added, removed, and switched
*   [gvfs](https://www.archlinux.org/packages/?name=gvfs) may not have to be installed for mounting, lessening memory use.

### Networks

**Note:** It will also be necessary to enable [Bluetooth](/index.php/Bluetooth "Bluetooth") and/or networking with [Windows](/index.php/Samba "Samba") to enable the relevant file manager functionality in turn.

*   [obexfs](https://www.archlinux.org/packages/?name=obexfs): Bluetooth device mounting and file transfers (see [Bluetooth](/index.php/Bluetooth "Bluetooth"))
*   [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb): Windows File and printer sharing for **Non-KDE** desktops (see [Samba](/index.php/Samba "Samba"))
*   [kdenetwork-filesharing](https://www.archlinux.org/packages/?name=kdenetwork-filesharing): Windows File and printer sharing for [KDE](/index.php/KDE "KDE") (see [Samba#KDE](/index.php/Samba#KDE "Samba"))
*   [sshfs](https://www.archlinux.org/packages/?name=sshfs): FUSE client based on the SSH File Transfer Protocol

#### Windows access

If using [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb), to access Windows/CIFS/Samba file shares first open the file manager, and enter the following into the path name, changing <sever name> and <share name> as appropriate:

```
smb://<server name>/<share name>

```

#### Apple access

AFP support is included in [gvfs](https://www.archlinux.org/packages/?name=gvfs). To access AFP files first open the file manager, and enter the following into the path name, changing <sever name> and <share name> as appropriate:

```
afp://<server name>/<share name>

```

### Thumbnail previews

Some file managers may not support thumbnailing, even when the packages listed have been installed. Check the documentation for the relevant file manager.

#### File managers other than Dolphin and Konqueror

These packages apply to most file managers, such as [PCManFM](/index.php/PCManFM "PCManFM"), [SpaceFM](/index.php/SpaceFM "SpaceFM"), [Thunar](/index.php/Thunar "Thunar") and [xfe](https://www.archlinux.org/packages/?name=xfe). The exceptions are Dolphin and Konqueror, used in the [KDE](/index.php/KDE "KDE") desktop environment.

*   [tumbler](https://www.archlinux.org/packages/?name=tumbler): Image files. This **<u>must</u>** also be installed to expand thumbnailing capabilities to other file types
*   [poppler-glib](https://www.archlinux.org/packages/?name=poppler-glib): Adobe `.pdf` files
*   [ffmpegthumbnailer](https://www.archlinux.org/packages/?name=ffmpegthumbnailer): Video files
*   [freetype2](https://www.archlinux.org/packages/?name=freetype2): Font files
*   [libgsf](https://www.archlinux.org/packages/?name=libgsf): `.odf` files
*   [raw-thumbnailer](https://www.archlinux.org/packages/?name=raw-thumbnailer): `.raw` files
*   [totem](https://www.archlinux.org/packages/?name=totem): Video files and tagged audio files ([GNOME Files](/index.php/GNOME_Files "GNOME Files"), [Nemo](/index.php/Nemo "Nemo") and Caja only)
*   [evince](https://www.archlinux.org/packages/?name=evince) or [atril](https://www.archlinux.org/packages/?name=atril): `.pdf` files

#### Dolphin and Konqueror (KDE)

See [Dolphin#File previews](/index.php/Dolphin#File_previews "Dolphin").

### Archive files

To extract compressed files such as tarballs (`.tar` and `.tar.gz`) within a file manager, it will first be necessary to install a GUI archiver such as [file-roller](https://www.archlinux.org/packages/?name=file-roller). See [List of applications#Archiving and compression tools](/index.php/List_of_applications#Archiving_and_compression_tools "List of applications") for further information. An additional package such as [unzip](https://www.archlinux.org/packages/?name=unzip) must also be installed to support the use of zipped `.zip` files. Once an archiver has been installed, files in the file manager may consequently be right-clicked to be archived or extracted.

Archive files are mounted under folder `/run/user/$(id -u)/gvfs/` with automatically created mount point that contains full path to the file in its name where all `/` are replaced with `%252F` and `:` replaced with `%253A` [hex codes](https://www.owasp.org/index.php/Double_Encoding).

Example of path to the mounted archive `/full/path/to/file/name.zip`

```
/run/user/$(id -u)/gvfs/archive:host=file%253A%252F%252F%252F**full%252Fpath%252Fto%252Ffile%252Fname.zip**

```

### NTFS read/write support

See the [NTFS-3G](/index.php/NTFS-3G "NTFS-3G") article.

### Desktop notifications

Some file managers make use of [desktop notifications](/index.php/Desktop_notifications "Desktop notifications") to confirm various events and statuses like mounting, unmounting and ejection of removable media.

### Enable Trash functionality on different filesystems (external drives)

Make [trash directories](http://www.ramendik.ru/docs/trashspec.html) `.Trash-*<uid>*` for each users on the top level of filesystems:

For example (mount point: /media/sdc1, uid: 1000, gid: 1000):

```
# mkdir /media/sdc1/.Trash-1000

```

and `chown` them:

```
# chown 1000:1000 /media/sdc1/.Trash-1000

```

## Troubleshooting

### "Not Authorized" when attempting to mount drives

File managers using [udisks](/index.php/Udisks "Udisks") require a [polkit](/index.php/Polkit "Polkit") authentication agent. See [polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit").

### Password required to access partitions

The need to enter a password to access other partitions or mounted removable media will likely be due to the default permission settings of [udisks2](https://www.archlinux.org/packages/?name=udisks2). More specifically, permission may be set to the root account only, not the user account. See [Udisks#Configuration](/index.php/Udisks#Configuration "Udisks") for details.

### Directories are not opened in the file manager

You may find that an application that is not a file manager, [Audacious](/index.php/Audacious "Audacious") for example, is set as the default application for opening directories — an application that specifies that it can handle the `inode/directory` MIME type in its desktop entry can become the default. You can query the default application for opening directories with the following command:

```
$ xdg-mime query default inode/directory

```

To ensure that directories are opened in the file manager, run the following command:

```
$ xdg-mime default *my-file-manager.desktop* inode/directory

```

where `*my-file-manager.desktop*` is the desktop entry for your file manager — `*org.gnome.Nautilus.desktop*` for example.

**Tip:** If you want the change to be system-wide, run the command above as root or create/edit the following file: `/usr/share/applications/mimeapps.list` 
```
[Default Applications]
inode/directory=*my-file-manager.desktop*
```