# Xdg user directories

Related articles

*   [xdg-menu](/index.php/Xdg-menu "Xdg-menu")
*   [xdg-open](/index.php/Xdg-open "Xdg-open")
*   [XDG Base Directory support](/index.php/XDG_Base_Directory_support "XDG Base Directory support")

User directories are a set of common user directories located within the `$HOME` directory, including `Documents`, `Downloads`, `Music`, and `Desktop`. Identified by unique icons within a file manager, they will commonly be automatically sourced by numerous programs and applications. [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) is a program that will automatically generate these directories. See the [freedesktop.org](http://freedesktop.org/wiki/Software/xdg-user-dirs) website for further information.

**Tip:** This program will be especially helpful for those who wish to use a file manager to manage their desktop for a [Window manager](/index.php/Window_manager "Window manager") such as [Openbox](/index.php/Openbox "Openbox"), as it will also automatically create a `~/Desktop` directory.

## Contents

*   [1 Installation](#Installation)
*   [2 Creating default directories](#Creating_default_directories)
*   [3 Creating custom directories](#Creating_custom_directories)
*   [4 Querying configured directories](#Querying_configured_directories)

## Installation

[Install](/index.php/Install "Install") the [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) package.

## Creating default directories

To create a full suite of localized default user directories within the `$HOME` directory, enter the following command:

```
$ xdg-user-dirs-update

```

**Tip:** To force the creation of English-named directories, `LC_ALL=C xdg-user-dirs-update` can be used.

When executed, it will also automatically:

*   Create a local `~/.config/user-dirs.dirs` configuration file: used by applications to find and use home directories specific to an account.
*   Create a global `/etc/xdg/user-dirs.defaults` configuration file: used by applications to find and use home directories generally.
*   Create a local `~/.config/user-dirs.locale` configuration file: used to set the language according to the locale in use.

## Creating custom directories

Both the local `~/.config/user-dirs.dirs` and global `/etc/xdg/user-dirs.defaults` configuration files use the following environmental variable format to point to user directories: `XDG_DIRNAME_DIR="$HOME/directory_name`" An example configuration file will/may likely look like this (these are all the template directories):

```
XDG_DESKTOP_DIR="$HOME/Desktop"
XDG_DOCUMENTS_DIR="$HOME/Documents"
XDG_DOWNLOAD_DIR="$HOME/Downloads"
XDG_MUSIC_DIR="$HOME/Music"
XDG_PICTURES_DIR="$HOME/Pictures"
XDG_PUBLICSHARE_DIR="$HOME/Public"
XDG_TEMPLATES_DIR="$HOME/.Templates"
XDG_VIDEOS_DIR="$HOME/Videos"

```

As [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) will source the local configuration file to point to the appropriate user directories, it is therefore possible to specify custom folders. For example, if a custom folder for the `XDG_DOWNLOAD_DIR` variable has named `$HOME/Internet` in `~/.config/user-dirs.dirs` any application that uses this variable will use this directory.

**Note:** Like with many configuration files, local settings override global settings. It will also be necessary to create any new custom directories.

Alternatively, it is also possible to specify custom folders using the command line. For example, the following command will produce the same results as the above configuration file edit:

```
$ xdg-user-dirs-update --set DOWNLOAD ~/Internet

```

## Querying configured directories

Once set, any user directory can be viewed with [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs). For example, the following command will specify the location of the `Templates` directory, which of course corresponds to the `XDG_TEMPLATES_DIR` variable in the local configuration file:

```
$ xdg-user-dir TEMPLATES

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Xdg_user_directories&oldid=412259](https://wiki.archlinux.org/index.php?title=Xdg_user_directories&oldid=412259)"