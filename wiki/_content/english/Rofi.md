Related articles

*   [List of applications/Other#Application launchers](/index.php/List_of_applications/Other#Application_launchers "List of applications/Other")

[Rofi](https://github.com/DaveDavenport/rofi) is a window switcher, run dialog, ssh-launcher and [dmenu](/index.php/Dmenu "Dmenu") replacement that started as a clone of [simpleswitcher](https://github.com/seanpringle/simpleswitcher), written by [Sean Pringle](https://github.com/seanpringle) and later expanded by [Dave Davenport](https://github.com/DaveDavenport).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Rofi as dmenu replacement](#Rofi_as_dmenu_replacement)
*   [4 Execute shell commands from rofi](#Execute_shell_commands_from_rofi)
*   [5 Custom Themes](#Custom_Themes)
    *   [5.1 Contributed Themes](#Contributed_Themes)

## Installation

[Install](/index.php/Install "Install") the [rofi](https://www.archlinux.org/packages/?name=rofi) package.

## Configuration

There are currently three methods of setting configuration options:

*   Local configuration. Normally, depending on XDG, in `~/.config/rofi/config`. This uses the Xresources format.
*   Xresources: A method of storing key values in the Xserver.
*   Command line options

So

```
rofi -combi-modi window,drun,ssh -theme solarized -font "hack 10" -show combi

```

can be expressed in a config file like this:

```
rofi.combi-modi:    window,drun,ssh
rofi.theme:         solarized
rofi.font:          hack 10
rofi.modi:          combi

```

To get a full list of options you can put in Xresources or in your config file run `rofi -dump-Xresources`

**Note:** i3 users be aware that putting commas in i3 config can cause issues. To bind a key to launch rofi, either use a config file or replace the commas with `#` eg `rofi -combi-modi window#drun#ssh`

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

## Execute shell commands from rofi

If you want the ability to run shell commands or use your own scripts directly from rofi with seeing the output, then ensure following:

*   configure the PATH variable in `~/.profile` (instead of e.g. `~/.bashrc`) and then logout and re-login to your window manager/desktop environment
*   define `-run-shell-command '{terminal} -e \\"{cmd}; read -n 1 -s"'`. This allows you to enter the command on the inputbar followed by SHIFT+ENTER. The terminal stays open until the next keypress.

This is an example with the recommended escaping sequence for i3:

```
 bindsym $mod+d exec --no-startup-id "rofi -show drun -font \\"DejaVu 9\\" -run-shell-command '{terminal} -e \\" {cmd}; read -n 1 -s\\"'"

```

## Custom Themes

You can preview and apply themes for rofi with

```
 rofi-theme-selector

```

Customizations may be saved to your [.Xresources file](/index.php/X_resources "X resources") (requires the [xorg-xrdb](https://www.archlinux.org/packages/?name=xorg-xrdb) package). To apply changes reload .Xresources with `xrdb -load ~/.Xresources`.

### Contributed Themes

See the official [rofi-themes](https://github.com/DaveDavenport/rofi-themes) repository for a list of custom themes.

Download one of the .rasi themes and place it in `~/.config/rofi/example.rasi`. Then load up the theme on the command line or in a config file:

```
 rofi <options> -theme example

```

or in your configuration file

```
 rofi.theme:    example

```