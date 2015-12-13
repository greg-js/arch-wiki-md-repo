# Zsh

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[Zsh](http://zsh.sourceforge.net/Intro/intro_1.html) is a powerful shell that operates as both an interactive shell and as a scripting language interpreter. While being compatible with [Bash](/index.php/Bash "Bash") (not by default, only if issuing `emulate sh`), it offers many advantages such as:

*   Efficiency
*   Improved tab completion
*   Improved globbing
*   Improved array handling
*   Full customisability

The [Zsh FAQ](http://zsh.sourceforge.net/FAQ/zshfaq01.html#l4) offers more reasons to use Zsh.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Initial configuration](#Initial_configuration)
    *   [1.2 Making Zsh your default shell](#Making_Zsh_your_default_shell)
*   [2 Configuration files](#Configuration_files)
    *   [2.1 Global configuration files](#Global_configuration_files)
*   [3 Configure Zsh](#Configure_Zsh)
    *   [3.1 Simple .zshrc](#Simple_.zshrc)
    *   [3.2 Configuring $PATH](#Configuring_.24PATH)
    *   [3.3 Command completion](#Command_completion)
    *   [3.4 The "command not found" hook](#The_.22command_not_found.22_hook)
    *   [3.5 Preventing duplicate lines in the history](#Preventing_duplicate_lines_in_the_history)
    *   [3.6 The ttyctl command](#The_ttyctl_command)
    *   [3.7 Key bindings](#Key_bindings)
        *   [3.7.1 Bind key to ncurses application](#Bind_key_to_ncurses_application)
        *   [3.7.2 Alternate way to bind ncurses application](#Alternate_way_to_bind_ncurses_application)
        *   [3.7.3 File manager key binds](#File_manager_key_binds)
    *   [3.8 History search](#History_search)
    *   [3.9 Prompts](#Prompts)
    *   [3.10 Customizing the prompt](#Customizing_the_prompt)
        *   [3.10.1 Colors](#Colors)
        *   [3.10.2 Example](#Example)
    *   [3.11 Dirstack](#Dirstack)
    *   [3.12 Help command](#Help_command)
    *   [3.13 Fish-like syntax highlighting](#Fish-like_syntax_highlighting)
    *   [3.14 Sample .zshrc files](#Sample_.zshrc_files)
    *   [3.15 Configuration Frameworks](#Configuration_Frameworks)
    *   [3.16 Autostarting applications](#Autostarting_applications)
    *   [3.17 Persistent rehash](#Persistent_rehash)
*   [4 Uninstallation](#Uninstallation)
*   [5 See also](#See_also)

## Installation

Before starting users may want to see what shell is currently being used:

```
$ echo $SHELL

```

[Install](/index.php/Install "Install") the [zsh](https://www.archlinux.org/packages/?name=zsh) package. For additional completion definitions, install the [zsh-completions](https://www.archlinux.org/packages/?name=zsh-completions) package as well.

### Initial configuration

Make sure that Zsh has been installed correctly by running the following in a terminal:

```
$ zsh

```

You should now see _zsh-newuser-install_, which will walk you through some basic configuration. If you want to skip this, press `q`. If you did not see it, you can invoke it manually with

```
$ zsh /usr/share/zsh/functions/Newuser/zsh-newuser-install -f

```

### Making Zsh your default shell

See [Command-line shell#Changing your default shell](/index.php/Command-line_shell#Changing_your_default_shell "Command-line shell").

**Tip:** If replacing [bash](https://www.archlinux.org/packages/?name=bash), users may want to move some code from `~/.bashrc` to `~/.zshrc` (e.g. the prompt and the [aliases](/index.php/Bash#Aliases "Bash")) and from `~/.bash_profile` to `~/.zprofile` (e.g. [the code that starts the X Window System](/index.php/Xinitrc#Autostart_X_at_login "Xinitrc")).

## Configuration files

When starting Zsh, it'll source the following files in this order by default:

`/etc/zsh/zshenv`

This file should contain commands to set the global [command search path](#Configuring_.24PATH) and other system-wide [environment variables](/index.php/Environment_variables "Environment variables"); it should not contain commands that produce output or assume the shell is attached to a tty.

`~/.zshenv`

Similar to `/etc/zsh/zshenv` but for per-user configuration. Generally used for setting some useful environment variables.

`/etc/zsh/zprofile`

This is a global configuration file, it'll be sourced at login. Usually used for executing some general commands at login. Please note that on Arch Linux, by default it contains [one line](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/zprofile?h=packages/zsh) which source the `/etc/profile`, see [#Global configuration files](#Global_configuration_files) for details.

`/etc/profile`

This file should be sourced by all Bourne-compatible shells upon login: it sets up an environment upon login and application-specific (`/etc/profile.d/*.sh`) settings. Note that on Arch Linux, Zsh will also source this by default.

`~/.zprofile`

This file is generally used for automatic execution of user's scripts at login.

`/etc/zsh/zshrc`

Global configuration file, will be sourced when starting as a interactive shell.

`~/.zshrc`

Main user configuration file, will be sourced when starting as a interactive shell.

`/etc/zsh/zlogin`

A global configuration file, will be sourced at the ending of initial progress when starting as a login shell.

`~/.zlogin`

Same as `/etc/zsh/zlogin` but for per-user configuration.

`/etc/zsh/zlogout`

A global configuration file, will be sourced when a login shell exits.

`~/.zlogout`

Same as `/etc/zsh/zlogout` but for per-user configuration.

**Note:**

*   The paths used in Arch's [zsh](https://www.archlinux.org/packages/?name=zsh) package are different from the default ones used in the [man pages](/index.php/Man_page "Man page")
*   `/etc/profile` is not a part of the regular list of startup files run for Zsh, but is sourced from `/etc/zsh/zprofile` in the [zsh](https://www.archlinux.org/packages/?name=zsh) package. Users should take note that `/etc/profile` sets the `$PATH` variable which will overwrite any `$PATH` variable set in `~/.zshenv`. To prevent this, please set the `$PATH` variable in `~/.zshrc` (it is not recommended to replace the default [one line](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/zprofile?h=packages/zsh) in `/etc/zsh/zprofile` with something other, it'll break the integrality of other packages which provide some scripts in `/etc/profile.d`)

### Global configuration files

Occasionally users might want to have some settings applied globally to all Zsh users. The zsh(1) said that there are some global configuration files, for example `/etc/zshrc`. This however is slightly different on Arch, since it has been compiled with flags specifically to target[[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/zsh#n34) `/etc/zsh/` instead.

So, for global configuration use `/etc/zsh/zshrc`, not `/etc/zshrc`. The same goes for `/etc/zsh/zshenv`, `/etc/zsh/zlogin` and `/etc/zsh/zlogout`. Note that these files are not installed by default, so create them if desired.

The only exception is `zprofile`, use `/etc/profile` instead.

## Configure Zsh

Although Zsh is usable out of the box, it is almost certainly not set up the way most users would like to use it, but due to the sheer amount of customization available in Zsh, configuring Zsh can be a daunting and time-consuming experience.

### Simple .zshrc

Included below is a sample configuration file, it provides a decent set of default options as well as giving examples of many ways that Zsh can be customized. In order to use this configuration save it as a file named `.zshrc`.

**Tip:** Apply the changes without needing to logout and then back in by running `source ~/.zshrc`

Here is a simple `.zshrc`:

 `~/.zshrc` 

```
autoload -U compinit promptinit
compinit
promptinit

# This will set the default prompt to the walters theme
prompt walters
```

### Configuring $PATH

In short, put the following in `~/.zshenv`:

 `~/.zshenv` 

```
typeset -U path
path=(~/bin /other/things/in/path $path[@])
```

See also [A User's Guide to the Z-Shell](http://zsh.sourceforge.net/Guide/zshguide02.html#l24) and the note in [#Configuration files](#Configuration_files).

### Command completion

Perhaps the most compelling feature of Zsh is its advanced autocompletion abilities. At the very least, enable autocompletion in `.zshrc`. To enable autocompletion, add the following to your `~/.zshrc`:

 `~/.zshrc` 

```
autoload -U compinit
compinit

```

The above configuration includes ssh/scp/sftp hostnames completion but in order for this feature to work, users need to prevent ssh from hashing hosts names in `~/.ssh/known_hosts`.

**Warning:** This makes the computer vulnerable to ["Island-hopping" attacks](http://blog.rootshell.be/2010/11/03/bruteforcing-ssh-known_hosts-files/). In that intention, comment the following line or set the value to `no`: `/etc/ssh/ssh_config`  `#HashKnownHosts yes` 

And move `~/.ssh/known_hosts` somewhere else so that ssh creates a new one with un-hashed hostnames (previously known hosts will thus be lost). For more information, see the SSH readme for [hashed-hosts](http://nms.lcs.mit.edu/projects/ssh/README.hashed-hosts).

For autocompletion with an arrow-key driven interface, add the following to:

 `~/.zshrc`  `zstyle ':completion:*' menu select` 

_To activate the menu, press tab twice._

For autocompletion of command line switches for aliases, add the following to:

 `~/.zshrc`  `setopt completealiases` 

### The "command not found" hook

See [Pkgfile#Command not found](/index.php/Pkgfile#Command_not_found "Pkgfile").

### Preventing duplicate lines in the history

To ignore duplicate lines in the history, use the following:

 `~/.zshrc`  `setopt HIST_IGNORE_DUPS` 

To free the history from already created duplicates, run:

```
$ sort -t ";" -k 2 -u ~/.zsh_history | sort -o ~/.zsh_history

```

### The ttyctl command

[[2]](http://zsh.sourceforge.net/Doc/Release/Shell-Builtin-Commands.html#index-tty_002c-freezing) describes the `ttyctl` command in Zsh. This may be used to "freeze/unfreeze" the terminal. Many programs change the terminal state, and often do not restore terminal settings on exiting abnormally. To avoid the need to manually reset the terminal, use the following:

 `~/.zshrc`  `ttyctl -f` 

### Key bindings

Zsh does not use readline, instead it uses its own and more powerful zle. It does not read `/etc/inputrc` or `~/.inputrc`. Zle has an [emacs](/index.php/Emacs "Emacs") mode and a [vi](/index.php/Vi "Vi") mode. By default, it tries to guess whether emacs or vi keys from the `$EDITOR` environment variable are desired. If it is empty, it will default to emacs. Change this with `bindkey -e` or `bindkey -v` respectively for emacs mode or vi mode.

See also [zshwiki: bindkeys](http://zshwiki.org/home/zle/bindkeys).

#### Bind key to ncurses application

Bind a ncurses application to a keystoke, but it will not accept interaction. Use `BUFFER` variable to make it work. The following example lets users open ncmpcpp using `Alt+\`:

 `~/.zshrc` 

```
ncmpcppShow() { BUFFER="ncmpcpp"; zle accept-line; }
zle -N ncmpcppShow
bindkey '^[\' ncmpcppShow
```

#### Alternate way to bind ncurses application

This method will keep everything you entered in the line before calling application

 `~/.zshrc` 

```
ncmpcppShow() { ncmpcpp <$TTY; zle redisplay; }
zle -N ncmpcppShow
bindkey '^[\' ncmpcppShow
```

#### File manager key binds

Key binds like those used in graphic file managers may come handy. The first comes back in directory history (`Alt+Left`), the second let the user go to the parent directory (`Alt+Up`). They also display the directory content.

 `~/.zshrc` 

```
cdUndoKey() {
  popd      > /dev/null
  zle       reset-prompt
  echo
  ls
  echo
}

cdParentKey() {
  pushd .. > /dev/null
  zle      reset-prompt
  echo
  ls
  echo
}

zle -N                 cdParentKey
zle -N                 cdUndoKey
bindkey '^[[1;3A'      cdParentKey
bindkey '^[[1;3D'      cdUndoKey

```

### History search

Add these lines to .zshrc

 `~/.zshrc` 

```
[[ -n "${key[PageUp]}"   ]]  && bindkey  "${key[PageUp]}"    history-beginning-search-backward
[[ -n "${key[PageDown]}" ]]  && bindkey  "${key[PageDown]}"  history-beginning-search-forward

```

Doing this, only past commands beginning with the current input would have been shown.

### Prompts

There is a quick and easy way to set up a colored prompt in Zsh. Make sure that prompt is set to autoload in `.zshrc`. This can be done by adding these lines to:

 `~/.zshrc` 

```
autoload -U promptinit
promptinit

```

Available prompts are listed by running the command:

```
$ prompt -l

```

For example, to use the prompt `walters`, enter:

```
$ prompt walters

```

To preview all available themes, use this command:

```
$ prompt -p

```

### Customizing the prompt

For users who are dissatisfied with the prompts mentioned above (or want to expand their usefulness), Zsh offers the possibility to build a custom prompt. Zsh supports a left- and right-sided prompt additional to the single, left-sided prompt that is common to all shells. Customize it by using `PROMPT=` with the following variables:

See [Prompt Expansion](http://zsh.sourceforge.net/Doc/Release/Prompt-Expansion.html) for a list of prompt variables and conditional substrings.

#### Colors

Zsh sets colors differently than [Bash](/index.php/Color_Bash_Prompt "Color Bash Prompt"). Add `autoload -U colors && colors` before `PROMPT=` in `.zshrc` to use them. Usually you will want to put these inside `%{ [...] %}` so the cursor does not move.

`$fg[color]` will set the text color (red, green, blue, etc. - defaults to whatever format set prior to text)

<table class="wikitable">

<tbody>

<tr>

<th>Command</th>

<th>Description</th>

</tr>

<tr>

<td>`%F{color} [...] %f`</td>

<td>effectively the same as the previous, but with less typing. Can also prefix F with a number instead.</td>

</tr>

<tr>

<td>`$fg_no_bold[color]`</td>

<td>will set text to non-bold and set the text color</td>

</tr>

<tr>

<td>`$fg_bold[color]`</td>

<td>will set the text to bold and set the text color</td>

</tr>

<tr>

<td>`$reset_color`</td>

<td>will reset the text color to the default color. Does not reset bold. use `%b` to reset bold. Saves typing if it's just `%f` though.</td>

</tr>

<tr>

<td>`%K{color} [...] %k`</td>

<td>will set the background color. Same color as non-bold text color. Prefixing with any single-digit number makes the bg black.</td>

</tr>

</tbody>

</table>

<table class="wikitable">

<tbody>

<tr>

<th colspan="2">Possible color values</th>

</tr>

<tr>

<td>`black` or `0`</td>

<td>`red` or `1`</td>

</tr>

<tr>

<td>`green` or `2`</td>

<td>`yellow` or `3`</td>

</tr>

<tr>

<td>`blue` or `4`</td>

<td>`magenta` or `5`</td>

</tr>

<tr>

<td>`cyan` or `6`</td>

<td>`white` or `7`</td>

</tr>

</tbody>

</table>

**Note:** Bold text does not necessarily use the same colors as normal text. For example, `$fg['yellow']` looks brown or a very dark yellow, while `$fg_bold['yellow']` looks like bright or regular yellow.

#### Example

This is an example of a two-sided prompt:

```
PROMPT="%{$fg[red]%}%n%{$reset_color%}@%{$fg[blue]%}%m %{$fg_no_bold[yellow]%}%1~ %{$reset_color%}%#"
RPROMPT="[%{$fg_no_bold[yellow]%}%?%{$reset_color%}]"

```

And here's how it will be displayed:

```
username@host ~ %                                                         [0]

```

### Dirstack

Zsh can be configured to remember the DIRSTACKSIZE last visited folders. This can then be used to _cd_ them very quickly. You need to add some lines to you configuration file:

 `.zshrc` 

```
DIRSTACKFILE="$HOME/.cache/zsh/dirs"
if [[ -f $DIRSTACKFILE ]] && [[ $#dirstack -eq 0 ]]; then
  dirstack=( ${(f)"$(< $DIRSTACKFILE)"} )
  [[ -d $dirstack[1] ]] && cd $dirstack[1]
fi
chpwd() {
  print -l $PWD ${(u)dirstack} >$DIRSTACKFILE
}

DIRSTACKSIZE=20

setopt autopushd pushdsilent pushdtohome

## Remove duplicate entries
setopt pushdignoredups

## This reverts the +/- operators.
setopt pushdminus

```

Now use

```
dirs -v

```

to print the dirstack. Use `cd -<NUM>` to go back to a visited folder. Use autocompletion after the dash. This proves very handy if using the autocompletion menu.

### Help command

Unlike [bash](/index.php/Bash "Bash"), _zsh_ does not enable a built in `help` command. To use `help` in zsh, add following to your `zshrc`:

```
autoload -U run-help
autoload run-help-git
autoload run-help-svn
autoload run-help-svk
unalias run-help
alias help=run-help
```

### Fish-like syntax highlighting

[Fish](/index.php/Fish "Fish") provides a very powerful shell syntax highlighting. To use this in zsh, you can install [zsh-syntax-highlighting](https://www.archlinux.org/packages/?name=zsh-syntax-highlighting) from offical repository and add following to your zshrc:

```
source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

```

### Sample .zshrc files

*   A package in offical repository named [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config) comes from [http://grml.org/zsh](http://grml.org/zsh) and provides a zshrc file that includes many tweaks for Zshell. This is the default configuration for the [monthly ISO releases](https://www.archlinux.org/download/).
*   Basic setup, with dynamic prompt and window title/hardinfo => [http://github.com/MrElendig/dotfiles-alice/blob/master/.zshrc](http://github.com/MrElendig/dotfiles-alice/blob/master/.zshrc);
*   [https://github.com/slashbeast/things/blob/master/configs/DOTzshrc](https://github.com/slashbeast/things/blob/master/configs/DOTzshrc) - zshrc with multiple features, be sure to check out comments into it. Notable features: confirm function to ensure that user want to run poweroff, reboot or hibernate, support for GIT in prompt (done without vcsinfo), tab completion with menu, printing current executed command into window's title bar and more.

### Configuration Frameworks

*   [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) is a popular, community-driven framework for managing your Zsh configuration. It comes bundled with a ton of helpful functions, helpers, plugins, themes.
*   [Prezto - Instantly Awesome Zsh](https://github.com/sorin-ionescu/prezto) (available as [prezto-git](https://aur.archlinux.org/packages/prezto-git/)<sup><small>AUR</small></sup>) is a configuration framework for Zsh. It comes with modules, enriching the command line interface environment with sane defaults, aliases, functions, auto completion, and prompt themes.
*   [Antigen](https://github.com/zsh-users/antigen) (available as [antigen-git](https://aur.archlinux.org/packages/antigen-git/)<sup><small>AUR</small></sup>) - A plugin manager for zsh, inspired by oh-my-zsh and vundle.

### Autostarting applications

**Note:** `$ZDOTDIR` defaults to `$HOME`

Zsh always executes `/etc/zsh/zshenv` and `$ZDOTDIR/.zshenv` so do not bloat these files.

If the shell is a login shell, commands are read from `/etc/profile` and then `$ZDOTDIR/.zprofile`. Then, if the shell is interactive, commands are read from `/etc/zsh/zshrc` and then `$ZDOTDIR/.zshrc`. Finally, if the shell is a login shell, `/etc/zsh/zlogin` and `$ZDOTDIR/.zlogin` are read.

See also the _STARTUP/SHUTDOWN FILES_ section of `man zsh`.

### Persistent rehash

Typically, compinit will not automatically find new executables in the $PATH. For example, after you install a new package, the files in /usr/bin would not be immediately or automatically included in the completion. Thus, to have these new exectuables included, one would run:

```
$ rehash

```

This 'rehash' can be set to happen automatically. Simply include the following in your `zshrc`:

 `~/.zshrc`  `zstyle ':completion:*' rehash true` 

**Note:** This hack has been found in a PR for Oh My Zsh [[3]](https://github.com/robbyrussell/oh-my-zsh/issues/3440)

## Uninstallation

Change the default shell before removing the [zsh](https://www.archlinux.org/packages/?name=zsh) package.

**Warning:** Failure to follow the below procedure may result in users no longer having access to a working shell.

Run following command:

```
$ chsh -s /bin/bash _user_

```

Use it for every user with _zsh_ set as their login shell (including root if needed). When completed, the [zsh](https://www.archlinux.org/packages/?name=zsh) package can be removed.

Alternatively, change the default shell back to Bash by editing `/etc/passwd` as root.

**Warning:** It is strongly recommended to use `vipw` when editing `/etc/passwd` as it helps prevent invalid entries and/or syntax errors.

For example, change the following:

```
_username_:x:1000:1000:_Full Name_,,,:/home/_username_:/bin/zsh

```

To this:

```
_username_:x:1000:1000:_Full Name_,,,:/home/_username_:/bin/bash

```

## See also

*   [A User's Guide to ZSH](http://zsh.sourceforge.net/Guide/zshguide.html)
*   [The Z Shell Manual](http://zsh.sourceforge.net/Doc/Release/index-frame.html) (different format available [here](http://zsh.sourceforge.net/Doc/))
*   [Zsh FAQ](http://zsh.sourceforge.net/FAQ/zshfaq01.html)
*   [zsh-lovers(1)](http://grml.org/zsh/zsh-lovers.html) (this is also available as [zsh-lovers](https://www.archlinux.org/packages/?name=zsh-lovers) in offical repository)
*   [Zsh Wiki](http://zshwiki.org/home/)
*   [Gentoo Wiki: Zsh/HOWTO](https://wiki.gentoo.org/wiki/Zsh/HOWTO)
*   [Bash2Zsh Reference Card](http://www.bash2zsh.com/zsh_refcard/refcard.pdf)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Zsh&oldid=411931](https://wiki.archlinux.org/index.php?title=Zsh&oldid=411931)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Command shells](/index.php/Category:Command_shells "Category:Command shells")