The traditional Unix archiving and compression tools are separated according to the [Unix philosophy](https://en.wikipedia.org/wiki/Unix_philosophy "wikipedia:Unix philosophy"):

*   A [file archiver](https://en.wikipedia.org/wiki/File_archiver "wikipedia:File archiver") combines several files into one archive file, e.g. *tar*.
*   A [compression](https://en.wikipedia.org/wiki/Data_compression "wikipedia:Data compression") tool compresses and decompresses data.

These tools are often used in sequence by firstly creating an archive file and then compressing it.

Of course there are also [tools that do both](#Archiving_and_compression), which tend to additionally offer encryption, error detection and recovery.

## Contents

*   [1 Archiving only](#Archiving_only)
*   [2 Compression tools](#Compression_tools)
    *   [2.1 Compression only](#Compression_only)
    *   [2.2 Archiving and compression](#Archiving_and_compression)
    *   [2.3 Esoteric, rare or deprecated tools](#Esoteric.2C_rare_or_deprecated_tools)
    *   [2.4 Feature charts](#Feature_charts)
        *   [2.4.1 Decompress](#Decompress)
*   [3 Usage comparison](#Usage_comparison)
    *   [3.1 Archiving only](#Archiving_only_2)
    *   [3.2 Compression only](#Compression_only_2)
    *   [3.3 Archiving and compression](#Archiving_and_compression_2)
*   [4 Convenience tools](#Convenience_tools)
*   [5 Determining archive format](#Determining_archive_format)
*   [6 See also](#See_also)

## Archiving only

| Name | Packages | Manuals | Description |
| [ar](https://en.wikipedia.org/wiki/ar_(Unix) | [binutils](https://www.archlinux.org/packages/?name=binutils) | [ar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ar.1) | Legacy Unix archiver before *tar*. Today only used for creating [static library](https://en.wikipedia.org/wiki/Static_library "wikipedia:Static library") files. |
| [cpio](https://en.wikipedia.org/wiki/cpio "wikipedia:cpio") | [cpio](https://www.archlinux.org/packages/?name=cpio) | [cpio(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cpio.1) | File archiver via stdin/stdout, supports cpio and tar formats. |
| GNU [tar](https://en.wikipedia.org/wiki/tar_(computing) | [coreutils](https://www.archlinux.org/packages/?name=coreutils) | [tar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tar.1) | GNU utility for manipulating the ubiquitous tar archives (tarballs), see [tar](/index.php/Tar "Tar") for usage examples. |
| [libarchive](http://libarchive.org/) | [libarchive](https://www.archlinux.org/packages/?name=libarchive) | [bsdtar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bsdtar.1)
[bsdcpio(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bsdcpio.1) | Implementation of *tar* and *cpio* that also offers a library. Used by [pacman](/index.php/Pacman "Pacman") and [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"). |

**Tip:** Both GNU and BSD tar automatically do decompression delegation for bzip2, compress, gzip, lzip, lzma and xz compressed archives. When creating archives both support the `-a` switch to automatically filter the created archive through the right compression program based on the file extension. While BSD tar recognizes compression formats based on the format, GNU tar only guesses based on the file extension.

## Compression tools

### Compression only

These compression programs implement their own file format.

| Name | Packages | Manual | Ext | Tar ext | Description | Parallel implementations |
| [bzip2](https://en.wikipedia.org/wiki/bzip2 "wikipedia:bzip2") | [bzip2](https://www.archlinux.org/packages/?name=bzip2) | [bzip2(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bzip2.1) | .bz2, .bz | .tbz2, .tbz | Uses the [Burrows–Wheeler algorithm](https://en.wikipedia.org/wiki/Burrows%E2%80%93Wheeler_transform "wikipedia:Burrows–Wheeler transform"). | [lbzip2](https://www.archlinux.org/packages/?name=lbzip2), [pbzip2](https://www.archlinux.org/packages/?name=pbzip2) |
| [gzip](https://en.wikipedia.org/wiki/gzip "wikipedia:gzip") | [gzip](https://www.archlinux.org/packages/?name=gzip) | [gzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gzip.1) | .gz, .z | .tgz, .taz | GNU zip, based on [DEFLATE](https://en.wikipedia.org/wiki/DEFLATE "wikipedia:DEFLATE") algorithm. | [pigz](https://www.archlinux.org/packages/?name=pigz) |
| [lrzip](/index.php/Lrzip "Lrzip") | [lrzip](https://www.archlinux.org/packages/?name=lrzip) | [lrzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lrzip.1) | .lrz | Improved version of [rzip](https://en.wikipedia.org/wiki/rzip "wikipedia:rzip"), uses multiple algorithms. | is multithreaded |
| [lzip](https://en.wikipedia.org/wiki/lzip "wikipedia:lzip") | [lzip](https://www.archlinux.org/packages/?name=lzip) | [lzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lzip.1) | .lz | Uses [LZMA](https://en.wikipedia.org/wiki/LZMA "wikipedia:LZMA"). |
| [lzop](https://en.wikipedia.org/wiki/lzop "wikipedia:lzop") | [lzop](https://www.archlinux.org/packages/?name=lzop) | [lzop(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lzop.1) | .lzop | .tzo | Uses [LZO](https://en.wikipedia.org/wiki/Lempel%E2%80%93Ziv%E2%80%93Oberhumer "wikipedia:Lempel–Ziv–Oberhumer"). |
| [xz](https://en.wikipedia.org/wiki/xz "wikipedia:xz") | [xz](https://www.archlinux.org/packages/?name=xz) | [xz(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xz.1) | .xz, .lzma | .txz, .tlz | Uses [LZMA](https://en.wikipedia.org/wiki/LZMA "wikipedia:LZMA"), default for GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) and kernel archive files. | [pixz](https://www.archlinux.org/packages/?name=pixz), [pxz](https://aur.archlinux.org/packages/pxz/) |

*   Parallel implementations offer improved speeds by using multiple CPU cores.
*   Tar extensions refers to compressed archives where `tar` and the compression tool is used, e.g. `.tzo` is `.tar.lzo`.

### Archiving and compression

| Name | Packages | Manual | Ext | Description |
| [7z](https://en.wikipedia.org/wiki/7z "wikipedia:7z") | [p7zip](https://www.archlinux.org/packages/?name=p7zip) | [7z(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/7z.1) | .7z | Popular OpenSource tool on non-Linux machines. See [p7zip](/index.php/P7zip "P7zip"). |
| [RAR](https://en.wikipedia.org/wiki/RAR_(file_format) | [rar](https://aur.archlinux.org/packages/rar/), [unrar](https://www.archlinux.org/packages/?name=unrar) | rar(1) | .rar | Popular Windows tool available for Linux. See [RAR](/index.php/RAR "RAR"). |
| [ZIP](https://en.wikipedia.org/wiki/Zip_(file_format) | [zip](https://www.archlinux.org/packages/?name=zip), [unzip](https://www.archlinux.org/packages/?name=unzip) | [zip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zip.1), [unzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/unzip.1) | .zip | Widely used outside of the Linux-world. |
| [Unarchiver](https://theunarchiver.com/) | [unarchiver](https://www.archlinux.org/packages/?name=unarchiver) | [unar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/unar.1), [lsar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsar.1) | *many* | Command-line tool of a Mac application, supports over 40 archive formats. |

### Esoteric, rare or deprecated tools

| Name | Packages | Ext | Description |
| [ARC](https://en.wikipedia.org/wiki/ARC_(file_format) | [arc](https://aur.archlinux.org/packages/arc/) | .arc, .ark | Was very popular during the early days of the dial-up BBS. Superseded by ZIP. |
| [ARJ](https://en.wikipedia.org/wiki/ARJ "wikipedia:ARJ") | [arj](https://www.archlinux.org/packages/?name=arj) | .arj | An archiver used on DOS/Windows in mid-1990s. This is an open source clone. |
| [compress](https://en.wikipedia.org/wiki/compress "wikipedia:compress") | [ncompress](https://aur.archlinux.org/packages/ncompress/) | .Z | The classic unix compression utility which can handle the ancient .Z archive. |
| [PAR2](https://en.wikipedia.org/wiki/Parchive "wikipedia:Parchive") | [par2cmdline](https://www.archlinux.org/packages/?name=par2cmdline) | .par2 | Parity archiver for increased data integrity. See also [Parchive](/index.php/Parchive "Parchive"). |
| [shar](https://en.wikipedia.org/wiki/shar "wikipedia:shar") | [sharutils](https://www.archlinux.org/packages/?name=sharutils) | .shar | Creates self-extracting archives that are valid shell scripts. |

### Feature charts

#### Decompress

| Name | gzip | bzip2 | ZIP | compress | pack | CAB | ARJ |
| [gzip](https://www.archlinux.org/packages/?name=gzip) | Yes | No | Yes | Yes | Yes | No | No |
| [p7zip](https://www.archlinux.org/packages/?name=p7zip) | Yes | Yes | Yes | No | Yes | Yes | Yes |
| [unarchiver](https://www.archlinux.org/packages/?name=unarchiver) | Yes | Yes | Yes | Yes | No | Yes | partial |

## Usage comparison

### Archiving only

| Name | Create archive | Extract archive | List content |
| [tar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tar.1) | `tar cfv archive.tar file1 file2` | `tar xfv archive.tar` | `tar -tvf archive.tar` |
| [cpio(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cpio.1) | `ls file1 file2 | cpio -o > archive.cpio` | `cpio -i -vd < archive.cpio` | `cpio -t < archive.cpio` |

### Compression only

| Name | Compress | Decompress | Decompress to stdout |
| [bzip2(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bzip2.1) | `bzip2 file` | `bzip2 -d file.bz2` | `bzcat file.bz2` |
| [gzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gzip.1) | `gzip file` | `gzip -d file.gz` | `zcat file.gz` |
| [lrzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lrzip.1) | `lrzip file`
`lrztar folder` | `lrzip -d file.lrz`
`lrztar -d folder.tar.lrz` | `lrzcat file.lrz` |
| [xz(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xz.1) | `xz file` | `xz -d file.xz` | `xzcat file.xz` |

### Archiving and compression

| Name | Compress | Decompress | Decompress to stdout | List content |
| [7z(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/7z.1) | `7z a archive.7z file1 file2` | `7z x archive.7z` | `7z e -so archive.7z file1` | `7z l archive.7z` |
| rar(1) & unrar | `rar a archive.rar file1 file2` | `rar x archive.rar` | `rar p -inul archive.rar file1` | `rar l archive.rar` |
| [zip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zip.1), [unzip(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/unzip.1) | `zip archive.zip file1 file2` | `unzip archive.zip` | `unzip -p archive.zip file1` | `unzip -l archive.zip` |

## Convenience tools

*   **atool** — Script for managing file archives of various types.

	[https://www.nongnu.org/atool/](https://www.nongnu.org/atool/) || [atool](https://www.archlinux.org/packages/?name=atool)

*   **dtrx** — An intelligent archive extraction tool.

	[https://brettcsmith.org/2007/dtrx/](https://brettcsmith.org/2007/dtrx/) || [dtrx](https://aur.archlinux.org/packages/dtrx/)

*   **unp** — Command line tool that can unpack archives easily.

	[https://github.com/mitsuhiko/unp](https://github.com/mitsuhiko/unp) || [python-unp](https://aur.archlinux.org/packages/python-unp/)

*   **unpack** — Wrapper script for handling multiple archive formats.

	[https://github.com/githaff/unpack](https://github.com/githaff/unpack) || [unpack-git](https://aur.archlinux.org/packages/unpack-git/)

*   [Bash/Functions#Extract](/index.php/Bash/Functions#Extract "Bash/Functions")

## Determining archive format

To extract an archive, its file format needs to be determined. If the file is properly named you can deduce its format from the file extension.

Otherwise you can use the [file](https://www.archlinux.org/packages/?name=file) tool, see [file(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/file.1).

## See also

*   [List of applications/Utilities#Archiving and compression tools](/index.php/List_of_applications/Utilities#Archiving_and_compression_tools "List of applications/Utilities")
*   [Wikipedia:Comparison of file archivers](https://en.wikipedia.org/wiki/Comparison_of_file_archivers "wikipedia:Comparison of file archivers")
*   [Wikipedia:List of archive formats](https://en.wikipedia.org/wiki/List_of_archive_formats "wikipedia:List of archive formats")
*   [Wikipedia:Comparison of archive formats](https://en.wikipedia.org/wiki/Comparison_of_archive_formats "wikipedia:Comparison of archive formats")
*   [List of applications/Multimedia#Image compression](/index.php/List_of_applications/Multimedia#Image_compression "List of applications/Multimedia")