# p7zip

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

p7zip is command line port of [7-Zip](https://en.wikipedia.org/wiki/7zip "wikipedia:7zip") for [POSIX](https://en.wikipedia.org/wiki/POSIX "wikipedia:POSIX") systems, including Linux.

## Contents

*   [1 Installation](#Installation)
*   [2 Examples](#Examples)
*   [3 Differences between 7z, 7za and 7zr binaries](#Differences_between_7z.2C_7za_and_7zr_binaries)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Pacman "Pacman") the [p7zip](https://www.archlinux.org/packages/?name=p7zip) package which is available in the [official repositories](/index.php/Official_repositories "Official repositories").

The command to run the program is the following:

```
$ 7z

```

## Examples

To extract all files from an archive to the current directory without using directory names, run:

```
$ 7za e <archive name>

```

To extract with full paths, run:

```
$ 7za x <archive name>

```

To extract into a new directory, run:

```
$ 7za x -o<folder name> <archive name>

```

## Differences between 7z, 7za and 7zr binaries

The package includes three binaries, `/usr/bin/7z`, `/usr/bin/7za`, and `/usr/bin/7zr`. Their manual pages explain the differences:

*   7z uses plugins to handle archives.
*   7za is a stand-alone executable. 7za handles fewer archive formats than 7z, but does not need any others.
*   7zr is a stand-alone executable. 7zr handles fewer archive formats than 7z, but does not need any others. 7zr is a "light-version" of 7za that only handles 7z archives.

## See also

*   [Homepage.](http://p7zip.sourceforge.net/)
*   [7zip homepage.](http://www.7-zip.org/download.html)
*   [How to use 7zip on Linux command Line.](https://www.ibm.com/developerworks/community/blogs/6e6f6d1b-95c3-46df-8a26-b7efd8ee4b57/entry/how_to_use_7zip_on_linux_command_line144?lang=en)

Retrieved from "[https://wiki.archlinux.org/index.php?title=P7zip&oldid=398973](https://wiki.archlinux.org/index.php?title=P7zip&oldid=398973)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Data compression and archiving](/index.php/Category:Data_compression_and_archiving "Category:Data compression and archiving")