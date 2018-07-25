Related articles

*   [GNOME](/index.php/GNOME "GNOME")
*   [File manager functionality](/index.php/File_manager_functionality "File manager functionality")
*   [Nemo](/index.php/Nemo "Nemo")
*   [Thunar](/index.php/Thunar "Thunar")
*   [PCManFM](/index.php/PCManFM "PCManFM")

Files is the default file manager for [GNOME](https://wiki.gnome.org/). Files attempts to provide a streamlined method to manage both files and applications.

**Note:** Files was known as [Nautilus](https://wiki.gnome.org/Apps/Nautilus) prior to version 3.6\. The application was given new descriptive names, one for each supported language. The name *Nautilus* is still used in numerous places such as the executable name, some package names, some desktop entries, and some GSettings schemas.

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
    *   [3.4 Hiding files](#Hiding_files)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Files is no longer the default file manager](#Files_is_no_longer_the_default_file_manager)
    *   [4.2 Thumbnailing not working for video files](#Thumbnailing_not_working_for_video_files)
    *   [4.3 Freezes for a few seconds after every copy operation](#Freezes_for_a_few_seconds_after_every_copy_operation)

## Installation

[Install](/index.php/Install "Install") the [nautilus](https://www.archlinux.org/packages/?name=nautilus) package. This package is part of the [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group. See also [File manager functionality#Additional features](/index.php/File_manager_functionality#Additional_features "File manager functionality").

**Note:** Files does not depend on the [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell) package, only requiring [gnome-desktop](https://www.archlinux.org/packages/?name=gnome-desktop).

### Plugins

Some programs can add extra functionality to Files. Here are a few packages in the official repositories that do just that.

*   **Eiciel** — Include extension which add graphical [ACL](/index.php/ACL "ACL") editor into the file properties window.

	[http://rofi.roger-ferrer.org/eiciel/](http://rofi.roger-ferrer.org/eiciel/) || [eiciel](https://aur.archlinux.org/packages/eiciel/)

*   **Folder Color** — Change the color of each icon separately then you are easily notice the right folder!

	[http://foldercolor.tuxfamily.org/](http://foldercolor.tuxfamily.org/) || [folder-color-nautilus-bzr](https://aur.archlinux.org/packages/folder-color-nautilus-bzr/)

**Tip:** This extension works only with these icon-themes which contain additional colored icons, eg:
[numix-icon-theme-git](https://aur.archlinux.org/packages/numix-icon-theme-git/), [vibrancy-colors](https://aur.archlinux.org/packages/vibrancy-colors/), [vivacious-colors-icon-theme](https://aur.archlinux.org/packages/vivacious-colors-icon-theme/), [humanity-icon-theme](https://aur.archlinux.org/packages/humanity-icon-theme/), [mint-x-icons](https://aur.archlinux.org/packages/mint-x-icons/)

*   **File Manager Actions** — Configures programs to be launched when files are selected in Files

	[https://git.gnome.org/browse/filemanager-actions](https://git.gnome.org/browse/filemanager-actions) || [filemanager-actions](https://www.archlinux.org/packages/?name=filemanager-actions)

*   **Nautilus Admin** — Add to menu: "Open as administrator" or "Edit as administrator"

	[https://bitbucket.org/brunonova/nautilus-admin](https://bitbucket.org/brunonova/nautilus-admin) || [nautilus-admin](https://aur.archlinux.org/packages/nautilus-admin/)

*   **Nautilus Terminal** — Terminal embedded in Files. It is always open in the current folder, and follows the navigation.

	[http://projects.flogisoft.com/nautilus-terminal/](http://projects.flogisoft.com/nautilus-terminal/) || [nautilus-terminal](https://www.archlinux.org/packages/?name=nautilus-terminal)

*   **Send to Menu** — Files context menu for sending files.

	[http://download.gnome.org/sources/nautilus-sendto/](http://download.gnome.org/sources/nautilus-sendto/) || [nautilus-sendto](https://www.archlinux.org/packages/?name=nautilus-sendto)

*   **Seahorse Nautilus** — PGP encryption and signing for Files

	[http://git.gnome.org/browse/seahorse-nautilus/](http://git.gnome.org/browse/seahorse-nautilus/) || [seahorse-nautilus](https://www.archlinux.org/packages/?name=seahorse-nautilus)

*   **File Roller** — An application for browsing archives

	[https://wiki.gnome.org/Apps/FileRoller](https://wiki.gnome.org/Apps/FileRoller) || [file-roller](https://www.archlinux.org/packages/?name=file-roller)

## Configuration

Files is simple to configure graphically, but not all options are available in the preferences menu. More options are available with *dconf-editor* under `org.gnome.nautilus`.

### Desktop Icons

See [GNOME#Icons on the Desktop](/index.php/GNOME#Icons_on_the_Desktop "GNOME").

### Change default item view

You can change the default view for the items by setting the `default-folder-viewer` variable, e.g. for the list view:

```
$ gsettings set org.gnome.nautilus.preferences default-folder-viewer 'list-view'

```

### Remove folders from the places sidebar

The displayed folders are specified in `~/.config/user-dirs.dirs` and can be altered with any editor. An execution of `xdg-user-dirs-update` will change them again, thus it may be advisable to set the file permissions to read-only.

### Always show text-entry location

The standard Files toolbar shows a button bar interface for path navigation. To enter path locations using the *keyboard*, you must expose the location text-entry field. This is done by pressing `Ctrl+l`

To make the location text-entry field always present, use *gsettings* as shown below:

```
$ gsettings set org.gnome.nautilus.preferences always-use-location-entry true

```

**Note:** After changing this setting, you will not be able to expose the button bar. Only when the setting is **false** can both forms of location navigation be employed.

## Tips and tricks

### Thumbnails

See [File manager functionality#Thumbnail previews](/index.php/File_manager_functionality#Thumbnail_previews "File manager functionality").

Sometimes video thumbnails are not shown. To solve it (as mentioned in [No video thumbnails on nautilus](https://bbs.archlinux.org/viewtopic.php?id=168626)), you must install [ffmpegthumbnailer](https://www.archlinux.org/packages/?name=ffmpegthumbnailer), [gst-libav](https://www.archlinux.org/packages/?name=gst-libav), [gst-plugins-ugly](https://www.archlinux.org/packages/?name=gst-plugins-ugly), and remove the content of `~/.cache/thumbnails/fail/`.

### Create an empty document in Files 3.6 and above

GNOME 3.6 brought changes to Files. The option to create an empty document has been removed from the right-click menu in Files. To get this option back one has to create a `~/Templates/` folder in your home folder and place an empty file inside the folder through your favorite Terminal by `touch ~/Templates/new` or by using any other file manager. Then just restart Files.

On non-English installations, the templates directory might have another name. One can find the actual directory with `xdg-user-dir TEMPLATES`.

The templates directory can be configure in `~/.config/user-dirs.dirs`

```
XDG_TEMPLATES_DIR="$HOME/some/path"

```

### Music files metadata in list view

**Note:** The script linked to below is slightly modified to fix an error. The original can be found [here](http://bazaar.launchpad.net/~team1/+junk/devel/view/head:/bsc-v2.py).

GNOME Files lacks the ability to display metadata for music files in list view mode. A [Python](/index.php/Python "Python") script is available which adds list view columns for the artist, album, track title, bit rate and more.

To use the script you first need to [install](/index.php/Install "Install") the following: [python2-nautilus](https://www.archlinux.org/packages/?name=python2-nautilus), [mutagen](https://www.archlinux.org/packages/?name=mutagen), [python2-pillow](https://www.archlinux.org/packages/?name=python2-pillow), [kaa-metadata](https://aur.archlinux.org/packages/kaa-metadata/) and [python2-exiv2](https://www.archlinux.org/packages/?name=python2-exiv2).

Once the dependencies are installed, save the [bsc-v2.py](http://pastebin.com/zN69twVP) script to `~/.local/share/nautilus-python/extensions` (create the directory if it does not exist) and restart Files.

The new columns should now have been added. To enable them, navigate to Preferences -> List columns and tick the columns that you wish to use.

### Hiding files

Like most other file managers GNOME Files hides files with names starting with a dot by default.

GNOME Files additionally hides files when their names are listed in a `.hidden` file in the same directory (one filename per line).

## Troubleshooting

### Files is no longer the default file manager

This can be caused by the file association for directories being reset. Installing [anjuta](https://www.archlinux.org/packages/?name=anjuta) tends to do this.

To solve this, open Files, right-click on a folder, and choose *Open With Other Application > Files > Select*. This will set the association for directories back to Files.

If this does not solve the issue, see [File manager functionality#Directories are not opened in the file manager](/index.php/File_manager_functionality#Directories_are_not_opened_in_the_file_manager "File manager functionality").

### Thumbnailing not working for video files

There is an ongoing issue with [totem](https://www.archlinux.org/packages/?name=totem) (the video thumbnailer for Nautilus) on computers with Intel GPUs. It will crash if [gstreamer-vaapi](https://www.archlinux.org/packages/?name=gstreamer-vaapi) is installed. Until this issue is resolved, it is recommended to remove this package.

### Freezes for a few seconds after every copy operation

In case you have [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect) installed in your system, the problem might be caused by its file sharing module. Deactivate file sharing, and it should stop happening.