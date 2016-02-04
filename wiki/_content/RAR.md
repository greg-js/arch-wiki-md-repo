# RAR

RAR (and UNRAR) is the Linux port of the commandline-only version of [WinRAR](http://www.rarlab.com/download.htm) available in both the i686 and x86-64 flavors.

## Contents

*   [1 Key features](#Key_features)
*   [2 Installation](#Installation)
    *   [2.1 RAR](#RAR)
    *   [2.2 UNRAR](#UNRAR)
*   [3 Configuration file](#Configuration_file)
*   [4 RAR compression examples](#RAR_compression_examples)
    *   [4.1 General syntax](#General_syntax)
    *   [4.2 Recursively compress an entire directory structure](#Recursively_compress_an_entire_directory_structure)
    *   [4.3 Mixed-mode archives](#Mixed-mode_archives)
    *   [4.4 Recursively compress many directory structures using a list](#Recursively_compress_many_directory_structures_using_a_list)
*   [5 UNRAR examples](#UNRAR_examples)
    *   [5.1 General syntax](#General_syntax_2)

## Key features

*   Variable amounts of redundancy ("recovery record" or "recovery volumes" both of which are demonstrated below) can be added to an archive, making it more resistant to corruption. Even if parts of an archive are damaged, it is possible to fully recover the stored data if a large enough recovery record exists. On its own, [Tar](/index.php/Tar "Tar") does not have this ability.
*   RAR is able to efficiently handle split volumes. Built-in support for multi-volume files enables the unpacking program to simply prompt the user for the next .partXXX RAR file, without the need to manually copy and then rejoin the pieces, or for extracting a file from a single piece without needing all pieces. RAR does not support tapes, as it uses seek and rename operations on its files.
*   RAR archives can be of a solid format, in which all of the compressed files are treated as a single data block. Most currently used compression formats (with the exception of the older ZIP) allow solid structuring.
*   Strong encryption capabilities. Older versions of the file format used a proprietary algorithm; newer versions use the AES encryption algorithm, a block cipher adopted as an encryption standard by the U.S. government. The only known ways to recover an encrypted file are via dictionary or brute force attacks. In newer versions, password protection can optionally protect filenames too, so that the filenames contained within the archive will not be displayed without the right password.

## Installation

### RAR

Obtain [rar](https://aur.archlinux.org/packages/rar/) (full package minus UNRAR) available in the [AUR](/index.php/AUR "AUR").

### UNRAR

The [unrar](https://www.archlinux.org/packages/?name=unrar) is provided separately and resides in the [official repositories](/index.php/Official_repositories "Official repositories"). Install it via [pacman](/index.php/Pacman "Pacman") as usual.

## Configuration file

RAR for Linux reads configuration information from the file `~/.rarrc` (i.e. in the user's home directory) or if you wish to define a global set of options for all users in the /etc directory.

The syntax of the file is simply the following string:

```
switches=any RAR switches, separated by spaces

```

For example:

```
switches=-m5 -rr5 -ol -msjpg;mp3;avi;zip;rar;tar;gz;jpg

```

For a complete listing and explanation of rar's switches, see the [user's manual](http://www.rarreg.com/users_manual.php)

## RAR compression examples

### General syntax

```
$ rar _command_ -_switch 1_ -_switch N_ _archive_ _files.rar_ _@listfiles..._

```

For a complete listing of commands and switches, see the last section of this article or simply run `rar`.

### Recursively compress an entire directory structure

*   Task: backup `/home/darkhorse` to `/media/data/darkhorse-backup.rar` using 10 % recovery records:

```
$ rar a -r -rr10 /media/data/darkhorse-backup.rar /home/darkhorse

```

*   Explained:

| Switch | Action |
| a | **a**dds files to archives. |
| -r | **r**ecurse subdirectories (includes all dirs/files under the parent directory). |
| -rr10 | adds **r**ecovery **r**ecords to the archive. This way up to 10% of the compressed archive can become corrupt or unusable, and it will be able to recover the data through parity. |

### Mixed-mode archives

You can also use mixed-mode archives which means that file types you specifiy do not get compressed - they simply get stored.

*   Task: backup `/home/darkhorse` to `/media/data/darkhorse-backup.rar`:

```
$ rar a -r -rr10 -s -m5 -msjpg;mp3;tar /media/data/darkhorse-backup.rar /home/darkhorse

```

*   Explained:

| Switch | Action |
| a | **a**dds files to archives. |
| -r | **r**ecurse subdirectories (includes all dirs/files under the parent directory). |
| -rr10 | adds **r**ecovery **r**ecords to the archive. This way up to 10% of the compressed archive can become corrupt or unusable, and it will be able to recover the data through parity. |
| -m5 | Use the highest level of compression (m0 = store ... m3 = default ... m5 = maximal level of compression. |
| -msjpg;mp3;tar | ignore the compression option and store all .jpg and .mp3 and .tar files. |

### Recursively compress many directory structures using a list

*   Task: backup `/home/darkhorse` and `/home/palomino` and `/home/seabiscuit` to `/media/data/homes-backup.rar`.

First create a list (simple text file) containing the various targets. In this example, the list will be three lines long. I named it 'home-list' in this example but you can call it anything you want:

```
/home/darkhorse
/home/palomino
/home/seabiscuit

```

```
$ rar a -r -rr10 -s /media/data/homes-backup.rar @/path/to/home-list

```

## UNRAR examples

### General syntax

```
$ unrar _command_ -_switch 1_ -_switch N_ _archive_ _files..._ _@listfiles..._ _path_to_extract\_

```

For a complete listing of commands and switches simply run:

```
$ unrar --help

```

To extract into a new folder:

```
$ unrar x /media/data/homes-backup.rar homes-backup/

```

For multi-part rar files, run:

```
$ unrar x homes-backup.part1.rar homes-backup/

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=RAR&oldid=383247](https://wiki.archlinux.org/index.php?title=RAR&oldid=383247)"