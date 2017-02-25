From the project [home page](http://wiki.lxde.org/en/PCManFM):

	*PCMan File Manager (PCManFM) is a file manager application developed by Hong Jen Yee from Taiwan which is meant to be a replacement for Nautilus, Konqueror and Thunar. Released under the GNU General Public License, PCManFM is free software. PCManFM is the standard file manager in [LXDE](/index.php/LXDE "LXDE"), which is also developed by the same author in conjunction with other developers.*

## Contents

*   [1 Installation](#Installation)
*   [2 Desktop management](#Desktop_management)
    *   [2.1 Desktop preferences](#Desktop_preferences)
    *   [2.2 Creating new icons](#Creating_new_icons)
*   [3 Daemon mode](#Daemon_mode)
*   [4 Autostarting](#Autostarting)
*   [5 Additional features and functionality](#Additional_features_and_functionality)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Get thumbnails for other file types](#Get_thumbnails_for_other_file_types)
    *   [6.2 Set the terminal emulator](#Set_the_terminal_emulator)
    *   [6.3 Integrate an archiver](#Integrate_an_archiver)
    *   [6.4 Templates are accessible under *Create New...*](#Templates_are_accessible_under_Create_New...)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Open With dialog window empty](#Open_With_dialog_window_empty)
    *   [7.2 No "Applications"](#No_.22Applications.22)
    *   [7.3 No icons](#No_icons)
    *   [7.4 No "Previous/Next Folder" functionality with mouse buttons](#No_.22Previous.2FNext_Folder.22_functionality_with_mouse_buttons)
    *   [7.5 --desktop parameter not working or crashing X-server](#--desktop_parameter_not_working_or_crashing_X-server)
    *   [7.6 Terminal emulator advanced configuration not saved](#Terminal_emulator_advanced_configuration_not_saved)
    *   [7.7 Make PCManFM remember your preferred Sort Files settings](#Make_PCManFM_remember_your_preferred_Sort_Files_settings)
    *   [7.8 "Not authorized" error when attempting to mount drive](#.22Not_authorized.22_error_when_attempting_to_mount_drive)
    *   [7.9 Operation not supported](#Operation_not_supported)

## Installation

[Install](/index.php/Install "Install") the [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm) package, or [pcmanfm-gtk3](https://www.archlinux.org/packages/?name=pcmanfm-gtk3) for the GTK3 version, or [pcmanfm-git](https://aur.archlinux.org/packages/pcmanfm-git/) for the development version. [gvfs](https://www.archlinux.org/packages/?name=gvfs) is recommended for trash support, mounting with [udisks](/index.php/Udisks "Udisks") and remote filesystems.

[Qt](/index.php/Qt "Qt") variants are available through [pcmanfm-qt](https://www.archlinux.org/packages/?name=pcmanfm-qt) and [pcmanfm-qt-git](https://aur.archlinux.org/packages/pcmanfm-qt-git/).

## Desktop management

The command to allow PCManFM to set wallpapers and enable the use of desktop icons is:

```
pcmanfm --desktop

```

The native desktop menu of the window manager will be replaced with that provided by PCManFM. However, it can easily be restored from the PCManFM menu itself by selecting `Desktop preferences` and then enabling the `Right click shows WM menu` option in the `Desktop` tab.

### Desktop preferences

If using the native desktop menu provided by a window manager, enter the following command to set or amend desktop preferences at any time:

```
$ pcmanfm --desktop-pref

```

It is worthwhile to consider adding this command to a keybind and/or the native desktop menu for easy access.

### Creating new icons

User content such as text files, documents, images and so forth can be dragged and dropped directly onto the desktop. To create shortcuts for applications it will be necessary to copy their `.desktop` files to the `~/Desktop` directory itself. Do not drag and drop the files there as they will be moved completely. The syntax of the command to do so is:

```
cp /usr/share/applications/<name of application>.desktop ~/Desktop

```

For example - where installed - to create a desktop shortcut for [lxterminal](https://www.archlinux.org/packages/?name=lxterminal), the following command would be used:

```
cp /usr/share/applications/lxterminal.desktop ~/Desktop

```

For those who used the [XDG user directories](/index.php/XDG_user_directories "XDG user directories") program to create their `$HOME` directories no further configuration will be required.

## Daemon mode

To run PCManFM in the background (to for example automatically mount removable media), use:

```
pcmanfm -d

```

Should automount fail, see [udisks](/index.php/Udisks "Udisks").

## Autostarting

How PCManFM may be autostarted as a [daemon](/index.php/Daemon "Daemon") process or to manage the desktop for a standalone [window manager](/index.php/Window_manager "Window manager") will depend on the window manager itself. For example, to enable management of the desktop for [Openbox](/index.php/Openbox "Openbox"), the following command would be added to the `~/.config/openbox/autostart` file:

```
pcmanfm --desktop &

```

Review the relevant wiki article and/or official home page for a particular installed or intended window manager. Should a window manager not provide an autostart file, PCManFM may be alternatively autostarted by editing one or both of the following files:

*   [xinitrc](/index.php/Xinitrc "Xinitrc"): When using the [SLiM](/index.php/SLiM "SLiM") [display manager](/index.php/Display_manager "Display manager") or [Startx](/index.php/Startx "Startx") command
*   [xprofile](/index.php/Xprofile "Xprofile"): When using a display manager such as [LXDM](/index.php/LXDM "LXDM") or [LightDM](/index.php/LightDM "LightDM")

## Additional features and functionality

Less experienced users should be aware that a file manager alone - especially when installed in a standalone [Window manager](/index.php/Window_manager "Window manager") such as [Openbox](/index.php/Openbox "Openbox") - will not provide the features and functionality users of full desktop environments such as [Xfce](/index.php/Xfce "Xfce") and [KDE](/index.php/KDE "KDE") will be accustomed to. Review the [file manager functionality](/index.php/File_manager_functionality "File manager functionality") article for further information.

## Tips and tricks

### Get thumbnails for other file types

PCManFM supports image thumbnails out of the box. However, in order to view thumbnails of other file types, PCManFM uses the information provided in the files located at `/usr/share/thumbnailers`. The packages which provide a thumbnailer usually add the corresponding *.thumbnail* file at `/usr/share/thumbnailers`. For example, in order to get thumbnails for OpenDocument files, you may install [libgsf](https://www.archlinux.org/packages/?name=libgsf) from the official repositories. For video files' thumbnails, the package [ffmpegthumbnailer](https://www.archlinux.org/packages/?name=ffmpegthumbnailer) is required. For PDF files, you may install [evince](https://www.archlinux.org/packages/?name=evince) from the official repositories, which provides `evince-thumbnailer` and the corresponding file at `/usr/share/thumbnailers`. However, if you prefer not to install `evince`, you can also replicate the functionality of `evince-thumbnailer` using [imagemagick](https://www.archlinux.org/packages/?name=imagemagick)'s `convert` command. This is accomplished by creating a new file with the *.thumbnailer* extension (e.g.: `imagemagick-pdf.thumbnailer`) at `/usr/share/thumbnailers` with the following content:

```
  [Thumbnailer Entry]
  TryExec=convert
  Exec=convert %i[0] -thumbnail %s %o
  MimeType=application/pdf;application/x-pdf;image/pdf;

```

**Note:** The *[0]* next to the input file is specified so that `convert` only generates a thumbnail of the first page. This is a `convert`-specific syntax and has nothing to do with the syntax of the thumbnailers' files.

Following this example, you can specify custom thumbnailers by creating your own *.thumbnail* files. Keep in mind that `%i` refers to the input file (the file which will have its thumbnail made), `%o` to the output file (the thumbnail image) and `%s` to the size of the thumbnail. These parameters will be automatically substituted with the corresponding data and passed to the thumbnailer program by PCManFM.

**Tip:** If you only get thumbnails of certain files and not of all the files of the same type try increasing the maximum file size of the files that get a thumbnail at *Edit > Preferences > Display*.

### Set the terminal emulator

You can configure what terminal emulator PCManFM should use for *Tools > Open Current Folder in Terminal* under *Edit > Preferences > Advanced* e.g. `bash -c 'pantheon-terminal --working-directory "$PWD"'`.

### Integrate an archiver

You can choose the integrated archiver under *Edit > Preferences > Advanced*. PCManFM supports [file-roller](https://www.archlinux.org/packages/?name=file-roller), [xarchiver](https://www.archlinux.org/packages/?name=xarchiver) (or [xarchiver-gtk2](https://www.archlinux.org/packages/?name=xarchiver-gtk2)), [engrampa](https://www.archlinux.org/packages/?name=engrampa), [ark](https://www.archlinux.org/packages/?name=ark) and [squeeze-git](https://aur.archlinux.org/packages/squeeze-git/).

### Templates are accessible under *Create New...*

PCManFM adds the files in `~/Templates` as *Create New...* context menu items on startup.

## Troubleshooting

### Open With dialog window empty

If you do not see any applications to choose from in the open with dialog, then you can try removing [gnome-menus](https://www.archlinux.org/packages/?name=gnome-menus) and instead install [lxmenu-data](https://www.archlinux.org/packages/?name=lxmenu-data). Furthermore, export the following variables:

```
export XDG_MENU_PREFIX=lxde-
export XDG_CURRENT_DESKTOP=LXDE

```

### No "Applications"

You can try this method: Delete all files in the `$HOME/.cache/menus` directory, and run PCManFM again.

PCManFM requires the environment variable *XDG_MENU_PREFIX* to be set. The value of the variable should match the beginning of a file present in the `/etc/xdg/menus/` directory. E.g. you can set the value in your `.xinitrc` file with the line:

```
export XDG_MENU_PREFIX="lxde-"

```

See these threads for more informations: [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1110903), and especially this post from the Linux Mint forums: [[2]](http://forums.linuxmint.com/viewtopic.php?f=175&t=53986#p501920)

### No icons

If you are using a [window manager](/index.php/Window_manager "Window manager") instead of a [desktop environment](/index.php/Desktop_environment "Desktop environment") and you have no icons for folders and files, specify a GTK+ icon theme.

If you have e.g. [oxygen-icons](https://www.archlinux.org/packages/?name=oxygen-icons) installed, edit `~/.gtkrc-2.0` **or** `/etc/gtk-2.0/gtkrc` and add the following line:

```
gtk-icon-theme-name = "oxygen"

```

**Note:** All instances of PCManFM have to be restarted for changes to apply!

Else, use an different one (*gnome*, *hicolor*, and *locolor* do not work). To list all installed icon themes:

```
$ ls ~/.icons/ /usr/share/icons/

```

If none of them is suitable, install one. To list all installable icon packages:

```
$ pacman -Ss icon-theme

```

**Tip:** For an alternative GUI solution, install [lxappearance](https://www.archlinux.org/packages/?name=lxappearance) and apply an icon theme from there.

### No "Previous/Next Folder" functionality with mouse buttons

A method to fix this is with [Xbindkeys](/index.php/Xbindkeys "Xbindkeys").

Install [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys), [xvkbd](https://www.archlinux.org/packages/?name=xvkbd) and edit `~/.xbindkeysrc` to contain the following:

```
# Sample .xbindkeysrc for a G9x mouse.
"/usr/bin/xvkbd -text '\[Alt_L]\[Left]'"
 b:8
"/usr/bin/xvkbd -text '\[Alt_L]\[Right]'"
 b:9

```

Actual button codes can be obtained with package [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev).

Add:

```
xbindkeys &

```

to your `~/.xinitrc` to execute xbindkeys on log-in.

### --desktop parameter not working or crashing X-server

Make sure you have ownership and write permissions on `~/.config/pcmanfm`.

Setting the wallpaper either by using the `--desktop-pref` parameter or editing `~/.config/pcmanfm/default/pcmanfm.config` solves the problem.

### Terminal emulator advanced configuration not saved

Make sure you have rights on libfm configuration file:

```
$ chmod -R 755 ~/.config/libfm
$ chmod 777 ~/.config/libfm/libfm.conf

```

### Make PCManFM remember your preferred Sort Files settings

You can use *View > Sort Files* to change the order in which PCManFM lists the files, but PCManFM won't remember that the next time you start it. To make it remember, go to *Edit > Preferences* and close. That will write your current sort_type and sort_by values into `~/.config/pcmanfm/LXDE/pcmanfm.conf`.

### "Not authorized" error when attempting to mount drive

Make this [polkit](/index.php/Polkit "Polkit") rule in `/etc/polkit-1/rules.d/00-mount-internal.rules`:

```
polkit.addRule(function(action, subject) {
   if ((action.id == "org.freedesktop.udisks2.filesystem-mount-system" &&
      subject.local && subject.active && subject.isInGroup("storage")))
      {
         return polkit.Result.YES;
      }
});

```

And add your user to storage group:

```
# usermod -aG storage username

```

### Operation not supported

See the General troubleshooting article on [Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting").