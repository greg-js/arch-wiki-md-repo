fzf is a general-purpose command-line fuzzy finder.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 bash](#bash)
    *   [2.2 zsh](#zsh)
    *   [2.3 fish](#fish)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [fzf](https://www.archlinux.org/packages/?name=fzf) package. The development version is [fzf-git](https://aur.archlinux.org/packages/fzf-git/).

## Configuration

Optional fzf keybindings and completion are available for various shells.

### bash

[Source](/index.php/Source "Source") the desired files from your `.bashrc`:

*   `/usr/share/fzf/key-bindings.bash`
*   `/usr/share/fzf/completion.bash`

### zsh

Source the desired files from your `.zshrc`:

*   `/usr/share/fzf/key-bindings.zsh`
*   `/usr/share/fzf/completion.zsh`

### fish

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

## See also

*   [https://github.com/junegunn/fzf](https://github.com/junegunn/fzf) - Development page
*   [https://github.com/junegunn/fzf/wiki](https://github.com/junegunn/fzf/wiki) - The wiki with customization examples.