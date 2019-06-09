[Neovim](https://neovim.io/) is a fork of [Vim](/index.php/Vim "Vim") aiming to improve user experience, plugins, and GUIs.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Migrating from Vim](#Migrating_from_Vim)
    *   [2.2 Shared Configuration between Vim and Nvim](#Shared_Configuration_between_Vim_and_Nvim)
        *   [2.2.1 Loading vim addons](#Loading_vim_addons)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Replacing vi and vim with neovim](#Replacing_vi_and_vim_with_neovim)
    *   [3.2 Symlinking init.vim to .vimrc](#Symlinking_init.vim_to_.vimrc)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Cursor is not restored to previous state after exit](#Cursor_is_not_restored_to_previous_state_after_exit)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [neovim](https://www.archlinux.org/packages/?name=neovim) package.

**Note:** With neovim, some of its features are delegated to external "providers". For Python providers, use [python-pynvim](https://aur.archlinux.org/packages/python-pynvim/).

## Configuration

Nvim's user-specific configuration file is located at `$XDG_CONFIG_HOME/nvim/init.vim`, by default `~/.config/nvim/init.vim`. The global configuration file is loaded from `$XDG_CONFIG_DIRS/nvim/sysinit.vim` (by default `/etc/xdg/nvim/sysinit.vim`) if it exists, or if it does not, from `/usr/share/nvim/sysinit.vim` which should not be user-edited. [[1]](https://github.com/neovim/neovim/blob/master/runtime/doc/starting.txt#L437) By default, the former global configuration file does not exist. If you create the former file, you may wish to have it source the latter if you still want the functionality it provides, which is allowing pacman-installed vim packages to work with Nvim.

Nvim is compatible with most of Vim's options, however there are options specific to Nvim. For a complete list of Nvim options, see Neovim's [help file](https://neovim.io/doc/user/options.html).

Nvim's data directory is located in `~/.local/share/nvim/` and contains swap for open files, the [ShaDa](https://neovim.io/doc/user/starting.html#shada) (Shared Data) file, and the site directory for plugins.

### Migrating from Vim

If you wish to migrate your existing Vim configuration to Nvim, simply copy your `~/.vimrc` to `~/.config/nvim/init.vim`. If applicable, copy the contents of `~/.vim/autoload/` to `~/.local/share/nvim/site/autoload/`.

### Shared Configuration between Vim and Nvim

Neovim uses `$XDG_CONFIG_HOME/nvim` instead of `~/.vim` as its main configuration directory and `$XDG_CONFIG_HOME/nvim/init.vim` instead of `~/.vimrc` as its main configuration file.

If you wish to continue using Vim and wish to source your existing Vim configuration in Nvim, see [nvim-from-vim](https://neovim.io/doc/user/nvim.html#nvim-from-vim) or the `:help nvim-from-vim` neovim command.

#### Loading vim addons

If you would like to use plugins, syntax definitions, or other addons that are installed for vim, you can add the default vim runtime path to neovim by adding it to the `rtp`. For example, you could run the following within nvim or add it to your neovim config:

```
set rtp^=/usr/share/vim/vimfiles/

```

## Tips and tricks

### Replacing vi and vim with neovim

Setting `$VISUAL` and `$EDITOR` [environment variables](/index.php/Environment_variables "Environment variables") should be sufficient in most cases.

Some applications may hardcode vi or vim as default editor, to use *neovim* in their place, install [neovim-drop-in](https://aur.archlinux.org/packages/neovim-drop-in/).

### Symlinking init.vim to .vimrc

As neovim is mostly compatible with standard vim, you can symlink `nvim/init.vim` to your old `.vimrc` to keep old configuration options:

```
$ ln -s ~/.vimrc ~/.config/nvim/init.vim

```

If you want some lines to specific to each version, you can use an `if` block in your `.vimrc` file:

```
if has('nvim')
    " Neovim specific commands
else
    " Standard vim specific commands
endif

```

## Troubleshooting

### Cursor is not restored to previous state after exit

If after exiting neovim cursor is still blinking see solution on [neovim FAQ](https://github.com/neovim/neovim/wiki/FAQ#cursor-style-isnt-restored-after-exiting-nvim).

## See also

*   [Github repository](https://github.com/neovim/neovim)
*   [Github wiki](https://github.com/neovim/neovim/wiki)