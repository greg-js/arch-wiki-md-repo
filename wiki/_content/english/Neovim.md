[Neovim](https://neovim.io/) is a fork of [Vim](/index.php/Vim "Vim") aiming to improve user experience, plugins, and GUIs.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Transition from vim](#Transition_from_vim)
        *   [2.1.1 Loading vim addons](#Loading_vim_addons)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Replacing vi and vim with neovim](#Replacing_vi_and_vim_with_neovim)
    *   [3.2 Symlinking init.vim to .vimrc](#Symlinking_init.vim_to_.vimrc)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Cursor is not restored to previous state after exit](#Cursor_is_not_restored_to_previous_state_after_exit)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [neovim](https://www.archlinux.org/packages/?name=neovim) package.

## Configuration

### Transition from vim

Neovim uses `$XDG_CONFIG_HOME/nvim` instead of `~/.vim` as its main configuration directory and `$XDG_CONFIG_HOME/nvim/init.vim` instead of `~/.vimrc` as its main configuration file.

See [nvim-from-vim](https://neovim.io/doc/user/nvim.html#nvim-from-vim) or the `:help nvim-from-vim` neovim command to use your vim configuration in neovim.

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

In case the provided solution does not work, set blinking to **on** instead. See [issue 6665](https://github.com/neovim/neovim/issues/6665).

 `~/.config/nvim/init.vim`  `au VimLeave * set guicursor+=a:blinkon**1**` 

## See also

*   [Github repository](https://github.com/neovim/neovim)
*   [Github wiki](https://github.com/neovim/neovim/wiki)