[Rofi](https://github.com/DaveDavenport/rofi) is a window switcher, run dialog, ssh-launcher and [dmenu](/index.php/Dmenu "Dmenu") replacement that started as a clone of [simpleswitcher](https://github.com/seanpringle/simpleswitcher), written by [Sean Pringle](https://github.com/seanpringle) and later expanded by [Dave Davenport](https://github.com/DaveDavenport).

## Contents

*   [1 Installation](#Installation)
*   [2 Custom Themes](#Custom_Themes)
    *   [2.1 Official Theme Generator](#Official_Theme_Generator)
    *   [2.2 Contributed Themes](#Contributed_Themes)
    *   [2.3 Rofi as a drop-in replacement for dmenu](#Rofi_as_a_drop-in_replacement_for_dmenu)
    *   [2.4 Rofi Theme](#Rofi_Theme)

## Installation

[Install](/index.php/Install "Install") [rofi](https://www.archlinux.org/packages/?name=rofi) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Custom Themes

### Official Theme Generator

See the [official theme generator](https://davedavenport.github.io/rofi/p11-Generator.html).

### Contributed Themes

See the official [rofi-themes](https://github.com/DaveDavenport/rofi-themes) repository for a list of custom themes.

### Rofi as a drop-in replacement for dmenu

For those users wanting to use [Rofi](https://github.com/DaveDavenport/rofi) as a drop-in replacement for [dmenu](/index.php/Dmenu "Dmenu"), you can use the following command:

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

**Tip:** You can add the `-dump-xresources` flag above, save the text output to a file and upload it to the [official theme generator](https://davedavenport.github.io/rofi/p11-Generator.html) to further customize the above theme.

**Note:** The command line options `-show run` and `-modi run` above will make [Rofi](https://github.com/DaveDavenport/rofi) act similar to `dmenu_run` which is provided by [dmenu](https://www.archlinux.org/packages/?name=dmenu), limiting the capabilities of Rofi. See `man rofi` and the [official project description](https://github.com/DaveDavenport/rofi) for more information on the additional modes available.

### Rofi Theme

Require xorg-xrdb installed. Choose one theme you like [Rofi Theme](https://davedavenport.github.io/rofi/p05-Themes.html) Copy code to ~/.Xresources Reload .Xresources file by xrdb -load ~/.Xresources or restart your computer it will works. If you don't understand, you can watch this video [Youtube](https://youtu.be/r4EYovtjLCk)