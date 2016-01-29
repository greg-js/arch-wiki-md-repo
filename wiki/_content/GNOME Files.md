# GNOME Files

Related articles

*   [GNOME](/index.php/GNOME "GNOME")
*   [File manager functionality](/index.php/File_manager_functionality "File manager functionality")
*   [Nemo](/index.php/Nemo "Nemo")
*   [Thunar](/index.php/Thunar "Thunar")
*   [PCManFM](/index.php/PCManFM "PCManFM")

Files is the default file manager for [GNOME](https://live.gnome.org/). Files attempts to provide a streamlined method to manage both files and applications.

**Note:** Files was known as [Nautilus](http://live.gnome.org/Nautilus) prior to version 3.6\. The application was given new descriptive names, one for each supported language. The name _Nautilus_ is still used in numerous places such as the executable name, some package names, some desktop entries, and some GSettings schemas.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Plugins](#Plugins)
*   [2 Configuration](#Configuration)
    *   [2.1 Desktop Icons](#Desktop_Icons)
    *   [2.2 Change default item view](#Change_default_item_view)
    *   [2.3 Remove folders from the places sidebar](#Remove_folders_from_the_places_sidebar)
    *   [2.4 Always show text-entry location](#Always_show_text-entry_location)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Thumbnails](#Thumbnails)
    *   [3.2 Create an empty document in Files 3.6 and above](#Create_an_empty_document_in_Files_3.6_and_above)
    *   [3.3 Music files metadata in list view](#Music_files_metadata_in_list_view)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Files is no longer the default file manager](#Files_is_no_longer_the_default_file_manager)

## Installation

**Files** can be [installed](/index.php/Install "Install") with the [nautilus](https://www.archlinux.org/packages/?name=nautilus) package from the [official repositories](/index.php/Official_repositories "Official repositories"). This package is part of the [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group.

**Note:** Files does not depend on the [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell) package, only requiring [gnome-desktop](https://www.archlinux.org/packages/?name=gnome-desktop).

*   [Install](/index.php/Install "Install") package [gvfs-smb](https://www.archlinux.org/packages/?name=gvfs-smb) for Windows network shares.
*   [Install](/index.php/Install "Install") package [gvfs-afp](https://www.archlinux.org/packages/?name=gvfs-afp)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [gvfs](https://www.archlinux.org/packages/?name=gvfs)]</sup> and [avahi](https://www.archlinux.org/packages/?name=avahi) for accessing apple network shares. In addition to installing [Avahi](/index.php/Avahi "Avahi"), it must be [enabled](/index.php/Enable "Enable") too.

### Plugins

Some programs can add extra functionality to Files. Here are a few packages in the official repositories that do just that.

*   **Eiciel** — Include extension which add graphical [ACL](/index.php/ACL "ACL") editor into the file properties window.

NaN

*   **Folder Color** — Change the color of each icon separately then you are easily notice the right folder!

NaN

*   **Nautilus Actions** — Configures programs to be launched when files are selected in Files

NaN

*   **Nautilus Admin** — Add to menu: "Open as administrator" or "Edit as administrator"

NaN

*   **Nautilus Terminal** — Terminal embedded in Files. It is always open in the current folder, and follows the navigation.

NaN

*   **Open in Terminal** — A Files plugin for opening terminals in arbitrary local paths

NaN

*   **Send to Menu** — Files context menu for sending files.

NaN

*   **Seahorse Nautilus** — PGP encryption and signing for Files

NaN

## Configuration

Files is simple to configure graphically, but not all options are available in the preferences menu. More options are available with _dconf-editor_ under `org.gnome.nautilus`.

### Desktop Icons

Files, by default, no longer manages the desktop window in GNOME Shell. However, Files does have the ability to provide desktop icons if they are desired. Files achieves this by drawing a transparent window (containing the icons) which sits on top of the desktop window.

To enable desktop icons, in [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool), choose: _Desktop > Icons on Desktop > ON_. You may have to restart Files by running `killall nautilus; nautilus` or if you are running [GNOME](/index.php/GNOME "GNOME"), press `ALT+F2`, type `r`, and press `Enter` (this restarts GNOME Shell).

Alternatively, run the following command which will achieve the same effect:

```
$ gsettings set org.gnome.desktop.background show-desktop-icons true

```

**Note:** Sessions such as GNOME Classic call the _nautilus-classic_ desktop entry which will ensure that desktop icons are always enabled.

### Change default item view

You can change the default view for the items by setting the `default-folder-viewer` variable, e.g. for the list view:

```
$ gsettings set org.gnome.nautilus.preferences default-folder-viewer 'list-view'

```

### Remove folders from the places sidebar

The displayed folders are specified in `~/.config/user-dirs.dirs` and can be altered with any editor. An execution of `xdg-user-dirs-update` will change them again, thus it may be advisable to set the file permissions to read-only.

### Always show text-entry location

The standard Files toolbar shows a button bar interface for path navigation. To enter path locations using the _keyboard_, you must expose the location text-entry field. This is done by pressing `Ctrl+l`

To make the location text-entry field always present, use _gsettings_ as shown below:

```
$ gsettings set org.gnome.nautilus.preferences always-use-location-entry true

```

**Note:** After changing this setting, you will not be able to expose the button bar. Only when the setting is **false** can both forms of location navigation be employed.

## Tips and tricks

### Thumbnails

See [File manager functionality#Thumbnail previews](/index.php/File_manager_functionality#Thumbnail_previews "File manager functionality").

### Create an empty document in Files 3.6 and above

GNOME 3.6 brought changes to Files. The option to create an empty document has been removed from the right-click menu in Files. To get this option back one has to create a `~/Templates/` folder in your home folder and place an empty file inside the folder through your favorite Terminal by `touch ~/Templates/new` or by using any other file manager. Then just restart Files.

On non-English installations, the templates directory might have another name. One can find the actual directory with `xdg-user-dir TEMPLATES`.

### Music files metadata in list view

**Note:** The script linked to below is slightly modified to fix an error. The original can be found [here](http://bazaar.launchpad.net/~team1/+junk/devel/view/head:/bsc-v2.py).

GNOME Files lacks the ability to display metadata for music files in list view mode. A [Python](/index.php/Python "Python") script is available which adds list view columns for the artist, album, track title, bit rate and more.

To use the script you first need to [install](/index.php/Install "Install") the following: [python2-nautilus](https://www.archlinux.org/packages/?name=python2-nautilus), [mutagen](https://www.archlinux.org/packages/?name=mutagen), [python2-pillow](https://www.archlinux.org/packages/?name=python2-pillow), [kaa-metadata](https://www.archlinux.org/packages/?name=kaa-metadata) and [python2-exiv2](https://www.archlinux.org/packages/?name=python2-exiv2).

Once the dependencies are installed, save the [bsc-v2.py](http://pastebin.com/zN69twVP) script to `~/.local/share/nautilus-python/extensions` (create the directory if it does not exist) and restart Files.

The new columns should now have been added. To enable them, navigate to Preferences -> List columns and tick the columns that you wish to use.

## Troubleshooting

### Files is no longer the default file manager

This can happen for a number of reasons, primarily when an installation of another application forces mime type changes. If Files is not recognized as the default file manager, set Files as default handler for the mime type _inode/directory_:

```
$ xdg-mime default org.gnome.Nautilus.desktop inode/directory

```

... which will generate:

 `~/.local/share/applications/mimeapps.list` 

```
[Default Applications]
inode/directory=org.gnome.Nautilus.desktop
```

**Tip:** If you want the change to be system-wide, run the command above as root or create/edit the file `/usr/share/applications/mimeapps.list` and add the line there.

Retrieved from "[https://wiki.archlinux.org/index.php?title=GNOME_Files&oldid=412081](https://wiki.archlinux.org/index.php?title=GNOME_Files&oldid=412081)"