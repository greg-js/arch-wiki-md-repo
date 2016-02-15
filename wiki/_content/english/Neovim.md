Neovim is a fork of [Vim](/index.php/Vim "Vim") aiming to improve user experience, plugins, and GUIs.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Transition from vim](#Transition_from_vim)
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

## See also

*   [Homepage](https://neovim.io/)
*   [Github repository](https://github.com/neovim/neovim)
*   [Github wiki](https://github.com/neovim/neovim/wiki)