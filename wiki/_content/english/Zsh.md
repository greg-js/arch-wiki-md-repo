[Zsh](http://zsh.sourceforge.net/Intro/intro_1.html) is a powerful [shell](/index.php/Shell "Shell") that operates as both an interactive shell and as a scripting language interpreter. While being compatible with [Bash](/index.php/Bash "Bash") (not by default, only if issuing `emulate sh`), it offers advantages such as improved [tab completion](http://zsh.sourceforge.net/Guide/zshguide06.html) and [globbing](http://zsh.sourceforge.net/Doc/Release/Expansion.html).

The [Zsh FAQ](http://zsh.sourceforge.net/FAQ/zshfaq01.html#l4) offers more reasons to use Zsh.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Initial configuration](#Initial_configuration)
    *   [1.2 Making Zsh your default shell](#Making_Zsh_your_default_shell)
*   [2 Startup/Shutdown files](#Startup.2FShutdown_files)
*   [3 Configure Zsh](#Configure_Zsh)
    *   [3.1 Simple .zshrc](#Simple_.zshrc)
    *   [3.2 Configuring $PATH](#Configuring_.24PATH)
    *   [3.3 Command completion](#Command_completion)
    *   [3.4 Key bindings](#Key_bindings)
    *   [3.5 History search](#History_search)
    *   [3.6 Prompts](#Prompts)
        *   [3.6.1 Prompt themes](#Prompt_themes)
        *   [3.6.2 Customized prompt](#Customized_prompt)
            *   [3.6.2.1 Colors](#Colors)
            *   [3.6.2.2 Example](#Example)
    *   [3.7 Sample .zshrc files](#Sample_.zshrc_files)
    *   [3.8 Configuration Frameworks](#Configuration_Frameworks)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Autostart X at login](#Autostart_X_at_login)
    *   [4.2 The "command not found" hook](#The_.22command_not_found.22_hook)
    *   [4.3 The ttyctl command](#The_ttyctl_command)
    *   [4.4 Remembering recent directories](#Remembering_recent_directories)
        *   [4.4.1 Dirstack](#Dirstack)
        *   [4.4.2 cdr](#cdr)
    *   [4.5 Help command](#Help_command)
    *   [4.6 Fish-like syntax highlighting](#Fish-like_syntax_highlighting)
    *   [4.7 Persistent rehash](#Persistent_rehash)
    *   [4.8 Bind key to ncurses application](#Bind_key_to_ncurses_application)
    *   [4.9 File manager key binds](#File_manager_key_binds)
    *   [4.10 xterm title](#xterm_title)
*   [5 Uninstallation](#Uninstallation)
*   [6 See also](#See_also)

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

You should now see *zsh-newuser-install*, which will walk you through some basic configuration. If you want to skip this, press `q`. If you did not see it, you can invoke it manually with

```
$ zsh /usr/share/zsh/functions/Newuser/zsh-newuser-install -f

```

### Making Zsh your default shell

See [Command-line shell#Changing your default shell](/index.php/Command-line_shell#Changing_your_default_shell "Command-line shell").

**Tip:** If replacing [bash](https://www.archlinux.org/packages/?name=bash), users may want to move some code from `~/.bashrc` to `~/.zshrc` (e.g. the prompt and the [aliases](/index.php/Bash#Aliases "Bash")) and from `~/.bash_profile` to `~/.zprofile` (e.g. [the code that starts the X Window System](/index.php/Xinitrc#Autostart_X_at_login "Xinitrc")).

## Startup/Shutdown files

**Tip:** See [A User's Guide to the Z-Shell](http://zsh.sourceforge.net/Guide/zshguide02.html) for explanation on interactive and login shells, and what to put in your startup files.

**Note:**

*   If `$ZDOTDIR` is not set, `$HOME` is used instead.
*   If option `RCS` is unset in any of the files, no configuration files will be sourced after that file.
*   If option `GLOBAL_RCS` is unset in any of the files, no global configuration files (`/etc/zsh/*`) will be sourced after that file.

When starting Zsh, it'll source the following files in this order by default:

	`/etc/zsh/zshenv`

	Used for setting system-wide [environment variables](/index.php/Environment_variables "Environment variables"); it should not contain commands that produce output or assume the shell is attached to a tty. This file will ***always*** be sourced, this cannot be overridden.

	`$ZDOTDIR/.zshenv`

	Used for setting user's environment variables; it should not contain commands that produce output or assume the shell is attached to a tty. This file will ***always*** be sourced.

	`/etc/zsh/zprofile`

	Used for executing commands at start, will be sourced when starting as a ***login shell***. Please note that on Arch Linux, by default it contains [one line](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/zprofile?h=packages/zsh) which source the `/etc/profile`.

	`/etc/profile`

	This file should be sourced by all Bourne-compatible shells upon login: it sets up `$PATH` and other environment variables and application-specific (`/etc/profile.d/*.sh`) settings upon login.

	`$ZDOTDIR/.zprofile`

	Used for executing user's commands at start, will be sourced when starting as a ***login shell***.

	`/etc/zsh/zshrc`

	Used for setting interactive shell configuration and executing commands, will be sourced when starting as an ***interactive shell***.

	`$ZDOTDIR/.zshrc`

	Used for setting user's interactive shell configuration and executing commands, will be sourced when starting as an ***interactive shell***.

	`/etc/zsh/zlogin`

	Used for executing commands at ending of initial progress, will be sourced when starting as a ***login shell***.

	`$ZDOTDIR/.zlogin`

	Used for executing user's commands at ending of initial progress, will be sourced when starting as a ***login shell***.

	`$ZDOTDIR/.zlogout`

	Will be sourced when a ***login shell*** **exits**.

	`/etc/zsh/zlogout`

	Will be sourced when a ***login shell*** **exits**.

**Note:**

*   The paths used in Arch's [zsh](https://www.archlinux.org/packages/?name=zsh) package are different from the default ones used in the [man pages](/index.php/Man_page "Man page") ([FS#48992](https://bugs.archlinux.org/task/48992)).
*   `/etc/profile` is not a part of the regular list of startup files run for Zsh, but is sourced from `/etc/zsh/zprofile` in the [zsh](https://www.archlinux.org/packages/?name=zsh) package. Users should take note that `/etc/profile` sets the `$PATH` variable which will overwrite any `$PATH` variable set in `$ZDOTDIR/.zshenv`. To prevent this, please set the `$PATH` variable in `$ZDOTDIR/.zprofile`.

**Warning:** It is not recommended to replace the default [one line](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/zprofile?h=packages/zsh) in `/etc/zsh/zprofile` with something other, it will break the integrality of other packages which provide some scripts in `/etc/profile.d`.

## Configure Zsh

Although Zsh is usable out of the box, it is almost certainly not set up the way most users would like to use it, but due to the sheer amount of customization available in Zsh, configuring Zsh can be a daunting and time-consuming experience.

### Simple .zshrc

Included below is a sample configuration file, it provides a decent set of default options as well as giving examples of many ways that Zsh can be customized. In order to use this configuration save it as a file named `.zshrc`.

**Tip:** Apply the changes without needing to logout and then back in by running `source ~/.zshrc`.

Here is a simple `.zshrc`:

 `~/.zshrc` 
```
autoload -Uz compinit promptinit
compinit
promptinit

# This will set the default prompt to the walters theme
prompt walters

```

### Configuring $PATH

Normally, the path should be set in `~/.zshenv`, but Arch Linux sources `/etc/profile` after sourcing `~/.zshenv`.

To prevent your `$PATH` being overwritten, set it in `~/.zprofile`.

 `~/.zprofile` 
```
typeset -U path
path=(*~/bin* */other/things/in/path* $path[@])
```

See also [A User's Guide to the Z-Shell](http://zsh.sourceforge.net/Guide/zshguide02.html#l24) and the note in [#Startup/Shutdown files](#Startup.2FShutdown_files).

### Command completion

Perhaps the most compelling feature of Zsh is its advanced autocompletion abilities. At the very least, enable autocompletion in `.zshrc`. To enable autocompletion, add the following to your `~/.zshrc`:

 `~/.zshrc` 
```
autoload -Uz compinit
compinit

```

The above configuration includes ssh/scp/sftp hostnames completion but in order for this feature to work, users need to prevent ssh from hashing hosts names in `~/.ssh/known_hosts`.

**Warning:** This makes the computer vulnerable to ["Island-hopping" attacks](http://blog.rootshell.be/2010/11/03/bruteforcing-ssh-known_hosts-files/). In that intention, comment the following line or set the value to `no`: `/etc/ssh/ssh_config` 
```
#HashKnownHosts yes

```

And move `~/.ssh/known_hosts` somewhere else so that ssh creates a new one with un-hashed hostnames (previously known hosts will thus be lost). For more information, see the SSH readme for [hashed-hosts](http://nms.lcs.mit.edu/projects/ssh/README.hashed-hosts).

For autocompletion with an arrow-key driven interface, add the following to:

 `~/.zshrc` 
```
zstyle ':completion:*' menu select

```

	*To activate the menu, press tab twice.*

For autocompletion of command line switches for aliases, add the following to:

 `~/.zshrc` 
```
setopt COMPLETE_ALIASES

```

### Key bindings

Zsh does not use [readline](/index.php/Readline "Readline"), instead it uses its own and more powerful Zsh Line Editor, ZLE. It does not read `/etc/inputrc` or `~/.inputrc`. ZLE has an [emacs](/index.php/Emacs "Emacs") mode and a [vi](/index.php/Vi "Vi") mode. If one of the `$VISUAL` or `$EDITOR` environment variables contain the string `vi` then vi mode will be used; otherwise, it will default to emacs mode. Set the mode explicitly with `bindkey -e` or `bindkey -v` respectively for emacs mode or vi mode.

See also [zshwiki: bindkeys](http://zshwiki.org/home/zle/bindkeys).

### History search

Add these lines to .zshrc

 `~/.zshrc` 
```
autoload -Uz up-line-or-beginning-search down-line-or-beginning-search
zle -N up-line-or-beginning-search
zle -N down-line-or-beginning-search

[[ -n "${key[Up]}"   ]] && bindkey "${key[Up]}"   up-line-or-beginning-search
[[ -n "${key[Down]}" ]] && bindkey "${key[Down]}" down-line-or-beginning-search

```

Doing this, only past commands matching the current line up to the current cursor position will be shown.

### Prompts

#### Prompt themes

There is a quick and easy way to set up a colored prompt in Zsh. Make sure that prompt theme system is set to autoload in `.zshrc`. This can be done by adding these lines to:

 `~/.zshrc` 
```
autoload -Uz promptinit
promptinit

```

Available prompt themes are listed by running the command:

```
$ prompt -l

```

For example, to use the `walters` theme, enter:

```
$ prompt walters

```

To preview all available themes, use this command:

```
$ prompt -p

```

#### Customized prompt

For users who are dissatisfied with the prompts mentioned above (or want to expand their usefulness), Zsh offers the possibility to build a custom prompt. Zsh supports a left- and right-sided prompt additional to the single, left-sided prompt that is common to all shells. Customize it by using `PROMPT=` with prompt escapes.

See [Prompt Expansion](http://zsh.sourceforge.net/Doc/Release/Prompt-Expansion.html) for a list of prompt variables and conditional substrings, or take a look at the zshmisc(1) manpage.

##### Colors

Zsh sets colors differently than [Bash](/index.php/Color_Bash_Prompt "Color Bash Prompt").

See [Visual effects](http://zsh.sourceforge.net/Doc/Release/Prompt-Expansion.html#Visual-effects) in zshmisc(1) for prompt escapes to set foreground color, background color and other visual effects.

Colors can be specified by [numeric color code](https://upload.wikimedia.org/wikipedia/en/1/15/Xterm_256color_chart.svg) or by name (see zshzle(1) section [CHARACTER HIGHLIGHTING](http://zsh.sourceforge.net/Doc/Release/Zsh-Line-Editor.html#Character-Highlighting)). Most terminals support the following colors by name:

| Possible color values |
| `black` or `0` | `red` or `1` |
| `green` or `2` | `yellow` or `3` |
| `blue` or `4` | `magenta` or `5` |
| `cyan` or `6` | `white` or `7` |

**Note:** Bold text does not necessarily use the same colors as normal text. For example, `%F{yellow}*text*%f` looks brown or a very dark yellow, while `%F{yellow}%B*text*%b%f` looks like bright or regular yellow.

**Tip:** Prompt escapes can be tested with command `print -P *"prompt escapes"*`, for example:
```
$ print -P '%B%F{red}co%F{green}lo%F{blue}rs%f%b'

```

##### Example

This is an example of a two-sided prompt:

```
PROMPT='%F{red}%n%f@%F{blue}%m%f %F{yellow}%1~%f %# '
RPROMPT='[%F{yellow}%?%f]'

```

And here's how it will be displayed:

```
username@host ~ %                                                         [0]

```

### Sample .zshrc files

*   A package in offical repository named [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config) comes from [https://grml.org/zsh](https://grml.org/zsh) and provides a zshrc file that includes many tweaks for Zshell. This is the default configuration for the [monthly ISO releases](https://www.archlinux.org/download/).
*   [https://github.com/MrElendig/dotfiles-alice/blob/master/.zshrc](https://github.com/MrElendig/dotfiles-alice/blob/master/.zshrc) - basic setup, with dynamic prompt and window title/hardinfo.
*   [https://github.com/slashbeast/things/blob/master/configs/DOTzshrc](https://github.com/slashbeast/things/blob/master/configs/DOTzshrc) - zshrc with multiple features, be sure to check out comments into it. Notable features: confirm function to ensure that user want to run poweroff, reboot or hibernate, support for GIT in prompt (done without vcsinfo), tab completion with menu, printing current executed command into window's title bar and more.

See [dotfiles#Repositories](/index.php/Dotfiles#Repositories "Dotfiles") for more.

### Configuration Frameworks

*   **Antigen** — A plugin manager for zsh, inspired by oh-my-zsh and vundle.

	[https://github.com/zsh-users/antigen](https://github.com/zsh-users/antigen) || [antigen-git](https://aur.archlinux.org/packages/antigen-git/)

*   **oh-my-zsh** — A popular, community-driven framework for managing your Zsh configuration. It comes bundled with a ton of helpful functions, helpers, plugins, themes.

	[https://github.com/robbyrussell/oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) || [oh-my-zsh-git](https://aur.archlinux.org/packages/oh-my-zsh-git/)

**Note:** For themes to work you may need to set `setopt NO_GLOBAL_RCS` in the `~/.zshenv` file, otherwise changes to some variables (such as `$PROMPT`) may be overwritten.

*   **Prezto** — A configuration framework for Zsh. It comes with modules, enriching the command line interface environment with sane defaults, aliases, functions, auto completion, and prompt themes.

	[https://github.com/sorin-ionescu/prezto](https://github.com/sorin-ionescu/prezto) || [prezto-git](https://aur.archlinux.org/packages/prezto-git/)

## Tips and tricks

### Autostart X at login

See [Xinitrc#Autostart X at login](/index.php/Xinitrc#Autostart_X_at_login "Xinitrc").

### The "command not found" hook

[pkgfile](/index.php/Pkgfile "Pkgfile") includes a "command not found" hook that will automatically search the official repositories, when entering an unrecognized command.

You need to [source](/index.php/Source "Source") the hook to enable it, for example:

 `~/.zshrc` 
```
source /usr/share/doc/pkgfile/command-not-found.zsh

```

### The ttyctl command

[[1]](http://zsh.sourceforge.net/Doc/Release/Shell-Builtin-Commands.html#index-tty_002c-freezing) describes the `ttyctl` command in Zsh. This may be used to "freeze/unfreeze" the terminal. Many programs change the terminal state, and often do not restore terminal settings on exiting abnormally. To avoid the need to manually reset the terminal, use the following:

 `~/.zshrc` 
```
ttyctl -f

```

### Remembering recent directories

#### Dirstack

Zsh can be configured to remember the DIRSTACKSIZE last visited folders. This can then be used to *cd* them very quickly. You need to add some lines to your configuration file:

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

setopt AUTO_PUSHD PUSHD_SILENT PUSHD_TO_HOME

## Remove duplicate entries
setopt PUSHD_IGNORE_DUPS

## This reverts the +/- operators.
setopt PUSHD_MINUS

```

Now use

```
$ dirs -v

```

to print the dirstack. Use `cd -<NUM>` to go back to a visited folder. Use autocompletion after the dash. This proves very handy if using the autocompletion menu.

**Note:** This will not work if you have more than one *zsh* session open, and attempt to `cd`, due to a conflict in both sessions writing to the same file.

#### cdr

cdr allows you to change the working directory to a previous working directory from a list maintained automatically. It stores all entries in files that are maintained across sessions and (by default) between terminal emulators in the current session.

See [Remembering Recent Directories](http://zsh.sourceforge.net/Doc/Release/User-Contributions.html#Recent-Directories) in zshcontrib(1).

### Help command

Zsh `help` command is called `run-help`. Unlike [bash](/index.php/Bash "Bash"), *zsh* does not enable it by default. To use `help` in zsh, add following to your `zshrc`:

```
autoload -Uz run-help
unalias run-help
alias help=run-help
```

`run-help` will invoke *man* for external commands. Default keyboard shortcut is `Alt+h` or `Esc+h`.

`run-help` has helper functions, they need to be enabled separately:

```
autoload -Uz run-help-git
autoload -Uz run-help-ip
autoload -Uz run-help-openssl
autoload -Uz run-help-p4
autoload -Uz run-help-sudo
autoload -Uz run-help-svk
autoload -Uz run-help-svn
```

For example `run-help git commit` command will now open the man page [git-commit(1)](http://man7.org/linux/man-pages/man1/git-commit.1.html) instead of [git(1)](http://man7.org/linux/man-pages/man1/git.1.html).

### Fish-like syntax highlighting

[Fish](/index.php/Fish "Fish") provides a very powerful shell syntax highlighting. To use this in zsh, you can install [zsh-syntax-highlighting](https://www.archlinux.org/packages/?name=zsh-syntax-highlighting) from offical repository and add following to your zshrc:

```
source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

```

### Persistent rehash

Typically, compinit will not automatically find new executables in the `$PATH`. For example, after you install a new package, the files in /usr/bin would not be immediately or automatically included in the completion. Thus, to have these new exectuables included, one would run:

```
$ rehash

```

This 'rehash' can be set to happen automatically. Simply include the following in your `zshrc`:

 `~/.zshrc` 
```
zstyle ':completion:*' rehash true

```

**Note:** This hack has been found in a [PR for Oh My Zsh](https://github.com/robbyrussell/oh-my-zsh/issues/3440).

### Bind key to ncurses application

Bind a ncurses application to a keystoke, but it will not accept interaction. Use `BUFFER` variable to make it work. The following example lets users open ncmpcpp using `Alt+\`:

 `~/.zshrc` 
```
ncmpcppShow() { BUFFER="ncmpcpp"; zle accept-line; }
zle -N ncmpcppShow
bindkey '^[\' ncmpcppShow
```

An alternate method, that will keep everything you entered in the line before calling application:

 `~/.zshrc` 
```
ncmpcppShow() { ncmpcpp <$TTY; zle redisplay; }
zle -N ncmpcppShow
bindkey '^[\' ncmpcppShow
```

### File manager key binds

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

### xterm title

xterm title is set with [xterm escape sequences](http://tldp.org/HOWTO/Xterm-Title-3.html#ss3.1). For example:

```
print -n '\e]2;My xterm title\a'

```

will set the title to

```
My xterm title

```

An simple way to have a dynamic title is to set the title in a [hook function](http://zsh.sourceforge.net/Doc/Release/Functions.html#Hook-Functions), particularly `precmd` and `preexec`.

By using `print -P` you can take advantage of prompt escapes. Title printing can be split up in multiple commands as long as they are sequential.

 `~/.zshrc` 
```
autoload -Uz add-zsh-hook

function xterm_title_precmd () {
	print -Pn '\e]2;%n@%m %1~\a'
}

function xterm_title_preexec () {
	print -Pn '\e]2;%n@%m %1~ %# '
	print -n "${(q)1}\a"
}

if [[ "$TERM" == (screen*|xterm*|rxvt*) ]]; then
	add-zsh-hook -Uz precmd xterm_title_precmd
	add-zsh-hook -Uz preexec xterm_title_preexec
fi

```

**Warning:**

*   Do not use `-P` option of `print` when printing variables to prevent them from being parsed as prompt escapes.
*   Use `q` [parameter expansion flag](http://zsh.sourceforge.net/Doc/Release/Expansion.html#Parameter-Expansion-Flags) when printing variables to prevent them from being parsed as escape sequences.

## Uninstallation

Change the default shell before removing the [zsh](https://www.archlinux.org/packages/?name=zsh) package.

**Warning:** Failure to follow the below procedure may result in users no longer having access to a working shell.

Run following command:

```
$ chsh -s /bin/bash *user*

```

Use it for every user with *zsh* set as their login shell (including root if needed). When completed, the [zsh](https://www.archlinux.org/packages/?name=zsh) package can be removed.

Alternatively, change the default shell back to Bash by editing `/etc/passwd` as root.

**Warning:** It is strongly recommended to use `vipw` when editing `/etc/passwd` as it helps prevent invalid entries and/or syntax errors.

For example, change the following:

```
*username*:x:1000:1000:*Full Name*,,,:/home/*username*:/bin/zsh

```

To this:

```
*username*:x:1000:1000:*Full Name*,,,:/home/*username*:/bin/bash

```

## See also

*   [A User's Guide to ZSH](http://zsh.sourceforge.net/Guide/zshguide.html)
*   [The Z Shell Manual](http://zsh.sourceforge.net/Doc/Release/index-frame.html) (different format available [here](http://zsh.sourceforge.net/Doc/))
*   [Zsh FAQ](http://zsh.sourceforge.net/FAQ/zshfaq01.html)
*   [zsh-lovers(1)](https://grml.org/zsh/zsh-lovers.html) (available as [zsh-lovers](https://www.archlinux.org/packages/?name=zsh-lovers) package)
*   [Zsh Wiki](http://zshwiki.org/home/)
*   [Gentoo: Zsh/Guide](https://wiki.gentoo.org/wiki/Zsh/Guide "gentoo:Zsh/Guide")
*   [Bash2Zsh Reference Card](http://www.bash2zsh.com/zsh_refcard/refcard.pdf)