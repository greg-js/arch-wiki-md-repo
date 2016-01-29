# Arch filesystem hierarchy

Related articles

*   [ABS](/index.php/ABS "ABS")
*   [File systems](/index.php/File_systems "File systems")
*   [Pacman](/index.php/Pacman "Pacman")
*   [Partitioning](/index.php/Partitioning "Partitioning")

Arch Linux is among the many distributions that follow the [filesystem hierarchy standard (FHS)](http://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html). For an explanation of each directory along with their designations, see the [man page](/index.php/Man_page "Man page") of `file-hierarchy`. Note that Arch follows the [systemd](/index.php/Systemd "Systemd") FHS convention of symlinking `/bin`, `/sbin`, and `/usr/sbin` to `/usr/bin`. Additionally, `/lib` (and `/lib64` if applicable) are symlinks to `/usr/lib`. The [ABS](/index.php/ABS "ABS") tree (`/var/abs`) and pacman package cache (`/var/cache/pacman/pkg`) are two notable Arch-specific modifications. Additionally `/usr/local` is empty by default, and since [pacman](/index.php/Pacman "Pacman") installs to the `/usr` directory, manually compiled/installed software installed to `/usr/local` may peacefully co-exist with pacman-tracked system software.

## See also

*   [wikipedia:Filesystem Hierarchy Standard](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard "wikipedia:Filesystem Hierarchy Standard")
*   [Linux FHS Homepage](http://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Arch_filesystem_hierarchy&oldid=394878](https://wiki.archlinux.org/index.php?title=Arch_filesystem_hierarchy&oldid=394878)"