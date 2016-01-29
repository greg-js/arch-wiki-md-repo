# Tar

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Coreutils](/index.php/Coreutils "Coreutils").**

**Notes:** Offers very little over `man tar` (Discuss in [Talk:Tar#](https://wiki.archlinux.org/index.php/Talk:Tar))

From [GNU's Tar Page](http://www.gnu.org/software/tar/):

NaN

As an early Unix compression format, `tar` files (known as **tarballs**) are widely used for packaging in Unix-like operating systems. Both [pacman](/index.php/Pacman "Pacman") and [AUR](/index.php/AUR "AUR") packages are tarballs, and Arch uses [GNU's](/index.php/GNU_Project "GNU Project") `Tar` program by default.

## Contents

*   [1 Usage](#Usage)
    *   [1.1 Creating an archive and updating](#Creating_an_archive_and_updating)
    *   [1.2 Backup with parallel compression](#Backup_with_parallel_compression)
*   [2 See also](#See_also)

## Usage

For `tar` archives, `tar` by default will extract the file according to its extension:

```
$ tar xvf file.EXTENSION

```

Forcing a given format:

| File Type | Extraction Command |
| `file.tar` | `tar xvf file.tar` |
| `file.tgz` | `tar xvzf file.tgz` |
| `file.tar.gz` | `tar xvzf file.tar.gz` |
| `file.tar.bz` | `bzip -cd file.bz | tar xvf -` |
| `file.tar.bz2` | `tar xvjf file.tar.bz2`
`bzip2 -cd file.bz2 | tar xvf -` |
| `file.tar.xz` | `tar xvJf file.tar.xz`
`xz -cd file.xz | tar xvf -` |

The construction of some of these `tar` arguments may be considered legacy, but they are still useful when performing specific operations. The **Compatibility** section of `tar`'s [man page](/index.php/Man_page "Man page") shows how they work in detail.

### Creating an archive and updating

Creating an initial archive and updating it proves useful for updating web-domains. First, create an archive in the present working directory. Note that `tar` will not include `./archive.tar` into the new tarball if `./archive.tar` already exists.

```
 $ tar -cf ./archive.tar .

```

When updating the archive, keep in mind that `tar` will only update files listed in the archive.

```
 $ tar --list -f ./archive.tar
 $ tar -uf ./archive.tar

```

### Backup with parallel compression

To back up using parallel compression ([SMP](https://en.wikipedia.org/wiki/Symmetric_multiprocessing "wikipedia:Symmetric multiprocessing")), use [pbzip2](https://www.archlinux.org/packages/?name=pbzip2) (Parallel bzip2).

First back up the files to a plain tarball with no compression:

```
# tar -cvf /_destionation_path_/etc-backup.tar /etc

```

Then use pbzip2 to compress it in parallel:

```
$ pbzip2 /path/to/chosen/directory/etc-backup.tar.bz2

```

Store `etc-backup.tar.bz2` on one or more offline media, such as a USB stick, external hard drive, or CD-R. Occasionally verify the integrity of the backup process by comparing original files and directories with their backups. Possibly maintain a list of hashes of the backed up files to make the comparison quicker.

Restore corrupted `/etc` files by extracting the `etc-backup.tar.bz2` file in a temporary working directory, and copying over individual files and directories as needed. To restore the entire `/etc` directory with all its contents, move the `etc-backup.tar.bz2` files into the `/` directory. As root, execute the following command:

```
tar -xvjf etc-backup.tar.bz2

```

## See also

*   [GNU tar manual](http://www.gnu.org/software/tar/manual/index.html) (Also available via `info tar`)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Tar&oldid=408772](https://wiki.archlinux.org/index.php?title=Tar&oldid=408772)"