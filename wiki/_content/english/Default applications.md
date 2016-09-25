Before setting the default application per file type, the file type must be detected. There are two common ways that this detection is done:

*   using the file name extension e.g. *.html* or *.jpeg*
*   using a [magic number](https://en.wikipedia.org/wiki/List_of_file_signatures "w:List of file signatures") in the first few bytes of the file

However it is possible that a single file type is identified by several different magic numbers and file name extensions, therefore [MIME types](https://en.wikipedia.org/wiki/MIME_type "w:MIME type") are used to represent distinct file types (regardless of the representation). In Arch, tools from the [shared-mime-info](https://www.archlinux.org/packages/?name=shared-mime-info) package are used to maintain the [#MIME database](#MIME_database), which is used by other packages to register new MIME types. Each package can also use [desktop entries](/index.php/Desktop_entries "Desktop entries") to provide information about the MIME types that can be handled by the packaged software.

While the base install of Arch Linux does not define default applications, [desktop environments](/index.php/Desktop_environments "Desktop environments") you install may do so. Some desktop environments also provide a GUI or a file-manager which can interactively configure default applications. If you do not use a desktop environment, you may need to install additional software in order to conveniently manage default applications.

**Note:** If you are looking for default applications in the sense of "default shell", "default text editor", etc. see [Environment variables#Examples](/index.php/Environment_variables#Examples "Environment variables").

## Contents

*   [1 MIME types and desktop entries](#MIME_types_and_desktop_entries)
*   [2 mimeapps.list](#mimeapps.list)
    *   [2.1 Format](#Format)
*   [3 MIME database](#MIME_database)
    *   [3.1 New MIME types](#New_MIME_types)
*   [4 Utilities to manage MIME types](#Utilities_to_manage_MIME_types)
    *   [4.1 Examples of usage](#Examples_of_usage)
        *   [4.1.1 Detect MIME type](#Detect_MIME_type)
        *   [4.1.2 Set use of MIME type by default](#Set_use_of_MIME_type_by_default)
    *   [4.2 Application launchers](#Application_launchers)
        *   [4.2.1 xdg-open](#xdg-open)
        *   [4.2.2 mimeopen](#mimeopen)
        *   [4.2.3 mailcap](#mailcap)
    *   [4.3 Extended practical examples](#Extended_practical_examples)
        *   [4.3.1 xdg-open](#xdg-open_2)
            *   [4.3.1.1 Set the default browser](#Set_the_default_browser)
    *   [4.4 lsdesktopf](#lsdesktopf)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Missing .desktop file](#Missing_.desktop_file)
    *   [5.2 Missing association](#Missing_association)
    *   [5.3 Non-default application](#Non-default_application)
    *   [5.4 Nonstandard association](#Nonstandard_association)
    *   [5.5 Variables in .desktop files that affect application launch](#Variables_in_.desktop_files_that_affect_application_launch)

## MIME types and desktop entries

MIME types are specified by two parts separated by a slash: `*type*/*subtype*`. The type describes the general category of the content, while the subtype identifies the specific data type. For example, `image/jpeg` is the MIME type for [JPEG](https://en.wikipedia.org/wiki/JPEG "w:JPEG") images, while `video/H264` is the MIME type for [H.264](https://en.wikipedia.org/wiki/H.264/MPEG-4_AVC "w:H.264/MPEG-4 AVC") video. Technically, every MIME type should be registered with the [IANA](https://en.wikipedia.org/wiki/Internet_Assigned_Numbers_Authority "w:Internet Assigned Numbers Authority")[[1]](http://www.iana.org/assignments/media-types/media-types.xhtml), however many applications use unofficial MIME types; these often have a type starting with `x-`, for example `x-scheme-handler/https` for a HTTPS URL.

Each MIME type is associated with a [desktop entry](/index.php/Desktop_entry "Desktop entry"), specifying which application should open files of that type. These associations are usually stored in [#mimeapps.list](#mimeapps.list) files, but some programs store them in their own custom configuration files. Additionally, `.desktop` files may list the MIME types that they are able to open.

If you ever require to create a custom association of a new file extension to a MIME type, see the the short [#Example: .xml and related .desktop configuration](#Example:_.xml_and_related_.desktop_configuration) and the [Association between MIME types and applications](http://standards.freedesktop.org/mime-apps-spec/mime-apps-spec-1.0.html) standard.

## mimeapps.list

Default applications for each MIME type are stored in `mimeapps.list` files. These files can be stored in several locations. They are searched in the following order, with earlier associations taking precedence over later ones:

| Path | Usage |
| `~/.config/mimeapps.list` | user overrides |
| `/etc/xdg/mimeapps.list` | system-wide overrides |
| `~/.local/share/applications/mimeapps.list` | (**deprecated**) user overrides |
| `/usr/local/share/applications/mimeapps.list`
`/usr/share/applications/mimeapps.list` | distribution-provided defaults |

Additionally, it is possible to define [desktop-environment](/index.php/Desktop_environment "Desktop environment")-specific default applications in a file named `*desktop*-mimeapps.list` where `*desktop*` is the name of the desktop environment (from the `XDG_CURRENT_DESKTOP` environment variable). For example, `/etc/xdg/xfce-mimeapps.list` defines system-wide default application overrides for [XFCE](/index.php/XFCE "XFCE"). These desktop-specific overrides take precedence over the corresponding non-desktop-specific file. For example, `/etc/xdg/xfce-mimeapps.list` takes precedence over `/etc/xdg/mimeapps.list` but is still overridden by `~/.config/mimeapps.list`.

**Tip:** Although deprecated, several applications still read/write to `~/.local/share/applications/mimeapps.list`. To simplify maintenance, simply symlink it to the non-deprecated one:
```
$ ln -s ~/.config/mimeapps.list ~/.local/share/applications/mimeapps.list

```

**Note:** You might also find files in these locations named `defaults.list`. This file is similar to `mimeapps.list` except it only lists default applications (not added/removed associations). It is now deprecated and should be manually merged with `mimeapps.list`.

### Format

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

## MIME database

The system maintains a database of recognized MIME types: the [Shared MIME-info Database](https://specifications.freedesktop.org/shared-mime-info-spec/shared-mime-info-spec-0.11.html#idm139839923550176). The database is automatically built from the XML files installed by packages in `/usr/share/mime/packages` and `/usr/share/mimelnk/application`. These XML files should not be directly edited, however it is possible to define new MIME types on a per-user basis.

### New MIME types

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

Of course this will not have any affect if no desktop entries are associated with the MIME type. You may need to create new [desktop entries](/index.php/Desktop_entries "Desktop entries") or modify [#mimeapps.list](#mimeapps.list).

## Utilities to manage MIME types

Many of the file managers has options to set up and configure associations of mime types with programs.

It can be done by using:

*   Preferences for selected file
*   File manager configuration menu
*   External program for a specific file manager

Other utilities to manage MIME types are:

| Name/Package | Method | Based on | xdg-utils replacement | Configuration file |
| [mime-editor](https://www.archlinux.org/packages/?name=mime-editor) | MIME type | Utility for [ROX](http://rox.sourceforge.net/desktop/home.html) applications |
| [busking-git](https://aur.archlinux.org/packages/busking-git/) | regex | [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) | yes | custom |
| [linopen](https://aur.archlinux.org/packages/linopen/) | [file](https://www.archlinux.org/packages/?name=file) | custom |
| [mimeo](https://aur.archlinux.org/packages/mimeo/) | MIME type
regex | [file](https://www.archlinux.org/packages/?name=file) | [xdg-utils-mimeo](https://aur.archlinux.org/packages/xdg-utils-mimeo/) | `mimeapps.list`
`defaults.list`
custom is optional |
| [mimi-git](https://aur.archlinux.org/packages/mimi-git/) | [file](https://www.archlinux.org/packages/?name=file) | yes | custom |
| `rifle`
part of [ranger](https://www.archlinux.org/packages/?name=ranger) | MIME type
name
regex | [file](https://www.archlinux.org/packages/?name=file) | custom |
| [sx-open](https://aur.archlinux.org/packages/sx-open/) | regex | [file](https://www.archlinux.org/packages/?name=file)
bash regex | yes | custom |
| [whippet](https://aur.archlinux.org/packages/whippet/) | MIME type
name
regex | SQLite database
[file](https://www.archlinux.org/packages/?name=file)
[perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo), etc | xdg-open | custom SQLite database
`mimeapps.list` |
| [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) | [file](https://www.archlinux.org/packages/?name=file)
[perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) |

### Examples of usage

Here is a short description about how to use command line tools to show MIME type of a file or set preferred program as default to open MIME type.

#### Detect MIME type

Tools detecting MIME type by reading meta-data from header of the file or detecting by magic number that is in two bytes identifier in the begin of the file. See [File header](https://en.wikipedia.org/wiki/File_format#File_header "wikipedia:File format").

Many programs are using command *file* to detect correct MIME type. For detection it uses compiled database that is stored in the `/usr/share/misc/magic/` directory. It has many options to determinate correct MIME type and for showing output.

In Linux it is two standards to detect MIME type that can affect which program will start and open the file, e.g. extension is associated with one program but content is associated with another MIME type. The simplest way to see what is your system prioritizes is by renaming file extension and check again with tools that can use custom [*.xml](#Associate_file_extensions_with_applications_MIME_type) configuration files.

Here is examples of utility *xdg-mime* that first checking association of extension in [*.xml](#Associate_file_extensions_with_applications_MIME_type) configuration files.

| Without extension | With extension |
| xdg-mime query filetype *foo-file* | xdg-mime query filetype *foo-file*.*jpg* |
| application/vnd.oasis.opendocument.text | image/jpeg |

Comparison functionality of the tools

Here is shown options only for simple or multiple checks of a file, for more options read their own documentation.

| Tool | Option | Detection order | Functionality | Type | Interface |
| file | *(has many)* | Magic(Byte/Pattern) | Show only | binary | terminal |
| xdg-mime | query filetype | *.xml -> Magic | Show / Set | script | terminal |
| mimetype | -i *(*.xml)* -M *(Magic)* | *.xml -> Magic | Show only | script | terminal |
| mimeo | -m | *.xml -> Magic | Show / Set / Launch | script | terminal |

#### Set use of MIME type by default

Comparison functionality of the tools

Here is shown options only for single file associations, for more options read their own documentation.

| Tool | Option | Functionality | Type | Interface |
| xdg-mime | default **.desktop* Type1/Extension1 Type2/Extension2 | Show / Set | script | terminal |
| mimeo | --prefer 'regex:^Type/(Extension**1** |Extension?**2**)$' **.desktop* | Show / Set / Launch | script | terminal |
| mimeopen | --ask-default *(interactive)* | Set / Launch | script | terminal |

### Application launchers

#### xdg-open

*xdg-open* (from the [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) package) uses [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) as a fallback ("generic") method if no [desktop environment](/index.php/Desktop_environment "Desktop environment") is detected. It is a desktop-independent tool. Many applications invoke the `xdg-open` command internally. Inside a [desktop environment](/index.php/Desktop_environment "Desktop environment") it passes the arguments to desktop supported environment's file-opener applications (e.g. *gvfs-open*, *kde-open*, or *exo-open*). When no desktop environment is detected the *xdg-open* will use its own configuration files.

#### mimeopen

*mimeopen* (from the [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) package) can launch applications from command line. It can use custom database and prompt user to chose default application from a list of detected relevant and offers to chose own alternative.

Example of the prompt:

 `$ mimeopen -d /path/to/foo-file` 
```
 Please choose a default application for files of type *Type*/*Extension*
        1) notepad  (wine-extension-txt)
        2) Leafpad  (leafpad)
        3) OpenOffice.org Writer  (writer)
        4) gVim  (gvim)
        5) Other...

```

Your answer becomes the default handler for that type of file. Mimeopen is installed as `/usr/bin/vendor_perl/mimeopen`.

If you run *xdg-open* without a desktop environment, you should also install [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo), or [xdg-utils-mimeo](https://aur.archlinux.org/packages/xdg-utils-mimeo/) and [mimeo](https://aur.archlinux.org/packages/mimeo/) from the [AUR](/index.php/AUR "AUR") for a faster alternative.

#### mailcap

The [mailcap](http://linux.die.net/man/4/mailcap) file.

The *.mailcap* file format is used by mail programs such as [mutt](https://www.archlinux.org/packages/?name=mutt) and [sylpheed](https://www.archlinux.org/packages/?name=sylpheed). To have those programs use *xdg-open*, edit `~/.mailcap`:

 `~/.mailcap` 
```
*/*; xdg-open "%s"

```

### Extended practical examples

#### xdg-open

*xdg-mime* modifies the local file `~/.local/share/applications/mimeapps.list` (deprecated).

To **query** the mime type used by an existing file, use

```
$ xdg-mime query filetype *file.ext*

```

To change an associated desktop entry by setting [Thunar](/index.php/Thunar "Thunar") as the default file browser:

```
$ xdg-mime default Thunar.desktop inode/directory

```

Note that you should not specify the complete path, but only the name of the *.desktop* file.

This command can take multiple MIME types, allowing related files to be handled by the same program. The example below associates [Emacs](/index.php/Emacs "Emacs") to all known source files:

```
$ xdg-mime default emacs.desktop $(grep '^text/x-*' /usr/share/mime/types)

```

##### Set the default browser

To set the default application for `http(s)://` internet protocols:

```
$ xdg-mime default midori.desktop x-scheme-handler/http
$ xdg-mime default midori.desktop x-scheme-handler/https

```

As an alternative try:

```
$ xdg-settings set default-web-browser netsurf.desktop

```

To verify if the URLs opens correctly:

```
$ xdg-open https://archlinux.org

```

To associate *.html* files with the [netsurf](https://www.archlinux.org/packages/?name=netsurf) web-browser:

```
$ xdg-mime default netsurf.desktop text/html

```

It is important to note that if the envirnoment variable *BROWSER* is set, xdg will not be able to override it, which means *xdg-open* will use the browser set in the *BROWSER* env var rather than the one you specified with one of the commands above.

### lsdesktopf

[lsdesktopf](https://aur.archlinux.org/packages/lsdesktopf/) provides several methods of searching the MIME database and desktop MIME entries.

For example, to see all MIME extensions in the system's *.desktop* files that have MIME type `video` you can use `lsdesktopf --gm -gx video` or to search in the XML database files use `lsdesktopf --gdx -gx video`. To get a quick overview of how many and which *.desktop* files can be associated with a certain MIME type, use `lsdesktopf --gen-mimeapps`. To see all file name extensions in XML database files, use `lsdesktopf --gdx -gfx`.

## Troubleshooting

If a file is not being opened by your desired default application, there are several possible causes. You may need to check each case.

### Missing .desktop file

A [desktop entry](/index.php/Desktop_entry "Desktop entry") is required in order to associate an application with a MIME type. Ensure that such an entry exists and can be used to (manually) open files in the application.

### Missing association

If the application's desktop entry does not specify the MIME type under its `MimeType` key, it will not be considered when an application is needed to open that type. Edit [#mimeapps.list](#mimeapps.list) to add an association between the .desktop file and the MIME type.

### Non-default application

If the desktop entry is associated with the MIME type, it may simply not be set as the default. Edit [#mimeapps.list](#mimeapps.list) to set the default association.

### Nonstandard association

The formats and procedures described in this article are merely a standard defined by freedesktop.org; applications are free to ignore or only partially implement the standard. Check for usage of deprecated files such as `~/.local/share/applications/mimeapps.list` and `~/.local/share/applications/defaults.list`. If you are attempting to open the file from another application (e.g. a web browser or file manager) check if that application has its own method of selecting default applications.

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