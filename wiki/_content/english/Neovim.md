Neovim is a fork of [Vim](/index.php/Vim "Vim") aiming to improve user experience, plugins, and GUIs.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Transition from vim](#Transition_from_vim)
        *   [2.1.1 Loading vim addons](#Loading_vim_addons)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Replacing vi and vim with neovim](#Replacing_vi_and_vim_with_neovim)
*   [4 See also](#See_also)

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

## See also

*   [Homepage](https://neovim.io/)
*   [Github repository](https://github.com/neovim/neovim)
*   [Github wiki](https://github.com/neovim/neovim/wiki)