# GNOME Files

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
*   [Install](/index.php/Install "Install") package [gvfs-afp](https://www.archlinux.org/packages/?name=gvfs-afp) and [avahi](https://www.archlinux.org/packages/?name=avahi) for accessing apple network shares. In addition to installing [Avahi](/index.php/Avahi "Avahi"), it must be [enabled](/index.php/Enable "Enable") too.

### Plugins

Some programs can add extra functionality to Files. Here are a few packages in the official repositories that do just that.

*   **Eiciel** — Include extension which add graphical [ACL](/index.php/ACL "ACL") editor into the file properties window.

	[http://rofi.roger-ferrer.org/eiciel/](http://rofi.roger-ferrer.org/eiciel/) || [eiciel](https://aur.archlinux.org/packages/eiciel/)

*   **Folder Color** — Change the color of each icon separately then you are easily notice the right folder!

	[http://foldercolor.tuxfamily.org/](http://foldercolor.tuxfamily.org/) || [folder-color-nautilus-bzr](https://aur.archlinux.org/packages/folder-color-nautilus-bzr/)

**Tip:** This extension works only with these icon-themes which contain additional colored icons, eg:
[numix-icon-theme-git](https://aur.archlinux.org/packages/numix-icon-theme-git/), [vibrancy-colors](https://aur.archlinux.org/packages/vibrancy-colors/), [vivacious-folder-colors-addon](https://aur.archlinux.org/packages/vivacious-folder-colors-addon/), [humanitycolors-icon-theme](https://aur.archlinux.org/packages/humanitycolors-icon-theme/)

*   **Nautilus Actions** — Configures programs to be launched when files are selected in Files

	[http://www.nautilus-actions.org/](http://www.nautilus-actions.org/) || [nautilus-actions](https://www.archlinux.org/packages/?name=nautilus-actions)

*   **Nautilus Admin** — Add to menu: "Open as administrator" or "Edit as administrator"

	[https://bitbucket.org/brunonova/nautilus-admin](https://bitbucket.org/brunonova/nautilus-admin) || [nautilus-admin](https://aur.archlinux.org/packages/nautilus-admin/)

*   **Nautilus Terminal** — Terminal embedded in Files. It is always open in the current folder, and follows the navigation.

	[http://projects.flogisoft.com/nautilus-terminal/](http://projects.flogisoft.com/nautilus-terminal/) || [nautilus-terminal](https://www.archlinux.org/packages/?name=nautilus-terminal)

*   **Open in Terminal** — A Files plugin for opening terminals in arbitrary local paths

	[http://ftp.gnome.org/pub/GNOME/sources/nautilus-open-terminal](http://ftp.gnome.org/pub/GNOME/sources/nautilus-open-terminal) || [nautilus-open-terminal](https://www.archlinux.org/packages/?name=nautilus-open-terminal)

**Tip:** This plugin is not needed if you have [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal) installed: since version 3.10.0-2 it provides the extension `/usr/lib/nautilus/extensions-3.0/libterminal-nautilus.so` which creates an entry in Files' context menu for opening the selected directory in a new terminal - see [this commit](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/gnome-terminal&id=b143484f73a75663abacb69435fd663c348861d2).

*   **Send to Menu** — Files context menu for sending files.

	[http://download.gnome.org/sources/nautilus-sendto/](http://download.gnome.org/sources/nautilus-sendto/) || [nautilus-sendto](https://www.archlinux.org/packages/?name=nautilus-sendto)

*   **Seahorse Nautilus** — PGP encryption and signing for Files

	[http://git.gnome.org/browse/seahorse-nautilus/](http://git.gnome.org/browse/seahorse-nautilus/) || [seahorse-nautilus](https://www.archlinux.org/packages/?name=seahorse-nautilus)

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

See [File manager functionality#Directories are not opened in the file manager](/index.php/File_manager_functionality#Directories_are_not_opened_in_the_file_manager "File manager functionality").

Retrieved from "[https://wiki.archlinux.org/index.php?title=GNOME_Files&oldid=419521](https://wiki.archlinux.org/index.php?title=GNOME_Files&oldid=419521)"