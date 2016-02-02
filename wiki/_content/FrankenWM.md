# FrankenWM

FrankenWM is a dynamic tiling [window manager](/index.php/Window_manager "Window manager"), comparable to dwm or awesome. This means there are a number of predefined layouts that are used to tile the windows. The source code is based on monsterwm-xcb, but includes a lot of bugfixes and additonal features like extensive runtime configuration, a scratchpad window, window minimizing, floating control via keyboard and currently 13 different tiling layouts.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 AUR](#AUR)
    *   [1.2 Git](#Git)
    *   [1.3 Launching FrankenWM](#Launching_FrankenWM)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
*   [4 Panels](#Panels)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 I do not see anything](#I_do_not_see_anything)
    *   [5.2 I cannot open a terminal/menu](#I_cannot_open_a_terminal.2Fmenu)

## Installation

You can get FrankenWM by [installing](/index.php/Installing "Installing") the [frankenwm-git](https://aur.archlinux.org/packages/frankenwm-git/) package or directly from [Github](https://github.com/sulami/FrankenWM). Any Configuration has to be done at compile time, so you might want to have a look at the section below.

### AUR

When using the AUR-version, you can supply you own `config.h` which whill be used instead of the default config.

### Git

**Note:** Compiling manually requires you to get the dependencies needed yourself, which are `libxcb xcb-util xcb-util-wm xcb-util-keysyms` (as well as `make` and `gcc`).

When using the Git-version, you will need to copy `config.def.h` to `config.h` and make the modifications you need before compiling FrankenWM. Then you can run `make` and `sudo make install` to install the binaries and manpage.

### Launching FrankenWM

FrankenWM is usually started using the `.xinitrc`, either manually via `startx` or automatically using a display manager like `slim` or `lightdm`.

## Configuration

Configuration is done at compile time by edititing `config.h`. There are lots of comments in the default config (`config.def.h`) which explain what the settings are doing.

## Usage

The basic usage includes opening a terminal (`Meta+Enter`), opening dmenu (`Meta+r`) and closing windows (`Meta+c`). There is a complete, sorted list of the default keybinds and explanations of the tiling layouts in the manpage, which you can view with `man ./frankenwm.1` before install, or `man frankenwm` after install.

## Panels

FrankenWM does not come with a panel included, but gives you the possibility to leave space either at the top or bottom for one, like `conky` or `dzen`. There are a couple of settings in the config to configure this space.

If you want to use FrankenWM's status in your bar, you can pipe FrankenWM to a shell script to parse the output and pipe it to a bar. Sample scripts to accomplish this with a few different bar are located [here](https://gist.github.com/sulami/d6a53179d6d7479e0709).

## Troubleshooting

### I do not see anything

This is normal behaviour, as FrankenWM does not come with a bar included or a desktop background, so after running `frankenwm` without anything else, you will probably see a black screen. See Panels above for information on how to add a panel to your desktop. Wallpapers can be set by using software like xsetroot, feh or hsetroot.

### I cannot open a terminal/menu

Have a look at the `config.h` used to build your currently running version of FrankenWM, which is located in the build directory. Make sure that both the shortcut to run the `termcmd`/`menucmd` command and the `termcmd`/`menucmd` itself are set properly to start an installed terminal/menu.

Retrieved from "[https://wiki.archlinux.org/index.php?title=FrankenWM&oldid=389395](https://wiki.archlinux.org/index.php?title=FrankenWM&oldid=389395)"