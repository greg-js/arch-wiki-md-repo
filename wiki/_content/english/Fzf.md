[fzf](https://github.com/junegunn/fzf) is a general-purpose command-line fuzzy finder.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Shells](#Shells)
        *   [2.1.1 bash](#bash)
        *   [2.1.2 zsh](#zsh)
        *   [2.1.3 fish](#fish)
    *   [2.2 Vim](#Vim)

## Installation

[Install](/index.php/Install "Install") the [fzf](https://www.archlinux.org/packages/?name=fzf) package. The development version is [fzf-git](https://aur.archlinux.org/packages/fzf-git/).

## Configuration

### Shells

Optional fzf keybindings and completion are available for various shells.

#### bash

[Source](/index.php/Source "Source") the desired files from your `.bashrc`:

*   `/usr/share/fzf/key-bindings.bash`
*   `/usr/share/fzf/completion.bash`

#### zsh

Source the desired files from your `.zshrc`:

*   `/usr/share/fzf/key-bindings.zsh`
*   `/usr/share/fzf/completion.zsh`

#### fish

For fish, keybindings are in:

*   `/usr/share/fish/functions/fzf.fish`

fish will source this by default but the bindings have to be enabled manually:

 `~/.config/fish/functions/fish_user_key_bindings.fish` 
```
function fish_user_key_bindings
	fzf_key_bindings
end

```

fzf completion in fish can be enabled with custom functions: [https://github.com/junegunn/fzf/wiki/Examples-(fish)](https://github.com/junegunn/fzf/wiki/Examples-(fish))

### Vim

The basic Vim plugin is already included within the package and installed to Vim's global plugin directory. Thus, you don't need to add anything to your `.vimrc` to be able to use it. It only provides the FZF command, though. There is an additional Vim plugin made by the author of fzf that defines some convenience functions, see [https://github.com/junegunn/fzf.vim](https://github.com/junegunn/fzf.vim).