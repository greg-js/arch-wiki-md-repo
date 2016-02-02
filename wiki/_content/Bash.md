# Bash

Related articles

*   [Bash/Functions](/index.php/Bash/Functions "Bash/Functions")
*   [Environment variables](/index.php/Environment_variables "Environment variables")
*   [Readline](/index.php/Readline "Readline")
*   [Color Bash Prompt](/index.php/Color_Bash_Prompt "Color Bash Prompt")
*   [Fortune](/index.php/Fortune "Fortune")
*   [Pkgfile](/index.php/Pkgfile "Pkgfile")

**Bash** (Bourne-again Shell) is a [command-line shell](/index.php/Command-line_shell "Command-line shell")/programming language by the [GNU Project](/index.php/GNU_Project "GNU Project"). Its name is a homaging reference to its predecessor: the long-deprecated Bourne shell. Bash can be run on most UNIX-like operating systems, including GNU/Linux.

## Contents

*   [1 Invocation](#Invocation)
    *   [1.1 Configuration files](#Configuration_files)
    *   [1.2 Shell and environment variables](#Shell_and_environment_variables)
*   [2 Command line](#Command_line)
    *   [2.1 Tab completion](#Tab_completion)
        *   [2.1.1 Single-tab ability](#Single-tab_ability)
        *   [2.1.2 Additional programs and options](#Additional_programs_and_options)
        *   [2.1.3 Additional programs and options manually](#Additional_programs_and_options_manually)
    *   [2.2 History completion](#History_completion)
    *   [2.3 Fast word movement with Ctrl](#Fast_word_movement_with_Ctrl)
    *   [2.4 Mimic Zsh run-help ability](#Mimic_Zsh_run-help_ability)
*   [3 Aliases](#Aliases)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Prompt customization](#Prompt_customization)
        *   [4.1.1 Customize title](#Customize_title)
    *   [4.2 Command-not-found (AUR)](#Command-not-found_.28AUR.29)
    *   [4.3 Disable Ctrl+z in terminal](#Disable_Ctrl.2Bz_in_terminal)
    *   [4.4 Clear the screen after logging out](#Clear_the_screen_after_logging_out)
    *   [4.5 Auto "cd" when entering just a path](#Auto_.22cd.22_when_entering_just_a_path)
    *   [4.6 Autojump](#Autojump)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Line wrap on window resize](#Line_wrap_on_window_resize)
    *   [5.2 Shell exits even if ignoreeof set](#Shell_exits_even_if_ignoreeof_set)
*   [6 See also](#See_also)
    *   [6.1 Tutorials](#Tutorials)
    *   [6.2 Community](#Community)
    *   [6.3 Examples](#Examples)

## Invocation

Bash behaviour can be altered depending on how it is invoked. Some descriptions of different modes follow.

If Bash is spawned by `login` in a TTY, by an [SSH](/index.php/SSH "SSH") daemon, or similar means, it is considered a **login shell**. This mode can also be engaged using the `-l`/`--login` command line option.

Bash is considered an **interactive shell** when its standard input and error are connected to a terminal (for example, when run in a terminal emulator), and it is not started with the `-c` option or [non-option](http://unix.stackexchange.com/a/96805) arguments (for example, `bash **script**`). All interactive shells source `/etc/bash.bashrc` and `~/.bashrc`, while interactive _login_ shells also source `/etc/profile` and `~/.bash_profile`.

**Note:** In Arch `/bin/sh` (which used to be the Bourne shell executable) is symlinked to `/bin/bash`. If Bash is invoked with the name `sh`, it tries to mimic the startup behavior of historical versions of `sh`, including POSIX compability.

### Configuration files

See [6.2 Bash Startup Files](http://www.gnu.org/software/bash/manual/bash.html#Bash-Startup-Files) and [DotFiles](http://mywiki.wooledge.org/DotFiles) for a complete description.

| File | Description | Login shells <sup>(see note)</sup> | Interactive, _non-login_ shells |
| `/etc/profile` | [Sources](/index.php/Source "Source") application settings in `/etc/profile.d/*.sh` and `/etc/bash.bashrc`. | Yes | No |
| `~/.bash_profile` | Per-user, after `/etc/profile`. If this file does not exist, `~/.bash_login` and `~/.profile` are checked in that order. The skeleton file `/etc/skel/.bash_profile` also sources `~/.bashrc`. | Yes | No |
| `~/.bash_logout` | After exit of a login shell. | Yes | No |
| `/etc/bash.bashrc` | Depends on the `-DSYS_BASHRC="/etc/bash.bashrc"` compilation flag. Sources `/usr/share/bash-completion/bash_completion`. | No | Yes |
| `~/.bashrc` | Per-user, after `/etc/bash.bashrc`. | No | Yes |

**Note:**

*   Login shells can be non-interactive when called with the `--login` argument.
*   While interactive, _non-login_ shells do **not** source `~/.bash_profile`, they still inherit the environment from their parent process (which may be a login shell). See [On processes, environments and inheritance](http://mywiki.wooledge.org/ProcessManagement#On_processes.2C_environments_and_inheritance) for details.

### Shell and environment variables

The behavior of Bash and programs run by it can be influenced by a number of environment variables. [Environment variables](/index.php/Environment_variables "Environment variables") are used to store useful values such as command search directories, or which browser to use. When a new shell or script is launched it inherits its parent's variables, thus starting with an internal set of shell variables[[1]](http://www.kingcomputerservices.com/unix_101/understanding_unix_shells_and_environment_variables.htm).

These shell variables in Bash can be exported in order to become environment variables:

```
VARIABLE=content
export VARIABLE

```

or with a shortcut

```
export VARIABLE=content

```

Environment variables are conventionally placed in `~/.profile` or `/etc/profile` so that all bourne-compatible shells can use them.

See [Environment variables](/index.php/Environment_variables "Environment variables") for more general information.

## Command line

Bash command line is managed by the separate library called [Readline](/index.php/Readline "Readline"). Readline provides a lot of shortcuts for interacting with the command line i.e. moving back and forth on the word basis, deleting words etc. It is also Readline's responsibility to manage [history](/index.php/Readline#History "Readline") of input commands. Last, but not least, it allows you to create [macros](/index.php/Readline#Macros "Readline").

### Tab completion

[Tab completion](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion") is the option to auto-complete partial typed commands by pressing `Tab` twice (enabled by default).

#### Single-tab ability

For single press `Tab` results for when a partial or no completion is possible:

 `~/.inputrc` 

```
set show-all-if-ambiguous on

```

Alternatively, for results when no completion is possible:

 `~/.inputrc` 

```
set show-all-if-unmodified on

```

#### Additional programs and options

Bash has native support for tab completion of: commands, filenames, and variables. This functionality can be extended with the package [bash-completion](https://www.archlinux.org/packages/?name=bash-completion); it extends its functionality by adding a subset of tab completions to popular commands and their options. With [bash-completion](https://www.archlinux.org/packages/?name=bash-completion) know that normal completions (such as `$ ls file.*<tab><tab>`) will behave different; however, they can be re-enabled with `$ compopt -o bashdefault <prog>` (see [[2]](https://bbs.archlinux.org/viewtopic.php?id=128471) and [[3]](https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins.html) for more detail). Also for older systems [bash-completion](https://www.archlinux.org/packages/?name=bash-completion) may not be resourcefully convenient.

#### Additional programs and options manually

For basic completion use lines in the form of `complete -cf your_command` (these will conflict with the [bash-completion](https://www.archlinux.org/packages/?name=bash-completion) settings):

 `~/.bashrc` 

```
complete -cf sudo
complete -cf man

```

### History completion

History completion bound to arrow keys (down, up) (see: [Readline#History](/index.php/Readline#History "Readline") and [Readline Init File Syntax](https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax.html)):

 `~/.bashrc` 

```
 bind '"\e[A": history-search-backward'
 bind '"\e[B": history-search-forward'

```

or:

 `~/.inputrc` 

```
"\e[A": history-search-backward
"\e[B": history-search-forward

```

### Fast word movement with Ctrl

[Xterm](/index.php/Xterm "Xterm") supports moving between words with `Ctrl+Left` and `Ctrl+Right` [by default](http://stackoverflow.com/a/7783928). To achieve this effect with other terminal emulators, find the correct [terminal codes](http://wiki.bash-hackers.org/scripting/terminalcodes), and bind them to `backward-word` and `forward-word` in `~/.inputrc`. The codes can be made visible by first issuing the _cat_ command.

For example, for [urxvt](/index.php/Urxvt "Urxvt"):

 `~/.inputrc` 

```
"\eOd": backward-word
"\eOc": forward-word
```

### Mimic Zsh run-help ability

Zsh can invoke the manual for the written command pushing `Alt+h`. A similar behaviour is obtained in Bash by appending this line in your `inputrc` file:

 `/etc/inputrc` 

```
"\eh": "\C-a\eb\ed\C-y\e#man \C-y\C-m\C-p\C-p\C-a\C-d\C-e"

```

## Aliases

[alias](https://en.wikipedia.org/wiki/Alias_(command) "wikipedia:Alias (command)") is a command, which enables a replacement of a word with another string. It is often used for abbreviating a system command, or for adding default arguments to a regularly used command.

Personal aliases are preferably stored in `~/.bashrc`, and system-wide aliases (which affect all users) belong in `/etc/bash.bashrc`. See [[4]](https://gist.github.com/anonymous/a9055e30f97bd19645c2) and [Pacman tips#Shortcuts](/index.php/Pacman_tips#Shortcuts "Pacman tips") for example aliases.

For functions, see [Bash/Functions](/index.php/Bash/Functions "Bash/Functions").

## Tips and tricks

### Prompt customization

The Bash prompt is governed by the variable `$PS1`. To colorize the Bash prompt, use:

 `~/.bashrc` 

```
#PS1='[\u@\h \W]\$ '  # To leave the default one
#DO NOT USE RAW ESCAPES, USE TPUT
reset=$(tput sgr0)
red=$(tput setaf 1)
blue=$(tput setaf 4)
green=$(tput setaf 2)

PS1='\[$red\]\u\[$reset\] \[$blue\]\w\[$reset\] \[$red\]\$ \[$reset\]\[$green\] '
```

This `$PS1` is useful for a root Bash prompt, with red designation and green console text. The `\[` and `\[` should wrap non-printing characters sequences to avoid wrong estimation of PS1 size which leads to display issues when navigating through history and editing the command line. For more info, see: [Color Bash Prompt](/index.php/Color_Bash_Prompt "Color Bash Prompt").

#### Customize title

The `$PROMPT_COMMAND` variable allows you to execute a command before the prompt. For example, this will change the title to your full current working directory:

 `~/.bashrc` 

```
export PROMPT_COMMAND='echo -ne "\033]0;$PWD\007"'

```

This will change your title to the last command run, and make sure your history file is always up-to-date:

 `~/.bashrc` 

```
export HISTCONTROL=ignoreboth
export HISTIGNORE='history*'
export PROMPT_COMMAND='history -a;echo -en "\e]2;";history 1|sed "s/^[ \t]*[0-9]\{1,\}  //g";echo -en "\e\\";'

```

### Command-not-found (AUR)

[pkgfile](/index.php/Pkgfile "Pkgfile") includes a "command not found" hook that will automatically search the official repositories, when entering an unrecognized command. An alternative "command not found" hook is provided by [command-not-found](https://aur.archlinux.org/packages/command-not-found/)<sup><small>AUR</small></sup>. Usage example:

 `$ abiword` 

```
The command 'abiword' is been provided by the following packages:
**abiword** (2.8.6-7) from extra
	[ abiword ]
**abiword** (2.8.6-7) from staging
	[ abiword ]
**abiword** (2.8.6-7) from testing
	[ abiword ]

```

To load it automatically:

 `_~/.bashrc_ or _~/.zshrc_` 

```
[ -r /etc/profile.d/cnf.sh ] && . /etc/profile.d/cnf.sh

```

### Disable Ctrl+z in terminal

You can disable the `Ctrl+z` feature (pauses/closes your application) by wrapping your command like this:

```
#!/bin/bash
trap "" 20
_adom_

```

Now when you accidentally press `Ctrl+z` in [adom](https://aur.archlinux.org/packages/adom/)<sup><small>AUR</small></sup> instead of `Shift+z` nothing will happen because `Ctrl+z` will be ignored.

### Clear the screen after logging out

To clear the screen after logging out on a virtual terminal:

 `~/.bash_logout` 

```
clear
reset

```

### Auto "cd" when entering just a path

Bash can automatically prepend `cd` when entering just a path in the shell. For example:

 `$ /etc` 

```
bash: /etc: Is a directory

```

But after adding one line into `.bashrc` file:

 `~/.bashrc` 

```
...
shopt -s autocd
...

```

You get:

```
[user@host ~]$ /etc
cd /etc
[user@host etc]$

```

### Autojump

[autojump](https://www.archlinux.org/packages/?name=autojump) allows navigating the file system by searching for strings in a database with the user's most-visited paths.

After installation, `/etc/profile.d/autojump.bash` must be [sourced](/index.php/Source "Source") in order to start using the application.

## Troubleshooting

### Line wrap on window resize

When resizing a [terminal emulator](/index.php/Terminal_emulator "Terminal emulator"), Bash may not receive the resize signal. This will cause typed text to not wrap correctly and overlap the prompt. The `checkwinsize` shell option checks the window size after each command and, if necessary, updates the values of `LINES` and `COLUMNS`.

 `~/.bashrc` 

```
shopt -s checkwinsize

```

### Shell exits even if ignoreeof set

If you have set the `ignoreeof` option and you find that repeatedly hitting `ctrl-d` causes the shell to exit, it is because this option only allows 10 consecutive invocations of this keybinding (or 10 consecutive EOF characters, to be precise), before exiting the shell.

To allow higher values, you have to use the IGNOREEOF variable.

For example:

```
 export IGNOREEOF=100

```

## See also

*   [Bash Reference](https://www.gnu.org/software/bash/manual/bashref.html)
*   [Bash manual page](https://www.gnu.org/software/bash/manual/bash.html)
*   [Readline Init File Syntax](https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax.html)
*   [The Bourne-Again Shell](http://www.aosabook.org/en/bash.html) - The third chapter of _The Architecture of Open Source Applications_
*   [Shellcheck](http://shellcheck.net) - Check bash scripts for common errors

### Tutorials

*   [BashGuide on Greg's Wiki](http://mywiki.wooledge.org/BashGuide)
*   [BashFAQ on Greg's Wiki](http://mywiki.wooledge.org/BashFAQ)
*   [Bash Hackers Wiki](http://wiki.bash-hackers.org/doku.php)
*   [Advanced Bash Scripting Guide](http://tldp.org/LDP/abs/html/)
*   [Quote Tutorial](http://www.grymoire.com/Unix/Quote.html)

### Community

*   [An active and friendly IRC channel for Bash](irc://irc.freenode.net#bash)
*   [Bashscripts.org](http://bashscripts.org)

### Examples

*   [How to change the title of an xterm](http://tldp.org/HOWTO/Xterm-Title-4.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Bash&oldid=413121](https://wiki.archlinux.org/index.php?title=Bash&oldid=413121)"