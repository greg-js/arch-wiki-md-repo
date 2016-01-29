# FtpFs

From [Wikipedia](http://en.wikipedia.org/wiki/FTPFS):

NaN

The old implementation (ftpfs) was replaced by [LUFS](http://lufs.sourceforge.net/) (UserLand FileSystem), which in turn was made obsolete by [FUSE](http://fuse.sourceforge.net/) (Filesystem in Userspace).

Two ftpfs implementations exist today: **fuseftp** and **lufis/ftpfs**. Fuseftp is quite unusable IMO, and lufis is not supported by Arch Linux -- but it is possible to make it work.

**Note:** the recommended way to mount ftp is with [CurlFtpFS](/index.php/CurlFtpFS "CurlFtpFS").

## Contents

*   [1 Fuseftp](#Fuseftp)
    *   [1.1 Installation](#Installation)
    *   [1.2 Usage example](#Usage_example)
*   [2 LUFIS / ftpfs](#LUFIS_.2F_ftpfs)
    *   [2.1 To install](#To_install)
    *   [2.2 Usage example](#Usage_example_2)

## Fuseftp

[Fuseftp](http://freshmeat.net/projects/fuseftp/) is a FTP filesystem written in Perl, based on FUSE.

### Installation

You can get it from the [AUR](https://aur.archlinux.org/packages.php?do_Details=1&ID=3069). It's useful to install the dependencies with CPAN.

### Usage example

Mount:

```
# fuseftp /mnt/ftp_local/ ftp.example.com  --cache=memory --passive

```

Unmount:

```
# fusermount -u /mnt/ftp_local

```

Refer to the Fuseftp website for more examples and information.

## LUFIS / ftpfs

To use LUFS modules with 2.6x kernel, You will need a bridge called [LUFIS](http://sourceforge.net/project/showfiles.php?group_id=121684&package_id=132803).

### To install

*   Get LUFS [tar.gz](http://prdownloads.sourceforge.net/lufs/lufs-0.9.7.tar.gz?download)
*   `./configure`, `make`, `make install`
*   Copy the "liblufs-ftpfs.so*" files from MAKEDIR/filesystems/ftpfs to /usr/lib
*   [Install](/index.php/Install "Install") the [fuse](https://www.archlinux.org/packages/?name=fuse) package.
*   Get LUFIS [tar.gz](http://prdownloads.sourceforge.net/fuse/lufis-0.3.tar.gz?download)
*   `./configure`, `make`, then copy lufis to /usr/bin

### Usage example

Mount:

```
# lufis fs=ftpfs,host=ftp.exaple.com,username=USERNAME,password=ABCD /mnt/ftp_local/ -s

```

Unmount:

```
# fusermount -u /mnt/ftp_local

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=FtpFs&oldid=378842](https://wiki.archlinux.org/index.php?title=FtpFs&oldid=378842)"