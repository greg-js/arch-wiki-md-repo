[Filesystem in Userspace](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") (FUSE) is a mechanism for Unix-like operating systems that lets non-privileged users create their own file systems without editing kernel code. This is achieved by running file system code in *user space*, while the FUSE kernel module provides only a "bridge" to the actual kernel interfaces.

## Unmounting

FUSE filesystems can be unmounted with:

```
$ fusermount -u *mountpoint*

```

## List of FUSE filesystems

*   **adbfs-git** — Mount an Android device connected via USB.

	[http://collectskin.com/adbfs/](http://collectskin.com/adbfs/) || [adbfs-git](https://aur.archlinux.org/packages/adbfs-git/)

*   **apfs-fuse-git** — FUSE driver for APFS (Apple File System).

	[https://github.com/sgan81/apfs-fuse](https://github.com/sgan81/apfs-fuse) || [apfs-fuse-git](https://aur.archlinux.org/packages/apfs-fuse-git/)

*   **CloudFusion** — Linux file system (FUSE) to access Dropbox, Sugarsync, Amazon S3, Google Drive or WebDAV servers.

	[https://joe42.github.io/CloudFusion/](https://joe42.github.io/CloudFusion/) || [cloudfusion-git](https://aur.archlinux.org/packages/cloudfusion-git/)

*   **[CurlFtpFS](/index.php/CurlFtpFS "CurlFtpFS")** — Filesystem for accessing FTP hosts based on FUSE and libcurl.

	[http://curlftpfs.sourceforge.net/](http://curlftpfs.sourceforge.net/) || [curlftpfs](https://www.archlinux.org/packages/?name=curlftpfs)

*   **[davfs2](/index.php/Davfs2 "Davfs2")** — File system driver that allows you to mount a WebDAV folder.

	[https://savannah.nongnu.org/projects/davfs2](https://savannah.nongnu.org/projects/davfs2) || [davfs2](https://www.archlinux.org/packages/?name=davfs2)

*   **[EncFS](/index.php/EncFS "EncFS")** — Userspace stackable cryptographic file-system.

	[https://vgough.github.io/encfs/](https://vgough.github.io/encfs/) || [encfs](https://www.archlinux.org/packages/?name=encfs)

*   **fuseiso** — Mount an ISO as a regular user.

	[http://sourceforge.net/projects/fuseiso/](http://sourceforge.net/projects/fuseiso/) || [fuseiso](https://www.archlinux.org/packages/?name=fuseiso)

*   **GDriveFS** — Innovative FUSE wrapper for Google Drive.

	[https://github.com/dsoprea/GDriveFS](https://github.com/dsoprea/GDriveFS) || [gdrivefs](https://aur.archlinux.org/packages/gdrivefs/)

*   **[gitfs](/index.php/Gitfs "Gitfs")** — gitfs is a FUSE file system that fully integrates with git.

	[https://www.presslabs.com/gitfs/](https://www.presslabs.com/gitfs/) || [gitfs](https://aur.archlinux.org/packages/gitfs/)

*   **[gocryptfs](/index.php/Gocryptfs "Gocryptfs")** — gocryptfs is a userspace stackable cryptographic file-system.

	[https://nuetzlich.net/gocryptfs/](https://nuetzlich.net/gocryptfs/) || [gocryptfs](https://www.archlinux.org/packages/?name=gocryptfs)

*   **google-drive-ocamlfuse** — FUSE-based file system backed by Google Drive, written in OCaml.

	[https://astrada.github.io/google-drive-ocamlfuse/](https://astrada.github.io/google-drive-ocamlfuse/) || [google-drive-ocamlfuse](https://aur.archlinux.org/packages/google-drive-ocamlfuse/)

*   **gphotofs** — FUSE module to mount camera as a filesystem.

	[http://www.gphoto.org/proj/gphotofs/](http://www.gphoto.org/proj/gphotofs/) || [gphotofs](https://aur.archlinux.org/packages/gphotofs/)

*   **MegaFuse** — MEGA client for Linux, based on FUSE.

	[https://github.com/matteoserva/MegaFuse](https://github.com/matteoserva/MegaFuse) || [megafuse-git](https://aur.archlinux.org/packages/megafuse-git/)

*   **s3fs** — FUSE-based file system backed by Amazon S3.

	[https://github.com/s3fs-fuse/s3fs-fuse](https://github.com/s3fs-fuse/s3fs-fuse) || [s3fs-fuse](https://www.archlinux.org/packages/?name=s3fs-fuse)

*   **[SSHFS](/index.php/SSHFS "SSHFS")** — FUSE-based filesystem client for mounting directories over SSH.

	[https://github.com/libfuse/sshfs](https://github.com/libfuse/sshfs) || [sshfs](https://www.archlinux.org/packages/?name=sshfs)

*   **TMSU** — A command-line tool for tagging your files and accessing them through a virtual filesystem.

	[http://tmsu.org/](http://tmsu.org/) || [tmsu](https://aur.archlinux.org/packages/tmsu/)

*   **vdfuse** — Mounting VirtualBox disk images (VDI/VMDK/VHD).

	[https://github.com/muflone/virtualbox-includes](https://github.com/muflone/virtualbox-includes) || [vdfuse](https://aur.archlinux.org/packages/vdfuse/)

*   **xbfuse-git** — Mount an Xbox (360) ISO.

	[http://multimedia.cx/xbfuse/](http://multimedia.cx/xbfuse/) || [xbfuse-git](https://aur.archlinux.org/packages/xbfuse-git/)

*   **xmlfs** — Represent an XML file as a directory structure for easy access.

	[https://github.com/halhen/xmlfs](https://github.com/halhen/xmlfs) || [xmlfs](https://aur.archlinux.org/packages/xmlfs/)

*   [Media Transfer Protocol#FUSE filesystems](/index.php/Media_Transfer_Protocol#FUSE_filesystems "Media Transfer Protocol")

## See also

*   [Wikipedia:Filesystem in Userspace#Example uses](https://en.wikipedia.org/wiki/Filesystem_in_Userspace#Example_uses "wikipedia:Filesystem in Userspace")