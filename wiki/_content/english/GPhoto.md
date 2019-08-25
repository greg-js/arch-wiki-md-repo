[Libgphoto2](http://www.gphoto.org/proj/libgphoto2/) is the core library designed to allow access to digital cameras by external (front end) programs, such as Digikam and gphoto2\. The current 'officially' supported cameras are [here](http://www.gphoto.org/proj/libgphoto2/support.php) (though more may work).

This article documents the configuration of `libgphoto2` to access digital cameras. Some digital cameras will mount as normal [USB storage devices](/index.php/USB_storage_devices "USB storage devices") and may not require the use of libgphoto2.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Frontend applications](#Frontend_applications)
*   [2 GPhoto2 usage](#GPhoto2_usage)
    *   [2.1 Example usage with gvfs](#Example_usage_with_gvfs)
*   [3 Permission issues](#Permission_issues)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [libgphoto2](https://www.archlinux.org/packages/?name=libgphoto2) package, and optionally [gphoto2](https://www.archlinux.org/packages/?name=gphoto2) to have a command line interface.

### Frontend applications

*   **[darktable](https://en.wikipedia.org/wiki/darktable "wikipedia:darktable")** — Utility to organize and develop raw images.

	[http://darktable.org/](http://darktable.org/) || [darktable](https://www.archlinux.org/packages/?name=darktable)

*   **[digiKam](/index.php/Digikam "Digikam")** — Digital photo management application for [KDE](/index.php/KDE "KDE").

	[https://www.digikam.org/](https://www.digikam.org/) || [digikam](https://www.archlinux.org/packages/?name=digikam)

*   **Entangle** — Provides a graphical interface for “tethered shooting”, aka taking photographs with a digital camera completely controlled from the computer.

	[https://entangle-photo.org/](https://entangle-photo.org/) || [entangle](https://aur.archlinux.org/packages/entangle/)

*   **gphotofs** — [Fuse](/index.php/Fuse "Fuse") module to mount camera as a filesystem.

	[http://www.gphoto.org/proj/gphotofs/](http://www.gphoto.org/proj/gphotofs/) || [gphotofs](https://aur.archlinux.org/packages/gphotofs/)

*   **[gThumb](https://en.wikipedia.org/wiki/GThumb "wikipedia:GThumb")** — Image browser and viewer for [GNOME](/index.php/GNOME "GNOME").

	[http://wiki.gnome.org/gthumb](http://wiki.gnome.org/gthumb) || [gthumb](https://www.archlinux.org/packages/?name=gthumb)

*   **GTKam** — Graphical [GTK](/index.php/GTK "GTK") 2 front-end to gphoto2.

	[http://www.gphoto.org/proj/gtkam/](http://www.gphoto.org/proj/gtkam/) || [gtkam](https://aur.archlinux.org/packages/gtkam/)

*   **gvfs-gphoto2** — gphoto2 backend for GVfs to mount camera as a filesystem from a file manager that supports GVfs such as [GNOME Files](/index.php/GNOME_Files "GNOME Files"), [Nemo](/index.php/Nemo "Nemo"), [PCManFM](/index.php/PCManFM "PCManFM") and [Thunar](/index.php/Thunar "Thunar").

	[https://wiki.gnome.org/Projects/gvfs](https://wiki.gnome.org/Projects/gvfs) || [gvfs-gphoto2](https://www.archlinux.org/packages/?name=gvfs-gphoto2)

*   **Kamera** — [KDE](/index.php/KDE "KDE") integration for gphoto2 cameras.

	[https://github.com/KDE/kamera](https://github.com/KDE/kamera) || [kamera](https://www.archlinux.org/packages/?name=kamera)

*   **Pantheon Photos** — Image viewer for Pantheon.

	[https://launchpad.net/pantheon-photos](https://launchpad.net/pantheon-photos) || [pantheon-photos](https://www.archlinux.org/packages/?name=pantheon-photos)

*   **Rapid Photo Downloader** — Download photos and videos from cameras, memory cards and portable storage devices.

	[http://www.damonlynch.net/rapid/](http://www.damonlynch.net/rapid/) || [rapid-photo-downloader](https://www.archlinux.org/packages/?name=rapid-photo-downloader)

*   **[Rawstudio](https://en.wikipedia.org/wiki/Rawstudio "wikipedia:Rawstudio")** — An open source raw-image converter written in GTK. Supports tethered shooting with gphoto2.

	[https://rawstudio.org/](https://rawstudio.org/) || [rawstudio](https://aur.archlinux.org/packages/rawstudio/)

*   **[Shotwell](https://en.wikipedia.org/wiki/Shotwell_(software) "wikipedia:Shotwell (software)")** — Digital photo organizer designed for [GNOME](/index.php/GNOME "GNOME").

	[http://wiki.gnome.org/Apps/Shotwell](http://wiki.gnome.org/Apps/Shotwell) || [shotwell](https://www.archlinux.org/packages/?name=shotwell)

## GPhoto2 usage

GPhoto2 is a command line client for libgphoto2\. GPhoto2 allows access to the libgphoto2 library from a terminal or from a script shell to perform any camera operation that can be done. This is the main user interface.

GPhoto2 also provides convenient debugging features for camera driver developers.

**Quick Commands**

*   `gphoto2 --list-ports`
*   `gphoto2 --auto-detect`
*   `gphoto2 --summary`
*   `gphoto2 --list-files`
*   `gphoto2 --get-all-files`
*   `gphoto2 --set-config datetime=now` - sets the camera to the current time

For advanced file manipulation, use

*   `gphoto2 --shell`

### Example usage with gvfs

Auto detect the connected camera and list the required port:

```
$ gphoto2 --auto-detect
Model                          Port                                            
----------------------------------------------------------
Canon Digital IXUS 980 IS      usb:006,011 

```

Now open your favorite file manager and enter the address with the found port detail "gphoto2://[usb:006,011]" - the camera will be mounted with gvfs and can be managed with the file manager.

## Permission issues

Users with a local session have permissions granted for cameras using [ACLs](https://en.wikipedia.org/wiki/Access_control_list "wikipedia:Access control list"). See [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") if it does not work.

## See also

*   [A list of cameras supported by gPhoto](http://www.gphoto.org/proj/libgphoto2/support.php)
*   [another more detailed list](http://www.teaser.fr/~hfiguiere/linux/digicam.html)