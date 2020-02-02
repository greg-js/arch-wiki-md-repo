Programs implement default application associations in different ways. While command-line programs traditionally use [environment variables](/index.php/Environment_variables#Default_programs "Environment variables"), graphical applications tend to use [XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications") through either the [GIO](https://en.wikipedia.org/wiki/GIO_(software) API, the [Qt](/index.php/Qt "Qt") API, or by executing `/usr/bin/xdg-open`, which is part of [xdg-utils](/index.php/Xdg-utils "Xdg-utils"). Because [xdg-open](/index.php/Xdg-open "Xdg-open") and [XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications") are quite complex, various alternative [resource openers](#Resource_openers) were developed. The following table lists example applications for each method.

| Method | Uses XDG | Application examples |
| [GIO's GAppInfo](https://developer.gnome.org/gio/stable/GAppInfo.html) | Yes | [Firefox](/index.php/Firefox "Firefox"), [GNOME Files](/index.php/GNOME_Files "GNOME Files"), [PCManFM](/index.php/PCManFM "PCManFM"), [Thunar](/index.php/Thunar "Thunar"), [Thunderbird](/index.php/Thunderbird "Thunderbird") |
| `/usr/bin/xdg-open` | By default | [Chromium](/index.php/Chromium "Chromium") |
| custom | Usually not | [mc](/index.php/Mc "Mc"), [ranger](/index.php/Ranger "Ranger") |
| [environment variables](/index.php/Environment_variables#Default_programs "Environment variables") | No | [man](/index.php/Man "Man"), [sudoedit](/index.php/Sudoedit "Sudoedit"), [systemctl](/index.php/Systemctl "Systemctl") |
| [D-Bus](/index.php/D-Bus "D-Bus")'s FileManager1 | org.freedesktop.FileManager1 | [Firefox](/index.php/Firefox "Firefox") (Open containing folder) |

Many [desktop environments](/index.php/Desktop_environment "Desktop environment") and graphical [file managers](/index.php/File_manager "File manager") provide a GUI for configuring default applications.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Background information](#Background_information)
*   [2 Resource openers](#Resource_openers)
    *   [2.1 xdg-open](#xdg-open)
    *   [2.2 perl-file-mimeinfo](#perl-file-mimeinfo)
    *   [2.3 mimeo](#mimeo)
    *   [2.4 whippet](#whippet)
    *   [2.5 Minimalist replacements](#Minimalist_replacements)
        *   [2.5.1 run-mailcap](#run-mailcap)

## Background information

Programs sometimes need to open a file or a [URI](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier "wikipedia:Uniform Resource Identifier") in the user's preferred application. To open a file in the user's preferred application the filetype needs to be detected (usually using filename extensions or [magic numbers](https://en.wikipedia.org/wiki/List_of_file_signatures "wikipedia:List of file signatures") mapped to [MIME types](https://en.wikipedia.org/wiki/Media_type "wikipedia:Media type")) and there needs to be an application associated with the filetype.

[Heirloom](/index.php/Heirloom "Heirloom") UNIX programs used [mime.types](https://en.wikipedia.org/wiki/Media_type#mime.types "wikipedia:Media type") for MIME type detection and [mailcap](https://en.wikipedia.org/wiki/Media_type#Mailcap "wikipedia:Media type") for application association.

## Resource openers

*   **XDG MIME Apps**: implements the [XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications") specification
*   **RegEx rules**: allows MIME types to be associated with applications using regular expressions
*   **URI support**: allows arbitrary URI schemes to be associated with applications

| Name | Package | XDG MIME Apps | RegEx rules | URI support |
| [xdg-open](/index.php/Xdg-open "Xdg-open") | [xdg-utils](/index.php/Xdg-utils "Xdg-utils") | Yes | No | Yes |
| [mimeopen(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mimeopen.1p) | [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) | Yes | No | No |
| mimeo | [mimeo](https://aur.archlinux.org/packages/mimeo/) | Yes | Yes | Yes |
| whippet | [whippet](https://aur.archlinux.org/packages/whippet/) | Yes | No | Yes |
| linopen | [linopen](https://aur.archlinux.org/packages/linopen/) | No | Yes | Yes |
| mimi | [mimi-git](https://aur.archlinux.org/packages/mimi-git/) | No | No | partly |
| busking | [busking-git](https://aur.archlinux.org/packages/busking-git/) | No | Yes | Yes |
| sx-open | [sx-open](https://aur.archlinux.org/packages/sx-open/) | No | Yes | Yes |
| [rifle(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rifle.1) | [ranger](/index.php/Ranger "Ranger") | No | Yes | No |

### xdg-open

[xdg-open](/index.php/Xdg-open "Xdg-open") (part of [xdg-utils](/index.php/Xdg-utils "Xdg-utils")) implements [XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications") and is used by many programs.

Because of the complexity of the [xdg-utils](/index.php/Xdg-utils "Xdg-utils") version of [xdg-open](/index.php/Xdg-open "Xdg-open"), it can be difficult to debug when the wrong default application is being opened. Because of this, there are many alternatives that attempt to improve upon it. Several of these alternatives replace the `/usr/bin/xdg-open` executable, thus changing the default application behavior of most applications. Others simply provide an alternative method of choosing default applications.

### perl-file-mimeinfo

[perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) provides the tools [mimeopen(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mimeopen.1p) and [mimetype(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mimetype.1p). These have a slightly nicer interface than their [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) equivalents:

```
# determine a file's MIME type
$ mimetype photo.jpeg
photo.jpeg: image/jpeg

# choose the default application for this file
$ mimeopen -d photo.jpeg
Please choose an application

    1) Feh (feh)
    2) GNU Image Manipulation Program (gimp)
    3) Pinta (pinta)

use application #

# open a file with its default application
$ mimeopen -n photo.jpeg

```

Most importantly, [xdg-utils](/index.php/Xdg-utils "Xdg-utils") programs will actually call `file` instead of `mimetype` for MIME type detection if it does not detect your [desktop environment](/index.php/Desktop_environment "Desktop environment"). This is important because `file` does not follow the XDG standard.

**Note:** [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) before 0.28-1 did not *entirely* follow the XDG standard. For example it did not not read [distribution-wide defaults](https://github.com/mbeijen/File-MimeInfo/issues/20) and it saved its config in [deprecated locations](https://github.com/mbeijen/File-MimeInfo/issues/8).

### mimeo

[mimeo](https://aur.archlinux.org/packages/mimeo/) provides the tool `mimeo`, which unifies the functionality of `xdg-open` and `xdg-mime`.

```
# determine a file's MIME type
$ mimeo -m photo.jpeg
photo.jpeg
  image/jpeg

# choose the default application for this MIME type
$ mimeo --add image/jpeg feh.desktop

# open a file with its default application
$ mimeo photo.jpeg

```

However a big difference with *xdg-utils* is that mimeo also supports custom "association files" that allow for more complex associations. For example, passing specific command line arguments based on a regular expression match:

```
# open youtube links in VLC without opening a new instance
vlc --one-instance --playlist-enqueue %U
  ^https?://(www.)?youtube.com/watch\?.*v=

```

[xdg-utils-mimeo](https://aur.archlinux.org/packages/xdg-utils-mimeo/) patches *xdg-utils* so that `xdg-open` falls back to mimeo if no desktop environment is detected.

### whippet

[whippet](https://aur.archlinux.org/packages/whippet/) provides the tool `whippet`, which is similar to `xdg-open`. It has X11 integration by using [libnotify](https://www.archlinux.org/packages/?name=libnotify) to display errors and [dmenu](https://www.archlinux.org/packages/?name=dmenu) to display choices between applications to open.

```
# open a file with its default application
$ whippet -M photo.jpeg

# choose from all possible applications for opening a file (without setting a default)
$ whippet -m photo.jpeg

```

In addition to implementing [XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications"), *whippet* can also use a SQlite database of weighted application/MIME type/regex associations to determine which app to use.

### Minimalist replacements

The following packages conflict with and provide [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) because they provide their own `/usr/bin/xdg-open` script.

If you want to use one of these resource openers while still being able to use [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils), install them manually in a PATH directory before `/usr/bin`.

*   [linopen](https://aur.archlinux.org/packages/linopen/) - 170-line Bash script, supports regex rules
*   [mimi-git](https://aur.archlinux.org/packages/mimi-git/) - 130-line Bash script, can change command arguments for each MIME type
*   [busking-git](https://aur.archlinux.org/packages/busking-git/) - 80-line Perl script similar to *mimi* but also supports regex rules
*   [sx-open](https://aur.archlinux.org/packages/sx-open/) - 60-line Bash script, uses a simple shell-based config file

#### run-mailcap

**Warning:** If you use [run-mailcap](https://aur.archlinux.org/packages/run-mailcap/), it is possible for `xdg-open` to delegate to it. This will cause an infinite loop if you are using the `/etc/mailcap` from [mailcap](https://www.archlinux.org/packages/?name=mailcap), because it also delegates to `xdg-open`.