[Alacritty](https://github.com/alacritty/alacritty) is a simple, GPU-accelerated terminal emulator written in [Rust](/index.php/Rust "Rust"). It supports scrollback, truecolor, copy/paste, clicking on URLS, and custom key bindings.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Colors](#Colors)
    *   [2.2 Font](#Font)
*   [3 Tips and Tricks](#Tips_and_Tricks)
    *   [3.1 Spawn new instance in same directory](#Spawn_new_instance_in_same_directory)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Mouse not working properly in Vim](#Mouse_not_working_properly_in_Vim)

## Installation

Install the [alacritty](https://www.archlinux.org/packages/?name=alacritty) package or [alacritty-git](https://aur.archlinux.org/packages/alacritty-git/) for the development version.

## Configuration

*Alacritty* searches for a configuration file at the following places in this order:

*   `$XDG_CONFIG_HOME/alacritty/alacritty.yml`
*   `$XDG_CONFIG_HOME/alacritty.yml`
*   `$HOME/.config/alacritty/alacritty.yml`
*   `$HOME/.alacritty.yml`

Copy the example configuration file at `/usr/share/doc/alacritty/example/alacritty.yml` to one of those places and uncomment the settings you want to change. Most settings take effect as soon as you save the file.

### Colors

See [[1]](https://github.com/alacritty/alacritty/wiki/Color-schemes) for a list of available color schemes. If your preferred color scheme is on the list, paste the provided code into your configuration file.

### Font

If you do not want to use your system’s default font, you can specify a different font by changing the following lines:

```
font:
  normal:
    family: monospace
    style: Regular

  bold:
    family: monospace
    style: Bold

  italic:
    family: monospace
    style: Italic

  bold_italic:
    family: monospace
    style: Bold Italic

```

Substitute `monospace` with a font name from the output of

```
$ fc-list : family style

```

Note that some fonts do not provide an `Italic` style but an `Oblique` style instead.

## Tips and Tricks

### Spawn new instance in same directory

Add the following lines to your configuration file to spawn a new instance of *Alacritty* in the current working directory by pressing `Ctrl+Shift+Enter`:

```
key_bindings:
  - { key: Return,   mods: Control|Shift, action: SpawnNewInstance }

```

## Troubleshooting

### Mouse not working properly in Vim

Add `ttymouse=sgr` to your `.vimrc` or switch to [Neovim](/index.php/Neovim "Neovim"). Also see [this issue](https://github.com/alacritty/alacritty/issues/803).