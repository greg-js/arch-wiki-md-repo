[Partclone](http://partclone.org), like the well-known [Partimage](http://www.partimage.org/Main_Page), can be used to back up and restore a partition while considering only used blocks.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Using Partclone with an ext4-formatted partition](#Using_Partclone_with_an_ext4-formatted_partition)
    *   [2.1 Without compression](#Without_compression)
    *   [2.2 With compression](#With_compression)

## Installation

[Install](/index.php/Install "Install") the [partclone](https://www.archlinux.org/packages/?name=partclone) package.

## Using Partclone with an ext4-formatted partition

### Without compression

To backup *without* compression:

```
$ partclone.ext4 -c -s /dev/sda1 -o ~/image_sda1.pcl

```

To restore it:

```
$ partclone.ext4 -r -s ~/image_sda1.pcl -o /dev/sda1

```

### With compression

To backup *with* compression:

```
$ partclone.ext4 -c -s /dev/sda1 | gzip -c > ~/image_sda1.pcl.gz

```

**Note:** For maximum compression use "gzip -c9"

To restore it:

```
zcat ~/image_sda1.pcl.gz | partclone.ext4 -r -o /dev/sda1

```