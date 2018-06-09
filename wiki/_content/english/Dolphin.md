Related articles

*   [File manager functionality](/index.php/File_manager_functionality "File manager functionality")
*   [KDE](/index.php/KDE "KDE")
*   [udisks](/index.php/Udisks "Udisks")

[Dolphin](https://www.kde.org/applications/system/dolphin/) is the default file manager of [KDE](/index.php/KDE "KDE"). For the video game console emulator, see [Dolphin emulator](/index.php/Dolphin_emulator "Dolphin emulator").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Compare files](#Compare_files)
    *   [1.2 File previews](#File_previews)
*   [2 Usage](#Usage)
    *   [2.1 Open Terminal](#Open_Terminal)
    *   [2.2 KIO Slaves](#KIO_Slaves)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Device names shown as "X GiB Harddrive"](#Device_names_shown_as_.22X_GiB_Harddrive.22)
    *   [3.2 Transparent fonts](#Transparent_fonts)
    *   [3.3 Crashes on mounted SMB share](#Crashes_on_mounted_SMB_share)
    *   [3.4 Icons not showing](#Icons_not_showing)
    *   [3.5 Mismatched folder view background colors](#Mismatched_folder_view_background_colors)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [dolphin](https://www.archlinux.org/packages/?name=dolphin) package.

For version control and [Dropbox](/index.php/Dropbox "Dropbox") support, install [dolphin-plugins](https://www.archlinux.org/packages/?name=dolphin-plugins). To enable the relevant plugin go to *Control > Configure Dolphin... > Services*.

### Compare files

The *Compare files* dialog depends on [kompare](https://www.archlinux.org/packages/?name=kompare). Alternatively, you can compare files in any diff tool (such as meld) by selecting two files, right clicking, selecting open with, and then the diff tool.

### File previews

*   [kdegraphics-thumbnailers](https://www.archlinux.org/packages/?name=kdegraphics-thumbnailers): Image files and PDFs
*   [kimageformats](https://www.archlinux.org/packages/?name=kimageformats): Gimp *.xcf* files
*   [kdesdk-thumbnailers](https://www.archlinux.org/packages/?name=kdesdk-thumbnailers): Plugins for the thumbnailing system
*   [ffmpegthumbs](https://www.archlinux.org/packages/?name=ffmpegthumbs): Video files (based on ffmpeg)
*   [raw-thumbnailer](https://www.archlinux.org/packages/?name=raw-thumbnailer): *.raw* files
*   [taglib](https://www.archlinux.org/packages/?name=taglib) : Audio files
*   [kde-thumbnailer-apk](https://aur.archlinux.org/packages/kde-thumbnailer-apk/): **A**ndroid **a**pplication **p**ackage files
*   [kde-thumbnailer-blender](https://aur.archlinux.org/packages/kde-thumbnailer-blender/): Blender application files
*   [kde-thumbnailer-epub](https://aur.archlinux.org/packages/kde-thumbnailer-epub/): Electronic book files

Enable preview showing of required file type in *Control > Configure Dolphin... > General > Previews*.

## Usage

### Open Terminal

Dolphin and other KDE applications use [konsole](https://www.archlinux.org/packages/?name=konsole) by default. To change the default terminal emulator, run `kcmshell5 componentchooser` and select *Terminal Emulator > Use a different terminal program*.

### KIO Slaves

Dolphin uses *KIO slaves* for network access, trash and other functionality, unlike [GTK+](/index.php/GTK%2B "GTK+") file managers which use [GVFS](/index.php/GVFS "GVFS"). Available protocols are shown in the location bar (editable mode) [[1]](https://docs.kde.org/stable/en/applications/dolphin/location-bar.html#location-bar-editable). To quickly bookmark them, right-click in the workspace, and select "Add to Places".

## Troubleshooting

### Device names shown as "X GiB Harddrive"

Create a filesystem label, or a partition label, and Dolphin will show this label in the device list instead of the size. See [Persistent block device naming#by-label](/index.php/Persistent_block_device_naming#by-label "Persistent block device naming").

### Transparent fonts

Fonts in selection frames may become transparent when using the [GTK+ Qt style](/index.php/Uniform_look_for_Qt_and_GTK_applications#QGtkStyle "Uniform look for Qt and GTK applications"). Native Qt styles such as *Cleanlooks* and *Oxygen* are unaffected.

### Crashes on mounted SMB share

See [Samba#Unable to overwrite files](/index.php/Samba#Unable_to_overwrite_files.2C_permissions_errors "Samba").

### Icons not showing

If icons are not displaying on Dolphin, and an error similar to "Pixmap is a null Pixmap" appears on the console, try putting this line in your `~/.profile`

```
[ "$XDG_CURRENT_DESKTOP" = "KDE" ] || [ "$XDG_CURRENT_DESKTOP" = "GNOME" ] || export QT_QPA_PLATFORMTHEME="qt5ct"

```

### Mismatched folder view background colors

When running Dolphin under something other than Plasma, it is possible the background color in the folder view pane will not match the system Qt theme. This is because Dolphin reads the folder view's background color from the `[Colors:View]` section in `~/.config/kdeglobals`. Change the following line to the R,G,B values you prefer:

 `~/.config/kdeglobals` 
```
...
[Colors:View]
BackgroundNormal=23,24,24
...

```

## See also

*   [Wikipedia:Dolphin (file manager)](https://en.wikipedia.org/wiki/Dolphin_(file_manager) "wikipedia:Dolphin (file manager)")
*   [KDE userbase: Dolphin](https://userbase.kde.org/Dolphin)
*   [Dolphin Handbook](https://docs.kde.org/stable/en/applications/dolphin/index.html)