# dmenu

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [List of applications/Other#Application launchers](/index.php/List_of_applications/Other#Application_launchers "List of applications/Other")

[dmenu](http://tools.suckless.org/dmenu) is a fast and lightweight dynamic menu for X. It reads arbitrary text from stdin, and creates a menu with one item for each line. The user can then select an item, through the arrow keys or typing a part of the name, and the line is printed to stdout. dmenu_run is a wrapper that ships with the dmenu distribution that allows its use as an application launcher.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Displaying Custom Items](#Displaying_Custom_Items)
    *   [2.2 Manually Adding Items](#Manually_Adding_Items)
    *   [2.3 Fonts](#Fonts)
    *   [2.4 Support for shell aliases](#Support_for_shell_aliases)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 No locale support](#No_locale_support)
    *   [3.2 Missing menu entries](#Missing_menu_entries)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [dmenu](https://www.archlinux.org/packages/?name=dmenu) package from the [official repositories](/index.php/Official_repositories "Official repositories"). If you want the development build from git, install the [dmenu-git](https://aur.archlinux.org/packages/dmenu-git/)<sup><small>AUR</small></sup> package from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

Various patched variants exist which extend dmenu's default functionality. Consider installing one of the following packages from the [AUR](/index.php/AUR "AUR"):

*   [dmenu-xft](https://aur.archlinux.org/packages/dmenu-xft/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/dmenu-xft)]</sup>: XFT font support
*   [dmenu-xft-height](https://aur.archlinux.org/packages/dmenu-xft-height/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/dmenu-xft-height)]</sup>: XFT font support and custom height support
*   [dmenu-xft-transparency](https://aur.archlinux.org/packages/dmenu-xft-transparency/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/dmenu-xft-transparency)]</sup>: XFT font support and transparency
*   [dmenu-xft-mouse-height](https://aur.archlinux.org/packages/dmenu-xft-mouse-height/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/dmenu-xft-mouse-height)]</sup>: XFT font support, custom height, and mouse support
*   [dmenu2](https://aur.archlinux.org/packages/dmenu2/)<sup><small>AUR</small></sup>: dmenu fork with many useful patches applied and additional capabilities added including dimming, specifying a custom opacity, and underlining.

You may run _dmenu_ with:

```
$ dmenu_run

```

## Configuration

Now, you will want to attach the `dmenu_run` command to a keystroke combination. This can be done either via your window manager or desktop environment configuration, or with a program like [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys). See the [Hotkeys](/index.php/Hotkeys "Hotkeys") article for more information. Also, it is helpful to [Prelink](/index.php/Prelink "Prelink") _dmenu_.

### Displaying Custom Items

Custom items may be shown by piping them into _dmenu_. For example:

```
$ echo -e "first\nsecond\nthird" | dmenu

```

### Manually Adding Items

_dmenu_ will look for executables in the directories defined in your `$PATH`. See the following article for information on modifying your `$PATH`: [Environment variables](/index.php/Environment_variables "Environment variables")

### Fonts

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** Since dmenu 4.6 XFT font rendering is enabled by default: [4.6 Release Notes](http://lists.suckless.org/dev/1511/27503.html). Specifying fonts via [X logical font description](https://en.wikipedia.org/wiki/XLFD "wikipedia:XLFD") does not work anymore. Instead [fontconfig](https://www.archlinux.org/packages/?name=fontconfig)'s [font.conf syntax](http://www.freedesktop.org/software/fontconfig/fontconfig-user.html) is used. (Discuss in [Talk:Dmenu#](https://wiki.archlinux.org/index.php/Talk:Dmenu))

_dmenu_ can display fonts using the [X logical font description](https://en.wikipedia.org/wiki/XLFD "wikipedia:XLFD") as found using the tool _xfontsel_, which is provided by [xorg-xfontsel](https://www.archlinux.org/packages/?name=xorg-xfontsel). This example will run dmenu using the [terminus-font](https://www.archlinux.org/packages/?name=terminus-font):

```
$ dmenu_run -fn "-xos4-terminus-medium-r-*-*-14-*"

```

The syntax is similar if using a _dmenu_ variant patched with XFT support.

```
$ dmenu_run -fn 'Droid Sans Mono-9'

```

### Support for shell aliases

_dmenu_ does not support [shell aliases](/index.php/Bash#Aliases "Bash"). To have _dmenu_ recognize your aliases, [install](/index.php/Install "Install") the [dmenu-recent-aliases](https://aur.archlinux.org/packages/dmenu-recent-aliases/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/dmenu-recent-aliases)]</sup> package from the [AUR](/index.php/AUR "AUR") and run `dmenu_run_aliases`. Your aliases must be in either `~/.bash_aliases` or `~/.zsh_aliases` to be recognized by _dmenu_run_aliases_.

## Troubleshooting

### No locale support

Running _dmenu_run_ results in the following error message:

 `$ dmenu_run` 

```
no locale support

```

Make sure that the environment variable `LANG` is correctly set. See the following for more information: [Locale#Troubleshooting](/index.php/Locale#Troubleshooting "Locale")

### Missing menu entries

If certain entries are missing from _dmenu_, the cache may be malformed. Delete it and restart _dmenu_.

```
$ rm ~/.dmenu_cache
$ rm ~/.cache/dmenu_run

```

Note that there will most likely be only one cache file, depending on if `$XDG_CACHE_HOME` is set. See the contents of `/usr/bin/dmenu_run` for more information.

## See also

*   [dmenu](http://tools.suckless.org/dmenu) – The official dmenu website
*   [Dmenu Hacking thread](https://bbs.archlinux.org/viewtopic.php?id=80145) – Dmenu hacking thread in arch linux forums. An overview of scripts is provided in the [dmenu_scripts collection](https://github.com/orschiro/dmenu-scripts-collection).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dmenu&oldid=412065](https://wiki.archlinux.org/index.php?title=Dmenu&oldid=412065)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Application launchers](/index.php/Category:Application_launchers "Category:Application launchers")

Hidden categories:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")
*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")