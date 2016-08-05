This article documents the configuration of `libgphoto2` to access digital cameras. Some digital cameras will mount as normal [USB storage devices](/index.php/USB_storage_devices "USB storage devices") and may not require the use of libgphoto2.

## Contents

*   [1 libgphoto2](#libgphoto2)
    *   [1.1 Installation](#Installation)
    *   [1.2 Permission issues](#Permission_issues)
    *   [1.3 GPhoto2 usage](#GPhoto2_usage)
        *   [1.3.1 Other frontend applications for libgphoto2](#Other_frontend_applications_for_libgphoto2)
*   [2 See also](#See_also)

## libgphoto2

[Libgphoto2](http://www.gphoto.org/proj/libgphoto2/) is the core library designed to allow access to digital cameras by external (front end) programs, such as Digikam and gphoto2\. The current 'officially' supported cameras are [here](http://www.gphoto.org/proj/libgphoto2/support.php) (though more may work).

### Installation

[Install](/index.php/Install "Install") the [libgphoto2](https://www.archlinux.org/packages/?name=libgphoto2) package, and optionally [gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2) for [GNOME Files](/index.php/GNOME_Files "GNOME Files") integration and [gphoto2](https://www.archlinux.org/packages/?name=gphoto2) to have a command line interface. Actually, any package that lists [gvfs](https://www.archlinux.org/packages/?name=gvfs) as a dependency can use gvfs-gphoto2, such as [Nemo](/index.php/Nemo "Nemo"), [PCManFM](/index.php/PCManFM "PCManFM"), and [Thunar](/index.php/Thunar "Thunar").

### Permission issues

Users with a local session have permissions granted for cameras using [ACLs](https://en.wikipedia.org/wiki/Access_control_list "wikipedia:Access control list"). See [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") if it does not work.

### GPhoto2 usage

GPhoto2 is a command line client for libgphoto2\. GPhoto2 allows access to the libgphoto2 library from a terminal or from a script shell to perform any camera operation that can be done. This is the main user interface.

GPhoto2 also provides convenient debugging features for camera driver developers.

**Quick Commands**

*   `gphoto2 --list-ports`
*   `gphoto2 --auto-detect`
*   `gphoto2 --summary`
*   `gphoto2 --list-files`
*   `gphoto2 --get-all-files`

For advanced file manipulation, use

*   `gphoto2 --shell`

#### Other frontend applications for libgphoto2

*   [gphotofs](http://www.gphoto.org/proj/gphotofs/) - [gphotofs](https://aur.archlinux.org/packages/gphotofs/) - FUSE ([fuse](https://www.archlinux.org/packages/?name=fuse)) module to mount camera as a filesystem
*   [darktable](http://darktable.org/) - [darktable](https://www.archlinux.org/packages/?name=darktable) - utility to organize and develop raw images
*   [Digikam](/index.php/Digikam "Digikam") - [digikam](https://www.archlinux.org/packages/?name=digikam) - digital photo management application for [KDE](/index.php/KDE "KDE")
*   [F-Spot](http://f-spot.org/) - photo management [Mono](/index.php/Mono "Mono") application for [GNOME](/index.php/GNOME "GNOME")
*   [Gthumb](http://live.gnome.org/gthumb) - [gthumb](https://www.archlinux.org/packages/?name=gthumb) - image browser and viewer for [GNOME](/index.php/GNOME "GNOME")
*   [GTKam](http://www.gphoto.org/proj/gtkam/) - [gtkam](https://aur.archlinux.org/packages/gtkam/) - graphical [GTK](/index.php/GTK "GTK") front-end to gphoto2
*   [Pantheon Photos](https://launchpad.net/pantheon-photos) - [pantheon-photos](https://www.archlinux.org/packages/?name=pantheon-photos) - "continuation" of Shotwell for [Pantheon](/index.php/Pantheon "Pantheon")
*   [Shotwell](http://wiki.gnome.org/Apps/Shotwell) - [shotwell](https://www.archlinux.org/packages/?name=shotwell) - digital photo organizer designed for [GNOME](/index.php/GNOME "GNOME")
*   [GNOME Files](/index.php/GNOME_Files "GNOME Files") - Supports accessing digital cameras and smartphones using MTP, and has two backends: the new [gvfs-mtp](https://www.archlinux.org/packages/?name=gvfs-mtp) using libmtp, and the old [gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2) using libgphoto2.

## See also

*   [A list of cameras supported by gPhoto](http://www.gphoto.org/proj/libgphoto2/support.php)
*   [another more detailed list](http://www.teaser.fr/~hfiguiere/linux/digicam.html)