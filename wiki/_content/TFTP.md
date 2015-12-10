# TFTP

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

The [Trivial File Transfer Protocol](https://en.wikipedia.org/wiki/Trivial_File_Transfer_Protocol "wikipedia:Trivial File Transfer Protocol") (TFTP) provides a minimalistic means for transferring files. It is generally used as a part of [PXE](/index.php/PXE "PXE") booting or for updating configuration and firmware on devices which have limited memory such as routers and printers.

## Server

There are several TFTP server implementations, some listed below.

### tftp-hpa

[Install](/index.php/Install "Install") [tftp-hpa](https://www.archlinux.org/packages/?name=tftp-hpa) and then [start](/index.php/Start "Start") `tftpd.service`.

To modify service parameters edit `/etc/conf.d/tftpd`.

### atftp

[Install](/index.php/Install "Install") [atftp](https://www.archlinux.org/packages/?name=atftp) and then [start](/index.php/Start "Start") `atftpd.service`.

To modify service parameters edit `/etc/conf.d/atftpd`.

Retrieved from "[https://wiki.archlinux.org/index.php?title=TFTP&oldid=409597](https://wiki.archlinux.org/index.php?title=TFTP&oldid=409597)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [File Transfer Protocol](/index.php/Category:File_Transfer_Protocol "Category:File Transfer Protocol")