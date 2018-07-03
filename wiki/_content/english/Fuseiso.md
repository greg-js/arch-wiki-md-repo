The *fuseiso* command line program is a simple tool that uses [FUSE](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") so an unprivileged user can mount [ISO](https://en.wikipedia.org/wiki/ISO_9660 "wikipedia:ISO 9660") disk images. The *fuseiso* tool does not create an automatically generated destination by a pattern and is specialized on mounting of the optical disk image formats as `.iso`, `.nrg`, `.bin`, `.mdf` and `.img`.

## Contents

*   [1 Installation](#Installation)
*   [2 Basic functions](#Basic_functions)
    *   [2.1 Mounting an ISO image](#Mounting_an_ISO_image)
        *   [2.1.1 Unmounting](#Unmounting)
*   [3 Using with GNOME Files](#Using_with_GNOME_Files)
*   [4 nemo](#nemo)

## Installation

[Install](/index.php/Install "Install") the [fuseiso](https://www.archlinux.org/packages/?name=fuseiso) package.

## Basic functions

### Mounting an ISO image

The syntax for mounting an image is:

```
$ fuseiso *source_imagefile* *destination_directory*

```

The destination mount point must be writable and have no other mounted files/devices to it.

Run `fuseiso -h` for all the available options.

#### Unmounting

To unmount the image, use `fusermount -u *mountpoint*`, it works fine even with many other unmount tools like *pumount* or *umount*. The `fusermount -u` command can be used to disconnect any other storage devices that were mounted by other mount tools.

## Using with GNOME Files

For users of GNOME there is an easy way of using fuseiso from the nautilus-context menu. First you will need the [filemanager-actions](https://www.archlinux.org/packages/?name=filemanager-actions) package, then you need to save the following scripts to a folder of your choice (eg. `/usr/local/bin`):

 `filemanager-actions-iso-mount.sh` 
```
 #!/bin/bash

 FILE=$(basename "$1")
 MOUNTPOINT="$HOME/Desktop/$FILE"

 fuseiso -p "$1" "$MOUNTPOINT"

```
 `filemanager-actions-iso-umount.sh` 
```
 #!/bin/bash

 FILE=$(basename "$1")
 MOUNTPOINT="$HOME/Desktop/$FILE"

 fusermount -u "$MOUNTPOINT"

```

and make them executable:

```
chmod +x */path_to_scripts/*filemanager-actions-iso-*

```

Now, start *fma-config-tool* (*System > Preferences > Nautilus Actions Configuration*).

Add a new action with the following settings:

*   Label: *Mount ISO*
*   Icon: A symbol of your choice (eg: *gtk-cdrom*)
*   Path: `*/path_to_scripts/*filemanager-actions-iso-mount.sh`
*   Parameters: *%F*
*   Working directory: *%d*
*   Basenames: **.iso ; *.nrg ; *.bin ; *.img ; *.mdf (for each add a seperated entry)*
*   Match case: *"must match one of"*
*   Mimetypes: **/**

With this action you can mount ISO-images to your Desktop. It will create a folder in ~/Desktop with the name of the iso. fuseiso will mount the iso to this folder.

And a second one:

*   Label: *Unmount ISO*
*   Icon: A symbol of your choice (eg: *gtk-cdrom*)
*   Path: `*/path_to_scripts/*filemanager-actions-iso-umount.sh`
*   Parameters: *%F*
*   Working directory: *%d*
*   Basenames: **.iso ; *.nrg ; *.bin ; *.img ; *.mdf (for each add a seperated entry)*
*   Match case: *"must match one of"*
*   Mimetypes: **/**

This second action will unmount the mounted iso and remove the folder from the desktop.

Sometimes you have to logout to be able to mount any image of the given types simply by right clicking it in Files and selecting *Mount ISO*. To unmount it again, just right click the corresponding folder on your desktop and select *Unmount ISO*.

## nemo

nemo as a file browser has a packaged function on right click to mount an iso. unmount is done by clicking on the respective icon of the mounted iso, just like one would do for USB drives.