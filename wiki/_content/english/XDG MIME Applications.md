Related articles

*   [Desktop entries](/index.php/Desktop_entries "Desktop entries")
*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Window manager](/index.php/Window_manager "Window manager")

The [XDG MIME Applications specification](https://specifications.freedesktop.org/mime-apps-spec/mime-apps-spec-latest.html) builds upon the [#Shared MIME database](#Shared_MIME_database) and [#Desktop entries](#Desktop_entries) to provide [default applications](/index.php/Default_applications "Default applications").

## Contents

*   [1 Shared MIME database](#Shared_MIME_database)
    *   [1.1 New MIME types](#New_MIME_types)
*   [2 Desktop entries](#Desktop_entries)
*   [3 mimeapps.list](#mimeapps.list)
    *   [3.1 Format](#Format)
*   [4 Utilities](#Utilities)
    *   [4.1 lsdesktopf](#lsdesktopf)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Missing desktop entry](#Missing_desktop_entry)
    *   [5.2 Missing association](#Missing_association)
    *   [5.3 Non-default application](#Non-default_application)
    *   [5.4 Nonstandard association](#Nonstandard_association)
    *   [5.5 Variables in .desktop files that affect application launch](#Variables_in_.desktop_files_that_affect_application_launch)

## Shared MIME database

The [XDG Shared MIME-info Database specification](https://specifications.freedesktop.org/shared-mime-info-spec/shared-mime-info-spec-latest.html) facilitates a shared MIME database across desktop environments and allows applications to easily register new MIME types system-wide.

The database is built from the XML files installed by packages in `/usr/share/mime/packages/` using the tools from [shared-mime-info](https://www.archlinux.org/packages/?name=shared-mime-info).

The files in `/usr/share/mime/` should not be directly edited, however it is possible to maintain a separate database on a per-user basis in the `~/.local/share/mime/` tree.

"URI scheme handling [..] are handled through applications handling the `x-scheme-handler/foo mime-type`, where foo is the URI scheme in question."[[1]](https://specifications.freedesktop.org/shared-mime-info-spec/shared-mime-info-spec-latest.html#idm140625828587776)

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

And then update the MIME database:

```
$ update-mime-database ~/.local/share/mime

```

Of course this will not have any effect if no desktop entries are associated with the MIME type. You may need to create new [desktop entries](/index.php/Desktop_entries "Desktop entries") or modify [#mimeapps.list](#mimeapps.list).

## Desktop entries

Each package can use [desktop entries](/index.php/Desktop_entries "Desktop entries") to provide information about the MIME types that can be handled by the packaged software. In order to provide fast search in the reverse direction, the system uses the tools from the [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils) package to analyze the desktop files and to create an inverse mapping stored in the `/usr/share/applications/mimeinfo.cache` file. This is the only file that programs need to read to find all desktop files that might be used to handle given MIME type. Using the database is easier and faster than reading hundreds of *.desktop* files directly.

The files in `/usr/share/applications/` should not be edited directly, it is possible to maintain a separate database on a per-user basis in the `~/.local/share/applications/` tree. See [Desktop entries](/index.php/Desktop_entries "Desktop entries") for details.

## mimeapps.list

The [XDG standard](https://specifications.freedesktop.org/mime-apps-spec/mime-apps-spec-1.0.html) is the most common for configuring desktop environments. Default applications for each MIME type are stored in `mimeapps.list` files, which can be stored in several locations. They are searched in the following order, with earlier associations taking precedence over later ones:

| Path | Usage |
| `~/.config/mimeapps.list` | user overrides |
| `/etc/xdg/mimeapps.list` | system-wide overrides |
| `~/.local/share/applications/mimeapps.list` | (**deprecated**) user overrides |
| `/usr/local/share/applications/mimeapps.list`
`/usr/share/applications/mimeapps.list` | distribution-provided defaults |

Additionally, it is possible to define [desktop environment](/index.php/Desktop_environment "Desktop environment")-specific default applications in a file named `*desktop*-mimeapps.list` where `*desktop*` is the name of the desktop environment (from the `XDG_CURRENT_DESKTOP` environment variable). For example, `/etc/xdg/xfce-mimeapps.list` defines system-wide default application overrides for [Xfce](/index.php/Xfce "Xfce"). These desktop-specific overrides take precedence over the corresponding non-desktop-specific file. For example, `/etc/xdg/xfce-mimeapps.list` takes precedence over `/etc/xdg/mimeapps.list` but is still overridden by `~/.config/mimeapps.list`.

**Tip:** Although deprecated, several applications still read/write to `~/.local/share/applications/mimeapps.list`. To simplify maintenance, simply symlink it `$ ln -s ~/.config/mimeapps.list ~/.local/share/applications/mimeapps.list` . Note that the symlink must be in this direction because [xdg-utils](/index.php/Xdg-utils "Xdg-utils") deletes and recreates `~/.config/mimeapps.list` when it writes to it, which will break any symbolic/hard links

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

## Utilities

While it is possible to configure default applications and MIME types by directly editing [#mimeapps.list](#mimeapps.list) and the [#Shared MIME database](#Shared_MIME_database), there are many tools that can simplify the process. These tools are also important because applications may delegate opening of files to these tools rather than trying to implement the MIME type standard themselves.

If you use a [desktop environment](/index.php/Desktop_environment "Desktop environment") you should first check if it provides its own utility. That should be preferred over these alternatives.

The official [xdg-utils](/index.php/Xdg-utils "Xdg-utils") contain tools for managing MIME types and default applications according to the XDG standard ([xdg-mime](/index.php/Xdg-utils#xdg-mime "Xdg-utils")). Most importantly it provides [xdg-open](/index.php/Xdg-open "Xdg-open") which many applications use to open a file with its default application.

### lsdesktopf

[lsdesktopf](https://aur.archlinux.org/packages/lsdesktopf/) provides several methods of searching the MIME database and desktop MIME entries.

For example, to see all MIME extensions in the system's *.desktop* files that have MIME type `video` you can use `lsdesktopf --gm -gx video` or to search in the XML database files use `lsdesktopf --gdx -gx video`. To get a quick overview of how many and which *.desktop* files can be associated with a certain MIME type, use `lsdesktopf --gen-mimeapps`. To see all file name extensions in XML database files, use `lsdesktopf --gdx -gfx`.

## Troubleshooting

If a file is not being opened by your desired default application, there are several possible causes. You may need to check each case.

### Missing desktop entry

A [desktop entry](/index.php/Desktop_entry "Desktop entry") is required in order to associate an application with a MIME type. Ensure that such an entry exists and can be used to (manually) open files in the application.

### Missing association

If the application's desktop entry does not specify the MIME type under its `MimeType` key, it will not be considered when an application is needed to open that type. Edit [#mimeapps.list](#mimeapps.list) to add an association between the .desktop file and the MIME type.

### Non-default application

If the desktop entry is associated with the MIME type, it may simply not be set as the default. Edit [#mimeapps.list](#mimeapps.list) to set the default association.

### Nonstandard association

Applications are free to ignore or only partially implement the XDG standard. Check for usage of deprecated files such as `~/.local/share/applications/mimeapps.list` and `~/.local/share/applications/defaults.list`. If you are attempting to open the file from another application (e.g. a web browser or file manager) check if that application has its own method of selecting default applications.

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