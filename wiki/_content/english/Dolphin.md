This article is about **Dolphin**, the default [file manager](/index.php/Category:File_managers "Category:File managers") of the [K Desktop Environment](/index.php/K_Desktop_Environment "K Desktop Environment"). For the game emulator, see [Dolphin emu](/index.php/Dolphin_emu "Dolphin emu").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 File previews](#File_previews)
*   [2 Usage](#Usage)
    *   [2.1 Open Terminal](#Open_Terminal)
    *   [2.2 KIO Slaves](#KIO_Slaves)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 No search results](#No_search_results)
    *   [3.2 Transparent fonts](#Transparent_fonts)
    *   [3.3 Unicode characters are not shown](#Unicode_characters_are_not_shown)
    *   [3.4 Crashes on mounted SMB share](#Crashes_on_mounted_SMB_share)
    *   [3.5 Cannot write to NTFS: Operation not permitted](#Cannot_write_to_NTFS:_Operation_not_permitted)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [dolphin](https://www.archlinux.org/packages/?name=dolphin) package, or [dolphinpart4](https://www.archlinux.org/packages/?name=dolphinpart4) for the legacy KDE4 version.

For version control and [Dropbox](/index.php/Dropbox "Dropbox") support, install [dolphin-plugins](https://www.archlinux.org/packages/?name=dolphin-plugins). The *Compare files* dialog depends on [kompare](https://www.archlinux.org/packages/?name=kompare).

### File previews

*   [kdegraphics-thumbnailers](https://www.archlinux.org/packages/?name=kdegraphics-thumbnailers): Image files
*   [kdesdk-thumbnailers](https://www.archlinux.org/packages/?name=kdesdk-thumbnailers): Plugins for the thumbnailing system
*   [ffmpegthumbs](https://www.archlinux.org/packages/?name=ffmpegthumbs): Video files (based on ffmpeg)
*   [raw-thumbnailer](https://www.archlinux.org/packages/?name=raw-thumbnailer): `.raw` files
*   [audiothumbs-frameworks-git](https://aur.archlinux.org/packages/audiothumbs-frameworks-git/) : Audio files
*   [kde-thumbnailer-apk](https://aur.archlinux.org/packages/kde-thumbnailer-apk/): **A**ndroid **a**pplication **p**ackage files
*   [kde-thumbnailer-blender](https://aur.archlinux.org/packages/kde-thumbnailer-blender/): Blender application files
*   [kde-thumbnailer-epub](https://aur.archlinux.org/packages/kde-thumbnailer-epub/): Electronic book files

## Usage

### Open Terminal

Dolphin and other KDE applications use [konsole](https://www.archlinux.org/packages/?name=konsole) by default. To change the default terminal emulator, run `kcmshell4 componentchooser` and select *Terminal Emulator > Use a different terminal program*.

### KIO Slaves

Dolphin uses *KIO slaves* for network access, trash and other functionality, unlike [GTK+](/index.php/GTK%2B "GTK+") file managers which use [GVFS](/index.php/GVFS "GVFS"). Available protocols are shown in the location bar (editable mode) [[1]](https://docs.kde.org/stable/en/applications/dolphin/location-bar.html#location-bar-editable). To quickly bookmark them, right-click in the workspace, and select "Add to Places".

## Troubleshooting

### No search results

If *Baloo* is enabled, Dolphin attempts to use it for file searches even if no file index is present. Either create a Baloo file index, or disable file indexing through `kcmshell4 kcm_baloofile`.

### Transparent fonts

Fonts in selection frames may become transparent when using the [GTK+ Qt style](/index.php/Uniform_look_for_Qt_and_GTK_applications#QGtkStyle "Uniform look for Qt and GTK applications"). Native Qt styles such as *Cleanlooks* and *Oxygen* are unaffected.

### Unicode characters are not shown

This was a general issue in Qt4 and [kdelibs](https://www.archlinux.org/packages/?name=kdelibs), solved in v4.11 and later versions. [[2]](https://bugs.kde.org/show_bug.cgi?id=165044#c145)

### Crashes on mounted SMB share

See [Samba#Unable to overwrite files](/index.php/Samba#Unable_to_overwrite_files.2C_permissions_errors "Samba").

### Cannot write to NTFS: Operation not permitted

If you are not able to do any write operations (create/delete/rename file/folder) as normal user to your NTFS partition, then you probably missing to install the [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) package. See [NTFS-3G](/index.php/NTFS-3G "NTFS-3G") for details.

## See also

*   [Wikipedia:Dolphin (file manager)](https://en.wikipedia.org/wiki/Dolphin_(file_manager) "wikipedia:Dolphin (file manager)")
*   [KDE userbase: Dolphin](https://userbase.kde.org/Dolphin)
*   [Dolphin Handbook](https://docs.kde.org/stable/en/applications/dolphin/index.html)