There is frequently more than one application able to handle data of a certain type, so users and even some packages assemble lists of default applications for each [#MIME type](#MIME_types). While the base install of Arch Linux does not define default applications, [desktop environments](/index.php/Desktop_environments "Desktop environments") you install may do so. Some desktop environments also provide a GUI or a file-manager which can interactively configure default applications. If you do not use a desktop environment, you may need to install additional software in order to conveniently manage default applications.

The configuration of default applications depends on which launcher is used. Unfortunately there are multiple incompatible standards and many programs even have their own custom formats.

The most common standards are explained below for manual editing. There are also several [#Launchers](#Launchers) which can do the job, which may or may not implement the following standards.

## Contents

*   [1 MIME types](#MIME_types)
*   [2 Standards](#Standards)
    *   [2.1 Environment variables](#Environment_variables)
    *   [2.2 XDG standard](#XDG_standard)
    *   [2.3 mailcap](#mailcap)
*   [3 Launchers](#Launchers)
    *   [3.1 xdg-open](#xdg-open)
    *   [3.2 perl-file-mimeinfo](#perl-file-mimeinfo)
    *   [3.3 mimeo](#mimeo)
    *   [3.4 whippet](#whippet)
    *   [3.5 Minimalist replacements](#Minimalist_replacements)

## MIME types

Before setting the default application per file type, the file type must be detected. There are two common ways that this detection is done:

*   using the file name extension e.g. *.html* or *.jpeg*
*   using a [file signature](https://en.wikipedia.org/wiki/List_of_file_signatures "wikipedia:List of file signatures") in the first few bytes of the file

However it is possible that a single file type is identified by several different magic numbers and file name extensions, therefore [MIME types](https://en.wikipedia.org/wiki/MIME_type "wikipedia:MIME type") are used to represent distinct file types. MIME types are specified by two parts separated by a slash: `*type*/*subtype*`. The type describes the general category of the content, while the subtype identifies the specific data type. For example, `image/jpeg` is the MIME type for [JPEG](https://en.wikipedia.org/wiki/JPEG "w:JPEG") images, while `video/H264` is the MIME type for [H.264](https://en.wikipedia.org/wiki/H.264/MPEG-4_AVC "wikipedia:H.264/MPEG-4 AVC") video.

Technically, every MIME type should be registered with the [IANA](https://en.wikipedia.org/wiki/Internet_Assigned_Numbers_Authority "wikipedia:Internet Assigned Numbers Authority")[[1]](http://www.iana.org/assignments/media-types/media-types.xhtml), however many applications use unofficial MIME types; these often have a type starting with `x-`, for example `x-scheme-handler/https` for a HTTPS URL. For local use, the [XDG MIME Applications#Shared MIME database](/index.php/XDG_MIME_Applications#Shared_MIME_database "XDG MIME Applications") can be used by other packages to register new MIME types.

## Standards

### Environment variables

Console programs in particular are configured by setting an appropriate [environment variable](/index.php/Environment_variable "Environment variable"), e.g. `BROWSER` or `EDITOR`. See [Environment variables#Default programs](/index.php/Environment_variables#Default_programs "Environment variables").

### XDG standard

See [XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications").

### mailcap

Some applications use the UNIX-traditional [mailcap and mime.types](https://en.wikipedia.org/wiki/Media_type#Mailcap "wikipedia:Media type") files. See [RFC 1524](https://tools.ietf.org/html/rfc1524) and [mailcap(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mailcap.4) for the format documentation.

The [mailcap](https://www.archlinux.org/packages/?name=mailcap) package provides a `/etc/mailcap` that uses [xdg-open(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdg-open.1) for the most common MIME types.

**Warning:** If you use [run-mailcap](https://aur.archlinux.org/packages/run-mailcap/), it is possible for `xdg-open` to delegate to it. This will cause an infinite loop if you configured your `mailcap` as described above.

## Launchers

### xdg-open

*   [xdg-open](/index.php/Xdg-open "Xdg-open")

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

Most importantly, [#xdg-utils](#xdg-utils) apps will actually call `mimetype` instead of `file` for MIME type detection, if it does not detect your [desktop environment](/index.php/Desktop_environment "Desktop environment"). This is important because `file` does not follow the XDG standard.

**Note:** [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) before 0.28-1 does not *entirely* follow the XDG standard. For example it does not read [distribution-wide defaults](https://github.com/mbeijen/File-MimeInfo/issues/20) and it saves its config in [deprecated locations](https://github.com/mbeijen/File-MimeInfo/issues/8).

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
vlc --one-instance --playlist-enqueue %U
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

In addition to the standard [#mimeapps.list](#mimeapps.list), *whippet* can also use a SQlite database of weighted application/MIME type/regex associations to determine which app to use.

### Minimalist replacements

The following packages replace [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) however they only provide an `xdg-open` script. These versions of `xdg-open` do not do any delegation to desktop-environment-specific tools and do not read/write the standard [#mimeapps.list](#mimeapps.list) config file (each has its own custom config), so they may not integrate well with other programs that manipulate default applications. However you may find them simpler to use if you do not use a desktop environment.

**Warning:** If you need any `xdg-*` binaries from [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) other than `xdg-open` you should not use these applications, since they do not provide them.

*   [linopen](https://aur.archlinux.org/packages/linopen/) - 170-line Bash script, supports regex rules
*   [mimi-git](https://aur.archlinux.org/packages/mimi-git/) - 130-line Bash script, can change command arguments for each MIME type
*   [busking-git](https://aur.archlinux.org/packages/busking-git/) - 80-line Perl script similar to *mimi* but also supports regex rules
*   [sx-open](https://aur.archlinux.org/packages/sx-open/) - 60-line Bash script, uses a simple shell-based config file