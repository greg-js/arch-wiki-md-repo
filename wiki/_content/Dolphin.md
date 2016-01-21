# Dolphin

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [File manager functionality](/index.php/File_manager_functionality "File manager functionality")
*   [KDE](/index.php/KDE "KDE")
*   [udisks](/index.php/Udisks "Udisks")

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Expand on the KDE5 version (Discuss in [Talk:Dolphin#File previews](https://wiki.archlinux.org/index.php/Talk:Dolphin#File_previews))

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
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [dolphinpart4](https://www.archlinux.org/packages/?name=dolphinpart4) package. For version control and [Dropbox](/index.php/Dropbox "Dropbox") support, install [dolphin-plugins](https://www.archlinux.org/packages/?name=dolphin-plugins). The _Compare files_ dialog depends on [kompare](https://www.archlinux.org/packages/?name=kompare).

### File previews

*   [kdegraphics-thumbnailers](https://www.archlinux.org/packages/?name=kdegraphics-thumbnailers): Image files
*   [kdesdk-thumbnailers](https://www.archlinux.org/packages/?name=kdesdk-thumbnailers): Plugins for the thumbnailing system
*   [kdemultimedia-mplayerthumbs](https://www.archlinux.org/packages/?name=kdemultimedia-mplayerthumbs): Video files
*   [raw-thumbnailer](https://www.archlinux.org/packages/?name=raw-thumbnailer): `.raw` files
*   [audiothumbs](https://aur.archlinux.org/packages/audiothumbs/)<sup><small>AUR</small></sup>: Audio files
*   [kde-thumbnailer-apk](https://aur.archlinux.org/packages/kde-thumbnailer-apk/)<sup><small>AUR</small></sup>: **A**ndroid **a**pplication **p**ackage files
*   [kde-thumbnailer-blender](https://aur.archlinux.org/packages/kde-thumbnailer-blender/)<sup><small>AUR</small></sup>: Blender application files
*   [kde-thumbnailer-epub](https://aur.archlinux.org/packages/kde-thumbnailer-epub/)<sup><small>AUR</small></sup>: Electronic book files

## Usage

### Open Terminal

Dolphin and other KDE applications use [konsole](https://www.archlinux.org/packages/?name=konsole) by default. To change the default terminal emulator, run `kcmshell4 componentchooser` and select _Terminal Emulator > Use a different terminal program_.

### KIO Slaves

Dolphin uses _KIO slaves_ for network access, trash and other functionality, unlike [GTK+](/index.php/GTK%2B "GTK+") file managers which use [GVFS](/index.php/GVFS "GVFS"). Available protocols are shown in the location bar (editable mode) [[1]](https://docs.kde.org/stable/en/applications/dolphin/location-bar.html#location-bar-editable). To quickly bookmark them, right-click in the workspace, and select "Add to Places".

## Troubleshooting

### No search results

If _Baloo_ is enabled, Dolphin attempts to use it for file searches even if no file index is present. Either create a Baloo file index, or disable file indexing through `kcmshell4 kcm_baloofile`.

### Transparent fonts

Fonts in selection frames may become transparent when using the [GTK+ Qt style](/index.php/Uniform_look_for_Qt_and_GTK_applications#QGtkStyle "Uniform look for Qt and GTK applications"). Native Qt styles such as _Cleanlooks_ and _Oxygen_ are unaffected.

### Unicode characters are not shown

This was a general issue in Qt4 and [kdelibs](https://www.archlinux.org/packages/?name=kdelibs), solved in v4.11 and later versions. [[2]](https://bugs.kde.org/show_bug.cgi?id=165044#c145)

## See also

*   [Wikipedia:Dolphin (file manager)](https://en.wikipedia.org/wiki/Dolphin_(file_manager) "wikipedia:Dolphin (file manager)")
*   [KDE userbase: Dolphin](https://userbase.kde.org/Dolphin)
*   [Dolphin Handbook](https://docs.kde.org/stable/en/applications/dolphin/index.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dolphin&oldid=416173](https://wiki.archlinux.org/index.php?title=Dolphin&oldid=416173)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [File managers](/index.php/Category:File_managers "Category:File managers")

Hidden category:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")