Desktop entries is a [freedesktop.org](http://www.freedesktop.org/wiki/) standard for specifying the behaviour of programs running on [Xorg](/index.php/Xorg "Xorg"). It is a configuration file that describes how an application is launched and how it appears in a menu with an icon. The most common desktop entries are the `.desktop` and `.directory` files. This article explains briefly how to create useful and standard compliant desktop entries. It is mainly intended for package contributors and maintainers, but may also be useful for software developers and others.

There are roughly three types of desktop entries:

	Application 

	a shortcut to an application

	Link 

	a shortcut to a web link.

	Directory 

	a container of meta data of a menu entry

The following sections will roughly explain how these are created and validated.

## Contents

*   [1 Application entry](#Application_entry)
    *   [1.1 File example](#File_example)
    *   [1.2 Key definition](#Key_definition)
        *   [1.2.1 Deprecation](#Deprecation)
*   [2 Icons](#Icons)
    *   [2.1 Common image formats](#Common_image_formats)
    *   [2.2 Converting icons](#Converting_icons)
    *   [2.3 Obtaining icons](#Obtaining_icons)
*   [3 Tools](#Tools)
    *   [3.1 gendesk](#gendesk)
        *   [3.1.1 How to use](#How_to_use)
    *   [3.2 lsdsk](#lsdsk)
    *   [3.3 fbrokendesktop](#fbrokendesktop)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Hide desktop entries](#Hide_desktop_entries)
    *   [4.2 Autostart](#Autostart)
*   [5 See also](#See_also)

## Application entry

Desktop entries for applications, or `.desktop` files, are generally a combination of meta information resources and a shortcut of an application. These files usually reside in `/usr/share/applications` or `/usr/local/share/applications` for applications installed system-wide, or `~/.local/share/applications` for user-specific applications. User entries take precedence over system entries.

### File example

Following is an example of its structure with additional comments. The example is only meant to give a quick impression, and does not show how to utilize all possible entry keys. The complete list of keys can be found in the [freedesktop.org specification](http://standards.freedesktop.org/desktop-entry-spec/latest/ar01s05.html).

```
[Desktop Entry]
Type=Application                          # Indicates the type as listed above
Version=1.0                               # The version of the desktop entry specification to which this file complies
Name=jMemorize                            # The name of the application
Comment=Flash card based learning tool    # A comment which can/will be used as a tooltip
Path=/opt/jmemorise                       # The path to the folder in which the executable is run
Exec=jmemorize                            # The executable of the application.
Icon=jmemorize                            # The name of the icon that will be used to display this entry
Terminal=false                            # Describes whether this application needs to be run in a terminal or not
Categories=Education;Languages;Java;      # Describes the categories in which this entry should be shown

```

### Key definition

All Desktop recognized desktop entries can be found on the [freedesktop.org](http://standards.freedesktop.org/desktop-entry-spec/latest/ar01s05.html) site. For example, the `Type` key defines three types of desktop entries: Application (type 1), Link (type 2) and Directory (type 3).

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

#### Deprecation

There are quite some keys that have become deprecated over time as the standard has matured. The best/simplest way is to use the tool `desktop-file-validate` which is part of the package [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils). To validate, run

```
$ desktop-file-validate <your desktop file>

```

This will give you very verbose and useful warnings and error messages.

## Icons

### Common image formats

Here is a short overview of image formats commonly used for icons.

<caption>Support for image formats for icons as specified by the [freedesktop.org standard](http://standards.freedesktop.org/icon-theme-spec/latest/ar01s02.html).</caption>
| Extension | Full Name and/or Description | Graphics Type | Container Format | Supported |
| .[png](https://en.wikipedia.org/wiki/Portable_Network_Graphics "wikipedia:Portable Network Graphics") | Portable Network Graphics | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | no | yes |
| .[svg(z)](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics "wikipedia:Scalable Vector Graphics") | Scalable Vector Graphics | [Vector](https://en.wikipedia.org/wiki/Vector_graphics "wikipedia:Vector graphics") | no | yes (optional) |
| .[xpm](https://en.wikipedia.org/wiki/X_PixMap "wikipedia:X PixMap") | X PixMap | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | no | yes (deprecated) |
| .[gif](https://en.wikipedia.org/wiki/Graphics_Interchange_Format "wikipedia:Graphics Interchange Format") | Graphics Interchange Format | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | no | no |
| .[ico](https://en.wikipedia.org/wiki/ICO_(icon_image_file_format) | MS Windows Icon Format | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | yes | no |
| .[icns](https://en.wikipedia.org/wiki/Apple_Icon_Image "wikipedia:Apple Icon Image") | Apple Icon Image | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | yes | no |

### Converting icons

If you stumble across an icon which is in a format that is not supported by the freedesktop.org standard (like `gif` or `ico`), you can use the *convert* tool (which is part of the [imagemagick](https://www.archlinux.org/packages/?name=imagemagick)) to convert it to a supported/recommended format, e.g.:

```
$ convert <icon name>.gif <icon name>.png

```

If you convert from a container format like `ico`, you will get all images that were encapsulated in the `ico` file in the form `<icon name>-<number>.png`. If you want to know the size of the image, or the number of images in a container file like `ico` you can use the *identify* tool (also part of the [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) package)

```
$ identify /usr/share/vlc/vlc48x48.ico
/usr/share/vlc/vlc48x48.ico[0] ICO 32x32 32x32+0+0 8-bit DirectClass 84.3kb
/usr/share/vlc/vlc48x48.ico[1] ICO 16x16 16x16+0+0 8-bit DirectClass 84.3kb
/usr/share/vlc/vlc48x48.ico[2] ICO 128x128 128x128+0+0 8-bit DirectClass 84.3kb
/usr/share/vlc/vlc48x48.ico[3] ICO 48x48 48x48+0+0 8-bit DirectClass 84.3kb
/usr/share/vlc/vlc48x48.ico[4] ICO 32x32 32x32+0+0 8-bit DirectClass 84.3kb
/usr/share/vlc/vlc48x48.ico[5] ICO 16x16 16x16+0+0 8-bit DirectClass 84.3kb

```

As you can see, the example *ico* file, although its name might suggest a single image of size 48x48, contains no less than 6 different sizes, of which one is even greater than 48x48, namely 128x128\. And to give a bit of motivation on this subject, at the point of writing this section (2008-10-27), the 128x128 size was missing in the *vlc* package (0.9.4-2). So the next step would be to look at the vlc PKGBUILD and check whether this icon format was not in the source package to begin with (in that case we would inform the vlc developers), or whether this icon was somehow omitted from the Arch-specific package (in that case we can file a bug report at [the Arch Linux bug tracker](https://bugs.archlinux.org/)). (*Update:* this bug has now been [fixed](https://bugs.archlinux.org/task/11923), so as you can see, your work will not be in vain.)

### Obtaining icons

Although packages that already ship with a .desktop-file most certainly contain an icon or a set of icons, there is sometimes the case when a developer has not created a .desktop-file, but may ship icons, nonetheless. So a good start is to look for icons in the source package. You can i.e. first filter for the extension with **find** and then use **grep** to filter further for certain buzzwords like the package name, "icon", "logo", etc, if there are quite a lot of images in the source package.

```
$ find /path/to/source/package -regex ".*\.\(svg\|png\|xpm\|gif\|ico\)$"

```

If the developers of an application do not include icons in their source packages, the next step would be to search on their web sites. Some projects, like i.e. *tvbrowser* have an [artwork/logo page](http://enwiki.tvbrowser.org/index.php/Banners,_Logos_and_other_Promotion_Material) where additional icons may be found. If a project is multi-platform, there may be the case that even if the linux/unix package does not come with an icon, the Windows package might provide one. If the project uses a [Version control system](https://en.wikipedia.org/wiki/Version_control_system "wikipedia:Version control system") like CVS/SVN/etc. and you have some experience with it, you also might consider browsing it for icons. If everything fails, the project might simple have no icon/logo yet.

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

*   Use `--exec='/opt/some_app/elf --with-ponies'` for setting the exec field.

*   See the [gendesk project](https://github.com/xyproto/gendesk) for more information.

### lsdsk

The [lsdsk](https://aur.archlinux.org/packages/lsdsk/) bash script searching for content in "Categories" or "Exec", if "Categories" doesn't exist then it uses content of "Name". It's main purpose to get a quick overview in console of the available programs with their command lines and categories in *.desktop. It shows coloured existing base path defined in "DskPath" array.

Examples

```
# lsdsk
# lsdsk game
# lsdsk gtk

```

### fbrokendesktop

The [fbrokendesktop](https://aur.archlinux.org/packages/fbrokendesktop/) bash script using command "which" to detect broken Exec that points to not existing path. Without any parameters it uses preset folders in "DskPath" array. It shows only broken *.desktop with full path and filename that is missing.

Examples

```
# fbrokendesktop
# fbrokendesktop /usr
# fbrokendesktop /usr/share/apps/kdm/sessions/icewm.desktop

```

## Tips and tricks

### Hide desktop entries

**Tip:** Desktop entries can be hidden by creating a symbolic link to `/dev/null`. For example:
```
$ ln -s /dev/null ~/.local/share/applications/*foo*.desktop

```

Firstly, copy the desktop entry file in question to `~/.local/share/applications` to avoid your changes being overwritten.

Then, to hide the entry in all environments, open the desktop entry file in a text editor and add the following line: `NoDisplay=true`.

To hide the entry in a specific desktop, add the following line to the desktop entry file: `NotShowIn=*desktop-name*`

where *desktop-name* can be option such as *GNOME*, *Xfce*, *KDE* etc. A desktop entry can be hidden in more than desktop at once - simply separate the desktop names with a semi-colon.

### Autostart

If you use an XDG-compliant desktop environment, such as GNOME or KDE, the desktop environment will automatically start ***.desktop** files found in the following directories:

*   System-wide: `$XDG_CONFIG_DIRS/autostart/` (`/etc/xdg/autostart/` by default)

*   GNOME also starts files found in `/usr/share/gnome/autostart/`

*   User-specific: `$XDG_CONFIG_HOME/autostart/` (`~/.config/autostart/` by default)

Users can override system-wide `*.desktop` files by copying them into the user-specific `~/.config/autostart/` folder.

For an explanation of the desktop file standard refer to [Desktop Entry Specification](http://standards.freedesktop.org/desktop-entry-spec/latest/). For a more specific description of directories used, [Desktop Application Autostart Specification](http://standards.freedesktop.org/autostart-spec/autostart-spec-latest.html).

**Note:** This method is supported only by XDG-compliant desktop environments. Tools like [dapper](https://aur.archlinux.org/packages/dapper/), [dex](https://www.archlinux.org/packages/?name=dex), or [fbautostart](https://aur.archlinux.org/packages/fbautostart/) can be used to offer XDG autostart in unsupported desktop environments as long as some other autostart mechanism exists. Use the existing mechanism to start the xdg compliant autostart tool.

## See also

*   [DeveloperWiki:Removal of desktop files](/index.php/DeveloperWiki:Removal_of_desktop_files "DeveloperWiki:Removal of desktop files")
*   [desktop wikipedia article](https://en.wikipedia.org/wiki/.desktop "wikipedia:.desktop")
*   [recognized desktop entry keys](http://standards.freedesktop.org/desktop-entry-spec/latest/ar01s05.html)
*   [freedesktop.org desktop entry specification](http://freedesktop.org/wiki/Specifications/desktop-entry-spec)
*   [freedesktop.org icon theme specification](http://freedesktop.org/wiki/Specifications/icon-theme-spec)
*   [freedesktop.org menu specification](http://freedesktop.org/wiki/Specifications/menu-spec)
*   [freedesktop.org basedir specification](http://freedesktop.org/wiki/Specifications/basedir-spec)
*   [information for developers](http://freedesktop.org/wiki/Howto_desktop_files)