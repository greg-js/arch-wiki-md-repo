**xdg-open** is a desktop-independent tool for configuring the [default applications](/index.php/Default_applications "Default applications") of a user. Many applications invoke the `xdg-open` command internally.

Inside a [desktop environment](/index.php/Desktop_environment "Desktop environment") (like [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), or [Xfce](/index.php/Xfce "Xfce")), _xdg-open_ simply passes the arguments to those desktop environment's file-opener application (eg. _gvfs-open_, _kde-open_, or _exo-open_). which means that the associations are left up to the desktop environment.

When no desktop environment is detected (for example when one runs a standalone [window manager](/index.php/Window_manager "Window manager") like eg. [Openbox](/index.php/Openbox "Openbox")), _xdg-open_ will use its own configuration files.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Set the default browser](#Set_the_default_browser)
    *   [2.2 perl-file-mimeinfo](#perl-file-mimeinfo)
*   [3 Drop-in replacements and useful tools](#Drop-in_replacements_and_useful_tools)
    *   [3.1 xdg-open replacements](#xdg-open_replacements)
    *   [3.2 mailcap](#mailcap)
    *   [3.3 mimetype](#mimetype)
    *   [3.4 Environment variables](#Environment_variables)

## Installation

_xdg-open_ is part of the [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) package available in the [official repositories](/index.php/Official_repositories "Official repositories"). It is for use inside a desktop session only, and should not be run as root.

If you run _xdg-open_ without a desktop environment, you should also install [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo), or [xdg-utils-mimeo](https://aur.archlinux.org/packages/xdg-utils-mimeo/) and [mimeo](https://aur.archlinux.org/packages/mimeo/) from the [AUR](/index.php/AUR "AUR") for a faster alternative.

## Configuration

_xdg-open_ is configured by the files mentioned in [Default applications](/index.php/Default_applications#MIME_types_and_desktop_entries "Default applications"). _xdg-mime_ modifies the local file `~/.config/mimeapps.list` and `~/.local/share/applications/mimeapps.list` (deprecated).

To **query** the mime type used by an existing file, use

```
$ xdg-mime query **filetype** _file.ext_

```

Reversely, to query the default [desktop entry](/index.php/Desktop_entry "Desktop entry") associated with a specific mime type, run

```
$ xdg-mime query **default** _mime/type_

```

Examples for _mime/type_ can be:

```
inode/directory (file browser)
image/jpeg (JPEG images)
application/pdf (PDF viewer)
or others

```

To change an associated desktop entry, use:

```
$ xdg-mime **default** _application.desktop_ _mime/type_

```

For example set [Thunar](/index.php/Thunar "Thunar") as the default file browser just run:

```
$ xdg-mime default Thunar.desktop inode/directory

```

This command can take multiple mime-types, allowing related files to be handled by the same program. The example below associates [Emacs](/index.php/Emacs "Emacs") to all known source files:

```
$ xdg-mime default emacs.desktop $(grep '^text/x-*' /usr/share/mime/types)

```

### Set the default browser

To set the default application for `http(s)://` web URLs, write

```
$ xdg-mime default _browser_.desktop x-scheme-handler/http
$ xdg-mime default _browser_.desktop x-scheme-handler/https

```

To do so for `.html` files:

```
$ xdg-mime default _browser_.desktop text/html

```

Alternatively, run:

```
$ xdg-settings set default-web-browser _browser_.desktop

```

To test if this was applied successfully, try to open an URL with _xdg-open_ as follows:

```
$ xdg-open [https://archlinux.org](https://archlinux.org)

```

### perl-file-mimeinfo

_xdg-open_ uses [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) as a fallback ("generic") method if no [desktop environment](/index.php/Desktop_environment "Desktop environment") is detected. It can be invoked directly with:

```
$ mimeopen -d /path/to/file

```

You are asked which application to use when opening `/path/to/file`:

```
Please choose a default application for files of type text/plain
       1) notepad  (wine-extension-txt)
       2) Leafpad  (leafpad)
       3) OpenOffice.org Writer  (writer)
       4) gVim  (gvim)
       5) Other...

```

Your answer becomes the default handler for that type of file. Mimeopen is installed as `/usr/bin/vendor_perl/mimeopen`.

## Drop-in replacements and useful tools

### xdg-open replacements

| Name/Package | Method | Based on | Configuration file |
| [busking-git](https://aur.archlinux.org/packages/busking-git/) | Regular expressions | [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) | custom |
| [linopen](https://aur.archlinux.org/packages/linopen/) | [file](https://www.archlinux.org/packages/?name=file) | custom |
| [mimeo](https://aur.archlinux.org/packages/mimeo/) | MIME-type, regular expressions | [file](https://www.archlinux.org/packages/?name=file) | `mimeapps.list`, `defaults.list`; custom is optional |
| [mimi-git](https://aur.archlinux.org/packages/mimi-git/) | [file](https://www.archlinux.org/packages/?name=file) | custom |
| [whippet](https://aur.archlinux.org/packages/whippet/) | MIME-type, name, regular expressions | SQLite database or [file](https://www.archlinux.org/packages/?name=file), [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo), etc | custom SQLite database or `mimeapps.list` |
| [ayr](https://aur.archlinux.org/packages/ayr/) | MIME-type, name, regular expressions | [file](https://www.archlinux.org/packages/?name=file) or [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo), etc | `mimeapps.list`, `defaults.list` |
| [sx-open](https://aur.archlinux.org/packages/sx-open/) | Regular expressions | [file](https://www.archlinux.org/packages/?name=file), bash regex | custom |
| [ranger](https://www.archlinux.org/packages/?name=ranger) (rifle command) | MIME-type, name, regular expressions | custom |

**Note:** Some of the above packages replace `xdg-utils`. Those that do not can be symbolically linked to _xdg-open_ in the user's `$PATH` above `/usr/bin`, but some applications hard-code the absolute path `/usr/bin/xdg-open`. In this case, install [xdg-utils-no-open](https://aur.archlinux.org/packages/xdg-utils-no-open/) from the [AUR](/index.php/AUR "AUR") and copy the replacement to `/usr/bin/xdg-open`.

### mailcap

The _.mailcap_ file format is used by mail programs such as [mutt](https://www.archlinux.org/packages/?name=mutt) and [sylpheed](https://www.archlinux.org/packages/?name=sylpheed). To have those programs use _xdg-open_, edit `~/.mailcap`:

 `~/.mailcap` 

```
*/*; xdg-open "%s"

```

### mimetype

_mimetype_ in [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) package can display some mimetype-related information about a file.

For example:

```
$ mimetype file.ext

```

returns the mimetype of a file,

```
$ mimetype -d file.extension

```

returns a description of that mimetype.

When _xdg-open_ fails to detect one of the [desktop environments](/index.php/Desktop_environments "Desktop environments") it knows about, it normally falls back to using `file -i`, which uses only file contents to determine the mimetype, resulting in some file types not being detected correctly. With _mimetype_ available, _xdg-open_ will use that instead, with better detection results, as _mimetype_ uses the information in the [shared mime info database](http://standards.freedesktop.org/shared-mime-info-spec/shared-mime-info-spec-0.18.html).

### Environment variables

Some environment variables, such as `BROWSER`, `DE`, and `DESKTOP_SESSION`, will change the behaviour of the default _xdg-open_. See [Environment variables](/index.php/Environment_variables "Environment variables") for more information.