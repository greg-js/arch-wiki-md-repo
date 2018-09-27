The [XDG Desktop Entry specification](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html) defines a standard for applications to integrate into application menus of [desktop environments](/index.php/Desktop_environment "Desktop environment") implementing the [XDG Desktop Menu](https://specifications.freedesktop.org/menu-spec/menu-spec-latest.html) specification.

Each desktop entry must have a `Type` and a `Name` and can optionally define its appearance in the application menu.

The three available types are:

	Application

	Defines how to launch an application and what MIME types it supports (used by [XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications")). With [XDG Autostart](/index.php/XDG_Autostart "XDG Autostart") Application entries can be [started automatically](/index.php/Autostarting "Autostarting") by placing them in specific directories. Application entries use the `.desktop` file extension. See [#Application entry](#Application_entry).

	Link

	Defines a shortcut to a `URL`. Link entries use the `.desktop` file extension.

	Directory

	Defines the appearance of a submenu in the application menu. Link entries use the `.directory` file extension.

The following sections will roughly explain how these are created and validated.

## Contents

*   [1 Application entry](#Application_entry)
    *   [1.1 File example](#File_example)
    *   [1.2 Key definition](#Key_definition)
    *   [1.3 Validation](#Validation)
*   [2 Icons](#Icons)
    *   [2.1 Common image formats](#Common_image_formats)
    *   [2.2 Converting icons](#Converting_icons)
    *   [2.3 Obtaining icons](#Obtaining_icons)
    *   [2.4 Icon path](#Icon_path)
*   [3 Tools](#Tools)
    *   [3.1 gendesk](#gendesk)
        *   [3.1.1 How to use](#How_to_use)
    *   [3.2 lsdesktopf](#lsdesktopf)
    *   [3.3 fbrokendesktop](#fbrokendesktop)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Run a desktop file from a terminal](#Run_a_desktop_file_from_a_terminal)
    *   [4.2 Hide desktop entries](#Hide_desktop_entries)
    *   [4.3 Modify environment variables](#Modify_environment_variables)
*   [5 See also](#See_also)

## Application entry

Desktop entries for applications, or *.desktop* files, are generally a combination of meta information resources and a shortcut of an application. These files usually reside in `/usr/share/applications` or `/usr/local/share/applications` for applications installed system-wide, or `~/.local/share/applications` for user-specific applications. User entries take precedence over system entries.

### File example

Following is an example of its structure with additional comments. The example is only meant to give a quick impression, and does not show how to utilize all possible entry keys. The complete list of keys can be found in the [freedesktop.org specification](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#recognized-keys).

```
[Desktop Entry]

# The type as listed above
Type=Application

# The version of the desktop entry specification to which this file complies
Version=1.0

# The name of the application
Name=jMemorize

# A comment which can/will be used as a tooltip
Comment=Flash card based learning tool

# The path to the folder in which the executable is run
Path=/opt/jmemorise

# The executable of the application, possibly with arguments.
Exec=jmemorize

# The name of the icon that will be used to display this entry
Icon=jmemorize

# Describes whether this application needs to be run in a terminal or not
Terminal=false

# Describes the categories in which this entry should be shown
Categories=Education;Languages;Java;

```

### Key definition

All Desktop recognized desktop entries can be found on the [freedesktop.org](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#recognized-keys) site. For example, the `Type` key defines three types of desktop entries: Application (type 1), Link (type 2) and Directory (type 3).

*   `Version` key does not stand for the version of the application, but for the version of the desktop entry specification to which this file complies.

*   `Name`, `GenericName` and `Comment` often contain redundant values in the form of combinations of them, like:

```
Name=Pidgin Internet Messenger
GenericName=Internet Messenger

```

or

```
Name=NoteCase notes manager
Comment=Notes Manager

```

This should be avoided, as it will only be confusing to users. The `Name` key should only contain the name, or maybe an abbreviation/acronym if available.

*   `GenericName` should state what you would generally call an application that does what this specific application offers (i.e. Firefox is a "Web Browser").
*   `Comment` is intended to contain any usefull additional information.

### Validation

As some keys have become deprecated over time, you may want validate your desktop entries using [desktop-file-validate(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/desktop-file-validate.1) which is part of the [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils) package. To validate, run

```
$ desktop-file-validate <your desktop file>

```

This will give you very verbose and useful warnings and error messages.

## Icons

See also the [Icon Theme Specification](https://specifications.freedesktop.org/icon-theme-spec/icon-theme-spec-latest.html).

### Common image formats

Here is a short overview of image formats commonly used for icons.

<caption>Support for image formats for icons as specified by the freedesktop.org standard.</caption>
| Extension | Full Name and/or Description | Graphics Type | Container Format | Supported |
| .[png](https://en.wikipedia.org/wiki/Portable_Network_Graphics "wikipedia:Portable Network Graphics") | Portable Network Graphics | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | No | Yes |
| .[svg(z)](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics "wikipedia:Scalable Vector Graphics") | Scalable Vector Graphics | [Vector](https://en.wikipedia.org/wiki/Vector_graphics "wikipedia:Vector graphics") | No | Yes (optional) |
| .[xpm](https://en.wikipedia.org/wiki/X_PixMap "wikipedia:X PixMap") | X PixMap | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | No | Yes (deprecated) |
| .[gif](https://en.wikipedia.org/wiki/Graphics_Interchange_Format "wikipedia:Graphics Interchange Format") | Graphics Interchange Format | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | No | No |
| .[ico](https://en.wikipedia.org/wiki/ICO_(icon_image_file_format) | MS Windows Icon Format | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | Yes | No |
| .[icns](https://en.wikipedia.org/wiki/Apple_Icon_Image "wikipedia:Apple Icon Image") | Apple Icon Image | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | Yes | No |

### Converting icons

If you stumble across an icon which is in a format that is not supported by the freedesktop.org standard (like `gif` or `ico`), you can use the *convert* tool (which is part of the [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) package) to convert it to a supported/recommended format, e.g.:

```
$ convert <icon name>.gif <icon name>.png

```

If you convert from a container format like `ico`, you will get all images that were encapsulated in the `ico` file in the form `<icon name>-<number>.png`. If you want to know the size of the image, or the number of images in a container file like `ico` you can use the *identify* tool (also part of the [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) package):

 `$ identify /usr/share/vlc/vlc48x48.ico` 
```
/usr/share/vlc/vlc48x48.ico[0] ICO 32x32 32x32+0+0 8-bit DirectClass 84.3kb
/usr/share/vlc/vlc48x48.ico[1] ICO 16x16 16x16+0+0 8-bit DirectClass 84.3kb
/usr/share/vlc/vlc48x48.ico[2] ICO 128x128 128x128+0+0 8-bit DirectClass 84.3kb
/usr/share/vlc/vlc48x48.ico[3] ICO 48x48 48x48+0+0 8-bit DirectClass 84.3kb
/usr/share/vlc/vlc48x48.ico[4] ICO 32x32 32x32+0+0 8-bit DirectClass 84.3kb
/usr/share/vlc/vlc48x48.ico[5] ICO 16x16 16x16+0+0 8-bit DirectClass 84.3kb

```

As you can see, the example *ico* file, although its name might suggest a single image of size 48x48, contains no less than 6 different sizes, of which one is even greater than 48x48, namely 128x128.

Alternatively, you can use *icotool* (from [icoutils](https://www.archlinux.org/packages/?name=icoutils)) to extract png images from ico container:

```
$ icotool -x <icon name>.ico

```

For extracting images from .icns container, you can use *icns2png* (provided by [libicns](https://aur.archlinux.org/packages/libicns/)):

```
$ icns2png -x <icon name>.icns

```

### Obtaining icons

Although packages that already ship with a *.desktop* file most certainly contain an icon or a set of icons, there is sometimes the case when a developer has not created a *.desktop* file, but may ship icons, nonetheless. So a good start is to look for icons in the source package. You can i.e. first filter for the extension with **find** and then use **grep** to filter further for certain buzzwords like the package name, "icon", "logo", etc, if there are quite a lot of images in the source package.

```
$ find /path/to/source/package -regex ".*\.\(svg\|png\|xpm\|gif\|ico\)$"

```

If the developers of an application do not include icons in their source packages, the next step would be to search on their web sites. Some projects, like i.e. *tvbrowser* have an [artwork/logo page](http://enwiki.tvbrowser.org/index.php/Banners,_Logos_and_other_Promotion_Material) where additional icons may be found. If a project is multi-platform, there may be the case that even if the linux/unix package does not come with an icon, the Windows package might provide one. If the project uses a [Version control system](https://en.wikipedia.org/wiki/Version_control_system "wikipedia:Version control system") like CVS/SVN/etc. and you have some experience with it, you also might consider browsing it for icons. If everything fails, the project might simply have no icon/logo yet.

### Icon path

The [freedesktop.org standard](http://standards.freedesktop.org/icon-theme-spec/icon-theme-spec-latest.html) specifies in which order and directories programs should look for icons:

1.  `$HOME/.icons` (for backwards compatibility)
2.  `$XDG_DATA_DIRS/icons`
3.  `/usr/share/pixmaps`

## Tools

### gendesk

[gendesk](https://www.archlinux.org/packages/?name=gendesk) started as an Arch Linux-specific tool for generating .desktop files by fetching the needed information directly from PKGBUILD files. Now it is a general tool that takes command-line arguments.

Icons can be automatically downloaded from [openiconlibrary](http://openiconlibrary.sourceforge.net/), if available. (The source for icons can easily be changed in the future).

#### How to use

*   Add `gendesk` to makedepends

*   Start the `prepare()` function with:

 `gendesk --pkgname "$pkgname" --pkgdesc "$pkgdesc"` 

*   Alternatively, if an icon is already provided ($pkgname.png, for instance). The `-n` flag is for not downloading an icon or using the default icon. Example:

 `gendesk -n --pkgname "$pkgname" --pkgdesc "$pkgdesc"` 

*   `$srcdir/$pkgname.desktop` will be created and can be installed in the `package()` function with:

 `install -Dm644 "$pkgname.desktop" "$pkgdir/usr/share/applications/$pkgname.desktop"` 

*   The icon can be installed with:

 `install -Dm644 "$pkgname.png" "$pkgdir/usr/share/pixmaps/$pkgname.png"` 

*   Use `--name='Program Name'` for choosing a name for the menu entry.

*   Use `--exec='/opt/some_app/elf --some-arg --other-arg'` for setting the exec field.

*   See the [gendesk project](https://github.com/xyproto/gendesk) for more information.

### lsdesktopf

[lsdesktopf](https://aur.archlinux.org/packages/lsdesktopf/) can list available *.desktop* files or search their contents.

```
$ lsdesktopf
$ lsdesktopf --list
$ lsdesktopf --list gtk zh_TW,zh_CN,en_GB

```

It can also perform MIME-type-related searches. See [XDG MIME Applications#lsdesktopf](/index.php/XDG_MIME_Applications#lsdesktopf "XDG MIME Applications").

### fbrokendesktop

The [fbrokendesktop](https://aur.archlinux.org/packages/fbrokendesktop/) Bash script detects broken `Exec` values pointing to non-existent paths. Without any arguments it uses preset directories in the `DskPath` array. It shows only broken *.desktop* with full path and filename that is missing.

Examples

```
$ fbrokendesktop
$ fbrokendesktop /usr
$ fbrokendesktop /usr/share/apps/kdm/sessions/icewm.desktop

```

## Tips and tricks

### Run a desktop file from a terminal

Install the [dex](https://www.archlinux.org/packages/?name=dex) package and run `dex */path/to/application.desktop*`.

### Hide desktop entries

Firstly, copy the desktop entry file in question to `~/.local/share/applications` to avoid your changes being overwritten.

Then, to hide the entry in all environments, open the desktop entry file in a text editor and add the following line: `NoDisplay=true`.

To hide the entry in a specific desktop, add the following line to the desktop entry file: `NotShowIn=*desktop-name*`

where *desktop-name* can be option such as *GNOME*, *Xfce*, *KDE* etc. A desktop entry can be hidden in more than desktop at once - simply separate the desktop names with a semi-colon.

### Modify environment variables

Edit the `Exec` command by prepending `env`, for example:

 `~/.local/share/applications/abiword.desktop`  `Exec=env LANG=he_IL.UTF-8 abiword %U` 

## See also

*   [Wikipedia:.desktop](https://en.wikipedia.org/wiki/.desktop "wikipedia:.desktop")
*   [Information for developers](http://freedesktop.org/wiki/Howto_desktop_files)