[p7zip](http://p7zip.sourceforge.net/) is command line port of [7-Zip](https://en.wikipedia.org/wiki/7zip "wikipedia:7zip") for [POSIX](https://en.wikipedia.org/wiki/POSIX "wikipedia:POSIX") systems, including Linux.

## Contents

*   [1 Installation](#Installation)
*   [2 Examples](#Examples)
*   [3 Differences between 7z, 7za and 7zr binaries](#Differences_between_7z.2C_7za_and_7zr_binaries)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [p7zip](https://www.archlinux.org/packages/?name=p7zip) package.

The command to run the program is the following:

```
$ 7z

```

## Examples

*   List the content of an archive:

```
$ 7z l <archive name>

```

*   Extract all files from an archive to the current directory without using directory names:

```
$ 7z e <archive name>

```

*   Extract with full paths:

```
$ 7z x <archive name>

```

*   Extract into a new directory:

```
$ 7z x -o<folder name> <archive name>

```

## Differences between 7z, 7za and 7zr binaries

The package includes three binaries, `/usr/bin/7z`, `/usr/bin/7za`, and `/usr/bin/7zr`. Their manual pages explain the differences:

*   [7z(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/7z.1) uses plugins to handle archives.
*   [7za(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/7za.1) is a stand-alone executable that handles fewer archive formats than 7z.
*   [7zr(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/7zr.1) is a stand-alone executable. It is a "light-version" of 7za that only handles 7z archives. In contrast to 7za, it cannot handle encrypted archives.

## See also

*   [7zip homepage.](http://www.7-zip.org/download.html)
*   [How to use 7zip on Linux command Line.](https://www.ibm.com/developerworks/community/blogs/6e6f6d1b-95c3-46df-8a26-b7efd8ee4b57/entry/how_to_use_7zip_on_linux_command_line144?lang=en)