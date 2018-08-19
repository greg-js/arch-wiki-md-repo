[Powerline](https://powerline.readthedocs.io/en/master/index.html) is a statusline plugin for Vim, and provides statuslines and prompts for several other applications, including zsh, bash, tmux, IPython, Awesome, i3 and Qtile.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Official repositories](#Official_repositories)
    *   [1.2 Using python-pip](#Using_python-pip)
    *   [1.3 Using a vim plugin manager](#Using_a_vim_plugin_manager)
    *   [1.4 Fonts](#Fonts)
    *   [1.5 Airline-vim alternative](#Airline-vim_alternative)
    *   [1.6 Special plugins](#Special_plugins)
*   [2 Usage](#Usage)
    *   [2.1 Bash](#Bash)
    *   [2.2 Zsh](#Zsh)
    *   [2.3 Other plugins](#Other_plugins)

## Installation

Powerline can be installed in multiple ways, depending on preference and/or usage intent.

### Official repositories

[Install](/index.php/Install "Install") [powerline](https://www.archlinux.org/packages/?name=powerline) and [powerline-fonts](https://www.archlinux.org/packages/?name=powerline-fonts) from the [official repositories](/index.php/Official_repositories "Official repositories")

### Using python-pip

*   [Install](/index.php/Install "Install") [python-pip](https://www.archlinux.org/packages/?name=python-pip) from the [official repositories](/index.php/Official_repositories "Official repositories")
*   Please refer to the [Powerline installation guide](https://powerline.readthedocs.io/en/master/installation.html) for additional python-pip instructions

### Using a vim plugin manager

There are many vim plugin managers available which are able to install and update Powerline, assuming you are using a version of vim with Python support or you install [python](https://www.archlinux.org/packages/?name=python). For example, using [vim-plug](https://aur.archlinux.org/packages/vim-plug/) from the [AUR](/index.php/AUR "AUR"), add the following to your vimrc file:

 `~/.vimrc` 
```
call plug#begin('*path/to/vim/plugins/directory*')

Plug 'powerline/powerline'

call plug#end()

```

Substitute `*path/to/vim/plugins/directory*` with the actual directory, such as `~/.vim/plugged`, or `~/.local/share/nvim/plugged` for Neovim, and run the vim-plug command `:PlugInstall` within vim. This will download Powerline from the [Powerline GitHub page](https://github.com/powerline/powerline) to the specified plugin directory and add it to vim.

### Fonts

Powerline uses special glyphs and symbols that will not appear correctly unless they are added to fontconfig or patched fonts are installed and used. The fontconfig and some patched fonts are available in the [powerline-fonts](https://www.archlinux.org/packages/?name=powerline-fonts) package from the [official repositories](/index.php/Official_repositories "Official repositories"). A reduced set of fonts for the text console are available in [powerline-console-fonts](https://aur.archlinux.org/packages/powerline-console-fonts/).

### Airline-vim alternative

There is currently one known alternative to Powerline - [Vim-airline](https://github.com/vim-airline). It is a part of [vim-plugins](https://www.archlinux.org/groups/x86_64/vim-plugins/) and can be installed separately as [vim-airline](https://www.archlinux.org/packages/?name=vim-airline). Optionally, install [vim-airline-themes](https://www.archlinux.org/packages/?name=vim-airline-themes).

### Special plugins

Depending on where you want to use Powerline, you might need to install additional packages.

	[Vim](/index.php/Vim "Vim")

	[powerline-vim](https://www.archlinux.org/packages/?name=powerline-vim)

After installing the package, you may need to add `let g:powerline_pycmd="py3"` or `let g:powerline_pycmd="py"` to your vimrc if you have more than one version of python installed.

**Tip:** By default, the statusline (and therefore Powerline) only appears when there are multiple windows open. To show it all the time, use `:set laststatus=2`

**Tip:** This package installs Powerline to `/usr/share/vim/vimfiles/plugin`, which vim is configured to check by default, meaning this will install Powerline in vim for all users and may require additional configuration. If this is not intended, consider either using a vim plugin manager, or installing the [powerline](https://www.archlinux.org/packages/?name=powerline) package and adding `set rtp+=/usr/lib/python3.7/site-packages/powerline/bindings/vim` to your vimrc.

## Usage

### Bash

After installing [powerline](https://www.archlinux.org/packages/?name=powerline) and [powerline-fonts](https://www.archlinux.org/packages/?name=powerline-fonts). Add the following to your **~/.bashrc**:

```
powerline-daemon -q
POWERLINE_BASH_CONTINUATION=1
POWERLINE_BASH_SELECT=1
. /usr/share/powerline/bindings/bash/powerline.sh

```

Close and reopen your terminal and it should be working. If not, check the [Powerline bash prompt](https://powerline.readthedocs.io/en/latest/usage/shell-prompts.html#bash-prompt) usage instructions to ensure that it has not changed.

### Zsh

After installing [powerline](https://www.archlinux.org/packages/?name=powerline) and [powerline-fonts](https://www.archlinux.org/packages/?name=powerline-fonts). Add the following to your **~/.zshrc**:

```
powerline-daemon -q
. /usr/lib/python3.7/site-packages/powerline/bindings/zsh/powerline.zsh

```

### Other plugins

For detailed usage instructions, such as configuring your system to use Powerline with other shells, window manager widgets, etc., please refer to the [Usage section](https://powerline.readthedocs.io/en/latest/usage.html#usage) of the [Powerline documentation](https://powerline.readthedocs.io/en/latest/index.html).