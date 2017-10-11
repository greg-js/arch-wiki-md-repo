Related articles

*   [List of applications/Other#Application launchers](/index.php/List_of_applications/Other#Application_launchers "List of applications/Other")

[Rofi](https://github.com/DaveDavenport/rofi) is a window switcher, run dialog, ssh-launcher and [dmenu](/index.php/Dmenu "Dmenu") replacement that started as a clone of [simpleswitcher](https://github.com/seanpringle/simpleswitcher), written by [Sean Pringle](https://github.com/seanpringle) and later expanded by [Dave Davenport](https://github.com/DaveDavenport).

## Contents

*   [1 Installation](#Installation)
*   [2 Rofi as dmenu replacement](#Rofi_as_dmenu_replacement)
*   [3 Custom Themes](#Custom_Themes)
    *   [3.1 Contributed Themes](#Contributed_Themes)

## Installation

[Install](/index.php/Install "Install") [rofi](https://www.archlinux.org/packages/?name=rofi) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Rofi as dmenu replacement

If called as dmenu (via a symlink), rofi acts like dmenu. You may want to install [rofi-dmenu](https://aur.archlinux.org/packages/rofi-dmenu/), which symlinks dmenu to rofi. Then programs that call dmenu from a script (like passmenu from [pass](/index.php/Pass "Pass")) will use rofi instead of dmenu.

If you prefer the look of dmenu, this approximates it:

```
rofi -show run -modi run -location 1 -width 100 \
		 -lines 2 -line-margin 0 -line-padding 1 \
		 -separator-style none -font "mono 10" -columns 9 -bw 0 \
		 -disable-history \
		 -hide-scrollbar \
		 -color-window "#222222, #222222, #b1b4b3" \
		 -color-normal "#222222, #b1b4b3, #222222, #005577, #b1b4b3" \
		 -color-active "#222222, #b1b4b3, #222222, #007763, #b1b4b3" \
		 -color-urgent "#222222, #b1b4b3, #222222, #77003d, #b1b4b3" \
		 -kb-row-select "Tab" -kb-row-tab ""

```

## Custom Themes

1.  Requires the [xorg-xrdb](https://www.archlinux.org/packages/?name=xorg-xrdb) package.
2.  Add your customisations to your [.Xresources file](/index.php/X_resources "X resources") (see below for examples).
3.  Reload .Xresources with `xrdb -load ~/.Xresources`.

### Contributed Themes

See the official [rofi-themes](https://github.com/DaveDavenport/rofi-themes) repository for a list of custom themes.