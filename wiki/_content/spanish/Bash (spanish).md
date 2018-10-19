**Estado de la traducción**
Este artículo es una traducción de [Bash](/index.php/Bash "Bash"), revisada por última vez el **2018-10-18**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Bash&diff=0&oldid=542792) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Bash/Functions](/index.php/Bash/Functions "Bash/Functions")
*   [Bash/Prompt customization](/index.php/Bash/Prompt_customization "Bash/Prompt customization")
*   [Environment variables](/index.php/Environment_variables "Environment variables")
*   [Readline](/index.php/Readline "Readline")
*   [Fortune](/index.php/Fortune "Fortune")
*   [Pkgfile](/index.php/Pkgfile "Pkgfile")
*   [Command-line shell](/index.php/Command-line_shell "Command-line shell")

[Bash](https://www.gnu.org/software/bash/) (Bourne-again Shell) es un [intérprete de línea de órdenes](/index.php/Command-line_shell "Command-line shell")/lenguaje de programación por el [proyecto GNU](/index.php/GNU_Project_(Espa%C3%B1ol) "GNU Project (Español)"). Su nombre es un homenaje en referencia a su predecesor, el intérprete de línea de órdenes Bourne, que ha estado en desuso desde hace mucho tiempo. Bash se puede ejecutar en la mayoría de los sistemas operativos similares a UNIX, incluido GNU/Linux.

## Contents

*   [1 Invocación](#Invocaci.C3.B3n)
    *   [1.1 Archivos de configuración](#Archivos_de_configuraci.C3.B3n)
    *   [1.2 Shell and environment variables](#Shell_and_environment_variables)
*   [2 Command line](#Command_line)
    *   [2.1 Tab completion](#Tab_completion)
        *   [2.1.1 Single-tab](#Single-tab)
        *   [2.1.2 Common programs and options](#Common_programs_and_options)
        *   [2.1.3 Customize per-command](#Customize_per-command)
    *   [2.2 History](#History)
        *   [2.2.1 History completion](#History_completion)
        *   [2.2.2 Shorter history](#Shorter_history)
    *   [2.3 Mimic Zsh run-help ability](#Mimic_Zsh_run-help_ability)
*   [3 Alias](#Alias)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Prompt customization](#Prompt_customization)
    *   [4.2 Command not found](#Command_not_found)
    *   [4.3 Disable Ctrl+z in terminal](#Disable_Ctrl.2Bz_in_terminal)
    *   [4.4 Clear the screen after logging out](#Clear_the_screen_after_logging_out)
    *   [4.5 Auto "cd" when entering just a path](#Auto_.22cd.22_when_entering_just_a_path)
    *   [4.6 Autojump](#Autojump)
    *   [4.7 Prevent overwrite of files](#Prevent_overwrite_of_files)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Line wrap on window resize](#Line_wrap_on_window_resize)
    *   [5.2 Shell exits even if ignoreeof set](#Shell_exits_even_if_ignoreeof_set)
*   [6 See also](#See_also)
    *   [6.1 Tutorials](#Tutorials)
    *   [6.2 Community](#Community)
    *   [6.3 Examples](#Examples)

## Invocación

El comportamiento de Bash se puede alterar dependiendo de como se invoca. A continuación se describen distintos modos.

Si Bash es iniciado por `login` en un TTY, por un demonio [SSH](/index.php/SSH_(Espa%C3%B1ol) "SSH (Español)"), o por algo similar, se considera un **intérprete de línea de órdenes de inicio de sesión**. Este modo también se puede activar mediante la opción de línea de órdenes `-l`/`--login`.

Bash se considera un **intérprete de línea de órdenes interactivo** cuando su entrada estándar y de error están conectadas a un terminal (por ejemplo, cuando se ejecuta en un emulador de terminal), y no se inicia con la opción `-c` o con [argumentos no opcionales](http://unix.stackexchange.com/a/96805) (por ejemplo, `bash **script**`). Todos los intérpretes de línea de órdenes interactivos cargan `/etc/bash.bashrc` y `~/.bashrc`, mientras que los intérpretes de línea de órdenes interactivos de *inicio de sesion* también cargan `/etc/profile` y { {ic|~/.bash_profile}}.

**Nota:** En Arch `/bin/sh` (que solía ser el ejecutable del interprete de línea de órdenes Bourne) es un enlace simbólico a `/bin/bash`. Si Bash se invoca con el nombre `sh`, intenta imitar el comportamiento de inicio de las versiones históricas de `sh`, incluida la compatibilidad con POSIX.

### Archivos de configuración

Véase la sección "6.2 Archivos de inicio de Bash" en `/usr/share/doc/bash/bashref.html` ([enlace en línea](https://www.gnu.org/software/bash/manual/bash.html#Bash-Startup-Files)) y [GregsWiki:DotFiles](https://mywiki.wooledge.org/DotFiles "gregswiki:DotFiles") para una completa descripción.

| Archivo | Descripción | Intérprete de inicio de sesión  | Intérprete interactivo *sin inicio de sesión* |
| `/etc/profile` | [Carga](/index.php/Source_(Espa%C3%B1ol) "Source (Español)") las configuraciones de la aplicación en `/etc/profile.d/*.sh` y `/etc/bash.bashrc`. | Sí | No |
| `~/.bash_profile` | Por usuario, después de `/etc/profile`. Si este archivo no existe, `~/.bash_login` y `~/.profile` son comprobados en ese orden. El archivo de estructura `/etc/skel/.bash_profile` también carga `~/.bashrc`. | Sí | No |
| `~/.bash_logout` | Después de salir de un intérprete de línea de órdenes de incoo de sesión. | Sí | No |
| `/etc/bash.bashrc` | Depende de la opción de compilación `-DSYS_BASHRC="/etc/bash.bashrc"`. Carga `/usr/share/bash-completion/bash_completion`. | No | Sí |
| `~/.bashrc` | Por usuario, después de `/etc/bash.bashrc`. | No | Sí |

**Nota:**

*   Login shells can be non-interactive when called with the `--login` argument.
*   While interactive, *non-login* shells do **not** source `~/.bash_profile`, they still inherit the environment from their parent process (which may be a login shell). See [GregsWiki:ProcessManagement#On processes, environments and inheritance](https://mywiki.wooledge.org/ProcessManagement#On_processes.2C_environments_and_inheritance "gregswiki:ProcessManagement") for details.

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

Environment variables are conventionally placed in `~/.profile` or `/etc/profile` so that other Bourne-compatible shells can use them.

See [Environment variables](/index.php/Environment_variables "Environment variables") for more general information.

## Command line

Bash command line is managed by the separate library called [Readline](/index.php/Readline "Readline"). Readline provides [emacs](/index.php/Emacs "Emacs") and [vi](/index.php/Vi "Vi") styles of shortcuts for interacting with the command line, i.e. moving back and forth on the word basis, deleting words etc. It is also Readline's responsibility to manage [history](/index.php/Readline#History "Readline") of input commands. Last, but not least, it allows you to create [macros](/index.php/Readline#Macros "Readline").

### Tab completion

[Tab completion](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion") is the option to auto-complete typed commands by pressing `Tab` (enabled by default).

#### Single-tab

It may require up to three tab-presses to show all possible completions for a command. To reduce the needed number of tab-presses, see [Readline#Faster completion](/index.php/Readline#Faster_completion "Readline").

#### Common programs and options

By default, Bash only tab-completes commands, filenames, and variables. The package [bash-completion](https://www.archlinux.org/packages/?name=bash-completion) extends this by adding more specialized tab completions for common commands and their options, which can be enabled by sourcing `/usr/share/bash-completion/bash_completion`. With [bash-completion](https://www.archlinux.org/packages/?name=bash-completion), normal completions (such as `$ ls file.*<tab><tab>`) will behave differently; however, they can be re-enabled with `$ compopt -o bashdefault *program*` (see [[2]](https://bbs.archlinux.org/viewtopic.php?id=128471) and [[3]](https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins.html) for more detail).

#### Customize per-command

**Note:** Using the `complete` builtin may cause conflicts with [bash-completion](https://www.archlinux.org/packages/?name=bash-completion).

By default Bash only tab-completes file names following a command. You can change it to complete command names using `complete -c`:

 `~/.bashrc` 
```
complete -c man which

```

or complete command names and file names with `-cf`:

 `complete -cf sudo` 

See the Bash man page for more completion options.

### History

#### History completion

You can bind the up and down arrow keys to search through Bash's history (see: [Readline#History](/index.php/Readline#History "Readline") and [Readline Init File Syntax](https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax.html)):

 `~/.bashrc` 
```
 bind '"\e[A": history-search-backward'
 bind '"\e[B": history-search-forward'

```

or to affect all readline programs:

 `~/.inputrc` 
```
"\e[A": history-search-backward
"\e[B": history-search-forward

```

#### Shorter history

The `HISTCONTROL` variable can prevent certain commands from being logged to the history. For example, to stop logging of repeated identical commands

 `~/.bashrc`  `export HISTCONTROL=ignoredups` 

or set it to `erasedups` to ensure that Bash's history will only contain one copy of each command (regardless of order). See the Bash man page for more options.

### Mimic Zsh run-help ability

[Zsh](/index.php/Zsh "Zsh") can invoke the manual for the command preceding the cursor by pressing `Alt+h`. A similar behaviour is obtained in Bash using this [Readline](/index.php/Readline "Readline") bind:

 `~/.bashrc` 
```
bind '"\eh": "\C-a\eb\ed\C-y\e#man \C-y\C-m\C-p\C-p\C-a\C-d\C-e"'

```

This assumes are you using the (default) Emacs [editing mode](/index.php/Readline#Editing_mode "Readline").

## Alias

[alias](https://en.wikipedia.org/wiki/Alias_(command) is a command, which enables a replacement of a word with another string. It is often used for abbreviating a system command, or for adding default arguments to a regularly used command.

Personal aliases are preferably stored in `~/.bashrc`, and system-wide aliases (which affect all users) belong in `/etc/bash.bashrc`. See [[4]](https://gist.github.com/anonymous/a9055e30f97bd19645c2) for example aliases.

For functions, see [Bash/Functions](/index.php/Bash/Functions "Bash/Functions").

## Tips and tricks

### Prompt customization

See [Bash/Prompt customization](/index.php/Bash/Prompt_customization "Bash/Prompt customization").

### Command not found

[pkgfile](/index.php/Pkgfile "Pkgfile") includes a "command not found" hook that will automatically search the official repositories, when entering an unrecognized command.

You need to [source](/index.php/Source "Source") the hook to enable it, for example:

 `~/.bashrc`  `source /usr/share/doc/pkgfile/command-not-found.bash` 

Then attempting to run an unavailable command will show the following info:

 `$ abiword` 
```
abiword may be found in the following packages:
  extra/abiword 3.0.1-2	/usr/bin/abiword

```

**Note:** The pkgfile database may need to be updated before this will work. See [pkgfile#Installation](/index.php/Pkgfile#Installation "Pkgfile") for details.

An alternative "command not found" hook is provided by [command-not-found](https://aur.archlinux.org/packages/command-not-found/), which looks like this:

 `$ abiword` 
```
The command 'abiword' is provided by the following packages:
**abiword** (2.8.6-7) from extra
	[ abiword ]
**abiword** (2.8.6-7) from staging
	[ abiword ]
**abiword** (2.8.6-7) from testing
	[ abiword ]

```

### Disable Ctrl+z in terminal

You can disable the `Ctrl+z` feature (pauses/closes your application) by wrapping your command like this:

```
#!/bin/bash
trap "" 20
*adom*

```

Now when you accidentally press `Ctrl+z` in [adom](https://aur.archlinux.org/packages/adom/) instead of `Shift+z` nothing will happen because `Ctrl+z` will be ignored.

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

### Prevent overwrite of files

For the current session, to disallow existing regular files to be overwritten by redirection of shell output:

```
$ set -o noclobber

```

This is identical to `set -C`.

To make the changes persistent for your user:

 `~/.bashrc` 
```
...
set -o noclobber
```

To manually overwrite a file while `noclobber` is set:

```
$ echo "output" >| file.txt

```

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

*   [Wikipedia:Bash (Unix shell)](https://en.wikipedia.org/wiki/Bash_(Unix_shell) "wikipedia:Bash (Unix shell)")
*   [Bash Reference Manual](https://www.gnu.org/software/bash/manual/bashref.html), or `/usr/share/doc/bash/bashref.html`
*   [Readline Init File Syntax](https://www.gnu.org/software/bash/manual/html_node/Readline-Init-File-Syntax.html)
*   [The Bourne-Again Shell](http://www.aosabook.org/en/bash.html) - The third chapter of *The Architecture of Open Source Applications*
*   [Shellcheck](http://shellcheck.net) - Check bash scripts for common errors (based on [shellcheck](https://github.com/koalaman/shellcheck))
*   [PS1 generator](http://bashrcgenerator.com/) - generate your .bashrc/PS1 bash prompt with a drag and drop interface
*   [Even more useful .bashrc commands](https://serverfault.com/questions/3743/what-useful-things-can-one-add-to-ones-bashrc)

### Tutorials

*   [Greg's Wiki](https://mywiki.wooledge.org/ "gregswiki:")
*   [GregsWiki:BashGuide](https://mywiki.wooledge.org/BashGuide "gregswiki:BashGuide")
*   [GregsWiki:BashFAQ](https://mywiki.wooledge.org/BashFAQ "gregswiki:BashFAQ")
*   [Bash Hackers Wiki](http://wiki.bash-hackers.org/doku.php)
*   [Bash Hackers Wiki: List of Bash online tutorials](http://wiki.bash-hackers.org/scripting/tutoriallist)
*   [Quote Tutorial](http://www.grymoire.com/Unix/Quote.html)

### Community

*   [An active and friendly IRC channel for Bash](ircs://chat.freenode.net#bash)
*   [Bashscripts.org](http://bashscripts.org)

### Examples

*   [How to change the title of an xterm](http://tldp.org/HOWTO/Xterm-Title-4.html)