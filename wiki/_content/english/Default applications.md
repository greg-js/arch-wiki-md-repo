Related articles

*   [Desktop entries](/index.php/Desktop_entries "Desktop entries")
*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Window manager](/index.php/Window_manager "Window manager")

There is frequently more than one application able to handle data of a certain type, so users and even some packages assemble lists of default applications for each [#MIME type](#MIME_types). While the base install of Arch Linux does not define default applications, [desktop environments](/index.php/Desktop_environments "Desktop environments") you install may do so. Some desktop environments also provide a GUI or a file-manager which can interactively configure default applications. If you do not use a desktop environment, you may need to install additional software in order to conveniently manage default applications.

## Contents

*   [1 MIME types](#MIME_types)
    *   [1.1 MIME database](#MIME_database)
        *   [1.1.1 New MIME types](#New_MIME_types)
    *   [1.2 Desktop entries](#Desktop_entries)
*   [2 Set default applications](#Set_default_applications)
    *   [2.1 Environment variables](#Environment_variables)
    *   [2.2 XDG standard](#XDG_standard)
        *   [2.2.1 Format](#Format)
    *   [2.3 mailcap](#mailcap)
*   [3 Utilities](#Utilities)
    *   [3.1 xdg-utils](#xdg-utils)
    *   [3.2 xdg-open alternatives](#xdg-open_alternatives)
        *   [3.2.1 perl-file-mimeinfo](#perl-file-mimeinfo)
        *   [3.2.2 mimeo](#mimeo)
        *   [3.2.3 whippet](#whippet)
        *   [3.2.4 Naive replacements](#Naive_replacements)
    *   [3.3 lsdesktopf](#lsdesktopf)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Missing .desktop file](#Missing_.desktop_file)
    *   [4.2 Missing association](#Missing_association)
    *   [4.3 Non-default application](#Non-default_application)
    *   [4.4 Nonstandard association](#Nonstandard_association)
    *   [4.5 Variables in .desktop files that affect application launch](#Variables_in_.desktop_files_that_affect_application_launch)

## MIME types

Before setting the default application per file type, the file type must be detected. There are two common ways that this detection is done:

*   using the file name extension e.g. *.html* or *.jpeg*
*   using a [magic number](https://en.wikipedia.org/wiki/List_of_file_signatures "w:List of file signatures") in the first few bytes of the file

However it is possible that a single file type is identified by several different magic numbers and file name extensions, therefore [MIME types](https://en.wikipedia.org/wiki/MIME_type "w:MIME type") are used to represent distinct file types. MIME types are specified by two parts separated by a slash: `*type*/*subtype*`. The type describes the general category of the content, while the subtype identifies the specific data type. For example, `image/jpeg` is the MIME type for [JPEG](https://en.wikipedia.org/wiki/JPEG "w:JPEG") images, while `video/H264` is the MIME type for [H.264](https://en.wikipedia.org/wiki/H.264/MPEG-4_AVC "w:H.264/MPEG-4 AVC") video.

Technically, every MIME type should be registered with the [IANA](https://en.wikipedia.org/wiki/Internet_Assigned_Numbers_Authority "w:Internet Assigned Numbers Authority")[[1]](http://www.iana.org/assignments/media-types/media-types.xhtml), however many applications use unofficial MIME types; these often have a type starting with `x-`, for example `x-scheme-handler/https` for a HTTPS URL. For local use, the [#MIME database](#MIME_database) can be used by other packages to register new MIME types.

### MIME database

The system maintains a database of recognized MIME types: the [Shared MIME-info Database](https://specifications.freedesktop.org/shared-mime-info-spec/shared-mime-info-spec-0.11.html#idm139839923550176). The database is built from the XML files installed by packages in `/usr/share/mime/packages` using the tools from [shared-mime-info](https://www.archlinux.org/packages/?name=shared-mime-info).

The files in `/usr/share/mime/` should not be directly edited, however it is possible to maintain a separate database on a per-user basis in the `~/.local/share/mime/` tree.

#### New MIME types

This example defines a new MIME type `application/x-foobar` and assigns it to any file with a name ending in *.foo*. Simply create the following file:

 `~/.local/share/mime/packages/application-x-foobar.xml` 
```
<?xml version="1.0" encoding="UTF-8"?>
<mime-info xmlns="http://www.freedesktop.org/standards/shared-mime-info">
    **<mime-type type="application/x-foobar">**
        <comment>foo file</comment>
        <icon name="application-x-foobar"/>
        <glob-deleteall/>
        **<glob pattern="*.foo"/>**
    </mime-type>
</mime-info>
```

And then update the MIME database

```
$ update-mime-database ~/.local/share/mime

```

Of course this will not have any effect if no desktop entries are associated with the MIME type. You may need to create new [desktop entries](/index.php/Desktop_entries "Desktop entries") or modify [#mimeapps.list](#XDG_standard).

### Desktop entries

Each package can use [desktop entries](/index.php/Desktop_entries "Desktop entries") to provide information about the MIME types that can be handled by the packaged software. In order to provide fast search in the reverse direction, the system uses the tools from the [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils) package to analyze the desktop files and to create an inverse mapping stored in the `/usr/share/applications/mimeinfo.cache` file. This is the only file that programs need to read to find all desktop files that might be used to handle given MIME type. Using the database is easier and faster than reading hundreds of *.desktop* files directly.

The files in `/usr/share/applications/` should not be edited directly, it is possible to maintain a separate database on a per-user basis in the `~/.local/share/applications/` tree. See [Desktop entries](/index.php/Desktop_entries "Desktop entries") for details.

## Set default applications

The configuration of default applications depends on which launcher is used. Unfortunately there are multiple incompatible standards and many programs even have their own custom formats.

The most common standards are explained below for manual editing. There are also several [#Utilities](#Utilities) which can do the job, which may or may not implement the following standards.

### Environment variables

Console programs in particular are configured by setting an appropriate [environment variable](/index.php/Environment_variable "Environment variable"), e.g. `BROWSER` or `EDITOR`. See [Environment variables#Examples](/index.php/Environment_variables#Examples "Environment variables").

### XDG standard

The [XDG standard](https://specifications.freedesktop.org/mime-apps-spec/mime-apps-spec-1.0.html) is the most common for configuring desktop environments. Default applications for each MIME type are stored in `mimeapps.list` files, which can be stored in several locations. They are searched in the following order, with earlier associations taking precedence over later ones:

| Path | Usage |
| `~/.config/mimeapps.list` | user overrides |
| `/etc/xdg/mimeapps.list` | system-wide overrides |
| `~/.local/share/applications/mimeapps.list` | (**deprecated**) user overrides |
| `/usr/local/share/applications/mimeapps.list`
`/usr/share/applications/mimeapps.list` | distribution-provided defaults |

Additionally, it is possible to define [desktop environment](/index.php/Desktop_environment "Desktop environment")-specific default applications in a file named `*desktop*-mimeapps.list` where `*desktop*` is the name of the desktop environment (from the `XDG_CURRENT_DESKTOP` environment variable). For example, `/etc/xdg/xfce-mimeapps.list` defines system-wide default application overrides for [Xfce](/index.php/Xfce "Xfce"). These desktop-specific overrides take precedence over the corresponding non-desktop-specific file. For example, `/etc/xdg/xfce-mimeapps.list` takes precedence over `/etc/xdg/mimeapps.list` but is still overridden by `~/.config/mimeapps.list`.

**Tip:** Although deprecated, several applications still read/write to `~/.local/share/applications/mimeapps.list`. To simplify maintenance, simply symlink it `$ ln -s ~/.config/mimeapps.list ~/.local/share/applications/mimeapps.list` . Note that the symlink must be in this direction because [#xdg-utils](#xdg-utils) deletes and recreates `~/.config/mimeapps.list` when it writes to it, which will break any symbolic/hard links

**Note:** You might also find files in these locations named `defaults.list`. This file is similar to `mimeapps.list` except it only lists default applications (not added/removed associations). It is now deprecated and should be manually merged with `mimeapps.list`.

#### Format

Consider the following example:

 `mimeapps.list` 
```
[Added Associations]
image/jpeg=bar.desktop;baz.desktop
video/H264=bar.desktop
[Removed Associations]
video/H264=baz.desktop
[Default Applications]
image/jpeg=foo.desktop
```

Each section assigns one or more desktop entries to MIME types.

*   **Added Associations** indicates that the applications support opening that MIME type. For example, `bar.desktop` and `baz.desktop` can open JPEG images. This might affect the application list you see when right-clicking a file in a file browser.
*   **Removed Associations** indicates that the applications *do not* support that MIME type. For example, `baz.desktop` cannot open H.264 video.
*   **Default Applications** indicates that the applications should be the default choice for opening that MIME type. For example, JPEG images should be opened with `foo.desktop`. This implicitly adds an association between the application and the MIME type. If there are multiple applications, they are tried in order.

Each section is optional and can be omitted if unneeded.

### mailcap

The [mailcap(4)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mailcap.4) file format is used by mail programs such as [mutt](https://www.archlinux.org/packages/?name=mutt) and [sylpheed](https://www.archlinux.org/packages/?name=sylpheed) to open non-text files. To have those programs use [xdg-open](#xdg-utils), edit `~/.mailcap`:

 `~/.mailcap` 
```
*/*; xdg-open "%s"

```

**Warning:** If you use [run-mailcap](https://aur.archlinux.org/packages/run-mailcap/), it is possible for `xdg-open` to delegate to it. This will cause an infinite loop if you configured your `.mailcap` as described above.

## Utilities

While it is possible to configure default applications and MIME types by directly editing [#mimeapps.list](#XDG_standard) and the [#MIME database](#MIME_database), there are many tools that can simplify the process. These tools are also important because applications may delegate opening of files to these tools rather than trying to implement the MIME type standard themselves.

If you use a [desktop environment](/index.php/Desktop_environment "Desktop environment") you should first check if it provides its own utility. That should be preferred over these alternatives.

### xdg-utils

[xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) provides the official utilities for managing MIME types and default applications according to the [#XDG standard](#XDG_standard). Most importantly, it provides `/usr/bin/xdg-open` which many applications use to open a file with its default application. It is desktop-environment-independent in the sense that it attempts to use each environment's native default application tool and provides its own mechanism if no known environment is detected. Examples:

```
# determine a file's MIME type
$ xdg-mime query filetype photo.jpeg
image/jpeg

# determine the default application for a MIME type
$ xdg-mime query default image/jpeg
gimp.desktop

# change the default application for a MIME type
$ xdg-mime default feh.desktop image/jpeg

# open a file with its default application
$ xdg-open photo.jpeg

# shortcut to open all web MIME types with a single application
$ xdg-settings set default-web-browser firefox.desktop

# shortcut for setting the default application for a URL scheme
$ xdg-settings set default-url-scheme-handler irc xchat.desktop

```

**Tip:** If no desktop environment is detected, MIME type detection falls back to using [file](https://www.archlinux.org/packages/?name=file) which—ironically—does not implement the XDG standard. If you want [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) to work properly without a desktop environment, you will need to install [#perl-file-mimeinfo](#perl-file-mimeinfo) or one of the [#xdg-open alternatives](#xdg-open_alternatives).

### xdg-open alternatives

Because of the complexity of the [#xdg-utils](#xdg-utils) version of `xdg-open`, it can be difficult to debug when the wrong default application is being opened. Because of this, there are many alternatives that attempt to improve upon it. Several of these alternatives replace the `/usr/bin/xdg-open` binary, thus changing the default application behavior of most applications. Others simply provide an alternative method of choosing default applications.

#### perl-file-mimeinfo

[perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) provides the tools `mimeopen` and `mimetype`. These have a slightly nicer interface than their [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) equivalents:

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

Most importantly, [#xdg-utils](#xdg-utils) apps will actually call `mimetype` instead of `file` for MIME type detection, if it does not detect your [desktop environment](/index.php/Desktop_environment "Desktop environment"). This is important because `file` does not follow the [#XDG standard](#XDG_standard).

**Note:** [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) before 0.28-1 does not *entirely* follow the [#XDG standard](#XDG_standard). For example it does not read [distribution-wide defaults](https://github.com/mbeijen/File-MimeInfo/issues/20) and it saves its config in [deprecated locations](https://github.com/mbeijen/File-MimeInfo/issues/8).

#### mimeo

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

#### whippet

[whippet](https://aur.archlinux.org/packages/whippet/) provides the tool `whippet`, which is similar to `xdg-open`. It has X11 integration by using [libnotify](https://www.archlinux.org/packages/?name=libnotify) to display errors and [dmenu](https://www.archlinux.org/packages/?name=dmenu) to display choices between applications to open.

```
# open a file with its default application
$ whippet -M photo.jpeg

# choose from all possible applications for opening a file (without setting a default)
$ whippet -m photo.jpeg

```

In addition to the standard [#mimeapps.list](#XDG_standard), *whippet* can also use a SQlite database of weighted application/MIME type/regex associations to determine which app to use.

#### Naive replacements

The following packages replace [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) however they only provide an `xdg-open` script. These versions of `xdg-open` do not do any delegation to desktop-environment-specific tools and do not read/write the standard [#mimeapps.list](#XDG_standard) config file (each has its own custom config), so they may not integrate well with other programs that manipulate default applications. However you may find them simpler to use if you do not use a desktop environment.

**Warning:** If you need any `xdg-*` binaries from [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) other than `xdg-open` you should not use these applications, since they do not provide them.

| Package | Features |
| [linopen](https://aur.archlinux.org/packages/linopen/) | Allows regex rules, can specify fallback file opener |
| [mimi-git](https://aur.archlinux.org/packages/mimi-git/) | Can change command arguments for each MIME type |
| [busking-git](https://aur.archlinux.org/packages/busking-git/) | similar to *mimi* but also supports regex rules |
| [sx-open](https://aur.archlinux.org/packages/sx-open/) | uses a simple shell-based config file |

### lsdesktopf

[lsdesktopf](https://aur.archlinux.org/packages/lsdesktopf/) provides several methods of searching the MIME database and desktop MIME entries.

For example, to see all MIME extensions in the system's *.desktop* files that have MIME type `video` you can use `lsdesktopf --gm -gx video` or to search in the XML database files use `lsdesktopf --gdx -gx video`. To get a quick overview of how many and which *.desktop* files can be associated with a certain MIME type, use `lsdesktopf --gen-mimeapps`. To see all file name extensions in XML database files, use `lsdesktopf --gdx -gfx`.

## Troubleshooting

If a file is not being opened by your desired default application, there are several possible causes. You may need to check each case.

### Missing .desktop file

A [desktop entry](/index.php/Desktop_entry "Desktop entry") is required in order to associate an application with a MIME type. Ensure that such an entry exists and can be used to (manually) open files in the application.

### Missing association

If the application's desktop entry does not specify the MIME type under its `MimeType` key, it will not be considered when an application is needed to open that type. Edit [#mimeapps.list](#XDG_standard) to add an association between the .desktop file and the MIME type.

### Non-default application

If the desktop entry is associated with the MIME type, it may simply not be set as the default. Edit [#mimeapps.list](#XDG_standard) to set the default association.

### Nonstandard association

Applications are free to ignore or only partially implement the [#XDG standard](#XDG_standard). Check for usage of deprecated files such as `~/.local/share/applications/mimeapps.list` and `~/.local/share/applications/defaults.list`. If you are attempting to open the file from another application (e.g. a web browser or file manager) check if that application has its own method of selecting default applications.

### Variables in .desktop files that affect application launch

Desktop environments and file managers supporting the specifications launch programs according to definition in the *.desktop* files. See [Desktop entries#Application entry](/index.php/Desktop_entries#Application_entry "Desktop entries").

Usually, configuration of the packaged *.desktop* files is not required, but it may not be bug-free. Even if an application containing necessary MIME type description in the *.desktop* file `MimeType` variable that is used for association, it can fail to start correctly, not start at all or start without opening a file.

This may happen, for example, if the `Exec` variable is missing internal options needed for how to open a file, or how the application is shown in the menu. The `Exec` variable usually begins with `%`; for its currently supported options, see [exec-variables](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#exec-variables).

The following table lists the main variable entries of *.desktop* files that affect how an application starts, if it has a MIME type associated with it.

| Variable names | Example 1 content | Example 2 content | Description |
| DBusActivatable | DBusActivatable=true | DBusActivatable=false | Application interact with [D-Bus](https://www.freedesktop.org/wiki/Software/dbus/).
See also configuration: [D-Bus](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#dbus). |
| MimeType | MimeType=application/vnd.oasis.opendocument.text | MimeType=application/vnd.sun.xml.math | List of MIME types supported by application |
| StartupWMClass | StartupWMClass=google-chrome | StartupWMClass=xpad | Associate windows with the owning application |
| Terminal | Terminal=true | Terminal=false | Start in default terminal |