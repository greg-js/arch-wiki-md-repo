Related articles

*   [xdg-menu](/index.php/Xdg-menu "Xdg-menu")
*   [Default applications](/index.php/Default_applications "Default applications")
*   [XDG Base Directory support](/index.php/XDG_Base_Directory_support "XDG Base Directory support")

From [freedesktop.org](https://www.freedesktop.org/wiki/Software/xdg-user-dirs/):

	xdg-user-dirs is a tool to help manage "well known" user directories like the desktop folder and the music folder. It also handles localization (i.e. translation) of the filenames.

	The way it works is that [xdg-user-dirs-update(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-user-dirs-update.1) is run very early in the login phase. This program reads a configuration file, and a set of default directories. It then creates localized versions of these directories in the users home directory and sets up a config file in `$XDG_CONFIG_HOME/user-dirs.dirs` (`XDG_CONFIG_HOME` defaults to `~/.config`) that applications can read to find these directories.

Most [file managers](/index.php/File_manager "File manager") indicate XDG user directories with special icons.

## Creating default directories

Creating a full suite of localized default user directories within the `$HOME` directory can be done automatically using [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) and running:

```
$ xdg-user-dirs-update

```

**Tip:** To force the creation of English-named directories, `LC_ALL=C xdg-user-dirs-update --force` can be used.

When executed, it will also automatically:

*   Create a local `~/.config/user-dirs.dirs` configuration file: used by applications to find and use home directories specific to an account.
*   Create a local `~/.config/user-dirs.locale` configuration file: used to set the language according to the locale in use.

The user service `xdg-user-dirs-update.service` will also be installed and enabled by default, in order to keep your directories up to date by running this command at the beginning of each login session.

## Creating custom directories

Both the local `~/.config/user-dirs.dirs` and global `/etc/xdg/user-dirs.defaults` configuration files use the following environmental variable format to point to user directories: `XDG_DIRNAME_DIR="$HOME/directory_name"` An example configuration file will/may likely look like this (these are all the template directories):

 `~/.config/user-dirs.dirs` 
```
XDG_DESKTOP_DIR="$HOME/Desktop"
XDG_DOCUMENTS_DIR="$HOME/Documents"
XDG_DOWNLOAD_DIR="$HOME/Downloads"
XDG_MUSIC_DIR="$HOME/Music"
XDG_PICTURES_DIR="$HOME/Pictures"
XDG_PUBLICSHARE_DIR="$HOME/Public"
XDG_TEMPLATES_DIR="$HOME/Templates"
XDG_VIDEOS_DIR="$HOME/Videos"
```

As [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) will source the local configuration file to point to the appropriate user directories, it is therefore possible to specify custom folders. For example, if a custom folder for the `XDG_DOWNLOAD_DIR` variable has named `$HOME/Internet` in `~/.config/user-dirs.dirs` any application that uses this variable will use this directory.

**Note:** Like with many configuration files, local settings override global settings. It will also be necessary to create any new custom directories.

Alternatively, it is also possible to specify custom folders using the command line. For example, the following command will produce the same results as the above configuration file edit:

```
$ xdg-user-dirs-update --set DOWNLOAD ~/Internet

```

## Querying configured directories

Once set, any user directory can be viewed with [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs). For example, the following command will show the location of the `Templates` directory, which of course corresponds to the `XDG_TEMPLATES_DIR` variable in the local configuration file:

```
$ xdg-user-dir TEMPLATES

```