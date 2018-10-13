Related articles

*   [X Logical Font Description](/index.php/X_Logical_Font_Description "X Logical Font Description")
*   [dotfiles](/index.php/Dotfiles "Dotfiles")

**Xresources** is a user-level configuration *dotfile*, typically located at `~/.Xresources`. It can be used to set [X resources](https://en.wikipedia.org/wiki/X_resources "wikipedia:X resources"), which are configuration parameters for X client applications.

Among other things they can be used to:

*   configure terminal preferences (e.g. terminal colors)
*   set DPI, anti-aliasing, hinting and other X font settings
*   change the Xcursor theme
*   theme [XScreenSaver](/index.php/XScreenSaver "XScreenSaver")
*   configure low-level X applications like: [xorg-xclock](https://www.archlinux.org/packages/?name=xorg-xclock), [xpdf](https://www.archlinux.org/packages/?name=xpdf), [rxvt-unicode](/index.php/Rxvt-unicode "Rxvt-unicode")

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Load resource file](#Load_resource_file)
    *   [2.2 xinitrc](#xinitrc)
    *   [2.3 Default settings](#Default_settings)
    *   [2.4 Xresources syntax](#Xresources_syntax)
        *   [2.4.1 Basic syntax](#Basic_syntax)
        *   [2.4.2 Wildcard matching](#Wildcard_matching)
        *   [2.4.3 Comments](#Comments)
        *   [2.4.4 Include files](#Include_files)
    *   [2.5 Getting resource values](#Getting_resource_values)
*   [3 Sample usage](#Sample_usage)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Parsing errors](#Parsing_errors)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [xorg-xrdb](https://www.archlinux.org/packages/?name=xorg-xrdb) package.

## Usage

### Load resource file

Resources are stored in the X server, so have to only be read once. They are also accessible to *remote* X11 clients (such as those [forwarded over SSH](/index.php/Secure_Shell#X11_forwarding "Secure Shell")).

Load a resource file (such as the conventional `.Xresources`), replacing any current settings:

```
$ xrdb *~/.Xresources*

```

Load a resource file, and merge with the current settings:

```
$ xrdb -merge *~/.Xresources*

```

**Note:**

*   Most [Display managers](/index.php/Display_manager "Display manager") load the `~/.Xresources` file on login.
*   The older `~/.Xdefaults` file is read when an X11 program starts, but only if *xrdb* has not been used in the current session. [[1]](https://groups.google.com/forum/#!msg/comp.windows.x/hQBEdql8l-Q/hF3DETcIHGwJ)

### xinitrc

If you are using a copy of the default [xinitrc](/index.php/Xinitrc "Xinitrc") as your `.xinitrc` it already merges `~/.Xresources`.

If you are using a custom `.xinitrc` add the following line:

```
[[ -f ~/.Xresources ]] && xrdb -merge -I$HOME ~/.Xresources

```

**Note:** Do not background the xrdb command within `~/.xinitrc`. Otherwise, programs launched after xrdb may look for resources before it has finished loading them.

### Default settings

To see the default settings for your installed X11 apps, look in `/usr/share/X11/app-defaults/`.

Detailed information on program-specific resources is usually provided in the man page for the program. xterm's man page is a good example, as it contains a list of X resources and their default values.

To see the currently loaded resources:

```
$ xrdb -query -all

```

### Xresources syntax

#### Basic syntax

The syntax of an Xresources file is as follows:

```
**name.Class.resource: value**

```

and here is a real world example:

```
xscreensaver.Dialog.headingFont: -*-fixed-bold-r-*-*-*-100-*-*-*-*-iso8859-1

```

	name

	The name of the application, such as xterm, xpdf, etc

	class

	The classification used to group resources together. Class names are typically uppercase.

	resource

	The name of the resource whose value is to be changed. Resources are typically lowercase with uppercase concatenation.

	value

	The actual value of the resource. This can be 1 of 3 types:

*   Integer (whole numbers)
*   Boolean (true/false, yes/no, on/off)
*   String (a string of characters) (for example a word (`white`), a color (`#ffffff`), or a path (`/usr/bin/firefox`))

	delimiters

	A dot (`**.**`) is used to signify each step down into the hierarchy — in the above example we start at name, then descend into Class, and finally into the resource itself. A colon (`**:**`) is used to separate the resource declaration from the actual value.

**Note:** For more information about Xresources file syntax see [XrmGetDatabase(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/XrmGetDatabase.3#FILE_SYNTAX).

#### Wildcard matching

Question mark (`?`) and asterisk (`*`) can be used as wildcards, making it easy to write a single rule that can be applied to many different applications or elements. `?` is used to match any single component name, while `*` is used to represent any number of intervening components including none.

Using the previous example, if you want to apply the same font to all programs (not just XScreenSaver) that contain the class name `Dialog` which contains the resource name `headingFont`, you could write:

```
**?**.Dialog.headingFont:     -*-fixed-bold-r-*-*-*-100-*-*-*-*-iso8859-1

```

If you want to apply this same rule to all programs that contain the resource `headingFont`, regardless of its class, you could write:

```
*****headingFont:    -*-fixed-bold-r-*-*-*-100-*-*-*-*-iso8859-1

```

For more information about wildcard matching rules see [XrmGetResource(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/XrmGetResource.3#MATCHING_RULES).

#### Comments

Lines starting with an exclamation mark (`!`) are ignored, for example:

```
! The following rule will be ignored because it has been commented out
!Xft.antialias: true

```

#### Include files

**Note:** You need to have a C preprocessor, such as `GNU CPP`, installed to use this functionality.

To use different files for each application, use `#include` in the main file. For example:

 `~/.Xresources` 
```
#include ".Xresources.d/xterm"
#include ".Xresources.d/rxvt-unicode"
#include ".Xresources.d/fonts"
#include ".Xresources.d/xscreensaver"

```

If files fail to load, specify the directory to *xrdb* with the `-I` parameter. For example:

 `~/.xinitrc` 
```
xrdb -I*$HOME* ~/.Xresources

```

### Getting resource values

If you want to get the value of a resource (for example if you want to use it in a bash script) you can use [xgetres](https://aur.archlinux.org/packages/xgetres/):

```
$ xgetres xscreensaver.Dialog.headingFont
-*-fixed-bold-r-*-*-*-100-*-*-*-*-iso8859-1

```

## Sample usage

The following samples should provide a good understanding of how application settings can be modified using an Xresources file. See [[2]](https://gist.github.com/anonymous/fa98de9fd70b51611303) for more examples. Refer to the man page of the application in question otherwise.

*   [Color output in console#Terminal emulators](/index.php/Color_output_in_console#Terminal_emulators "Color output in console")
*   [Cursor themes#X resources](/index.php/Cursor_themes#X_resources "Cursor themes")
*   [Font configuration#Applications without fontconfig support](/index.php/Font_configuration#Applications_without_fontconfig_support "Font configuration")
*   [Xterm#Configuration](/index.php/Xterm#Configuration "Xterm")
*   [rxvt-unicode#Configuration](/index.php/Rxvt-unicode#Configuration "Rxvt-unicode")
*   [xpdf(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xpdf.1#OPTIONS)

## Troubleshooting

### Parsing errors

[Display managers](/index.php/Display_manager "Display manager") such as [GDM](/index.php/GDM "GDM") may use the `--nocpp` argument for *xrdb*.

## See also

*   [Using the Xdefaults File](https://engineering.purdue.edu/ECN/Support/KB/Docs/UsingTheXdefaultsFil) - An in-depth article on how X interprets the Xdefaults file