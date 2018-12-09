**Estado de la traducción**
Este artículo es una traducción de [FUSE](/index.php/FUSE "FUSE"), revisada por última vez el **2018-11-10**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=FUSE&diff=0&oldid=554482) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

El [sistema de archivos en el espacio de usuario](https://en.wikipedia.org/wiki/es:Sistema_de_archivos_en_el_espacio_de_usuario "wikipedia:es:Sistema de archivos en el espacio de usuario") (FUSE) es un mecanismo para sistemas operativos similares a Unix que permite a los usuarios sin privilegios de root crear sus propios sistemas de archivos sin editar el código del kernel. Esto se logra ejecutando el código del sistema de archivos en el *espacio de usuario*, mientras que el módulo del kernel FUSE proporciona solo un «puente» a las interfaces reales del kernel.

## Desmontaje

Los sistemas de archivos FUSE se pueden desmontar con:

```
$ fusermount -u *punto_de_montaje*

```

## Lista de sistemas de archivos FUSE

*   **adbfs-git** — Monta un dispositivo Android conectado a través de USB..

	[http://collectskin.com/adbfs/](http://collectskin.com/adbfs/) || [adbfs-git](https://aur.archlinux.org/packages/adbfs-git/)

*   **apfs-fuse-git** — Controlador de FUSE para APFS (sistema de archivos de Apple).

	[https://github.com/sgan81/apfs-fuse](https://github.com/sgan81/apfs-fuse) || [apfs-fuse-git](https://aur.archlinux.org/packages/apfs-fuse-git/)

*   **CloudFusion** — Sistema de archivos Linux (FUSE) para acceder a los servidores Dropbox, Sugarsync, Amazon S3, Google Drive o WebDAV.

	[https://joe42.github.io/CloudFusion/](https://joe42.github.io/CloudFusion/) || [cloudfusion-git](https://aur.archlinux.org/packages/cloudfusion-git/)

*   **[CurlFtpFS](/index.php/CurlFtpFS "CurlFtpFS")** — Sistema de archivos para acceder a servidores FTP basados ​​en FUSE y libcurl.

	[http://curlftpfs.sourceforge.net/](http://curlftpfs.sourceforge.net/) || [curlftpfs](https://www.archlinux.org/packages/?name=curlftpfs)

*   **[davfs2](/index.php/Davfs2 "Davfs2")** — Controlador del sistema de archivos que permite montar una carpeta WebDAV.

	[https://savannah.nongnu.org/projects/davfs2](https://savannah.nongnu.org/projects/davfs2) || [davfs2](https://www.archlinux.org/packages/?name=davfs2)

*   **[EncFS](/index.php/EncFS "EncFS")** — Sistema de archivos criptográfico apilable del espacio del usuario.

	[https://vgough.github.io/encfs/](https://vgough.github.io/encfs/) || [encfs](https://www.archlinux.org/packages/?name=encfs)

*   **fuseiso** — Monta una ISO como usuario regular.

	[http://sourceforge.net/projects/fuseiso/](http://sourceforge.net/projects/fuseiso/) || [fuseiso](https://www.archlinux.org/packages/?name=fuseiso)

*   **GDriveFS** — [Wrapper](/index.php?title=Wikiprfis:esWrapper&action=edit&redlink=1 "Wikiprfis:esWrapper (page does not exist)") innovador de FUSE para Google Drive..

	[https://github.com/dsoprea/GDriveFS](https://github.com/dsoprea/GDriveFS) || [gdrivefs](https://aur.archlinux.org/packages/gdrivefs/)

*   **[gitfs](/index.php/Gitfs "Gitfs")** — gitfs es un sistema de archivos FUSE que se integra completamente con git.

	[https://www.presslabs.com/gitfs/](https://www.presslabs.com/gitfs/) || [gitfs](https://aur.archlinux.org/packages/gitfs/)

*   **[gocryptfs](/index.php/Gocryptfs "Gocryptfs")** — gocryptfs es un sistema de archivos criptográfico apilable de espacio de usuario.

	[https://nuetzlich.net/gocryptfs/](https://nuetzlich.net/gocryptfs/) || [gocryptfs](https://www.archlinux.org/packages/?name=gocryptfs)

*   **google-drive-ocamlfuse** — Sistema de archivos basado en FUSE respaldado por Google Drive, escrito en OCaml.

	[https://astrada.github.io/google-drive-ocamlfuse/](https://astrada.github.io/google-drive-ocamlfuse/) || [google-drive-ocamlfuse](https://aur.archlinux.org/packages/google-drive-ocamlfuse/)

*   **gphotofs** — Módulo de FUSE para montar la cámara como un sistema de archivos.

	[http://www.gphoto.org/proj/gphotofs/](http://www.gphoto.org/proj/gphotofs/) || [gphotofs](https://aur.archlinux.org/packages/gphotofs/)

*   **MegaFuse** — Cliente MEGA para Linux, basado en FUSE.

	[https://github.com/matteoserva/MegaFuse](https://github.com/matteoserva/MegaFuse) || [megafuse-git](https://aur.archlinux.org/packages/megafuse-git/)

*   **s3fs** — Sistema de archivos basado en FUSE respaldado por Amazon S3.

	[https://github.com/s3fs-fuse/s3fs-fuse](https://github.com/s3fs-fuse/s3fs-fuse) || [s3fs-fuse](https://www.archlinux.org/packages/?name=s3fs-fuse)

*   **[SSHFS](/index.php/SSHFS "SSHFS")** — Cliente de sistema de archivos basado en FUSE para montar directorios sobre SSH.

	[https://github.com/libfuse/sshfs](https://github.com/libfuse/sshfs) || [sshfs](https://www.archlinux.org/packages/?name=sshfs)

*   **TMSU** — Una herramienta de línea de órdenes para etiquetar los archivos y acceder a ellos a través de un sistema de archivos virtual.

	[http://tmsu.org/](http://tmsu.org/) || [tmsu](https://aur.archlinux.org/packages/tmsu/)

*   **vdfuse** — Montaje de imágenes de discos de VirtualBox (VDI/VMDK/VHD).

	[https://github.com/muflone/virtualbox-includes](https://github.com/muflone/virtualbox-includes) || [vdfuse](https://aur.archlinux.org/packages/vdfuse/)

*   **xbfuse-git** — Monta una Xbox (360) ISO.

	[http://multimedia.cx/xbfuse/](http://multimedia.cx/xbfuse/) || [xbfuse-git](https://aur.archlinux.org/packages/xbfuse-git/)

*   **xmlfs** — Representa un archivo XML como una estructura de directorio para un fácil acceso.

	[https://github.com/halhen/xmlfs](https://github.com/halhen/xmlfs) || [xmlfs](https://aur.archlinux.org/packages/xmlfs/)

*   [Media Transfer Protocol#FUSE filesystems](/index.php/Media_Transfer_Protocol#FUSE_filesystems "Media Transfer Protocol")

## Véase también

*   [Wikipedia:Filesystem in Userspace#Example uses](https://en.wikipedia.org/wiki/Filesystem_in_Userspace#Example_uses "wikipedia:Filesystem in Userspace")