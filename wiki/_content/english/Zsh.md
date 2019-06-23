[Zsh](http://zsh.sourceforge.net/Intro/intro_1.html) is a powerful [shell](/index.php/Shell "Shell") that operates as both an interactive shell and as a scripting language interpreter. While being compatible with the Bourne shell (not by default, only if issuing `emulate sh`), it offers advantages such as improved [tab completion](http://zsh.sourceforge.net/Guide/zshguide06.html) and [globbing](http://zsh.sourceforge.net/Doc/Release/Expansion.html).

The [Zsh FAQ](http://zsh.sourceforge.net/FAQ/zshfaq01.html#l4) offers more reasons to use Zsh.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Initial configuration](#Initial_configuration)
    *   [1.2 Making Zsh your default shell](#Making_Zsh_your_default_shell)
*   [2 Startup/Shutdown files](#Startup/Shutdown_files)
*   [3 Configure Zsh](#Configure_Zsh)
    *   [3.1 Simple .zshrc](#Simple_.zshrc)
    *   [3.2 Configuring $PATH](#Configuring_$PATH)
    *   [3.3 Command completion](#Command_completion)
    *   [3.4 Key bindings](#Key_bindings)
    *   [3.5 History search](#History_search)
    *   [3.6 Prompts](#Prompts)
        *   [3.6.1 Prompt themes](#Prompt_themes)
            *   [3.6.1.1 Manually installing prompt themes](#Manually_installing_prompt_themes)
        *   [3.6.2 Customized prompt](#Customized_prompt)
            *   [3.6.2.1 Colors](#Colors)
            *   [3.6.2.2 Example](#Example)
    *   [3.7 Sample .zshrc files](#Sample_.zshrc_files)
    *   [3.8 Configuration Frameworks](#Configuration_Frameworks)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Autostart X at login](#Autostart_X_at_login)
    *   [4.2 The "command not found" hook](#The_"command_not_found"_hook)
    *   [4.3 The ttyctl command](#The_ttyctl_command)
    *   [4.4 Remembering recent directories](#Remembering_recent_directories)
        *   [4.4.1 Dirstack](#Dirstack)
        *   [4.4.2 cdr](#cdr)
    *   [4.5 Help command](#Help_command)
    *   [4.6 Fish-like syntax highlighting](#Fish-like_syntax_highlighting)
    *   [4.7 Persistent rehash](#Persistent_rehash)
        *   [4.7.1 On-demand rehash](#On-demand_rehash)
        *   [4.7.2 Alternative on-demand rehash using SIGUSR1](#Alternative_on-demand_rehash_using_SIGUSR1)
    *   [4.8 Bind key to ncurses application](#Bind_key_to_ncurses_application)
    *   [4.9 File manager key binds](#File_manager_key_binds)
    *   [4.10 xterm title](#xterm_title)
        *   [4.10.1 Terminal emulator tab title](#Terminal_emulator_tab_title)
    *   [4.11 Shell environment detection](#Shell_environment_detection)
*   [5 Uninstallation](#Uninstallation)
*   [6 See also](#See_also)

## Installation

Before starting, users may want to see what shell is currently being used:

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

**Note:** Make sure your terminal's size is at least 72×15 otherwise *zsh-newuser-install* will not run.

### Making Zsh your default shell

See [Command-line shell#Changing your default shell](/index.php/Command-line_shell#Changing_your_default_shell "Command-line shell").

**Tip:** If replacing [bash](https://www.archlinux.org/packages/?name=bash), users may want to move some code from `~/.bashrc` to `~/.zshrc` (e.g. the prompt and the [aliases](/index.php/Bash#Aliases "Bash")) and from `~/.bash_profile` to `~/.zprofile` (e.g. [the code that starts the X Window System](/index.php/Xinit#Autostart_X_at_login "Xinit")).

## Startup/Shutdown files

**Tip:** See [A User's Guide to the Z-Shell](http://zsh.sourceforge.net/Guide/zshguide02.html) for explanation on interactive and login shells, and what to put in your startup files.

**Note:**

*   If `$ZDOTDIR` is not set, `$HOME` is used instead.
*   If option `RCS` is unset in any of the files, no configuration files will be sourced after that file.
*   If option `GLOBAL_RCS` is unset in any of the files, no global configuration files (`/etc/zsh/*`) will be sourced after that file.

When starting Zsh, it will source the following files in this order by default:

*   `/etc/zsh/zshenv` Used for setting system-wide [environment variables](/index.php/Environment_variables "Environment variables"); it should not contain commands that produce output or assume the shell is attached to a tty. This file will ***always*** be sourced, this cannot be overridden.
*   `$ZDOTDIR/.zshenv` Used for setting user's environment variables; it should not contain commands that produce output or assume the shell is attached to a tty. This file will ***always*** be sourced.
*   `/etc/zsh/zprofile` Used for executing commands at start, will be sourced when starting as a ***login shell***. Please note that on Arch Linux, by default it contains [one line](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/zprofile?h=packages/zsh) which source the `/etc/profile`.
    *   `/etc/profile` This file should be sourced by all Bourne-compatible shells upon login: it sets up `$PATH` and other environment variables and application-specific (`/etc/profile.d/*.sh`) settings upon login.
*   `$ZDOTDIR/.zprofile` Used for executing user's commands at start, will be sourced when starting as a ***login shell***.
    *   `$HOME/.profile` is **not** sourced by zsh.
*   `/etc/zsh/zshrc` Used for setting interactive shell configuration and executing commands, will be sourced when starting as an ***interactive shell***.
*   `$ZDOTDIR/.zshrc` Used for setting user's interactive shell configuration and executing commands, will be sourced when starting as an ***interactive shell***.
*   `/etc/zsh/zlogin` Used for executing commands at ending of initial progress, will be sourced when starting as a ***login shell***.
*   `$ZDOTDIR/.zlogin` Used for executing user's commands at ending of initial progress, will be sourced when starting as a ***login shell***.
*   `$ZDOTDIR/.zlogout` Will be sourced when a ***login shell*** **exits**.
*   `/etc/zsh/zlogout` Will be sourced when a ***login shell*** **exits**.

**Note:** The paths used in Arch's [zsh](https://www.archlinux.org/packages/?name=zsh) package are different from the default ones used in the [man pages](/index.php/Man_page "Man page") ([FS#48992](https://bugs.archlinux.org/task/48992)).

**Warning:** It is not recommended to replace the default [one line](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/zprofile?h=packages/zsh) in `/etc/zsh/zprofile` with something else, otherwise it will break the integrity of other packages which provide some scripts in `/etc/profile.d/`.

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

See [A User's Guide to the Z-Shell](http://zsh.sourceforge.net/Guide/zshguide02.html#l24) and also the note in [#Startup/Shutdown files](#Startup/Shutdown_files) for details.

The incantation `typeset -U path`, where the `-U` stands for unique, tells the shell that it should not add anything to `$PATH` if it is there already:

 `~/.zshenv` 
```
typeset -U path
path=(*~/.local/bin* */other/things/in/path* $path[@])
```

### Command completion

Perhaps the most compelling feature of Zsh is its advanced autocompletion abilities. At the very least, enable autocompletion in `.zshrc`. To enable autocompletion, add the following to your `~/.zshrc`:

 `~/.zshrc` 
```
autoload -Uz compinit
compinit

```

The above configuration includes ssh/scp/sftp hostnames completion but in order for this feature to work, users must not enable ssh's hostname hashing (i.e. option `HashKnownHosts` in ssh client configuration).

For autocompletion with an arrow-key driven interface, add the following to:

 `~/.zshrc` 
```
zstyle ':completion:*' menu select

```

To activate the menu, press `Tab` twice.

For autocompletion of command line switches for aliases, add the following to:

 `~/.zshrc` 
```
setopt COMPLETE_ALIASES

```

For enabling autocompletion of privileged environments in privileged commands (e.g. if you complete a command starting with [sudo](/index.php/Sudo "Sudo"), completion scripts will also try to determine your completions with sudo), include:

 `~/.zshrc` 
```
zstyle ':completion::complete:*' gain-privileges 1

```

**Warning:** This will let zsh completion scripts run commands with sudo privileges. You should not enable this if you use untrusted autocompletion scripts.

**Note:** This special kind of context-aware completion is only available for a small number of commands.

### Key bindings

Zsh does not use [readline](/index.php/Readline "Readline"), instead it uses its own and more powerful Zsh Line Editor (ZLE). It does not read `/etc/inputrc` or `~/.inputrc`.

ZLE has an [emacs](/index.php/Emacs "Emacs") mode and a [vi](/index.php/Vi "Vi") mode. If one of the `$VISUAL` or `$EDITOR` [environment variables](/index.php/Environment_variables "Environment variables") contain the string `vi` then vi mode will be used; otherwise, it will default to emacs mode. Set the mode explicitly with `bindkey -e` or `bindkey -v` respectively for emacs mode or vi mode.

Add the following to your `~/.zshrc` to set up key bindings using key sequences from [terminfo(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/terminfo.5):

 `~/.zshrc` 
```
# create a zkbd compatible hash;
# to add other keys to this hash, see: man 5 terminfo
typeset -g -A key

key[Home]="${terminfo[khome]}"
key[End]="${terminfo[kend]}"
key[Insert]="${terminfo[kich1]}"
key[Backspace]="${terminfo[kbs]}"
key[Delete]="${terminfo[kdch1]}"
key[Up]="${terminfo[kcuu1]}"
key[Down]="${terminfo[kcud1]}"
key[Left]="${terminfo[kcub1]}"
key[Right]="${terminfo[kcuf1]}"
key[PageUp]="${terminfo[kpp]}"
key[PageDown]="${terminfo[knp]}"
key[ShiftTab]="${terminfo[kcbt]}"

# setup key accordingly
[[ -n "${key[Home]}"      ]] && bindkey -- "${key[Home]}"      beginning-of-line
[[ -n "${key[End]}"       ]] && bindkey -- "${key[End]}"       end-of-line
[[ -n "${key[Insert]}"    ]] && bindkey -- "${key[Insert]}"    overwrite-mode
[[ -n "${key[Backspace]}" ]] && bindkey -- "${key[Backspace]}" backward-delete-char
[[ -n "${key[Delete]}"    ]] && bindkey -- "${key[Delete]}"    delete-char
[[ -n "${key[Up]}"        ]] && bindkey -- "${key[Up]}"        up-line-or-history
[[ -n "${key[Down]}"      ]] && bindkey -- "${key[Down]}"      down-line-or-history
[[ -n "${key[Left]}"      ]] && bindkey -- "${key[Left]}"      backward-char
[[ -n "${key[Right]}"     ]] && bindkey -- "${key[Right]}"     forward-char
[[ -n "${key[PageUp]}"    ]] && bindkey -- "${key[PageUp]}"    beginning-of-buffer-or-history
[[ -n "${key[PageDown]}"  ]] && bindkey -- "${key[PageDown]}"  end-of-buffer-or-history
[[ -n "${key[ShiftTab]}"  ]] && bindkey -- "${key[ShiftTab]}"  reverse-menu-complete

# Finally, make sure the terminal is in application mode, when zle is
# active. Only then are the values from $terminfo valid.
if (( ${+terminfo[smkx]} && ${+terminfo[rmkx]} )); then
	autoload -Uz add-zle-hook-widget
	function zle_application_mode_start {
		echoti smkx
	}
	function zle_application_mode_stop {
		echoti rmkx
	}
	add-zle-hook-widget -Uz zle-line-init zle_application_mode_start
	add-zle-hook-widget -Uz zle-line-finish zle_application_mode_stop
fi
```

See [ZshWiki:Keybindings](http://zshwiki.org/home/keybindings/) for more information.

### History search

You need to set up [#Key bindings](#Key_bindings) to use this. To enable history search add these lines to `.zshrc` file:

 `~/.zshrc` 
```
autoload -Uz up-line-or-beginning-search down-line-or-beginning-search
zle -N up-line-or-beginning-search
zle -N down-line-or-beginning-search

[[ -n "${key[Up]}"   ]] && bindkey -- "${key[Up]}"   up-line-or-beginning-search
[[ -n "${key[Down]}" ]] && bindkey -- "${key[Down]}" down-line-or-beginning-search

```

By doing this, only the past commands matching the current line up to the current cursor position will be shown when `Up` or `Down` keys are pressed.

### Prompts

Zsh offers the options of using a prompt theme or, for users who are dissatisfied with the themes (or want to expand their usefulness), the possibility to build a custom prompt.

#### Prompt themes

Prompt themes are a quick and easy way to set up a colored prompt in Zsh. See [zshcontrib(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zshcontrib.1#PROMPT_THEMES) for more information about them.

To use a theme, make sure that prompt theme system is set to autoload in `.zshrc`. This can be done by adding these lines to:

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

##### Manually installing prompt themes

It is possible to install themes manually, without external configuration manager tools. For a local installation, first create a folder and add it to the `fpath` array, eg:

```
$ mkdir ~/.zprompts && fpath=( "$HOME/.zprompts" $fpath )

```

Now create a symbolic link of your theme file in this folder:

```
$ ln -s mytheme.zsh ~/.zprompts/prompt_mytheme_setup

```

If instead you wish to install a theme globally, do:

```
# ln -s mytheme.zsh /usr/share/zsh/functions/Prompts/prompt_mytheme_setup

```

Now you should be able to activate it using:

```
$ prompt mytheme

```

If everything works, you can edit your `.zshrc` accordingly.

#### Customized prompt

Additionally to a primary left-sided prompt `PS1` (`PROMPT`, `prompt`) that is common to all shells, Zsh also supports a right-sided prompt `RPS1` (`RPROMPT`). These two variables are the ones you will want to set to a custom value.

Other special purpose prompts, such as `PS2` (`PROMPT2`), `PS3` (`PROMPT3`), `PS4` (`PROMPT4`), `RPS1` (`RPROMPT`), `RPS2` (`RPROMPT2`) and `SPROMPT`, are explained in [zshparam(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zshparam.1#PARAMETERS_USED_BY_THE_SHELL).

All prompts can be customized with prompt escapes. The available prompt escapes are listed in [zshmisc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zshmisc.1#EXPANSION_OF_PROMPT_SEQUENCES).

##### Colors

Zsh sets colors differently than [Bash](/index.php/Bash/Prompt_customization "Bash/Prompt customization"), you do not need to use ANSI escape sequences. Zsh provides convenient prompt escapes to set the foreground color, background color and other visual effects; see [zshmisc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zshmisc.1#Visual_effects) for a list of them.

[Colors](http://zsh.sourceforge.net/FAQ/zshfaq03.html#l42) can be specified using a decimal integer, the name of one of the eight most widely-supported colors or as a # followed by an RGB triplet in hexadecimal format. See the description of fg=colour in [zshzle(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zshzle.1#CHARACTER_HIGHLIGHTING) for more details.

Most terminals support the following colors by name:

| Name | Number |
| `black` | `0` |
| `red` | `1` |
| `green` | `2` |
| `yellow` | `3` |
| `blue` | `4` |
| `magenta` | `5` |
| `cyan` | `6` |
| `white` | `7` |

Color numbers 0–255 for terminal emulators compatible with xterm 256 colors can be found in the [xterm-256color chart](https://upload.wikimedia.org/wikipedia/commons/1/15/Xterm_256color_chart.svg).

With a correctly set TERM environment variable, the terminal's supported maximum number of colors can be found from the [terminfo(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/terminfo.5) database using `echoti colors`. In the case of 24-bit colors, also check the COLORTERM environment variable with `echo $COLORTERM`. If it returns `24bit` or `truecolor` then your terminal supports 16777216 (2) colors even if terminfo shows a smaller number.

**Note:**

*   The colors 0–15 may differ between terminal emulators and their used color schemes.
*   Many terminal emulators display bold with a brighter color.

**Tip:**

*   Prompt escapes can be tested with command `print -P *"prompt escapes"*`, for example: `$ print -P '%B%F{red}co%F{green}lo%F{blue}rs%f%b'` 
*   If you use 24-bit colors, you might want to load the `zsh/nearcolor` module in terminals that do not support them. E.g.: `[[ "$COLORTERM" == (24bit|truecolor) || "${terminfo[colors]}" -eq '16777216' ]] || zmodload zsh/nearcolor` See [zshmodules(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zshmodules.1#THE_ZSH%2FNEARCOLOR_MODULE) for details about the `zsh/nearcolor` module.

##### Example

This is an example of a two-sided prompt:

```
PROMPT='%F{green}%n%f@%F{magenta}%m%f %F{blue}%B%~%b%f %# '
RPROMPT='[%F{yellow}%?%f]'

```

And here is how it will be displayed:

username@host ~ % [0]

### Sample .zshrc files

*   To get the same setup as the [monthly ISO releases](https://www.archlinux.org/download/) (which use Zsh by default), install [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config). It includes the many tweaks and advanced optimizations from [grml](https://grml.org/zsh/).
*   [https://github.com/MrElendig/dotfiles-alice/blob/master/.zshrc](https://github.com/MrElendig/dotfiles-alice/blob/master/.zshrc) - basic setup, with dynamic prompt and window title/hardinfo.
*   [https://github.com/slashbeast/conf-mgmt/blob/master/roles/home_files/files/DOTzshrc](https://github.com/slashbeast/conf-mgmt/blob/master/roles/home_files/files/DOTzshrc) - zshrc with multiple features, be sure to check out comments into it. Notable features: confirm function to ensure that user want to run poweroff, reboot or hibernate, support for GIT in prompt (done without vcsinfo), tab completion with menu, printing current executed command into window's title bar and more.

See [dotfiles#User repositories](/index.php/Dotfiles#User_repositories "Dotfiles") for more.

### Configuration Frameworks

*   **Antigen** — A plugin manager for zsh, inspired by oh-my-zsh and vundle.

	[https://github.com/zsh-users/antigen](https://github.com/zsh-users/antigen) || [antigen-git](https://aur.archlinux.org/packages/antigen-git/)

*   **Antibody** — A performance-focused plugin manager similar to Antigen.

	[https://github.com/getantibody/antibody](https://github.com/getantibody/antibody) || [antibody](https://aur.archlinux.org/packages/antibody/)

*   **oh-my-zsh** — A popular, community-driven framework for managing your Zsh configuration. It comes bundled with a ton of helpful functions, helpers, plugins, themes.

	[https://github.com/robbyrussell/oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) || [oh-my-zsh-git](https://aur.archlinux.org/packages/oh-my-zsh-git/)

*   **Prezto** — A configuration framework for Zsh. It comes with modules, enriching the command line interface environment with sane defaults, aliases, functions, auto completion, and prompt themes.

	[https://github.com/sorin-ionescu/prezto](https://github.com/sorin-ionescu/prezto) || [prezto-git](https://aur.archlinux.org/packages/prezto-git/)

*   **ZIM** — A configuration framework with blazing speed and modular extensions. Zim is very easy to customize, and comes with a rich set of modules and features without compromising on speed or functionality.

	[https://github.com/zimfw/zimfw](https://github.com/zimfw/zimfw) || [zsh-zim-git](https://aur.archlinux.org/packages/zsh-zim-git/)

## Tips and tricks

### Autostart X at login

See [xinit#Autostart X at login](/index.php/Xinit#Autostart_X_at_login "Xinit").

### The "command not found" hook

[pkgfile](/index.php/Pkgfile "Pkgfile") includes a "command not found" hook that will automatically search the official repositories, when entering an unrecognized command.

You need to [source](/index.php/Source "Source") the hook to enable it, for example:

 `~/.zshrc` 
```
source /usr/share/doc/pkgfile/command-not-found.zsh

```

**Note:** The pkgfile database may need to be updated before this will work. See [pkgfile#Installation](/index.php/Pkgfile#Installation "Pkgfile") for details.

### The ttyctl command

The [ttyctl](http://zsh.sourceforge.net/Doc/Release/Shell-Builtin-Commands.html#index-tty_002c-freezing) command can be used to "freeze/unfreeze" the terminal. Many programs change the terminal state, and often do not restore terminal settings on exiting abnormally. To avoid the need to manually reset the terminal, use the following:

 `~/.zshrc` 
```
ttyctl -f

```

### Remembering recent directories

#### Dirstack

Zsh can be configured to remember the DIRSTACKSIZE last visited folders. This can then be used to *cd* them very quickly. You need to add some lines to your configuration file:

 `~/.zshrc` 
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

See [zshcontrib(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zshcontrib.1#REMEMBERING_RECENT_DIRECTORIES).

### Help command

Zsh `help` command is called `run-help`. Unlike [bash](/index.php/Bash "Bash"), *zsh* does not enable it by default. To use `help` in zsh, add following to your `zshrc`:

```
autoload -Uz run-help
unalias run-help
alias help=run-help
```

`run-help` will invoke *man* for external commands. Default keyboard shortcut is `Alt+h` or `Esc+h`.

`run-help` has assistant functions, they need to be enabled separately:

```
autoload -Uz run-help-git
autoload -Uz run-help-ip
autoload -Uz run-help-openssl
autoload -Uz run-help-p4
autoload -Uz run-help-sudo
autoload -Uz run-help-svk
autoload -Uz run-help-svn
```

For example `run-help git commit` command will now open the [man page](/index.php/Man_page "Man page") [git-commit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-commit.1) instead of [git(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git.1).

### Fish-like syntax highlighting

[Fish](/index.php/Fish "Fish") provides a very powerful shell syntax highlighting. To use this in zsh, you can install [zsh-syntax-highlighting](https://www.archlinux.org/packages/?name=zsh-syntax-highlighting) from offical repository and add following to your zshrc:

```
source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

```

### Persistent rehash

Typically, compinit will not automatically find new executables in the `$PATH`. For example, after you install a new package, the files in `/usr/bin/` would not be immediately or automatically included in the completion. Thus, to have these new executables included, one would run:

```
$ rehash

```

This 'rehash' can be set to happen automatically.[[2]](https://github.com/robbyrussell/oh-my-zsh/issues/3440) Simply include the following in your `zshrc`:

 `~/.zshrc` 
```
zstyle ':completion:*' rehash true

```

#### On-demand rehash

As above, however [pacman](/index.php/Pacman "Pacman") can be configured with [hooks](/index.php/Pacman#Hooks "Pacman") to automatically request a `rehash`, which does not incur the performance penalty of constant rehashing as above. To enable this, create the `/etc/pacman.d/hooks` directory, and a `/var/cache/zsh` directory, then create a hook file:

 `/etc/pacman.d/hooks/zsh.hook` 
```
[Trigger]
Operation = Install
Operation = Upgrade
Operation = Remove
Type = Package
Target = *
[Action]
Depends = zsh
When = PostTransaction
Exec = /usr/bin/env touch /var/cache/zsh/pacman
```

This keeps the modification date of the file `/var/cache/zsh/pacman` consistent with the last time a package was installed, upgraded or removed. Then, `zsh` must be coaxed into rehashing its own command cache when it goes out of date, by adding to your `~/.zshrc`:

 `~/.zshrc` 
```
zshcache_time="$(date +%s%N)"

autoload -Uz add-zsh-hook

rehash_precmd() {
  if [[ -a /var/cache/zsh/pacman ]]; then
    local paccache_time="$(date -r /var/cache/zsh/pacman +%s%N)"
    if (( zshcache_time < paccache_time )); then
      rehash
      zshcache_time="$paccache_time"
    fi
  fi
}

add-zsh-hook -Uz precmd rehash_precmd

```

If the `precmd` hook is triggered before `/var/cache/zsh/pacman` is updated, completion may not work until a new prompt is initiated. Running an empty command, e.g. pressing `enter`, should be sufficient.

#### Alternative on-demand rehash using SIGUSR1

As above, however the hook file looks like this:

 `/etc/pacman.d/hooks/zsh-rehash.hook` 
```
[Trigger]
Operation = Install
Operation = Upgrade
Operation = Remove
Type = Package
Target = *

[Action]
Depends = zsh
Depends = procps-ng
When = PostTransaction
Exec = /usr/bin/pkill zsh --signal=USR1
```

**Warning:** This sends SIGUSR1 to all running `zsh` instances. Note that the default behavior for SIGUSR1 is terminate so when you first configure this all running `zsh` instances of all users (including login shells) will terminate if they have not sourced the trap below.
 `~/.zshrc` 
```
catch_signal_usr1() {
  trap catch_signal_usr1 USR1
  rehash
}
trap catch_signal_usr1 USR1

```

This method will instantly `rehash` all `zsh` instances, removing the need to press enter to trigger `precmd`.

### Bind key to ncurses application

Bind a ncurses application to a keystroke, but it will not accept interaction. Use `BUFFER` variable to make it work. The following example lets users open ncmpcpp using `Alt+\`:

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
  popd
  zle       reset-prompt
  echo
  ls
  zle       reset-prompt
}

cdParentKey() {
  pushd ..
  zle      reset-prompt
  echo
  ls
  zle       reset-prompt
}

zle -N                 cdParentKey
zle -N                 cdUndoKey
bindkey '^[[1;3A'      cdParentKey
bindkey '^[[1;3D'      cdUndoKey

```

### xterm title

If your terminal emulator supports it you can set its title from Zsh. This allows dynamically changing the the title to display relevant information about the shell state, for example showing the user name and current directory or the currently executing command.

xterm title is set with the [xterm escape sequence](https://www.tldp.org/HOWTO/Xterm-Title-3.html#ss3.1) `\e]2;``\a`. For example:

```
$ print -n '\e]2;My xterm title\a'

```

will set the title to

```
My xterm title

```

An simple way to have a dynamic title is to set the title in a hook functions `precmd` and `preexec`. See [zshmisc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zshmisc.1#Hook_Functions).

By using `print -P` you can take advantage of prompt escapes.

**Tip:**

*   Title printing can be split up in multiple commands as long as they are sequential.
*   [GNU Screen](/index.php/GNU_Screen "GNU Screen") sends the xterm title to the hardstatus (`%h`). If you want to use Screen's [string escapes](https://www.gnu.org/software/screen/manual/html_node/String-Escapes.html) (e.g. for colors) you should set the hardstatus with the `\e_``\e\\` escape sequence. Otherwise, if string escapes are used in `\e]2;``\a`, the terminal emulator will get a garbled title due to it being incapable of interpreting them.

**Note:**

*   Do not use `-P` option of `print` when printing variables to prevent them from being parsed as prompt escapes.
*   Use `q` [parameter expansion flag](http://zsh.sourceforge.net/Doc/Release/Expansion.html#Parameter-Expansion-Flags) when printing variables to prevent them from being parsed as escape sequences.

 `~/.zshrc` 
```
autoload -Uz add-zsh-hook

function xterm_title_precmd () {
	print -Pn '\e]2;%n@%m %~\a'
	[[ "$TERM" == 'screen'* ]] && print -Pn '\e_\005{g}%n\005{-}@\005{m}%m\005{-} \005{B}%~\005{-}\e\\'
}

function xterm_title_preexec () {
	print -Pn '\e]2;%n@%m %~ %# ' && print -n "${(q)1}\a"
	[[ "$TERM" == 'screen'* ]] && { print -Pn '\e_\005{g}%n\005{-}@\005{m}%m\005{-} \005{B}%~\005{-} %# ' && print -n "${(q)1}\e\\"; }
}

if [[ "$TERM" == (screen*|xterm*|rxvt*) ]]; then
	add-zsh-hook -Uz precmd xterm_title_precmd
	add-zsh-hook -Uz preexec xterm_title_preexec
fi

```

#### Terminal emulator tab title

Some terminal emulators and multiplexers support setting the title of the tab. The escape sequences depend on the terminal:

| Terminal | Escape sequences | Description |
| [GNU Screen](/index.php/GNU_Screen "GNU Screen") | `\ek``\e\\` | Screen's window title (`%t`). |
| Konsole | `\e]30;``\a` | Konsole's tab title. |

### Shell environment detection

See [a repository about shell environment detection](https://gitlab.com/jdorel-documentation/shell-environment-detection) for tests to detect the shell environment. This includes login/interactive shell, Xorg session, TTY and SSH session.

## Uninstallation

Change the default shell before removing the [zsh](https://www.archlinux.org/packages/?name=zsh) package.

**Warning:** Failure to follow the below procedure may result in users no longer having access to a working shell.

Run following command:

```
$ chsh -s /bin/bash *user*

```

Use it for every user with *zsh* set as their login shell (including root if needed). When completed, the [zsh](https://www.archlinux.org/packages/?name=zsh) package can be removed.

Alternatively, change the default shell back to Bash by editing `/etc/passwd` as root.

**Warning:** It is strongly recommended to use [vipw(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vipw.8) when editing `/etc/passwd` as it helps prevent invalid entries and/or syntax errors.

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
*   [Zsh Wiki](http://zshwiki.org/home/)
*   [zsh-lovers(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/zsh-lovers.1) (available as [zsh-lovers](https://www.archlinux.org/packages/?name=zsh-lovers) package)
*   [Gentoo: Zsh/Guide](https://wiki.gentoo.org/wiki/Zsh/Guide "gentoo:Zsh/Guide")
*   [Bash2Zsh Reference Card](http://www.bash2zsh.com/zsh_refcard/refcard.pdf)