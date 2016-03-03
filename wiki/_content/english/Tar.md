From [GNU's Tar Page](http://www.gnu.org/software/tar/):

	*"The `Tar` program provides the ability to create tar archives, as well as various other kinds of manipulation. For example, you can use Tar on previously created archives to extract files, to store additional files, or to update or list files which were already stored."*

As an early Unix compression format, `tar` files (known as **tarballs**) are widely used for packaging in Unix-like operating systems. Both [pacman](/index.php/Pacman "Pacman") and [AUR](/index.php/AUR "AUR") packages are tarballs, and Arch uses [GNU's](/index.php/GNU_Project "GNU Project") `Tar` program by default.

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

### Backup with parallel compression

To back up using parallel compression ([SMP](https://en.wikipedia.org/wiki/Symmetric_multiprocessing "wikipedia:Symmetric multiprocessing")), use [pbzip2](https://www.archlinux.org/packages/?name=pbzip2) (Parallel bzip2).

First back up the files to a plain tarball with no compression:

```
# tar -cvf /*destionation_path*/etc-backup.tar /etc

```

Then use pbzip2 to compress it in parallel:

```
$ pbzip2 /path/to/chosen/directory/etc-backup.tar.bz2

```

Store `etc-backup.tar.bz2` on one or more offline media, such as a USB stick, external hard drive, or CD-R. Occasionally verify the integrity of the backup process by comparing original files and directories with their backups. Possibly maintain a list of hashes of the backed up files to make the comparison quicker.

Restore corrupted `/etc` files by extracting the `etc-backup.tar.bz2` file in a temporary working directory, and copying over individual files and directories as needed. To restore the entire `/etc` directory with all its contents execute the following command as root:

```
tar -xvjf etc-backup.tar.bz2 -C /

```

## See also

*   [GNU tar manual](http://www.gnu.org/software/tar/manual/index.html) (Also available via `info tar`)