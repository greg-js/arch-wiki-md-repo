# fuseiso

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Fuseiso#](https://wiki.archlinux.org/index.php/Talk:Fuseiso))

The _fuseiso_ command line program is a simple tool that uses [FUSE](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") and helps for a regular user to mount [ISO](https://en.wikipedia.org/wiki/ISO_9660 "wikipedia:ISO 9660") disk images. The _fuseiso_ tool does not create an automatically generated destination by a pattern and is specialized on mounting of the optical disk image formats as .iso, .nrg, .bin, .mdf and .img.

## Contents

*   [1 Installation](#Installation)
*   [2 Basic functions](#Basic_functions)
    *   [2.1 Mounting an ISO image](#Mounting_an_ISO_image)
        *   [2.1.1 Unmounting](#Unmounting)
*   [3 Using with GNOME Files](#Using_with_GNOME_Files)

## Installation

[Install](/index.php/Install "Install") [fuseiso](https://www.archlinux.org/packages/?name=fuseiso) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Basic functions

### Mounting an ISO image

The syntax for mounting an image is:

```
# fuseiso _source_imagefile_ _destination_directory_

```

The destination mount point must be writable and have no other mounted files/devices to it.

Run `fuseiso -h` for all the available options.

#### Unmounting

To unmount the image, use `fusermount -u _mountpoint_`, it works fine even with many other unmount tools like _pumount_ or _umount_. The `fusermount -u` command can be used to disconnect any other storage devices that were mounted by other mount tools.

## Using with GNOME Files

For users of GNOME there is an easy way of using fuseiso from the nautilus-context menu. First you will need the [nautilus-actions](https://www.archlinux.org/packages/?name=nautilus-actions) package, then you need to save the following scripts to a folder of your choice (eg. `/usr/bin`):

 `nautilus-actions-iso-mount.sh` 

```
 #!/bin/bash

 FILE=$(basename "$1")
 MOUNTPOINT="$HOME/Desktop/$FILE"

 fuseiso -p "$1" "$MOUNTPOINT"

```

 `nautilus-actions-iso-umount.sh` 

```
 #!/bin/bash

 FILE=$(basename "$1")
 MOUNTPOINT="$HOME/Desktop/$FILE"

 fusermount -u "$MOUNTPOINT"

```

and make them executable:

```
chmod +x _/path_to_scripts/_nautilus-actions-iso-*

```

Now, start _nautilus-actions-config_ (_System > Preferences > Nautilus Actions Configuration_).

Add a new action with the following settings:

*   Label: _Mount ISO_
*   Icon: A symbol of your choice (eg: _gtk-cdrom_)
*   Path: `_/path_to_scripts/_nautilus-actions-iso-mount.sh`
*   Parameters: _%F_
*   Working directory: _%d_
*   Basenames: _*.iso ; *.nrg ; *.bin ; *.img ; *.mdf (for each add a seperated entry)_
*   Match case: _"must match one of"_
*   Mimetypes: _*/*_

With this action you can mount ISO-images to your Desktop. It will create a folder in ~/Desktop with the name of the iso. fuseiso will mount the iso to this folder.

And a second one:

*   Label: _Unmount ISO_
*   Icon: A symbol of your choice (eg: _gtk-cdrom_)
*   Path: `_/path_to_scripts/_nautilus-actions-iso-umount.sh`
*   Parameters: _%F_
*   Working directory: _%d_
*   Basenames: _*.iso ; *.nrg ; *.bin ; *.img ; *.mdf (for each add a seperated entry)_
*   Match case: _"must match one of"_
*   Mimetypes: _*/*_

This second action will unmount the mounted iso and remove the folder from the desktop.

Sometimes you have to logout to be able to mount any image of the given types simply by right clicking it in Files and selecting _Mount ISO_. To unmount it again, just right click the corresponding folder on your desktop and select _Unmount ISO_.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Fuseiso&oldid=412080](https://wiki.archlinux.org/index.php?title=Fuseiso&oldid=412080)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [File systems](/index.php/Category:File_systems "Category:File systems")

Hidden category:

*   [Pages flagged with Template:Stub](/index.php/Category:Pages_flagged_with_Template:Stub "Category:Pages flagged with Template:Stub")