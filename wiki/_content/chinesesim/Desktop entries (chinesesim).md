Related articles

**翻译状态：** 本文是英文页面 [Desktop entries](/index.php/Desktop_entries "Desktop entries") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-10-29，点击[这里](https://wiki.archlinux.org/index.php?title=Desktop+entries&diff=0&oldid=587379)可以查看翻译后英文页面的改动。

[XDG 桌面配置项规范](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html)为应用程序和[桌面环境](/index.php/Desktop_environment "Desktop environment")的菜单整合提供了一个标准方法。只要桌面环境遵守[菜单规范](https://specifications.freedesktop.org/menu-spec/menu-spec-latest.html)，应用程序图标就可以显示在系统菜单中。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 分类](#分类)
*   [2 应用程序配置项](#应用程序配置项)
    *   [2.1 范例文件](#范例文件)
    *   [2.2 关键字定义](#关键字定义)
    *   [2.3 安装](#安装)
    *   [2.4 更新桌面文件数据库](#更新桌面文件数据库)
*   [3 图标](#图标)
    *   [3.1 通用图像格式](#通用图像格式)
    *   [3.2 图标格式转换](#图标格式转换)
    *   [3.3 Obtaining icons](#Obtaining_icons)
    *   [3.4 Icon path](#Icon_path)
*   [4 工具](#工具)
    *   [4.1 gendesk](#gendesk)
        *   [4.1.1 用法](#用法)
    *   [4.2 lsdesktopf](#lsdesktopf)
    *   [4.3 fbrokendesktop](#fbrokendesktop)
*   [5 提示与技巧](#提示与技巧)
    *   [5.1 从终端启动程序](#从终端启动程序)
    *   [5.2 隐藏窗口启动](#隐藏窗口启动)
    *   [5.3 修改环境变量](#修改环境变量)
*   [6 参阅](#参阅)

## 分类

桌面配置项大致分为三类：

	应用程序 

	文件后缀是 *.desktop*，包含程序启动方式，[XDG MIME Applications](/index.php/XDG_MIME_Applications "XDG MIME Applications") 使用的 `MimeType`等。将带 [XDG 自动启动程序](/index.php/XDG_Autostart "XDG Autostart")设置的文件放到特定位置，可以[自动启动](/index.php/Autostarting "Autostarting")应用程序。

	链接 

	文件后缀是 *.desktop*，定义指向某个 `URL` 的链接。

	目录 

	文件后缀是 *.directory*，定义应用程序菜单中的子菜单。

下列章节概述如何创建它们并使其生效。

## 应用程序配置项

应用程序配置项，即 `.desktop` 文件是元信息资源和应用程序快捷图标的集合。系统程序的配置项通常位于 `/usr/share/applications` 或 `/usr/local/share/applications`目录，单用户安装的程序位于 `~/.local/share/applications` 目录，桌面环境会优先使用用户的配置项。

### 范例文件

下面是一个示例结构和注释，这个示例文件没有使用所有的键值，[freedesktop.org 规范](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#recognized-keys)包含了完整的键值列表.

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

**Note:** 仅 `Type` 和 `Name` 是必须的。

### 关键字定义

全部有效的桌面配置项可参阅[freedesktop.org网站](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#recognized-keys)。 举例：`Type`关键字（类型）定义了三类桌面项：应用程序（Application (type 1)），链接（Link (type 2)）和目录（Directory (type 3)）。

*   `Version` （版本）关键字不是指应用程序的版本，而是本文件所遵循的**桌面配置项规范**的版本。

*   `Name`（名称）、`GenericName`（通称）和`Comment` 注释often contain redundant values in the form of combinations of them, like:

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

### 安装

用 [desktop-file-install(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/desktop-file-install.1) 将文件安装到目标目录:

```
desktop-file-install --dir=~/.local/share/applications ~/app.desktop

```

### 更新桌面文件数据库

要将 `~/.local/share/applications` 下的设置生效，执行下面命令:

```
$ update-desktop-database ~/.local/share/applications

```

## 图标

参考 [图标主题标准](https://specifications.freedesktop.org/icon-theme-spec/icon-theme-spec-latest.html).

### 通用图像格式

用于图标的图像文件格式简述如下：

<caption>Support for image formats for icons as specified by the freedesktop.org standard.</caption>
| Extension | Full Name and/or Description | Graphics Type | Container Format | Supported |
| .[png](https://en.wikipedia.org/wiki/Portable_Network_Graphics "wikipedia:Portable Network Graphics") | Portable Network Graphics | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | No | Yes |
| .[svg(z)](https://en.wikipedia.org/wiki/Scalable_Vector_Graphics "wikipedia:Scalable Vector Graphics") | Scalable Vector Graphics | [Vector](https://en.wikipedia.org/wiki/Vector_graphics "wikipedia:Vector graphics") | No | Yes (optional) |
| .[xpm](https://en.wikipedia.org/wiki/X_PixMap "wikipedia:X PixMap") | X PixMap | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | No | Yes (不推荐) |
| .[gif](https://en.wikipedia.org/wiki/Graphics_Interchange_Format "wikipedia:Graphics Interchange Format") | Graphics Interchange Format | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | No | No |
| .[ico](https://en.wikipedia.org/wiki/ICO_(icon_image_file_format) | MS Windows Icon Format | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | Yes | No |
| .[icns](https://en.wikipedia.org/wiki/Apple_Icon_Image "wikipedia:Apple Icon Image") | Apple Icon Image | [Raster](https://en.wikipedia.org/wiki/Raster_graphics "wikipedia:Raster graphics") | Yes | No |

### 图标格式转换

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

For extracting images from .icns container, you can use *icns2png* (provided by [libicns](https://www.archlinux.org/packages/?name=libicns)):

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

The [freedesktop.org standard](https://specifications.freedesktop.org/icon-theme-spec/icon-theme-spec-latest.html) specifies in which order and directories programs should look for icons:

1.  `$HOME/.icons` (for backwards compatibility)
2.  `$XDG_DATA_DIRS/icons`
3.  `/usr/share/pixmaps`

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

## 提示与技巧

### 从终端启动程序

安装软件包 [dex](https://www.archlinux.org/packages/?name=dex)，并运行 `dex */path/to/application.desktop*`.

### 隐藏窗口启动

首先，将桌面配置项复制到 `~/.local/share/applications`，避免修改被后续升级覆盖。

要在所有环境隐藏，在桌面配置项中加入 `NoDisplay=true`. 要在某个环境中隐藏，在桌面配置项中加入 `NotShowIn=*desktop-name*`

*desktop-name* 可以是 *GNOME*, *Xfce*, *KDE* 等，指定多个桌面时用分号隔开。

### 修改环境变量

在 `Exec` 命令中可以使用 `env` 修改环境变量:

 `~/.local/share/applications/abiword.desktop`  `Exec=env LANG=he_IL.UTF-8 abiword %U` 

## 参阅

*   [DeveloperWiki:Removal of desktop files](/index.php/DeveloperWiki:Removal_of_desktop_files "DeveloperWiki:Removal of desktop files")
*   [desktop wikipedia article](https://en.wikipedia.org/wiki/.desktop "wikipedia:.desktop")
*   [information for developers](http://freedesktop.org/wiki/Howto_desktop_files)