**翻译状态：** 本文是英文页面 [Desktop_entries](/index.php/Desktop_entries "Desktop entries") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-11-24，点击[这里](https://wiki.archlinux.org/index.php?title=Desktop_entries&diff=0&oldid=409972)可以查看翻译后英文页面的改动。

桌面配置项（Desktop entries）是 [freedesktop.org（自由桌面社区）](http://www.freedesktop.org/wiki/) 制订的一个用于规范 [Xorg](/index.php/Xorg "Xorg") 环境中程序运行行为的标准。它是一个配置文件，描述了某个应用程序如何被启动以及怎样在菜单中以图标形式出现。大部分桌面配置项是 `.desktop` 和 `.directory` 文件。本文将概述如何创建一个合规可用的桌面配置项，主要面向软件包发布者和维护者，但对软件开发者及其他人也会是有用的。

桌面配置项大致分为三类：

	应用程序 

	指向某个应用程序的快捷方式

	链接 

	指向某个网址的链接

	目录 

	某个菜单项元数据的容器

下列章节概述如何创建它们并使其生效。

## Contents

*   [1 应用程序配置项](#.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.E9.85.8D.E7.BD.AE.E9.A1.B9)
    *   [1.1 范例文件](#.E8.8C.83.E4.BE.8B.E6.96.87.E4.BB.B6)
    *   [1.2 关键字定义](#.E5.85.B3.E9.94.AE.E5.AD.97.E5.AE.9A.E4.B9.89)
        *   [1.2.1 过时的内容](#.E8.BF.87.E6.97.B6.E7.9A.84.E5.86.85.E5.AE.B9)
*   [2 图标](#.E5.9B.BE.E6.A0.87)
    *   [2.1 通用图像格式](#.E9.80.9A.E7.94.A8.E5.9B.BE.E5.83.8F.E6.A0.BC.E5.BC.8F)
    *   [2.2 图标格式转换](#.E5.9B.BE.E6.A0.87.E6.A0.BC.E5.BC.8F.E8.BD.AC.E6.8D.A2)
    *   [2.3 Obtaining icons](#Obtaining_icons)
*   [3 工具](#.E5.B7.A5.E5.85.B7)
    *   [3.1 gendesk](#gendesk)
        *   [3.1.1 用法](#.E7.94.A8.E6.B3.95)
    *   [3.2 在*.desktop文件目錄或搜索](#.E5.9C.A8.2A.desktop.E6.96.87.E4.BB.B6.E7.9B.AE.E9.8C.84.E6.88.96.E6.90.9C.E7.B4.A2)
    *   [3.3 fbrokendesktop](#fbrokendesktop)
*   [4 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [4.1 隐藏桌面配置项](#.E9.9A.90.E8.97.8F.E6.A1.8C.E9.9D.A2.E9.85.8D.E7.BD.AE.E9.A1.B9)
    *   [4.2 自动启动](#.E8.87.AA.E5.8A.A8.E5.90.AF.E5.8A.A8)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 应用程序配置项

Desktop entries for applications, or `.desktop` files, are generally a combination of meta information resources and a shortcut of an application. These files usually reside in `/usr/share/applications` or `/usr/local/share/applications` for applications installed system-wide, or `~/.local/share/applications` for user-specific applications. User entries take precedence over system entries.

### 范例文件

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

### 关键字定义

All Desktop recognized desktop entries can be found [on the freedesktop.org site](http://standards.freedesktop.org/desktop-entry-spec/latest/ar01s05.html). For example, the `Type` key defines three types of desktop entries: Application (type 1), Link (type 2) and Directory (type 3).

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

#### 过时的内容

There are quite some keys that have become deprecated over time as the standard has matured. The best/simplest way is to use the tool `desktop-file-validate` which is part of the package [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils). To validate, run

```
$ desktop-file-validate <your desktop file>

```

This will give you very verbose and useful warnings and error messages.

## 图标

### 通用图像格式

Here is a short overview of image formats commonly used for icons.

<caption>Support for image formats for icons as specified by the [freedesktop.org standard](http://standards.freedesktop.org/icon-theme-spec/latest/ar01s02.html).</caption>
| Extension | Full Name and/or Description | Graphics Type | Container Format | Supported |
| .[png](https://en.wikipedia.org/wiki/Portable_Network_Graphics "wikipedia:Portable Network Graphics") | Portable Network Graphics | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | no | yes |
| .[svg(z)](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics "wikipedia:Scalable Vector Graphics") | Scalable Vector Graphics | [Vector](https://en.wikipedia.org/wiki/Vector_graphics "wikipedia:Vector graphics") | no | yes (optional) |
| .[xpm](https://en.wikipedia.org/wiki/X_PixMap "wikipedia:X PixMap") | X PixMap | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | no | yes (deprecated) |
| .[gif](https://en.wikipedia.org/wiki/Graphics_Interchange_Format "wikipedia:Graphics Interchange Format") | Graphics Interchange Format | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | no | no |
| .[ico](https://en.wikipedia.org/wiki/ICO_(icon_image_file_format) | MS Windows Icon Format | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | yes | no |
| .[icns](https://en.wikipedia.org/wiki/Apple_Icon_Image "wikipedia:Apple Icon Image") | Apple Icon Image | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | yes | no |

### 图标格式转换

If you stumble across an icon which is in a format that is not supported by the freedesktop.org standard (like *gif* or *ico*), you can **convert** (which is part of the **imagemagick** package) it to a supported/recommended format, e.g.:

```
$ convert <icon name>.gif <icon name>.png

```

If you convert from a container format like *ico*, you will get all images that were encapsulated in the *ico* file in the form *<icon name>-<number>.png*. If you want to know the size of the image, or the number of images in a container file like *ico* you can use **identify** (also part of the **imagemagick** package)

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

## 工具

### gendesk

[gendesk](https://www.archlinux.org/packages/?name=gendesk) started as an Arch Linux-specific tool for generating .desktop files by fetching the needed information directly from PKGBUILD files. Now it is a general tool that takes command-line arguments.

Icons can be automatically downloaded from [openiconlibrary](http://openiconlibrary.sourceforge.net/), if available. (The source for icons can easily be changed in the future).

#### 用法

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

### 在*.desktop文件目錄或搜索

該[lsdesktopf](https://aur.archlinux.org/packages/lsdesktopf/)腳本列出可用*.desktop文件或在自己的搜索內容。它的主要目的是讓在可用程序控制台的簡要概述他們的命令行，並在`*.desktop`文件設置的類別。

例子

```
# lsdesktopf
# lsdesktopf game
# lsdesktopf gtk

```

完全相同的功能之上，但垂直文本輸出可讀性，包括相關的變量名：

```
# lsdesktopf --more
# lsdesktopf --more game

```

欲了解更多的選擇使用 `lsdesktopf --help`.

### fbrokendesktop

The [fbrokendesktop](https://aur.archlinux.org/packages/fbrokendesktop/) bash script using command "which" to detect broken Exec that points to not existing path. Without any parameters it uses preset folders in "DskPath" array. It shows only broken *.desktop with full path and filename that is missing.

Examples

```
# fbrokendesktop
# fbrokendesktop /usr
# fbrokendesktop /usr/share/apps/kdm/sessions/icewm.desktop

```

## 提示与技巧

### 隐藏桌面配置项

**Tip:** Desktop entries can be hidden by creating a symbolic link to `/dev/null`. For example:
```
$ ln -s /dev/null ~/.local/share/applications/*foo*.desktop

```

Firstly, copy the desktop entry file in question to `~/.local/share/applications` to avoid your changes being overwritten.

Then, to hide the entry in all environments, open the desktop entry file in a text editor and add the following line: `NoDisplay=true`.

To hide the entry in a specific desktop, add the following line to the desktop entry file: `NotShowIn=*desktop-name*`

where *desktop-name* can be option such as *GNOME*, *Xfce*, *KDE* etc. A desktop entry can be hidden in more than desktop at once - simply separate the desktop names with a semi-colon.

### 自动启动

If you use an XDG-compliant desktop environment, such as GNOME or KDE, the desktop environment will automatically start [*.desktop](/index.php/Desktop_entries "Desktop entries") files found in the following directories:

*   System-wide: `$XDG_CONFIG_DIRS/autostart/` (`/etc/xdg/autostart/` by default)

*   GNOME also starts files found in `/usr/share/gnome/autostart/`

*   User-specific: `$XDG_CONFIG_HOME/autostart/` (`~/.config/autostart/` by default)

Users can override system-wide `*.desktop` files by copying them into the user-specific `~/.config/autostart/` folder.

For an explanation of the desktop file standard refer to [Desktop Entry Specification](http://standards.freedesktop.org/desktop-entry-spec/latest/). For a more specific description of directories used, [Desktop Application Autostart Specification](http://standards.freedesktop.org/autostart-spec/autostart-spec-latest.html).

**Note:** This method is supported only by XDG-compliant desktop environments. Tools like [dapper](https://aur.archlinux.org/packages/dapper/), [dex](https://www.archlinux.org/packages/?name=dex), or [fbautostart](https://aur.archlinux.org/packages/fbautostart/) can be used to offer XDG autostart in unsupported desktop environments as long as some other autostart mechanism exists. Use the existing mechanism to start the xdg compliant autostart tool.

## 参阅

*   [DeveloperWiki:Removal of desktop files](/index.php/DeveloperWiki:Removal_of_desktop_files "DeveloperWiki:Removal of desktop files")
*   [desktop wikipedia article](https://en.wikipedia.org/wiki/.desktop "wikipedia:.desktop")
*   [recognized desktop entry keys](http://standards.freedesktop.org/desktop-entry-spec/latest/ar01s05.html)
*   [freedesktop.org desktop entry specification](http://freedesktop.org/wiki/Specifications/desktop-entry-spec)
*   [freedesktop.org icon theme specification](http://freedesktop.org/wiki/Specifications/icon-theme-spec)
*   [freedesktop.org menu specification](http://freedesktop.org/wiki/Specifications/menu-spec)
*   [freedesktop.org basedir specification](http://freedesktop.org/wiki/Specifications/basedir-spec)
*   [information for developers](http://freedesktop.org/wiki/Howto_desktop_files)