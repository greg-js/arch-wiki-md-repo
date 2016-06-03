Neovim is a fork of [Vim](/index.php/Vim "Vim") aiming to improve user experience, plugins, and GUIs.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Transition from vim](#Transition_from_vim)
        *   [2.1.1 Loading vim addons](#Loading_vim_addons)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [neovim](https://www.archlinux.org/packages/?name=neovim) package.

## Configuration

### Transition from vim

Neovim uses `$XDG_CONFIG_HOME/nvim` instead of `~/.vim` as its main configuration directory and `$XDG_CONFIG_HOME/nvim/init.vim` instead of `~/.vimrc` as its main configuration file. To use your vim configuration in neovim execute the following commands which will create the appropriate symlinks:

```
$ mkdir -p ${XDG_CONFIG_HOME:=$HOME/.config}
$ ln -s ~/.vim $XDG_CONFIG_HOME/nvim
$ ln -s ~/.vimrc $XDG_CONFIG_HOME/nvim/init.vim

```

To get more info about the transition run the following command in neovim:

```
:help nvim-from-vim

```

#### Loading vim addons

If you would like to use plugins, syntax definitions, or other addons that are installed for vim, you can add the default vim runtime path to neovim by adding it to the `rtp`. For example, you could run the following within nvim or add it to your neovim config:

```
set rtp^=/usr/share/vim/vimfiles/

```

## See also

*   [Homepage](https://neovim.io/)
*   [Github repository](https://github.com/neovim/neovim)
*   [Github wiki](https://github.com/neovim/neovim/wiki)