Related articles

*   [List of applications/Other#Application launchers](/index.php/List_of_applications/Other#Application_launchers "List of applications/Other")

[dmenu](https://tools.suckless.org/dmenu) is a fast and lightweight dynamic menu for X. It reads arbitrary text from stdin, and creates a menu with one item for each line. The user can then select an item, through the arrow keys or typing a part of the name, and the line is printed to stdout. *dmenu_run* is a wrapper that ships with the dmenu distribution that allows its use as an application launcher.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Displaying Custom Items](#Displaying_Custom_Items)
    *   [2.2 Manually Adding Items](#Manually_Adding_Items)
    *   [2.3 Fonts](#Fonts)
    *   [2.4 Support for shell aliases](#Support_for_shell_aliases)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 No locale support](#No_locale_support)
    *   [3.2 Missing menu entries](#Missing_menu_entries)
    *   [3.3 Environment Variables](#Environment_Variables)
    *   [3.4 Current window loses focus](#Current_window_loses_focus)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [dmenu](https://www.archlinux.org/packages/?name=dmenu) package, or [dmenu-git](https://aur.archlinux.org/packages/dmenu-git/) for the development version.

Various patched variants exist which extend dmenu's default functionality. Consider installing one of the following packages from the [AUR](/index.php/AUR "AUR"):

*   [dmenu2](https://aur.archlinux.org/packages/dmenu2/): dmenu fork with many useful patches applied and additional capabilities added including dimming, specifying a custom opacity, and underlining.

You may run *dmenu* with:

```
$ dmenu_run

```

## Configuration

Now, you will want to attach the `dmenu_run` command to a keystroke combination. This can be done either via your window manager or desktop environment configuration, or with a program like [xbindkeys](https://www.archlinux.org/packages/?name=xbindkeys). See the [Hotkeys](/index.php/Hotkeys "Hotkeys") article for more information.

### Displaying Custom Items

Custom items will be shown by separating them with a new line (*
*) and piping them into *dmenu*. For example:

```
$ echo -e "first
second
third" | dmenu

```

### Manually Adding Items

*dmenu* will look for executables in the directories defined in your `$PATH`. For information on modifying your `$PATH` see [environment variables](/index.php/Environment_variables "Environment variables").

### Fonts

*dmenu* can display fonts using the [X logical font description](https://en.wikipedia.org/wiki/XLFD "wikipedia:XLFD") as found using the tool *xfontsel*, which is provided by [xorg-xfontsel](https://www.archlinux.org/packages/?name=xorg-xfontsel). This example will run dmenu using the [terminus-font](https://www.archlinux.org/packages/?name=terminus-font):

```
$ dmenu_run -fn "-xos4-terminus-medium-r-*-*-14-*"

```

The syntax is similar if using a *dmenu* variant patched with XFT support.

```
$ dmenu_run -fn 'Droid Sans Mono-9'

```

### Support for shell aliases

*dmenu* does not support [shell aliases](/index.php/Bash#Aliases "Bash"). To have *dmenu* recognize your aliases, [install](/index.php/Install "Install") the [dmenu-recent-aliases](https://aur.archlinux.org/packages/dmenu-recent-aliases/) package from the [AUR](/index.php/AUR "AUR") and run `dmenu_run_aliases`. Your aliases must be in either `~/.bash_aliases` or `~/.zsh_aliases` to be recognized by *dmenu_run_aliases*.

## Troubleshooting

### No locale support

Running *dmenu_run* results in the following error message:

 `$ dmenu_run` 
```
no locale support

```

Make sure that the environment variable `LANG` is correctly set. See the following for more information: [Locale#Troubleshooting](/index.php/Locale#Troubleshooting "Locale")

### Missing menu entries

If certain entries are missing from *dmenu*, the cache may be malformed. Delete it and restart *dmenu*.

```
$ rm ~/.dmenu_cache
$ rm ~/.cache/dmenu_run

```

Note that there will most likely be only one cache file, depending on if `$XDG_CACHE_HOME` is set. See the contents of `/usr/bin/dmenu_run` for more information.

### Environment Variables

Environment variables needed for applications should instead be added to `/etc/environment`.

### Current window loses focus

A [bug](https://git.suckless.org/dmenu/commit/db6093f6ec1bb884f7540f2512935b5254750b30.html) in dmenu 4.9 causes the current window to lose focus when dmenu is opened and to not regain focus when it is closed. It can also happen that a newly launched program is does not gain focus. You can fix this by downgrading to dmenu 4.8\. See [this](https://github.com/i3/i3/issues/3528) ticket for a discussion.

## See also

*   [dmenu](https://tools.suckless.org/dmenu) – The official dmenu website
*   [Dmenu Hacking thread](https://bbs.archlinux.org/viewtopic.php?id=80145) – Dmenu hacking thread in Arch Linux forum. An overview of scripts is provided in the [dmenu_scripts collection](https://github.com/orschiro/dmenu-scripts-collection).