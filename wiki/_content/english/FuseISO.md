[FuseISO](https://sourceforge.net/projects/fuseiso/) is a [FUSE](/index.php/FUSE "FUSE") module to let unprivileged users mount [ISO](https://en.wikipedia.org/wiki/ISO_9660 "wikipedia:ISO 9660") filesystem images (*.iso*, *.nrg*, *.bin*, *.mdf* and *.img*).

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Mounting](#Mounting)
    *   [2.2 Unmounting](#Unmounting)
*   [3 Integration](#Integration)
    *   [3.1 GNOME Files](#GNOME_Files)
    *   [3.2 Nemo](#Nemo)

## Installation

[Install](/index.php/Install "Install") the [fuseiso](https://www.archlinux.org/packages/?name=fuseiso) package.

## Usage

### Mounting

To mount an image:

```
$ fuseiso *image* *directory*

```

The destination mount point must be writable and have no other mounted files or devices to it.

Run `fuseiso -h` for all the available options.

### Unmounting

To unmount the image:

```
$ fusermount -u *directory*

```

The command can be used to disconnect other storage devices mounted by other mount tools.

## Integration

### GNOME Files

For users of GNOME there is an easy way of using fuseiso from the nautilus-context menu.

First you will need the [filemanager-actions](https://www.archlinux.org/packages/?name=filemanager-actions) package, then you need to save the following scripts to a folder of your choice (e.g. `~/.local/bin/`):

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

Make them executable:

```
$ chmod +x /*path_to_scripts*/filemanager-actions-iso-*

```

Now, start *fma-config-tool* (*System > Preferences > Nautilus Actions Configuration*).

Add a new action with the following settings:

*   Label: *Mount ISO*
*   Icon: A symbol of your choice (eg: *gtk-cdrom*)
*   Path: `/*path_to_scripts*/filemanager-actions-iso-mount.sh`
*   Parameters: *%F*
*   Working directory: *%d*
*   Basenames: **.iso ; *.nrg ; *.bin ; *.img ; *.mdf (for each add a seperated entry)*
*   Match case: *"must match one of"*
*   Mimetypes: **/**

With this action you can mount ISO-images to your Desktop. It will create a folder in ~/Desktop with the name of the iso. fuseiso will mount the iso to this folder.

And a second one:

*   Label: *Unmount ISO*
*   Icon: A symbol of your choice (eg: *gtk-cdrom*)
*   Path: `/*path_to_scripts*/filemanager-actions-iso-umount.sh`
*   Parameters: *%F*
*   Working directory: *%d*
*   Basenames: **.iso ; *.nrg ; *.bin ; *.img ; *.mdf (for each add a seperated entry)*
*   Match case: *"must match one of"*
*   Mimetypes: **/**

This second action will unmount the mounted iso and remove the folder from the desktop.

Sometimes you have to logout to be able to mount any image of the given types simply by right clicking it in Files and selecting *Mount ISO*. To unmount it again, just right click the corresponding folder on your desktop and select *Unmount ISO*.

### Nemo

[Nemo](/index.php/Nemo "Nemo") as a file browser has a packaged function on right click to mount an iso. unmount is done by clicking on the respective icon of the mounted iso, just like one would do for USB drives.