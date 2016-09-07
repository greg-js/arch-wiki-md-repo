Setting default applications per file type involves detection of the file type as the first step. Since the application launcher cannot fully understand all file types, the detection is based on reading only a small part of the file. There are two common ways to determine the file type:

*   using the file name extension, for example *.html* or *.jpeg*
*   using the so-called "magic bytes" at the start of the file

The first method is very simple and fast, but inaccurate if the file is not named "correctly". The second is more accurate, but slower.

Since files are not required to have an extension and multiple file name extensions can be used for the same file type, [MIME types](https://en.wikipedia.org/wiki/MIME_type "w:MIME type") are commonly used instead to uniquely represent the type of a file. In Arch, tools from the [shared-mime-info](https://www.archlinux.org/packages/?name=shared-mime-info) package are used to maintain the MIME type database, which is used by other packages to register new MIME types. Each package can also use the [Desktop entries](/index.php/Desktop_entries "Desktop entries") to provide information about the MIME types that can be handled by the packaged software. There is frequently more than one application able to handle data of a certain MIME type, so users and even some packages (e.g. [desktop environments](/index.php/Desktop_environments "Desktop environments")) assemble lists of default applications for each MIME type.

Note that while Arch Linux does not provide custom presets for default applications, the [desktop environment](/index.php/Desktop_environment "Desktop environment") you install may do so. Some desktop environments also provide a GUI or a file-manager which enables to interactively configure default applications for certain file extensions. If this suffices for your system usage, you may not need to configure anything further.

The scope of this article are the freedesktop [Association between MIME types and applications](https://specifications.freedesktop.org/mime-apps-spec/mime-apps-spec-1.0.html) specification and related parts of the [Shared MIME-info Database](https://specifications.freedesktop.org/shared-mime-info-spec/shared-mime-info-spec-0.11.html#idm139839923550176) specification.

## Contents

*   [1 MIME types and desktop entries](#MIME_types_and_desktop_entries)
*   [2 Set default applications](#Set_default_applications)
    *   [2.1 Default mimeapps.list files](#Default_mimeapps.list_files)
    *   [2.2 Configuration of the mimeapps.list file](#Configuration_of_the_mimeapps.list_file)
    *   [2.3 Shared MIME-info database](#Shared_MIME-info_database)
        *   [2.3.1 Example: .xml and related .desktop configuration](#Example:_.xml_and_related_.desktop_configuration)
*   [3 Utilities to manage MIME types](#Utilities_to_manage_MIME_types)
    *   [3.1 Examples of usage](#Examples_of_usage)
        *   [3.1.1 Detect MIME-type](#Detect_MIME-type)
        *   [3.1.2 Set use of MIME-type by default](#Set_use_of_MIME-type_by_default)
    *   [3.2 Application launchers](#Application_launchers)
        *   [3.2.1 xdg-open](#xdg-open)
        *   [3.2.2 mimeopen](#mimeopen)
        *   [3.2.3 mailcap](#mailcap)
    *   [3.3 Extended practical examples](#Extended_practical_examples)
        *   [3.3.1 xdg-open](#xdg-open_2)
            *   [3.3.1.1 Set the default browser](#Set_the_default_browser)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Variables in .desktop files that affect application launch](#Variables_in_.desktop_files_that_affect_application_launch)

## MIME types and desktop entries

MIME-types are specified by two slash (`/`) parts: *Type/Extension*, for example `video/x-ms-wmv`. The second part of the MIME-type is expanding faster, for example with new applications or data encoding standards.

The default applications to open a MIME-type are usually stored in [mimeapps.list](#Default_mimeapps.list_files) files, but some programs store MIME-type associations in their own custom configuration files. If a MIME-type association is not found in the default configuration, the program should look for the first match of the MIME-type in *.desktop* files.

Description of some MIME-type first part and examples of second parts:

| Type of MIME (1st part) | Description | Examples of extension (2nd part) |
| application | Files with binary content such, e.g.: documents,archives,... | epub+zip, ereader, excel, gbr, gzip |
| audio | Audio files that that can be played by a music player or audio editor | flac, m4a, midi |
| chemical | Chemical information, molecular and other chemical data | x-cif, x-cml, x-daylight-smiles, x-gamess-input, x-gamess-output, x-gaussian-checkpoint, x-gaussian-cube, x-gaussian-log, x-mopac-out, x-pdb, x-qchem-output, x-xyz |
| image | Image files that can be opened by image editor or image viewer | bmp, crw, g3fax, gif, jp2, jpeg, jpeg2000, jpg |
| inode | Can be opened by a file manager | blockdevice, chardevice, directory, fifo, mount-point, socket, symlink |
| message | Message protocols | delivery-status, disposition-notification, external-body, news, partial, rfc822, x-gnu-rmail |
| misc | Streaming meta data | ultravox |
| text | Text documents that can be viewed (e.g. with command *less*) or opened with a text editor | html, javascript, mathml, mml, plain |
| video | Video files that can be played or edited with a video editor | flv, mp2t, mp4 |
| x-content | Content on disks such as e.g. Audio,Video,Image or blank disk | audio-cdda, audio-player, blank-bd, blank-cd, blank-dvd, blank-hddvd, image-picturecd, video-dvd, video-svcd, video-vcd |
| x-scheme-handler | Internet protocol | ftp, geo, ghelp, help, http, https, hwplay, icy, icyx, info, irc, magnet, mailto, man, mms, mmsh, net, pnm, rtmp, rtp, rtsp, skype, uvox, vnc, xmpp |
| x-epoc | SISX package | x-sisx-app |
| multipart | Multi-part mime messages | alternative, appledouble, digest, encrypted, mixed, related, report, signed, x-mixed-replace |
| model | such as 3D model | x-kpovmodeler, vrml, x-modelica |

For the description of MIME-types you can search in XDG database:

```
$ grep -e 'mime-type type=' -e '<comment>'  /usr/share/mime/packages/freedesktop.org.xml

```

**Tip:** To see all MIME extensions in the system's *.desktop* files that belongs to a MIME-type you can use [lsdesktopf](https://aur.archlinux.org/packages/lsdesktopf/), for example `lsdesktopf --gm -gx video`, to search available in *.xml* configuration/database files use `lsdesktopf --gdx -gx video`.

If you ever require to create a custom association of a new file extension to a MIME-type, see the the short [#Example: .xml and related .desktop configuration](#Example:_.xml_and_related_.desktop_configuration) and the [Association between MIME types and applications](http://standards.freedesktop.org/mime-apps-spec/mime-apps-spec-1.0.html) standard.

## Set default applications

In order to set a default application, you need to

*   decide which of the [#Default mimeapps.list files](#Default_mimeapps.list_files) is applicable for your case and,
*   change the [#Configuration of the mimeapps.list file](#Configuration_of_the_mimeapps.list_file) accordingly.

Any manual configuration of the [#Shared MIME-info database](#Shared_MIME-info_database) is only required, if the application is not setup correctly or desktop does not comply to the standard yet.

### Default mimeapps.list files

The `mimeapps.list` file stores the configuration for the default application to open a MIME-type. There are different locations for it:

*   system-wide,
*   per-user,
*   custom locations used by some programs.

The `*$desktop*` in the following list denotes the name of the related desktop environment or window manager. The search order of paths is:

| Path | Usage |
| `$HOME/.config/*$desktop*-mimeapps.list` | user overrides, desktop-specific |
| `$HOME/.config/mimeapps.list` | user overrides |
| `/etc/xdg/*$desktop*-mimeapps.list` | sysadmin and vendor overrides, desktop-specific |
| `/etc/xdg/mimeapps.list` | sysadmin and vendor overrides |
| `$HOME/.local/share/applications/*$desktop*-mimeapps.list` | for compatibility but now deprecated, desktop-specific |
| `$HOME/.local/share/applications/mimeapps.list` | for compatibility but now deprecated |
| `/usr/local/share/applications/*$desktop*-mimeapps.list`
`/usr/share/applications/$desktop-mimeapps.list` | distribution-provided defaults, desktop-specific |
| `/usr/local/share/applications/mimeapps.list`
`/usr/share/applications/mimeapps.list` | distribution-provided defaults |

### Configuration of the mimeapps.list file

The file contains two main sections for default and additional alternatives to open files of a MIME-type. The second and the third section (`[Removed Associations]`) are optional.

If the application installed a correct [desktop entry](/index.php/Desktop_entry "Desktop entry") file (examples used below `default1.desktop`, `foo1.desktop`, etc.), it contains the registered MIME-types it can handle. To **set a default application**, all you need to do is adjust the associations in the respective `mimeapps.list` (see also the freedesktop [specification](https://specifications.freedesktop.org/mime-apps-spec/mime-apps-spec-1.0.html#associations)).

For example, the following sets `default1.desktop` to open `mimetype1`:

```
[Default Applications]
mimetype1=default1.desktop

```

Defined additional associations of applications to MIME-types (these might appear in file manager *Open with* GUI, for example):

```
[Added Associations]
mimetype1=foo1.desktop;foo2.desktop;foo3.desktop;
mimetype2=foo4.desktop;

```

Removed associations of applications with MIME-types (blacklisting a MIME-type association of an application in its *.desktop* file):

```
[Removed Associations]
mimetype1=foo5.desktop

```

Multiple *.desktop* files for a single MIME-type must be semicolon-separated. Not supported entries are ignored in `mimeapps.list`. The DE/WM then searches for the first match to the needed MIME-type them in the default path for *.desktop* files.

**Tip:** To get a quick overview of how many and which *.desktop* files can be associated with a certain MIME-type, you can use the [lsdesktopf](https://aur.archlinux.org/packages/lsdesktopf/) utility, e.g. `lsdesktopf --gen-mimeapps`.

**Note:** Arch Linux itself does not provide system-wide presets for associations, but other distributions and specific desktop environments may do so via packaged `mimeapps.list` files, or the older and deprecated `defaults.list` files.

Your choice of desktop environment, or none, will affect how your default applications are associated. Further, note that some packages use additional work-around presets, for example Mozilla's packages install a `/etc/mime.types` file.

### Shared MIME-info database

In background to the `mimeapps.list` files, the system holds a database of MIME-type information registered via the installed applications' *.desktop* files, the [Shared MIME-info Database](https://specifications.freedesktop.org/shared-mime-info-spec/shared-mime-info-spec-0.11.html#idm139839923550176). It is created automatically as soon as an application depending on it is installed, via the following [pacman#Hooks](/index.php/Pacman#Hooks "Pacman"):

*   `/usr/share/libalpm/hooks/update-mime-database.hook` from [shared-mime-info](https://www.archlinux.org/packages/?name=shared-mime-info)

	updates the MIME-info database in `/usr/share/mime`, in particular also the *.xml* specification in `/usr/share/mime/packages/freedesktop.org.xml` for the MIME-types standards

*   `/usr/share/libalpm/hooks/update-desktop-database.hook` from [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils)

	updates the `mimeinfo.cache` located (per default) in `/usr/share/applications`

These files keep track of which MIME-types are associated with which *.desktop* files overall. When an application is installed, updated or removed, the pacman hooks keep the database updated accordingly.

**Warning:** The database files are not meant to be edited directly.

Application specific configuration is stored in *.xml* files and further files of the database (see [.xml source files](https://specifications.freedesktop.org/shared-mime-info-spec/shared-mime-info-spec-0.11.html#idm139839923550176)) are stored in *.keys* and *.mime* files that are located in `/usr/share/mime-info/`.

Global directories for the *.xml* files are:

```
/usr/share/mimelnk/application/
/usr/share/mime/packages/ 

```

**Warning:** Above should not be modified, for user-specific configuration see below.

Any user-specific *.xml* configuration may be stored in:

```
~/.local/share/mime/packages/

```

#### Example: .xml and related .desktop configuration

The following is a short example to *create* files to associate an application with a MIME-type. It only needs to be followed, if the application has **not** setup and registered its configuration sufficiently.

User-specific paths are used to override system defaults, while keeping the integrity of the rest of the system-wide configuration.

Create and edit `~/.local/share/mime/packages/application-x-foobar.xml`:

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

**Tip:** To see all file name extensions in *.xml* configuration or database files, that available in *glob pattern*, with their description in *comment* use [lsdesktopf](https://aur.archlinux.org/packages/lsdesktopf/): `lsdesktopf --gdx -gfx`.

Create a related [desktop entry](/index.php/Desktop_entry "Desktop entry") file:

 `~/.local/share/applications/foobar.desktop` 
```
[Desktop Entry]
Name=Foobar
Exec=/usr/bin/foobar
**MimeType=application/x-foobar**
Icon=foobar
Terminal=false
Type=Application
Categories=AudioVideo;Player;Video;
Comment=
```

Now update the application and mime database with:

```
$ update-desktop-database ~/.local/share/applications
$ update-mime-database    ~/.local/share/mime

```

Programs that use MIME-types, such as file managers, should now open `*.foo` files with foobar (you may need to restart your file manager to see the change.)

See also [Environment variables#Examples](/index.php/Environment_variables#Examples "Environment variables") about global variables that can be used in start-up scripts to set default applications for specific actions.

## Utilities to manage MIME types

Many of the file managers has options to set up and configure associations of mime types with programs.

It can be done by using:

*   Preferences for selected file
*   File manager configuration menu
*   External program for a specific file manager

Other utilities to manage MIME-types are:

| Name/Package | Method | Based on | xdg-utils replacement | Configuration file |
| [mime-editor](https://www.archlinux.org/packages/?name=mime-editor) | MIME-type | Utility for [ROX](http://rox.sourceforge.net/desktop/home.html) applications |
| [busking-git](https://aur.archlinux.org/packages/busking-git/) | regex | [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) | yes | custom |
| [linopen](https://aur.archlinux.org/packages/linopen/) | [file](https://www.archlinux.org/packages/?name=file) | custom |
| [mimeo](https://aur.archlinux.org/packages/mimeo/) | MIME-type
regex | [file](https://www.archlinux.org/packages/?name=file) | [xdg-utils-mimeo](https://aur.archlinux.org/packages/xdg-utils-mimeo/) | `mimeapps.list`
`defaults.list`
custom is optional |
| [mimi-git](https://aur.archlinux.org/packages/mimi-git/) | [file](https://www.archlinux.org/packages/?name=file) | yes | custom |
| `rifle`
part of [ranger](https://www.archlinux.org/packages/?name=ranger) | MIME-type
name
regex | [file](https://www.archlinux.org/packages/?name=file) | custom |
| [sx-open](https://aur.archlinux.org/packages/sx-open/) | regex | [file](https://www.archlinux.org/packages/?name=file)
bash regex | yes | custom |
| [whippet](https://aur.archlinux.org/packages/whippet/) | MIME-type
name
regex | SQLite database
[file](https://www.archlinux.org/packages/?name=file)
[perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo), etc | xdg-open | custom SQLite database
`mimeapps.list` |
| [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) | [file](https://www.archlinux.org/packages/?name=file)
[perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) |

### Examples of usage

Here is a short description about how to use command line tools to show MIME-type of a file or set preferred program as default to open MIME-type.

#### Detect MIME-type

Tools detecting MIME-type by reading meta-data from header of the file or detecting by magic number that is in two bytes identifier in the begin of the file. See [File header](https://en.wikipedia.org/wiki/File_format#File_header "wikipedia:File format").

Many programs are using command *file* to detect correct MIME-type. For detection it uses compiled database that is stored in the `/usr/share/misc/magic/` directory. It has many options to determinate correct MIME-type and for showing output.

In Linux it is two standards to detect MIME-type that can affect which program will start and open the file, e.g. extension is associated with one program but content is associated with another MIME-type. The simplest way to see what is your system prioritizes is by renaming file extension and check again with tools that can use custom [*.xml](#Associate_file_extensions_with_applications_MIME-type) configuration files.

Here is examples of utility *xdg-mime* that first checking association of extension in [*.xml](#Associate_file_extensions_with_applications_MIME-type) configuration files.

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

#### Set use of MIME-type by default

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

This command can take multiple mime-types, allowing related files to be handled by the same program. The example below associates [Emacs](/index.php/Emacs "Emacs") to all known source files:

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

## Troubleshooting

### Variables in .desktop files that affect application launch

Desktop environments and file managers supporting the specifications launch programs according to definition in the *.desktop* files. See [Desktop entries#Application entry](/index.php/Desktop_entries#Application_entry "Desktop entries").

Usually, configuration of the packaged *.desktop* files is not required, but it may not be bug-free. Even if an application containing necessary MIME-type description in the *.desktop* file `MimeType` variable that is used for association, it can fail to start correctly, not start at all or start without opening a file.

This may happen, for example, if the `Exec` variable is missing internal options needed for how to open a file, or how the application is shown in the menu. The `Exec` variable usually begins with `%`; for its currently supported options, see [exec-variables](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#exec-variables).

The following table lists the main variable entries of *.desktop* files that affect how an application starts, if it has a MIME-type associated with it.

| Variable names | Example 1 content | Example 2 content | Description |
| DBusActivatable | DBusActivatable=true | DBusActivatable=false | Application interact with [D-Bus](https://www.freedesktop.org/wiki/Software/dbus/).
See also configuration: [D-Bus](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#dbus). |
| MimeType | MimeType=application/vnd.oasis.opendocument.text | MimeType=application/vnd.sun.xml.math | List of MIME types supported by application |
| StartupWMClass | StartupWMClass=google-chrome | StartupWMClass=xpad | Associate windows with the owning application |
| Terminal | Terminal=true | Terminal=false | Start in default terminal |